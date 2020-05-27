---
title: "S&P 500 Analysis with Covid 19"
date: 2020-05-17
tags: [Data Analysis]
header:
  image: "/images/titanic_analysis/percept.jpg"
excerpt: "Data Analysis"
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




```python
#Number of companies
len(stocks_df)
```




    505




```python
stocks_df[stocks_df['Security'].str.contains("Class")].head(5)
```




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

<img src="{{ site.url }}{{ site.baseurl }}/images/stocks_covid/output_32_0.png" alt="linearly separable data">



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

<img src="{{ site.url }}{{ site.baseurl }}/images/stocks_covid/output_38_0.png" alt="linearly separable data">
