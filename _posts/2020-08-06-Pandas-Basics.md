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

```python
# create a new series
ser1 = pd.Series([1, 2, 3, 4], index=['USA', 'Germany', 'USSR', 'Japan']) 
ser1

USA        1
Germany    2
USSR       3
Japan      4
dtype: int64

# return location index
ser1['USA']

1

ser2 = pd.Series([1, 4, 5, 6], index=['USA', 'Germany', 'Italy', 'Japan'])
ser2

USA        1
Germany    4
Italy      5
Japan      6
dtype: int64

# adding the series
ser1 + ser2

Germany     6.0
Italy       NaN
Japan      10.0
USA         2.0
USSR        NaN
dtype: float64
```

```python

# Dataframes
from numpy.random import randn
np.random.seed(101)

rand_matrix = randn(5,4)
rand_matrix

array([[ 2.70684984,  0.62813271,  0.90796945,  0.50382575],
       [ 0.65111795, -0.31931804, -0.84807698,  0.60596535],
       [-2.01816824,  0.74012206,  0.52881349, -0.58900053],
       [ 0.18869531, -0.75887206, -0.93323722,  0.95505651],
       [ 0.19079432,  1.97875732,  2.60596728,  0.68350889]])

# create the dataframe
df = pd.DataFrame(data=rand_matrix, index='A B C D E'.split(), columns=('W X Y Z').split())
df
```

<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>2.706850</td>
      <td>0.628133</td>
      <td>0.907969</td>
      <td>0.503826</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>-0.319318</td>
      <td>-0.848077</td>
      <td>0.605965</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-2.018168</td>
      <td>0.740122</td>
      <td>0.528813</td>
      <td>-0.589001</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.188695</td>
      <td>-0.758872</td>
      <td>-0.933237</td>
      <td>0.955057</td>
    </tr>
    <tr>
      <th>E</th>
      <td>0.190794</td>
      <td>1.978757</td>
      <td>2.605967</td>
      <td>0.683509</td>
    </tr>
  </tbody>
</table>

```python
# slicing dataframes -- column
df['W']

A    2.706850
B    0.651118
C   -2.018168
D    0.188695
E    0.190794
Name: W, dtype: float64

ind_list = ['W', 'X']
df[ind_list]
```

<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>W</th>
      <th>X</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>2.706850</td>
      <td>0.628133</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>-0.319318</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-2.018168</td>
      <td>0.740122</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.188695</td>
      <td>-0.758872</td>
    </tr>
    <tr>
      <th>E</th>
      <td>0.190794</td>
      <td>1.978757</td>
    </tr>
  </tbody>
</table>

```python
# or 
df[['W', 'X']]
```

<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>W</th>
      <th>X</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>2.706850</td>
      <td>0.628133</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>-0.319318</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-2.018168</td>
      <td>0.740122</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.188695</td>
      <td>-0.758872</td>
    </tr>
    <tr>
      <th>E</th>
      <td>0.190794</td>
      <td>1.978757</td>
    </tr>
  </tbody>
</table>

```python
# creating a new column on the df by summing two columns
df['NEW'] = df['W'] + df['X']
df
```

<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
      <th>NEW</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>2.706850</td>
      <td>0.628133</td>
      <td>0.907969</td>
      <td>0.503826</td>
      <td>3.334983</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>-0.319318</td>
      <td>-0.848077</td>
      <td>0.605965</td>
      <td>0.331800</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-2.018168</td>
      <td>0.740122</td>
      <td>0.528813</td>
      <td>-0.589001</td>
      <td>-1.278046</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.188695</td>
      <td>-0.758872</td>
      <td>-0.933237</td>
      <td>0.955057</td>
      <td>-0.570177</td>
    </tr>
    <tr>
      <th>E</th>
      <td>0.190794</td>
      <td>1.978757</td>
      <td>2.605967</td>
      <td>0.683509</td>
      <td>2.169552</td>
    </tr>
  </tbody>
</table>

```python
# to delete a column- use .drop(axis=1) axis=0 is for rows
df.drop('NEW', axis=1)
```

<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>2.706850</td>
      <td>0.628133</td>
      <td>0.907969</td>
      <td>0.503826</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>-0.319318</td>
      <td>-0.848077</td>
      <td>0.605965</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-2.018168</td>
      <td>0.740122</td>
      <td>0.528813</td>
      <td>-0.589001</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.188695</td>
      <td>-0.758872</td>
      <td>-0.933237</td>
      <td>0.955057</td>
    </tr>
    <tr>
      <th>E</th>
      <td>0.190794</td>
      <td>1.978757</td>
      <td>2.605967</td>
      <td>0.683509</td>
    </tr>
  </tbody>
</table>

```python
df
```

<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
      <th>NEW</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>2.706850</td>
      <td>0.628133</td>
      <td>0.907969</td>
      <td>0.503826</td>
      <td>3.334983</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>-0.319318</td>
      <td>-0.848077</td>
      <td>0.605965</td>
      <td>0.331800</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-2.018168</td>
      <td>0.740122</td>
      <td>0.528813</td>
      <td>-0.589001</td>
      <td>-1.278046</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.188695</td>
      <td>-0.758872</td>
      <td>-0.933237</td>
      <td>0.955057</td>
      <td>-0.570177</td>
    </tr>
    <tr>
      <th>E</th>
      <td>0.190794</td>
      <td>1.978757</td>
      <td>2.605967</td>
      <td>0.683509</td>
      <td>2.169552</td>
    </tr>
  </tbody>
