---
title: "S&P 500 Analysis with Covid 19 continued"
date: 2020-05-17
tags: [Data Analysis]
header:
  image: "/images/titanic_analysis/percept.jpg"
excerpt: "Data Analysis on stocks and covid-19"
mathjax: "true"
---




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

<img src="{{ site.url }}{{ site.baseurl }}/images/stocks_covid/output_96_0.png" alt="linearly separable data">



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

<img src="{{ site.url }}{{ site.baseurl }}/images/stocks_covid/output_98_0.png" alt="linearly separable data">




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



<img src="{{ site.url }}{{ site.baseurl }}/images/stocks_covid/output_99_1.png" alt="linearly separable data">




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


<img src="{{ site.url }}{{ site.baseurl }}/images/stocks_covid/output_100_0.png" alt="linearly separable data">



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
```

<img src="{{ site.url }}{{ site.baseurl }}/images/stocks_covid/output_111_0.png" alt="linearly separable data">



### Insights from trendline:
#### - We can see how death cases are increasing with the lowest rate while Confirm cases have highest rate.

#### - We see a strong curve in recovered and confirm cases showing a flattening of the curve after 2020-02-15.
