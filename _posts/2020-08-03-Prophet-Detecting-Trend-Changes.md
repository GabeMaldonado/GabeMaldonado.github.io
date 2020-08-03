---
title: "Prophet - Detecting Changes in Trend"
date: 2020-08-03
tags: [ML&AI]
excerpt: "Prophet - Detecting Changes in Trend"
mathjax: "True"
---

## Detecting Trend Changes

```python

import pandas as pd 
import numpy as np 
from fbprophet import Prophet

```

## Load Data

Load Hospitality dataset

```python
df = pd.read_csv('HospitalityEmployees.csv')

# rename columns to Prophet specs
# Change date to time series

df.columns = ['ds', 'y']
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
      <td>1990-01-01</td>
      <td>1064.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1990-02-01</td>
      <td>1074.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1990-03-01</td>
      <td>1090.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1990-04-01</td>
      <td>1097.4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1990-05-01</td>
      <td>1108.7</td>
    </tr>
  </tbody>
</table>


