---
title: "Introduction to md "
date: 2020-03-31
tags: [Face Recognition]
header:
  image: "/images/face_rec/face_header.jpg"
excerpt: " libraries"
mathjax: "true"
---

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
```


```python
plt.style.use('fivethirtyeight')
```

# S&P 500 companies analysis:

# Requesting data from Wikipedia list of 500 companies


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
#Number of companis
len(stocks_df)
```




    505




```python
stocks_df[stocks_df['Security'].str.contains("Class")]
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
      <th>24</th>
      <td>GOOGL</td>
      <td>Alphabet Inc Class A</td>
      <td>reports</td>
      <td>Communication Services</td>
      <td>Interactive Media &amp; Services</td>
      <td>Mountain View, California</td>
      <td>2014-04-03</td>
      <td>1652044</td>
      <td>1998</td>
    </tr>
    <tr>
      <th>25</th>
      <td>GOOG</td>
      <td>Alphabet Inc Class C</td>
      <td>reports</td>
      <td>Communication Services</td>
      <td>Interactive Media &amp; Services</td>
      <td>Mountain View, California</td>
      <td>2006-04-03</td>
      <td>1652044</td>
      <td>1998</td>
    </tr>
    <tr>
      <th>148</th>
      <td>DISCA</td>
      <td>Discovery Inc. Class A</td>
      <td>reports</td>
      <td>Communication Services</td>
      <td>Broadcasting</td>
      <td>Silver Spring, Maryland</td>
      <td>2010-03-01</td>
      <td>1437107</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>149</th>
      <td>DISCK</td>
      <td>Discovery Inc. Class C</td>
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
      <td>Fox Corporation Class A</td>
      <td>reports</td>
      <td>Communication Services</td>
      <td>Movies &amp; Entertainment</td>
      <td>New York, New York</td>
      <td>2013-07-01</td>
      <td>1308161</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>204</th>
      <td>FOX</td>
      <td>Fox Corporation Class B</td>
      <td>reports</td>
      <td>Communication Services</td>
      <td>Movies &amp; Entertainment</td>
      <td>New York, New York</td>
      <td>2015-09-18</td>
      <td>1308161</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>339</th>
      <td>NWSA</td>
      <td>News Corp. Class A</td>
      <td>reports</td>
      <td>Communication Services</td>
      <td>Publishing</td>
      <td>New York, New York</td>
      <td>2013-08-01</td>
      <td>1564708</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>340</th>
      <td>NWS</td>
      <td>News Corp. Class B</td>
      <td>reports</td>
      <td>Communication Services</td>
      <td>Publishing</td>
      <td>New York, New York</td>
      <td>2015-09-18</td>
      <td>1564708</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>457</th>
      <td>UAA</td>
      <td>Under Armour Class A</td>
      <td>reports</td>
      <td>Consumer Discretionary</td>
      <td>Apparel, Accessories &amp; Luxury Goods</td>
      <td>Baltimore, Maryland</td>
      <td>2014-05-01</td>
      <td>1336917</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>458</th>
      <td>UA</td>
      <td>Under Armour Class C</td>
      <td>reports</td>
      <td>Consumer Discretionary</td>
      <td>Apparel, Accessories &amp; Luxury Goods</td>
      <td>Baltimore, Maryland</td>
      <td>2016-04-08</td>
      <td>1336917</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
stocks_df['GICS Sector'].value_counts()
```




    Industrials               72
    Information Technology    71
    Financials                66
    Consumer Discretionary    63
    Health Care               60
    Consumer Staples          33
    Real Estate               31
    Utilities                 28
    Materials                 28
    Energy                    27
    Communication Services    26
    Name: GICS Sector, dtype: int64




```python
stocks_df['GICS Sub Industry'].value_counts()
```




    Health Care Equipment                    19
    Industrial Machinery                     14
    Semiconductors                           13
    Electric Utilities                       13
    Data Processing & Outsourced Services    12
                                             ..
    Water Utilities                           1
    Household Appliances                      1
    Metal & Glass Containers                  1
    Specialized Consumer Services             1
    Housewares & Specialties                  1
    Name: GICS Sub Industry, Length: 128, dtype: int64



