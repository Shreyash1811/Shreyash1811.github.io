---
title: "S&P 500 Analysis with Covid 19"
date: 2020-05-17
tags: [Stock Market]
categories:
- Python
header:
  image: "/images/stocks_covid/covid_header.jpg"
excerpt: "Deep diving into impact of covid on Stock Market and Schools"
mathjax: "true"
---
# Impact on S&P 500 companies with Covid 19:

### What is s&p 500?
*The S&P 500 stock market index, maintained by S&P Dow Jones Indices, comprises 505 common stocks issued by 500 large-cap companies and traded on American stock exchanges (including the 30 companies that compose the Dow Jones Industrial Average), and covers about 80 percent of the American equity market*


```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
```


```python
plt.style.use('fivethirtyeight')
```

## PART-1 of Data Acquisition:
For this analysis we will take data of s&p 500 companies from wikipedia as it contains very useful attributes of these companies.

### Requesting data from Wikipedia list of 500 companies


```python
url = 'https://en.wikipedia.org/wiki/List_of_S%26P_500_companies'

stocks_df = pd.read_html(url, header=0)[0]

stocks_df.head()
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
      <th>Symbol</th>
      <th>Security</th>
      <th>SEC filings</th>
      <th>GICS Sector</th>
      <th>GICS Sub Industry</th>
      <th>Headquarters Location</th>
      <th>Date first added</th>
      <th>CIK</th>
      <th>Founded</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>MMM</td>
      <td>3M Company</td>
      <td>reports</td>
      <td>Industrials</td>
      <td>Industrial Conglomerates</td>
      <td>St. Paul, Minnesota</td>
      <td>1976-08-09</td>
      <td>66740</td>
      <td>1902</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ABT</td>
      <td>Abbott Laboratories</td>
      <td>reports</td>
      <td>Health Care</td>
      <td>Health Care Equipment</td>
      <td>North Chicago, Illinois</td>
      <td>1964-03-31</td>
      <td>1800</td>
      <td>1888</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ABBV</td>
      <td>AbbVie Inc.</td>
      <td>reports</td>
      <td>Health Care</td>
      <td>Pharmaceuticals</td>
      <td>North Chicago, Illinois</td>
      <td>2012-12-31</td>
      <td>1551152</td>
      <td>2013 (1888)</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ABMD</td>
      <td>ABIOMED Inc</td>
      <td>reports</td>
      <td>Health Care</td>
      <td>Health Care Equipment</td>
      <td>Danvers, Massachusetts</td>
      <td>2018-05-31</td>
      <td>815094</td>
      <td>1981</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ACN</td>
      <td>Accenture plc</td>
      <td>reports</td>
      <td>Information Technology</td>
      <td>IT Consulting &amp; Other Services</td>
      <td>Dublin, Ireland</td>
      <td>2011-07-06</td>
      <td>1467373</td>
      <td>1989</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Number of companies
len(stocks_df)
```




    505




