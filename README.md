Main goal of project: forecasting trends and uncovering seasonality of data post pandemic. 

# Forecasting Future U.S. Unemployement Rate
## Introduction
Unemployment rate is a significant measure of economic health as changes in rate can provide insights on changes in the labor market and socio-economic conditions. This project focuses on understanding and predicting unemployment rate in the United States from 1948 to 2023 using time series analysis. By having a better understanding on past unemployment trends in relation to changes over time and external factors, we can uncover long term trends that can be found about the U.S. labor market. Time series analysis techniques can provide further understanding of variations of unemployment rate, and forecasting can aid those such as economists or businesses in planning.

It is important to note that major events that have impacted the economy during this time, such as the COVID-19 pandemic, which can affect how the model characterizes changes in rate. Another notable economic event, the global financial crisis in 2008, has also had a significant impact on labor markets and thus unemployment rates. Events such as these have resulted in disruptions on the economy such as unprecedented closures and job losses.

The data collected from 1948 to 2023 still showcases a period of various policy shifts, recessions, and worldly events that can be used to understand underlying patterns and trends. Researchers can use this information to determine proper measures to mitigate and recover from economic declines. Specifically, policy makers can use unemployment forecasts to determine methods that will reduce future job losses and also provide resources for relief measures. Those who are interested in unemployment forecasts can use this information to make informed decisions on how to navigate the labor market for themselves and their career choices.

In this project, I will be implementing two time series methods to analyze the dataset, including the SARIMA model and Spectral Analysis in RStudio. Specifically, I will be applying the Box-Jenkins Approach for the ARIMA model. For the first model, I will also be predicting 12 points ahead to understand implications of such models on the U.S. Unemployment rate. The goal of this project is to have a holistic understanding of the unemployment rate over time, which will be valuable in making optimal economic decisions.

## Methodology
### Data Cleaning & Exploratory Data Analysis (EDA) 📊
To clean the dataset, I 
- removed missing values
- converted date columns into dates
- created time series and data frame for plotting 

## Method 1: SARIMA(p,d,q)x(P,D,Q) model🔍
- applied the Box-Jenkins approach
- plotted time series original data
- analyzed ACF and PACF plots
To understand the `ACF` or `PACF` plots, we will analyze significant points and determine if there is any seasonality present. Specifically, the ACF plot will reveal whether or not the model estimated could be a moving average MA(q) model; the PACF plot indicates if the model can be `autoregressive AR(p)`. An autoregressive (AR) model will incorporate past data points to predict within the same time series. The `moving average (MA)` model is a smoothing technique that applies the averages of points in the time series to highlight long term trends. The diagnostic plots to consider are: `standardized residuals`, `ACF of residuals`, `Normal Q-Q` plot of standardized residuals, and p-values for the `Ljung Box` Statistic. To analyze these, we will first consider the standardized residuals and determine if it appears stationary. As for the ACF of residuals, we will determine if there are any significant spikes. The  `Q-Q plot` will reveal if the residuals follow a normal distribution if they are along the line. The p-values for Ljung Box Statistic will test whether the residuals are independent or have an auto correlated relationship.

### Results: 
Based on the diagnostic plots, I selected the SARIMA(1,0,1)x(1,0,1)[12] model.
For this SARIMA(1,0,1)x(1,0,1)[12] model, there are no apparent patterns in the data and it is relatively stationary, with the exception of 2020. This makes sense as it corresponds to the recession during the COVID-19 pandemic, so the unemployment rate peaks significantly. The ACF plot tails off, and there are not any significant points of residuals. We can observe that the Q-Q plot appears to be relatively normal as it follows the straight line. There are outliers in the beginning of the plot and a significant outlier at the highest theoretical quantile, but it still reasonably follows a normal distribution. As for the p-values for the Ljung-Box statistic, there are two lower p-values that falls close to being statistically significant at earlier lags. Overall, as the lags increase, the p-values increase as well and are greater than 0.05. This indicates the values are not autocorrelated.

## Forecasting Future Unemployment Rate:
Now we can use the estimated model on the original data and forecast the next 12 data points (months) in the future. Since we are using the original data with our SARIMA model, we will set d = 1 and D = 1 to account for differencing. 

To view forecasted points, check out my full report linked below!

### Method 2: Spectral Analysis 

Unemployment follows a cycle related to business and fluctuations in the economy. As an economy reaches a peak or experiences growth, the rate of cyclical unemployment will be low. 

We will compute the raw and log spectrum with a periodogram. The periodogram will display the relative strengths of different frequencies that can explain the variation or cyclic behavior in the time series. It is a rough sample estimate of the spectral density, calculated using the `Fourier Transform`.

## Results: 

We can identify the first three dominant frequencies of the raw spectrum, and their respective periods (Frequencies A, B, C). I've also found the periods for the significant peaks as well as their respective frequency, spectrum, and confidence interval bounds as shown in Table 2. I also computed the confidence interval at the yearly cycle 1/12 = 80/960, which is (0.4576484, 66.68073).

From the top three frequencies, we can see that Frequency A is 0.0625 with a period of 16. Similarly, we can also see that Frequency B has a high period of 26. However, upon observation of their respective confidence intervals, we cannot establish significance between these top frequencies A, B, and C. This is because their spectrum values lie within the upper and lower confidence bounds of the other top frequencies. For example, the frequency A  has a spectrum value of 16.17, which lies within the bounds of the second and third top frequencies. 

Overall, the peak at $1\Delta$ corresponds to a strong periodic component that repeats every 12 months (yearly) at a spectrum of 1.6882. This is reasonable as unemployment rates may follow an annual cycle as it exhibits some seasonal variation.

## Conclusion & Next Steps 🎯

Through the two methods, SARIMA and Spectral Analysis, we were able to forecast the next 12 months of U.S. Unemployment rate and explore its frequencies. Overall, this project utilized time series analysis through SARIMA and Spectral Analysis to forecast and uncover underlying seasonality in U.S. unemployment rate. These findings have significant implications on future planning in regards to the changing U.S. economy and its employment rates.

Other predictors such as demographic information or location would be beneficial in supplementing this project and forecasting accuracy. 

## Resources: 
Shumway, Robert H., and David S. Stoffer. Time Series Analysis and Its Applications: With R Examples. Springer International Publishing, 2017.

“Unemployment Rate (UNRATENSA) | FRED | St. Louis Fed.” Federal Reserve Economic Data | FRED, https://fred.stlouisfed.org/series/UNRATENSA. Accessed 7 June 2024.

“Time Series.” 1.5 Spectral analysis | timeseRies, https://lbelzile.github.io/timeseRies/spectral-analysis.html. Accessed 7 June 2024.

## Full Project Report: 
Project: https://sarahllew.github.io/Forecasting-US-Unemployment.pdf  
