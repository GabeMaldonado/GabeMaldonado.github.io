---
title: "Numpy Basics"
date: 2020-08-05
tags: [ML&AI]
excerpt: "Numpy Basics"
mathjax: "True"
---


# Numpy Basics

```python
# import packages
import pandas as pd
import numpy as np

# Creating an array linearly-spaced
np.linspace(0,10,20)
```

```
array([ 0.        ,  0.52631579,  1.05263158,  1.57894737,  2.10526316,
        2.63157895,  3.15789474,  3.68421053,  4.21052632,  4.73684211,
        5.26315789,  5.78947368,  6.31578947,  6.84210526,  7.36842105,
        7.89473684,  8.42105263,  8.94736842,  9.47368421, 10.        ])
```

```python
# return an array with ones in the diagonal and zero otherwise
np.eye(5)
```

```
array([[1., 0., 0., 0., 0.],
       [0., 1., 0., 0., 0.],
       [0., 0., 1., 0., 0.],
       [0., 0., 0., 1., 0.],
       [0., 0., 0., 0., 1.]])
```

```python
# create an array of random numbers
np.random.rand(4,4)
```

```
array([[0.23912098, 0.26176023, 0.65033571, 0.26975701],
       [0.31568221, 0.89199535, 0.19985759, 0.15676016],
       [0.47552317, 0.00933197, 0.1337214 , 0.95415866],
       [0.42100403, 0.04881252, 0.96221299, 0.1989001 ]])
```

```python
# random integer from 1 - 100 third parameters defines how many numbers we want returned
np.random.randint(1,100,20)
```

```
array([13, 17, 22, 68,  1,  7, 55, 10, 89, 22, 28, 29, 57,  2, 73, 26, 54,
       16, 32,  9])
```

```python
# setting the seed to generate random numbers
# good for reproducibility
np.random.seed(42)
np.random.rand(4)
```

`array([0.37454012, 0.95071431, 0.73199394, 0.59865848])`

```python
# array attributes and methods
arr = np.arange(25)
arr
```

`array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16,
       17, 18, 19, 20, 21, 22, 23, 24])
`

```python
ranarr = np.random.randint(0, 50, 10)
ranarr
```

`array([38, 18, 22, 10, 10, 23, 35, 39, 23,  2])`

```python
arr.shape
```

`(25,)`

```python
# reshape array
arr.reshape(5,5)
```

```
array([[ 0,  1,  2,  3,  4],
       [ 5,  6,  7,  8,  9],
       [10, 11, 12, 13, 14],
       [15, 16, 17, 18, 19],
       [20, 21, 22, 23, 24]])
```

```python
# return max value
ranarr.max()
39

# return min value
2

# returning the index location
ranarr.argmax()
7

ranarr.argmin()
9


```

```python
# Indexing and selection
arr1 = np.arange(0,11)
arr1
```

`array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10])`

```python
# return the value at index 8
arr1[8]

8

# select form 1:5
arr1[1:5]
array([1, 2, 3, 4])

arr1[:5]
array([0, 1, 2, 3, 4])

arr1[5:]
array([ 5,  6,  7,  8,  9, 10])
```

```python

# Broadcasting -- performing functions and operations across the array
# adding a number to every single number of the array
# changes are not permanent

arr1 + 100
array([100, 101, 102, 103, 104, 105, 106, 107, 108, 109, 110])

# divide every single number of the array
arr1 / 2
array([0. , 0.5, 1. , 1.5, 2. , 2.5, 3. , 3.5, 4. , 4.5, 5. ])

# multiply every single number of the array
arr1 ** 2
array([  0,   1,   4,   9,  16,  25,  36,  49,  64,  81, 100])

# create a new array by slicing the original array
slice_of_array = arr1[0:6]
slice_of_array
array([0, 1, 2, 3, 4, 5])

# update array's values
slice_of_array[:] = 99
slice_of_array
array([99, 99, 99, 99, 99, 99])

# since slice_of_array was created by slicing the array when we broadcast to slice_of_array
# the original array gets affected, too.
arr1
array([99, 99, 99, 99, 99, 99,  6,  7,  8,  9, 10])

# To prevent this we have to explicitly create a copy using 'arr.copy'
arr1_copy = arr1.copy()
arr1_copy[:] = 10000
arr1_copy

array([10000, 10000, 10000, 10000, 10000, 10000, 10000, 10000, 10000,
       10000, 10000])
```

```python
# Indexing on a 2D array
# create a 2D array
arr_2d = np.array([[5, 10, 15],[20, 25, 30],[35, 40, 45]])
arr_2d
```

```
array([[ 5, 10, 15],
       [20, 25, 30],
       [35, 40, 45]])
```

```python
arr_2d.shape
(3, 3)

# Slicing a 2D array, index of row & index of column
# slicing to get row in index 1 [20, 25, 30]
arr_2d[1]
array([20, 25, 30])

# to get an element by row and column
arr_2d[1][1]
25

# or
arr_2d[1,1]
25

# to get the '45'
arr_2d[2, 2]
45

# slicing subsets of the array 10 & 15 from the first row
# and 25, 30 from second row
arr_2d[:2,1:]

array([[10, 15],
       [25, 30]])

# Conditional Selection
# allows us to use conditional operators to grab elements
arr2 = np.arange(1,11)
arr2
array([ 1,  2,  3,  4,  5,  6,  7,  8,  9, 10])

# Return boolean for elements that are greater than 4
arr2  > 4
array([False, False, False, False,  True,  True,  True,  True,  True,
        True])

bool_arr = arr2 > 4
bool_arr
array([False, False, False, False,  True,  True,  True,  True,  True,
        True])

arr2[bool_arr]
array([ 5,  6,  7,  8,  9, 10])

arr2[arr2<=6]
array([1, 2, 3, 4, 5, 6])
```

```python
# Apply square root to all elements of the array
np.sqrt(arr2)
```

```
array([1.        , 1.41421356, 1.73205081, 2.        , 2.23606798,
       2.44948974, 2.64575131, 2.82842712, 3.        , 3.16227766])
```

```python
# apply the log
np.log(arr2)
```

```
array([0.        , 0.69314718, 1.09861229, 1.38629436, 1.60943791,
       1.79175947, 1.94591015, 2.07944154, 2.19722458, 2.30258509])
```

```python
# getting the sum of the array
arr2.sum()
55

# get mean of the array
# mean
arr2.mean()
5.5
```




