# Time Series Analysis

This project serves as an exercise in time series analysis. 

As an example, we will fit several models (usually ARIMA, GARCH) for the prices and returns of Bitcoin, the Euro and Gold (measured against the US Dollar).

A word of caution: in this exercise we are focusing on the **practical** implementation rather than the mathematical correct interpretaiton. 
We do not claim that any results obtained in this exercise are correct form the point of view of financcial analysis and hence should not be used for investment strategies without further study.

## Data
The data is acquired using the yahoo finance API `yfinance` whose `download()` method directly organizes the data into a pandas DataFrame whose index is already the date (of type datetime).

## Methodology

1. **Data Cleanning.**
   The frequency retrieved data is set to businessdays.
   However, we observe that many of the missing data of *gold* falls on US holidays.
   We therefore reset the frequencies of the DataFrames to respect the US holidays.
   Since we do not spot any apparant pattern among the missing data which is left, we fill in their values using a *forward fill*

2. **Data Pre-Processing.**
   We are interested in the closing price and returns.
   We therefore frist create new DataFrames keeping only the information of the closing prices and add a columnn of returns using the `pct_change()` method.

3. **Exploration of Data.**
   We plot prices for each currency as well as their normalized values (normalized by the respective maximum) in order to better compare the fluctuations in price.
   Furthermore we compare the returns for each currency.

4. **Analysis of Stationarity.**
   We check stationarity of the currencies using ACF and PACF plots as well as the Dickey-Fuller Test.
   We observe that, as expected, *prices*, in contrast to *returns*, are non-stationary.
   Moreover, we find from the PCAF plots that only the first lag is significant.

5. **Annalysis of Gold.**
   We first re-verify the stationarity of the gold returns using the Dickey-Fuller test.
   Furthermore, we test once more for missing values.
   Next, we split the data in training (80%) and test data (20%).
   To model the volatility of gold, we choose a GARCH(1,1) model.

## Results
   A GARCH(1,1) model, assuming normally distributed errors, yields standardized returns (using the estimated mean and variance) which exhibit properties of white noise.
   However the model fails to predict the *magnitude* of the true squared returns accurately, while it does predict the general pattern and clustering behavior quite well.
   A GARCH(1,1) model assuming that the errors forllow a t-distribution, on the other hand, performs fairely well in predicting both, the magnitude and the clustering behavior of the squared returns.
   We remark, however, that the true squared returns and the model prediction differ by a constant.






   
   
