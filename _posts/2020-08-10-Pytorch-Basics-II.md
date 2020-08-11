---
title: "Pytorch Basics II"
date: 2020-08-10
tags: [ML&AI]
excerpt: "Pytorch Basics II"
mathjax: "True"
---
## Pytorch Basics II

### Working with Gradients

**Weights** and **biases** of individual neurons are determined during the training process. 

Regression-- the simplest neural network. It tries to best-fit a line that passes through the data. 
  *   `y = Wx + b`
  *   Minimize the sum of squares of the distance of the points from the regression line.

The actual training of a neural network happens via Gradient Descent Optimization. 

MSE = Mean Square Error of Loss. A metric to be minimized during training of regression model. 

Loss = `ypredicted` - `yactual`

Where `ypredicted` is, given x, model outputs predicted value of y and `yactual` is the actual label, available in the training data. 

There are three ways to calculate gradients: 

1.   Symbolic Differentiation -- Conceptually simple but hard to implement

2.   Numeric Differentiation -- Easy to implement but won't scale

3.   Automatic Differentiation -- Conceptually difficult but easy to implement. 

Pytorch and Tensorflow rely on automatic differentiation. 

In Pytorch, the package used to calculate gradients for bacpropagation is **Autograd**

- Optimizer uses the error function and tweaks the model parameters to minimize error. 

- Backward pass: updates parameter values. 

- Backpropagation is implemented using a technique called reverse auto-differentiation. 

- Gradient -- vector of partial derivatives -- these gradients apply to specific time t. 

- Parameters (t+1) = Parameters (t) - learning_rate X Gradient(t)

- For next time step: update parameter values. Move each parameter value in the direction of reducing gradient.

- **Learning rate** is the size of the step  in the direction of the reducing gradient. If we want to take small steps to converge to what's the min value of loss, keep the LR small and vice versa. Keep in mind that using a small LR the model would take long to train and converge to the lowest loss value. 

## Automatic Differentiation

Reverse-mode auto-differentiation

- Used in Pytorch and TF

- Two passes in each training step

   -   Forward step: Calculate loss
   -   Backward step: Update parameter values

Automatic Differentiation:

-   Relies on a mathematical trick

-   Based on Taylor's Series Expansion

-   Allows fast approximation of gradients

-   It can be performed in two modes: Reverse and Forward mode
   
    - Forward-mode is similar to numeric differentiation. It requires one pass per parameter and will not scale to complex networks. 


### Implementing Autograd in Pytorch

```python
# Create two 2X3 tensors

tensor_1 = torch.Tensor([[1, 2, 3],
                         [4, 5, 6]])

tensor_1
```

```
tensor([[1., 2., 3.],
        [4., 5., 6.]])
```

```python
tensor_2 = torch.Tensor([[7, 8, 9],
                         [10, 11, 12]])
tensor_2
```

```
tensor([[ 7.,  8.,  9.],
        [10., 11., 12.]])
```

```python
# Every tensor created in Pytorch has the ```requires_grad``` property

tensor_1.requires_grad
```

``False`

When `requires_grad` = True, it tracks computations for a tensor in the forward phase and will calculate gradients for this tensor in the backward phase.
The default value is False

```python
tensor_2.requires_grad
```

`False`

```python
# To enable tracking on the tensor:

tensor_1.requires_grad_()
```

```
tensor([[1., 2., 3.],
        [4., 5., 6.]], requires_grad=True)
```

```python
# Check property again

tensor_1.requires_grad
```

`True`

Gradients calculated using Automatic Differentiation with respect to any tensor is present in the graph matric associated with that tensor. 

```python
print(tensor_1.grad)
```

`None`

It returned None because no gradients have been calculated. This is still part of a computation graph but no forward or backward passes have been made yet. 
We have created a tensor but haven't used it to perform any calculations. 

The computation graph in Pytorch is made up of tensors and functions, where tensors can be the nodes and functions are the transformations performed along the edges. 
Every tensor has a function that is used to create that function:

```python
print(tensor_1.grad_fn)
```

`None`

```python
# Set up a graph by performing a calculation on the tensors

