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

    MMM
    [*********************100%***********************]  1 of 1 completed
    ABT
    [*********************100%***********************]  1 of 1 completed
    ABBV
    [*********************100%***********************]  1 of 1 completed
    ABMD
    [*********************100%***********************]  1 of 1 completed
    ACN
    [*********************100%***********************]  1 of 1 completed
    ATVI
    [*********************100%***********************]  1 of 1 completed
    ADBE
    [*********************100%***********************]  1 of 1 completed
    AMD
    [*********************100%***********************]  1 of 1 completed
    AAP
    [*********************100%***********************]  1 of 1 completed
    AES
    [*********************100%***********************]  1 of 1 completed
    AFL
    [*********************100%***********************]  1 of 1 completed
    A
    [*********************100%***********************]  1 of 1 completed
    APD
    [*********************100%***********************]  1 of 1 completed
    AKAM
    [*********************100%***********************]  1 of 1 completed
    ALK
    [*********************100%***********************]  1 of 1 completed
    ALB
    [*********************100%***********************]  1 of 1 completed
    ARE
    [*********************100%***********************]  1 of 1 completed
    ALXN
    [*********************100%***********************]  1 of 1 completed
    ALGN
    [*********************100%***********************]  1 of 1 completed
    ALLE
    [*********************100%***********************]  1 of 1 completed
    AGN
    [*********************100%***********************]  1 of 1 completed
    ADS
    [*********************100%***********************]  1 of 1 completed
    LNT
    [*********************100%***********************]  1 of 1 completed
    ALL
    [*********************100%***********************]  1 of 1 completed
    GOOGL
    [*********************100%***********************]  1 of 1 completed
    GOOG
    [*********************100%***********************]  1 of 1 completed
    MO
    [*********************100%***********************]  1 of 1 completed
    AMZN
    [*********************100%***********************]  1 of 1 completed
    AMCR
    [*********************100%***********************]  1 of 1 completed
    AEE
    [*********************100%***********************]  1 of 1 completed
    AAL
    [*********************100%***********************]  1 of 1 completed
    AEP
    [*********************100%***********************]  1 of 1 completed
    AXP
    [*********************100%***********************]  1 of 1 completed
    AIG
    [*********************100%***********************]  1 of 1 completed
    AMT
    [*********************100%***********************]  1 of 1 completed
    AWK
    [*********************100%***********************]  1 of 1 completed
    AMP
    [*********************100%***********************]  1 of 1 completed
    ABC
    [*********************100%***********************]  1 of 1 completed
    AME
    [*********************100%***********************]  1 of 1 completed
    AMGN
    [*********************100%***********************]  1 of 1 completed
    APH
    [*********************100%***********************]  1 of 1 completed
    ADI
    [*********************100%***********************]  1 of 1 completed
    ANSS
    [*********************100%***********************]  1 of 1 completed
    ANTM
    [*********************100%***********************]  1 of 1 completed
    AON
    [*********************100%***********************]  1 of 1 completed
    AOS
    [*********************100%***********************]  1 of 1 completed
    APA
    [*********************100%***********************]  1 of 1 completed
    AIV
    [*********************100%***********************]  1 of 1 completed
    AAPL
    [*********************100%***********************]  1 of 1 completed
    AMAT
    [*********************100%***********************]  1 of 1 completed
    APTV
    [*********************100%***********************]  1 of 1 completed
    ADM
    [*********************100%***********************]  1 of 1 completed
    ANET
    [*********************100%***********************]  1 of 1 completed
    AJG
    [*********************100%***********************]  1 of 1 completed
    AIZ
    [*********************100%***********************]  1 of 1 completed
    T
    [*********************100%***********************]  1 of 1 completed
    ATO
    [*********************100%***********************]  1 of 1 completed
    ADSK
    [*********************100%***********************]  1 of 1 completed
    ADP
    [*********************100%***********************]  1 of 1 completed
    AZO
    [*********************100%***********************]  1 of 1 completed
    AVB
    [*********************100%***********************]  1 of 1 completed
    AVY
    [*********************100%***********************]  1 of 1 completed
    BKR
    [*********************100%***********************]  1 of 1 completed
    BLL
    [*********************100%***********************]  1 of 1 completed
    BAC
    [*********************100%***********************]  1 of 1 completed
    BK
    [*********************100%***********************]  1 of 1 completed
    BAX
    [*********************100%***********************]  1 of 1 completed
    BDX
    [*********************100%***********************]  1 of 1 completed
    BBY
    [*********************100%***********************]  1 of 1 completed
    BIIB
    [*********************100%***********************]  1 of 1 completed
    BLK
    [*********************100%***********************]  1 of 1 completed
    BA
    [*********************100%***********************]  1 of 1 completed
    BKNG
    [*********************100%***********************]  1 of 1 completed
    BWA
    [*********************100%***********************]  1 of 1 completed
    BXP
    [*********************100%***********************]  1 of 1 completed
    BSX
    [*********************100%***********************]  1 of 1 completed
    BMY
    [*********************100%***********************]  1 of 1 completed
    AVGO
    [*********************100%***********************]  1 of 1 completed
    BR
    [*********************100%***********************]  1 of 1 completed
    CHRW
    [*********************100%***********************]  1 of 1 completed
    COG
    [*********************100%***********************]  1 of 1 completed
    CDNS
    [*********************100%***********************]  1 of 1 completed
    CPB
    [*********************100%***********************]  1 of 1 completed
    COF
    [*********************100%***********************]  1 of 1 completed
    CPRI
    [*********************100%***********************]  1 of 1 completed
    CAH
    [*********************100%***********************]  1 of 1 completed
    KMX
    [*********************100%***********************]  1 of 1 completed
    CCL
    [*********************100%***********************]  1 of 1 completed
    CAT
    [*********************100%***********************]  1 of 1 completed
    CBOE
    [*********************100%***********************]  1 of 1 completed
    CBRE
    [*********************100%***********************]  1 of 1 completed
    CDW
    [*********************100%***********************]  1 of 1 completed
    CE
    [*********************100%***********************]  1 of 1 completed
    CNC
    [*********************100%***********************]  1 of 1 completed
    CNP
    [*********************100%***********************]  1 of 1 completed
    CTL
    [*********************100%***********************]  1 of 1 completed
    CERN
    [*********************100%***********************]  1 of 1 completed
    CF
    [*********************100%***********************]  1 of 1 completed
    SCHW
    [*********************100%***********************]  1 of 1 completed
    CHTR
    [*********************100%***********************]  1 of 1 completed
    CVX
    [*********************100%***********************]  1 of 1 completed
    CMG
    [*********************100%***********************]  1 of 1 completed
    CB
    [*********************100%***********************]  1 of 1 completed
    CHD
    [*********************100%***********************]  1 of 1 completed
    CI
    [*********************100%***********************]  1 of 1 completed
    CINF
    [*********************100%***********************]  1 of 1 completed
    CTAS
    [*********************100%***********************]  1 of 1 completed
    CSCO
    [*********************100%***********************]  1 of 1 completed
    C
    [*********************100%***********************]  1 of 1 completed
    CFG
    [*********************100%***********************]  1 of 1 completed
    CTXS
    [*********************100%***********************]  1 of 1 completed
    CLX
    [*********************100%***********************]  1 of 1 completed
    CME
    [*********************100%***********************]  1 of 1 completed
    CMS
    [*********************100%***********************]  1 of 1 completed
    KO
    [*********************100%***********************]  1 of 1 completed
    CTSH
    [*********************100%***********************]  1 of 1 completed
    CL
    [*********************100%***********************]  1 of 1 completed
    CMCSA
    [*********************100%***********************]  1 of 1 completed
    CMA
    [*********************100%***********************]  1 of 1 completed
    CAG
    [*********************100%***********************]  1 of 1 completed
    CXO
    [*********************100%***********************]  1 of 1 completed
    COP
    [*********************100%***********************]  1 of 1 completed
    ED
    [*********************100%***********************]  1 of 1 completed
    STZ
    [*********************100%***********************]  1 of 1 completed
    COO
    [*********************100%***********************]  1 of 1 completed
    CPRT
    [*********************100%***********************]  1 of 1 completed
    GLW
    [*********************100%***********************]  1 of 1 completed
    CTVA
    [*********************100%***********************]  1 of 1 completed
    COST
    [*********************100%***********************]  1 of 1 completed
    COTY
    [*********************100%***********************]  1 of 1 completed
    CCI
    [*********************100%***********************]  1 of 1 completed
    CSX
    [*********************100%***********************]  1 of 1 completed
    CMI
    [*********************100%***********************]  1 of 1 completed
    CVS
    [*********************100%***********************]  1 of 1 completed
    DHI
    [*********************100%***********************]  1 of 1 completed
    DHR
    [*********************100%***********************]  1 of 1 completed
    DRI
    [*********************100%***********************]  1 of 1 completed
    DVA
    [*********************100%***********************]  1 of 1 completed
    DE
    [*********************100%***********************]  1 of 1 completed
    DAL
    [*********************100%***********************]  1 of 1 completed
    XRAY
    [*********************100%***********************]  1 of 1 completed
    DVN
    [*********************100%***********************]  1 of 1 completed
    FANG
    [*********************100%***********************]  1 of 1 completed
    DLR
    [*********************100%***********************]  1 of 1 completed
    DFS
    [*********************100%***********************]  1 of 1 completed
    DISCA
    [*********************100%***********************]  1 of 1 completed
    DISCK
    [*********************100%***********************]  1 of 1 completed
    DISH
    [*********************100%***********************]  1 of 1 completed
    DG
    [*********************100%***********************]  1 of 1 completed
    DLTR
    [*********************100%***********************]  1 of 1 completed
    D
    [*********************100%***********************]  1 of 1 completed
    DOV
    [*********************100%***********************]  1 of 1 completed
    DOW
    [*********************100%***********************]  1 of 1 completed
    DTE
    [*********************100%***********************]  1 of 1 completed
    DUK
    [*********************100%***********************]  1 of 1 completed
    DRE
    [*********************100%***********************]  1 of 1 completed
    DD
    [*********************100%***********************]  1 of 1 completed
    DXC
    [*********************100%***********************]  1 of 1 completed
    ETFC
    [*********************100%***********************]  1 of 1 completed
    EMN
    [*********************100%***********************]  1 of 1 completed
    ETN
    [*********************100%***********************]  1 of 1 completed
    EBAY
    [*********************100%***********************]  1 of 1 completed
    ECL
    [*********************100%***********************]  1 of 1 completed
    EIX
    [*********************100%***********************]  1 of 1 completed
    EW
    [*********************100%***********************]  1 of 1 completed
    EA
    [*********************100%***********************]  1 of 1 completed
    EMR
    [*********************100%***********************]  1 of 1 completed
    ETR
    [*********************100%***********************]  1 of 1 completed
    EOG
    [*********************100%***********************]  1 of 1 completed
    EFX
    [*********************100%***********************]  1 of 1 completed
    EQIX
    [*********************100%***********************]  1 of 1 completed
    EQR
    [*********************100%***********************]  1 of 1 completed
    ESS
    [*********************100%***********************]  1 of 1 completed
    EL
    [*********************100%***********************]  1 of 1 completed
    EVRG
    [*********************100%***********************]  1 of 1 completed
    ES
    [*********************100%***********************]  1 of 1 completed
    RE
    [*********************100%***********************]  1 of 1 completed
    EXC
    [*********************100%***********************]  1 of 1 completed
    EXPE
    [*********************100%***********************]  1 of 1 completed
    EXPD
    [*********************100%***********************]  1 of 1 completed
    EXR
    [*********************100%***********************]  1 of 1 completed
    XOM
    [*********************100%***********************]  1 of 1 completed
    FFIV
    [*********************100%***********************]  1 of 1 completed
    FB
    [*********************100%***********************]  1 of 1 completed
    FAST
    [*********************100%***********************]  1 of 1 completed
    FRT
    [*********************100%***********************]  1 of 1 completed
    FDX
    [*********************100%***********************]  1 of 1 completed
    FIS
    [*********************100%***********************]  1 of 1 completed
    FITB
    [*********************100%***********************]  1 of 1 completed
    FE
    [*********************100%***********************]  1 of 1 completed
    FRC
    [*********************100%***********************]  1 of 1 completed
    FISV
    [*********************100%***********************]  1 of 1 completed
    FLT
    [*********************100%***********************]  1 of 1 completed
    FLIR
    [*********************100%***********************]  1 of 1 completed
    FLS
    [*********************100%***********************]  1 of 1 completed
    FMC
    [*********************100%***********************]  1 of 1 completed
    F
    [*********************100%***********************]  1 of 1 completed
    FTNT
    [*********************100%***********************]  1 of 1 completed
    FTV
    [*********************100%***********************]  1 of 1 completed
    FBHS
    [*********************100%***********************]  1 of 1 completed
    FOXA
    [*********************100%***********************]  1 of 1 completed
    FOX
    [*********************100%***********************]  1 of 1 completed
    BEN
    [*********************100%***********************]  1 of 1 completed
    FCX
    [*********************100%***********************]  1 of 1 completed
    GPS
    [*********************100%***********************]  1 of 1 completed
    GRMN
    [*********************100%***********************]  1 of 1 completed
    IT
    [*********************100%***********************]  1 of 1 completed
    GD
    [*********************100%***********************]  1 of 1 completed
    GE
    [*********************100%***********************]  1 of 1 completed
    GIS
    [*********************100%***********************]  1 of 1 completed
    GM
    [*********************100%***********************]  1 of 1 completed
    GPC
    [*********************100%***********************]  1 of 1 completed
    GILD
    [*********************100%***********************]  1 of 1 completed
    GL
    [*********************100%***********************]  1 of 1 completed
    GPN
    [*********************100%***********************]  1 of 1 completed
    GS
    [*********************100%***********************]  1 of 1 completed
    GWW
    [*********************100%***********************]  1 of 1 completed
    HRB
    [*********************100%***********************]  1 of 1 completed
    HAL
    [*********************100%***********************]  1 of 1 completed
    HBI
    [*********************100%***********************]  1 of 1 completed
    HOG
    [*********************100%***********************]  1 of 1 completed
    HIG
    [*********************100%***********************]  1 of 1 completed
    HAS
    [*********************100%***********************]  1 of 1 completed
    HCA
    [*********************100%***********************]  1 of 1 completed
    PEAK
    [*********************100%***********************]  1 of 1 completed
    HP
    [*********************100%***********************]  1 of 1 completed
    HSIC
    [*********************100%***********************]  1 of 1 completed
    HSY
    [*********************100%***********************]  1 of 1 completed
    HES
    [*********************100%***********************]  1 of 1 completed
    HPE
    [*********************100%***********************]  1 of 1 completed
    HLT
    [*********************100%***********************]  1 of 1 completed
    HFC
    [*********************100%***********************]  1 of 1 completed
    HOLX
    [*********************100%***********************]  1 of 1 completed
    HD
    [*********************100%***********************]  1 of 1 completed
    HON
    [*********************100%***********************]  1 of 1 completed
    HRL
    [*********************100%***********************]  1 of 1 completed
    HST
    [*********************100%***********************]  1 of 1 completed
    HPQ
    [*********************100%***********************]  1 of 1 completed
    HUM
    [*********************100%***********************]  1 of 1 completed
    HBAN
    [*********************100%***********************]  1 of 1 completed
    HII
    [*********************100%***********************]  1 of 1 completed
    IEX
    [*********************100%***********************]  1 of 1 completed
    IDXX
    [*********************100%***********************]  1 of 1 completed
    INFO
    [*********************100%***********************]  1 of 1 completed
    ITW
    [*********************100%***********************]  1 of 1 completed
    ILMN
    [*********************100%***********************]  1 of 1 completed
    INCY
    [*********************100%***********************]  1 of 1 completed
    IR
    [*********************100%***********************]  1 of 1 completed
    INTC
    [*********************100%***********************]  1 of 1 completed
    ICE
    [*********************100%***********************]  1 of 1 completed
    IBM
    [*********************100%***********************]  1 of 1 completed
    IP
    [*********************100%***********************]  1 of 1 completed
    IPG
    [*********************100%***********************]  1 of 1 completed
    IFF
    [*********************100%***********************]  1 of 1 completed
    INTU
    [*********************100%***********************]  1 of 1 completed
    ISRG
    [*********************100%***********************]  1 of 1 completed
    IVZ
    [*********************100%***********************]  1 of 1 completed
    IPGP
    [*********************100%***********************]  1 of 1 completed
    IQV
    [*********************100%***********************]  1 of 1 completed
    IRM
    [*********************100%***********************]  1 of 1 completed
    JKHY
    [*********************100%***********************]  1 of 1 completed
    J
    [*********************100%***********************]  1 of 1 completed
    JBHT
    [*********************100%***********************]  1 of 1 completed
    SJM
    [*********************100%***********************]  1 of 1 completed
    JNJ
    [*********************100%***********************]  1 of 1 completed
    JCI
    [*********************100%***********************]  1 of 1 completed
    JPM
    [*********************100%***********************]  1 of 1 completed
    JNPR
    [*********************100%***********************]  1 of 1 completed
    KSU
    [*********************100%***********************]  1 of 1 completed
    K
    [*********************100%***********************]  1 of 1 completed
    KEY
    [*********************100%***********************]  1 of 1 completed
    KEYS
    [*********************100%***********************]  1 of 1 completed
    KMB
    [*********************100%***********************]  1 of 1 completed
    KIM
    [*********************100%***********************]  1 of 1 completed
    KMI
    [*********************100%***********************]  1 of 1 completed
    KLAC
    [*********************100%***********************]  1 of 1 completed
    KSS
    [*********************100%***********************]  1 of 1 completed
    KHC
    [*********************100%***********************]  1 of 1 completed
    KR
    [*********************100%***********************]  1 of 1 completed
    LB
    [*********************100%***********************]  1 of 1 completed
    LHX
    [*********************100%***********************]  1 of 1 completed
    LH
    [*********************100%***********************]  1 of 1 completed
    LRCX
    [*********************100%***********************]  1 of 1 completed
    LW
    [*********************100%***********************]  1 of 1 completed
    LVS
    [*********************100%***********************]  1 of 1 completed
    LEG
    [*********************100%***********************]  1 of 1 completed
    LDOS
    [*********************100%***********************]  1 of 1 completed
    LEN
    [*********************100%***********************]  1 of 1 completed
    LLY
    [*********************100%***********************]  1 of 1 completed
    LNC
    [*********************100%***********************]  1 of 1 completed
    LIN
    [*********************100%***********************]  1 of 1 completed
    LYV
    [*********************100%***********************]  1 of 1 completed
    LKQ
    [*********************100%***********************]  1 of 1 completed
    LMT
    [*********************100%***********************]  1 of 1 completed
    L
    [*********************100%***********************]  1 of 1 completed
    LOW
    [*********************100%***********************]  1 of 1 completed
    LYB
    [*********************100%***********************]  1 of 1 completed
    MTB
    [*********************100%***********************]  1 of 1 completed
    MRO
    [*********************100%***********************]  1 of 1 completed
    MPC
    [*********************100%***********************]  1 of 1 completed
    MKTX
    [*********************100%***********************]  1 of 1 completed
    MAR
    [*********************100%***********************]  1 of 1 completed
    MMC
    [*********************100%***********************]  1 of 1 completed
    MLM
    [*********************100%***********************]  1 of 1 completed
    MAS
    [*********************100%***********************]  1 of 1 completed
    MA
    [*********************100%***********************]  1 of 1 completed
    MKC
    [*********************100%***********************]  1 of 1 completed
    MXIM
    [*********************100%***********************]  1 of 1 completed
    MCD
    [*********************100%***********************]  1 of 1 completed
    MCK
    [*********************100%***********************]  1 of 1 completed
    MDT
    [*********************100%***********************]  1 of 1 completed
    MRK
    [*********************100%***********************]  1 of 1 completed
    MET
    [*********************100%***********************]  1 of 1 completed
    MTD
    [*********************100%***********************]  1 of 1 completed
    MGM
    [*********************100%***********************]  1 of 1 completed
    MCHP
    [*********************100%***********************]  1 of 1 completed
    MU
    [*********************100%***********************]  1 of 1 completed
    MSFT
    [*********************100%***********************]  1 of 1 completed
    MAA
    [*********************100%***********************]  1 of 1 completed
    MHK
    [*********************100%***********************]  1 of 1 completed
    TAP
    [*********************100%***********************]  1 of 1 completed
    MDLZ
    [*********************100%***********************]  1 of 1 completed
    MNST
    [*********************100%***********************]  1 of 1 completed
    MCO
    [*********************100%***********************]  1 of 1 completed
    MS
    [*********************100%***********************]  1 of 1 completed
    MOS
    [*********************100%***********************]  1 of 1 completed
    MSI
    [*********************100%***********************]  1 of 1 completed
    MSCI
    [*********************100%***********************]  1 of 1 completed
    MYL
    [*********************100%***********************]  1 of 1 completed
    NDAQ
    [*********************100%***********************]  1 of 1 completed
    NOV
    [*********************100%***********************]  1 of 1 completed
    NTAP
    [*********************100%***********************]  1 of 1 completed
    NFLX
    [*********************100%***********************]  1 of 1 completed
    NWL
    [*********************100%***********************]  1 of 1 completed
    NEM
    [*********************100%***********************]  1 of 1 completed
    NWSA
    [*********************100%***********************]  1 of 1 completed
    NWS
    [*********************100%***********************]  1 of 1 completed
    NEE
    [*********************100%***********************]  1 of 1 completed
    NLSN
    [*********************100%***********************]  1 of 1 completed
    NKE
    [*********************100%***********************]  1 of 1 completed
    NI
    [*********************100%***********************]  1 of 1 completed
    NBL
    [*********************100%***********************]  1 of 1 completed
    JWN
    [*********************100%***********************]  1 of 1 completed
    NSC
    [*********************100%***********************]  1 of 1 completed
    NTRS
    [*********************100%***********************]  1 of 1 completed
    NOC
    [*********************100%***********************]  1 of 1 completed
    NLOK
    [*********************100%***********************]  1 of 1 completed
    NCLH
    [*********************100%***********************]  1 of 1 completed
    NRG
    [*********************100%***********************]  1 of 1 completed
    NUE
    [*********************100%***********************]  1 of 1 completed
    NVDA
    [*********************100%***********************]  1 of 1 completed
    NVR
    [*********************100%***********************]  1 of 1 completed
    ORLY
    [*********************100%***********************]  1 of 1 completed
    OXY
    [*********************100%***********************]  1 of 1 completed
    ODFL
    [*********************100%***********************]  1 of 1 completed
    OMC
    [*********************100%***********************]  1 of 1 completed
    OKE
    [*********************100%***********************]  1 of 1 completed
    ORCL
    [*********************100%***********************]  1 of 1 completed
    PCAR
    [*********************100%***********************]  1 of 1 completed
    PKG
    [*********************100%***********************]  1 of 1 completed
    PH
    [*********************100%***********************]  1 of 1 completed
    PAYX
    [*********************100%***********************]  1 of 1 completed
    PAYC
    [*********************100%***********************]  1 of 1 completed

    1 Failed download:
    - PAYC: Request Failed
    PYPL
    [*********************100%***********************]  1 of 1 completed
    PNR
    [*********************100%***********************]  1 of 1 completed
    PBCT
    [*********************100%***********************]  1 of 1 completed
    PEP
    [*********************100%***********************]  1 of 1 completed
    PKI
    [*********************100%***********************]  1 of 1 completed
    PRGO
    [*********************100%***********************]  1 of 1 completed
    PFE
    [*********************100%***********************]  1 of 1 completed
    PM
    [*********************100%***********************]  1 of 1 completed
    PSX
    [*********************100%***********************]  1 of 1 completed
    PNW
    [*********************100%***********************]  1 of 1 completed
    PXD
    [*********************100%***********************]  1 of 1 completed
    PNC
    [*********************100%***********************]  1 of 1 completed
    PPG
    [*********************100%***********************]  1 of 1 completed

    1 Failed download:
    - PPG: Request Failed
    PPL
    [*********************100%***********************]  1 of 1 completed
    PFG
    [*********************100%***********************]  1 of 1 completed
    PG
    [*********************100%***********************]  1 of 1 completed
    PGR
    [*********************100%***********************]  1 of 1 completed
    PLD
    [*********************100%***********************]  1 of 1 completed
    PRU
    [*********************100%***********************]  1 of 1 completed
    PEG
    [*********************100%***********************]  1 of 1 completed
    PSA
    [*********************100%***********************]  1 of 1 completed
    PHM
    [*********************100%***********************]  1 of 1 completed
    PVH
    [*********************100%***********************]  1 of 1 completed
    QRVO
    [*********************100%***********************]  1 of 1 completed
    PWR
    [*********************100%***********************]  1 of 1 completed
    QCOM
    [*********************100%***********************]  1 of 1 completed
    DGX
    [*********************100%***********************]  1 of 1 completed
    RL
    [*********************100%***********************]  1 of 1 completed
    RJF
    [*********************100%***********************]  1 of 1 completed
    RTX
    [*********************100%***********************]  1 of 1 completed
    O
    [*********************100%***********************]  1 of 1 completed
    REG
    [*********************100%***********************]  1 of 1 completed
    REGN
    [*********************100%***********************]  1 of 1 completed
    RF
    [*********************100%***********************]  1 of 1 completed
    RSG
    [*********************100%***********************]  1 of 1 completed
    RMD
    [*********************100%***********************]  1 of 1 completed
    RHI
    [*********************100%***********************]  1 of 1 completed
    ROK
    [*********************100%***********************]  1 of 1 completed
    ROL
    [*********************100%***********************]  1 of 1 completed
    ROP
    [*********************100%***********************]  1 of 1 completed
    ROST
    [*********************100%***********************]  1 of 1 completed
    RCL
    [*********************100%***********************]  1 of 1 completed
    SPGI
    [*********************100%***********************]  1 of 1 completed
    CRM
    [*********************100%***********************]  1 of 1 completed
    SBAC
    [*********************100%***********************]  1 of 1 completed
    SLB
    [*********************100%***********************]  1 of 1 completed
    STX
    [*********************100%***********************]  1 of 1 completed
    SEE
    [*********************100%***********************]  1 of 1 completed
    SRE
    [*********************100%***********************]  1 of 1 completed
    NOW
    [*********************100%***********************]  1 of 1 completed
    SHW
    [*********************100%***********************]  1 of 1 completed
    SPG
    [*********************100%***********************]  1 of 1 completed
    SWKS
    [*********************100%***********************]  1 of 1 completed
    SLG
    [*********************100%***********************]  1 of 1 completed
    SNA
    [*********************100%***********************]  1 of 1 completed
    SO
    [*********************100%***********************]  1 of 1 completed
    LUV
    [*********************100%***********************]  1 of 1 completed
    SWK
    [*********************100%***********************]  1 of 1 completed
    SBUX
    [*********************100%***********************]  1 of 1 completed
    STT
    [*********************100%***********************]  1 of 1 completed
    STE
    [*********************100%***********************]  1 of 1 completed
    SYK
    [*********************100%***********************]  1 of 1 completed
    SIVB
    [*********************100%***********************]  1 of 1 completed
    SYF
    [*********************100%***********************]  1 of 1 completed
    SNPS
    [*********************100%***********************]  1 of 1 completed
    SYY
    [*********************100%***********************]  1 of 1 completed
    TMUS
    [*********************100%***********************]  1 of 1 completed
    TROW
    [*********************100%***********************]  1 of 1 completed
    TTWO
    [*********************100%***********************]  1 of 1 completed
    TPR
    [*********************100%***********************]  1 of 1 completed
    TGT
    [*********************100%***********************]  1 of 1 completed
    TEL
    [*********************100%***********************]  1 of 1 completed

    1 Failed download:
    - TEL: No data found for this date range, symbol may be delisted
    FTI
    [*********************100%***********************]  1 of 1 completed
    TFX
    [*********************100%***********************]  1 of 1 completed
    TXN
    [*********************100%***********************]  1 of 1 completed
    TXT
    [*********************100%***********************]  1 of 1 completed
    TMO
    [*********************100%***********************]  1 of 1 completed
    TIF
    [*********************100%***********************]  1 of 1 completed
    TJX
    [*********************100%***********************]  1 of 1 completed
    TSCO
    [*********************100%***********************]  1 of 1 completed
    TDG
    [*********************100%***********************]  1 of 1 completed
    TRV
    [*********************100%***********************]  1 of 1 completed
    TFC
    [*********************100%***********************]  1 of 1 completed
    TWTR
    [*********************100%***********************]  1 of 1 completed
    TSN
    [*********************100%***********************]  1 of 1 completed
    UDR
    [*********************100%***********************]  1 of 1 completed
    ULTA
    [*********************100%***********************]  1 of 1 completed
    USB
    [*********************100%***********************]  1 of 1 completed
    UAA
    [*********************100%***********************]  1 of 1 completed
    UA
    [*********************100%***********************]  1 of 1 completed
    UNP
    [*********************100%***********************]  1 of 1 completed
    UAL
    [*********************100%***********************]  1 of 1 completed
    UNH
    [*********************100%***********************]  1 of 1 completed
    UPS
    [*********************100%***********************]  1 of 1 completed
    URI
    [*********************100%***********************]  1 of 1 completed
    UHS
    [*********************100%***********************]  1 of 1 completed
    UNM
    [*********************100%***********************]  1 of 1 completed
    VFC
    [*********************100%***********************]  1 of 1 completed
    VLO
    [*********************100%***********************]  1 of 1 completed
    VAR
    [*********************100%***********************]  1 of 1 completed
    VTR
    [*********************100%***********************]  1 of 1 completed
    VRSN
    [*********************100%***********************]  1 of 1 completed
    VRSK
    [*********************100%***********************]  1 of 1 completed
    VZ
    [*********************100%***********************]  1 of 1 completed
    VRTX
    [*********************100%***********************]  1 of 1 completed
    VIAC
    [*********************100%***********************]  1 of 1 completed
    V
    [*********************100%***********************]  1 of 1 completed
    VNO
    [*********************100%***********************]  1 of 1 completed
    VMC
    [*********************100%***********************]  1 of 1 completed
    WRB
    [*********************100%***********************]  1 of 1 completed
    WAB
    [*********************100%***********************]  1 of 1 completed
    WMT
    [*********************100%***********************]  1 of 1 completed
    WBA
    [*********************100%***********************]  1 of 1 completed
    DIS
    [*********************100%***********************]  1 of 1 completed
    WM
    [*********************100%***********************]  1 of 1 completed
    WAT
    [*********************100%***********************]  1 of 1 completed
    WEC
    [*********************100%***********************]  1 of 1 completed
    WFC
    [*********************100%***********************]  1 of 1 completed
    WELL
    [*********************100%***********************]  1 of 1 completed
    WDC
    [*********************100%***********************]  1 of 1 completed
    WU
    [*********************100%***********************]  1 of 1 completed
    WRK
    [*********************100%***********************]  1 of 1 completed
    WY
    [*********************100%***********************]  1 of 1 completed
    WHR
    [*********************100%***********************]  1 of 1 completed
    WMB
    [*********************100%***********************]  1 of 1 completed
    WLTW
    [*********************100%***********************]  1 of 1 completed
    WYNN
    [*********************100%***********************]  1 of 1 completed
    XEL
    [*********************100%***********************]  1 of 1 completed
    XRX
    [*********************100%***********************]  1 of 1 completed
    XLNX
    [*********************100%***********************]  1 of 1 completed
    XYL
    [*********************100%***********************]  1 of 1 completed
    YUM
    [*********************100%***********************]  1 of 1 completed
    ZBRA
    [*********************100%***********************]  1 of 1 completed
    ZBH
    [*********************100%***********************]  1 of 1 completed
    ZION
    [*********************100%***********************]  1 of 1 completed
    ZTS
    [*********************100%***********************]  1 of 1 completed


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




