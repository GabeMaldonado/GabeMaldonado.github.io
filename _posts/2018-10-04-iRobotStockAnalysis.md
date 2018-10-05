---
title: "iRobot Stock Analysis"
date: 2018-10-04
header:
   image: "/images/IMG_0880.jpg"
tags: [data science, data visualizations, machine learning]
excerpt: "Data Science, Data Visualizations, Machine Learning"
---

# In this Jupyter Notebook I have done some exploratory data analysis of iRobot stock.

```python
import quandl
import pandas as pd
import numpy as np
import pandas_datareader as pdr 
#from datetime import datetime
import datetime
from __future__ import division
import math
from sklearn import preprocessing, cross_validation, svm
from sklearn.linear_model import LinearRegression
import pickle

import matplotlib.pyplot as plt
import seaborn as sns
sns.set_style('whitegrid')
%matplotlib inline
```


```python
#Set times, -1 = yearg ago from now
end = datetime.now()
print (end)

start = datetime(end.year -1, end.month, end.day)
print (start)
```

    2018-06-07 22:12:03.122418
    2017-06-07 00:00:00



```python
#Import data from yahoo and assign it to IRBT
IRBT = pdr.DataReader('IRBT', 'yahoo', start, end)

```


```python
IRBT.info()
```

    <class 'pandas.core.frame.DataFrame'>
    DatetimeIndex: 253 entries, 2017-06-07 to 2018-06-07
    Data columns (total 6 columns):
    Open         253 non-null float64
    High         253 non-null float64
    Low          253 non-null float64
    Close        253 non-null float64
    Adj Close    253 non-null float64
    Volume       253 non-null int64
    dtypes: float64(5), int64(1)
    memory usage: 13.8 KB



```python
#View historical trend of the closing price Adj Close column
IRBT['Adj Close'].plot(legend=True, figsize=(10,4))
```




    <matplotlib.axes._subplots.AxesSubplot at 0x11efda048>




![png](iRobot%20Stock_files/iRobot%20Stock_4_1.png)



```python
IRBT.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
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
      <th>2017-06-07</th>
      <td>96.860001</td>
      <td>99.309998</td>
      <td>96.080002</td>
      <td>99.230003</td>
      <td>99.230003</td>
      <td>687500</td>
    </tr>
    <tr>
      <th>2017-06-08</th>
      <td>98.980003</td>
      <td>100.480003</td>
      <td>97.820000</td>
      <td>99.930000</td>
      <td>99.930000</td>
      <td>633700</td>
    </tr>
    <tr>
      <th>2017-06-09</th>
      <td>100.419998</td>
      <td>100.949997</td>
      <td>93.129997</td>
      <td>95.989998</td>
      <td>95.989998</td>
      <td>1135700</td>
    </tr>
    <tr>
      <th>2017-06-12</th>
      <td>95.989998</td>
      <td>98.760002</td>
      <td>91.510002</td>
      <td>98.650002</td>
      <td>98.650002</td>
      <td>1133200</td>
    </tr>
    <tr>
      <th>2017-06-13</th>
      <td>99.430000</td>
      <td>101.540001</td>
      <td>98.500000</td>
      <td>100.279999</td>
      <td>100.279999</td>
      <td>801200</td>
    </tr>
  </tbody>
</table>
</div>




```python
IRBT.tail()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
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
      <th>2018-06-01</th>
      <td>62.820000</td>
      <td>64.349998</td>
      <td>62.820000</td>
      <td>63.730000</td>
      <td>63.730000</td>
      <td>619600</td>
    </tr>
    <tr>
      <th>2018-06-04</th>
      <td>64.099998</td>
      <td>65.639999</td>
      <td>64.099998</td>
      <td>65.360001</td>
      <td>65.360001</td>
      <td>659500</td>
    </tr>
    <tr>
      <th>2018-06-05</th>
      <td>65.290001</td>
      <td>66.080002</td>
      <td>65.000000</td>
      <td>65.919998</td>
      <td>65.919998</td>
      <td>510500</td>
    </tr>
    <tr>
      <th>2018-06-06</th>
      <td>66.220001</td>
      <td>69.250000</td>
      <td>65.949997</td>
      <td>68.349998</td>
      <td>68.349998</td>
      <td>933200</td>
    </tr>
    <tr>
      <th>2018-06-07</th>
      <td>68.160004</td>
      <td>69.290001</td>
      <td>67.290001</td>
      <td>69.040001</td>
      <td>69.040001</td>
      <td>625500</td>
    </tr>
  </tbody>
