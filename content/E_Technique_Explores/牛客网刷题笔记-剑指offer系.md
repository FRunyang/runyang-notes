---
title: 二维数组中的查找
date: 2020-02-11 19:49:48
tags:
  - 刷题
  - Code
cover: https://user-images.githubusercontent.com/60562661/74247994-e2a5d600-4d21-11ea-8524-81fb2d58117a.jpeg
---

自己最近正好有空，因此开始了刷题系列，牛客网上的剑指offer题目。今天记录一个比较有思想的题目。因为这些都是算法题目，如果去用穷举蒙混过关就没意思了，因此尽量找比较优化的算法。我这里用python来解答。

最近正好也是有空，因此开始了刷题系列，牛客网上的剑指offer题目。今天记录一个比较有思想的题目。因为这些都是算法题目，如果去用穷举蒙混过关就没意思了，因此尽量找比较优化的算法。我这里用python来解答。

## 题目：

`在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。`

## 思路：

#### 思路一：

因为数组的有序性，从左到右从上到下递增，利用这一个规律，选取左下角的数为基点，如果目标数大于该数，那么目标肯定在基点的右边，所以 **column + 1 **; 如果目标小于基点数，那么 **row - 1 **。

逻辑是这样，每移动一次，都会以目前所在的点为基点，因此会排除一行或者一列，这种复杂度就会比较低了。‘

#### 代码

```python
# -*- coding:utf-8 -*-
class Solution:
    # array 二维列表
    def Find(self, target, array):
        hang = len(array)
        lie = len(array[0])
        i = hang - 1
        j = 0
        result = False
        while(i>=0 and j<lie):
            if target < array[i][j]:
                i = i - 1
            elif target > array[i][j]:
                j = j + 1
            elif target == array[i][j]:
                result = True
                return result
        return result
```

#### 思路二：

遍历每一行用二分查找法，这个代码还没写，所以明天补上，这种方法比较通俗易懂。



 