```python
final_df.groupby("GICS Sub Industry").mean()['pct_change_dec19_may20'].sort_values()[0:10]
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




```python
plt.figure(figsize=(18, 6))
plt.tick_params('both', labelsize='15', color="white")

plt.title("Top 10 Sectors that got affected the Most",fontsize=18, color='white')
t = final_df.groupby("GICS Sub Industry").mean()['pct_change_dec19_may20'].sort_values()[0:10].plot.barh(color='midnightblue')
#plt.xticks(rotation=30)
plt.ylabel("Sub Industry",size= 20, color ="white")
plt.tick_params('both', labelsize='25', colors="white")
plt.tight_layout()
plt.savefig('C:/Users/shrey/OneDrive/desktop/temp.png', transparent=True)
```


![png](output_31_0.png)


# Time series analysis on Covid Cases:

## Data Extraction:


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

# Quality check:


```python
full_df.isin([" ","NA", "NULL"]).sum()
```




    date              0
    count             0
    country           0
    coordinates       0
    country_code    321
    province          0
    data_type         0
    dtype: int64




```python
#Preview od the dataframe
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




```python
# Aggregate of confirmed
full_agg_confirm = full_confirmed_df.groupby("country").agg(sum_confirmed=('count','sum'))
# Agg of deaths
full_agg_deaths = full_death_df.groupby("country").agg(sum_death=('count','sum'))
# Agg of recovered
full_agg_recovered = full_recovered_df.groupby("country").agg(sum_recovered=('count','sum'))
```


