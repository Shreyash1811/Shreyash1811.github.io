---
title: "Stock market forecasting using yfinance and fbprophet"
date: 2020-05-31
categories: [Python]
tags: [Stock Market]
header:
  image: "/images/stocks_fbprophet/header.gif"
excerpt: "The objective of the project was to successfully retrieve data from Yahoo Finance and use various predictive mothod fbprophet  "
mathjax: "true"
---

# Stock Market Forecasting Using FB-Prophet:

### What is fbprophet?
*Fbprophet is an open source released by Facebook in order to provide some useful guidance for producing forecast at scale. By default, it would divide a time series into trend and seasonality, which might contain yearly, weekly and daily. However, analysts can define their own seasonality. To get better understanding about the package, the document from Prophet is really helpful.*

*One of the feature for package is its simplicity and flexibility. Since cycles in stock market we want to figure out are not limited to yearly, weekly or daily, we should define our own cycles and find out which can fit the data better. Besides, we should not use weekly seasonality since there is no trading on weekend. We can also define our ‘self_define_cycle’ by add_seasonality function. All the settings can be done with only two lines of code.*


*In this article, we will experiment with using Prophet to forecast stock prices. Prophet uses a decomposable time series model with three main model components: growth, seasonality and holidays. They are combined using the equation*

$$y(t) = g(t) + s(t) + h(t) + e(t)$$

where g(t) represents the growth function which models non-periodic changes, s(t) represents periodic changes due to weekly or yearly seasonality, h(t) represents the effects of holidays, and e(t) represents the error term. Such decomposable time series are very common in forecasting and later in the article we will see how to tune each component of the above equation.


```python
import numpy as np
import pandas as pd
from pandas_datareader import data
import matplotlib.pyplot as plt
from datetime import datetime
from datetime import timedelta
```


```python
from fbprophet import Prophet
from sklearn.metrics import mean_squared_error
import yfinance as yf
```

## First Step: Data Acquisition.
We need some stocks data to train, test and forcast.

1) We can simple go to yahoo finance and download the data in a csv, but that wouldnt be cool now, would it be?

2) There are plenty on libraries that let you trim stock data. I will be using yfinance as it is convenient and easy to use.

**Now that we know where to get the data from, we have to decided from what date we want the data**

*This depends on what is your objective for the project*
- I want to see the forecasting with and without considering the fall of market due to the terror of Pandemic.
- Also want to have fun along the way.



```python
# Function to get the stock data
def stock_data(stock, start_date, end_date):

    #define the ticker symbol
    tickerSymbol = stock

    #get data on this ticker
    tickerData = yf.Ticker(tickerSymbol)

    #get the historical prices for this ticker
    tickerDf = tickerData.history(period='1d', start=start_date, end=end_date)

    #see your data
    return tickerDf
```

## Picking S&P 500 for this notebook:
I beleive the best way to see the impact would be to consider analysing the Index that would cover good portion of the market companies. I would go ahead with S&P 500 Index for this.


```python
stock_data = stock_data("^GSPC","2013-01-01","2020-06-01")
```

### That was easy!!!


```python
stock_data.tail()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Dividends</th>
      <th>Stock Splits</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-05-22</th>
      <td>2948.05</td>
      <td>2956.76</td>
      <td>2933.59</td>
      <td>2955.45</td>
      <td>3952800000</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2020-05-26</th>
      <td>3004.08</td>
      <td>3021.72</td>
      <td>2988.17</td>
      <td>2991.77</td>
      <td>5837060000</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2020-05-27</th>
      <td>3015.65</td>
      <td>3036.25</td>
      <td>2969.75</td>
      <td>3036.13</td>
      <td>6371230000</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2020-05-28</th>
      <td>3046.61</td>
      <td>3068.67</td>
      <td>3023.40</td>
      <td>3029.73</td>
      <td>5402670000</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2020-05-29</th>
      <td>3025.17</td>
      <td>3049.17</td>
      <td>2998.61</td>
      <td>3044.31</td>
      <td>7275080000</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
stock_data
```




    Index(['Open', 'High', 'Low', 'Close', 'Volume', 'Dividends', 'Stock Splits'], dtype='object')




```python
stock_data['Close'].plot(figsize=(16,8),color='#002699',alpha=0.8)
plt.xlabel("Date",fontsize=12,fontweight='bold',color='black')
plt.ylabel('Price',fontsize=12,fontweight='bold',color='black')
plt.title("Stock price for S&P 500",fontsize=18)
plt.show()
```


![png](images/stocks_fbprophet/output_11_0.png)


### The timeseries Graph above is informative to see through a couple of things:
- We see a steep drop in the start of 2020. This was due to chaos caused by the pandemic.
- We also see the recovery of the market, gradually going back to where dropped from.

## This is all great but when are we using fbprophet?
Lets use fbprophet to see how easy it is to forecast a time series data and learn the trend.