# Extracting their stock price data from yfinance:


```python
# Importing the library
import yfinance as yf
```


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

- January 2nd, 2020 is the first date of the year. We want to have this price in order to calculate the price drop since the beggining of 2020.
- March 23rd, 2020 is the date when the S&P 500 reached the bottom in 2020.
- May 05 Last date when I made this code

# Cleaning the data with NA


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
      <th>367</th>
      <td>PAYC</td>
      <td>Paycom</td>
      <td>reports</td>
      <td>Information Technology</td>
      <td>Application Software</td>
      <td>Oklahoma City, Oklahoma</td>
      <td>2020-01-28</td>
      <td>1590955</td>
      <td>1998</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
    </tr>
    <tr>
      <th>380</th>
      <td>PPG</td>
      <td>PPG Industries</td>
      <td>reports</td>
      <td>Materials</td>
      <td>Specialty Chemicals</td>
      <td>Pittsburgh, Pennsylvania</td>
      <td>NaN</td>
      <td>79879</td>
      <td>1883</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
      <td>NA</td>
    </tr>
    <tr>
      <th>439</th>
      <td>TEL</td>
      <td>TE Connectivity Ltd.</td>
      <td>reports</td>
      <td>Information Technology</td>
      <td>Electronic Manufacturing Services</td>
      <td>Schaffhausen, Switzerland</td>
      <td>2011-10-17</td>
      <td>1385157</td>
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