```python
# all the built dataframes has all the country
print(len(full_agg_confirm.index))
print(len(full_agg_deaths.index))
print(len(full_agg_recovered.index))
```

    187
    187
    187


## Merging data with total Confirm cases, Deaths and Recovered by country


```python
# Merge columns
merged_covid_Df = full_agg_confirm.merge(full_agg_deaths, left_index=True, right_index=True)
merged_covid_Df = merged_covid_Df.merge(full_agg_recovered,left_index=True, right_index=True)
#reset index
merged_covid_Df.reset_index(inplace=True)
```


```python
merged_covid_Df
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
      <td>49043</td>
      <td>1509</td>
      <td>5683</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Albania</td>
      <td>23527</td>
      <td>1036</td>
      <td>11994</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Algeria</td>
      <td>106913</td>
      <td>12790</td>
      <td>38880</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Andorra</td>
      <td>27137</td>
      <td>1272</td>
      <td>9166</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Angola</td>
      <td>892</td>
      <td>80</td>
      <td>207</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>182</th>
      <td>West Bank and Gaza</td>
      <td>12493</td>
      <td>71</td>
      <td>2723</td>
    </tr>
    <tr>
      <th>183</th>
      <td>Western Sahara</td>
      <td>184</td>
      <td>0</td>
      <td>75</td>
    </tr>
    <tr>
      <th>184</th>
      <td>Yemen</td>
      <td>142</td>
      <td>24</td>
      <td>14</td>
    </tr>
    <tr>
      <th>185</th>
      <td>Zambia</td>
      <td>2874</td>
      <td>85</td>
      <td>1401</td>
    </tr>
    <tr>
      <th>186</th>
      <td>Zimbabwe</td>
      <td>915</td>
      <td>123</td>
      <td>77</td>
    </tr>
  </tbody>
</table>
<p>187 rows × 4 columns</p>
</div>



## More demogrphics data like population by age group and GDP



```python
df = pd.read_excel(r"C:\Users\shrey\OneDrive\Desktop\BE_NEWDATA.xlsx", na_values=" ")
df = df.loc[:,["Country","Region Extended","GDP 2018 ($)","Statusof Schools","Population in age range 50-100"]]
```


```python
#merging using unique key we created
merged_covid_Df= pd.merge(left=df, right=merged_covid_Df, left_on='Country', right_on='country')
```


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
merged_covid_Df["Statusof Schools"]
```




    0      Closed
    1      Closed
    2      Closed
    3         NaN
    4      Closed
            ...  
    160    Closed
    161    Closed
    162    Closed
    163    Closed
    164    Closed
    Name: Statusof Schools, Length: 165, dtype: object




```python
# make copy of merged covid data
cluster_df = merged_covid_Df.copy()
# Dropping repeatinf columns
cluster_df.drop("country",axis=1, inplace= True)
```


```python
cluster_df.loc[cluster_df["Region Extended"] == "North America",'sum_recovered'].sum()
```




    681555




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
cluster_df
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
      <td>49043</td>
      <td>1509</td>
      <td>5683</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Albania</td>
      <td>1</td>
      <td>1.936297e+10</td>
      <td>0</td>
      <td>995.719</td>
      <td>23527</td>
      <td>1036</td>
      <td>11994</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Algeria</td>
      <td>3</td>
      <td>1.057510e+11</td>
      <td>0</td>
      <td>8144.237</td>
      <td>106913</td>
      <td>12790</td>
      <td>38880</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Andorra</td>
      <td>1</td>
      <td>3.236544e+09</td>
      <td>-1</td>
      <td>NaN</td>
      <td>27137</td>
      <td>1272</td>
      <td>9166</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Angola</td>
      <td>6</td>
      <td>2.774315e+12</td>
      <td>0</td>
      <td>2666.820</td>
      <td>892</td>
      <td>80</td>
      <td>207</td>
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
    </tr>
    <tr>
      <th>160</th>
      <td>Uruguay</td>
      <td>2</td>
      <td>NaN</td>
      <td>0</td>
      <td>1094.002</td>
      <td>22320</td>
      <td>399</td>
      <td>10785</td>
    </tr>
    <tr>
      <th>161</th>
      <td>Uzbekistan</td>
      <td>1</td>
      <td>3.855000e+09</td>
      <td>0</td>
      <td>5839.939</td>
      <td>51395</td>
      <td>221</td>
      <td>19221</td>
    </tr>
    <tr>
      <th>162</th>
      <td>Yemen</td>
      <td>3</td>
      <td>3.682889e+11</td>
      <td>0</td>
      <td>2806.298</td>
      <td>142</td>
      <td>24</td>
      <td>14</td>
    </tr>
    <tr>
      <th>163</th>
      <td>Zambia</td>
      <td>6</td>
      <td>2.672007e+10</td>
      <td>0</td>
      <td>1390.767</td>
      <td>2874</td>
      <td>85</td>
      <td>1401</td>
    </tr>
    <tr>
      <th>164</th>
      <td>Zimbabwe</td>
      <td>6</td>
      <td>3.100052e+10</td>
      <td>0</td>
      <td>1386.523</td>
      <td>915</td>
      <td>123</td>
      <td>77</td>
    </tr>
  </tbody>
