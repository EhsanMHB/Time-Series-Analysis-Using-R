### Objective
The objective is to find a proper time series model by which we would be able to estimate the 8 missing observations.

### Data Sets
The data set includes a monthly time series of monthly total number of passengers in thousands between Jan., 1949 to Dec., 1960. We have 136 observed values.

### How to do this task using R in 3 steps?

#### Step 1.
At first, we plot our data to examine their patterns or some irregularities. In this case, number of passengers does not show significant outliers to take into account. However, ***tsclean()*** is a convenient method for outlier removal and inputting missing values which is not our purpose now.

![](images/data%20plot.png)

#### Step 2.
Autocorrelation plots (also known as **ACF** function) are a useful visual tool to determine whether a series is stationary or not. These plots can also help choosing the order parameters for **ARIMA** model. However, ***auto.arima()*** function in **R** is able to work with time series with missing values and find the optimal arima parameters. In this case, we have implemented the ***auto.arima()*** and the fitted **ARIMA** model is as follows:

![](images/ARIMA%20model.png)

The model is a seasonal ARIMA model with:

non-seasonal AR order = 2

non-seasonal differencing = 1

non-seasonal MA order = 2

seasonal AR order = 2

seasonal differencing = 1

seasonal MA order = 0

and S = 12 represents time span of repeating seasonal patterns.

A seasonal second order autoregressive model would use x<sub>t-12</sub> and x<sub>t-24</sub> to predict x<sub>t</sub>. For example, here we would predict this August’s number of passengers from the past two Augusts. Besides, A seasonal second order MA(2) model would use w<sub>t-12</sub> and 
w<sub>t-24</sub> to predict.

Non-seasonal differencing usually detrend the data when it is available. Here a first difference has been implemented to detrend the data. Also, when we have both seasonality and trend, the model applies both a non-seasonal first difference and a seasonal difference.

#### Step 3.
Now using ARIMA parameters and ***KalmanRun()*** function in R we would be able to estimate missing values. This function predicts and returns consecutive values of a univariate time series using the best evaluated ARIMA model automatically fitted with Kalman filter. However, we have used it to evaluate missing observations in samples corresponding to dates in test set.

In the following plot you would be able to see estimated values for missing observations.

![](images/estimated%20values%20plot.png)

Also, the estimated values for missing observations have been reported in the following table:

![](images/estimated%20values%20table.png)

In addition, considering these values we could fit another ARIMA model and do forecasting for future values.
