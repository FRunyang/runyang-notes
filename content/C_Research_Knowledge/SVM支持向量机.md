---
date: 2020-05-03 13:53:47
tags:
  - SVM
  - Classification
cover: https://user-images.githubusercontent.com/60562661/80908552-52d95c00-8d53-11ea-897b-6008854c7054.jpg
---

李宏毅老师视频：https://www.bilibili.com/video/BV14W411u78t?from=search&seid=16299976979408181063

知乎讲解  ：https://zhuanlan.zhihu.com/p/49331510

数学完整推导视频：https://www.bilibili.com/video/BV12J41157qV?p=6 （浙大机器学习课程）

文中几张图引自改知乎文章。

#  Support Vector Machine

## 概述

整体上，支持向量机是一个分类算法，即寻找能分开两类数据的超平面，并且这个超平面满足距离超平面最近的数据点的到超平面距离最大。

![1588485540815](https://user-images.githubusercontent.com/60562661/80908414-43a5de80-8d52-11ea-85e0-4c37fbcf497a.png)

如图，H2和H3都实现了正确的分类，但是SVM会选择H3，因为两类数据中距离H3最近的点的距离比其他所有的点到H3的距离都要大，满足一开始所述的条件。

![](https://user-images.githubusercontent.com/60562661/80908422-486a9280-8d52-11ea-9567-210a53e582f8.jpg)

 目前求解目标是使得图中`margin`最大,经过推导得出最终的抽象的公式：
$$
min_{W,b}\frac{1}{2}||W||^2,
s.t. y_i*(X_i^TW+B) >= 1
$$


这个公式也就是硬匹配规则，简单解释一下：

- yi表示第i个数据的真实类别，取值为 1，-1；
- 第i笔数据真实类别与计算出来的值同号，即保证分类准确的前提下，最大化边界。



![1588486535546](https://user-images.githubusercontent.com/60562661/80908416-456fa200-8d52-11ea-9f08-6e017d7a1002.png)

这些处于边界的几个数据点称为支持向量，**在决定最佳超平面时只有支持向量起作用，而其他数据点并不起作用。**

## 推导

`SVM = Hingle_loss + Kernel_Method `

### Hingle Loss

$$
l(f(x_n),\hat y_n) = max(0,1-\hat y_n*f(x_n))
$$

其中，
$$
\hat y_n = 1,-1
$$
当真值与预测值同号，并且乘积比比正确的好过一段距离，即乘积大于等于1时，loss为0，好过的这段距离即为margin。参考下图：

![1588487132298](https://user-images.githubusercontent.com/60562661/80908417-46083880-8d52-11ea-8411-64b067eb54d7.png)

### Linear SVM

- **Model:**

$$
f(x) = \sum_iw_ix_i +b =  \begin{bmatrix}
   w\\
   b \\
  \end{bmatrix} ·\begin{bmatrix}
   x\\
   1 \\
  \end{bmatrix}= W^Tx
$$



- **Loss function**

$$
L(f) = \sum_nl(f(x_n),\hat y_n) + \lambda||w||_2
$$

损失函数是一个凸函数，因此可以用梯度下降法来求解，具体看李宏毅老师视频。

这里的SVM损失函数和一开始概述里面提到的目标函数似乎不太一样？经过如下转换，就得到了最初的形式。

![1588487368252](https://user-images.githubusercontent.com/60562661/80908419-46a0cf00-8d52-11ea-92f7-659896a8e9be.png)

最后面1减去了一项，表示是软匹配，不一定能达到1的情况。

### Kernel Method

首先，要找的W*(w,b)是数据点的线性组合：
$$
w^* = \sum_na^*_n*x^n
$$
为了解释这件事，一般就引入了拉格朗日方法来算一通，这里用另外一种思路：

![1588488346353](https://user-images.githubusercontent.com/60562661/80908420-47396580-8d52-11ea-8ebc-e4f024e97b2d.png)

用梯度下降法求解时，cn(w)由于hingleloss的原因，会有一部分值为0，即不是所有的xn都会对w有影响，w初始化为0时很多数据点对更新w的值毫无用处，即a*是稀疏的。

当a* != 0时，对应的数据点就叫做 `Support vector`.支持向量机名字也由此得来。

此时w可以换一种形式写：


$$
w = \sum_na_nx_n = X \alpha
$$
故，Model：
$$
f(x) = w^Tx = \alpha^TX^Tx =\sum_na_n(x_n·x) = \sum_na_nK(x_n,x)
$$
找一个最好的 **α** ，最小化损失函数：
$$
L(f) =\sum_nl(f(x_n),\hat y_n) = \sum_nl(\sum_{n'}a_{n'}K(x_{n'},x_n),\hat y_n)
$$
这里不需要知道具体的x，只要能求出`K(x,z)`的值即可。

### Kernel Trick

上述的损失函数如果直接用x，z是不好的，需要用他们的特征。用核方法就不用管他们的 特征是什么样子的。

即两个向量转化为特征向量再求内积是比较麻烦的，直接计算两个向量的内积再求特征会更快。

此时需要定义一个核函数，就可以简化计算。这里的
$$
K(x,z)
$$
就是一个核函数，**可以选取不同的核函数。**

![1588490434815](https://user-images.githubusercontent.com/60562661/80908421-47d1fc00-8d52-11ea-8c1b-0d4d26919f99.png)

而核函数计算就是把原始数据投影到高维的一个内积，即在做分类时，先把二维数据投影到高维空间，在做一个 线性分类，上图就很明显了。



## 疑问

- Kernel Trick 是投影到高维的一个计算？
- 逻辑是计算出K，就可以找出α了。而投影到高维只是计算K的一个方法，为什么可以代表svm呢?
- 这些疑问以后再看。

---

2020-6-7日更新：

**SVM通过数学理解更加合理！**