</table>
<p>165 rows × 8 columns</p>
</div>




```python
# Making country as index
cluster_df.set_index(["Country"], inplace=True)
```


```python
cluster_df.columns
```




    Index(['Region Extended', 'GDP 2018 ($)', 'Statusof Schools',
           'Population in age range 50-100', 'sum_confirmed', 'sum_death',
           'sum_recovered'],
          dtype='object')




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




```python
cluster_df.isin([" "]).sum()
```




    Region Extended                   0
    GDP 2018 ($)                      0
    Statusof Schools                  0
    Population in age range 50-100    0
    sum_confirmed                     0
    sum_death                         0
    sum_recovered                     0
    dtype: int64




```python
cluster_df['Population in age range 50-100'].replace(' ', np.nan, inplace=True)
```


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




```python
cluster_df.index
```




    Index(['Afghanistan', 'Albania', 'Algeria', 'Angola', 'Antigua and Barbuda',
           'Argentina', 'Armenia', 'Australia', 'Austria', 'Azerbaijan',
           ...
           'Tunisia', 'Turkey', 'Uganda', 'Ukraine', 'United Arab Emirates',
           'United Kingdom', 'Uzbekistan', 'Yemen', 'Zambia', 'Zimbabwe'],
          dtype='object', name='Country', length=155)




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
      6.43019279e-03 1.56443416e-03 1.07828423e-03]
     [1.66666667e-01 3.56427133e-04 2.50000000e-01 2.05962014e-03
      3.08265644e-03 1.07405818e-03 2.27572428e-03]
     [5.00000000e-01 1.95013444e-03 2.50000000e-01 1.72067596e-02
      1.40223675e-02 1.32598495e-02 7.37703518e-03]
     [1.00000000e+00 5.11804559e-02 2.50000000e-01 5.60054987e-03
      1.13088899e-04 8.29388554e-05 3.92758818e-05]
     [3.33333333e-01 7.64008885e-03 2.50000000e-01 6.19784171e-06
      1.07972348e-04 8.60490625e-05 4.42090843e-05]]



```python

#Replacing scalled in the data frame
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
      <td>0.006430</td>
      <td>0.001564</td>
      <td>0.001078</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.166667</td>
      <td>0.000356</td>
      <td>0.25</td>
      <td>0.002060</td>
      <td>0.003083</td>
      <td>0.001074</td>
      <td>0.002276</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.500000</td>
      <td>0.001950</td>
      <td>0.25</td>
      <td>0.017207</td>
      <td>0.014022</td>
      <td>0.013260</td>
      <td>0.007377</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.000000</td>
      <td>0.051180</td>
      <td>0.25</td>
      <td>0.005601</td>
      <td>0.000113</td>
      <td>0.000083</td>
      <td>0.000039</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.333333</td>
      <td>0.007640</td>
      <td>0.25</td>
      <td>0.000006</td>
      <td>0.000108</td>
      <td>0.000086</td>
      <td>0.000044</td>
    </tr>
  </tbody>
</table>
</div>




```python

# making clusters
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

    [1, 6, 0, 1, 0]



```python
df
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
      <th>K-means Cluster Labels</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.833333</td>
      <td>0.000049</td>
      <td>0.25</td>
      <td>0.007332</td>
      <td>0.006430</td>
      <td>0.001564</td>
      <td>0.001078</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.166667</td>
      <td>0.000356</td>
      <td>0.25</td>
      <td>0.002060</td>
      <td>0.003083</td>
      <td>0.001074</td>
      <td>0.002276</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.500000</td>
      <td>0.001950</td>
      <td>0.25</td>
      <td>0.017207</td>
      <td>0.014022</td>
      <td>0.013260</td>
      <td>0.007377</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.000000</td>
      <td>0.051180</td>
      <td>0.25</td>
      <td>0.005601</td>
      <td>0.000113</td>
      <td>0.000083</td>
      <td>0.000039</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.333333</td>
      <td>0.007640</td>
      <td>0.25</td>
      <td>0.000006</td>
      <td>0.000108</td>
      <td>0.000086</td>
      <td>0.000044</td>
      <td>0</td>
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
    </tr>
    <tr>
      <th>150</th>
      <td>0.166667</td>
      <td>0.000931</td>
      <td>0.25</td>
      <td>0.054494</td>
      <td>0.597603</td>
      <td>0.697153</td>
      <td>0.004430</td>
      <td>2</td>
    </tr>
    <tr>
      <th>151</th>
      <td>0.166667</td>
      <td>0.000070</td>
      <td>0.25</td>
      <td>0.012324</td>
      <td>0.006739</td>
      <td>0.000229</td>
      <td>0.003647</td>
      <td>6</td>
    </tr>
    <tr>
      <th>152</th>
      <td>0.500000</td>
      <td>0.006793</td>
      <td>0.25</td>
      <td>0.005896</td>
      <td>0.000015</td>
      <td>0.000025</td>
      <td>0.000003</td>
      <td>0</td>
    </tr>
    <tr>
      <th>153</th>
      <td>1.000000</td>
      <td>0.000492</td>
      <td>0.25</td>
      <td>0.002897</td>
      <td>0.000373</td>
      <td>0.000088</td>
      <td>0.000266</td>
      <td>1</td>
    </tr>
    <tr>
      <th>154</th>
      <td>1.000000</td>
      <td>0.000571</td>
      <td>0.25</td>
      <td>0.002888</td>
      <td>0.000116</td>
      <td>0.000128</td>
      <td>0.000015</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>155 rows × 8 columns</p>
</div>




```python
df.iloc[:,0:6]
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.833333</td>
      <td>0.000049</td>
      <td>0.25</td>
      <td>0.007332</td>
      <td>0.006430</td>
      <td>0.001564</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.166667</td>
      <td>0.000356</td>
      <td>0.25</td>
      <td>0.002060</td>
      <td>0.003083</td>
      <td>0.001074</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.500000</td>
      <td>0.001950</td>
      <td>0.25</td>
      <td>0.017207</td>
      <td>0.014022</td>
      <td>0.013260</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.000000</td>
      <td>0.051180</td>
      <td>0.25</td>
      <td>0.005601</td>
      <td>0.000113</td>
      <td>0.000083</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.333333</td>
      <td>0.007640</td>
      <td>0.25</td>
      <td>0.000006</td>
      <td>0.000108</td>
      <td>0.000086</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>150</th>
      <td>0.166667</td>
      <td>0.000931</td>
      <td>0.25</td>
      <td>0.054494</td>
      <td>0.597603</td>
      <td>0.697153</td>
    </tr>
    <tr>
      <th>151</th>
      <td>0.166667</td>
      <td>0.000070</td>
      <td>0.25</td>
      <td>0.012324</td>
      <td>0.006739</td>
      <td>0.000229</td>
    </tr>
    <tr>
      <th>152</th>
      <td>0.500000</td>
      <td>0.006793</td>
      <td>0.25</td>
      <td>0.005896</td>
      <td>0.000015</td>
      <td>0.000025</td>
    </tr>
    <tr>
      <th>153</th>
      <td>1.000000</td>
      <td>0.000492</td>
      <td>0.25</td>
      <td>0.002897</td>
      <td>0.000373</td>
      <td>0.000088</td>
    </tr>
    <tr>
      <th>154</th>
      <td>1.000000</td>
      <td>0.000571</td>
      <td>0.25</td>
      <td>0.002888</td>
      <td>0.000116</td>
      <td>0.000128</td>
    </tr>
  </tbody>
</table>
<p>155 rows × 6 columns</p>
</div>




```python
# PCA for visualisation

from sklearn.decomposition import PCA
pca = PCA(n_components=2)
pca.fit(df.iloc[:,0:6])

new_pca = pca.fit_transform( df.iloc[:,0:6] , y=None)
```


```python
cluster_pca_data = pd.DataFrame(new_pca, columns=["pva_1","pca_2"])
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
      <th>pva_1</th>
      <th>pca_2</th>
      <th>country</th>
      <th>K-means Cluster Labels</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.351767</td>
      <td>0.015057</td>
      <td>Afghanistan</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.301016</td>
      <td>-0.119686</td>
      <td>Albania</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.022222</td>
      <td>-0.035857</td>
      <td>Algeria</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.517841</td>
      <td>0.038231</td>
      <td>Angola</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.136762</td>
      <td>-0.090742</td>
      <td>Antigua and Barbuda</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>150</th>
      <td>0.471677</td>
      <td>0.747139</td>
      <td>United Kingdom</td>
      <td>2</td>
    </tr>
    <tr>
      <th>151</th>
      <td>0.301893</td>
      <td>-0.115255</td>
      <td>Uzbekistan</td>
      <td>6</td>
    </tr>
    <tr>
      <th>152</th>
      <td>-0.026413</td>
      <td>-0.056865</td>
      <td>Yemen</td>
      <td>0</td>
    </tr>
    <tr>
      <th>153</th>
      <td>-0.516457</td>
      <td>0.041357</td>
      <td>Zambia</td>
      <td>1</td>
    </tr>
    <tr>
      <th>154</th>
      <td>-0.516496</td>
      <td>0.041178</td>
      <td>Zimbabwe</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>155 rows × 4 columns</p>
</div>




```python
import plotly.express as px
fig = px.scatter_3d(cluster_pca_data, x='pva_1', y='pca_2', z='K-means Cluster Labels',
              symbol ='K-means Cluster Labels', color='country' )
