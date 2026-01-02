---
title: pytorch、numpy中的shape和size
date: 2020-03-18 22:04:54
tags:
  - pytorch编程
  - Code
cover: https://user-images.githubusercontent.com/60562661/76972030-01266f00-6969-11ea-9264-3760a01d3860.jpg
---

每次在获得图片尺寸时我都会写错，因此来记录一下shape、size。

## Pytorch

`.size() `是方法(function),可以传参数，例如：

```python
 c = torch.randn(2,3)
# c
#tensor([[ 1.4753, -0.5479, -0.4448],
#        [ 0.1452,  0.9948,  0.1481]])
c.size(0)
#2
c.size(1)
#3
c.size[0]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'builtin_function_or_method' object is not subscriptable
c.size[1]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'builtin_function_or_method' object is not subscriptable
```

`.shape则是属性`

```python
c.shape
# torch.Size([2, 3])
c.shape(0)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'torch.Size' object is not callable
c.shape[0]
# 2
c.shape[1]
# 3
type(c.shape)
<class 'torch.Size'>
```

故如果是torch的张量，在需要调用图像尺寸时，应该写：

```python
c.size(0)
c.size(1)
#或者
c.shape[0]
c.shape[1]
```



## Numpy

numpy中，`.size()`是属性，用来输出元素个数 

```python
a = np.array([2,3])
a
#array([2, 3])
a.size
#2
a.size()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'int' object is not callable
>>> a.size(0)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'int' object is not callable
```

`.shape`也是属性

```python
a.shape(0)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object is not callable
>>> a.shape
(2,)
>>> a.shape[0]
2
>>> a.shape[1]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: tuple index out of range
```

故如果是numpy类型的数组，获取图片尺寸应用：

```python
a.shape[0]
a.shape[1]
```

## 小结

- **torch**的**Tensor**形状可以用`size`，也可以用`shape`；

- **numpy**则只用`shape`