# Predict-RDU-Weather

Objective: Predict hourly temperature at RDU Airport for the period September 17–30, 2025

# Overview

This project focuses on forecasting hourly temperature at Raleigh–Durham International Airport using historical weather time-series data. Multiple regression models were evaluated, with Random Forest selected as the final model due to its superior performance and ability to capture non-linear relationships in weather patterns.

# Data Collection

Weather data was obtained using the Meteostat API at an hourly frequency. All timestamps were originally stored in UTC and converted to Eastern Time to ensure proper temporal alignment and prevent feature leakage.

# Data Cleaning and Imputation

Several data quality issues were addressed prior to modeling. The tsun and snow variables were removed due to extensive missing values and limited relevance for temperature prediction in the RDU region. Wind gust values were sparse and were imputed using wind speed while also creating a gust indicator flag. Wind direction was transformed using sine and cosine components to preserve its circular nature. Pressure values had minimal missingness and were interpolated. Precipitation values were forward-filled to avoid leaking future information. Weather codes were retained as a categorical signal and used from July 2018 onward.

# Feature Engineering

Strong temporal autocorrelation motivated the creation of lag and rolling features. Lag features included 1-hour and 24-hour temperature values. Rolling averages were calculated over 1, 3, 5, 7, 15, and 30-day windows. Additional meteorological variables included dew point, pressure, and wind speed. Feature selection using f-regression identified the 1-hour and 24-hour lags as the strongest predictors.

# Modeling Approach

The following models were evaluated using a time-based train-validation split of 80 percent training and 20 percent validation data. Linear Regression, Ridge Regression, Lasso Regression, and Random Forest Regressor. All numeric features were standardized using StandardScaler. Random Forest was selected as the final model due to its superior validation performance and ability to model non-linear feature interactions.

# Evaluation Metrics

Model performance was assessed using Mean Absolute Error to measure average prediction error in degrees Fahrenheit and R squared to quantify the proportion of variance explained.

# Results

Random Forest achieved the highest validation performance. Using 1-hour and 24-hour lag features resulted in an R squared of approximately 0.918. When only rolling averages were used, performance dropped significantly to an R squared of approximately 0.25. While Random Forest showed some overfitting, it still generalized better than linear models.

# Key Observations

Temperature exhibits strong short-term persistence and daily cyclical behavior. Lag features are the dominant drivers of model accuracy but may limit performance during sudden weather changes. Random Forest captured non-linear interactions between meteorological variables that linear models could not.


