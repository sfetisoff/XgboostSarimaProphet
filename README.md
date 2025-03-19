# Xgboost vs SARIMA vs Prophet

A comparison of machine learning and time series forecasting models for predicting electricity consumption.

Data: [Hourly Energy Consumption (Kaggle)](https://www.kaggle.com/datasets/robikscube/hourly-energy-consumption)

---

## Project Overview

This project compares three approaches to time series forecasting:
- **Xgboost**: Gradient boosting with various feature sets and forecasting horizons.
- **SARIMA**: A classic time series model accounting for seasonality.
- **Prophet**: Facebook’s tool for forecasting with trends and seasonality.

Additionally, three baseline models are used for comparison:
- **Mean**: Average value across the dataset.
- **Naive (h=1)**: Previous value as the forecast for tomorrow.
- **Week Ago**: Value from the same day of the week, one week prior.

---

## Models and Features

### Xgboost
1. **Simple Xgboost**  
   - Forecasts for any horizon.  
   - Features:  
     - Day of year  
     - Day of week  
     - Quarter  
     - Month  
     - Year  
     - Week of year  

2. **Xgboost with Lags (h=1, h=3, h=7)**  
   - Adds 7 lags to the base features.  
   - Forecasting horizons: 1, 3, and 7 days.

### SARIMA
- Seasonal ARIMA model with a recursive strategy.  
- Accounts for both seasonal and non-seasonal components.  
- Horizons: 1, 3, and 7 days.

### Prophet
- Facebook’s Prophet model.  
- Considers trends, seasonality, and anomalous days.  
- Horizons: 1, 3, and 7 days.

---

## Results

### Baseline Models (Dummy Forecast)
| Model       | MAE          | RMSE         |
|-------------|--------------|--------------|
| Mean        | 41865.49     | 49643.85     |
| Naive (h=1) | 18651.22     | 24426.22     |
| Week Ago    | 32056.83     | 41803.93     |

### Xgboost
| Model             | MAE          | RMSE         |
|-------------------|--------------|--------------|
| Simple XGB        | 30970.17     | 37263.02     |
| XGB (h=1)         | 15779.46     | 19756.25     |
| XGB (h=3)         | 27142.49     | 34184.66     |
| XGB (h=7)         | 28499.39     | 35512.29     |

### SARIMA
| Model        | MAE          | RMSE         |
|--------------|--------------|--------------|
| SARIMA (h=1) | 13441.56     | 17741.46     |
| SARIMA (h=3) | 24561.76     | 32010.47     |
| SARIMA (h=7) | 28125.31     | 35802.78     |

### Prophet
| Model         | MAE          | RMSE         |
|---------------|--------------|--------------|
| Prophet (h=1) | 25686.60     | 33679.69     |
| Prophet (h=3) | 26002.26     | 34074.73     |
| Prophet (h=7) | 26363.79     | 34484.40     |

---

## Model Comparison by Horizon

### Horizon = 1 Day
| Model         | MAE          | RMSE         |
|---------------|--------------|--------------|
| SARIMA        | **13441.56** | **17741.46** |
| XGB           | 15779.46     | 19756.25     |
| Naive         | 18651.22     | 24426.22     |
| Prophet       | 25686.60     | 33679.69     |
| Simple XGB    | 30970.17     | 37263.02     |

**Conclusion**: SARIMA excels due to precise autoregression on short horizons.

### Horizon = 3 Days
| Model         | MAE          | RMSE         |
|---------------|--------------|--------------|
| SARIMA        | **24561.76** | **32010.47** |
| Prophet       | 26002.26     | 34074.73     |
| XGB           | 27142.49     | 34184.66     |
| Simple XGB    | 30970.17     | 37263.02     |

**Conclusion**: SARIMA again delivers the best results.

### Horizon = 7 Days
| Model         | MAE          | RMSE         |
|---------------|--------------|--------------|
| Prophet       | **26363.79** | **34484.40** |
| SARIMA        | 28125.31     | 35802.78     |
| XGB           | 28499.39     | 35512.29     |
| Simple XGB    | 30970.17     | 37263.02     |
| Week Ago      | 32056.83     | 41803.93     |

**Conclusion**: Prophet outperforms due to its focus on trends and seasonality.

---

## Conclusions
- **SARIMA**: Best accuracy on short horizons (1 and 3 days).
- **Prophet**: Optimal for longer horizons (7 days).
- **Xgboost with Lags**: Consistently strong performance across all horizons, closely competing with SARIMA and Prophet.