```python
#Preview of the dataframe
stocks_df
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
      <td>170.95</td>
      <td>170.39</td>
      <td>155.505</td>
      <td>134.39</td>
      <td>147.045</td>
      <td>147.47</td>
      <td>1.23948e+07</td>
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
      <td>86.255</td>
      <td>88.23</td>
      <td>82.05</td>
      <td>73.005</td>
      <td>87.675</td>
      <td>91.625</td>
      <td>3.01279e+07</td>
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
      <td>88.79</td>
      <td>85.35</td>
      <td>89.39</td>
      <td>77.205</td>
      <td>78.7</td>
      <td>84.325</td>
      <td>5.94375e+07</td>
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
      <td>179.77</td>
      <td>175.63</td>
      <td>173.27</td>
      <td>142.255</td>
      <td>169.285</td>
      <td>185.01</td>
      <td>2.8725e+06</td>
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
      <td>204.86</td>
      <td>207.555</td>
      <td>195.845</td>
      <td>164.525</td>
      <td>168.225</td>
      <td>182.155</td>
      <td>9.1669e+06</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>500</th>
      <td>YUM</td>
      <td>Yum! Brands Inc</td>
      <td>reports</td>
      <td>Consumer Discretionary</td>
      <td>Restaurants</td>
      <td>Louisville, Kentucky</td>
      <td>1997-10-06</td>
      <td>1041061</td>
      <td>NaN</td>
      <td>100.115</td>
      <td>103.455</td>
      <td>97.59</td>
      <td>74.92</td>
      <td>76.345</td>
      <td>83.32</td>
      <td>9.2675e+06</td>
    </tr>
    <tr>
      <th>501</th>
      <td>ZBRA</td>
      <td>Zebra Technologies</td>
      <td>reports</td>
      <td>Information Technology</td>
      <td>Electronic Equipment &amp; Instruments</td>
      <td>Lincolnshire, Illinois</td>
      <td>2019-12-23</td>
      <td>877212</td>
      <td>1969</td>
      <td>252.15</td>
      <td>249.63</td>
      <td>229.71</td>
      <td>188.585</td>
      <td>209.42</td>
      <td>228.735</td>
      <td>1.5415e+06</td>
    </tr>
    <tr>
      <th>502</th>
      <td>ZBH</td>
      <td>Zimmer Biomet Holdings</td>
      <td>reports</td>
      <td>Health Care</td>
      <td>Health Care Equipment</td>
      <td>Warsaw, Indiana</td>
      <td>2001-08-07</td>
      <td>1136869</td>
      <td>NaN</td>
      <td>147.17</td>
      <td>148.73</td>
      <td>146.81</td>
      <td>108.41</td>
      <td>105.55</td>
      <td>116.965</td>
      <td>6.2742e+06</td>
    </tr>
    <tr>
      <th>503</th>
      <td>ZION</td>
      <td>Zions Bancorp</td>
      <td>reports</td>
      <td>Financials</td>
      <td>Regional Banks</td>
      <td>Salt Lake City, Utah</td>
      <td>2001-06-22</td>
      <td>109380</td>
      <td>NaN</td>
      <td>50.055</td>
      <td>48.94</td>
      <td>43.755</td>
      <td>32.46</td>
      <td>28.625</td>
      <td>30.53</td>
      <td>1.67335e+07</td>
    </tr>
    <tr>
      <th>504</th>
      <td>ZTS</td>
      <td>Zoetis</td>
      <td>reports</td>
      <td>Health Care</td>
      <td>Pharmaceuticals</td>
      <td>Florham Park, New Jersey</td>
      <td>2013-06-21</td>
      <td>1555280</td>
      <td>1952</td>
      <td>125.83</td>
      <td>137.405</td>
      <td>136.63</td>
      <td>116.92</td>
      <td>121.145</td>
      <td>127.805</td>
      <td>1.25098e+07</td>
    </tr>
  </tbody>
</table>
<p>499 rows × 16 columns</p>
</div>



# Lets calculate change in price from 2019-12-01 to 2020-05-01


```python
final_df = stocks_df.copy()
```


```python
final_df.to_csv(r"C:\Users\shrey\OneDrive\Desktop\stocks.csv")
```


```python
final_df = pd.read_csv(r"C:\Users\shrey\OneDrive\Desktop\stocks.csv")
```


```python
final_df
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
      <th>Unnamed: 0</th>
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
      <th>0</th>
      <td>0</td>
      <td>MMM</td>
      <td>3M Company</td>
      <td>reports</td>
      <td>Industrials</td>
      <td>Industrial Conglomerates</td>
      <td>St. Paul, Minnesota</td>
      <td>1976-08-09</td>
      <td>66740</td>
      <td>1902</td>
      <td>170.949997</td>
      <td>170.389999</td>
      <td>155.504997</td>
      <td>134.390003</td>
      <td>147.044998</td>
      <td>147.469994</td>
      <td>12394800.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>ABT</td>
      <td>Abbott Laboratories</td>
      <td>reports</td>
      <td>Health Care</td>
      <td>Health Care Equipment</td>
      <td>North Chicago, Illinois</td>
      <td>1964-03-31</td>
      <td>1800</td>
      <td>1888</td>
      <td>86.254997</td>
      <td>88.230000</td>
      <td>82.049999</td>
      <td>73.005001</td>
      <td>87.674999</td>
      <td>91.625000</td>
      <td>30127900.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>ABBV</td>
      <td>AbbVie Inc.</td>
      <td>reports</td>
      <td>Health Care</td>
      <td>Pharmaceuticals</td>
      <td>North Chicago, Illinois</td>
      <td>2012-12-31</td>
      <td>1551152</td>
      <td>2013 (1888)</td>
      <td>88.789997</td>
      <td>85.350002</td>
      <td>89.389999</td>
      <td>77.205000</td>
      <td>78.700001</td>
      <td>84.325001</td>
      <td>59437500.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>ABMD</td>
      <td>ABIOMED Inc</td>
      <td>reports</td>
      <td>Health Care</td>
      <td>Health Care Equipment</td>
      <td>Danvers, Massachusetts</td>
      <td>2018-05-31</td>
      <td>815094</td>
      <td>1981</td>
      <td>179.769997</td>
      <td>175.630005</td>
      <td>173.269997</td>
      <td>142.255001</td>
      <td>169.284996</td>
      <td>185.010002</td>
      <td>2872500.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>ACN</td>
      <td>Accenture plc</td>
      <td>reports</td>
      <td>Information Technology</td>
      <td>IT Consulting &amp; Other Services</td>
      <td>Dublin, Ireland</td>
      <td>2011-07-06</td>
      <td>1467373</td>
      <td>1989</td>
      <td>204.860001</td>
      <td>207.555000</td>
      <td>195.845001</td>
      <td>164.524994</td>
      <td>168.224998</td>
      <td>182.154999</td>
      <td>9166900.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>494</th>
      <td>500</td>
      <td>YUM</td>
      <td>Yum! Brands Inc</td>
      <td>reports</td>
      <td>Consumer Discretionary</td>
      <td>Restaurants</td>
      <td>Louisville, Kentucky</td>
      <td>1997-10-06</td>
      <td>1041061</td>
      <td>NaN</td>
      <td>100.114998</td>
      <td>103.455002</td>
      <td>97.590000</td>
      <td>74.920000</td>
      <td>76.344999</td>
      <td>83.320004</td>
      <td>9267500.0</td>
    </tr>
    <tr>
      <th>495</th>
      <td>501</td>
      <td>ZBRA</td>
      <td>Zebra Technologies</td>
      <td>reports</td>
      <td>Information Technology</td>
      <td>Electronic Equipment &amp; Instruments</td>
      <td>Lincolnshire, Illinois</td>
      <td>2019-12-23</td>
      <td>877212</td>
      <td>1969</td>
      <td>252.149994</td>
      <td>249.629997</td>
      <td>229.709999</td>
      <td>188.584999</td>
      <td>209.420006</td>
      <td>228.735001</td>
      <td>1541500.0</td>
    </tr>
    <tr>
      <th>496</th>
      <td>502</td>
      <td>ZBH</td>
      <td>Zimmer Biomet Holdings</td>
      <td>reports</td>
      <td>Health Care</td>
      <td>Health Care Equipment</td>
      <td>Warsaw, Indiana</td>
      <td>2001-08-07</td>
      <td>1136869</td>
      <td>NaN</td>
      <td>147.169998</td>
      <td>148.729996</td>
      <td>146.809998</td>
      <td>108.410000</td>
      <td>105.549999</td>
      <td>116.965000</td>
      <td>6274200.0</td>
    </tr>
    <tr>
      <th>497</th>
      <td>503</td>
      <td>ZION</td>
      <td>Zions Bancorp</td>
      <td>reports</td>
      <td>Financials</td>
      <td>Regional Banks</td>
      <td>Salt Lake City, Utah</td>
      <td>2001-06-22</td>
      <td>109380</td>
      <td>NaN</td>
      <td>50.055000</td>
      <td>48.940001</td>
      <td>43.754999</td>
      <td>32.460000</td>
      <td>28.625000</td>
      <td>30.530000</td>
      <td>16733500.0</td>
    </tr>
    <tr>
      <th>498</th>
      <td>504</td>
      <td>ZTS</td>
      <td>Zoetis</td>
      <td>reports</td>
      <td>Health Care</td>
      <td>Pharmaceuticals</td>
      <td>Florham Park, New Jersey</td>
      <td>2013-06-21</td>
      <td>1555280</td>
      <td>1952</td>
      <td>125.830002</td>
      <td>137.404999</td>
      <td>136.629997</td>
      <td>116.919998</td>
      <td>121.144997</td>
      <td>127.805004</td>
      <td>12509800.0</td>
    </tr>
  </tbody>
