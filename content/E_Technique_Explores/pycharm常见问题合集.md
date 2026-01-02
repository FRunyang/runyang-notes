---
title: pycharm常见问题合集
date: 2021-02-26 10:22:08
tags:
  - 软件
cover: https://user-images.githubusercontent.com/60562661/109247017-2cbf0400-781e-11eb-9498-12db5e2d02a7.jpeg
---
> [[Mac pycharm 任意版本永久激活]]
## Pycharm DeBug进不去

forward函数运行能进去，但是debug进不去，很抓狂

**网上说的对pycharm本身进行设置基本解决不了该问题。**

**解决过程：**

1. 初始化时， `init` 内部打断点，看是否在正确的文件内部打了断点；
2. **终极操作：**

- **改成单gpu，单线程 运行，bug消除。**



## Pycharm DeBug卡死

![](https://user-images.githubusercontent.com/60562661/109246366-1cf2f000-781d-11eb-89c8-f4da5b58f417.png)



## Pycharm 修改缓存位置

**配置文件位置（win）：**

**D:\Program Files\JetBrains\PyCharm 2019.2.5\bin\idea.properties**

![](https://user-images.githubusercontent.com/60562661/109246591-7e1ac380-781d-11eb-9f31-b1eb3ab3dc92.png)



## Pycharm 代码模版

在pycharm菜单栏找File -> settings -> Editor -> File and Code Templates -> Python Script，找到后编辑：

```python
1 #!/usr/bin/env python
2 # _*_ coding: utf-8 _*_
3 # @Time : ${DATE} ${TIME} 
4 # @Author : Runyang 
5 # @Version：V 0.1
6 # @File : ${NAME}.py
7 # @desc :

'''
# @Lab : CVer
# @Time :  2020/12/3 21:00
# @Author : Runyang
# @Email : runyang.feng@qq.com
# @File : dcpose_backbone.py
'''
```

