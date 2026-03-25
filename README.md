# Kaggle Boys and Girls HW2 Project

本專案旨在預測 Kaggle 競賽中的性別標籤。本版本以 `stacking_ultimate.ipynb` 為最終實作版本。

## 專案結構 (Project Structure)

```text
Kaggle_Boys_and_Girls_HW2/
├───data/                   # 原始資料集 (CSV)
├───src/                    # 原始程式碼 (.ipynb 或 .py)
│   ├───ensemble.ipynb      # 基礎模型整合
│   └───stacking_ultimate.ipynb # 最終版本 (Stacking + Optuna)
├───results/                # 輸出結果 (Submission files)
├───requirements.txt        # Python 相依套件列表
├───pyproject.toml          # 專案設定與套件管理
└───README.md               # 專案說明
```

## 檔案說明

- **`data/`**: 包含訓練集、測試集與樣品繳交檔案。
- **`src/stacking_ultimate.ipynb`**: **最終版本**。包含進階特徵工程 (BMI, 衍生比例)、BGE-Large 語意嵌入 (NLP)、Permutation Importance 特徵篩選、Optuna 自動參數優化與 Stacking 模型整合 (XGBoost, LightGBM, Random Forest)。
- **`results/`**: 執行程式後產出的預測 CSV 檔案（如 `submission_ultimate.csv`）。

## 安裝與執行 (Installation & Execution)

### 安裝相依套件
請確保您的環境中已安裝 Python 3.9+，接著執行：
```bash
pip install -r requirements.txt
```

### 執行程式
您可以使用 Jupyter Notebook 或 VS Code 打開 `src/stacking_ultimate.ipynb` 並執行所有儲存格。預測結果會自動儲存在 `results/` 資料夾中。

## 套件依賴 (Dependencies)
- `pandas`
- `numpy`
- `scikit-learn`
- `xgboost`
- `lightgbm`
- `category-encoders`
- `sentence-transformers` (使用 BGE-Large 模型)
- `optuna` (參數優化)
- `matplotlib`
- `ipykernel` (執行 Jupyter Notebook 必備)
