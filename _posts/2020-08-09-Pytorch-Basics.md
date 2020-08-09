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

```python
# chage default d-type

torch.set_default_dtype(torch.float32)
torch.get_default_dtype()
```

`torch.float32`

```python
# Create a Pytorch Tensor

tensor_array = torch.Tensor([[1, 2, 3], [4, 5, 6]])
tensor_array
```

```
tensor([[1., 2., 3.],
        [4., 5., 6.]])
```

```python
torch.is_tensor(tensor_array)
```

`True`

```python
# Check the number of elements in the tensor
# numel would print the number of elements regarding of the tensor's shape
 
torch.numel(tensor_array)
```
`6`

```python
tensor_uninitialized = torch.Tensor(2,2)
tensor_uninitialized
```

```
tensor([[3.5377e-35, 0.0000e+00],
        [8.4078e-45, 0.0000e+00]])
```

The two lines of code above show that when we run `torch.Tensor(2, 2)` we create a 2X2 tensor that has no initial values. Pytorch creates the tensor and allocates memory for future values that will be passed to the tensor. The numbers we see are memory addresses. 
However, if we run `torch.rand(2, 2)` we are creating a 2X2 tensor that it is initialized with random values:

```python
tensor_initialized = torch.rand(2, 2)
```
`tensor([[0.5521, 0.3260],
        [0.2627, 0.0585]])
`

```python
# Create a tensor of a particular type (int)

tensor_init = torch.Tensor([5, 3]).type(torch.IntTensor)
tensor_init
```
`tensor([5, 3], dtype=torch.int32)`

```python
# Create a tensor of int16 d-type

tensor_short = torch.ShortTensor([1, 2, 3])
tensor_short
```
`tensor([1, 2, 3], dtype=torch.int16)`

```python
# Create a tensor of half float d-type

tensor_float = torch.tensor([1, 2, 3]).type(torch.half)
tensor_float
```
`tensor([1., 2., 3.], dtype=torch.float16)`




