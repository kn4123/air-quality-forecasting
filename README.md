# Air Quality Forecasting

Time-series forecasting of next-hour carbon monoxide (CO) concentration using Python and machine learning.

> **Project type:** Academic coursework / practical exercise  
> **Status:** Notebook prepared; reproduce the results by running it from top to bottom.

## Overview

This project explores the UCI Air Quality dataset and builds one-hour-ahead forecasts for the `CO(GT)` variable. The workflow covers exploratory data analysis, missing-value handling, time-based feature engineering, baseline forecasting, model training, and time-series evaluation.

## Dataset

- **Source:** [UCI Machine Learning Repository – Air Quality](https://archive.ics.uci.edu/dataset/360/air+quality)
- **Observations:** 9,357 hourly records
- **Target:** CO concentration one hour ahead
- Missing sensor readings encoded as `-200` are treated as missing values.

The dataset is not included in this repository. The notebook retrieves it from UCI using `ucimlrepo`.

## Methods

### Exploratory analysis and preprocessing
- Inspect missing values and variable distributions.
- Analyze hourly patterns, correlations, and time-series behavior.
- Preserve chronological order during preprocessing and evaluation.
- Do not impute the target variable.

### Feature engineering
- Calendar and cyclical time features.
- Lag features and rolling-window statistics.
- Sensor and weather measurements.

### Forecasting methods
- Persistence baseline.
- Seasonal Naive (24-hour) baseline.
- Hourly Mean baseline.
- Ridge Regression.
- Random Forest Regressor.

### Evaluation
- 5-fold expanding-window `TimeSeriesSplit`.
- A 14-day chronological holdout period.
- MAE, RMSE, R², sMAPE, and MASE.
- Residual diagnostics and Random Forest feature importance.

## Results

In the current notebook results, Random Forest performed best among the evaluated models:

| Evaluation | Model | MAE | RMSE | R² |
|---|---|---:|---:|---:|
| Time-series CV (mean) | Random Forest | 0.494 | 0.716 | 0.727 |
| Holdout | Random Forest | 0.334 | 0.484 | 0.862 |
| Holdout | Ridge Regression | 0.391 | — | 0.787 |

Holdout metrics are calculated only on timestamps with valid target values. Results may vary with library versions or changes to the notebook.

## Repository structure

```text
air-quality-forecasting/
├── Air_Quality_Forecasting_v2.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

## Run locally

1. Clone the repository:
   ```bash
   git clone https://github.com/kn4123/air-quality-forecasting.git
   cd air-quality-forecasting
   ```

2. Create and activate a virtual environment (recommended).

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Start Jupyter:
   ```bash
   jupyter notebook
   ```

5. Open `Air_Quality_Forecasting_v2.ipynb` and run all cells from top to bottom. An internet connection is required to retrieve the dataset from UCI.

## Notes

This is an academic exercise focused on applying time-series forecasting concepts. The results should be interpreted within the scope of this dataset and chronological split; they do not establish that one model is universally superior.