</table>
</div>




```python
df = IRBT[['Open','High','Low','Close', 'Volume']]

df['HL_PCT'] = (df['High']-df['Close'])/ df['Close'] * 100.0

df['PCT_Change'] = (df['Close']-df['Open'])/ df['Open'] * 100.0

```


```python
df = df [['Close','HL_PCT','PCT_Change','Volume']]
```


```python
df.tail()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Close</th>
      <th>HL_PCT</th>
      <th>PCT_Change</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-06-01</th>
      <td>63.730000</td>
      <td>0.972851</td>
      <td>1.448583</td>
      <td>619600</td>
    </tr>
    <tr>
      <th>2018-06-04</th>
      <td>65.360001</td>
      <td>0.428394</td>
      <td>1.965683</td>
      <td>659500</td>
    </tr>
    <tr>
      <th>2018-06-05</th>
      <td>65.919998</td>
      <td>0.242725</td>
      <td>0.964921</td>
      <td>510500</td>
    </tr>
    <tr>
      <th>2018-06-06</th>
      <td>68.349998</td>
      <td>1.316755</td>
      <td>3.216546</td>
      <td>933200</td>
    </tr>
    <tr>
      <th>2018-06-07</th>
      <td>69.040001</td>
      <td>0.362109</td>
      <td>1.291075</td>
      <td>625500</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Define a label -- Adj Price in the future
forecast_col = 'Close' 
df.fillna(-99999, inplace=True)
forecast_out = int(math.ceil(0.01*len(df)))

df['Label'] = df[forecast_col].shift(-forecast_out)
df.dropna(inplace=True)

df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Close</th>
      <th>HL_PCT</th>
      <th>PCT_Change</th>
      <th>Volume</th>
      <th>Label</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2017-06-07</th>
      <td>99.230003</td>
      <td>0.080616</td>
      <td>2.446833</td>
      <td>687500</td>
      <td>98.650002</td>
    </tr>
    <tr>
      <th>2017-06-08</th>
      <td>99.930000</td>
      <td>0.550388</td>
      <td>0.959787</td>
      <td>633700</td>
      <td>100.279999</td>
    </tr>
    <tr>
      <th>2017-06-09</th>
      <td>95.989998</td>
      <td>5.167204</td>
      <td>-4.411472</td>
      <td>1135700</td>
      <td>101.989998</td>
    </tr>
    <tr>
      <th>2017-06-12</th>
      <td>98.650002</td>
      <td>0.111505</td>
      <td>2.771126</td>
      <td>1133200</td>
      <td>97.970001</td>
    </tr>
    <tr>
      <th>2017-06-13</th>
      <td>100.279999</td>
      <td>1.256484</td>
      <td>0.854872</td>
      <td>801200</td>
      <td>96.269997</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[['Close','Label']].plot(subplots=False,legend=True, figsize=(10,4))
```




    <matplotlib.axes._subplots.AxesSubplot at 0x121a8f588>




![png](iRobot%20Stock_files/iRobot%20Stock_11_1.png)



```python
#Define features X and labels y

X = np.array(df.drop(['Label'],1))

y = np.array(df['Label'])

#Scale X
X = preprocessing.scale(X)
y = np.array(df['Label'])
print(len(X),len(y))
```

    250 250



```python
#Create training and testing sets
X_train, X_test, y_train, y_test = cross_validation.train_test_split(X, y, test_size=0.2)

```


```python
#Define a classifier and test it .fit=train / .score=test
classf = LinearRegression()
classf.fit(X_train, y_train)
accuracy = classf.score(X_test, y_test)

print(forecast_out)
print(accuracy)
```

    3
    0.849147136972



