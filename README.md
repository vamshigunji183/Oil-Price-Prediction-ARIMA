# Oil-Price-Prediction-ARIMA

### Introduction
Oil price forecasting using ARIMA.
Data: Quadl Crude oil dataset
Challenge: Time Series data
Concepts: ARIMA(p,d,q), Time series
Algorithms: Support Vector Regression RBF, Linear Regression, Auto Correlation Function(ACF)

### Setup
Install Quandl `conda install -c anaconda quandl ` [here](https://anaconda.org/anaconda/quandl)
pandas==0.17.0
numpy
seaborn

### Discussion

# Time Series

<img src="./Images/value.png" alt="Price in USD"align= 'center' width="100%">

<img src="./Images/exponential-model.png" alt="Exponential Model Price in USD"align= 'center' width="100%">


Time series prediction or forecasting presents its own challenges which are different from machine-learning problems.  

Let's first define our time-series as

$$ \{X_t, t = \ldots, -1, 0, 1, \ldots\} \, . $$

In general, while we could use regression to make predictions, the goal of time series analysis is to take advantage of the temporal nature of the data to make more sophisticated models.

**Why not regression** : In typical time series analysis, the depended variables are missing. For exmaple, a simple linear regression would take a form of 

$$ Y = \beta_0 + \beta_1 X_1 + ...$$

where X_1, X_2 ... are unknown. All we know is Y as a function of time.

Here are a few concepts related to time series.  We take $\varepsilon \sim N(0, \sigma^2)$ to be i.i.d. normal errors.  
1. **Stationarity**.  Informally, this means that the distribution of the $X_t$ is independent of time $t$.  Formally, a time-series is stationary if for all $k \ge 0$ and $t$, the following two $k$-tuples have the same distribution:
$$ (X_0,\ldots,X_k) \sim (X_t,\ldots,X_{t+k}) $$
1. **Drift**.  One reason a time-series might not be stationary is that it possess a drift.  For example, we know that prices tend to creep up with inflation.  Mathematically, we might represent the (log) prices as
$$ X_t = \mu t + \varepsilon_t $$
1. **Seasonality**.  Another reason a time-series might not be stationary is that it posseses a seasonal component.  For example, we know that the temperature increases in the summer and decreases in the winter.  A simple model of this might be
$$ X_t = \alpha \sin(\omega t) + \beta \cos(\omega t)$$

### SVR RBF
<img src="./Images/SVM RBF.png" alt="SVM RBF, Linear Regression"align= 'center' width="100%">

## Advanced Time Series Models
### Check for Stationarity in a series?

***Plotting Rolling Statistics:*** Plot the moving average or moving variance and see if it varies with time. By moving average/variance I mean that at any instant ‘t’, we’ll take the average/variance of the last year, i.e. last 12 months. But again this is more of a visual technique.

**Dickey-Fuller Test:** This is one of the statistical tests for checking stationarity. Here the null hypothesis is that the time series is non-stationary. The test results comprise of a Test Statistic and some Critical Values for difference confidence levels. If the ‘Test Statistic’ is less than the ‘Critical Value’, we can reject the null hypothesis and say that the series is stationary.

Statistical tests make strong assumptions about your data. They can only be used to inform the degree to which a null hypothesis can be accepted or rejected. The result must be interpreted for a given problem to be meaningful.

***Null Hypothesis (H0):*** If accepted, it suggests the time series has a unit root, meaning it is non-stationary. It has some time dependent structure.

***Alternate Hypothesis (H1):*** The null hypothesis is rejected; it suggests the time series does not have a unit root, meaning it is stationary. It does not have time-dependent structure.
We interpret this result using the p-value from the test. 

A p-value below a threshold (such as 5% or 1%) suggests we reject the null hypothesis (stationary), otherwise a p-value above the threshold suggests we accept the null hypothesis (non-stationary).

***p-value > 0.05: *** Accept the null hypothesis (H0), the data has a unit root and is non-stationary.

***p-value <= 0.05: *** Reject the null hypothesis (H0), the data does not have a unit root and is stationary.
<img src="./Images/stationarity-test.png" alt="Rolling Means and Standard Deviation"align= 'center' width="100%">

### Non-Stationarity 
Decomposing the Time Series into `Seasonality`, `Trend` and `Residuals`
<img src="./Images/decomposition.png" alt="Seasonality, Trend, Residuals"align= 'center' width="100%">

### Stationarity Check

Checking for the Stationarity for all the decomposed values.

<img src="./Images/stationarity-decompose.png" alt="Stationarity for Decomposed Values"align= 'center' width="100%">

### Auto Correlation
The Pearson’s correlation coefficient is a number between -1 and 1 that describes a negative or positive correlation respectively. A value of zero indicates no correlation.

<img src="./Images/ACF.png" alt="AutoCorr on Price"align= 'center' width="100%">

### Partial Auto correlation
A partial auto correlation is a summary of the relationship between an observation in a time series with observations at prior time steps with the relationships of intervening observations removed.

PACF with 5 lags
<img src="./Images/PACF5.png" alt="Partial AutoCorr on Price with 5 lags"align= 'center' width="100%">

PACF with 10 lags
<img src="./Images/PACF10.png" alt="Partial AutoCorr on Price with 10 lags"align= 'center' width="100%">

In this plot, the two dotted lines on either sides of 0 are the confidence interevals. These can be used to determine the ‘p’ and ‘q’ values as:

**p** – The lag value where the **PACF** chart crosses the upper confidence interval for the first time. If you notice closely, in this case **p=2**.


**q** – The lag value where the **ACF** chart crosses the upper confidence interval for the first time. If you notice closely, in this case **q=3**.

## ARIMA(p,d,q) Model
ARIMA order (p,d,q) = 2, 2, 10
Predicting the next 6000 timestamps, the RSME is 1.49
<img src="./Images/pred.png" alt="Prediction" align= 'center' width="100%">

Comparing the predicted values with the actual values
<img src="./Images/pred2.png" alt="Prediction" align= 'center' width="100%">

### Testing

<img src="./Images/Test1.png" alt="Test RMSE= 1.05" align= 'center' width="100%">

<img src="./Images/Test1.png" alt="Test RMSE= 1.05" align= 'center' width="100%">