```python
stock_data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Dividends</th>
      <th>Stock Splits</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-02</th>
      <td>1426.19</td>
      <td>1462.43</td>
      <td>1426.19</td>
      <td>1462.42</td>
      <td>4202600000</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>1462.42</td>
      <td>1465.47</td>
      <td>1455.53</td>
      <td>1459.37</td>
      <td>3829730000</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>1459.37</td>
      <td>1467.94</td>
      <td>1458.99</td>
      <td>1466.47</td>
      <td>3424290000</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2013-01-07</th>
      <td>1466.47</td>
      <td>1466.47</td>
      <td>1456.62</td>
      <td>1461.89</td>
      <td>3304970000</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2013-01-08</th>
      <td>1461.89</td>
      <td>1461.89</td>
      <td>1451.64</td>
      <td>1457.15</td>
      <td>3601600000</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Copy of main df
time_series = stock_data.copy()
import fbprophet

time_series['Date'] = time_series.index
# Prophet requires columns ds (Date) and y (value)
time_series = time_series.rename(columns={'Date': 'ds', 'Close': 'y'})
```


```python
m = Prophet(weekly_seasonality=False,yearly_seasonality=False)
m.add_seasonality('self_define_cycle',period=8,fourier_order=8,mode='additive')
```




    <fbprophet.forecaster.Prophet at 0x23e2a0bf780>




```python
# Put market cap in billions
time_series['y'] = time_series['y'] / 1e9
```


```python
# Make the prophet model and fit on the data
corona_prophet = fbprophet.Prophet(changepoint_prior_scale=0.15, weekly_seasonality=False,yearly_seasonality=False)
corona_prophet.add_seasonality('self_define_cycle',period=8,fourier_order=8,mode='additive')
corona_prophet.fit(time_series)
```

    INFO:fbprophet:Disabling daily seasonality. Run prophet with daily_seasonality=True to override this.





    <fbprophet.forecaster.Prophet at 0x23e26f9b048>




```python
# Make a future dataframe for 6 months
corona_forecast = corona_prophet.make_future_dataframe(periods=180, freq='D')
# Make predictions
corona_forecast = corona_prophet.predict(corona_forecast)
```


```python
#Our future dataframes contain the estimated increase in corona cases
corona_prophet.plot(corona_forecast, xlabel = 'Date', ylabel = 'Close Price')
plt.title('Forecasted S&P 500')
```




    Text(0.5, 1, 'Forecasted S&P 500')




![png](images/stocks_fbprophet/output_20_1.png)


## Some cool functions in FBprophet:
**changepoints:**
- This method list down all the time there was a drastic change with S&P stock.

**Plot_components:**
- This method gives us forecast plots on the yearly and daily basis.


```python
# Times when stock significantly changed
corona_prophet.changepoints[:10]
```




    60    2013-04-01
    119   2013-06-24
    179   2013-09-18
    239   2013-12-12
    298   2014-03-11
    358   2014-06-05
    417   2014-08-28
    477   2014-11-21
    537   2015-02-20
    596   2015-05-15
    Name: ds, dtype: datetime64[ns]




```python
corona_prophet.plot_components(corona_forecast);
```


![png](images/stocks_fbprophet/output_23_0.png)


*We see a gradually rising blue line which implies forecasted growth for next 6 months*

## We will analyse the Stock market Cycle further in this Post:

Stock market cycles are the long-term price patterns of stock markets and are often associated with general business  cycles. They are key to technical analysis where the approach to investing is based on cycles or repeating price patterns.

The efficacy of the predictive nature of these cycles is controversial and some of these cycles have been quantitatively examined for statistical significance.

**Well known cycles include:**

- The lunar cycle
- Annual seasonality, also known as Sell in May or the Halloween indicator, as well as the January effect and July effect.
- The four-year United States presidential election cycle in the US.
- The 17.6 Year Stock Market Cycle,
- The 60 year Kondratiev cycles

### For prediction models, one way to evaluate them is out-sample mean squared error.
We can use 2015/10/1 to 2018/3/31 for training and keep the last 6 months for testing and calculating out-sample mean squared error. Within each cycle, we can optimized our return by buying at the lowest price and selling at the highest. To make the process easier, we use self-define function cycle_analysis. The output is a list containing projected return per cycle and out-

### sample mean squared error. Inputs for the function require:
- **data:** Pandas dataframe with time index
- **split_date:** the date to split training and testing data
- **cycle:** periods (days) per cycle
- **mode:** additive or multiplicative for seasonality (optional, default additive)
- **forecast_plot:** whether to print the forecast plot or not (optional, default False)
- **print_ind:** whether to print the projected return per cycle and out-sample mean squared error or not (optional, default False)


### Bringing it all under one roof:


