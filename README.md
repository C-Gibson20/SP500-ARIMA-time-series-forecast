# S&P500 ARIMA Time Series Forecast

This project performs statistical time series analysis and forecasting on historical S\&P 500 closing prices using the ARIMA (AutoRegressive Integrated Moving Average) model. It includes rigorous preprocessing, model selection via autocorrelation analysis, model fitting, and short-term forecasting with confidence intervals.

<br>

## Overview

* **Objective**: Forecast future S\&P 500 closing prices using a data-driven ARIMA modeling approach.
* **Data Source**: 5 years of daily closing prices from `S&P 500 Historical 5 Years.csv`.

<br>

## Implementation

### 1. Data Preparation

* Reverses the dataset for chronological ordering.
* Resets the index for proper time series formatting.
* Visualizes the raw closing prices over time.

### 2. Stationarity Testing

* **ADF Test**: Augmented Dickey-Fuller test is applied to assess stationarity.

  * If p-value > 0.05, the series is non-stationary and differencing is applied (`d = 1`).
  * If p-value ≤ 0.05, the series is stationary (`d = 0`).

### 3. Model Order Selection

* **ACF (AutoCorrelation Function)** and **PACF (Partial AutoCorrelation Function)** plots are generated.
* Significant lags are determined using confidence intervals:

  * `q` is selected based on significant ACF lags.
  * `p` is selected based on significant PACF lags.
* Lags are extracted using a custom function comparing coefficient bounds.

### 4. ARIMA Model Construction

* The ARIMA model is fit using the identified `(p, d, q)` parameters.
* A deterministic trend component is added:

  * `'t'` for differenced data, `'c'` otherwise.
* The model is trained using maximum likelihood estimation with extended iterations (`maxiter=2000`).

### 5. Forecasting and Visualization

* The model forecasts the next 10 time steps, producing mean estimates and 95% confidence intervals.
* Diagnostic plots evaluate model assumptions (e.g., residual normality and autocorrelation).
* Two forecast plots are generated:

  * Full-range comparison between observed and forecasted values.
  * Zoomed view on the last 50 days for short-term accuracy evaluation.
  * Highlights 1-day and 4-day forecasts.