</table>
<p>499 rows × 17 columns</p>
</div>




```python
final_df["pct_change_dec19_may20"] =  ((final_df["2019-12-01"] - final_df["2020-05-01"]) / final_df["2019-12-01"]) *100
```


```python
plt.figure(figsize=(18, 6))
plt.tick_params('both', labelsize='12',color = 'white')
plt.xticks(rotation=30)
sns.boxplot(x="GICS Sector", y="pct_change_dec19_may20", data=final_df,showfliers=False)
plt.ylabel("% change in price",fontsize=18,color = 'white')
plt.xlabel("GICS Sectors",fontsize=18, color = 'white')
plt.title("% change in S&P500 Stocks from Dec 19 to May 20",color = 'white')
plt.tick_params('both', labelsize='12', colors="white")
plt.tight_layout()
plt.savefig('C:/Users/shrey/OneDrive/desktop/temp.png', transparent=True)
#plt.savefig(r'C:\Users\shrey\OneDrive\Desktop\Data Engineering\Graph for Project\% change in Stocks from Dec 19 to May 20.png')
```


![png](output_24_0.png)



```python
final_df.groupby("GICS Sub Industry").mean()['pct_change_dec19_may20'].sort_values().head(10)
```




    GICS Sub Industry
    Gold                                  -50.103242
    Systems Software                      -20.796089
    Wireless Telecommunication Services   -18.321911
    Food Retail                           -16.318066
    Biotechnology                         -12.379637
    Interactive Home Entertainment        -11.822640
    Household Products                     -9.253875
    Application Software                   -6.286561
    Internet Services & Infrastructure     -4.244803
    Financial Exchanges & Data             -3.837230
    Name: pct_change_dec19_may20, dtype: float64



