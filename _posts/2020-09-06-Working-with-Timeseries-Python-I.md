---
title: "Wprking with Timeseries Data -- Python"
date: 2020-09-04
tags: [ML&AI]
excerpt: "Working with timeseries data using python"
mathjax: "True"
---

## Python/pandas for TimeSeries Data

### Date & time series functionality

*   At the core -- data types for date & time information
    *   Objects for points in time periods
    *   Attributes & methods reflect time-related details

*   Sequences of Dates & Periods  
    *   Series or DataFrame columns
    *   Index: converts entire dataframe into TimeSeries

*   Many series/dataframes methods rely on time information in the index to provide time-series functionality

The basic building block is pandas `Timestamp`:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from datetime import datetime

# create a timestamp manually
time_stamp = pd.Timestamp(datetime(2020, 1, 1))

time_stamp
```

```python
# we can also use a date string instead of a datetime object 
# to create the timestamp
pd.Timestamp('2020-01-01')
```

`Timestamp('2020-01-01 00:00:00')`

`pd.Timestamp` has different attributes so we can access different elements of the timestamp. For instance:

```python
# to get the year
time_stamp.year
```

`2020`

```python
# to get the week day
time_stamp.day_name()
```

`Wednesday`

We can also access more attributes for `pd.Timestamp` such as:
`.second`, `.minute`, `.hour`
`.day`, `.month`, `.quarter`, `.year`
`.weekday`, `.dayofweek`, `.weekofyear`, `.dayofyear`

### Period & Frequency

The period object has `freq` attribute to store frequency info:

```python
period = pd.Period('2020-01')
period
```

`Period('2020-01', 'M')`

```python
# change requency to daily 'D'
period.asfreq('D')
```
`Period('2020-01-31', 'D')`

```python
# we can do simply math with periods
period + 2
```

`Period('2020-03', 'M')`

There are other frequencies that we can use besides month 'M' and day 'D'

Hour   `H`

Day    `D`

Week   `W`

Month  `M`

Quarter `Q`

Year  `A`

Business Day `B`


```python
# create a sequence of timestamps
# 12 monthly timestamps

index = pd.date_range(start='2019-01-01', periods=12, freq='M')
index
```

```
DatetimeIndex(['2019-01-31', '2019-02-28', '2019-03-31', '2019-04-30',
               '2019-05-31', '2019-06-30', '2019-07-31', '2019-08-31',
               '2019-09-30', '2019-10-31', '2019-11-30', '2019-12-31'],
              dtype='datetime64[ns]', freq='M')
```              

`DatetimeIndex` is a sequence of Timestamp objects with frequency info. 
We can convert a `DatatimeIndex` to a `Periodindex`

```python
index[0]
```

`Timestamp('2019-01-31 00:00:00', freq='M')`

```python
index.to_period()
```

```
PeriodIndex(['2019-01', '2019-02', '2019-03', '2019-04', '2019-05', '2019-06',
             '2019-07', '2019-08', '2019-09', '2019-10', '2019-11', '2019-12'],
            dtype='period[M]', freq='M')
```

Now that we have an `DatetimeIndex` we can use it to create a time-series dataframe. 

```python
data = np.random.random(size=(12,2))

df = pd.DataFrame(data=data, index=index)

df.head(10)
```

```

                   0	1
2019-01-31	0.685220	0.456167
2019-02-28	0.809490	0.905552
2019-03-31	0.454890	0.683387
2019-04-30	0.860495	0.341041
2019-05-31	0.156462	0.030216
2019-06-30	0.885845	0.085404
2019-07-31	0.995309	0.719039
2019-08-31	0.417888	0.032380
2019-09-30	0.167757	0.773513
2019-10-31	0.631097	0.583592
```