```python
def analysis(data,split_date,cycle,mode='additive',forecast_plot = False,print_ind=False):
    training = data[:split_date].iloc[:-1,]
    testing = data[split_date:]
    predict_period = len(pd.date_range(split_date,max(data.index)))
    df = training.reset_index()
    df.columns = ['ds','y']
    m = Prophet(weekly_seasonality=False,yearly_seasonality=False,daily_seasonality=False)
    m.add_seasonality('self_define_cycle',period=cycle,fourier_order=8,mode=mode)
    m.fit(df)
    future = m.make_future_dataframe(periods=predict_period)
    forecast = m.predict(future)
    if forecast_plot:
        m.plot(forecast)
        plt.plot(testing.index,testing.values,'.',color='#ff3333',alpha=0.6)
        plt.xlabel('Date',fontsize=12,fontweight='bold',color='gray')
        plt.ylabel('Price',fontsize=12,fontweight='bold',color='gray')
        plt.show()
    ret = max(forecast.self_define_cycle)-min(forecast.self_define_cycle)
    model_tb = forecast['yhat']
    model_tb.index = forecast['ds'].map(lambda x:x.strftime("%Y-%m-%d"))
    out_tb = pd.concat([testing,model_tb],axis=1)
    out_tb = out_tb[~out_tb.iloc[:,0].isnull()]
    out_tb = out_tb[~out_tb.iloc[:,1].isnull()]
    mse = mean_squared_error(out_tb.iloc[:,0],out_tb.iloc[:,1])
    rep = [ret,mse]
    if print_ind:
        print ("Projected return per cycle: {}".format(round(rep[0],2)))
        print ("MSE: {}".format(round(rep[1],4)))
    return rep
```


```python
analysis(stock_data['Close'],'2020-05-01',30,forecast_plot=True,print_ind=True)
```


![png](images/stocks_fbprophet/output_29_0.png)


    Projected return per cycle: 23.01
    MSE: 27827.6604





    [23.014163612623296, 27827.66042664391]




```python
analysis(stock_data['Close'],'2020-05-01',300,forecast_plot=True,print_ind=True)
```


![png](images/stocks_fbprophet/output_30_0.png)


    Projected return per cycle: 128.26
    MSE: 40963.9459





    [128.26052883668086, 40963.945875953665]



The MSE is gigantic here and one of the ways to lower it would be to find the ideal value of length of cycle.

## Length of cycle plays a vital role here:
We can apply a loop over our cycle_analysis function to calculate projected return and out-sample mean squared error for different length of cycle, and we displayed the outcome.

As we can see, the longer the length, both projected return per cycle and out-sample mean square error would increase. In consideration of the cost of transaction, the projected return within per cycle should be greater than $ 10.

Under this constrain, we can choose the cycle that leads to minimum out-sample mean squared error.


```python
testing_box = range(10,301,10)
return_box = []
mse_box = []
for c in testing_box:
    f = analysis(stock_data['Close'],'2020-05-01',c)
    return_box.append(f[0])
    mse_box.append(f[1])
```


```python
f = plt.figure(figsize=(16,18))
ax = f.add_subplot(211)
ax2 = f.add_subplot(212)
ax.plot(testing_box,return_box,color='#002699',alpha=0.8)
ax2.plot(testing_box,mse_box,color='#002699',alpha=0.8)
ax.set_xlabel("Length of Cycle",fontsize=12,color='gray')
ax2.set_xlabel("Length of Cycle",fontsize=12,color='gray')
ax.set_ylabel("Projected Return per Cycle",fontsize=12,color='gray')
ax2.set_ylabel("Out-Sample Mean Squared Error",fontsize=12,color='gray')
ax.set_title("Projected Return per Cycle",fontsize=18,fontweight='bold',color='#000033')
ax2.set_title("Out-Sample Mean Squared Error",fontsize=18,fontweight='bold',color='#000033')
plt.show()
```


![png](images/stocks_fbprophet/output_34_0.png)


## It is still difficult to pin point the length of cycle with that volatile line graph:




```python
report = pd.DataFrame({'cycle':testing_box,'return':return_box,'mse':mse_box})
possible_choice = report[report['return'] >100]
possible_choice[possible_choice['mse']==min(possible_choice['mse'])]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>cycle</th>
      <th>return</th>
      <th>mse</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>25</th>
      <td>260</td>
      <td>103.64914</td>
      <td>16507.30357</td>
    </tr>
  </tbody>
</table>
</div>



## We can see the most ideal length of cycle would be 260 giving us a return of 104 $


```python
c = possible_choice[possible_choice['mse']==min(possible_choice['mse'])]['cycle'].values[0]
```


```python
analysis(stock_data['Close'],'2020-05-01', c , forecast_plot=True, print_ind=True)
```


![png](images/stocks_fbprophet/output_39_0.png)


    Projected return per cycle: 103.65
    MSE: 16507.3036





    [103.64914016955935, 16507.30356966114]