output_tensor = tensor_1 * tensor_2
```

The output tensor will inherit the `requires_graph` property that was given to tensor_1. 

```python
print(output_tensor.requires_grad)
```

`True`

```python
print(output_tensor.grad)
```

`None`

Still no gradients as we haven't made any backwards pass yet. 
But it will have a grad function because we used an specific multiplication operation (see `MulBackward0` below) to create this output tensor. User-created tensors have no corresponding function. 

```python
print(output_tensor.grad_fn)
```

`<MulBackward0 object at 0x7f53399177b8>`

```python

# Create another output tensor with a different operation

output_tensor_1 = (tensor_1 * tensor_2).mean()
print(output_tensor_1.grad_fn)
```
`<MeanBackward0 object at 0x7f5339917588>`

Notice that the function displayed now is `MeanBackward0` even though we also used a multiplication function to create this output tensor. The `grad_fn` references the loss function used to create this tensor, in this case the **mean**.

```python
print(tensor_1.grad)
```

`None`

Although we used `tensor_1` for several operations, it still does not have gradients. This is because we have't perform a backward pass used to calculate gradients. Gradient calculation (a vector of partial derivatives) will only be calculated when we pass the `backward` function to an output. 

```python
output_tensor_1.backward()
print(tensor_1.grad)
```

```
tensor([[1.1667, 1.3333, 1.5000],
        [1.6667, 1.8333, 2.0000]])

```

Since the gradients are the partial derivatives for the parameters in tensor_1 its shape will exactly match the shape of the tensor:

```python
tensor_1.grad.shape, tensor_1.shape
```

`(torch.Size([2, 3]), torch.Size([2, 3]))`

A tensor will inherit its properties to the output tensor, as seen above, if we do not want Pytorch to track the history of the tensors we can use `torch.no_grad`

```python
with torch.no_grad():

  new_tensor = tensor_1 * 3
  print('new_tensor = ', new_tensor)

  print('requires_grad for tensor = ', tensor_1.requires_grad)

  print('requires_grad for tensor = ', tensor_2.requires_grad)

  print('requires_grad for tensor = ', new_tensor.requires_grad)
  ```

  ```
  new_tensor =  tensor([[ 3.,  6.,  9.],
        [12., 15., 18.]])
requires_grad for tensor =  True
requires_grad for tensor =  False
requires_grad for tensor =  False
```

Here we can see that the `new_tensor` did not inherit the properties of  `tensor_1` even though it was used to create the output tensor because it was created inside the `torch.no_grad` code block. 

```python
# Create a function that multiplies any number by 2

def calculate(t):
  return t * 2


# Create same function but add the no_grad decorator

@torch.no_grad()
def calculate_no_grad(t):
  return t * 2
```
Both functions perform the same operation but for the second function, gradients will no be enabled, history tracking will not be turn-on even if the tensor has its grad property set to True.

```python
# Let's test the 1st function passing tensor_1

result_tensor = calculate(tensor_1)

result_tensor
```

```
tensor([[ 2.,  4.,  6.],
        [ 8., 10., 12.]], grad_fn=<MulBackward0>)
```

```python
# Test 2nd function

result_tensor_no_grad = calculate_no_grad(tensor_1)

result_tensor_no_grad
```

```
tensor([[ 2.,  4.,  6.],
        [ 8., 10., 12.]])
```

```python
result_tensor_no_grad.requires_grad
```

`False`

History tracking can be explicitly enabled even if the code is executed inside a `torch.no_grad()` code block. 

```python
with torch.no_grad():

  new_tensor_no_grad = tensor_1 * 3
  print('new_tensor_no_grad = ', new_tensor_no_grad)

  # Explicitly enable grad
  with torch.enable_grad():
    new_tensor_grad = tensor_1 * 3
    print('new_tensor_grad = ', new_tensor_grad)
