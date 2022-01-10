# Gold-Price-forecasting
In a personal endevaour to learn about time series analysis and forecasting, I decided to reserach and explore various quantitative forecasting methods.This notebook documents contains the methods that can be applied to forecast gold price and model deployment using streamlit, along with a detailed explaination of the different metrics used to evaluate the forecasts.

## Goal: 
The goal of this project was to predict future gold price based on previous gold price. I apply various quantitative methods, (i.e. Times Series Models and Causal Models) to forecast the Price of the gold available in the dataset obtained from Kaggle.

## Models covered in the Project include:

1.Naive Model

2.ARIMA and Seasonal ARIMA Models

3.Linear Regression Model

4.Model Deployment (Streamlit)

## Naive methods:
This method is like the naive method but predicts the last observed value of the same season of the year. This method works for highly seasonal data.
Before diving into sophisticated algorithms it is necessary to plot the time series data to gain intuition and even make direct predictions
There are several trends that occur in time series analysis, they are seasonal trends(increase or decrease at equal intervals and are associated with some aspect of the calendar) and cyclical ( increase or decrease at irregular intervals) cyclical trends can be observed in stock market where bull market is uptrend and bear market represents the downtrend. Cyclical patterns are tough to predict as they are could be very random.

Before we get to the more advanced time-series forecasting methods, let's take a look at a basic method - Seasonal Naive. It can serve as a quick calculation to get a baseline until something better can come along. Or, perhaps there is very little variance in the data, then this method can be good enough.

It is a naive method that takes the  patterns into account by looking at what happened same time previous day. For example, if we want to predict the sales during January 2021, the naive method will assume the previous number of sales for previous day. Fortunately, we have at least one-year of sales data, this method might make no sense otherwise.

## ARIMA and Seasonal ARIMA Models
#### ARIMA: 
ARIMA models are flexible and widely used in time series analysis. ARIMA combines three processes:
autoregressive (AR), differencing to strip off the integration (I) of the series and moving averages (MA). Each
of the three process types has its own characteristic way of responding to a random disturbance. Autoregressive integrated moving average (ARIMA) models predict future values based on past values. ARIMA makes use of lagged moving averages to smooth time series data. They are widely used in technical analysis to forecast future security prices. The practical difference is ARIMA packages are built to assume time series data, whereas most regression packages make no special allowances for time-dependent data. The ARIMA model uses differenced data to make the data stationary, which means there’s a consistency of the data over time. This function removes the effect of trends or seasonality, such as market or economic data.

#### Step 1: Check stationarity
Before going any further into our analysis, our series has to be made stationary.

Stationarity is the property of exhibiting constant statistical properties (mean, variance, autocorrelation, etc.). If the mean of a time-series increases over time, then it’s not stationary.

The mean across many time periods is only informative if the expected value is the same across those time periods. If these population parameters can vary, what are we really estimating by taking an average across time?

Stationarity requires that the statistical properties must be the same across time, making the sample average a reasonable way to estimate them.

##### Methods to Check Stationarity
Plotting rolling statistics: Plotting rolling means and variances is a first good way to visually inspect our series. If the rolling statistics exhibit a clear trend (upwards or downwards) and show varying variance (increasing or decreasing amplitude), then you might conclude that the series is very likely not to be stationary.

Augmented Dickey-Fuller Test: This test is used to assess whether or not a time-series is stationary. It gives a result called a “test-statistic”, based on which you can say, with different levels (or percentage) of confidence, if the time-series is stationary or not. The test statistic is expected to be negative; therefore, it has to be more negative(less) than the critical value for the hypothesis to be rejected and conclude that series is stationary.

ACF and PACF plots: An autocorrelation (ACF) plot represents the autocorrelation of the series with lags of itself. A partial autocorrelation (PACF) plot represents the amount of correlation between a series and a lag of itself that is not explained by correlations at all lower-order lags. Ideally, we want no correlation between the series and lags of itself. Graphically speaking, we would like all the spikes to fall in the blue region.

#### Step 2: Differencing
##### Differencing: 
Seasonal or cyclical patterns can be removed by substracting periodical values. If the data is 12-month seasonal, substracting the series with a 12-lag difference series will give a “flatter” series. Since we have aggregated the data to each day-level, we will shift by 1.

#### Step 3: Model Building
Interpreting the AR(p), I(d), MA(q) values:
Determining I(d):

Taking the first order difference makes the time series stationary. Therefore, I(d) = 1.

Determining AR(p): If the lag-1 autocorrelation of the differenced series PACF is negative, and/or there is a sharp cutoff, then choose a AR order of 1.

From the PACF plot we can clearly observe that within 6 lags the AR is significant. Therefore, we can use AR(p) = 6, (6 lines are crossed the blue lines so 6past days are required to predict).

Determining MA(q): If the lag-1 autocorrelation of the differenced series ACF is negative, and/or there is a sharp cutoff, then choose a MA order of 1.

From tha ACF plot we see a negative spike at lag 1, therfore we can use MA(q) = 1

#### Determine Error, Trend and Seasonality
An ETS model has three main components: error, trend, and seasonality. Each can be applied either additively, multiplicatively, or not at all. We will use the above Times Series Decomposition Plot to determine the additive or multiplicative property of the thre components.

Trend - If the trend plot is linear then we apply it additively (A). If the trend line grows or shrinks exponentially, we apply it multiplicatively (M). If there is no clear trend, no trend component is included (N).

Seasonal - If the peaks and valleys for seasonality are constant over time, we apply it additively (A). If the size of the seasonal fluctuations tends to increase or decrease with the level of time series, we apply it multiplicatively (M). If there is no seasonality, it is not applied (N).

Error - If the error plot has constant variance over time (peaks and valleys are about the same size), we apply it additively (A). If the error plot is fluctuating between large and small errors over time, we apply it multiplicatively (M).

For our Gold price data, we see a linear trend plot and a constant seasonality over time, so we will apply trend and seasonality additively. The your data is non stationary.


## Linear regression
It is one of the most commonly used predictive modelling techniques.It is represented by an equation 𝑌 = 𝑎 + 𝑏𝑋 + 𝑒, where a is the intercept, b is the slope of the line and e is the error term. This equation can be used to predict the value of a target variable based on given predictor variable(s).

#### Step 1: Feature Engineering

#### Step 2: Feature Selection and Model Building

#### Step 3: Model Evaluation and Predictions

## Model Deployment(Streamlit)
![Untitled](https://user-images.githubusercontent.com/82845139/148784613-923a4e30-4752-4367-a3ac-9f3c51298e05.png)

