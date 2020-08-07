---
title: "Pandas Basics"
date: 2020-08-06
tags: [ML&AI]
excerpt: "Pandas Basics"
mathjax: "True"
---

```python
import pandas as pd
import numpy as np

# create a list of labels
labels = ['a', 'b', 'c']

# create a list of numbers
mylist = [10, 20, 30]

# convert list to an np array
arr = np.array(mylist)
arr

array([10, 20, 30])

# create a dictionary using the lists
d = {'a':10, 'b':20, 'c':30}
d

{'a': 10, 'b': 20, 'c': 30}

# create a pandas series
pd.Series(data=mylist)

a    10
b    20
c    30
dtype: int64

# note the datatype when array is non-numeric
pd.Series(data=['a','b','c'])

0    a
1    b
2    c
dtype: object
```