fig.show()
```


<div>


            <div id="f6c368f9-77cd-4b29-a32a-769cc312f7bf" class="plotly-graph-div" style="height:525px; width:100%;"></div>
            <script type="text/javascript">
                require(["plotly"], function(Plotly) {
                    window.PLOTLYENV=window.PLOTLYENV || {};

                if (document.getElementById("f6c368f9-77cd-4b29-a32a-769cc312f7bf")) {
                    Plotly.newPlot(
                        'f6c368f9-77cd-4b29-a32a-769cc312f7bf',
                        [{"hovertemplate": "country=Afghanistan<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Afghanistan, 1", "marker": {"color": "#636efa", "symbol": "circle"}, "mode": "markers", "name": "Afghanistan, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.3517667258240914], "y": [0.015057235976773156], "z": [1]}, {"hovertemplate": "country=Albania<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Albania, 6", "marker": {"color": "#EF553B", "symbol": "diamond"}, "mode": "markers", "name": "Albania, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.3010160591741836], "y": [-0.11968567846302255], "z": [6]}, {"hovertemplate": "country=Algeria<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Algeria, 0", "marker": {"color": "#00cc96", "symbol": "square"}, "mode": "markers", "name": "Algeria, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.022221630527443387], "y": [-0.035856674526049605], "z": [0]}, {"hovertemplate": "country=Angola<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Angola, 1", "marker": {"color": "#ab63fa", "symbol": "circle"}, "mode": "markers", "name": "Angola, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5178405912407991], "y": [0.03823053704648661], "z": [1]}, {"hovertemplate": "country=Antigua and Barbuda<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Antigua and Barbuda, 0", "marker": {"color": "#FFA15A", "symbol": "square"}, "mode": "markers", "name": "Antigua and Barbuda, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.13676201951541467], "y": [-0.09074204114255667], "z": [0]}, {"hovertemplate": "country=Argentina<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Argentina, 0", "marker": {"color": "#19d3f3", "symbol": "square"}, "mode": "markers", "name": "Argentina, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.1409091940317644], "y": [-0.07027223434956453], "z": [0]}, {"hovertemplate": "country=Armenia<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Armenia, 6", "marker": {"color": "#FF6692", "symbol": "diamond"}, "mode": "markers", "name": "Armenia, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.30171917507271434], "y": [-0.11639490615162608], "z": [6]}, {"hovertemplate": "country=Australia<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Australia, 6", "marker": {"color": "#B6E880", "symbol": "diamond"}, "mode": "markers", "name": "Australia, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.47112230011321027], "y": [-0.12198194493298761], "z": [6]}, {"hovertemplate": "country=Austria<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Austria, 6", "marker": {"color": "#FF97FF", "symbol": "diamond"}, "mode": "markers", "name": "Austria, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.31500495360673497], "y": [-0.051268723279046836], "z": [6]}, {"hovertemplate": "country=Azerbaijan<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Azerbaijan, 6", "marker": {"color": "#FECB52", "symbol": "diamond"}, "mode": "markers", "name": "Azerbaijan, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.30165447492137193], "y": [-0.11654503671394964], "z": [6]}, {"hovertemplate": "country=Bahamas<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Bahamas, 0", "marker": {"color": "#636efa", "symbol": "square"}, "mode": "markers", "name": "Bahamas, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.1370380978447306], "y": [-0.08990877370485187], "z": [0]}, {"hovertemplate": "country=Bahrain<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Bahrain, 0", "marker": {"color": "#EF553B", "symbol": "square"}, "mode": "markers", "name": "Bahrain, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.024964951755383113], "y": [-0.04994312421061127], "z": [0]}, {"hovertemplate": "country=Bangladesh<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Bangladesh, 1", "marker": {"color": "#00cc96", "symbol": "circle"}, "mode": "markers", "name": "Bangladesh, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.3476907358830863], "y": [0.036375840820334716], "z": [1]}, {"hovertemplate": "country=Barbados<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Barbados, 0", "marker": {"color": "#ab63fa", "symbol": "square"}, "mode": "markers", "name": "Barbados, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.13703040764729152], "y": [-0.08994255277572356], "z": [0]}, {"hovertemplate": "country=Belarus<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Belarus, 3", "marker": {"color": "#FFA15A", "symbol": "x"}, "mode": "markers", "name": "Belarus, 3", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.3108203399788236], "y": [-0.08424774611003395], "z": [3]}, {"hovertemplate": "country=Belgium<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Belgium, 6", "marker": {"color": "#19d3f3", "symbol": "diamond"}, "mode": "markers", "name": "Belgium, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.3517935126474696], "y": [0.13726268543451914], "z": [6]}, {"hovertemplate": "country=Belize<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Belize, 0", "marker": {"color": "#FF6692", "symbol": "square"}, "mode": "markers", "name": "Belize, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.13695333805817214], "y": [-0.09029197237165756], "z": [0]}, {"hovertemplate": "country=Benin<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Benin, 8", "marker": {"color": "#B6E880", "symbol": "cross"}, "mode": "markers", "name": "Benin, 8", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.51500860894467], "y": [0.04431049381764786], "z": [8]}, {"hovertemplate": "country=Bhutan<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Bhutan, 1", "marker": {"color": "#FF97FF", "symbol": "circle"}, "mode": "markers", "name": "Bhutan, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.35324349202583943], "y": [0.007746852613674028], "z": [1]}, {"hovertemplate": "country=Bosnia and Herzegovina<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Bosnia and Herzegovina, 6", "marker": {"color": "#FECB52", "symbol": "diamond"}, "mode": "markers", "name": "Bosnia and Herzegovina, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.30168703747536557], "y": [-0.11642371694039436], "z": [6]}, {"hovertemplate": "country=Botswana<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Botswana, 1", "marker": {"color": "#636efa", "symbol": "circle"}, "mode": "markers", "name": "Botswana, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5166003298695317], "y": [0.040610343958307045], "z": [1]}, {"hovertemplate": "country=Brazil<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Brazil, 0", "marker": {"color": "#EF553B", "symbol": "square"}, "mode": "markers", "name": "Brazil, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.19247371733590163], "y": [0.18935963062658642], "z": [0]}, {"hovertemplate": "country=Bulgaria<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Bulgaria, 6", "marker": {"color": "#00cc96", "symbol": "diamond"}, "mode": "markers", "name": "Bulgaria, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.30161577439011306], "y": [-0.11666378849407921], "z": [6]}, {"hovertemplate": "country=Burkina Faso<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Burkina Faso, 1", "marker": {"color": "#ab63fa", "symbol": "circle"}, "mode": "markers", "name": "Burkina Faso, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5158855471959344], "y": [0.04419149626237156], "z": [1]}, {"hovertemplate": "country=Burundi<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Burundi, 8", "marker": {"color": "#FFA15A", "symbol": "cross"}, "mode": "markers", "name": "Burundi, 8", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5135869506316432], "y": [0.04713268570795567], "z": [8]}, {"hovertemplate": "country=Cabo Verde<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Cabo Verde, 8", "marker": {"color": "#19d3f3", "symbol": "cross"}, "mode": "markers", "name": "Cabo Verde, 8", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5144996066584961], "y": [0.04482351700639013], "z": [8]}, {"hovertemplate": "country=Cambodia<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Cambodia, 6", "marker": {"color": "#FF6692", "symbol": "diamond"}, "mode": "markers", "name": "Cambodia, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.46467884257310543], "y": [-0.15299301479845528], "z": [6]}, {"hovertemplate": "country=Cameroon<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Cameroon, 1", "marker": {"color": "#B6E880", "symbol": "circle"}, "mode": "markers", "name": "Cameroon, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5156807576351116], "y": [0.046051680136775304], "z": [1]}, {"hovertemplate": "country=Canada<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Canada, 0", "marker": {"color": "#FF97FF", "symbol": "square"}, "mode": "markers", "name": "Canada, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.1500346316379264], "y": [0.16685674302200373], "z": [0]}, {"hovertemplate": "country=Central African Republic<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Central African Republic, 1", "marker": {"color": "#FECB52", "symbol": "circle"}, "mode": "markers", "name": "Central African Republic, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5165858357214536], "y": [0.04068937406715135], "z": [1]}, {"hovertemplate": "country=Chad<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Chad, 1", "marker": {"color": "#636efa", "symbol": "circle"}, "mode": "markers", "name": "Chad, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.516493952911257], "y": [0.0412014545913178], "z": [1]}, {"hovertemplate": "country=Chile<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Chile, 0", "marker": {"color": "#EF553B", "symbol": "square"}, "mode": "markers", "name": "Chile, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.14673431574082899], "y": [-0.042661576980492465], "z": [0]}, {"hovertemplate": "country=China<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "China, 4", "marker": {"color": "#00cc96", "symbol": "circle"}, "mode": "markers", "name": "China, 4", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.6866520822475702], "y": [0.9573946293190687], "z": [4]}, {"hovertemplate": "country=Colombia<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Colombia, 0", "marker": {"color": "#ab63fa", "symbol": "square"}, "mode": "markers", "name": "Colombia, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.14209308953272803], "y": [-0.06449165474529346], "z": [0]}, {"hovertemplate": "country=Comoros<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Comoros, 1", "marker": {"color": "#FFA15A", "symbol": "circle"}, "mode": "markers", "name": "Comoros, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5181185194856063], "y": [0.037300534957955225], "z": [1]}, {"hovertemplate": "country=Costa Rica<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Costa Rica, 0", "marker": {"color": "#19d3f3", "symbol": "square"}, "mode": "markers", "name": "Costa Rica, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.13762082542587145], "y": [-0.08705885674825878], "z": [0]}, {"hovertemplate": "country=Croatia<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Croatia, 6", "marker": {"color": "#FF6692", "symbol": "diamond"}, "mode": "markers", "name": "Croatia, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.3021271528627489], "y": [-0.11429864339843072], "z": [6]}, {"hovertemplate": "country=Cuba<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Cuba, 0", "marker": {"color": "#B6E880", "symbol": "square"}, "mode": "markers", "name": "Cuba, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.1366318451481176], "y": [-0.0872511224820763], "z": [0]}, {"hovertemplate": "country=Cyprus<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Cyprus, 6", "marker": {"color": "#FF97FF", "symbol": "diamond"}, "mode": "markers", "name": "Cyprus, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.30101317825179424], "y": [-0.11980727655693439], "z": [6]}, {"hovertemplate": "country=Czechia<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Czechia, 6", "marker": {"color": "#FECB52", "symbol": "diamond"}, "mode": "markers", "name": "Czechia, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.3069213950574907], "y": [-0.09099417172711322], "z": [6]}, {"hovertemplate": "country=Denmark<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Denmark, 3", "marker": {"color": "#636efa", "symbol": "x"}, "mode": "markers", "name": "Denmark, 3", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.3125921007248742], "y": [-0.07491123688067834], "z": [3]}, {"hovertemplate": "country=Djibouti<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Djibouti, 1", "marker": {"color": "#EF553B", "symbol": "circle"}, "mode": "markers", "name": "Djibouti, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.516140151788303], "y": [0.04284070737750981], "z": [1]}, {"hovertemplate": "country=Dominican Republic<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Dominican Republic, 5", "marker": {"color": "#00cc96", "symbol": "diamond"}, "mode": "markers", "name": "Dominican Republic, 5", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.1332425913125182], "y": [-0.0872784839943409], "z": [5]}, {"hovertemplate": "country=Ecuador<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Ecuador, 0", "marker": {"color": "#ab63fa", "symbol": "square"}, "mode": "markers", "name": "Ecuador, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.15119095808137603], "y": [-0.020443453126610694], "z": [0]}, {"hovertemplate": "country=Egypt<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Egypt, 0", "marker": {"color": "#FFA15A", "symbol": "square"}, "mode": "markers", "name": "Egypt, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.02137270755634663], "y": [-0.03132893816274163], "z": [0]}, {"hovertemplate": "country=El Salvador<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "El Salvador, 0", "marker": {"color": "#19d3f3", "symbol": "square"}, "mode": "markers", "name": "El Salvador, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.13012562485063678], "y": [-0.10600400675816225], "z": [0]}, {"hovertemplate": "country=Equatorial Guinea<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Equatorial Guinea, 8", "marker": {"color": "#FF6692", "symbol": "cross"}, "mode": "markers", "name": "Equatorial Guinea, 8", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5135456348045789], "y": [0.04726675173322647], "z": [8]}, {"hovertemplate": "country=Eritrea<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Eritrea, 8", "marker": {"color": "#B6E880", "symbol": "cross"}, "mode": "markers", "name": "Eritrea, 8", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5143544614320184], "y": [0.045172233755103], "z": [8]}, {"hovertemplate": "country=Estonia<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Estonia, 6", "marker": {"color": "#FF97FF", "symbol": "diamond"}, "mode": "markers", "name": "Estonia, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.30178149813027055], "y": [-0.11604402984639367], "z": [6]}, {"hovertemplate": "country=Eswatini<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Eswatini, 1", "marker": {"color": "#FECB52", "symbol": "circle"}, "mode": "markers", "name": "Eswatini, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5166159156875606], "y": [0.04057483274069513], "z": [1]}, {"hovertemplate": "country=Ethiopia<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Ethiopia, 7", "marker": {"color": "#636efa", "symbol": "square"}, "mode": "markers", "name": "Ethiopia, 7", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5254529468514896], "y": [0.022259006286657338], "z": [7]}, {"hovertemplate": "country=Fiji<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Fiji, 6", "marker": {"color": "#EF553B", "symbol": "diamond"}, "mode": "markers", "name": "Fiji, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.4637534932438272], "y": [-0.15564458307389786], "z": [6]}, {"hovertemplate": "country=Finland<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Finland, 6", "marker": {"color": "#00cc96", "symbol": "diamond"}, "mode": "markers", "name": "Finland, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.3026784829415098], "y": [-0.10794578144947173], "z": [6]}, {"hovertemplate": "country=France<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "France, 2", "marker": {"color": "#ab63fa", "symbol": "x"}, "mode": "markers", "name": "France, 2", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.4892350661717118], "y": [0.8315858311457294], "z": [2]}, {"hovertemplate": "country=Gabon<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Gabon, 1", "marker": {"color": "#FFA15A", "symbol": "circle"}, "mode": "markers", "name": "Gabon, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5164742820234823], "y": [0.041173540311312706], "z": [1]}, {"hovertemplate": "country=Gambia<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Gambia, 1", "marker": {"color": "#19d3f3", "symbol": "circle"}, "mode": "markers", "name": "Gambia, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5165916251689401], "y": [0.04059784904002741], "z": [1]}, {"hovertemplate": "country=Georgia<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Georgia, 6", "marker": {"color": "#FF6692", "symbol": "diamond"}, "mode": "markers", "name": "Georgia, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.3007847263980087], "y": [-0.12084885132969829], "z": [6]}, {"hovertemplate": "country=Germany<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Germany, 9", "marker": {"color": "#B6E880", "symbol": "cross"}, "mode": "markers", "name": "Germany, 9", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.44099095691481394], "y": [0.5612633789016048], "z": [9]}, {"hovertemplate": "country=Ghana<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Ghana, 1", "marker": {"color": "#FF97FF", "symbol": "circle"}, "mode": "markers", "name": "Ghana, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5154917777368717], "y": [0.046374686320862855], "z": [1]}, {"hovertemplate": "country=Greece<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Greece, 6", "marker": {"color": "#FECB52", "symbol": "diamond"}, "mode": "markers", "name": "Greece, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.30319231750280334], "y": [-0.10883915856883003], "z": [6]}, {"hovertemplate": "country=Grenada<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Grenada, 0", "marker": {"color": "#636efa", "symbol": "square"}, "mode": "markers", "name": "Grenada, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.13696234543459035], "y": [-0.0902953193602524], "z": [0]}, {"hovertemplate": "country=Guatemala<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Guatemala, 5", "marker": {"color": "#EF553B", "symbol": "diamond"}, "mode": "markers", "name": "Guatemala, 5", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.10902281752013161], "y": [-0.15666232541872618], "z": [5]}, {"hovertemplate": "country=Guinea<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Guinea, 1", "marker": {"color": "#00cc96", "symbol": "circle"}, "mode": "markers", "name": "Guinea, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5161112926714726], "y": [0.04340180468346377], "z": [1]}, {"hovertemplate": "country=Guinea-Bissau<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Guinea-Bissau, 1", "marker": {"color": "#ab63fa", "symbol": "circle"}, "mode": "markers", "name": "Guinea-Bissau, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5165296972108093], "y": [0.04091447445099782], "z": [1]}, {"hovertemplate": "country=Guyana<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Guyana, 0", "marker": {"color": "#FFA15A", "symbol": "square"}, "mode": "markers", "name": "Guyana, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.1366588448512711], "y": [-0.09082246015899825], "z": [0]}, {"hovertemplate": "country=Haiti<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Haiti, 0", "marker": {"color": "#19d3f3", "symbol": "square"}, "mode": "markers", "name": "Haiti, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.137110692380589], "y": [-0.08939067967268242], "z": [0]}, {"hovertemplate": "country=Honduras<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Honduras, 5", "marker": {"color": "#FF6692", "symbol": "diamond"}, "mode": "markers", "name": "Honduras, 5", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.12174879946392082], "y": [-0.125134516097534], "z": [5]}, {"hovertemplate": "country=Hungary<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Hungary, 6", "marker": {"color": "#B6E880", "symbol": "diamond"}, "mode": "markers", "name": "Hungary, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.3017842739164773], "y": [-0.11264830663954926], "z": [6]}, {"hovertemplate": "country=Iceland<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Iceland, 6", "marker": {"color": "#FF97FF", "symbol": "diamond"}, "mode": "markers", "name": "Iceland, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.30139119547439736], "y": [-0.11677787690355472], "z": [6]}, {"hovertemplate": "country=India<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "India, 1", "marker": {"color": "#FECB52", "symbol": "circle"}, "mode": "markers", "name": "India, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.31350935044016753], "y": [0.21839019002845939], "z": [1]}, {"hovertemplate": "country=Indonesia<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Indonesia, 0", "marker": {"color": "#636efa", "symbol": "square"}, "mode": "markers", "name": "Indonesia, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.013086538352224175], "y": [0.008263454141441258], "z": [0]}, {"hovertemplate": "country=Iraq<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Iraq, 0", "marker": {"color": "#EF553B", "symbol": "square"}, "mode": "markers", "name": "Iraq, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.024365926290080567], "y": [-0.0471667865103394], "z": [0]}, {"hovertemplate": "country=Ireland<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Ireland, 6", "marker": {"color": "#00cc96", "symbol": "diamond"}, "mode": "markers", "name": "Ireland, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.31448350580704776], "y": [-0.05321259381330059], "z": [6]}, {"hovertemplate": "country=Israel<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Israel, 0", "marker": {"color": "#ab63fa", "symbol": "square"}, "mode": "markers", "name": "Israel, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.015034385810623078], "y": [-0.0028433997828649707], "z": [0]}, {"hovertemplate": "country=Italy<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Italy, 2", "marker": {"color": "#FFA15A", "symbol": "x"}, "mode": "markers", "name": "Italy, 2", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.5681788236741897], "y": [1.2292688042916793], "z": [2]}, {"hovertemplate": "country=Jamaica<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Jamaica, 0", "marker": {"color": "#19d3f3", "symbol": "square"}, "mode": "markers", "name": "Jamaica, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.1346049636042152], "y": [-0.09536529592376702], "z": [0]}, {"hovertemplate": "country=Japan<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Japan, 6", "marker": {"color": "#FF6692", "symbol": "diamond"}, "mode": "markers", "name": "Japan, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.4790271841027299], "y": [-0.08159907943739653], "z": [6]}, {"hovertemplate": "country=Jordan<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Jordan, 6", "marker": {"color": "#B6E880", "symbol": "diamond"}, "mode": "markers", "name": "Jordan, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.30080030833958316], "y": [-0.12066058299356286], "z": [6]}, {"hovertemplate": "country=Kazakhstan<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Kazakhstan, 6", "marker": {"color": "#FF97FF", "symbol": "diamond"}, "mode": "markers", "name": "Kazakhstan, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.30235225542481065], "y": [-0.11314252450981435], "z": [6]}, {"hovertemplate": "country=Kenya<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Kenya, 1", "marker": {"color": "#FECB52", "symbol": "circle"}, "mode": "markers", "name": "Kenya, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5159569778567012], "y": [0.04402614974134175], "z": [1]}, {"hovertemplate": "country=Kuwait<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Kuwait, 0", "marker": {"color": "#636efa", "symbol": "square"}, "mode": "markers", "name": "Kuwait, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.02709153489647296], "y": [-0.054293341623425424], "z": [0]}, {"hovertemplate": "country=Kyrgyzstan<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Kyrgyzstan, 6", "marker": {"color": "#EF553B", "symbol": "diamond"}, "mode": "markers", "name": "Kyrgyzstan, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.3008542946063482], "y": [-0.12051315741980531], "z": [6]}, {"hovertemplate": "country=Latvia<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Latvia, 6", "marker": {"color": "#00cc96", "symbol": "diamond"}, "mode": "markers", "name": "Latvia, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.300498897757901], "y": [-0.12094161071049994], "z": [6]}, {"hovertemplate": "country=Lebanon<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Lebanon, 0", "marker": {"color": "#ab63fa", "symbol": "square"}, "mode": "markers", "name": "Lebanon, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.02561707650742846], "y": [-0.053553009893245365], "z": [0]}, {"hovertemplate": "country=Liberia<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Liberia, 1", "marker": {"color": "#FFA15A", "symbol": "circle"}, "mode": "markers", "name": "Liberia, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5199859938015082], "y": [0.03270006153264003], "z": [1]}, {"hovertemplate": "country=Libya<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Libya, 5", "marker": {"color": "#19d3f3", "symbol": "diamond"}, "mode": "markers", "name": "Libya, 5", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.04295367439340685], "y": [-0.09727313041670381], "z": [5]}, {"hovertemplate": "country=Lithuania<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Lithuania, 5", "marker": {"color": "#FF6692", "symbol": "diamond"}, "mode": "markers", "name": "Lithuania, 5", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.2899224374434618], "y": [-0.14530351734578803], "z": [5]}, {"hovertemplate": "country=Luxembourg<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Luxembourg, 6", "marker": {"color": "#B6E880", "symbol": "diamond"}, "mode": "markers", "name": "Luxembourg, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.30363598581637125], "y": [-0.10711600691146211], "z": [6]}, {"hovertemplate": "country=Madagascar<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Madagascar, 1", "marker": {"color": "#FF97FF", "symbol": "circle"}, "mode": "markers", "name": "Madagascar, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5163615420785665], "y": [0.042026393465975684], "z": [1]}, {"hovertemplate": "country=Malawi<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Malawi, 1", "marker": {"color": "#FECB52", "symbol": "circle"}, "mode": "markers", "name": "Malawi, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5164727211290152], "y": [0.04127479996859073], "z": [1]}, {"hovertemplate": "country=Malaysia<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Malaysia, 6", "marker": {"color": "#636efa", "symbol": "diamond"}, "mode": "markers", "name": "Malaysia, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.46917147698233314], "y": [-0.12917185887428598], "z": [6]}, {"hovertemplate": "country=Maldives<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Maldives, 1", "marker": {"color": "#EF553B", "symbol": "circle"}, "mode": "markers", "name": "Maldives, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.35308759435671744], "y": [0.008427858478565269], "z": [1]}, {"hovertemplate": "country=Mali<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Mali, 1", "marker": {"color": "#00cc96", "symbol": "circle"}, "mode": "markers", "name": "Mali, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5162204348047437], "y": [0.042512727174701136], "z": [1]}, {"hovertemplate": "country=Malta<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Malta, 6", "marker": {"color": "#ab63fa", "symbol": "diamond"}, "mode": "markers", "name": "Malta, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.29881290016741563], "y": [-0.12590288233728955], "z": [6]}, {"hovertemplate": "country=Mauritania<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Mauritania, 0", "marker": {"color": "#FFA15A", "symbol": "square"}, "mode": "markers", "name": "Mauritania, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.02639287718957166], "y": [-0.05738616851520267], "z": [0]}, {"hovertemplate": "country=Mauritius<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Mauritius, 7", "marker": {"color": "#19d3f3", "symbol": "square"}, "mode": "markers", "name": "Mauritius, 7", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5326266619797217], "y": [0.002485698695705044], "z": [7]}, {"hovertemplate": "country=Mexico<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Mexico, 0", "marker": {"color": "#FF6692", "symbol": "square"}, "mode": "markers", "name": "Mexico, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.17512596002689626], "y": [0.049827086017754554], "z": [0]}, {"hovertemplate": "country=Mongolia<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Mongolia, 6", "marker": {"color": "#B6E880", "symbol": "diamond"}, "mode": "markers", "name": "Mongolia, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.4637957266994926], "y": [-0.1554193035706937], "z": [6]}, {"hovertemplate": "country=Montenegro<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Montenegro, 6", "marker": {"color": "#FF97FF", "symbol": "diamond"}, "mode": "markers", "name": "Montenegro, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.30061084778697567], "y": [-0.12175271508417407], "z": [6]}, {"hovertemplate": "country=Morocco<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Morocco, 0", "marker": {"color": "#FECB52", "symbol": "square"}, "mode": "markers", "name": "Morocco, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.02294121237131179], "y": [-0.04001623050432491], "z": [0]}, {"hovertemplate": "country=Mozambique<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Mozambique, 1", "marker": {"color": "#636efa", "symbol": "circle"}, "mode": "markers", "name": "Mozambique, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5163743030129647], "y": [0.04181906245175576], "z": [1]}, {"hovertemplate": "country=Namibia<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Namibia, 7", "marker": {"color": "#EF553B", "symbol": "square"}, "mode": "markers", "name": "Namibia, 7", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5282547905675684], "y": [0.01237074948416335], "z": [7]}, {"hovertemplate": "country=Netherlands<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Netherlands, 6", "marker": {"color": "#00cc96", "symbol": "diamond"}, "mode": "markers", "name": "Netherlands, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.34179179032534535], "y": [0.0853867568662187], "z": [6]}, {"hovertemplate": "country=New Zealand<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "New Zealand, 6", "marker": {"color": "#ab63fa", "symbol": "diamond"}, "mode": "markers", "name": "New Zealand, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.46501333234889775], "y": [-0.14952157905899804], "z": [6]}, {"hovertemplate": "country=Nicaragua<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Nicaragua, 3", "marker": {"color": "#FFA15A", "symbol": "x"}, "mode": "markers", "name": "Nicaragua, 3", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.14099819985344444], "y": [-0.0816214918626811], "z": [3]}, {"hovertemplate": "country=Niger<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Niger, 1", "marker": {"color": "#19d3f3", "symbol": "circle"}, "mode": "markers", "name": "Niger, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5161749423603087], "y": [0.0432972889364737], "z": [1]}, {"hovertemplate": "country=Nigeria<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Nigeria, 8", "marker": {"color": "#FF6692", "symbol": "cross"}, "mode": "markers", "name": "Nigeria, 8", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5126418644646585], "y": [0.057030584608126426], "z": [8]}, {"hovertemplate": "country=North Macedonia<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "North Macedonia, 6", "marker": {"color": "#B6E880", "symbol": "diamond"}, "mode": "markers", "name": "North Macedonia, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.3013853614471956], "y": [-0.11765445959761972], "z": [6]}, {"hovertemplate": "country=Norway<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Norway, 6", "marker": {"color": "#FF97FF", "symbol": "diamond"}, "mode": "markers", "name": "Norway, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.3075403202383475], "y": [-0.08815655819041837], "z": [6]}, {"hovertemplate": "country=Oman<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Oman, 0", "marker": {"color": "#FECB52", "symbol": "square"}, "mode": "markers", "name": "Oman, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.02530542796185701], "y": [-0.05212342671071645], "z": [0]}, {"hovertemplate": "country=Pakistan<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Pakistan, 0", "marker": {"color": "#636efa", "symbol": "square"}, "mode": "markers", "name": "Pakistan, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.14843026687806124], "y": [-0.033003371381080046], "z": [0]}, {"hovertemplate": "country=Panama<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Panama, 0", "marker": {"color": "#EF553B", "symbol": "square"}, "mode": "markers", "name": "Panama, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.14081423168411447], "y": [-0.07084950695705983], "z": [0]}, {"hovertemplate": "country=Papua New Guinea<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Papua New Guinea, 6", "marker": {"color": "#00cc96", "symbol": "diamond"}, "mode": "markers", "name": "Papua New Guinea, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.4631370282559093], "y": [-0.15690858607991617], "z": [6]}, {"hovertemplate": "country=Paraguay<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Paraguay, 0", "marker": {"color": "#ab63fa", "symbol": "square"}, "mode": "markers", "name": "Paraguay, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.13720386039135551], "y": [-0.08891864521210346], "z": [0]}, {"hovertemplate": "country=Philippines<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Philippines, 6", "marker": {"color": "#FFA15A", "symbol": "diamond"}, "mode": "markers", "name": "Philippines, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.30987605669419177], "y": [-0.07878989449620545], "z": [6]}, {"hovertemplate": "country=Poland<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Poland, 6", "marker": {"color": "#19d3f3", "symbol": "diamond"}, "mode": "markers", "name": "Poland, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.31034543366224654], "y": [-0.07329355792156085], "z": [6]}, {"hovertemplate": "country=Portugal<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Portugal, 6", "marker": {"color": "#FF6692", "symbol": "diamond"}, "mode": "markers", "name": "Portugal, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.3209469321445438], "y": [-0.026638099013973668], "z": [6]}, {"hovertemplate": "country=Qatar<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Qatar, 0", "marker": {"color": "#B6E880", "symbol": "square"}, "mode": "markers", "name": "Qatar, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.02058312011532639], "y": [-0.029552573635633243], "z": [0]}, {"hovertemplate": "country=Romania<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Romania, 6", "marker": {"color": "#FF97FF", "symbol": "diamond"}, "mode": "markers", "name": "Romania, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.30969752763202985], "y": [-0.0763617913448211], "z": [6]}, {"hovertemplate": "country=Rwanda<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Rwanda, 1", "marker": {"color": "#FECB52", "symbol": "circle"}, "mode": "markers", "name": "Rwanda, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5163778683179365], "y": [0.04170477839695239], "z": [1]}, {"hovertemplate": "country=Saint Lucia<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Saint Lucia, 0", "marker": {"color": "#636efa", "symbol": "square"}, "mode": "markers", "name": "Saint Lucia, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.1369664094928796], "y": [-0.09027971268150273], "z": [0]}, {"hovertemplate": "country=Saint Vincent and the Grenadines<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Saint Vincent and the Grenadines, 0", "marker": {"color": "#EF553B", "symbol": "square"}, "mode": "markers", "name": "Saint Vincent and the Grenadines, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.13696155758507186], "y": [-0.09030496281359374], "z": [0]}, {"hovertemplate": "country=Sao Tome and Principe<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Sao Tome and Principe, 1", "marker": {"color": "#00cc96", "symbol": "circle"}, "mode": "markers", "name": "Sao Tome and Principe, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5166228624618602], "y": [0.0404812657676298], "z": [1]}, {"hovertemplate": "country=Saudi Arabia<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Saudi Arabia, 0", "marker": {"color": "#ab63fa", "symbol": "square"}, "mode": "markers", "name": "Saudi Arabia, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.015670144057061557], "y": [-0.005779064140244995], "z": [0]}, {"hovertemplate": "country=Senegal<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Senegal, 1", "marker": {"color": "#FFA15A", "symbol": "circle"}, "mode": "markers", "name": "Senegal, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5161959811192507], "y": [0.0430348182446416], "z": [1]}, {"hovertemplate": "country=Serbia<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Serbia, 6", "marker": {"color": "#19d3f3", "symbol": "diamond"}, "mode": "markers", "name": "Serbia, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.305753286220826], "y": [-0.09675978935748172], "z": [6]}, {"hovertemplate": "country=Seychelles<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Seychelles, 1", "marker": {"color": "#FF6692", "symbol": "circle"}, "mode": "markers", "name": "Seychelles, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5166096076551693], "y": [0.040498210324334], "z": [1]}, {"hovertemplate": "country=Sierra Leone<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Sierra Leone, 1", "marker": {"color": "#B6E880", "symbol": "circle"}, "mode": "markers", "name": "Sierra Leone, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5165114786440528], "y": [0.04105475090241816], "z": [1]}, {"hovertemplate": "country=Singapore<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Singapore, 6", "marker": {"color": "#FF97FF", "symbol": "diamond"}, "mode": "markers", "name": "Singapore, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.4709457150866812], "y": [-0.12132803320620383], "z": [6]}, {"hovertemplate": "country=Slovakia<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Slovakia, 6", "marker": {"color": "#FECB52", "symbol": "diamond"}, "mode": "markers", "name": "Slovakia, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.3013889070563307], "y": [-0.11785385414093727], "z": [6]}, {"hovertemplate": "country=Slovenia<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Slovenia, 6", "marker": {"color": "#636efa", "symbol": "diamond"}, "mode": "markers", "name": "Slovenia, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.30094825954205595], "y": [-0.11783664595758261], "z": [6]}, {"hovertemplate": "country=Somalia<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Somalia, 8", "marker": {"color": "#EF553B", "symbol": "cross"}, "mode": "markers", "name": "Somalia, 8", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5150344969520895], "y": [0.04487723556199928], "z": [8]}, {"hovertemplate": "country=South Africa<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "South Africa, 1", "marker": {"color": "#00cc96", "symbol": "circle"}, "mode": "markers", "name": "South Africa, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5124900263021406], "y": [0.06097183339776572], "z": [1]}, {"hovertemplate": "country=South Sudan<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "South Sudan, 1", "marker": {"color": "#ab63fa", "symbol": "circle"}, "mode": "markers", "name": "South Sudan, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5165460868902887], "y": [0.04094423532362852], "z": [1]}, {"hovertemplate": "country=Spain<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Spain, 2", "marker": {"color": "#FFA15A", "symbol": "x"}, "mode": "markers", "name": "Spain, 2", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.544582071666677], "y": [1.102291413774356], "z": [2]}, {"hovertemplate": "country=Sri Lanka<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Sri Lanka, 1", "marker": {"color": "#19d3f3", "symbol": "circle"}, "mode": "markers", "name": "Sri Lanka, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.35240044525777703], "y": [0.012136962724226406], "z": [1]}, {"hovertemplate": "country=Sudan<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Sudan, 1", "marker": {"color": "#FF6692", "symbol": "circle"}, "mode": "markers", "name": "Sudan, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5159981021245786], "y": [0.04381813432816352], "z": [1]}, {"hovertemplate": "country=Suriname<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Suriname, 0", "marker": {"color": "#B6E880", "symbol": "square"}, "mode": "markers", "name": "Suriname, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.13670873284238647], "y": [-0.09088080897599304], "z": [0]}, {"hovertemplate": "country=Sweden<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Sweden, 3", "marker": {"color": "#FF97FF", "symbol": "x"}, "mode": "markers", "name": "Sweden, 3", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.3238513177750267], "y": [-0.017948141897153935], "z": [3]}, {"hovertemplate": "country=Switzerland<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Switzerland, 6", "marker": {"color": "#FECB52", "symbol": "diamond"}, "mode": "markers", "name": "Switzerland, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.32992347544230854], "y": [0.021867856065051584], "z": [6]}, {"hovertemplate": "country=Tajikistan<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Tajikistan, 3", "marker": {"color": "#636efa", "symbol": "x"}, "mode": "markers", "name": "Tajikistan, 3", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.021884951853729802], "y": [-0.047604999996114665], "z": [3]}, {"hovertemplate": "country=Thailand<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Thailand, 6", "marker": {"color": "#EF553B", "symbol": "diamond"}, "mode": "markers", "name": "Thailand, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.4681351198756371], "y": [-0.13298282131993946], "z": [6]}, {"hovertemplate": "country=Timor-Leste<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Timor-Leste, 6", "marker": {"color": "#00cc96", "symbol": "diamond"}, "mode": "markers", "name": "Timor-Leste, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.4619503119448053], "y": [-0.1600169096962333], "z": [6]}, {"hovertemplate": "country=Togo<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Togo, 1", "marker": {"color": "#ab63fa", "symbol": "circle"}, "mode": "markers", "name": "Togo, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5173566927825726], "y": [0.039106882156389085], "z": [1]}, {"hovertemplate": "country=Trinidad and Tobago<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Trinidad and Tobago, 0", "marker": {"color": "#FFA15A", "symbol": "square"}, "mode": "markers", "name": "Trinidad and Tobago, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.13709643904756535], "y": [-0.08956477154626374], "z": [0]}, {"hovertemplate": "country=Tunisia<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Tunisia, 0", "marker": {"color": "#19d3f3", "symbol": "square"}, "mode": "markers", "name": "Tunisia, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.025791976117880318], "y": [-0.053311284652426925], "z": [0]}, {"hovertemplate": "country=Turkey<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Turkey, 6", "marker": {"color": "#FF6692", "symbol": "diamond"}, "mode": "markers", "name": "Turkey, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.37400002201184634], "y": [0.2342482572864604], "z": [6]}, {"hovertemplate": "country=Uganda<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Uganda, 7", "marker": {"color": "#B6E880", "symbol": "square"}, "mode": "markers", "name": "Uganda, 7", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5291219451722947], "y": [0.011135257669429766], "z": [7]}, {"hovertemplate": "country=Ukraine<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Ukraine, 6", "marker": {"color": "#FF97FF", "symbol": "diamond"}, "mode": "markers", "name": "Ukraine, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.30695393255006603], "y": [-0.08993807359787814], "z": [6]}, {"hovertemplate": "country=United Arab Emirates<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "United Arab Emirates, 5", "marker": {"color": "#FECB52", "symbol": "diamond"}, "mode": "markers", "name": "United Arab Emirates, 5", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.030937908873079213], "y": [-0.05369241481695343], "z": [5]}, {"hovertemplate": "country=United Kingdom<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "United Kingdom, 2", "marker": {"color": "#636efa", "symbol": "x"}, "mode": "markers", "name": "United Kingdom, 2", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.4716766761950665], "y": [0.7471385722257922], "z": [2]}, {"hovertemplate": "country=Uzbekistan<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Uzbekistan, 6", "marker": {"color": "#EF553B", "symbol": "diamond"}, "mode": "markers", "name": "Uzbekistan, 6", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [0.3018927930332503], "y": [-0.1152546127114148], "z": [6]}, {"hovertemplate": "country=Yemen<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Yemen, 0", "marker": {"color": "#00cc96", "symbol": "square"}, "mode": "markers", "name": "Yemen, 0", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.026412639701028924], "y": [-0.05686460869628985], "z": [0]}, {"hovertemplate": "country=Zambia<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Zambia, 1", "marker": {"color": "#ab63fa", "symbol": "circle"}, "mode": "markers", "name": "Zambia, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5164570084889737], "y": [0.04135678677662421], "z": [1]}, {"hovertemplate": "country=Zimbabwe<br>K-means Cluster Labels=%{z}<br>pva_1=%{x}<br>pca_2=%{y}<extra></extra>", "legendgroup": "Zimbabwe, 1", "marker": {"color": "#FFA15A", "symbol": "circle"}, "mode": "markers", "name": "Zimbabwe, 1", "scene": "scene", "showlegend": true, "type": "scatter3d", "x": [-0.5164963966845438], "y": [0.04117773796831306], "z": [1]}],
                        {"legend": {"title": {"text": "country, K-means Cluster Labels"}, "tracegroupgap": 0}, "margin": {"t": 60}, "scene": {"domain": {"x": [0.0, 1.0], "y": [0.0, 1.0]}, "xaxis": {"title": {"text": "pva_1"}}, "yaxis": {"title": {"text": "pca_2"}}, "zaxis": {"categoryarray": [1, 6, 0, 3, 8, 4, 5, 7, 2, 9], "categoryorder": "array", "title": {"text": "K-means Cluster Labels"}}}, "template": {"data": {"bar": [{"error_x": {"color": "#2a3f5f"}, "error_y": {"color": "#2a3f5f"}, "marker": {"line": {"color": "#E5ECF6", "width": 0.5}}, "type": "bar"}], "barpolar": [{"marker": {"line": {"color": "#E5ECF6", "width": 0.5}}, "type": "barpolar"}], "carpet": [{"aaxis": {"endlinecolor": "#2a3f5f", "gridcolor": "white", "linecolor": "white", "minorgridcolor": "white", "startlinecolor": "#2a3f5f"}, "baxis": {"endlinecolor": "#2a3f5f", "gridcolor": "white", "linecolor": "white", "minorgridcolor": "white", "startlinecolor": "#2a3f5f"}, "type": "carpet"}], "choropleth": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "type": "choropleth"}], "contour": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "contour"}], "contourcarpet": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "type": "contourcarpet"}], "heatmap": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "heatmap"}], "heatmapgl": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "heatmapgl"}], "histogram": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "histogram"}], "histogram2d": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "histogram2d"}], "histogram2dcontour": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "histogram2dcontour"}], "mesh3d": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "type": "mesh3d"}], "parcoords": [{"line": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "parcoords"}], "pie": [{"automargin": true, "type": "pie"}], "scatter": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scatter"}], "scatter3d": [{"line": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scatter3d"}], "scattercarpet": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scattercarpet"}], "scattergeo": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scattergeo"}], "scattergl": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scattergl"}], "scattermapbox": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scattermapbox"}], "scatterpolar": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scatterpolar"}], "scatterpolargl": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scatterpolargl"}], "scatterternary": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scatterternary"}], "surface": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "surface"}], "table": [{"cells": {"fill": {"color": "#EBF0F8"}, "line": {"color": "white"}}, "header": {"fill": {"color": "#C8D4E3"}, "line": {"color": "white"}}, "type": "table"}]}, "layout": {"annotationdefaults": {"arrowcolor": "#2a3f5f", "arrowhead": 0, "arrowwidth": 1}, "coloraxis": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "colorscale": {"diverging": [[0, "#8e0152"], [0.1, "#c51b7d"], [0.2, "#de77ae"], [0.3, "#f1b6da"], [0.4, "#fde0ef"], [0.5, "#f7f7f7"], [0.6, "#e6f5d0"], [0.7, "#b8e186"], [0.8, "#7fbc41"], [0.9, "#4d9221"], [1, "#276419"]], "sequential": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "sequentialminus": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]]}, "colorway": ["#636efa", "#EF553B", "#00cc96", "#ab63fa", "#FFA15A", "#19d3f3", "#FF6692", "#B6E880", "#FF97FF", "#FECB52"], "font": {"color": "#2a3f5f"}, "geo": {"bgcolor": "white", "lakecolor": "white", "landcolor": "#E5ECF6", "showlakes": true, "showland": true, "subunitcolor": "white"}, "hoverlabel": {"align": "left"}, "hovermode": "closest", "mapbox": {"style": "light"}, "paper_bgcolor": "white", "plot_bgcolor": "#E5ECF6", "polar": {"angularaxis": {"gridcolor": "white", "linecolor": "white", "ticks": ""}, "bgcolor": "#E5ECF6", "radialaxis": {"gridcolor": "white", "linecolor": "white", "ticks": ""}}, "scene": {"xaxis": {"backgroundcolor": "#E5ECF6", "gridcolor": "white", "gridwidth": 2, "linecolor": "white", "showbackground": true, "ticks": "", "zerolinecolor": "white"}, "yaxis": {"backgroundcolor": "#E5ECF6", "gridcolor": "white", "gridwidth": 2, "linecolor": "white", "showbackground": true, "ticks": "", "zerolinecolor": "white"}, "zaxis": {"backgroundcolor": "#E5ECF6", "gridcolor": "white", "gridwidth": 2, "linecolor": "white", "showbackground": true, "ticks": "", "zerolinecolor": "white"}}, "shapedefaults": {"line": {"color": "#2a3f5f"}}, "ternary": {"aaxis": {"gridcolor": "white", "linecolor": "white", "ticks": ""}, "baxis": {"gridcolor": "white", "linecolor": "white", "ticks": ""}, "bgcolor": "#E5ECF6", "caxis": {"gridcolor": "white", "linecolor": "white", "ticks": ""}}, "title": {"x": 0.05}, "xaxis": {"automargin": true, "gridcolor": "white", "linecolor": "white", "ticks": "", "title": {"standoff": 15}, "zerolinecolor": "white", "zerolinewidth": 2}, "yaxis": {"automargin": true, "gridcolor": "white", "linecolor": "white", "ticks": "", "title": {"standoff": 15}, "zerolinecolor": "white", "zerolinewidth": 2}}}},
                        {"responsive": true}
                    ).then(function(){

var gd = document.getElementById('f6c368f9-77cd-4b29-a32a-769cc312f7bf');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })
                };
                });
            </script>
        </div>



```python
fig.write_image(r"C:\Users\shrey\OneDrive\Desktop\Data Engineering\Final\fig1.webp")
```


```python
cluster_pca_data.set_index(["country"],inplace=True )
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
      <th>pva_1</th>
      <th>pca_2</th>
      <th>K-means Cluster Labels</th>
    </tr>
    <tr>
      <th>country</th>
      <th></th>
      <th></th>
      <th></th>
      </thead>
    </tr>
  <tbody>
    <tr>
      <th>Afghanistan</th>
      <td>-0.351767</td>
      <td>0.015057</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Albania</th>
      <td>0.301016</td>
      <td>-0.119686</td>
      <td>6</td>
    </tr>
    <tr>
      <th>Algeria</th>
      <td>-0.022222</td>
      <td>-0.035857</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Angola</th>
      <td>-0.517841</td>
      <td>0.038231</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Antigua and Barbuda</th>
      <td>0.136762</td>
      <td>-0.090742</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>United Kingdom</th>
      <td>0.471677</td>
      <td>0.747139</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Uzbekistan</th>
      <td>0.301893</td>
      <td>-0.115255</td>
      <td>6</td>
    </tr>
    <tr>
      <th>Yemen</th>
      <td>-0.026413</td>
      <td>-0.056865</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Zambia</th>
      <td>-0.516457</td>
      <td>0.041357</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Zimbabwe</th>
      <td>-0.516496</td>
      <td>0.041178</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>155 rows × 3 columns</p>