```python
#Using the Support Vector Machine algo

classf = svm.SVR()
classf.fit(X_train, y_train)
accuracy = classf.score(X_test, y_test)

print(forecast_out)
print(accuracy)
```

    3
    0.708794197356



```python
#Forecasting into the future...
df['Label'] = df[forecast_col].shift(-forecast_out)
X = np.array(df.drop(['Label'],1))
X = preprocessing.scale(X)
X_lately = X[-forecast_out:]
X = X[:-forecast_out]

df.dropna(inplace=True)
y = np.array(df['Label'])


#Create training and testing sets
X_train, X_test, y_train, y_test = cross_validation.train_test_split(X, y, test_size=0.2)

#Define a classifier and test it .fit=train / .score=test
classf = LinearRegression()
classf.fit(X_train, y_train)
accuracy = classf.score(X_test, y_test)

print(forecast_out)
print(accuracy)

```

    3
    0.925348943641



```python
forecast_set = classf.predict(X_lately)
print (forecast_set, accuracy, forecast_out)
```

    [ 62.91718632  63.80245711  65.64647982] 0.925348943641 3



```python
df['Forecast']= np.nan
```


```python
last_date = df.iloc[-1].name
last_unix = last_date.timestamp()
one_day = 86400
next_unix = last_unix + one_day

for i in forecast_set:
    next_date = datetime.datetime.fromtimestamp(next_unix)
    next_unix += one_day
    df.loc[next_date] = [np.nan for _ in range(len(df.columns)-1)]+ [i]
   

df['Close'].plot()
df['Forecast'].plot()
plt.xlabel('Date')
plt.ylabel('Price')
plt.show()
```


![png](iRobot%20Stock_files/iRobot%20Stock_19_0.png)



```python
df[['Close','Forecast']].plot(subplots=False,legend=True, figsize=(10,4))
```




    <matplotlib.axes._subplots.AxesSubplot at 0x121f011d0>




![png](iRobot%20Stock_files/iRobot%20Stock_20_1.png)



