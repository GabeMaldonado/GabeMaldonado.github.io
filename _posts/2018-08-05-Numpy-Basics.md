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

