---
date: 2020-03-23 22:24:54
tags:
  - Classification
cover: https://user-images.githubusercontent.com/60562661/77335087-a6be5180-6d60-11ea-875b-2ea4da5fa554.jpg
---

## softmax 作用

`softmax` 函数一般用在分类场景，尤其是多分类，它接受一组任意值作为输入，然后输出对应的一组**0-1**之间的数值，并且加起来为1，也就是做了归一化，实际上输出的值代表概率值。

## softmax 计算方式
![](https://user-images.githubusercontent.com/60562661/77334644-0e27d180-6d60-11ea-9844-be15700132e4.png)

如上图，z1,z2,z3 作为输入，分别取`exp`, 然后加起来作为分母，分别的除以分母就得到对应的值。即zi的softmax值为：
$$
S_{z_i} = \frac{\exp(z_i)}{\sum_{j=1}^3 \exp(z_j)  }
$$
推广一下：
$$
S_{z_i} = \frac{ \exp(z_i)}{\sum_{j} \exp(z_j)  }
$$
其中，$\sum_{i} S_{z_i} = 1$

## 再看交叉熵
对于二分类问题，交叉熵函数为：
$$
L = \hat{y_i}*\ln {y_i} + (1-\hat{y_i})*\ln{(1- y_i)}
$$
对于多分类问题：
$$
L = -\hat{y}*\ln(y)
$$
其中，$\hat{y}$表示label，y表示预测的值，由softmax函数计算得到

## softmax求导
上面已经知道多分类时交叉熵的公式，预测第i个时，认为它的label是1，则：
$$
L_i = -\ln(y_i)
$$
则：
$$
\frac{\partial L_i}{\partial i} = -\frac{\partial{\ln(y_i)}}{\partial i} = \frac{\partial \ln (\frac{e^i}{\sum_j e^j})}{\partial i} =··· ···=y_i-1
$$
具体推导如下图：

<img src="https://user-images.githubusercontent.com/60562661/77334662-14b64900-6d60-11ea-9b3d-beca92583e36.png" style="zoom:70%;" />

---
以上便是softmax函数的相关知识了。

