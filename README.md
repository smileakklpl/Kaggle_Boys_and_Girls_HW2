# Kaggle Boys and Girls HW2 Project

本專案旨在預測 Kaggle 競賽中的性別標籤。本版本以 `ensemble_ultimate_v4.ipynb` 為最終實作版本。

## 專案結構 (Project Structure)

```text
Kaggle_Boys_and_Girls_HW2/
├───data/                   # 原始資料集 (CSV)
├───src/                    # 原始程式碼 (.ipynb)
│   ├───ensemble.ipynb      # 基礎模型整合
│   ├───stacking_ultimate.ipynb # Stacking 基礎版本
│   └───ensemble_ultimate_v4.ipynb # 最終版本 (Blending + BGE-Large)
├───results/                # 輸出結果 (Submission files)
├───requirements.txt        # Python 相依套件列表
├───pyproject.toml          # 專案設定與套件管理
└───README.md               # 專案說明
```

## 檔案說明

- **`data/`**: 包含訓練集、測試集與樣品繳交檔案。
- **`src/ensemble_ultimate_v4.ipynb`**: **最終版本 (Ultimate Blending)**。
  - **技術核心**：採用「保守、中庸、激進」三種模型配置進行 Blending 融合。
  - **特徵優化**：使用 BGE-Large v1.5 NLP 嵌入、投票制 Permutation Importance 特徵篩選。
  - **數據工程**：自動 BMI 計算、Log 轉換，並嚴格執行 CV 內部預處理以防止資料洩漏。
- **`src/stacking_ultimate.ipynb`**: 基礎 Stacking 版本，包含特徵工程與 Optuna 參數優化。
- **`results/`**: 執行程式後產出的預測 CSV 檔案（如 `submission_blending_ultimate.csv`）。

## 安裝與執行 (Installation & Execution)

### 安裝相依套件
請確保您的環境中已安裝 Python 3.9+，接著執行：
```bash
pip install -r requirements.txt
```

### 執行程式
您可以使用 Jupyter Notebook 或 VS Code 打開 `src/ensemble_ultimate_v4.ipynb` 並執行所有儲存格。預測結果會自動儲存在 `results/` 資料夾中。

## 套件依賴 (Dependencies)
- `pandas`
- `numpy`
- `scikit-learn`
- `xgboost`
- `lightgbm`
- `category-encoders`
- `sentence-transformers` (使用 BGE-Large 模型)
- `matplotlib`
- `ipykernel` (執行 Jupyter Notebook 必備)
