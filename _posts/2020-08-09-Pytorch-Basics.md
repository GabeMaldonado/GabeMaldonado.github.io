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

```
tensor([[10., 10., 10.],
        [10., 10., 10.]])
```

```python
# Add a value to the tensor

new_tensor = initial_tensor.add(5)
new_tensor
```

```
tensor([[15., 15., 15.],
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

```python
# Slice the tensor
random_tensor[1:, 1:]
```

```
tensor([[0.1374, 0.9261],
        [0.2100, 0.1969]])
```

```python
# Get size of tensor

random_tensor.size()
```

`torch.Size([3, 3])`

```python
# View the tensor as a 1-D tensor with 9 elements (3*3)

resized_tensor = random_tensor.view(9)
resized_tensor
```

`tensor([0.1804, 0.6054, 0.6588, 0.4810, 0.1374, 0.9261, 0.1096, 0.2100, 0.1969])`

```python
# note * resized tensor and original tensor have the same memory address so 
# a change to the original tensor would be reflected in the copy tensor

random_tensor[2,2] = 10.0
resized_tensor
```

```
tensor([ 0.1804,  0.6054,  0.6588,  0.4810,  0.1374,  0.9261,  0.1096,  0.2100,
        10.0000])
```

```python
random_tensor
```

```
tensor([[ 0.1804,  0.6054,  0.6588],
        [ 0.4810,  0.1374,  0.9261],
        [ 0.1096,  0.2100, 10.0000]])

```

```python
random_tensor.shape
```

`torch.Size([3, 3])`

```python
# Change shape of a tensor by squeezing and unsqueezing

tensor_unsqueeze = torch.unsqueeze(random_tensor, 2)
tensor_unsqueeze
```

```
tensor([[[ 0.1804],
         [ 0.6054],
         [ 0.6588]],

        [[ 0.4810],
         [ 0.1374],
         [ 0.9261]],

        [[ 0.1096],
         [ 0.2100],
         [10.0000]]])
```

```python
tensor_unsqueeze.shape
```

`torch.Size([3, 3, 1])`

```python
initial_tensor
```

```
tensor([[10., 10., 10.],
        [10., 10., 10.]])
```

```python
# Transpose tensor

tensor_transpose = torch.transpose(initial_tensor, 0, 1)
tensor_transpose
```

```python
# Transpose tensor

tensor_transpose = torch.transpose(initial_tensor, 0, 1)
tensor_transpose
```

```
tensor([[10., 10.],
        [10., 10.],
        [10., 10.]])
```

```python
# Sort values in tensor

sorted_tensor, sorted_indices = torch.sort(random_tensor)
sorted_tensor
```

```
tensor([[ 0.1804,  0.6054,  0.6588],
        [ 0.1374,  0.4810,  0.9261],
        [ 0.1096,  0.2100, 10.0000]])
```

```python
sorted_indices
```

```
tensor([[0, 1, 2],
        [1, 0, 2],
        [0, 1, 2]])
```

```python
# Create a 1-D float tensor 

tensor_float = torch.FloatTensor([-1.1, -2.2, 3.3])
tensor_float
```

`tensor([-1.1000, -2.2000,  3.3000])`

```python
# Get the absolute values of the tensor

tensor_abs = torch.abs(tensor_float)
tensor_abs
```

`tensor([1.1000, 2.2000, 3.3000])`

```python
# Create two tensors with random positivw values

rand1 = torch.abs(torch.rand(2, 3))
rand2 = torch.abs(torch.rand(2, 3))

rand1
```

```
tensor([[0.6688, 0.2732, 0.6260],
        [0.7696, 0.1880, 0.3173]])
```

```python
rand2
```

```
tensor([[0.1969, 0.4801, 0.5976],
        [0.5697, 0.6583, 0.8709]])
```

```
# Add the two tensors

add1 = rand1 + rand2
add1
```

```
tensor([[0.8656, 0.7533, 1.2237],
        [1.3393, 0.8463, 1.1881]])
```

```python
# Create another tensor with + and - values

tensor = torch.Tensor([[-1, -2, -3], [1, 2, 3]])
tensor
```

```
tensor([[-1., -2., -3.],
        [ 1.,  2.,  3.]])
```

```python
# Perform tensor-wise division
tensor_div = torch.div(tensor, tensor + 0.3)
tensor_div
```

```
tensor([[1.4286, 1.1765, 1.1111],
        [0.7692, 0.8696, 0.9091]])
```

```python
# Clamp tensor to certain min and max values

tensor_clamp = torch.clamp(tensor, min=-0.2, max=2)
tensor_clamp
```

```
tensor([[-0.2000, -0.2000, -0.2000],
        [ 1.0000,  2.0000,  2.0000]])
```

```python
# Create two new tensors

t1 = torch.Tensor([1, 2])
t2 = torch.Tensor([10, 20])
```

```python
# Perform matrix multiplication on the two tensors above
# using dot product