```python
stocks_df[stocks_df['Security'].str.contains("Class")].head(5)
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
      <th>Symbol</th>
      <th>Security</th>
      <th>SEC filings</th>
      <th>GICS Sector</th>
      <th>GICS Sub Industry</th>
      <th>Headquarters Location</th>
      <th>Date first added</th>
      <th>CIK</th>
      <th>Founded</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>23</th>
      <td>GOOGL</td>
      <td>Alphabet Inc. (Class A)</td>
      <td>reports</td>
      <td>Communication Services</td>
      <td>Interactive Media &amp; Services</td>
      <td>Mountain View, California</td>
      <td>2014-04-03</td>
      <td>1652044</td>
      <td>1998</td>
    </tr>
    <tr>
      <th>24</th>
      <td>GOOG</td>
      <td>Alphabet Inc. (Class C)</td>
      <td>reports</td>
      <td>Communication Services</td>
      <td>Interactive Media &amp; Services</td>
      <td>Mountain View, California</td>
      <td>2006-04-03</td>
      <td>1652044</td>
      <td>1998</td>
    </tr>
    <tr>
      <th>147</th>
      <td>DISCA</td>
      <td>Discovery, Inc. (Class A)</td>
      <td>reports</td>
      <td>Communication Services</td>
      <td>Broadcasting</td>
      <td>Silver Spring, Maryland</td>
      <td>2010-03-01</td>
      <td>1437107</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>148</th>
      <td>DISCK</td>
      <td>Discovery, Inc. (Class C)</td>
      <td>reports</td>
      <td>Communication Services</td>
      <td>Broadcasting</td>
      <td>Silver Spring, Maryland</td>
      <td>2014-08-07</td>
      <td>1437107</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>203</th>
      <td>FOXA</td>
      <td>Fox Corporation (Class A)</td>
      <td>reports</td>
      <td>Communication Services</td>
      <td>Movies &amp; Entertainment</td>
      <td>New York, New York</td>
      <td>2013-07-01</td>
      <td>1308161</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



### Data Understanding:
*Let dig a little into sectors and industries these companies come from.*

1) *Clearly! the top 5 Industries of 11 total industries cover 66% of the stocks*


```python
stocks_df['GICS Sector'].value_counts()
```




    Industrials               72
    Information Technology    71
    Financials                66
    Consumer Discretionary    63
    Health Care               61
    Consumer Staples          33
    Real Estate               31
    Materials                 28
    Utilities                 28
    Energy                    26
    Communication Services    26
    Name: GICS Sector, dtype: int64



2) Top Sub-Industries within industries are as follows
    - Health Care Equipment is at the top with big margin.


```python
stocks_df['GICS Sub Industry'].value_counts().head(10)
```




    Health Care Equipment                    20
    Industrial Machinery                     14
    Semiconductors                           13
    Electric Utilities                       13
    Data Processing & Outsourced Services    12
    Packaged Foods & Meats                   12
    Oil & Gas Exploration & Production       11
    Regional Banks                           11
    Multi-Utilities                          11
    Application Software                     11
    Name: GICS Sub Industry, dtype: int64





# PART-2 of Data Acquisition:
## Extracting their stock price data from yfinance:
Now that we have attributes of the top 500 stocks lets get the stock prices of these using yahoo finance.
-  We will be getting stock prices for 1 day of the month as going granular would be a broader analysis for another day.
-  Starting from 1-Dec-2019 to 1-May-2020 and inbetween


```python
# Importing the library
import yfinance as yf
```

#### Adding the columns we will fill with Yahoo finance data.


```python
# making require columns
stocks_df["2019-12-01"] = "NA"
stocks_df["2020-01-01"] = "NA"
stocks_df["2020-02-01"] = "NA"
stocks_df["2020-03-01"] = "NA"
stocks_df["2020-04-01"] = "NA"
stocks_df["2020-05-01"] = "NA"
stocks_df["Volume"]  = "NA"
```

#### Some of the stocks are causing a trouble with Yahoo Finance API for special characters in their names.
- We could have split them and taken out the special characters off them but since they are handful we will manually drop them.


```python
stocks_df = stocks_df.drop(stocks_df.index[[80,68,90,240,362,448]])
```


```python
fail_count = 0
name_fail = []
for stock in stocks_df["Symbol"]:
    print(stock)
    stock = str(stock)
    try:
        data = yf.download(stock, interval = "1mo",start="2019-12-01", end="2020-05-06")
    except Exception:
        fail_count+=1
        name_fail.append(stock)
        pass
    # convert Index date to column
    data.reset_index(inplace = True)
    # calculate Mid_val of stocks
    data["mid_value"] = (data["High"]+ data["Low"])/2

    # replacing value in the place
    try:
        stocks_df.loc[stocks_df["Symbol"] == stock,"2019-12-01"] = float(data.loc[data["Date"] == "2019-12-01","mid_value"])
        stocks_df.loc[stocks_df["Symbol"] == stock,"2020-01-01"] = float(data.loc[data["Date"] == "2020-01-01","mid_value"])
        stocks_df.loc[stocks_df["Symbol"] == stock,"2020-02-01"] = float(data.loc[data["Date"] == "2020-02-01","mid_value"])
        stocks_df.loc[stocks_df["Symbol"] == stock,"2020-03-01"] = float(data.loc[data["Date"] == "2020-03-01","mid_value"])
        stocks_df.loc[stocks_df["Symbol"] == stock,"2020-04-01"] = float(data.loc[data["Date"] == "2020-04-01","mid_value"])
        stocks_df.loc[stocks_df["Symbol"] == stock,"2020-05-01"] = float(data.loc[data["Date"] == "2020-05-01","mid_value"])
        stocks_df.loc[stocks_df["Symbol"] == stock,"Volume"] = float(data.loc[data["Date"] == "2020-05-01","Volume"])
    except Exception:
        fail_count+=1
        name_fail.append(stock)
        pass