```

```
new_tensor_no_grad =  tensor([[ 3.,  6.,  9.],
        [12., 15., 18.]])
new_tensor_grad =  tensor([[ 3.,  6.,  9.],
        [12., 15., 18.]], grad_fn=<MulBackward0>)
```

Also, the value for `requires_grad` can be defined when creating a new tensor:

```python
tensor_1_1 = torch.tensor([[1.0, 2.0],
                           [3.0, 4.0]], requires_grad=True)

tensor_1_1
```

```
tensor([[1., 2.],
        [3., 4.]], requires_grad=True)
```

If I create a new tensor `tensor_1_2`  by default-- the `requires_grad` parameter will be set to False.

```python
tensor_1_2 = torch.tensor([[3.0, 4.0 ], 
                           [5, 6]])

tensor_1_2
```

```
tensor([[3., 4.],
        [5., 6.]])
```

```python
# Update tensor_1_2 to True

tensor_1_2.requires_grad_()
```

```
tensor([[3., 4.],
        [5., 6.]], requires_grad=True)
```

```python
# Perform a simple calculation that'd perform the forward pass

final_tensor = (tensor_1_1 + tensor_1_2).mean()

final_tensor
```

`tensor(7., grad_fn=<MeanBackward0>)`

```python
# Check ```requires_grad``` property for the final tensor

final_tensor.requires_grad
```

`True`

There are no gradients for the two input tensors as we only perform the forward pass on the computation graph

```python
print(tensor_1_1.grad)
```

`None`

```python
print(tensor_1_2.grad)
```

`None`

Since we have history tracking enabled for these two input tensors in this computation, we can call `.backward()` to calculate the gradients. 

```python
final_tensor.backward()
print(tensor_1_1.grad)
```

```
tensor([[0.2500, 0.2500],
        [0.2500, 0.2500]])
```

```python
print(tensor_1_2)
```

```
tensor([[3., 4.],
        [5., 6.]], requires_grad=True)
```

Tensors involved in a computation are part of a larger computational graph. If we want to retreive a tensor that is detached of the current computation we can call `.detach()`. This detach tensor will always have `requires_grad=False`

```python
detached_tensor = tensor_1_1.detach()
detached_tensor
```

```
tensor([[1., 2.],
        [3., 4.]])
```

```python
tensor_1_1
```

```
tensor([[1., 2.],
        [3., 4.]], requires_grad=True)
```

```python
# Use the detach and the original tensor in a computation

mean_tensor = (tensor_1_1 + detached_tensor).mean()

mean_tensor.backward()

tensor_1_1.grad
```

```
tensor([[0.5000, 0.5000],
        [0.5000, 0.5000]])
```        

```python
print(detached_tensor.grad)
```

`None`

## Autograd with Variables

Variables are no longer needed to work with autograd and to store gradients, those parameters are now part of the tensor itself. 
However the **Variable** API still exists in Pytorch and can be used by:

```python
from torch.autograd import Variable

# Instantiate a variable

var = Variable(torch.FloatTensor([9]))
var
```

`tensor([9.])`

All the attributes of a tensor we saw above, are the same for the variable that holds the tensor.

```python
# Update the requires_grad property

var.requires_grad_()
```

`tensor([9.], requires_grad=True)`

```python
w1 = Variable(torch.FloatTensor([3]), requires_grad=True)
w2 = Variable(torch.FloatTensor([7]), requires_grad=True)

w1
```

`tensor([3.], requires_grad=True)`

```python
w2
```

`tensor([7.], requires_grad=True)`

```python
result_var = var * w1
result_var
```

`tensor([27.], grad_fn=<MulBackward0>)`

```python
result_var.backward()
w1.grad
```
`tensor([9.])`

```python
print(w2.grad)
```

`None`

```python
var.grad
```

`tensor([3.])`