dot_product = torch.dot(t1, t2)
dot_product
```

`tensor(50.)`

```python
# Create a matrix and a vector

matrix = torch.Tensor([[1, 2, 3],
                       [4, 5, 6]])

vector = torch.Tensor([0, 1, 2])
```

```python
# In Pytorch we can also multiply a matrix and a vector

matrix_vector = torch.mv(matrix, vector)
matrix_vector
```

`tensor([ 8., 17.])`

```python
# Create another matrix

matrix_2 = torch.Tensor([[10, 30],
                         [20, 0],
                         [0, 50]])

# Perform matrix multiuplication (mm)

matrix_mul = torch.mm(matrix, matrix_2)
matrix_mul                         
```       

```
tensor([[ 50., 180.],
        [140., 420.]])
```

```python
# Get the index of the max value across a particular dimension

torch.argmax(matrix_mul, dim=1)
```

`tensor([1, 1])`

```python
matrix_mul[1,1]
```

`tensor(420.)`

```python
# Get the index of the min value

torch.argmin(matrix_mul, dim=1)
```

`tensor([0, 0])`

```python
matrix_mul[0,0]
```

`tensor(50.)`

## Conversions between Pytorch and Numpy 

```python
import numpy as np

# Create a new tensor with random values

tensor = torch.rand(4, 3)
tensor
```

```
tensor([[0.4104, 0.4827, 0.5824],
        [0.5948, 0.8272, 0.8067],
        [0.2073, 0.0654, 0.7156],
        [0.2299, 0.3968, 0.7596]])
```

```python
# check type

type(tensor)
```

`torch.Tensor`

```python
# Convert tensor to a numpy array

numpy_from_tensor = tensor.numpy()
numpy_from_tensor
```

```
array([[0.4104271 , 0.48272985, 0.58242667],
       [0.59482265, 0.82721066, 0.80672765],
       [0.2073437 , 0.06537104, 0.71558857],
       [0.22989696, 0.3968014 , 0.7596284 ]], dtype=float32)
```

```python
# check type

type(numpy_from_tensor)
```

`numpy.ndarray`

```python
# check if it is a tensor

torch.is_tensor(tensor)
```

`True`

```python
# try same but with the np array

torch.is_tensor(numpy_from_tensor)
```

`False`

**The Pytorch tensor and the numpy array share the same memory address so the changes made to one would be reflected on the other.**

```python
numpy_from_tensor[0, 0] = 100.0

numpy_from_tensor
```

```
array([[1.0000000e+02, 4.8272985e-01, 5.8242667e-01],
       [5.9482265e-01, 8.2721066e-01, 8.0672765e-01],
       [2.0734370e-01, 6.5371037e-02, 7.1558857e-01],
       [2.2989696e-01, 3.9680141e-01, 7.5962842e-01]], dtype=float32)
```

```python
tensor
```

```
tensor([[1.0000e+02, 4.8273e-01, 5.8243e-01],
        [5.9482e-01, 8.2721e-01, 8.0673e-01],
        [2.0734e-01, 6.5371e-02, 7.1559e-01],
        [2.2990e-01, 3.9680e-01, 7.5963e-01]])
```

```python
# Instantiate a numpy array

numpy_arr = np.array([[1.0, 2.0, 3.0],
                      [10.0, 20.0, 30.0,],
                      [100.0, 200.0, 300.0]])
numpy_arr
```

```
array([[  1.,   2.,   3.],
       [ 10.,  20.,  30.],
       [100., 200., 300.]])
```

```python
# Convert the np array to a tensor

tensor_from_np = torch.from_numpy(numpy_arr)
tensor_from_np
```

```
tensor([[  1.,   2.,   3.],
        [ 10.,  20.,  30.],
        [100., 200., 300.]], dtype=torch.float64)
```

```python
# Check type

type(tensor_from_np)
```

`torch.Tensor`

```python
torch.is_tensor(tensor_from_np)
```

`True`

```python
# Change values in the tensor

tensor_from_np[0] = 1
tensor_from_np
```

```
tensor([[  1.,   1.,   1.],
        [ 10.,  20.,  30.],
        [100., 200., 300.]], dtype=torch.float64)
```

```python
numpy_arr
```

```
array([[  1.,   1.,   1.],
       [ 10.,  20.,  30.],
       [100., 200., 300.]])
```

```python
# Create a new np array

numpy_arr_1 = np.array([4, 8])
numpy_arr_1
```

`array([4, 8])`

```python
# Create a copy using '.as_tensor'

tensor_from_array1 = torch.as_tensor(numpy_arr_1)
tensor_from_array1
```

`tensor([4, 8])`

```python
# change values

numpy_arr_1[1] = 5
numpy_arr_1
```

`array([4, 5])`

```python
tensor_from_array1
```

`tensor([4, 5])`