```


### Some of the other important dates I had looked into for the major impacts on stock market from covid 19:
- January 2nd, 2020 is the first date of the year. We want to have this price in order to calculate the price drop since the beggining of 2020.
- March 23rd, 2020 is the date when the S&P 500 reached the bottom in 2020.

## Data Cleaning:
*Chances are that Yahoo Finance API could not get data for some of the companies and filled out dataset with inconsistencies.*


### Cleaning the data with NA :


```python
stocks_df.isnull().sum()
```




    Symbol                     0
    Security                   0
    SEC filings                0
    GICS Sector                0
    GICS Sub Industry          0
    Headquarters Location      0
    Date first added          97
    CIK                        0
    Founded                  266
    2019-12-01                 0
    2020-01-01                 0
    2020-02-01                 0
    2020-03-01                 0
    2020-04-01                 0
    2020-05-01                 0
    Volume                     0
    dtype: int64



*Some of these NA values are actually "NA" strings which can be missed out in a simple sanity check like show below*


```python
stocks_df.loc[stocks_df["2020-01-01"] == "NA"]
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
      <th>Symbol</th>
      <th>Security</th>
      <th>SEC filings</th>
      <th>GICS Sector</th>
      <th>GICS Sub Industry</th>
      <th>Headquarters Location</th>
      <th>Date first added</th>
      <th>CIK</th>
      <th>Founded</th>
      <th>2019-12-01</th>
      <th>2020-01-01</th>
      <th>2020-02-01</th>
      <th>2020-03-01</th>
      <th>2020-04-01</th>
      <th>2020-05-01</th>
      <th>Volume</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>67</th>
      <td>BRK.B</td>
      <td>Berkshire Hathaway</td>
      <td>reports</td>
      <td>Financials</td>
      <td>Multi-Sector Holdings</td>
      <td>Omaha, Nebraska</td>
      <td>2010-02-16</td>
      <td>1067983</td>
      <td>NaN</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
    </tr>
    <tr>
      <th>79</th>
      <td>BF.B</td>
      <td>Brown-Forman Corp.</td>
      <td>reports</td>
      <td>Consumer Staples</td>
      <td>Distillers &amp; Vintners</td>
      <td>Louisville, Kentucky</td>
      <td>1982-10-31</td>
      <td>14693</td>
      <td>NaN</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
    </tr>
    <tr>
      <th>88</th>
      <td>CARR</td>
      <td>Carrier Global</td>
      <td>reports</td>
      <td>Industrials</td>
      <td>Building Products</td>
      <td>Palm Beach Gardens, Florida</td>
      <td>2020-04-03</td>
      <td>1783180</td>
      <td>NaN</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
    </tr>
    <tr>
      <th>239</th>
      <td>HWM</td>
      <td>Howmet Aerospace</td>
      <td>reports</td>
      <td>Industrials</td>
      <td>Aerospace &amp; Defense</td>
      <td>New York, New York</td>
      <td>1964-03-31</td>
      <td>4281</td>
      <td>2016</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
    </tr>
    <tr>
      <th>361</th>
      <td>OTIS</td>
      <td>Otis Worldwide</td>
      <td>reports</td>
      <td>Industrials</td>
      <td>Industrial Machinery</td>
      <td>Farmington, Connecticut</td>
      <td>2020-04-03</td>
      <td>1781335</td>
      <td>NaN</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
    </tr>
    <tr>
      <th>447</th>
      <td>TT</td>
      <td>Trane Technologies plc</td>
      <td>reports</td>
      <td>Industrials</td>
      <td>Building Products</td>
      <td>Dublin, Ireland</td>
      <td>2010-11-17</td>
      <td>1466258</td>
      <td>NaN</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
    </tr>
  </tbody>
</table>
</div>



#### Lets save the data locally so that we dont have to retrieve and join them over and over again.


```python
final_df = stocks_df.copy()
```


```python
final_df.to_csv(r"C:\Users\shrey\OneDrive\Desktop\stocks.csv")
```

## Lets calculate percentage change in price from 2019-12-01 to 2020-05-01:
- This will help us compare the change in proce of different stocks relatively.


```python
final_df["pct_change_dec19_may20"] =  ((final_df["2019-12-01"] - final_df["2020-05-01"]) / final_df["2019-12-01"]) *100
```

## Basic Exploratory Analysis:


```python
plt.figure(figsize=(18, 6))
plt.tick_params('both', labelsize='12',color = 'Black')
plt.xticks(rotation=30)
sns.boxplot(x="GICS Sector", y="pct_change_dec19_may20", data=final_df,showfliers=False)
plt.ylabel("% change in price",fontsize=18,color = 'Black')
plt.xlabel("GICS Sectors",fontsize=18, color = 'Black')
plt.title("% change in S&P500 Stocks from Dec 19 to May 20",color = 'Black')
plt.tick_params('both', labelsize='12', colors="Black")
plt.tight_layout()
plt.savefig('C:/Users/shrey/OneDrive/desktop/temp.png', transparent=True)
#plt.savefig(r'C:\Users\shrey\OneDrive\Desktop\Data Engineering\Graph for Project\% change in Stocks from Dec 19 to May 20.png')
```


![png](/images/stocks_covid/output_32_0.png)


### Top 10 Sectors that got the worst hit due to Covid-19:


```python
final_df.groupby("GICS Sector").mean()['pct_change_dec19_may20'].sort_values().head(10)
```




    GICS Sector
    Health Care                0.741569
    Information Technology     6.657241
    Consumer Staples           8.342285
    Communication Services    12.529883
    Utilities                 14.561847
    Materials                 18.068353
    Industrials               20.236212
    Real Estate               23.151287
    Consumer Discretionary    27.457947
    Financials                28.482209
    Name: pct_change_dec19_may20, dtype: float64



### Deeper dive into Sub-Industries within these sectors:


```python
final_df.sort_values(by=['pct_change_dec19_may20'],inplace=True)
```


```python
final_df.groupby("GICS Sub Industry").mean()['pct_change_dec19_may20'].sort_values()[0:10]
```




    GICS Sub Industry
    Gold                                  -54.670222
    Systems Software                      -23.650745
    Wireless Telecommunication Services   -23.108069
    Food Retail                           -18.517852
    Interactive Home Entertainment        -14.974511
    Biotechnology                         -13.784027
    Financial Exchanges & Data            -11.011615
    Household Products                     -9.468149
    Application Software                   -5.821476
    Trucking                               -5.586044
    Name: pct_change_dec19_may20, dtype: float64




