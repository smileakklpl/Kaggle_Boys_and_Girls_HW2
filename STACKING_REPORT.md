# Kaggle Boys and Girls 性別預測實驗報告 (Ultimate Blending v4)

本報告詳述了針對 Kaggle 性別預測競賽開發的 **Ultimate Blending + Stacking** 終極模型。本版本核心在於引入了「多樣性融合策略」與「嚴格防洩漏預處理」。

---

## 1. 實驗流程 (Experimental Process)

本實驗採用的生產線確保了訓練集資訊絕不流向驗證集（Zero Data Leakage）：

1.  **精準資料清洗與動態邊界**：
    *   **OS 歸一化**：清理 `phone_os` 中的噪音值（Apple/Android/Other）。
    *   **99% 分位數防禦**：針對 `yt` (YouTube 觀看時間) 等長尾分佈，動態計算 99 百分位數作為上限，防止異常值破壞模型穩定性。
    *   **物理邊界強化**：對身高、體重、IQ 等欄位設定生理極限區間。

2.  **NLP 深層語意嵌入 (BGE-Large)**：
    *   使用目前頂尖的 **BGE-Large-v1.5** 模型處理 `self_intro`。
    *   **純淨版處理**：移除 Prefix 標籤，保留最原始的語意空間。

3.  **嚴格防洩漏預處理 (CV-Internal Preprocessing)**：
    *   **Target Encoding**、**PCA 降維 (5維)** 以及 **RF 迭代補值** 全部移入交叉驗證的 Fold 內部執行。確保 Imputer 與 Encoder 只學習 Training Fold 的分佈。

4.  **多次投票制特徵淘汰 (Permutation Importance Voting)**：
    *   使用 5 個不同隨機種子進行排列重要性計算。
    *   **決策規則**：只有在至少 3 輪中被判定為正貢獻的特徵才會保留，以此篩選出真正的核心特徵。

5.  **三檔位融合策略 (Three-tier Blending)**：
    *   同時訓練「保守」、「中庸」、「激進」三組性格迥異的模型，透過機率平均（Soft Voting）來中和單一模型的過擬合風險。

---

## 2. 模型參數說明 (Model Parameters)

本模型採用三層次的參數配置，以應對資料中不同的非線性特徵：

| 檔位 (Tier) | XGBoost (max_depth / learning_rate) | LightGBM (num_leaves / learning_rate) | Random Forest (max_depth) | 目的 |
| :--- | :--- | :--- | :--- | :--- |
| **Conservative (保守)** | 3 / 0.05 | 15 / 0.05 | 4 | 建立穩定基準，防止雜訊干擾。 |
| **Moderate (中庸)** | 5 / 0.03 | 31 / 0.03 | 6 | 捕捉特徵間的中度互動。 |
| **Aggressive (激進)** | 7 / 0.01 | 63 / 0.01 | 8 | 深層挖掘複雜模式。 |

*   **Meta-Model**: 所有檔位均使用 `Logistic Regression` 作為元學習器（Stacking），並最後進行 Blending 融合。

---

## 3. 核心模型特色

*   **多樣性融合 (Ensemble Diversity)**：透過三種不同複雜度的參數組合，讓模型在「偏誤 (Bias)」與「變異 (Variance)」之間取得完美平衡。
*   **BGE-Large 語意空間**：相較於傳統 Word2Vec，BGE 模型能捕捉到「描述自我」時細微的性別語意差異。
*   **RF 迭代補值 (Iterative Imputer)**：不使用簡單的中位數填補，而是利用隨機森林學習特徵間的關聯來預測缺失值。
*   **動態特徵工程**：自動計算 BMI 與身高體重比，並對高度偏態特徵進行 $Log(1+p)$ 轉換。

---

## 4. 實驗結果評估 (10-Fold CV)

根據 `ensemble_ultimate_v4.ipynb` 的最新運行結果，模型表現如下：

*   **準確率 (Accuracy)**: **0.8792** (std: 0.0559)
*   **排序力 (ROC-AUC)**: **0.9215** (std: 0.0750)
*   **平衡度 (F1-Score)**: **0.7841** (std: 0.0908)
*   **誤差值 (Log Loss)**: **0.3868** (std: 0.1163)