```python
df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Close</th>
      <th>HL_PCT</th>
      <th>PCT_Change</th>
      <th>Volume</th>
      <th>Label</th>
      <th>Forecast</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2017-06-07</th>
      <td>99.230003</td>
      <td>0.080616</td>
      <td>2.446833</td>
      <td>687500.0</td>
      <td>98.650002</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-06-08</th>
      <td>99.930000</td>
      <td>0.550388</td>
      <td>0.959787</td>
      <td>633700.0</td>
      <td>100.279999</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-06-09</th>
      <td>95.989998</td>
      <td>5.167204</td>
      <td>-4.411472</td>
      <td>1135700.0</td>
      <td>101.989998</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-06-12</th>
      <td>98.650002</td>
      <td>0.111505</td>
      <td>2.771126</td>
      <td>1133200.0</td>
      <td>97.970001</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-06-13</th>
      <td>100.279999</td>
      <td>1.256484</td>
      <td>0.854872</td>
      <td>801200.0</td>
      <td>96.269997</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-06-14</th>
      <td>101.989998</td>
      <td>2.568882</td>
      <td>1.644411</td>
      <td>1283400.0</td>
      <td>98.779999</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-06-15</th>
      <td>97.970001</td>
      <td>3.143822</td>
      <td>-2.225545</td>
      <td>1657400.0</td>
      <td>97.730003</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-06-16</th>
      <td>96.269997</td>
      <td>2.690354</td>
      <td>-2.442241</td>
      <td>1599000.0</td>
      <td>101.080002</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-06-19</th>
      <td>98.779999</td>
      <td>0.496050</td>
      <td>1.877063</td>
      <td>883400.0</td>
      <td>100.430000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-06-20</th>
      <td>97.730003</td>
      <td>2.302261</td>
      <td>-1.282825</td>
      <td>604500.0</td>
      <td>101.199997</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-06-21</th>
      <td>101.080002</td>
      <td>1.226749</td>
      <td>2.723577</td>
      <td>780200.0</td>
      <td>100.980003</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-06-22</th>
      <td>100.430000</td>
      <td>1.214778</td>
      <td>-0.554508</td>
      <td>560200.0</td>
      <td>90.650002</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-06-23</th>
      <td>101.199997</td>
      <td>1.482213</td>
      <td>0.806851</td>
      <td>696400.0</td>
      <td>92.470001</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-06-26</th>
      <td>100.980003</td>
      <td>1.871658</td>
      <td>-0.951441</td>
      <td>392100.0</td>
      <td>86.779999</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-06-27</th>
      <td>90.650002</td>
      <td>10.821839</td>
      <td>-9.675168</td>
      <td>1906600.0</td>
      <td>84.139999</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-06-28</th>
      <td>92.470001</td>
      <td>1.254457</td>
      <td>1.581898</td>
      <td>1359000.0</td>
      <td>83.540001</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-06-29</th>
      <td>86.779999</td>
      <td>6.914036</td>
      <td>-6.426568</td>
      <td>1299900.0</td>
      <td>82.180000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-06-30</th>
      <td>84.139999</td>
      <td>3.220821</td>
      <td>-2.412436</td>
      <td>1125500.0</td>
      <td>80.540001</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-07-03</th>
      <td>83.540001</td>
      <td>1.460379</td>
      <td>0.288113</td>
      <td>886300.0</td>
      <td>83.650002</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-07-05</th>
      <td>82.180000</td>
      <td>2.579707</td>
      <td>-1.035647</td>
      <td>1140600.0</td>
      <td>84.470001</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-07-06</th>
      <td>80.540001</td>
      <td>1.092621</td>
      <td>-0.297101</td>
      <td>1400600.0</td>
      <td>83.239998</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-07-07</th>
      <td>83.650002</td>
      <td>1.016136</td>
      <td>4.171854</td>
      <td>989000.0</td>
      <td>85.019997</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-07-10</th>
      <td>84.470001</td>
      <td>0.627441</td>
      <td>0.607434</td>
      <td>776500.0</td>
      <td>84.620003</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-07-11</th>
      <td>83.239998</td>
      <td>2.570878</td>
      <td>-1.257420</td>
      <td>812600.0</td>
      <td>83.989998</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-07-12</th>
      <td>85.019997</td>
      <td>0.270528</td>
      <td>1.069893</td>
      <td>814900.0</td>
      <td>84.900002</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-07-13</th>
      <td>84.620003</td>
      <td>1.217205</td>
      <td>-1.202567</td>
      <td>527500.0</td>
      <td>84.750000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-07-14</th>
      <td>83.989998</td>
      <td>1.154901</td>
      <td>-0.896758</td>
      <td>424200.0</td>
      <td>86.769997</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-07-17</th>
      <td>84.900002</td>
      <td>0.895173</td>
      <td>1.035348</td>
      <td>556900.0</td>
      <td>85.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-07-18</th>
      <td>84.750000</td>
      <td>0.436582</td>
      <td>-0.200186</td>
      <td>554000.0</td>
      <td>88.470001</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-07-19</th>
      <td>86.769997</td>
      <td>0.806735</td>
      <td>2.070339</td>
      <td>559200.0</td>
      <td>90.379997</td>
      <td>NaN</td>
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
      <th>2018-04-23</th>
      <td>59.950001</td>
      <td>5.054210</td>
      <td>-4.018569</td>
      <td>2061800.0</td>
      <td>58.240002</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-04-24</th>
      <td>59.080002</td>
      <td>4.807034</td>
      <td>-2.039461</td>
      <td>2178300.0</td>
      <td>58.580002</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-04-25</th>
      <td>57.060001</td>
      <td>8.499823</td>
      <td>-7.789269</td>
      <td>2951800.0</td>
      <td>58.360001</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-04-26</th>
      <td>58.240002</td>
      <td>2.970465</td>
      <td>2.050117</td>
      <td>1423100.0</td>
      <td>57.830002</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-04-27</th>
      <td>58.580002</td>
      <td>1.502214</td>
      <td>0.652923</td>
      <td>1150700.0</td>
      <td>58.310001</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-04-30</th>
      <td>58.360001</td>
      <td>0.822479</td>
      <td>-0.273409</td>
      <td>616500.0</td>
      <td>57.180000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-05-01</th>
      <td>57.830002</td>
      <td>0.916478</td>
      <td>-0.344644</td>
      <td>709300.0</td>
      <td>60.020000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-05-02</th>
      <td>58.310001</td>
      <td>0.840333</td>
      <td>1.144838</td>
      <td>549700.0</td>
      <td>61.759998</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-05-03</th>
      <td>57.180000</td>
      <td>2.168587</td>
      <td>-1.464758</td>
      <td>654200.0</td>
      <td>62.270000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-05-04</th>
      <td>60.020000</td>
      <td>0.216598</td>
      <td>5.520392</td>
      <td>850600.0</td>
      <td>62.060001</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-05-07</th>
      <td>61.759998</td>
      <td>0.259067</td>
      <td>2.404240</td>
      <td>824500.0</td>
      <td>61.930000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-05-08</th>
      <td>62.270000</td>
      <td>0.112414</td>
      <td>0.630250</td>
      <td>497600.0</td>
      <td>62.360001</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-05-09</th>
      <td>62.060001</td>
      <td>0.805672</td>
      <td>-0.369241</td>
      <td>517900.0</td>
      <td>62.299999</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-05-10</th>
      <td>61.930000</td>
      <td>1.356370</td>
      <td>-0.625802</td>
      <td>584900.0</td>
      <td>61.259998</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-05-11</th>
      <td>62.360001</td>
      <td>0.384857</td>
      <td>0.694334</td>
      <td>485200.0</td>
      <td>62.310001</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-05-14</th>
      <td>62.299999</td>
      <td>1.364371</td>
      <td>-0.272134</td>
      <td>509600.0</td>
      <td>62.880001</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-05-15</th>
      <td>61.259998</td>
      <td>1.142672</td>
      <td>-0.969937</td>
      <td>661000.0</td>
      <td>62.430000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-05-16</th>
      <td>62.310001</td>
      <td>0.866630</td>
      <td>1.070558</td>
      <td>462000.0</td>
      <td>62.889999</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-05-17</th>
      <td>62.880001</td>
      <td>0.795165</td>
      <td>0.930982</td>
      <td>693100.0</td>
      <td>63.160000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-05-18</th>
      <td>62.430000</td>
      <td>0.736824</td>
      <td>-0.731434</td>
      <td>464000.0</td>
      <td>61.869999</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-05-21</th>
      <td>62.889999</td>
      <td>0.079504</td>
      <td>0.143312</td>
      <td>633900.0</td>
      <td>62.389999</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-05-22</th>
      <td>63.160000</td>
      <td>2.184929</td>
      <td>-0.158075</td>
      <td>621600.0</td>
      <td>62.730000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-05-23</th>
      <td>61.869999</td>
      <td>1.874899</td>
      <td>-1.574932</td>
      <td>654600.0</td>
      <td>64.839996</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-05-24</th>
      <td>62.389999</td>
      <td>0.112197</td>
      <td>0.873082</td>
      <td>434200.0</td>
      <td>65.300003</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-05-25</th>
      <td>62.730000</td>
      <td>0.031883</td>
      <td>0.593327</td>
      <td>380900.0</td>
      <td>62.410000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-05-29</th>
      <td>64.839996</td>
      <td>0.046279</td>
      <td>3.413070</td>
      <td>739800.0</td>
      <td>63.730000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-05-30</th>
      <td>65.300003</td>
      <td>0.459410</td>
      <td>0.554359</td>
      <td>644800.0</td>
      <td>65.360001</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-05-31</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>62.917186</td>
    </tr>
    <tr>
      <th>2018-06-01</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>63.802457</td>
    </tr>
    <tr>
      <th>2018-06-02</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>65.646480</td>
    </tr>
  </tbody>
</table>
<p>250 rows × 6 columns</p>
</div>


