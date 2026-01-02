---
date: 2024-03-22T21:46:00
tags:
  - 环境
aliases:
  - numpy
---
**numpy.ndarray size changed, may indicate binary incompatibil**

二进制巴拉巴拉一堆问题

问题在于numpy版本太低。有两种解决方案：

1. 直接更新numpy版本

`pip install --upgrade numpy`

1. 卸载pycocotools库，先安装numpy，在安装pycocotools

推荐使用这种方案，这种方案可以保持旧版本numpy，新版本会有很多的warning