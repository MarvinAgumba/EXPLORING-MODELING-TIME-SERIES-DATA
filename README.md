# EXPLORING AND MODELING TIME SERIES DATA

## PREPROCESSING OUR TIME SERIES

The first step after loading our data is to change the dates in our dataset from "non-null object" to "non-null datetime" (i.e., change the data type of dates). This can be done using the `to_datetime()` function from Pandas. Afterward, we ensure the date becomes the index.


When data are missing, they can be handled in a multitude of ways: 
* Drop the data elements with missing values (this may result in low accuracy and loss of valuable information)
* Fill in the missing values under a defined criteria 
* Use advanced machine learning methods to predict the missing values
  
In general, the `.fillna()` method can be used along with methods like `.bfill()` or `.ffill()` as an argument/criterion for filling in missing values. `.bfill()` (backward filling) looks for the next valid entry in the time series and fills the gaps with this value. Similarly, `.ffill()` can be used to copy forward the previous valid entry of the time series (as demonstrated above).

## VISUALIZING OUR TIME SERIES
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

![image](https://github.com/MarvinAgumba/EXPLORING-MODELING-TIME-SERIES-DATA/assets/122484885/5b59fd56-d0ad-4fd1-bff2-4cc13db51264)




