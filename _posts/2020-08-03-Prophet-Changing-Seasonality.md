---
title: "Prophet-Changing Seasonality"
date: 2020-08-03
tags: [ML&AI]
excerpt: "Changing Seasonality with Prophet"
mathjax: "True"
---

## Changing Seasonality with Prophet

###Load Data

Load Airline dataset

```python
import pandas as pd
import numpy as np
from fbprophet import Prophet

df = pd.read_csv('airline_passengers.csv')
```

Changes in seasonality can be either additive or multiplicative so we have to keep that in mind when looking at seasonality.

## Format Data to Prophet's Specs

```python
# rename columns
df.columns = ['ds', 'y']

# convert date index to timeseries
df['ds'] = pd.to_datetime(df['ds'])

df.head()
```
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>ds</th>
      <th>y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1949-01-01</td>
      <td>112</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1949-02-01</td>
      <td>118</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1949-03-01</td>
      <td>132</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1949-04-01</td>
      <td>129</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1949-05-01</td>
      <td>121</td>
    </tr>
  </tbody>
</table>






