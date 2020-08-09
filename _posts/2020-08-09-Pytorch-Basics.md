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

```python
# Create a tensor and fill it with a default value

tensor_fill = torch.full((2, 4), fill_value=10)
tensor_fill
```

```
tensor([[10., 10., 10., 10.],
        [10., 10., 10., 10.]])
```

```python
# Create a tensor filled with ones

tensor_of_ones = torch.ones([2, 4], dtype=torch.int32)
tensor_of_ones
```
```
tensor([[1, 1, 1, 1],
        [1, 1, 1, 1]], dtype=torch.int32)
```

```python
# Create a tensor of zeros by passing the already created tensor of ones

tensor_of_zeros = torch.zeros_like(tensor_of_ones)
tensor_of_zeros
```

```
tensor([[0, 0, 0, 0],
        [0, 0, 0, 0]], dtype=torch.int32)
```      

```python
# Create a 2-D matrix filled with ones diagonally

tensor_eye = torch.eye(5)
tensor_eye
```

```
tensor([[1., 0., 0., 0., 0.],
        [0., 1., 0., 0., 0.],
        [0., 0., 1., 0., 0.],
        [0., 0., 0., 1., 0.],
        [0., 0., 0., 0., 1.]])
```

```python
# Get the indices of the non-zero values on the tensor above

non_zero = torch.nonzero(tensor_eye)
non_zero
```

```
tensor([[0, 0],
        [1, 1],
        [2, 2],
        [3, 3],
        [4, 4]])
```

## Operations on Tensors

```python
# Create a 2X3 tensor with random values

initial_tensor = torch.rand(2, 3)
initial_tensor
```

```
tensor([[0.8851, 0.7137, 0.2390],
        [0.0549, 0.0529, 0.1606]])
```

```python
# Perform an inplace fill (_) operation

initial_tensor.fill_(10)
initial_tensor
```

```tensor([[10., 10., 10.],
        [10., 10., 10.]])
```

```python
# Add a value to the tensor

new_tensor = initial_tensor.add(5)
new_tensor
```

```tensor([[15., 15., 15.],
        [15., 15., 15.]])
```

```python
# Perform a inplace square root on the new tensor

new_tensor.sqrt_()
new_tensor
```

```
tensor([[3.8730, 3.8730, 3.8730],
        [3.8730, 3.8730, 3.8730]])
```

```python
# Create a torch containing evenly spaced numbers from 1 - 12

x = torch.linspace(start=0.1, end=10.0, steps=15)
x
```

```
tensor([ 0.1000,  0.8071,  1.5143,  2.2214,  2.9286,  3.6357,  4.3429,  5.0500,
         5.7571,  6.4643,  7.1714,  7.8786,  8.5857,  9.2929, 10.0000])
```

```python
x.size()
```

`torch.Size([15])`

```python
# Chunk x into 3 separate parts

tensor_chunk = torch.chunk(x, 3, 0)
tensor_chunk
```

```
(tensor([0.1000, 0.8071, 1.5143, 2.2214, 2.9286]),
 tensor([3.6357, 4.3429, 5.0500, 5.7571, 6.4643]),
 tensor([ 7.1714,  7.8786,  8.5857,  9.2929, 10.0000]))
 ```

 ```python
 # Concatenate tensors

tensor1 = tensor_chunk[0]
tensor2 = tensor_chunk[1]
tensor3 = torch.tensor([3.0, 4.0, 5.0])

torch.cat((tensor1, tensor2, tensor3), 0)
```

```
tensor([0.1000, 0.8071, 1.5143, 2.2214, 2.9286, 3.6357, 4.3429, 5.0500, 5.7571,
        6.4643, 3.0000, 4.0000, 5.0000])
```

```python
# Create a 3X3 tensor with radon numbers

random_tensor = torch.rand(3,3)
random_tensor
```

```
tensor([[0.1804, 0.6054, 0.6588],
        [0.4810, 0.1374, 0.9261],
        [0.1096, 0.2100, 0.1969]])
```

```python
# Get values from the tensor by index

random_tensor[0, 1]
```

`tensor(0.6054)`

