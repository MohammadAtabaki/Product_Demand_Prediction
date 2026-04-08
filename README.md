## 📦 Forecasting product demand to optimize order planning

This Machine Learning project is dedicated to building a robust time-series forecasting model of **weekly product demand** in retail store. Based on historical sales data, the project focuses on analyzing the dependencies of several data points between themselves, taking into account trend and seasonal changes as well as studying and applying various machine learning algorithms.

The project had two **main tasks**:
1) Development a deep model and make forecast for the next 8 weeks;
2) Calculation of the optimal order volume for a given period, taking into account the probabilistic scenarios (forecast and confidence intervals) and cost of expenses (price per unit, storage cost, order cost, penalty of lost demand)

Applyed predictive modeling techniques:
- **ARIMA** - a classical statistical approach for univariate time series;
- **SARIMA** - seasonal Arima model;
- **XGBoost** - an efficient gradient boosting framework for machine learning;
- **Random Forest** - a machine learning model using lagged features and recursive prediction.

The dataset for the project was taken from the Kaggle platform. The code to download it is provided in the script file.
Models were trained under different seasonality assumptions (zero and 72‑week seasonal cycle) obtained after decomposition.

---

## 📁 Repository Structure
```
ml-demand-driven-order-planning/
├── product_demand_prediction.ipynb            # Python notebook of scripts
├── figures/                                   # Forecast plots and evaluation charts
├── Report/                                    # File with report in IEEE format and presentation
│ ├── Product_Demand_Forecasting_Presentation
│ └── Product_Demand_Forecasting_Report
├── .gitattributes
├── .gitignore
├── .python-version
├── requirements.txt
└── README.md
```

## 🗎 Project Structure

All code and modeling steps are contained in a single file - `product_demand_forecasting.ipynb`. It includes data loading, feature engineering, modeling, evaluation, forecasting, and calculation of the optimal order volume.
```
product_demand_forecasting.ipynb/
├── Import libraries
├── Data Import
├── First acquaintance with data
│ ├── The center description
│ └── The meal description
├── Data Preprocessing
│ ├── Data cleaning
│ ├── Detecting Outliers
│ ├── Correlational analysis
│ ├── Handling Outliers
│ ├── Seasonal–Trend Decomposition
│ └── Stationarity Check and Column Engineering
├── Modeling  
│ ├── Metrics functions
│ ├── Model creation
│   ├── ARIMA
│   ├── SARIMA
│   ├── Xgboost
│   └── Random Forest
├── Evaluation of predictions
├── Forecast
└── Calculation of the optimal order volume
```

---

## 📊 Results & Report

The metrics used to evaluate the accurancy of models are:
- _MSE_ - Mean Squared Error is computed as the average of the squared errors;
- _RMSE_ - Root Mean Squared Error is the square root of the Mean Squared Error;
- _MAPE_ - Mean Absolute Percent Error is computed by taking the error for each prediction, divided by the actual value

| Model                     | MSE        | RMSE   | MAPE |
|---------------------------|------------|--------|------|
| ARIMA                     | 118 223.96 | 343.84 | 0.1  |
| SARIMA                    | 118 223.96 | 343.84 | 0.1  |
| **XGBoost nonseasonal**   |  43 286.78 | 208.05 | 0.06 |
| XGBoost seasonal          | 175 164.23 | 418.53 | 0.15 |
| Random Forest nonseasonal | 174 710.91 | 417.98 | 0.12 |
| Random Forest seasonal	| 174 710.91 | 417.98 | 0.12 |

For the fisrt part of project, we got:
1. The non‑seasonal XGBoost model achieved the lowest error and was used for the final 8‑week demand forecast;
2. Forecast visualized with 95 % confidence intervals;
3. The forecast of the future order level does not look quite plausible - peaks not met increase decrease in demand. This may be due to the fact that for the trained model of XGBoost, the main important feature was _exponential smoothing_, which is done based on current values, which in this particular case were unknown. 
4. Also possible reasons are the complex behavior of the initial data, namely a _Random walk_.  

For the second part:
1. Five scenarios for customer demand manifestation were identified (upper confidence interval, upper middle ci, forecast, lower middle ci, lower ci);
2. Functions for calculating net profit and maximum profit have been developed taking into account the given order volume and probabilistic scenario;
3. The retail center will have a profit with any order size of the product, covering the minimum demand. It will receive the maximum profit with an order volume of 24 241 units of the beverage, and the profit will be equal to 28 625 euros.

## 📈 Future Work
As an improvement in the forecast in the future, we can:
- improve the current models, for example, changing the method for finding superparameters for XgBoost and Random Forest using **Grid / Bayes search** instead Random search;
- look at other forecasting models, namely for ML this is **SVR**, or for DL this is **TCN**, **LSTM**, Facebook's **Prophet**

Making the final choice about the order volume, we should add additional data about:
- volume of the warehouse / volume of the room allocated for this product;
- how much product fits on one pallet (basically, the price of storage in the warehouse is set per pallet);
- minimum and maximum order size (how much the supplier is ready to provide);
- market condition - market supply with this product.

---

## License
This project is licensed under the GPL-3.0 License
