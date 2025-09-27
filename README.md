Energy Load Forecasting and Weather Analysis (Sardinia, 2020-2024)

This project analyzes electricity consumption in Sardinia from 2020 to 2024 and investigates the relationship between weather conditions and load. It also includes forecast error analysis and preparation for predictive modeling using LightGBM.

Project Overview

The goal of this project is to:

Explore electricity consumption patterns in Sardinia (2020-2024).

Analyze forecast accuracy and identify error trends by hour, weekday, month, and season.

Merge weather data from Meteostat with load data to evaluate weather impact on electricity demand.

Prepare features for a predictive model for total load forecasting using LightGBM.

Data
Electricity Load Data

Source: https://dati.terna.it

Columns include:

Date

Total Load [MW]

Forecast Total Load [MW]

Bidding Zone

Weather Data

Source: Meteostat hourly weather data for Cagliari, Sardinia

Columns include:

temperature, dew_point, humidity, precipitation, wind_direction, wind_speed, wind_gust, pressure, sunshine, weather_code

Data Cleaning and Preprocessing

Combined data from 2020 to 2024.

Removed rows with missing values.

Converted Date column to datetime and set as index.

Created additional time-based features: Year, Month, Day, Weekday, Hour, Minute, Season.

Calculated forecast errors:

Error = Forecast Load - Total Load

Absolute Error and Percentage Error

Resampled weather data to match 15-minute frequency.

Filled missing weather data:

precipitation missing → filled with 0

sunshine missing → forward fill

Dropped snow column (mostly missing)

Feature Engineering

Created lag features for load: load_lag1, load_lag2, load_lag3.

Mapped Month to Season.

Renamed weather columns for clarity:

temp → temperature

dwpt → dew_point

rhum → humidity

prcp → precipitation

wdir → wind_direction

wspd → wind_speed

wpgt → wind_gust

pres → pressure

tsun → sunshine

coco → weather_code

Exploratory Data Analysis (EDA)

Forecast error analysis: calculated MAE, RMSE, MAPE.

Error trends:

By hour of day

By weekday

By month

By season

Load patterns:

Hourly, weekly, and monthly average loads

Weather correlation: scatter plots and heatmap between load and weather variables.

Daily maximum load: time series visualization.

Modeling

Target: total_load

Features:

Time features: Hour, Weekday, Month, Season

Weather features: temperature, dew_point, humidity, precipitation, wind_direction, wind_speed, wind_gust, pressure, sunshine, weather_code

Lag features: load_lag1, load_lag2, load_lag3

Forecasted load: forecast_load

Split: 80% training, 20% testing.

Model: LightGBM Regressor (LGBMRegressor)

Results

Forecast evaluation metrics:

MAE: 21.41 MW

RMSE: 28.14 MW

MAPE: 2.15%

Hourly, seasonal, and monthly error trends indicate higher forecast errors during summer afternoons and winter mornings.

Visualizations

Time series of total vs forecast load (2020–2024)

Load distribution and error distribution histograms

Boxplots of forecast error by season

Correlation heatmap of load vs weather variables

Scatterplots of total load vs temperature, humidity, precipitation, wind speed

Daily maximum load time series

Hourly and weekly average load line/bar plots

How to Run

Clone the repository:

git clone https://github.com/yourusername/energy-load-forecasting.git
cd energy-load-forecasting


Install dependencies:

pip install -r requirements.txt


or manually:

pip install pandas numpy matplotlib seaborn scikit-learn lightgbm meteostat


Place the energy Excel files (Energy consumption 2020.xlsx … 2024.xlsx) in the data/ folder.

Run the notebook:

jupyter notebook Energy_Load_Analysis.ipynb


The notebook will execute the full workflow: data loading, cleaning, feature engineering, EDA, modeling, and visualizations.