```python
plt.figure(figsize=(18, 6))
plt.tick_params('both', labelsize='15', color="Black")

plt.title("Top 10 Sectors that got affected the Most",fontsize=18, color='Black')
t = final_df.groupby("GICS Sub Industry").mean()['pct_change_dec19_may20'].sort_values()[0:10].plot.barh(color='midnightblue')
#plt.xticks(rotation=30)
plt.ylabel("Sub Industry",size= 20, color ="Black")
plt.tick_params('both', labelsize='25', colors="Black")
plt.tight_layout()
plt.savefig('C:/Users/shrey/OneDrive/desktop/temp.png', transparent=True)
```


![png](/images/stocks_covid/output_38_0.png)


## Time series analysis on Covid Cases:

## Data Extraction for Covid-19 cases:
*We have used an API built by herokuapp which has been consistent and accurate sourse*


```python
import pandas as pd
import numpy as np
import urllib, json
from urllib.request import urlopen
from pandas.io.json import json_normalize

import seaborn as sns

import warnings
warnings.filterwarnings('ignore')
```


```python
def build_master_df(data, label):
    frames = {}
    list_of_dfs = []

    for i in range(len(data['locations'])):
        coordinates = str(data['locations'][i]['coordinates'])
        country = data['locations'][i]['country']
        country_code = data['locations'][i]['country_code']
        province = data['locations'][i]['province']
        history = data['locations'][i]['history']
        df = pd.DataFrame(history, index=[0]).T
        df.reset_index(inplace=True)
        df.columns = ['date', 'count']
        df['date'] = pd.to_datetime(df['date'])
        df['country'] = country
        df['coordinates'] = coordinates
        df['country_code'] = country_code
        df['province'] = province

        country_key = country + '_' + str(i) # they key is never referenced elsewhere... just for building dict of df
        frames[country_key] = df # add to dict of dfs

    for key in frames.keys():
        list_of_dfs.append(frames[key]) # this needs to be key, not country key, IMPORTANT

    master_df = pd.concat(list_of_dfs)
    master_df = master_df.reset_index(drop=True)
    master_df['data_type'] = label

    return master_df
```


```python
# API
api_url = 'https://coronavirus-tracker-api.herokuapp.com/all'
# Json frame
json_data = pd.read_json(api_url)
# breaking the data
confirmed_data = json_data['confirmed']
death_data = json_data['deaths']
recovered_data = json_data['recovered']

full_confirmed_df = build_master_df(confirmed_data, 'confirmed')
full_death_df = build_master_df(death_data, 'death')
full_recovered_df = build_master_df(recovered_data, 'recovered')

full_df = pd.concat([full_confirmed_df, full_death_df, full_recovered_df])
full_df.reset_index(drop=True, inplace=True)

```

## Data Quality check:
- Check for empty values
- Check for NA values
- Check for NULL values


```python
full_df.isin([" ","NA", "NULL"]).sum()
```




    date              0
    count             0
    country           0
    coordinates       0
    country_code    375
    province          0
    data_type         0
    dtype: int64




```python
#Preview of the dataframe
full_df.head()
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
      <th>date</th>
      <th>count</th>
      <th>country</th>
      <th>coordinates</th>
      <th>country_code</th>
      <th>province</th>
      <th>data_type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020-01-22</td>
      <td>0</td>
      <td>Afghanistan</td>
      <td>{'lat': '33.0', 'long': '65.0'}</td>
      <td>AF</td>
      <td></td>
      <td>confirmed</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020-01-23</td>
      <td>0</td>
      <td>Afghanistan</td>
      <td>{'lat': '33.0', 'long': '65.0'}</td>
      <td>AF</td>
      <td></td>
      <td>confirmed</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2020-01-24</td>
      <td>0</td>
      <td>Afghanistan</td>
      <td>{'lat': '33.0', 'long': '65.0'}</td>
      <td>AF</td>
      <td></td>
      <td>confirmed</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2020-01-25</td>
      <td>0</td>
      <td>Afghanistan</td>
      <td>{'lat': '33.0', 'long': '65.0'}</td>
      <td>AF</td>
      <td></td>
      <td>confirmed</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020-01-26</td>
      <td>0</td>
      <td>Afghanistan</td>
      <td>{'lat': '33.0', 'long': '65.0'}</td>
      <td>AF</td>
      <td></td>
      <td>confirmed</td>
    </tr>
  </tbody>
</table>
</div>



### Grouping data by country:
- Collecting aggregates for deaths, Confirmed cases and recovered.


```python
# Aggregate of confirmed
full_agg_confirm = full_confirmed_df.groupby("country").agg(sum_confirmed=('count','sum'))
# Agg of deaths
full_agg_deaths = full_death_df.groupby("country").agg(sum_death=('count','sum'))
# Agg of recovered
full_agg_recovered = full_recovered_df.groupby("country").agg(sum_recovered=('count','sum'))
```

Data count on each DataFrame Matches, which is perfect for us.


```python
# all the built dataframes has all the country
print(len(full_agg_confirm.index))
print(len(full_agg_deaths.index))
print(len(full_agg_recovered.index))
```

    188
    188
    188


### Merging data with total Confirm cases, Deaths and Recovered by country to for one DataFrame to work with.


```python
# Merge columns
merged_covid_Df = full_agg_confirm.merge(full_agg_deaths, left_index=True, right_index=True)
merged_covid_Df = merged_covid_Df.merge(full_agg_recovered,left_index=True, right_index=True)
#reset index
merged_covid_Df.reset_index(inplace=True)
```


```python
# Preview of the dataframe
merged_covid_Df.head(5)
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
      <th>country</th>
      <th>sum_confirmed</th>
      <th>sum_death</th>
      <th>sum_recovered</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan</td>
      <td>173405</td>
      <td>4449</td>
      <td>19717</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Albania</td>
      <td>40224</td>
      <td>1596</td>
      <td>24885</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Algeria</td>
      <td>231373</td>
      <td>22615</td>
      <td>102427</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Andorra</td>
      <td>40810</td>
      <td>2168</td>
      <td>20075</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Angola</td>
      <td>1822</td>
      <td>127</td>
      <td>488</td>
    </tr>
  </tbody>
