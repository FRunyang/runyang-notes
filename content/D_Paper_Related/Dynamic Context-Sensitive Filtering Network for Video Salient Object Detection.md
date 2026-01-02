---
date: 
aliases:
  - 动态卷积
tags:
  - CNN
---

> 动态卷积

[GitHub - OIPLab-DUT/DCFNet: Dynamic Context-Sensitive Filtering Network for Video Salient Object Detection](https://github.com/OIPLab-DUT/DCFNet)

- 更复杂的卷积核生成方式；

![[Pasted image 20240326173841.png]]

DCFM estimates the location-related afﬁnity weights by introducing matrix multiplication into the kernels’ generation process.

**其实矩阵乘法到卷积核的位置关联特征我不太懂，感觉没什么道理**

- 双向特征融合

主要就是一个可学习的稀疏来加权两种特征

**整体网络结构特别复杂，感觉可以借鉴的不是很多**