---
title: "Working with Timeseries Data"
date: 2020-09-07
tags: [ML&AI]
excerpt: "Working with timeseries data using python"
mathjax: "True"
---
## Notes on Python/pandas for TimeSeries Data from Datacamp's Manipulating Time Series course

## Comparing Timeseries Growth Rate

*  Timeseries data, stocks for instance, are hard to compare at different levels. They must be normalized so that the price series starts at 100.
   *   This is done by dividing all prices by the first element in the series and multiplying by 100
   *   As a result, the first value = 1 and each subsequent price now reflects the relative change to the initial price. All prices are relative to the starting point
   *   Multiply the normalized series by 100 and now we get the relative change to the initial prince in percentage points. For instance, a price change from 100 to 130 represents a 30 percent point increase.

Let's look at an example. 

```python
# import packages
import pandas as pd
import pandas_datareader.data as web
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

Create a data frame containing the price (Adj Close ) for Kodak ('KODK'), iRobot ('IRBT'), Amazon ('AMZN') and Google ('GOOG') using pandas datareader which imports data from the web.

```python
all_data = {ticker : web.get_data_yahoo(ticker)
            for ticker in ['KODK', 'IRBT', 'AMZN', 'GOOG']}
price = pd.DataFrame({ticker : data['Adj Close']
                      for ticker, data in all_data.items()})

price.head()                      
```

```
	         KODK	   IRBT	     AMZN	     GOOG
Date				
2015-09-14	14.99	29.889999	521.380005	623.239990
2015-09-15	15.41	30.320000	522.369995	635.140015
2015-09-16	15.45	30.270000	527.390015	635.979980
2015-09-17	15.68	31.340000	538.869995	642.900024
2015-09-18	15.58	30.330000	540.260010	629.250000
```

`price.info()`

```
<class 'pandas.core.frame.DataFrame'>
DatetimeIndex: 1257 entries, 2015-09-14 to 2020-09-09
Data columns (total 4 columns):
 #   Column  Non-Null Count  Dtype  
---  ------  --------------  -----  
 0   KODK    1257 non-null   float64
 1   IRBT    1257 non-null   float64
 2   AMZN    1257 non-null   float64
 3   GOOG    1257 non-null   float64
dtypes: float64(4)
memory usage: 49.1 KB
```

```python
# Select the first price for the stocks
price.iloc[0]
```

```
KODK     14.990000
IRBT     29.889999
AMZN    521.380005
GOOG    623.239990
Name: 2015-09-14 00:00:00, dtype: float64
```

This returns a Series containing the first row of the dataframe which can now be used to normalize the data. 

```python
normalized_df = price.div(price.iloc[0])
normalized_df.head()
```

```
	          KODK	      IRBT	      AMZN	      GOOG
Date				
2015-09-14	1.000000	1.000000	1.000000	1.000000
2015-09-15	1.028019	1.014386	1.001899	1.019094
2015-09-16	1.030687	1.012713	1.011527	1.020442
2015-09-17	1.046031	1.048511	1.033546	1.031545
2015-09-18	1.039360	1.014721	1.036212	1.009643
```

We would need a benchmark to compare performance so we can import data from the web for SPDR S&P 500 ETF

```python
bench = {ticker : web.get_data_yahoo(ticker)
         for ticker in ['SPY']}
bench_price = pd.DataFrame({ticker : data['Adj Close']
                      for ticker, data in bench.items()})

bench_price.head()
```

```
	            SPY
Date	
2015-09-14	177.454758
2015-09-15	179.672806
2015-09-16	181.229980
2015-09-17	180.822556
2015-09-18	177.867691
```

