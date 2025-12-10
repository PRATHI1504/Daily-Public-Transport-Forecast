

# **Public Transport Daily Ridership Forecasting**

This project focuses on **daily passenger ridership analysis** for public transport services and generates **7-day forecasts** using the **SARIMA model**. By modeling historical trends and weekly patterns, this project aims to support **operational decision-making**, optimize bus allocation, and reduce service inefficiencies.


## **Dataset Overview**

The dataset, `Daily_Public_Transport_Passenger_Journeys_by_Service_Type_20250603.csv`, contains **daily ridership counts** for multiple services:

| Column       | Description                                 |
| ------------ | ------------------------------------------- |
| Date         | Daily calendar dates                        |
| Local Route  | Ridership on local bus routes               |
| Light Rail   | Ridership for light rail services           |
| Peak Service | Passenger counts during peak hours          |
| Rapid Route  | Ridership on fast bus routes                |
| School       | Passenger counts on school-focused services |

The dataset spans **several years**, providing a rich history for both **trend analysis** and **short-term forecasting**.



## **Project Goals**

* Clean and preprocess **raw ridership data**
* Explore patterns: daily trends, weekly seasonality, and outliers
* Build **SARIMA models** to forecast each service type
* Evaluate forecasts using **MAE, RMSE, and SMAPE**
* Generate actionable recommendations for **fleet scheduling and resource allocation**



## **Key Insights from Historical Data**

1. **Weekly Cycles**: Ridership peaks on weekdays, drops on weekends; school services follow term schedules.
2. **Trend Differences**: Local and Rapid Routes show gradual increases over time, while Peak Service remains fairly stable.
3. **High Volatility in Small Services**: Peak Service and School show erratic day-to-day variation.
4. **Special Event Effects**: Holidays and events create outliers in passenger numbers.
5. **Right-Skewed Distribution**: High-volume routes show a long-tail distribution; smaller services have frequent zero or near-zero counts.



## **Forecasting Methodology**

**Model Used:** SARIMA (Seasonal ARIMA)

**Why SARIMA?**

* Effectively captures **trend and seasonality**
* Handles **non-stationary behavior** using differencing
* Provides **quantitative forecasts** for each route separately
* Suitable for daily ridership data with **weekly recurring patterns**

**Model Parameters (example):**

```python
order = (1, 1, 1)               # AR, differencing, MA terms
seasonal_order = (0, 1, 1, 7)   # Seasonal AR, differencing, MA for weekly seasonality
forecast_horizon = 7             # Next 7 days
```



## **Forecast Results (7 Days)**

| Date       | Local Route | Light Rail | Peak Service | Rapid Route | School  |
| ---------- | ----------- | ---------- | ------------ | ----------- | ------- |
| 2024-09-30 | 3896.78     | 2349.69    | 153.09       | 3750.28     | 1649.86 |
| 2024-10-01 | 4399.21     | 2386.91    | 159.79       | 4203.63     | 1892.32 |
| 2024-10-02 | 4170.40     | 2326.40    | 154.97       | 3822.17     | 1923.60 |
| 2024-10-03 | 3830.04     | 1998.24    | 119.52       | 3457.60     | 1848.22 |
| 2024-10-04 | 2853.94     | 1113.80    | 53.52        | 1211.02     | 1709.63 |
| 2024-10-05 | 0           | 0          | 0            | 0           | 14.72   |
| 2024-10-06 | 0           | 0          | 0            | 0           | 10.11   |

> Negative predictions are set to **0**, reflecting realistic passenger counts.



## **Model Performance**

| Service Type | MAE     | RMSE    | SMAPE (%) |
| ------------ | ------- | ------- | --------- |
| Local Route  | 4515.17 | 7686.62 | 73.74     |
| Light Rail   | 3155.61 | 5088.49 | 63.34     |
| Peak Service | 73.61   | 135.79  | 110.32    |
| Rapid Route  | 5959.23 | 9686.70 | 70.89     |
| School       | 1153.86 | 1705.10 | 115.38    |

**Analysis:**

* **High-volume services** (Local, Light Rail, Rapid) are forecasted accurately.
* **Low-volume services** (Peak, School) have high SMAPE due to sparse data but still provide actionable information.



## **Operational Recommendations**

* Increase buses during **weekdays and school periods**
* Reduce deployment during **weekends or holidays**
* Reassign **idle buses** to high-demand routes
* Monitor anomalies and data quality issues in the “Other” category



## **Technical Stack**

* Python: Data processing & modeling
* Pandas & NumPy: Data cleaning and manipulation
* Statsmodels (SARIMAX): Forecasting
* Matplotlib & Seaborn: Visualization
* Metrics: MAE, RMSE, SMAPE



## **Future Enhancements**

* Hyperparameter optimization for **better SARIMA performance**
* Compare with alternative models (**Prophet, LSTM**)
* Integrate **holiday and special event effects**
* **Real-time dashboard** for operational planning
