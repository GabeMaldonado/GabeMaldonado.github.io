---
title: "Prophet Evaluation Metrics"
date: 2020-08-03
tags: [ML&AI]
excerpt: "Prophet Evaluation Metrics"
mathjax: "True"
---

```python
import pandas as pd
from fbprophet import Prophet
%matplotlib inline
```

## Load Data
 
 In this notebook we will use the  Miles_Traveled dataset.

```python
 df = pd.read_csv('Miles_Traveled.csv')
 df.head()
 ```
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>DATE</th>
      <th>TRFVOLUSM227NFWA</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1970-01-01</td>
      <td>80173.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1970-02-01</td>
      <td>77442.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1970-03-01</td>
      <td>90223.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1970-04-01</td>
      <td>89956.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1970-05-01</td>
      <td>97972.0</td>
    </tr>
  </tbody>
</table>

```python
df.info()
```
```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 588 entries, 0 to 587
Data columns (total 2 columns):
DATE                588 non-null object
TRFVOLUSM227NFWA    588 non-null float64
dtypes: float64(1), object(1)
memory usage: 9.3+ KB
```

```python
df.describe()
```

```
TRFVOLUSM227NFWA
count	588.000000
mean	190420.380952
std	57795.538934
min	77442.000000
25%	133579.000000
50%	196797.500000
75%	243211.500000
max	288145.000000
```

Change columns names to Prophet's specs and change the data column to a timeseries object.

```python
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
      <td>1970-01-01</td>
      <td>80173.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1970-02-01</td>
      <td>77442.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1970-03-01</td>
      <td>90223.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1970-04-01</td>
      <td>89956.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1970-05-01</td>
      <td>97972.0</td>
    </tr>
  </tbody>
</table>