</div>




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
plt.tick_params('both', labelsize='14', colors="white")
plt.tight_layout()
plt.grid(False)
plt.savefig(r"C:\Users\shrey\OneDrive\Desktop\Data Engineering\Final\pltt.png", format='png', bbox_inches='tight',transparent =True )
```


![png](output_79_0.png)


# Insights on Demographics and Covid cases


```python
plt.figure(figsize=(18, 6))

plt.xticks(rotation=30)
plt.title("Spread of Confirmed cases with Country Regions",fontsize=18,color="white")
sns.boxplot(x="Region Extended", y="sum_confirmed", data=merged_covid_Df,showfliers=False, )
plt.ylabel("Count of Confirmed cases",fontsize=18, color ='white')
plt.xlabel("Global Regions",fontsize=18)
plt.tick_params('both', labelsize='15',colors="white",color ='white')
plt.tight_layout()
plt.savefig('C:/Users/shrey/OneDrive/desktop/temp.png', transparent=True)
```


![png](output_81_0.png)



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




![png](output_82_1.png)



```python
sns.catplot(x="Region Extended", y="sum_recovered", data=merged_covid_Df,showfliers=False,
            row="Statusof Schools", kind="box",
                height=4, aspect=4)
plt.ylabel("Sum of Recovered cases",fontsize = 18)
plt.xlabel("Global Regions", fontsize = 18)
plt.title("Status of Schools in regions with Recovered Cases")
plt.xticks(rotation=30)
plt.ylabel("Sub Industry",size= 20, color ="white")
plt.tick_params('both', labelsize='25', colors="white")
#plt.tight_layout()
plt.savefig('C:/Users/shrey/OneDrive/desktop/temp.png', transparent=True)
#plt.savefig(r'C:\Users\shrey\OneDrive\Desktop\Data Engineering\Graph for Project\Status of Schools in regions with Recovered Cases.png')
```


![png](output_83_0.png)



```python
g = sns.catplot(x="Region Extended", y="sum_death", data=merged_covid_Df,showfliers=False,
            row="Statusof Schools", kind="box",
                height=4, aspect=4)
