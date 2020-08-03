---
title: "Prophet for TimeSeries Forecasting"
date: 2020-08-03
tags: [ML&AI]
excerpt: "Prophet for TimeSeries Forecasting"
mathjax: "True"
---

## Facebook's Prophet for TimeSeries Analysis

Prophet is a library used to analyze and forcast timeseries data. According to [Prophet's homepage](https://facebook.github.io/prophet/): 
"Prophet is a procedure for forecasting time series data based on an additive model where non-linear trends are fit with yearly, weekly, and daily seasonality, plus holiday effects. It works best with time series that have strong seasonal effects and several seasons of historical data. Prophet is robust to missing data and shifts in the trend, and typically handles outliers well"

This python notebook will provide a quick introduction to the Prophet library.

```python
import numpy as np
import pandas as pd

from fbprophet import Prophet
```

## Load Data

Load the Beer, Wine and Liquor dataset. 
Prophet requires the data to be in a particular format. It only takes two columns and they must be named *ds* and *y* where *ds* is a pandas datetime object. By default, prophets expects daily date but we can work with other frequencies.

```python
# Load the data, index does not need to be set and dates do not need to be parsed.
df = pd.read_csv('BeerWineLiquor.csv')
df.head()
```
```
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>date</th>
      <th>beer</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1/1/1992</td>
      <td>1509</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2/1/1992</td>
      <td>1541</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3/1/1992</td>
      <td>1597</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4/1/1992</td>
      <td>1675</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5/1/1992</td>
      <td>1822</td>
    </tr>
  </tbody>
</table>
```