</table>
</div>




### More demogrphics data like
- population by age group
- GDP
- Impact on Schools (Closed,Opened)

*I collected these data points from government census data sources.*



```python
# importing the data
df = pd.read_excel(r"C:\Users\shrey\OneDrive\Desktop\BE_NEWDATA.xlsx", na_values=" ")
# Picking the columns we require
df = df.loc[:,["Country","Region Extended","GDP 2018 ($)","Statusof Schools","Population in age range 50-100"]]
```


```python
#merging using unique key we created
merged_covid_Df= pd.merge(left=df, right=merged_covid_Df, left_on='Country', right_on='country')
```

### Quick Data Quality Check:


```python
merged_covid_Df.isnull().sum()
```




    Country                           0
    Region Extended                   0
    GDP 2018 ($)                      5
    Statusof Schools                  6
    Population in age range 50-100    7
    country                           0
    sum_confirmed                     0
    sum_death                         0
    sum_recovered                     0
    dtype: int64




```python
merged_covid_Df.head()
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
      <th>Country</th>
      <th>Region Extended</th>
      <th>GDP 2018 ($)</th>
      <th>Statusof Schools</th>
      <th>Population in age range 50-100</th>
      <th>country</th>
      <th>sum_confirmed</th>
      <th>sum_death</th>
      <th>sum_recovered</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan</td>
      <td>South Asia</td>
      <td>2.700559e+09</td>
      <td>Closed</td>
      <td>3484.074</td>
      <td>Afghanistan</td>
      <td>173405</td>
      <td>4449</td>
      <td>19717</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Albania</td>
      <td>Europe &amp; Central Asia</td>
      <td>1.936297e+10</td>
      <td>Closed</td>
      <td>995.719</td>
      <td>Albania</td>
      <td>40224</td>
      <td>1596</td>
      <td>24885</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Algeria</td>
      <td>Middle East &amp; North Africa</td>
      <td>1.057510e+11</td>
      <td>Closed</td>
      <td>8144.237</td>
      <td>Algeria</td>
      <td>231373</td>
      <td>22615</td>
      <td>102427</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Andorra</td>
      <td>Europe &amp; Central Asia</td>
      <td>3.236544e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Andorra</td>
      <td>40810</td>
      <td>2168</td>
      <td>20075</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Angola</td>
      <td>Sub-Saharan Africa</td>
      <td>2.774315e+12</td>
      <td>Closed</td>
      <td>2666.820</td>
      <td>Angola</td>
      <td>1822</td>
      <td>127</td>
      <td>488</td>
    </tr>
  </tbody>
</table>
</div>



## Clustering of countries with the data points on covid and census data:


```python
# make copy of merged covid data
cluster_df = merged_covid_Df.copy()
# Dropping repeatinf columns
cluster_df.drop("country",axis=1, inplace= True)
```


```python
cluster_df.loc[cluster_df["Region Extended"] == "North America",'sum_recovered'].sum()
```




    1961650



### As we can see a lot of the data points are categorical columns, we will encode it.


```python
# Converting column to category column
cluster_df["Statusof Schools"] = pd.Categorical(cluster_df["Statusof Schools"])
# Giving category codes
cluster_df['Statusof Schools'] = cluster_df["Statusof Schools"].cat.codes

```


```python
# Converting column to category column
cluster_df["Region Extended"] = pd.Categorical(cluster_df["Region Extended"])
# Giving category codes
cluster_df['Region Extended'] = cluster_df["Region Extended"].cat.codes

```


```python
cluster_df.head(5)
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
      <th>Country</th>
      <th>Region Extended</th>
      <th>GDP 2018 ($)</th>
      <th>Statusof Schools</th>
      <th>Population in age range 50-100</th>
      <th>sum_confirmed</th>
      <th>sum_death</th>
      <th>sum_recovered</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan</td>
      <td>5</td>
      <td>2.700559e+09</td>
      <td>0</td>
      <td>3484.074</td>
      <td>173405</td>
      <td>4449</td>
      <td>19717</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Albania</td>
      <td>1</td>
      <td>1.936297e+10</td>
      <td>0</td>
      <td>995.719</td>
      <td>40224</td>
      <td>1596</td>
      <td>24885</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Algeria</td>
      <td>3</td>
      <td>1.057510e+11</td>
      <td>0</td>
      <td>8144.237</td>
      <td>231373</td>
      <td>22615</td>
      <td>102427</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Andorra</td>
      <td>1</td>
      <td>3.236544e+09</td>
      <td>-1</td>
      <td>NaN</td>
      <td>40810</td>
      <td>2168</td>
      <td>20075</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Angola</td>
      <td>6</td>
      <td>2.774315e+12</td>
      <td>0</td>
      <td>2666.820</td>
      <td>1822</td>
      <td>127</td>
      <td>488</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Making country as index
