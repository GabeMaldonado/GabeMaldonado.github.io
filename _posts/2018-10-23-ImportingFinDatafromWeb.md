---
title: "Importing Financial Data form the Web"
date: 2018-10-23
tags: [data science, data visualizations, fintech]
mathjax: "True"
---

# Using pandas_datareader to import financial data from the web to a dataframe


It is convinient to use pandas_datareader to import fiancial data directly into a dataaframe. 
The process is very straight-forward, there is minimal code required to to do and the data si available from different sources such as Google Finance, Yahoo!, the Federal Reserve, the World Bank, etc.


```python
import pandas as pd
import numpy as np
import pandas_datareader as pdr 
from datetime import datetime
#import datetime
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

    2018-10-23 21:29:25.592488
    2017-10-23 00:00:00



```python
stock_data = pdr.DataReader('AAPL', 'yahoo', start, end)
stock_data.info()
```

    <class 'pandas.core.frame.DataFrame'>
    DatetimeIndex: 253 entries, 2017-10-23 to 2018-10-23
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
stock_data.head()
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
      <th>2017-10-23</th>
      <td>156.889999</td>
      <td>157.690002</td>
      <td>155.500000</td>
      <td>156.169998</td>
      <td>153.843857</td>
      <td>21984300</td>
    </tr>
    <tr>
      <th>2017-10-24</th>
      <td>156.289993</td>
      <td>157.419998</td>
      <td>156.199997</td>
      <td>157.100006</td>
      <td>154.760010</td>
      <td>17757200</td>
    </tr>
    <tr>
      <th>2017-10-25</th>
      <td>156.910004</td>
      <td>157.550003</td>
      <td>155.270004</td>
      <td>156.410004</td>
      <td>154.080307</td>
      <td>21207100</td>
    </tr>
    <tr>
      <th>2017-10-26</th>
      <td>157.229996</td>
      <td>157.830002</td>
      <td>156.779999</td>
      <td>157.410004</td>
      <td>155.065399</td>
      <td>17000500</td>
    </tr>
    <tr>
      <th>2017-10-27</th>
      <td>159.289993</td>
      <td>163.600006</td>
      <td>158.699997</td>
      <td>163.050003</td>
      <td>160.621384</td>
      <td>44454200</td>
    </tr>
  </tbody>
</table>
</div>




```python
stock_data.tail()
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
      <th>2018-10-17</th>
      <td>222.300003</td>
      <td>222.639999</td>
      <td>219.339996</td>
      <td>221.190002</td>
      <td>221.190002</td>
      <td>22885400</td>
    </tr>
    <tr>
      <th>2018-10-18</th>
      <td>217.860001</td>
      <td>219.740005</td>
      <td>213.000000</td>
      <td>216.020004</td>
      <td>216.020004</td>
      <td>32581300</td>
    </tr>
    <tr>
      <th>2018-10-19</th>
      <td>218.059998</td>
      <td>221.259995</td>
      <td>217.429993</td>
      <td>219.309998</td>
      <td>219.309998</td>
      <td>33078700</td>
    </tr>
    <tr>
      <th>2018-10-22</th>
      <td>219.789993</td>
      <td>223.360001</td>
      <td>218.940002</td>
      <td>220.649994</td>
      <td>220.649994</td>
      <td>28792100</td>
    </tr>
    <tr>
      <th>2018-10-23</th>
      <td>215.830002</td>
      <td>223.250000</td>
      <td>214.699997</td>
      <td>222.729996</td>
      <td>222.729996</td>
      <td>38616200</td>
    </tr>
  </tbody>
</table>
</div>




```python
#View historical trend of the closing price Adj Close column
stock_data['Adj Close'].plot(legend=True, figsize=(10,4))
```




    <matplotlib.axes._subplots.AxesSubplot at 0x11f3f0160>

![alt]({{ site.url }}{{ site.baseurl }}/images/datareader_appl.png)


