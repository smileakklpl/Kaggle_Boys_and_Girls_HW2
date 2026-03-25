# Kaggle Boys and Girls HW2 Project

本專案旨在預測 Kaggle 競賽中的性別標籤。

## 專案結構 (Project Structure)

```text
C:\Users\USER\OneDrive\Desktop\常用\研究所\課程\1142\機器學習\Kaggle_Boys_and_Girls_HW2\
├───data/                   # 原始資料集 (CSV)
├───src/                    # 原始程式碼 (.ipynb 或 .py)
├───results/                # 輸出結果 (Submission files)
├───requirements.txt        # Python 相依套件列表
├───pyproject.toml          # 專案設定與套件管理
└───README.md               # 專案說明
```

## 檔案說明

- **`data/`**: 包含訓練集、測試集與樣品繳交檔案。
- **`src/ensemble.ipynb`**: 主要的機器學習實作，包含特徵工程、缺失值補值、模型整合 (XGBoost, LightGBM, Random Forest) 與預測。
- **`results/`**: 執行程式後產出的預測 CSV 檔案。

## 安裝與執行 (Installation & Execution)

### 安裝相依套件
請確保您的環境中已安裝 Python 與 pip，接著執行：
```bash
pip install -r requirements.txt
```

### 執行程式
您可以使用 Jupyter Notebook 或 VS Code 打開 `src/ensemble.ipynb` 並執行所有儲存格。預測結果會自動儲存在 `results/` 資料夾中。

## 套件依賴 (Dependencies)
- `pandas`
- `numpy`
- `scikit-learn`
- `xgboost`
- `lightgbm`
- `ipykernel` (執行 Jupyter Notebook 必備)