cluster_df.set_index(["Country"], inplace=True)
```


```python
# Columns in the clustered dataframe
cluster_df.columns
```




    Index(['Region Extended', 'GDP 2018 ($)', 'Statusof Schools',
           'Population in age range 50-100', 'sum_confirmed', 'sum_death',
           'sum_recovered'],
          dtype='object')



**Checking Null values:**


```python
cluster_df.isnull().sum()
```




    Region Extended                   0
    GDP 2018 ($)                      5
    Statusof Schools                  0
    Population in age range 50-100    7
    sum_confirmed                     0
    sum_death                         0
    sum_recovered                     0
    dtype: int64



#### Some of the value places are empty spaces and would not get caught in NA or NULL checks:
- Replacing these empty strings to be NA


```python
cluster_df['Population in age range 50-100'].replace(' ', np.nan, inplace=True)
```

#### Droping rows with na values:


```python
cluster_df = cluster_df.dropna(how='any',axis=0)
```


```python
cluster_df.isnull().sum()
```




    Region Extended                   0
    GDP 2018 ($)                      0
    Statusof Schools                  0
    Population in age range 50-100    0
    sum_confirmed                     0
    sum_death                         0
    sum_recovered                     0
    dtype: int64



#### We have data on 156 countries:


```python
len(cluster_df.index)
```




    156



### Scaling the data to one range to avoid attributes from dominating:


```python
#scaling the data
# load module and instantiate scaler object
from sklearn.preprocessing import MinMaxScaler

cols = cluster_df.columns
# Make object of MinMaxScaler model
scaler = MinMaxScaler()

# Normalize the data and store in out_scaled
out_scaled = scaler.fit_transform(cluster_df[cols])

# Preview of normalized values
print("Normalised Data Values: \n",out_scaled[0:5])
```

    Normalised Data Values:
     [[8.33333333e-01 4.90348974e-05 2.50000000e-01 7.33224592e-03
      1.48629645e-02 2.89776535e-03 2.94410750e-03]
     [1.66666667e-01 3.56427133e-04 2.50000000e-01 2.05962014e-03
      3.44657770e-03 1.03952203e-03 3.71578410e-03]
     [5.00000000e-01 1.95013444e-03 2.50000000e-01 1.72067596e-02
      1.98320300e-02 1.47298187e-02 1.52942181e-02]
     [1.00000000e+00 5.11804559e-02 2.50000000e-01 5.60054987e-03
      1.54726111e-04 8.27188581e-05 7.28672952e-05]
     [3.33333333e-01 7.64008885e-03 2.50000000e-01 6.19784171e-06
      1.10236997e-04 8.92321541e-05 8.54100264e-05]]



```python
# Replacing scalled in the data frame
scaled_df_cluster = pd.DataFrame(out_scaled, columns= cols)
```


```python
scaled_df_cluster.head()
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
      <th>Region Extended</th>
      <th>GDP 2018 ($)</th>
      <th>Statusof Schools</th>
      <th>Population in age range 50-100</th>
      <th>sum_confirmed</th>
      <th>sum_death</th>
      <th>sum_recovered</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.833333</td>
      <td>0.000049</td>
      <td>0.25</td>
      <td>0.007332</td>
      <td>0.014863</td>
      <td>0.002898</td>
      <td>0.002944</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.166667</td>
      <td>0.000356</td>
      <td>0.25</td>
      <td>0.002060</td>
      <td>0.003447</td>
      <td>0.001040</td>
      <td>0.003716</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.500000</td>
      <td>0.001950</td>
      <td>0.25</td>
      <td>0.017207</td>
      <td>0.019832</td>
      <td>0.014730</td>
      <td>0.015294</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.000000</td>
      <td>0.051180</td>
      <td>0.25</td>
      <td>0.005601</td>
      <td>0.000155</td>
      <td>0.000083</td>
      <td>0.000073</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.333333</td>
      <td>0.007640</td>
      <td>0.25</td>
      <td>0.000006</td>
      <td>0.000110</td>
      <td>0.000089</td>
      <td>0.000085</td>
    </tr>
  </tbody>
</table>
</div>



## Making Clusters :


```python

# import module and instantiate K-means object
from sklearn.cluster import KMeans
clus = KMeans(n_clusters=10, tol=0.004, max_iter=300)

# fit to input main Dataframe
df = scaled_df_cluster.copy()

clus.fit(df)

# get cluster assignments of input data and print first five labels
df['K-means Cluster Labels'] = clus.labels_
print(df['K-means Cluster Labels'][:5].tolist())
```

    [1, 0, 4, 1, 4]


### Dimensionality Reduction:
Since the dataset has high dimensionality visualisation is difficult.
- We use PCA to reduce the dimensions to 2 points.


```python
# PCA for visualisation
from sklearn.decomposition import PCA
pca = PCA(n_components=2)
pca.fit(df.iloc[:,0:6])

new_pca = pca.fit_transform( df.iloc[:,0:6] , y=None)
```


