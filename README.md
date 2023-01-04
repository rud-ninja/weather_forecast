# Title: Forecasting land temperatures from only historical temperature data (univariate) using ARIMA model

### Objectives:
1. Exploratory data analysis
2. Long term forecast (2 years) and short term forecast (6 months)
3. Comment on the difference in results for long term and short term forecasts

#### Language used:
Python

#### Libraries used:
Pandas, NumPy, Matplotlib, seasonal_decompose, acf & pacf (auto-correlation function), ARIMA

#### The dataset:
The dataset consists of recorded average temperatures over a monthly period across several major cities of the world from 1800 to 2014. Check dataset [here]().

#### Data Imputation:
There were a few missing values for recorded average temperature. These values have been imputed using forward fill (ffill) function in pandas.

## Figures and discussions

### Data exploration

![]()

**Fig 1: A Look at the temperature distribution over all the major cities in the dataset**

We can see a skewed distribution leaning more towards warmer land temperatures. For the remainder of the task, we have selected 3 cities lying on different latitudes for comparison of local temperature characteristics and will attempt to forecast their land temperatures for long and short periods. The cities selected are *Calcutta* that experiences tropical climate, *London* that experiences temperate climate and *Rio De Janeiro* that also experiences tropical climate but lies in the southern hemisphere.

![]()

**Fig 2: Temperature distribution across the cities represented as histogram and boxplot**

Speaking of climate, an interesting thing to observe will be the gradual rise in land temperature over the years. Below is a trend plot with a period of 10 years that shows that.

![]()

**Fig 3: Trend of average land temperature since 1900 over a period of 10 years**

![]()

**Fig 4: A closer look at the temperature changes with time across the 3 cities**

![]()

**Fig 5: Monthly seasonality of land temperature values**

### Forecasts
The first thing to consider when using ARIMA model for time series forecasts is the stationarity of the series. We make use of autocorrelation and partial autocorrelation plots along with p value tests like Augmented Dickey Fuller test to determine whether a time series is stationary. If they are not, they have to be made stationary first before models can be trained on them.

![]()

**Fig 6: Plots of autocorrelation and partial aurocorrelation functions that demonstrate correlation between past and future values in the time series as a function of the time gap (or lag) between them. The above plot is for the city of London. The same has been performed for the remaining cities (not shown here).

The above figure was followed by an AD fuller test whose resutls were as follows:

*ADF Statistic for a decade for city of London: -1.2288251956924272
p-value: 0.661074580011341
Critical Values:
	1%: -3.486055829282407
	5%: -2.8859430324074076
	10%: -2.5797850694444446*
  
The p-value is greater than 0.05 which is our considered significance level. This indicates that the series is not stationary. To make it stationary, we perform first differenciation, which essentially means calculating the difference between subsequent temperature values. The results are as follows.

*ADF Statistic of 1st difference: -9.27663324265689
p-value: 1.2837472335018562e-15
Critical Values:
	1%: -3.486055829282407
	5%: -2.8859430324074076
	10%: -2.5797850694444446*
  
Now the p-value is less than 0.05 which means the series is now stationary and the ARIMA model can be trained on it.

#### Long term forecasts

![]()
![]()
![]()

**Fig 7: Long term land temperature forecasts for the 3 cities. The plots on the left display the training and test size while the plots on the right display the actual vs predicted values and the 95% confidence interval for the same.

#### Short term forecasts

![]()
![]()
![]()

**Fig 8: Short term forecasts
