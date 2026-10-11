# 🏢 Short-Term Energy Forecasting in Smart Buildings

Implementation of the methodology from the research paper:
> **"A Novel Approach for Short-Term Energy Forecasting in Smart Buildings"**  
> *M. Jayashankara, Priyansh Shah, Anshul Sharma, Prasenjit Chanak, and Sanjay Kumar Singh*  
> **IEEE Sensors Journal**, Vol. 23, No. 5, March 1, 2023. DOI: [10.1109/JSEN.2023.3237876](https://doi.org/10.1109/JSEN.2023.3237876)

---

## 📌 Project Overview
This repository implements a modular, reproducible deep learning framework for hourly building load forecasting using the **CU-BEMS** dataset (Chulalongkorn University Building Energy Management System). It evaluates:

* **Proposed Hybrid Models**:
  * **1D-CNN + LSTM** (1D Convolutional Neural Network followed by Long Short-Term Memory)
  * **1D-CNN + GRU** (1D Convolutional Neural Network followed by Gated Recurrent Unit) — *Top performer with 97% accuracy ($R^2 = 0.97$)*
* **Standalone Deep Learning Baselines**:
  * Standalone **LSTM**
  * Standalone **GRU**
* **Statistical & Machine Learning Baselines**:
  * **ARIMA(8, 0, 8)**
  * **Linear Regression**
* **Forecasting Scenarios**:
  * **Scenario 1 (Univariate)**: Energy load lag only ($t-2, t-4, t-8, t-10$).
  * **Scenario 2 (Multivariate)**: Energy load lag + **Hour of Day** (0–23) + **Day Type** (0–6).

---

## 📁 Directory Structure

```
Dataset/
├── configs/
│   └── config.yaml             # Hyperparameters, lag lengths & training configs
├── data/
│   ├── raw/                    # Raw CU-BEMS 1-minute interval data (not tracked)
│   └── processed/              # Resampled hourly, imputed & normalized data
├── notebooks/                  # Interactive exploration and visual analysis
├── results/
│   ├── figures/                # Actual vs Predicted plots, loss curves
│   └── metrics/                # Benchmark tables (MAE, RMSE, R² across lags)
├── saved_models/               # Serialized model checkpoints (.pt)
├── src/
│   ├── data/                   # Data loader, resampling, imputation & lag sequencing
│   ├── models/                 # PyTorch architectures (CNN-LSTM, CNN-GRU, LSTM, GRU, ARIMA, LR)
│   ├── training/               # Training engine, Adam optimizer, MAE loss
│   ├── evaluation/             # Metrics calculation (MAE, RMSE, R²) and plotting
│   └── utils/                  # Reproducibility seeding, config parser, logger
├── tests/                      # Unit tests for data preprocessing and tensor pipelines
├── requirements.txt            # Python package dependencies
├── .gitignore                  # Git exclusions for datasets and binaries
└── README.md                   # Project documentation
```

---

## ⚙️ Quick Start

### 1. Installation
```bash
pip install -r requirements.txt
```

### 2. Experimental Pipeline
1. **Preprocess CU-BEMS data**: Resample 1-minute to 1-hour interval, apply linear forward-fill imputation, and perform Z-score standardization.
2. **Train Models**: Execute training for both Univariate (Scenario 1) and Multivariate (Scenario 2) configurations across lag windows ($2\text{h}, 4\text{h}, 8\text{h}, 10\text{h}$).
3. **Evaluate**: Compute MAE, RMSE, and $R^2$ scores and generate comparison figures.