```python
cluster_pca_data = pd.DataFrame(new_pca, columns=["pca_1","pca_2"])
```


```python
cluster_pca_data["country"] = cluster_df.index

cluster_pca_data["K-means Cluster Labels"] = df["K-means Cluster Labels"]
```


```python
cluster_pca_data
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
      <th>pca_1</th>
      <th>pca_2</th>
      <th>country</th>
      <th>K-means Cluster Labels</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.348706</td>
      <td>0.018476</td>
      <td>Afghanistan</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.300912</td>
      <td>-0.130703</td>
      <td>Albania</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.020217</td>
      <td>-0.038411</td>
      <td>Algeria</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.515938</td>
      <td>0.036884</td>
      <td>Angola</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.136985</td>
      <td>-0.099933</td>
      <td>Antigua and Barbuda</td>
      <td>4</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>151</th>
      <td>0.527647</td>
      <td>0.952394</td>
      <td>United Kingdom</td>
      <td>3</td>
    </tr>
    <tr>
      <th>152</th>
      <td>0.302074</td>
      <td>-0.125504</td>
      <td>Uzbekistan</td>
      <td>0</td>
    </tr>
    <tr>
      <th>153</th>
      <td>-0.025728</td>
      <td>-0.064047</td>
      <td>Yemen</td>
      <td>4</td>
    </tr>
    <tr>
      <th>154</th>
      <td>-0.514466</td>
      <td>0.040480</td>
      <td>Zambia</td>
      <td>1</td>
    </tr>
    <tr>
      <th>155</th>
      <td>-0.514651</td>
      <td>0.039656</td>
      <td>Zimbabwe</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>156 rows × 4 columns</p>
</div>



### Visualizing the clusters:


```python
import plotly.express as px
fig = px.scatter_3d(cluster_pca_data, x='pca_1', y='pca_2', z='K-means Cluster Labels',
              symbol ='K-means Cluster Labels', color='country' )
fig.show()
```


```python
fig.write_image(r"C:\Users\shrey\OneDrive\Desktop\fig1.webp")
```


```python
cluster_pca_data.set_index(["country"],inplace=True )
```

## Dendogram for the country:


```python
# plot
# import scipy module
from scipy.cluster import hierarchy
```


```python
# Calculate the distance between each sample
Z = hierarchy.linkage(cluster_pca_data, 'ward')
```


```python
# Plot with Custom leaves (scroll down in console to see plot)
plt.figure(figsize=(20,20))
hierarchy.dendrogram(Z, leaf_rotation=0, leaf_font_size=8, labels=cluster_pca_data.index,orientation = 'right' )
plt.ylabel("Sub Industry",size= 20, color ="white")
plt.tick_params('both', labelsize='14', colors="Black")
plt.tight_layout()
plt.grid(False)
plt.savefig(r"C:\Users\shrey\OneDrive\Desktop\dendogram.png", format='png', bbox_inches='tight',transparent =True )
```


![png](/images/stocks_covid/output_96_0.png)


## Insights on Demographics and Covid cases with Regions:


```python
plt.figure(figsize=(18, 6))

plt.xticks(rotation=30)
plt.title("Spread of Confirmed cases with Country Regions",fontsize=18,color="Black")
sns.boxplot(x="Region Extended", y="sum_confirmed", data=merged_covid_Df,showfliers=False, )
plt.ylabel("Count of Confirmed cases",fontsize=18, color ='Black')
plt.xlabel("Global Regions",fontsize=18)
plt.tick_params('both', labelsize='15',colors="Black",color ='Black')
plt.tight_layout()
plt.savefig('C:/Users/shrey/OneDrive/desktop/temp.png', transparent=True)
```


![png](/images/stocks_covid/output_98_0.png)



```python
sns.set(style="whitegrid")
sns.set(color_codes=True)
plt.figure(figsize=(18, 6))
plt.tick_params('both', labelsize='15')
plt.title("Distribution of Recovered Cases by Region", fontsize = 18)
plt.xticks(rotation=30)
sns.boxplot(x="Region Extended", y="sum_recovered", data=merged_covid_Df,showfliers=False)
plt.ylabel("Count of Recovered cases",fontsize = 18)
plt.xlabel("Global Regions", fontsize = 18)
```




    Text(0.5, 0, 'Global Regions')




![png](/images/stocks_covid/output_99_1.png)



```python
sns.catplot(x="Region Extended", y="sum_recovered", data=merged_covid_Df,showfliers=False,
            row="Statusof Schools", kind="box",
                height=4, aspect=4)