</table>

```python
# the drop was not in-place as we can see 'NEW' is still there
# to delete permanently
df.drop('NEW', axis=1, inplace=True)
df
```

<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>2.706850</td>
      <td>0.628133</td>
      <td>0.907969</td>
      <td>0.503826</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>-0.319318</td>
      <td>-0.848077</td>
      <td>0.605965</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-2.018168</td>
      <td>0.740122</td>
      <td>0.528813</td>
      <td>-0.589001</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.188695</td>
      <td>-0.758872</td>
      <td>-0.933237</td>
      <td>0.955057</td>
    </tr>
    <tr>
      <th>E</th>
      <td>0.190794</td>
      <td>1.978757</td>
      <td>2.605967</td>
      <td>0.683509</td>
    </tr>
  </tbody>
</table>

```python
# to drop rows simple use drop
df.drop('A')
df
```
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>-0.319318</td>
      <td>-0.848077</td>
      <td>0.605965</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-2.018168</td>
      <td>0.740122</td>
      <td>0.528813</td>
      <td>-0.589001</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.188695</td>
      <td>-0.758872</td>
      <td>-0.933237</td>
      <td>0.955057</td>
    </tr>
    <tr>
      <th>E</th>
      <td>0.190794</td>
      <td>1.978757</td>
      <td>2.605967</td>
      <td>0.683509</td>
    </tr>
  </tbody>
</table>

```python

# select rows
# we can use .loc
df.loc['A']

W    2.706850
X    0.628133
Y    0.907969
Z    0.503826
Name: A, dtype: float64

# or we can use index/integer location iloc
df.iloc[0]

W    2.706850
X    0.628133
Y    0.907969
Z    0.503826
Name: A, dtype: float64

# selecting multiple rows
df.loc[['A','B']]
```

<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>2.706850</td>
      <td>0.628133</td>
      <td>0.907969</td>
      <td>0.503826</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>-0.319318</td>
      <td>-0.848077</td>
      <td>0.605965</td>
    </tr>
  </tbody>
</table>

`df.iloc[0:2]`

<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>2.706850</td>
      <td>0.628133</td>
      <td>0.907969</td>
      <td>0.503826</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>-0.319318</td>
      <td>-0.848077</td>
      <td>0.605965</td>
    </tr>
  </tbody>
</table>

```python
# to grab particular data points, lets say row AV and columns YZ
df.loc[['A','B']][['Y','Z']]
```

<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>0.907969</td>
      <td>0.503826</td>
    </tr>
    <tr>
      <th>B</th>
      <td>-0.848077</td>
      <td>0.605965</td>
    </tr>
  </tbody>
</table>

```python
# or
df.loc[['A','B'],['Y','Z']]
```

<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>0.907969</td>
      <td>0.503826</td>
    </tr>
    <tr>
      <th>B</th>
      <td>-0.848077</td>
      <td>0.605965</td>
    </tr>
  </tbody>
</table>

```python
# conditional selection
df > 0
```

<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>B</th>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>C</th>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>D</th>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>E</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
  </tbody>
</table>

```python
# pass the df_bool to original df to get the results of the condition
df[df_bool]
```

<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>2.706850</td>
      <td>0.628133</td>
      <td>0.907969</td>
      <td>0.503826</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.605965</td>
    </tr>
    <tr>
      <th>C</th>
      <td>NaN</td>
      <td>0.740122</td>
      <td>0.528813</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.188695</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.955057</td>
    </tr>
    <tr>
      <th>E</th>
      <td>0.190794</td>
      <td>1.978757</td>
      <td>2.605967</td>
      <td>0.683509</td>
    </tr>
  </tbody>
</table>

```python
# or 
df[df > 0]
```

<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>2.706850</td>
      <td>0.628133</td>
      <td>0.907969</td>
      <td>0.503826</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.605965</td>
    </tr>
    <tr>
      <th>C</th>
      <td>NaN</td>
      <td>0.740122</td>
      <td>0.528813</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.188695</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.955057</td>
    </tr>
    <tr>
      <th>E</th>
      <td>0.190794</td>
      <td>1.978757</td>
      <td>2.605967</td>
      <td>0.683509</td>
    </tr>
  </tbody>
</table>

```python
# to return the rows in a column with values greater than 0.5
df[df['W']>0.5]
```
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>2.706850</td>
      <td>0.628133</td>
      <td>0.907969</td>
      <td>0.503826</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>-0.319318</td>
      <td>-0.848077</td>
      <td>0.605965</td>
    </tr>
  </tbody>
</table>

```python
# lets get it from column 'Y'
df[df['W']> 0.5]['Y']

A    0.907969
B   -0.848077
Name: Y, dtype: float64
```

```python
#multiple conditions
df[(df['W'] > 0) & (df['Y'] > 1)]
```

<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>E</th>
      <td>0.190794</td>
      <td>1.978757</td>
      <td>2.605967</td>
      <td>0.683509</td>
    </tr>
  </tbody>
</table>















