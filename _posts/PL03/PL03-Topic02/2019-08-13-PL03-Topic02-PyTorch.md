---
layout : post
title : PL03-Topic02, PyTorch
categories: [PL03-Topic02]
comments : true
tags : [PL03-Topic02]
---
[Back to the previous page](https://userdyk-github.github.io/pl03/PL03-Libraries.html) ｜<a href="https://github.com/userdyk-github/userdyk-github.github.io/blob/master/_posts/PL03/PL03-Topic02/2019-08-13-PL03-Topic02-PyTorch.md" target="_blank">page management</a> <br>
List of posts to read before reading this article
- <a href='https://userdyk-github.github.io/'>post1</a>
- <a href='https://userdyk-github.github.io/'>post2</a>
- <a href='https://userdyk-github.github.io/'>post3</a>

---

## Contents
{:.no_toc}

* ToC
{:toc}

<hr class="division1">

## **Installation**
<a href="https://pytorch.org/get-started/locally/" target="_blank">URL</a>
<a href="https://anaconda.org/pytorch/pytorch">anaconda torch url</a>
<a href="https://anaconda.org/pytorch/torchvision">anaconda torchvision url</a>

### ***For linux***
```bash
$ 
```
<br><br><br>

### ***For windows***
```dos

```
<br><br><br>

### ***Version Control***
```python

```
<br><br><br>


<hr class="division2">

## **Tutorials**
### ***Dataset : loader***

<br><br><br>

---

### ***Neural net : Custom layers***
#### Sequential
<a href="https://pytorch.org/docs/stable/nn.html#sequential" targe="_blank">URL</a>

<br><br><br>
#### Module 
<a href="https://pytorch.org/docs/stable/nn.html#module" targe="_blank">URL</a>
```python
import torch.nn as nn
import torch.nn.functional as F

class Model(nn.Module):
    def __init__(self):
        super(Model, self).__init__()
        self.conv1 = nn.Conv2d(1, 20, 5)
        self.conv2 = nn.Conv2d(20, 20, 5)

    def forward(self, x):
        x = F.relu(self.conv1(x))
        return F.relu(self.conv2(x))

model = Model()

"""
for i,j in enumerate(model.modules()):
    print(i,j)
"""

for i,j in enumerate(model.modules()):
    if i==1:
        print(j.weight, j.bias)
```
- [manually set weight](https://discuss.pytorch.org/t/how-to-manually-set-the-weights-in-a-two-layer-linear-model/45902)

<br><br><br>

---

### ***Optimization : Training***

<br><br><br>

---

### ***Evaluation : Predicting***

<br><br><br>
<hr class="division2">


## **Tensor & Tensor operations**

### ***Using Tensors : autograd***
<a href="https://pytorch.org/docs/stable/tensors.html" target="_blank">torch.tensor api</a><br>

#### tensor as data type
```python
import torch

x = [12,23,34,45,56,67,78]
print(torch.is_tensor(x))
print(torch.is_storage(x))
```
```
False
False
```
<br><br><br>
```python
import torch

x = torch.tensor([1])
print(torch.is_tensor(x))
print(torch.is_storage(x))
```
```
True
False
```
<br><br><br>
```python
import torch

x = torch.randn(1,2,3,4,5)
print(torch.is_tensor(x))
print(torch.is_storage(x))
print(torch.numel(x))         #number of elements
```
```
True
False
120
```
<br><br><br>
```python
import numpy as np
import torch

x = [12,23,34,45,56,67]
y = np.array(x)
z = torch.from_numpy(y)

print(x)
print(y)
print(z)
```
```
[12, 23, 34, 45, 56, 67]
[12 23 34 45 56 67]
tensor([12, 23, 34, 45, 56, 67], dtype=torch.int32)
```
<details markdown="1">
<summary class='jb-small' style="color:blue">to numpy</summary>
<hr class='division3'>
```python
import torch

x = torch.tensor([1])
print(x.numpy())
```
```
[1]
```
<hr class='division3'>
</details>
<br><br><br>

#### creating tensor
<br><br><br>
```python
import torch

x = torch.eye(3,3)
print(x)
```
```
tensor([[1., 0., 0.],
        [0., 1., 0.],
        [0., 0., 1.]])
```
<br><br><br>

```python
import torch

x = torch.zeros(4,5)
y = torch.zeros(10)

print(x)
print(y)
```
```
tensor([[0., 0., 0., 0., 0.],
        [0., 0., 0., 0., 0.],
        [0., 0., 0., 0., 0.],
        [0., 0., 0., 0., 0.]])
tensor([0., 0., 0., 0., 0., 0., 0., 0., 0., 0.])
```
<br><br><br>


```python
import torch

x = torch.linspace(2,10,25)
y = torch.logspace(2,10,25)

print(x)
print(y)
```
```
tensor([ 2.0000,  2.3333,  2.6667,  3.0000,  3.3333,  3.6667,  4.0000,  4.3333,
         4.6667,  5.0000,  5.3333,  5.6667,  6.0000,  6.3333,  6.6667,  7.0000,
         7.3333,  7.6667,  8.0000,  8.3333,  8.6667,  9.0000,  9.3333,  9.6667,
        10.0000])
tensor([1.0000e+02, 2.1544e+02, 4.6416e+02, 1.0000e+03, 2.1544e+03, 4.6416e+03,
        1.0000e+04, 2.1544e+04, 4.6416e+04, 1.0000e+05, 2.1544e+05, 4.6416e+05,
        1.0000e+06, 2.1544e+06, 4.6416e+06, 1.0000e+07, 2.1544e+07, 4.6416e+07,
        1.0000e+08, 2.1544e+08, 4.6416e+08, 1.0000e+09, 2.1544e+09, 4.6416e+09,
        1.0000e+10])
```
<br><br><br>
```python
import torch

x = torch.rand(10)        # random numbers 10 from a uniform distribution between 0 and 1
y = torch.rand(4,5)       # random numbers 20 = 4*5 from a uniform distribution between 0 and 1
z = torch.randn(10)       # random numbers 10 from a normal distribution (0,1)
```
```
tensor([0.0329, 0.8617, 0.1021, 0.3931, 0.8998, 0.8649, 0.1870, 0.9334, 0.5804,
        0.9534])
tensor([[0.1078, 0.4410, 0.2292, 0.3280, 0.2127],
        [0.0472, 0.0099, 0.0181, 0.4200, 0.0257],
        [0.6366, 0.9422, 0.1212, 0.1833, 0.1107],
        [0.3173, 0.8371, 0.5419, 0.5221, 0.0068]])
tensor([ 0.2746, -0.8012,  0.7291, -1.0866,  1.3591,  0.3519,  1.3433,  0.1243,
         0.0065,  0.1567])
```
<br><br><br>

```python
import torch

x = torch.randperm(10)      # random permutation
y = torch.arange(10,40,2)   # step size = 2
z = torch.arange(10,40)     # step size = 1
```
```
tensor([8, 6, 0, 4, 9, 7, 5, 3, 1, 2])
tensor([10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38])
tensor([10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27,
        28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39])
```
<br><br><br>

#### indexing & slicing
```python
import torch

x = torch.randn(4,5)


print(x)
print(torch.argmin(x))
print(torch.argmin(x, dim=1))

print(torch.argmax(x))
print(torch.argmax(x, dim=1))
```
```
tensor([[-0.6006,  0.5420, -0.7122,  0.8044,  0.5344],
        [ 0.1702, -0.2696, -0.3626,  0.5435,  0.9020],
        [ 0.5961, -0.7445, -0.3796, -0.6009,  1.2564],
        [ 0.7729, -1.9188, -0.3456,  0.3841, -0.0653]])
tensor(16)
tensor([2, 2, 1, 1])
tensor(14)
tensor([3, 4, 4, 0])
```
<br><br><br>
<a href="http://www.programmersought.com/article/81801261179/;jsessionid=848520548A8855A35D2F4B97F617EE2B" target="_blank">URL</a>
```python
import torch

b = torch.Tensor([[1,2,3],[4,5,6]])
print(b)

index_1 = torch.LongTensor([[0,1],[2,0]])
index_2 = torch.LongTensor([[0,1,1],[0,0,0]])
print(torch.gather(b, dim=1, index=index_1))   # 'dim = 1' means axis-column
print(torch.gather(b, dim=0, index=index_2))   # 'dim = 0' means axis-row
```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
```
tensor([[1., 2., 3.],
        [4., 5., 6.]])
tensor([[1., 2.],
        [6., 4.]])
tensor([[1., 5., 6.],
        [1., 2., 3.]])
```
<hr class='division3'>
</details>
<br>
```python
import torch

a = torch.randn(4,4)
indices = torch.LongTensor([0,2])

result1 = torch.index_select(a, 0, indices)
result2 = torch.index_select(a, 1, indices)
print("a",a)
print("dim=0(row[0:2]) \n", result1)
print("dim=1(column[0:2]) \n", result2)
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
```
a tensor([[-0.9946,  0.9729, -0.9979, -1.1015],
        [-0.7123,  0.1369, -0.3352,  1.5771],
        [ 1.2470,  0.5784, -0.1455,  1.5894],
        [ 0.4785, -0.3342,  0.2051, -0.5731]])
dim=0(row[0:2])
 tensor([[-0.9946,  0.9729, -0.9979, -1.1015],
        [ 1.2470,  0.5784, -0.1455,  1.5894]])
dim=1(column[0:2])
 tensor([[-0.9946, -0.9979],
        [-0.7123, -0.3352],
        [ 1.2470, -0.1455],
        [ 0.4785,  0.2051]])
```
<hr class='division3'>
</details>
<br>
```python
import torch

a = torch.tensor([10, 0, 2, 0, 0])
non_zero = torch.nonzero(a)
print(non_zero)
```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
```
tensor([[0],
        [2]])
```
<hr class='division3'>
</details>
<br><br><br>

#### reshaping and resizeing
```python
import torch

x = torch.randn(1,4)
p = torch.cat((x,x))
q = torch.cat((x,x),0)
r = torch.cat((x,x,x), 1)


print(x)
print(p)
print(q)
print(r)
```
```
tensor([[ 0.2394, -2.9119,  0.1089,  0.6426]])
tensor([[ 0.2394, -2.9119,  0.1089,  0.6426],
        [ 0.2394, -2.9119,  0.1089,  0.6426]])
tensor([[ 0.2394, -2.9119,  0.1089,  0.6426],
        [ 0.2394, -2.9119,  0.1089,  0.6426]])
tensor([[ 0.2394, -2.9119,  0.1089,  0.6426,  0.2394, -2.9119,  0.1089,  0.6426,
          0.2394, -2.9119,  0.1089,  0.6426]])
```
<br><br><br>
```python
import torch

x = torch.randn(4,4)
p = torch.chunk(x, 2)
q = torch.chunk(x,2,0)
r = torch.chunk(x,2,1)

print(x)
print(p)
print(q)
print(r)
```
```
tensor([[-0.7438, -0.2451,  0.2383,  0.0779],
        [-1.3219, -0.2667,  0.1635,  1.2190],
        [ 1.0349,  0.6819,  0.9239,  0.8569],
        [-2.8974, -0.5763, -0.2475, -0.8700]])
(tensor([[-0.7438, -0.2451,  0.2383,  0.0779],
        [-1.3219, -0.2667,  0.1635,  1.2190]]), tensor([[ 1.0349,  0.6819,  0.9239,  0.8569],
        [-2.8974, -0.5763, -0.2475, -0.8700]]))
(tensor([[-0.7438, -0.2451,  0.2383,  0.0779],
        [-1.3219, -0.2667,  0.1635,  1.2190]]), tensor([[ 1.0349,  0.6819,  0.9239,  0.8569],
        [-2.8974, -0.5763, -0.2475, -0.8700]]))
(tensor([[-0.7438, -0.2451],
        [-1.3219, -0.2667],
        [ 1.0349,  0.6819],
        [-2.8974, -0.5763]]), tensor([[ 0.2383,  0.0779],
        [ 0.1635,  1.2190],
        [ 0.9239,  0.8569],
        [-0.2475, -0.8700]]))
```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

```python
import torch

a = torch.tensor([11, 12, 13, 14, 15, 16, 17, 18, 19, 20])
split_2 = torch.split(a,2)
split_3 = torch.split(a,3)
print(split_2)
print(split_3)
```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
```
(tensor([11, 12]), tensor([13, 14]), tensor([15, 16]), tensor([17, 18]), tensor([19, 20]))
(tensor([11, 12, 13]), tensor([14, 15, 16]), tensor([17, 18, 19]), tensor([20]))
```
<hr class='division3'>
</details>
<br><br><br>


```python
import torch

a = torch.tensor([[-0.9946,  0.9729, -0.9979, -1.1015],
                  [-0.7123,  0.1369, -0.3352,  1.5771],
                  [ 1.2470,  0.5784, -0.1455,  1.5894],
                  [ 0.4785, -0.3342,  0.2051, -0.5731]])

print(a)
print(a.t())
print(a.transpose(1,0))
```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
```
tensor([[-0.9946,  0.9729, -0.9979, -1.1015],
        [-0.7123,  0.1369, -0.3352,  1.5771],
        [ 1.2470,  0.5784, -0.1455,  1.5894],
        [ 0.4785, -0.3342,  0.2051, -0.5731]])
tensor([[-0.9946, -0.7123,  1.2470,  0.4785],
        [ 0.9729,  0.1369,  0.5784, -0.3342],
        [-0.9979, -0.3352, -0.1455,  0.2051],
        [-1.1015,  1.5771,  1.5894, -0.5731]])
tensor([[-0.9946, -0.7123,  1.2470,  0.4785],
        [ 0.9729,  0.1369,  0.5784, -0.3342],
        [-0.9979, -0.3352, -0.1455,  0.2051],
        [-1.1015,  1.5771,  1.5894, -0.5731]])
```
<hr class='division3'>
</details>
<br><br><br>
```python
import torch

a = torch.tensor([[-0.9946,  0.9729, -0.9979, -1.1015],
                  [-0.7123,  0.1369, -0.3352,  1.5771],
                  [ 1.2470,  0.5784, -0.1455,  1.5894],
                  [ 0.4785, -0.3342,  0.2051, -0.5731]])

print(a)
print(torch.unbind(a,1))    # dim = 1 removing a column
print(torch.unbind(a))      # dim = 0 removing a row
```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
```
tensor([[-0.9946,  0.9729, -0.9979, -1.1015],
        [-0.7123,  0.1369, -0.3352,  1.5771],
        [ 1.2470,  0.5784, -0.1455,  1.5894],
        [ 0.4785, -0.3342,  0.2051, -0.5731]])
(tensor([-0.9946, -0.7123,  1.2470,  0.4785]), tensor([ 0.9729,  0.1369,  0.5784, -0.3342]), tensor([-0.9979, -0.3352, -0.1455,  0.2051]), tensor([-1.1015,  1.5771,  1.5894, -0.5731]))
(tensor([-0.9946,  0.9729, -0.9979, -1.1015]), tensor([-0.7123,  0.1369, -0.3352,  1.5771]), tensor([ 1.2470,  0.5784, -0.1455,  1.5894]), tensor([ 0.4785, -0.3342,  0.2051, -0.5731]))
```
<hr class='division3'>
</details>

<br><br><br>

#### mathematical functions
```python
import torch

a = torch.tensor([[-0.9946,  0.9729, -0.9979, -1.1015],
                  [-0.7123,  0.1369, -0.3352,  1.5771],
                  [ 1.2470,  0.5784, -0.1455,  1.5894],
                  [ 0.4785, -0.3342,  0.2051, -0.5731]])

print("a\n", a)
print("add\n", torch.add(a,100))
print("mul\n", torch.mul(a,100))
print("ceil\n", torch.ceil(a))
print("floor\n", torch.floor(a))
print("clamp\n", torch.clamp(a, min=-0.8, max=0.8))
print("exp\n", torch.exp(a))
print("frac\n", torch.frac(a))
print("log\n", torch.log(a))
print("pow\n", torch.pow(a,2))
print("sigmoid\n", torch.sigmoid(a))
print("sqrt\n", torch.sqrt(a))
```
```
a
 tensor([[-0.9946,  0.9729, -0.9979, -1.1015],
        [-0.7123,  0.1369, -0.3352,  1.5771],
        [ 1.2470,  0.5784, -0.1455,  1.5894],
        [ 0.4785, -0.3342,  0.2051, -0.5731]])
add
 tensor([[ 99.0054, 100.9729,  99.0021,  98.8985],
        [ 99.2877, 100.1369,  99.6648, 101.5771],
        [101.2470, 100.5784,  99.8545, 101.5894],
        [100.4785,  99.6658, 100.2051,  99.4269]])
mul
 tensor([[ -99.4600,   97.2900,  -99.7900, -110.1500],
        [ -71.2300,   13.6900,  -33.5200,  157.7100],
        [ 124.7000,   57.8400,  -14.5500,  158.9400],
        [  47.8500,  -33.4200,   20.5100,  -57.3100]])
ceil
 tensor([[-0.,  1., -0., -1.],
        [-0.,  1., -0.,  2.],
        [ 2.,  1., -0.,  2.],
        [ 1., -0.,  1., -0.]])
floor
 tensor([[-1.,  0., -1., -2.],
        [-1.,  0., -1.,  1.],
        [ 1.,  0., -1.,  1.],
        [ 0., -1.,  0., -1.]])
clamp
 tensor([[-0.8000,  0.8000, -0.8000, -0.8000],
        [-0.7123,  0.1369, -0.3352,  0.8000],
        [ 0.8000,  0.5784, -0.1455,  0.8000],
        [ 0.4785, -0.3342,  0.2051, -0.5731]])
exp
 tensor([[0.3699, 2.6456, 0.3687, 0.3324],
        [0.4905, 1.1467, 0.7152, 4.8409],
        [3.4799, 1.7832, 0.8646, 4.9008],
        [1.6137, 0.7159, 1.2276, 0.5638]])
frac
 tensor([[-0.9946,  0.9729, -0.9979, -0.1015],
        [-0.7123,  0.1369, -0.3352,  0.5771],
        [ 0.2470,  0.5784, -0.1455,  0.5894],
        [ 0.4785, -0.3342,  0.2051, -0.5731]])
log
 tensor([[    nan, -0.0275,     nan,     nan],
        [    nan, -1.9885,     nan,  0.4556],
        [ 0.2207, -0.5475,     nan,  0.4634],
        [-0.7371,     nan, -1.5843,     nan]])
pow
 tensor([[0.9892, 0.9465, 0.9958, 1.2133],
        [0.5074, 0.0187, 0.1124, 2.4872],
        [1.5550, 0.3345, 0.0212, 2.5262],
        [0.2290, 0.1117, 0.0421, 0.3284]])
sigmoid
 tensor([[0.2700, 0.7257, 0.2694, 0.2495],
        [0.3291, 0.5342, 0.4170, 0.8288],
        [0.7768, 0.6407, 0.4637, 0.8305],
        [0.6174, 0.4172, 0.5511, 0.3605]])
sqrt
 tensor([[   nan, 0.9864,    nan,    nan],
        [   nan, 0.3700,    nan, 1.2558],
        [1.1167, 0.7605,    nan, 1.2607],
        [0.6917,    nan, 0.4529,    nan]])
```
<br><br><br>

#### gradient 
<a href="https://towardsdatascience.com/pytorch-autograd-understanding-the-heart-of-pytorchs-magic-2686cd94ec95" target="_blank">URL</a>,
<a href="https://stackoverflow.com/questions/43451125/pytorch-what-are-the-gradient-arguments" target="_blank">URL</a>

```python
import torch

x = torch.tensor([1.])
print(x.requires_grad)
```
```
False
```
```python
import torch

x = torch.tensor([1.])
x.requires_grad_(True)
print(x.requires_grad)
```

<br><br><br>
```python
import torch

x = torch.tensor([1], dtype=torch.float, requires_grad=True)
print(x.requires_grad)

print(x.detach().requires_grad)  # not in-place
print(x.requires_grad)

print(x.detach_().requires_grad) # in-place
print(x.requires_grad)
```
```
True

False
True

False
False
```




<br><br><br>

```python
import torch

# Creating the graph
x = torch.tensor(1.0, requires_grad = True)
y = torch.tensor(2.0)
z = x * y

# Displaying
for i, name in zip([x, y, z], "xyz"):
    print(f"{name}\n\
    data: {i.data}\n\
    requires_grad: {i.requires_grad}\n\
    grad: {i.grad}\n\
    grad_fn: {i.grad_fn}\n\
    is_leaf: {i.is_leaf}\n")
```
```
x
    data: 1.0
    requires_grad: True
    grad: None
    grad_fn: None
    is_leaf: True

y
    data: 2.0
    requires_grad: False
    grad: None
    grad_fn: None
    is_leaf: True

z
    data: 2.0
    requires_grad: True
    grad: None
    grad_fn: <MulBackward0 object at 0x7fcae8e33748>
    is_leaf: False
```
<br><br><br>
```python
import torch

# Creating the graph
x = torch.tensor(1.0, requires_grad = True); print(x.requires_grad) # True
y = x * 2;                                   print(y.requires_grad) # True

# Check if tracking is enabled
with torch.no_grad():      
    y = x * 2
    print(y.requires_grad) #False
```
```
True
True
False
```
<br><br><br>
```python
import torch

# Creating the graph
x = torch.tensor(1.0, requires_grad = True)
z = x ** 3

#Computes the gradient
z.backward();       print(x.grad.data) #Prints '3' which is dz/dx 
```
```
tensor(3.)
```

<br><br><br>


---


### ***GPU control : cuda***
```python
import torch
 
#  Returns a bool indicating if CUDA is currently available.
torch.cuda.is_available()
#  True
 
#  Returns the index of a currently selected device.
torch.cuda.current_device()
#  0
 
#  Returns the number of GPUs available.
torch.cuda.device_count()
#  1
 
#  Gets the name of a device.
torch.cuda.get_device_name(0)
#  'GeForce GTX 1060'
 
#  Context-manager that changes the selected device.
#  device (torch.device or int) – device index to select. 
torch.cuda.device(0)
```
```python
import torch
 
# Default CUDA device
cuda = torch.device('cuda')
 
# allocates a tensor on default GPU
a = torch.tensor([1., 2.], device=cuda)
 
# transfers a tensor from 'C'PU to 'G'PU
b = torch.tensor([1., 2.]).cuda()
 
# Same with .cuda()
b2 = torch.tensor([1., 2.]).to(device=cuda)
```
<br><br><br>
<hr class="division2">

## **Probability Distributions**

### ***Sampling Tensors***

```python
import torch

torch.manual_seed(1234)
a = torch.randn(4,4)
print(a)
```
```
tensor([[-0.1117, -0.4966,  0.1631, -0.8817],
        [ 0.0539,  0.6684, -0.0597, -0.4675],
        [-0.2153,  0.8840, -0.7584, -0.3689],
        [-0.3424, -1.4020,  0.3206, -1.0219]])
```
<br><br><br>

#### uniform
```python
import torch

torch.manual_seed(1234)
a = torch.Tensor(4,4)
print(a.uniform_(0,1))
```
```
tensor([[0.0290, 0.4019, 0.2598, 0.3666],
        [0.0583, 0.7006, 0.0518, 0.4681],
        [0.6738, 0.3315, 0.7837, 0.5631],
        [0.7749, 0.8208, 0.2793, 0.6817]])
```
<br><br><br>

#### bernoulli
```python
import torch

torch.manual_seed(1234)
a = torch.Tensor(4,4)
b = torch.bernoulli(a.uniform_(0,1))

print(b)
```
```
tensor([[0., 0., 1., 0.],
        [0., 1., 0., 0.],
        [0., 0., 1., 1.],
        [0., 1., 0., 1.]])
```
<br><br><br>

#### multinomial
```python
import torch

a = torch.Tensor([10,10,13,10,34,45,65,67,87,89,87,34])
b1 = torch.multinomial(a,3)
b2 = torch.multinomial(a,5, replacement=True)

print(b1, b2)
```
```
tensor([1, 6, 7]) tensor([7, 9, 9, 4, 8])
```
<br><br><br>

#### normal
```python
import torch

a1 = torch.normal(mean = torch.arange(1., 11.)
                  ,std = torch.arange(1, 0, -0.1))
a2 = torch.normal(mean = 0.5,
                  std = torch.arange(1., 6.))
a3 = torch.normal(mean = 0.5,
                  std = torch.arange(0.2, 0.6))

print(a1)
print(a2)
print(a3)
```
```
tensor([-0.1867,  1.0083,  2.6983,  3.6359,  5.4243,  5.0426,  7.3969,  8.1270,
         9.1576,  9.8825])
tensor([0.4635, 3.9725, 0.6453, 3.5979, 5.8550])
tensor([0.7702])
```
<br><br><br>

---


### ***Variable Tensors***

```python
from torch.autograd import Variable
import torch

a = torch.ones(2,2)

print(Variable(a))
print(Variable(a ,requires_grad=True))
```
```
tensor([[1., 1.],
        [1., 1.]])
tensor([[1., 1.],
        [1., 1.]], requires_grad=True)
```

<br><br><br>

```python

```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Basic Statistics***
#### mean
```python
import torch

torch.manual_seed(1234)
x = torch.randn(4,6)

print(x)
print(torch.mean(x))
print(torch.mean(x, dim=0))
print(torch.mean(x, dim=1))
```
```
tensor([[-0.1117, -0.4966,  0.1631, -0.8817,  0.0539,  0.6684],
        [-0.0597, -0.4675,  0.6369, -0.7141, -1.0831, -0.5547],
        [ 0.9717, -0.5150,  1.4255,  0.7987, -2.5273,  1.4778],
        [-0.1696, -0.9919, -1.4569,  0.2563, -0.4030,  0.4195]])
        
tensor(-0.1484)
tensor([ 0.1577, -0.6177,  0.1922, -0.1352, -0.9899,  0.5027])
tensor([-0.1008, -0.3737,  0.2719, -0.3909])
```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

#### median
```python
import torch

torch.manual_seed(1234)
x = torch.randn(4,6)

print(x)
print(torch.median(x))
print(torch.median(x, dim=0))
print(torch.median(x, dim=1))
```
```
tensor([[-0.1117, -0.4966,  0.1631, -0.8817,  0.0539,  0.6684],
        [-0.0597, -0.4675,  0.6369, -0.7141, -1.0831, -0.5547],
        [ 0.9717, -0.5150,  1.4255,  0.7987, -2.5273,  1.4778],
        [-0.1696, -0.9919, -1.4569,  0.2563, -0.4030,  0.4195]])
        
tensor(-0.1696)
torch.return_types.median(
values=tensor([-0.1117, -0.5150,  0.1631, -0.7141, -1.0831,  0.4195]),
indices=tensor([0, 2, 0, 1, 1, 3]))
torch.return_types.median(
values=tensor([-0.1117, -0.5547,  0.7987, -0.4030]),
indices=tensor([0, 5, 3, 4]))
```
<br><br><br>

#### mode
```python
import torch

torch.manual_seed(1234)
x = torch.randn(4,6)

print(x)
print(torch.mode(x))
print(torch.mode(x, dim=0))
print(torch.mode(x, dim=1))
```
```
tensor([[-0.1117, -0.4966,  0.1631, -0.8817,  0.0539,  0.6684],
        [-0.0597, -0.4675,  0.6369, -0.7141, -1.0831, -0.5547],
        [ 0.9717, -0.5150,  1.4255,  0.7987, -2.5273,  1.4778],
        [-0.1696, -0.9919, -1.4569,  0.2563, -0.4030,  0.4195]])
        
torch.return_types.mode(
values=tensor([-0.8817, -1.0831, -2.5273, -1.4569]),
indices=tensor([3, 4, 4, 2]))
torch.return_types.mode(
values=tensor([-0.1696, -0.9919, -1.4569, -0.8817, -2.5273, -0.5547]),
indices=tensor([3, 3, 3, 0, 2, 1]))
torch.return_types.mode(
values=tensor([-0.8817, -1.0831, -2.5273, -1.4569]),
indices=tensor([3, 4, 4, 2]))
```
<br><br><br>

#### standard deviation
```python
import torch

torch.manual_seed(1234)
x = torch.randn(4,6)

print(x)
print(torch.std(x))
print(torch.std(x, dim=0))
print(torch.std(x, dim=1))
```
```
tensor([[-0.1117, -0.4966,  0.1631, -0.8817,  0.0539,  0.6684],
        [-0.0597, -0.4675,  0.6369, -0.7141, -1.0831, -0.5547],
        [ 0.9717, -0.5150,  1.4255,  0.7987, -2.5273,  1.4778],
        [-0.1696, -0.9919, -1.4569,  0.2563, -0.4030,  0.4195]])
tensor(0.9230)
tensor([0.5445, 0.2502, 1.2165, 0.7995, 1.1264, 0.8373])
tensor([0.5388, 0.5968, 1.5497, 0.7242])
```
<br><br><br>

#### variance
```python
import torch

torch.manual_seed(1234)
x = torch.randn(4,6)

print(x)
print(torch.var(x))
print(torch.var(x, dim=0))
print(torch.var(x, dim=1))
```
```
tensor([[-0.1117, -0.4966,  0.1631, -0.8817,  0.0539,  0.6684],
        [-0.0597, -0.4675,  0.6369, -0.7141, -1.0831, -0.5547],
        [ 0.9717, -0.5150,  1.4255,  0.7987, -2.5273,  1.4778],
        [-0.1696, -0.9919, -1.4569,  0.2563, -0.4030,  0.4195]])
tensor(0.8519)
tensor([0.2965, 0.0626, 1.4798, 0.6393, 1.2688, 0.7011])
tensor([0.2903, 0.3561, 2.4014, 0.5245])
```
<br><br><br>

---


### ***Gradient Computation***

```python
import torch

def forward(x):
    return x*w

def loss(x,y):
    y_pred = forward(x)
    return (y_pred - y)*(y_pred - y)

x_data = [11., 22., 33.]
y_data = [21., 14., 64.]

w = torch.tensor([1.], requires_grad=True)

# training loop
for epoch in range(10):
    for x_val, y_val in zip(x_data, y_data):
        l = loss(x_val, y_val)
        l.backward();                         print("weight_grad : ", x_val,y_val,w.grad.data[0])
        w.data = w.data - 0.001*w.grad.data;  w.grad.data.zero_(); print("progess : ", epoch, l.data[0])
```
```
weight_grad :  11.0 21.0 tensor(-220.)
progess :  0 tensor(100.)
weight_grad :  22.0 14.0 tensor(564.9600)
progess :  0 tensor(164.8656)
weight_grad :  33.0 64.0 tensor(-2797.3230)
progess :  0 tensor(1796.3765)
weight_grad :  11.0 21.0 tensor(373.4719)
progess :  1 tensor(288.1844)
weight_grad :  22.0 14.0 tensor(2364.3669)
progess :  1 tensor(2887.5159)
weight_grad :  33.0 64.0 tensor(-2667.7661)
progess :  1 tensor(1633.8330)
weight_grad :  11.0 21.0 tensor(356.5143)
progess :  2 tensor(262.6084)
weight_grad :  22.0 14.0 tensor(2312.9514)
progess :  2 tensor(2763.2976)
weight_grad :  33.0 64.0 tensor(-2671.4675)
progess :  2 tensor(1638.3698)
weight_grad :  11.0 21.0 tensor(356.9987)
progess :  3 tensor(263.3225)
weight_grad :  22.0 14.0 tensor(2314.4204)
progess :  3 tensor(2766.8088)
weight_grad :  33.0 64.0 tensor(-2671.3621)
progess :  3 tensor(1638.2404)
weight_grad :  11.0 21.0 tensor(356.9850)
progess :  4 tensor(263.3022)
weight_grad :  22.0 14.0 tensor(2314.3782)
progess :  4 tensor(2766.7078)
weight_grad :  33.0 64.0 tensor(-2671.3647)
progess :  4 tensor(1638.2438)
weight_grad :  11.0 21.0 tensor(356.9853)
progess :  5 tensor(263.3027)
weight_grad :  22.0 14.0 tensor(2314.3794)
progess :  5 tensor(2766.7109)
weight_grad :  33.0 64.0 tensor(-2671.3647)
progess :  5 tensor(1638.2438)
weight_grad :  11.0 21.0 tensor(356.9853)
progess :  6 tensor(263.3027)
weight_grad :  22.0 14.0 tensor(2314.3794)
progess :  6 tensor(2766.7109)
weight_grad :  33.0 64.0 tensor(-2671.3647)
progess :  6 tensor(1638.2438)
weight_grad :  11.0 21.0 tensor(356.9853)
progess :  7 tensor(263.3027)
weight_grad :  22.0 14.0 tensor(2314.3794)
progess :  7 tensor(2766.7109)
weight_grad :  33.0 64.0 tensor(-2671.3647)
progess :  7 tensor(1638.2438)
weight_grad :  11.0 21.0 tensor(356.9853)
progess :  8 tensor(263.3027)
weight_grad :  22.0 14.0 tensor(2314.3794)
progess :  8 tensor(2766.7109)
weight_grad :  33.0 64.0 tensor(-2671.3647)
progess :  8 tensor(1638.2438)
weight_grad :  11.0 21.0 tensor(356.9853)
progess :  9 tensor(263.3027)
weight_grad :  22.0 14.0 tensor(2314.3794)
progess :  9 tensor(2766.7109)
weight_grad :  33.0 64.0 tensor(-2671.3647)
progess :  9 tensor(1638.2438)
```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Tensor Operations***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Distributions***
<a href="https://pytorch.org/docs/stable/distributions.html" target="_blank">URL</a>
```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>


<hr class="division2">

## **CNN and RNN**

### ***Setting Up a Loss Function***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Estimating the Derivative of the Loss Function***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Fine-Tuning a Model***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Selecting an Optimization Function***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Further Optimizing the Function***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Implementing a Convolutional Neural Network (CNN)***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Reloading a Model***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Implementing a Recurrent Neural Network (RNN)***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Implementing a RNN for Regression Problems***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Using PyTorch Built-in Functions***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Working with Autoencoders***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Fine-Tuning Results Using Autoencoder***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Visualizing the Encoded Data in a 3D Plot***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Restricting Model Overfitting***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Visualizing the Model Overfit***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Initializing Weights in the Dropout Rate***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Adding Math Operations***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Embedding Layers in RNN***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


<hr class="division2">

## **Neural Networks**

### ***Working with Activation Functions***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Visualizing the Shape of Activation Functions***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Basic Neural Network Model***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Tensor Differentiation***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


<hr class="division2">

## **Supervised Learning**

### ***Data Preparation for the Supervised Model***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Forward and Backward Propagation***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Optimization and Gradient Computation***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Viewing Predictions***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Supervised Model Logistic Regression***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


<hr class="division2">

## **Fine-Tuning Deep Learning Models**

### ***Building Sequential Neural Networks***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Deciding the Batch Size***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Deciding the Learning Rate***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***Performing Parallel Training***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


<hr class="division2">

## **Natural Language Processing**

### ***Word Embedding***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***CBOW Model in PyTorch***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

---


### ***LSTM Model***

```python
```

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
<br><br><br>

<hr class='diviision2'>

## **Example**
### ***XOR problem***
```python

```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>

<hr class='division3'>
</details>
<br><br><br>

---



### ***Simple linear regression***
```python

```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>

<hr class='division3'>
</details>
<br><br><br>

---

### ***Multi-variate linear regression***
```python

```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>

<hr class='division3'>
</details>
<br><br><br>

---

### ***Logistic regression : binary class***
```python

```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>

<hr class='division3'>
</details>
<br><br><br>

---

### ***Softmax regression : multi-class***
```python

```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>

<hr class='division3'>
</details>
<br><br><br>

---


### ***Neural network***
```python

```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>

<hr class='division3'>
</details>
<br><br><br>

---

### ***Convolutional neural network : Digit Recognition***
```python

```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>

<hr class='division3'>
</details>
<br><br><br>

---

### ***Recurrent neural network : Next-Word Prediction***
```python

```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>

<hr class='division3'>
</details>
<br><br><br>




<hr class="division1">

List of posts followed by this article
- [post1](https://userdyk-github.github.io/)
- <a href='https://userdyk-github.github.io/'>post2</a>
- <a href='https://userdyk-github.github.io/'>post3</a>

---

Reference
- Pradeepta Mishra, PyTorch Recipes, 2019
- <a href='https://wikidocs.net/book/2788' target="_blank">wikidocs, pytorch</a>
- <a href="https://github.com/deeplearningzerotoall/PyTorch" target="_blank">github : zerotoall, pytorch</a>
- <a href='https://www.youtube.com/watch?v=7eldOrjQVi0&list=PLQ28Nx3M4JrhkqBVIXg-i5_CVVoS1UzAv' target="_blank">lecture : zerotoall, pytorch</a>
- <a href="https://github.com/yunjey/pytorch-tutorial" target="_blank">github : yunjey tutorials</a>
- <a href="https://pytorch.org/tutorials/" target="_blank">pytorch official tutorials</a>
- <a href="http://www.gisdeveloper.co.kr/?p=8392">PyTorch의 Tensor 연산 퀵 레퍼런스</a>
- <a href="https://nn.readthedocs.io/en/rtd/index.html">nn readthedocs</a>
- <a href="https://teamdable.github.io/techblog/PyTorch-Autograd" target="_blank">techblog autograd</a>
- <a href="https://teamdable.github.io/techblog/PyTorch-Module" target="_blank">techblog module</a>

- [https://github.com/pytorch](https://github.com/pytorch)
- [https://github.com/pytorch/tutorials](https://github.com/pytorch/tutorials)
- [https://github.com/pytorch/vision](https://github.com/pytorch/vision)
- [https://github.com/pytorch/examples](https://github.com/pytorch/examples)
- [https://github.com/yunjey/pytorch-tutorial](https://github.com/yunjey/pytorch-tutorial)
- [https://github.com/GunhoChoi/PyTorch-FastCampus](https://github.com/GunhoChoi/PyTorch-FastCampus)

---




