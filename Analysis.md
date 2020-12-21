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
