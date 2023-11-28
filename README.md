# EXPLORING TIME SERIES DATA

## PREPROCESSING OUR TIME SERIES

The first step after loading our data is to change the dates in our dataset from "non-null object" to "non-null datetime" (i.e., change the data type of dates). This can be done using the `to_datetime()` function from Pandas. Afterward, we ensure the date becomes the index.


When data are missing, they can be handled in a multitude of ways: 
* Drop the data elements with missing values (this may result in low accuracy and loss of valuable information)
* Fill in the missing values under a defined criteria 
* Use advanced machine learning methods to predict the missing values
  
In general, the `.fillna()` method can be used along with methods like `.bfill()` or `.ffill()` as an argument/criterion for filling in missing values. `.bfill()` (backward filling) looks for the next valid entry in the time series and fills the gaps with this value. Similarly, `.ffill()` can be used to copy forward the previous valid entry of the time series (as demonstrated above).

## VISUALIZING OUR TIME SERIES
**Line plots** and **dot plots** can be useful for getting a sense of how a time series dataset changes over time\
**Histograms** and **density plots** can be useful for getting a sense of the time-independent distribution of a time series\
**Box** and **whisker plots** per year (or other seasonality periods - day, week, month, etc) can be a great way to easily see trends in the distribution of time series data over time\
**Heat maps** can also be useful for comparing changes in time series data across a couple of dimensions. For example, with months on one axis and years on another, they can be a great way to see both seasonality and year-on-year trends
![image](https://github.com/MarvinAgumba/EXPLORING-MODELING-TIME-SERIES-DATA/assets/122484885/20e67be2-0ae6-4180-a41f-bb25e6d42741)

## IDENTIFYING TRENDS
**Stationarity**: A time series is said to be stationary if its statistical properties such as mean, variance, etc. remain constant over time. Most time series models work on the assumption that **the time series are stationary**. For general time series datasets, if it shows a particular behavior over time, there is a very high probability that it will follow a similar behavior in the future. Also, the theories related to stationary series are more mature and easier to implement as compared to non-stationary series.

![image](https://github.com/MarvinAgumba/EXPLORING-MODELING-TIME-SERIES-DATA/assets/122484885/60855ffb-b365-4517-b7f6-030b46fa3308)

![image](https://github.com/MarvinAgumba/EXPLORING-MODELING-TIME-SERIES-DATA/assets/122484885/c5891040-4f5e-46d1-94a7-cf8654805e25)

![image](https://github.com/MarvinAgumba/EXPLORING-MODELING-TIME-SERIES-DATA/assets/122484885/4e27b9b0-eb84-4c60-a565-b8810b5f5d41)

**Trend Types:** Linear (Uppward and Downward); Periodic (go both up and down with similar variability); Trend with an increasing variance (variability changes over time); Exponential; Periodic and upward trend.

### Checking for Trends
- ***Rolling Statistic*** - plot the moving average or moving variance and see if it varies with time.
- ***The Dickey-Fuller Test*** - The Dickey-Fuller test is a statistical test for testing stationarity. The null hypothesis for the test is that the time series is not stationary. So if the test statistic is less than the critical value, we reject the null hypothesis and say that the series is stationary.

Below illustration: The red and black lines represent the rolling mean and rolling standard deviations. You can see that the mean is not constant over time, so we can reconfirm our conclusion that the time series is not stationary based on the rolling mean and rolling standard error.
![image](https://github.com/MarvinAgumba/EXPLORING-MODELING-TIME-SERIES-DATA/assets/122484885/a30b3f9e-9352-4381-8e78-cb152369c6ca)

## REMOVING TRENDS
Techniques:
- Log Transformation
- Subtracting Rolling Mean
- Differencing

**Time Series Decomposition:** Time series decomposition is a mathematical procedure that transforms a time series into multiple different time series. The original time series is often split into three component series:

- **Seasonal**: Patterns that repeat within a fixed period. For example, a website might receive more visits during weekends; this would produce data with a seasonality of 7 days.

- **Trend**: The underlying trend of the metrics. A website increasing in popularity should show a general trend that goes up.

- **Random**: Also called "noise", "irregular", or "remainder", this is the residual of the original time series after the seasonal and trend series are removed.

Decomposing allows you to separately view seasonality (which could be daily, weekly, annual, etc), trend, and random, which is the variability in time series after removing the effects of the seasonality and trend

![image](https://github.com/MarvinAgumba/EXPLORING-MODELING-TIME-SERIES-DATA/assets/122484885/5b59fd56-d0ad-4fd1-bff2-4cc13db51264)

# MODELING TIME SERIES DATA

Essentially, you're trying to find patterns and understand the data in a way that you can use this information to (hopefully) make accurate predictions about the future.
 - **White Noise Model** features: Fixed and constant mean; Fixed and constant variance; No Correlation over Time (Example: Gaussian White Noise)
 - **Random Walk Model** As opposed to the white noise model, the random walk model, however, has No Specified Mean/Variance; Strong Dependence over time; (Very common in Finance like exchange rate)

**Autocorrelation:** It helps us study how each time series observation is related to its recent (or not so recent) past. Processes with greater autocorrelation are more predictable than those without any form of autocorrelation.

**The Autocorrelation Function:** The autocorrelation function is a function that represents the autocorrelation of a time series as a function of the time lag. The autocorrelation function tells interesting stories about trends and seasonality. For example, if the original time series repeats itself every five days, you would expect to see a spike in the autocorrelation function at 5 days.

ACF Plot interpretation: The dotted lines in the plot tell you about the statistical significance of the correlation. For the below time series you can say that our data is definitely autocorrelated for lags of twelve months and 24 months, but for some later lags the result is not significant.
![image](https://github.com/MarvinAgumba/EXPLORING-MODELING-TIME-SERIES-DATA/assets/122484885/cefd4d3b-e06f-49c8-8c6e-7d3b3466648f)

Below autocorrelation for multiples of 12 seems consistently statistically significant, while it decays for a longer time lags
![image](https://github.com/MarvinAgumba/EXPLORING-MODELING-TIME-SERIES-DATA/assets/122484885/62571f1b-5bff-4211-b13b-48df92b4847a)

**Partial Autocorrelation Function** (or PACF) gives the partial correlation of a time series with its own lagged values, controlling for the values of the time series at all shorter lags (unlike the autocorrelation function, which does not control for other lags).

![image](https://github.com/MarvinAgumba/EXPLORING-MODELING-TIME-SERIES-DATA/assets/122484885/78d23898-23bc-47d2-ab85-b79c93451e99)

## Modeling with Autoregressive and Moving Average Models
ARMA (Autoregressive and Moving Average) modeling is a tool for forecasting time series values by regressing the variable on its own lagged (past) values

An autoregressive (AR) model is when a value from a time series is regressed on previous values from the same time series\
The first-order AR model would be represented as `(1,0,0)`.

The Moving Average model can be described as the weighted sum of today's and yesterday's noise\
The first-order MA model is represented as `(0,1)`. 

ARMA models assume that you've already detrended your data and that there is no seasonality

The ARIMA Time Series Model (**AutoregRessive Integrated Moving Average**) with parameters (p,d,q) where:
- `p` is the auto-regressive part of the model. It allows us to incorporate the effect of past values into our model. (Number of AR (Auto-Regressive) terms)
- `d` is the **Integrated** component of an ARIMA model. This value is concerned with the amount of differencing as it identifies the number of lag values to subtract from the current observation. (Number of Differences)
- `q` is the moving average part of the model which is used to set the error of the model as a linear combination of the error values observed at previous time points in the past. (Number of MA (Moving-Average) terms)

### Model Evaluation

**AIC (Akaike Information Criterion) as Regularization Measure** The Akaike information criterion (AIC) is an estimator of the relative quality of statistical models for a given set of data. Given a collection of models for the data, AIC estimates the quality of each model, relative to each of the other models. Thus, AIC provides a means for model selection. A model that fits the data very well while using lots of features will be assigned a larger AIC score than a model that uses fewer features to achieve the same goodness of fit. Therefore, we are interested in finding the model that yields the lowest AIC value. 

**MSE (Mean Squared Error)** used to check for the accuracy of our forecasts. An MSE this close to 0 indicates that the estimator is predicting observations of the parameter with perfect accuracy, which would be an ideal scenario but it is not typically possible.  

# ADDITIONAL READINGS

[This blogpost](https://machinelearningmastery.com/gentle-introduction-autocorrelation-partial-autocorrelation/) more about ACF & PACF

[here](https://www.quantstart.com/articles/Autoregressive-Integrated-Moving-Average-ARIMA-p-d-q-Models-for-Time-Series-Analysis). ARIMA Models for Time Series Analysis

[here](https://www.statsmodels.org/dev/generated/statsmodels.tsa.statespace.sarimax.SARIMAX.html) SARIMAX Documentation
