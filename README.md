
# Energy Consumption Forecasting with XGBoost

## Overview
A machine learning pipeline that predicts next-hour household energy consumption using the UCI Household Power Consumption dataset, enhanced with Nigeria-specific power source features.

## Dataset
- **Source:** UCI Household Power Consumption (`household_power_consumption.txt`)
- **Period:** December 2006 – November 2010
- **Granularity:** Minute-level → resampled to hourly

## Pipeline Summary

| Step | Description |
|------|-------------|
| 1 | Load raw data, handle `?` missing values |
| 2 | Create datetime index |
| 3 | Forward-fill remaining nulls |
| 4 | Resample minute-level data to hourly means |
| 5 | Engineer time features (hour, day, month, weekend, daytime) |
| 6 | Add Nigeria-specific power source features (grid, solar, generator) |
| 7 | Add lag features (1h, 24h, 168h) |
| 8 | Add rolling statistics (24h mean & std) |
| 9 | Define target variable (next hour's consumption) |
| 10 | Temporal train/val/test split (80/10/10) |
| 11–12 | Train & evaluate XGBoost model |

## Results

| Split | MAE | RMSE | MAPE |
|-------|-----|------|------|
| Validation | 0.3227 kW | 0.4688 kW | 38.6% |
| Test | 0.3105 kW | 0.4471 kW | 47.6% |

## Key Features by Importance
`Global_intensity` → `gen_active` → `grid_available` → `is_daytime`

## Requirements
```
pandas, numpy, xgboost, scikit-learn, matplotlib, joblib
```
