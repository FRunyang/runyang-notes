---
title: 分类到回归的过程
date: 2020-02-25 10:06:09
tags:
  - Classification
cover: https://user-images.githubusercontent.com/60562661/75113101-71511600-5685-11ea-8948-9f21b72b9130.png
---

DeepLearning中另外一个常见的问题就是分类问题，这里以二分类为例。

*做二分类可不可以直接当作回归问题来处理呢？例如人为规定 calss1 对应输出值为1， class2对应值为-1，然后以均方误差为loss，做损失函数，这样直接train是可以train出来的，但是这样有一个问题，回归损失函数会惩罚比较大的正确项，例如一个数得出来结果是10远大于1，但是它和1明显是一类，而用回归做的话就会尽量减小这一loss，导致出现错误的结果，如下图：本来绿色的线是正确的分类，但是因为回归的惩罚会导致偏向紫色。 这是因为回归和分类的判断标准不一样。

<img src="https://user-images.githubusercontent.com/60562661/75210259-88921f80-57bb-11ea-9985-19f163a398c7.png" alt="1582596902251" style="zoom: 67%;" />

## 分类流程

<img src="https://user-images.githubusercontent.com/60562661/75210541-5208d480-57bc-11ea-8f59-6ba28470aa88.png" alt="1582597091411" style="zoom:80%;" />

1. 这里的model直接用的贝叶斯求出概率
2. 假设x服从高斯分布，此时要求出  **μ，σ**  用最大似然估计使得这个高斯分布所采样出来的这些点的概率最大
3. 求解最优的μ，σ。**μ 就是一组书的均值mean**  ，  μ，σ都有对应公式，也可以根据微分来求，如下图：

![1582597521938](https://user-images.githubusercontent.com/60562661/75210260-8a5be300-57bb-11ea-9423-008452e862f7.png)



## 分类与回归的转化

这里用图片截图出所有的公式推导，可以从第一张图直接跳到最后一张图看结论

<img src="https://user-images.githubusercontent.com/60562661/75210261-8af47980-57bb-11ea-873f-1021dc6ebb25.png" alt="1582597604571" style="zoom: 67%;" />

<img src="https://user-images.githubusercontent.com/60562661/75210263-8b8d1000-57bb-11ea-8165-8be93e1efb95.png" alt="1582597627023" style="zoom:67%;" />

 

<img src="https://user-images.githubusercontent.com/60562661/75210265-8c25a680-57bb-11ea-9849-26770bf8584c.png" alt="1582597710255" style="zoom:67%;" />

<img src="https://user-images.githubusercontent.com/60562661/75210268-8d56d380-57bb-11ea-943d-fac3d39d44f8.png" alt="1582597747533" style="zoom:67%;" />

<img src="https://user-images.githubusercontent.com/60562661/75210270-8def6a00-57bb-11ea-89c0-bfd800f1c1c0.png" alt="1582597839955" style="zoom: 37%;" />

**也就是说分类函数经过一系列的转换，最终变成了线性函数，即 ` P(C1|X) = σ(w * x + b)`,之前的方法我们要求五个参数才可以计算到最终结果，现在我们可以直接计算w，b就可以得到最终的概率！此时就变成了回归问题。然后就有了后面的逻辑回归，用交叉熵求出w，b**

**同时以上公式也说明了为什么 σ函数可以用来分类!**