g.set_xticklabels()
#plt.savefig(r'C:\Users\shrey\OneDrive\Desktop\Data Engineering\Graph for Project\Status of Schools in regions with Death Cases.png')
```




    <seaborn.axisgrid.FacetGrid at 0x1e0f808eac8>




![png](output_84_1.png)



```python
g = sns.catplot(x="Region Extended", y="sum_confirmed", data=merged_covid_Df,showfliers=False,
            row="Statusof Schools", kind="box",
                height=4, aspect=4)
g.set_xticklabels()
#plt.savefig(r'C:\Users\shrey\OneDrive\Desktop\Data Engineering\Graph for Project\Status of Schools in regions with confirmed Cases.png')
```




    <seaborn.axisgrid.FacetGrid at 0x1e0fb000388>




![png](output_85_1.png)


# Time Series analysis for Corona cases:
- we need increases in corona cases by date


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
full_date_data.head()
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
      <th>0</th>
      <td>2020-01-22</td>
      <td>0</td>
      <td>AF</td>
      <td></td>
      <td>0</td>
      <td>0</td>
      <td>Afghanistan</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020-01-23</td>
      <td>0</td>
      <td>AF</td>
      <td></td>
      <td>0</td>
      <td>0</td>
      <td>Afghanistan</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2020-01-24</td>
      <td>0</td>
      <td>AF</td>
      <td></td>
      <td>0</td>
      <td>0</td>
      <td>Afghanistan</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2020-01-25</td>
      <td>0</td>
      <td>AF</td>
      <td></td>
      <td>0</td>
      <td>0</td>
      <td>Afghanistan</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020-01-26</td>
      <td>0</td>
      <td>AF</td>
      <td></td>
      <td>0</td>
      <td>0</td>
      <td>Afghanistan</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Function to get timeseries data for each country
def country_time_series(country):

    return full_date_data.loc[full_date_data["country"] == country]
```


