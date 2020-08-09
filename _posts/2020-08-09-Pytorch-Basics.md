---
title: "Pytorch Basics"
date: 2020-08-09
tags: [ML&AI]
excerpt: "Pytorch Basics"
mathjax: "True"
---

# Notes on Pytorch Foundations

## Tensor
 Tensor is the central unit of data in Pytorch. It consists of a set of values shaped into an **n-dimensional**  array. Every tensor has a number of dimensions and the number of elements in each dimension gives us the shape of the tensor. 

 *   **Scalar** is a 0-Dimensional tensor (0-D)
 *   **Vector** is a 1-D tensor, e.g. [2, 4, 6, 8, 10]
 *   **Matrix** is a 2-D tensor, e.g. [ [1, 3, 5], [2, 4, 6] ]  
 *   **N-Dimensional** matrices are N-D tensor, e.g. [ [ [1 ,2], [3, 4], [5, 6], [ [7, 8], [9, 10], [11, 12] ] ]

 Pytorch Tensors are similar to numpy arrays but they have been architectured to make optimal use of GPUs for massive parallel computations.

```python
 # Install pytorch

!pip3 install torch torchvision

import torch

# Check pytorch version
print(torch.__version__)
```

`1.4.0`

```python
# check default pytorch datatype

torch.get_default_dtype()
```

`torch.float32`

We can see that the default d-type is `float32` however, we can change the default to other datatypes as long as they are floating-points. Pytorch will not accept int as the default d-type.

[Check docs for more info](https://pytorch.org/docs/stable/tensors.html)