### Above are Top 10 sectors that got affected the most

# Sorting the data by percentage change to see the impact on sectors:


```python
final_df.sort_values(by=['pct_change_dec19_may20'],inplace=True)
```


```python
final_df[:10]
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
      <th>Unnamed: 0</th>
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
      <th>pct_change_dec19_may20</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>334</th>
      <td>338</td>
      <td>NEM</td>
      <td>Newmont Corporation</td>
      <td>reports</td>
      <td>Materials</td>
      <td>Gold</td>
      <td>Denver, Colorado</td>
      <td>1969-06-30</td>
      <td>1164727</td>
      <td>1921</td>
      <td>41.165001</td>
      <td>43.480000</td>
      <td>46.855000</td>
      <td>42.750000</td>
      <td>54.715000</td>
      <td>61.790001</td>
      <td>36138500.0</td>
      <td>-50.103242</td>
    </tr>
    <tr>
      <th>395</th>
      <td>400</td>
      <td>REGN</td>
      <td>Regeneron Pharmaceuticals</td>
      <td>reports</td>
      <td>Health Care</td>
      <td>Biotechnology</td>
      <td>Tarrytown, New York</td>
      <td>2013-05-01</td>
      <td>872589</td>
      <td>NaN</td>
      <td>369.625000</td>
      <td>362.300003</td>
      <td>404.695007</td>
      <td>468.005005</td>
      <td>525.385010</td>
      <td>547.774994</td>
      <td>5956800.0</td>
      <td>-48.197496</td>
    </tr>
    <tr>
      <th>332</th>
      <td>336</td>
      <td>NFLX</td>
      <td>Netflix Inc.</td>
      <td>reports</td>
      <td>Communication Services</td>
      <td>Movies &amp; Entertainment</td>
      <td>Los Gatos, California</td>
      <td>2010-12-20</td>
      <td>1065280</td>
      <td>1997</td>
      <td>315.009995</td>
      <td>340.525009</td>
      <td>369.615005</td>
      <td>341.884995</td>
      <td>403.514999</td>
      <td>425.750000</td>
      <td>34687900.0</td>
      <td>-35.154442</td>
    </tr>
    <tr>
      <th>350</th>
      <td>354</td>
      <td>NVDA</td>
      <td>Nvidia Corporation</td>
      <td>reports</td>
      <td>Information Technology</td>
      <td>Semiconductors</td>
      <td>Santa Clara, California</td>
      <td>2001-11-30</td>
      <td>1045810</td>
      <td>NaN</td>
      <td>221.089996</td>
      <td>245.385002</td>
      <td>275.885002</td>
      <td>232.785004</td>
      <td>271.295006</td>
      <td>294.125000</td>
      <td>43104300.0</td>
      <td>-33.034061</td>
    </tr>
    <tr>
      <th>110</th>
      <td>113</td>
      <td>CTXS</td>
      <td>Citrix Systems</td>
      <td>reports</td>
      <td>Information Technology</td>
      <td>Application Software</td>
      <td>Fort Lauderdale, Florida</td>
      <td>1999-12-01</td>
      <td>877890</td>
      <td>NaN</td>
      <td>110.799999</td>
      <td>120.455002</td>
      <td>112.399998</td>
      <td>125.094997</td>
      <td>144.400002</td>
      <td>146.440002</td>
      <td>7976500.0</td>
      <td>-32.166068</td>
    </tr>
    <tr>
      <th>111</th>
      <td>114</td>
      <td>CLX</td>
      <td>The Clorox Company</td>
      <td>reports</td>
      <td>Consumer Staples</td>
      <td>Household Products</td>
      <td>Oakland, California</td>
      <td>1969-03-31</td>
      <td>21076</td>
      <td>1913</td>
      <td>150.169998</td>
      <td>156.559998</td>
      <td>164.525002</td>
      <td>185.469994</td>
      <td>184.864998</td>
      <td>197.129997</td>
      <td>14451900.0</td>
      <td>-31.271226</td>
    </tr>
    <tr>
      <th>412</th>
      <td>417</td>
      <td>NOW</td>
      <td>ServiceNow</td>
      <td>reports</td>
      <td>Information Technology</td>
      <td>Systems Software</td>
      <td>Santa Clara, California</td>
      <td>2019-11-21</td>
      <td>1373715</td>
      <td>2003</td>
      <td>275.804993</td>
      <td>314.055008</td>
      <td>335.025009</td>
      <td>294.815002</td>
      <td>302.224998</td>
      <td>360.790009</td>
      <td>13110400.0</td>
      <td>-30.813444</td>
    </tr>
    <tr>
      <th>27</th>
      <td>27</td>
      <td>AMZN</td>
      <td>Amazon.com Inc.</td>
      <td>reports</td>
      <td>Consumer Discretionary</td>
      <td>Internet &amp; Direct Marketing Retail</td>
      <td>Seattle, Washington</td>
      <td>2005-11-18</td>
      <td>1018724</td>
      <td>1994</td>
      <td>1818.200012</td>
      <td>1935.529968</td>
      <td>1998.539978</td>
      <td>1811.179993</td>
      <td>2182.075012</td>
      <td>2316.189941</td>
      <td>24383800.0</td>
      <td>-27.389172</td>
    </tr>
    <tr>
      <th>327</th>
      <td>331</td>
      <td>MSCI</td>
      <td>MSCI Inc</td>
      <td>reports</td>
      <td>Financials</td>
      <td>Financial Exchanges &amp; Data</td>
      <td>New York, New York</td>
      <td>2018-04-04</td>
      <td>1408198</td>
      <td>NaN</td>
      <td>259.525002</td>
      <td>275.934998</td>
      <td>309.214996</td>
      <td>270.104996</td>
      <td>304.645004</td>
      <td>328.419998</td>
      <td>2119900.0</td>
      <td>-26.546574</td>
    </tr>
    <tr>
      <th>143</th>
      <td>146</td>
      <td>DLR</td>
      <td>Digital Realty Trust Inc</td>
      <td>reports</td>
      <td>Real Estate</td>
      <td>Specialized REITs</td>
      <td>San Francisco, California</td>
      <td>2016-05-18</td>
      <td>1297996</td>
      <td>NaN</td>
      <td>116.654999</td>
      <td>123.600002</td>
      <td>126.930004</td>
      <td>124.305000</td>
      <td>142.740002</td>
      <td>147.455002</td>
      <td>6468500.0</td>
      <td>-26.402643</td>
    </tr>
  </tbody>
</table>
</div>