```python
# Preview
country_time_series("Afghanistan")
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
      <th>0</th>
      <td>2020-01-22</td>
      <td>0</td>
      <td>AF</td>
      <td></td>
      <td>0</td>
      <td>0</td>
      <td>Afghanistan</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020-01-23</td>
      <td>0</td>
      <td>AF</td>
      <td></td>
      <td>0</td>
      <td>0</td>
      <td>Afghanistan</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2020-01-24</td>
      <td>0</td>
      <td>AF</td>
      <td></td>
      <td>0</td>
      <td>0</td>
      <td>Afghanistan</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2020-01-25</td>
      <td>0</td>
      <td>AF</td>
      <td></td>
      <td>0</td>
      <td>0</td>
      <td>Afghanistan</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020-01-26</td>
      <td>0</td>
      <td>AF</td>
      <td></td>
      <td>0</td>
      <td>0</td>
      <td>Afghanistan</td>
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
    </tr>
    <tr>
      <th>102</th>
      <td>2020-05-03</td>
      <td>2704</td>
      <td>AF</td>
      <td></td>
      <td>85</td>
      <td>345</td>
      <td>Afghanistan</td>
    </tr>
    <tr>
      <th>103</th>
      <td>2020-05-04</td>
      <td>2894</td>
      <td>AF</td>
      <td></td>
      <td>90</td>
      <td>397</td>
      <td>Afghanistan</td>
    </tr>
    <tr>
      <th>104</th>
      <td>2020-05-05</td>
      <td>3224</td>
      <td>AF</td>
      <td></td>
      <td>95</td>
      <td>421</td>
      <td>Afghanistan</td>
    </tr>
    <tr>
      <th>105</th>
      <td>2020-05-06</td>
      <td>3392</td>
      <td>AF</td>
      <td></td>
      <td>104</td>
      <td>458</td>
      <td>Afghanistan</td>
    </tr>
    <tr>
      <th>106</th>
      <td>2020-05-07</td>
      <td>3563</td>
      <td>AF</td>
      <td></td>
      <td>106</td>
      <td>468</td>
      <td>Afghanistan</td>
    </tr>
  </tbody>
</table>
<p>107 rows × 7 columns</p>
</div>



# Creating Timeline analysis with Increasing cases by date


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
      <td>2260344</td>
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
plt.ylabel('Cases Counts', fontsize = 18, color='white');
plt.title('Confirm cases vs recovered vs Deaths', fontsize= 30, color = 'white')
plt.legend();
plt.ylabel("Count of Confirmed cases",fontsize=18, color ='white')
plt.xlabel("Time Line",fontsize=18,color='white')
plt.tick_params('both', labelsize='15',colors="white",color ='white')
plt.tight_layout()
plt.grid(False)
plt.savefig('C:/Users/shrey/OneDrive/desktop/temp.png', transparent=True)
#plt.savefig(r'C:\Users\shrey\OneDrive\Desktop\Data Engineering\Graph for Project\Corona Cases Deaths Recovered.png')
```


![png](output_96_0.png)


# Modeling with Prophet


```python
import pandas as pd
from fbprophet import Prophet

```


```python
# Copy of main df
time_series = df_timeseries.copy()
import fbprophet
# Prophet requires columns ds (Date) and y (value)
time_series = time_series.rename(columns={'date': 'ds', 'count_confirmed': 'y'})
# Put market cap in billions
time_series['y'] = time_series['y'] / 1e9
# Make the prophet model and fit on the data
gm_prophet = fbprophet.Prophet(changepoint_prior_scale=0.15)
gm_prophet.fit(time_series)
```


```python
df_timeseries
```