plt.ylabel("Sum of Recovered cases",fontsize = 18)
plt.xlabel("Global Regions", fontsize = 18)
plt.title("Status of Schools in regions with Recovered Cases")
plt.xticks(rotation=30)
plt.ylabel("Sub Industry",size= 20, color ="Black")
plt.tick_params('both', labelsize='25', colors="Black")
#plt.tight_layout()
plt.savefig('C:/Users/shrey/OneDrive/desktop/temp.png', transparent=True)
#plt.savefig(r'C:\Users\shrey\OneDrive\Desktop\Data Engineering\Graph for Project\Status of Schools in regions with Recovered Cases.png')
```


![png](/images/stocks_covid/output_100_0.png)


## Time Series analysis for Corona cases:
### Data Preparation:
**Since our data was aggregated by Country and not date, we need to aggregate it by date to proceed with Time Series Analysis**

#### We will make unique key combining Date and Country to make datasets for each country by date:


```python
# Making Unique key combining Country and Date
full_confirmed_df["key"] = full_confirmed_df["date"].astype(str) +full_confirmed_df["country"]
full_death_df["key"] = full_death_df["date"].astype(str) +full_death_df["country"]
full_recovered_df["key"] = full_recovered_df["date"].astype(str) +full_recovered_df["country"]
#removing redundant data from other two columns
full_death_df=full_death_df.drop(["province","country_code","data_type","date"],axis =1)
full_recovered_df=full_recovered_df.drop(["province","country_code","data_type","date"],axis =1)
# Changing count column for all dataframes
full_confirmed_df.rename(columns={'count': 'confirmed_count'}, inplace=True)
full_death_df.rename(columns={'count': 'death_count'}, inplace=True)
full_recovered_df.rename(columns={'count': 'recovered_count'}, inplace=True)
#merging using unique key we created
full_date_data= pd.merge(left=full_confirmed_df, right=full_death_df, left_on='key', right_on='key')
full_date_data = pd.merge(left=full_date_data, right=full_recovered_df, left_on='key', right_on='key')
#dropping unwanted columns
full_date_data.drop(['country_x','coordinates_x','coordinates_y','data_type','country_y','key','coordinates'],axis=1,
                    inplace=True)
```

# Preview of the data:


```python
# Function to get timeseries data for each country
def country_time_series(country):

    return full_date_data.loc[full_date_data["country"] == country]
```


```python
# Preview
country_time_series("Afghanistan").tail(3)
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
      <th>date</th>
      <th>confirmed_count</th>
      <th>country_code</th>
      <th>province</th>
      <th>death_count</th>
      <th>recovered_count</th>
      <th>country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>122</th>
      <td>2020-05-23</td>
      <td>9998</td>
      <td>AF</td>
      <td></td>
      <td>216</td>
      <td>1040</td>
      <td>Afghanistan</td>
    </tr>
    <tr>
      <th>123</th>
      <td>2020-05-24</td>
      <td>10582</td>
      <td>AF</td>
      <td></td>
      <td>218</td>
      <td>1075</td>
      <td>Afghanistan</td>
    </tr>
    <tr>
      <th>124</th>
      <td>2020-05-25</td>
      <td>11173</td>
      <td>AF</td>
      <td></td>
      <td>219</td>
      <td>1097</td>
      <td>Afghanistan</td>
    </tr>
  </tbody>
</table>
</div>



## Aggregating data by dates to see global trend in cases:


```python
# Grouping and egg data by date to see impact as whole
df_timeseries = full_date_data.groupby("date").agg(count_death=('death_count','sum'),
                                                count_recovered=('recovered_count','sum'),
                                                  count_confirmed=('confirmed_count','sum'))
```


```python
df_timeseries.reset_index(inplace = True)
# Preview
df_timeseries.head()
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
      <th>date</th>
      <th>count_death</th>
      <th>count_recovered</th>
      <th>count_confirmed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020-01-22</td>
      <td>18513</td>
      <td>30492</td>
      <td>596779</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020-01-23</td>
      <td>19602</td>
      <td>32670</td>
      <td>700238</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2020-01-24</td>
      <td>28314</td>
      <td>39204</td>
      <td>1002141</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2020-01-25</td>
      <td>45738</td>
      <td>42471</td>
      <td>1531522</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020-01-26</td>
      <td>60984</td>
      <td>53364</td>
      <td>2260343</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_timeseries.to_csv(r"C:\Users\shrey\OneDrive\Desktop\timeseries_data.csv")
```


```python
plt.figure(figsize=(10, 8))
plt.plot(df_timeseries["date"],df_timeseries["count_confirmed"]  ,'#253b61', label = 'confirm cases')
plt.plot(df_timeseries["date"],df_timeseries["count_death"] , '#ef4349', label = 'Deaths')
plt.plot(df_timeseries["date"],df_timeseries["count_recovered"]  ,'#f3797e', label = 'Recovered cases')

plt.xticks(rotation=30);
plt.ylabel('Cases Counts', fontsize = 18, color='black');
plt.title('Confirm cases vs recovered vs Deaths', fontsize= 30, color = 'black')
plt.legend();
plt.ylabel("Count of Confirmed cases",fontsize=18, color ='black')
plt.xlabel("Time Line",fontsize=18,color='black')
plt.tick_params('both', labelsize='15',colors="black",color ='black')
plt.tight_layout()
plt.grid(False)
plt.savefig('C:/Users/shrey/OneDrive/desktop/temp.png', transparent=True)
#plt.savefig(r'C:\Users\shrey\OneDrive\Desktop\Data Engineering\Graph for Project\Corona Cases Deaths Recovered.png')
```


![png](/images/stocks_covid/output_111_0.png)


### Insights from trendline:
#### - We can see how death cases are increasing with the lowest rate while Confirm cases have highest rate.

#### - We see a strong curve in recovered and confirm cases showing a flattening of the curve after 2020-02-15.
