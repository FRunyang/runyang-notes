---
title: Pytorch / Python 中的GPU调用
date: 2021-02-26 23:45:16
tags:
  - pytorch编程
  - Code
cover: https://user-images.githubusercontent.com/60562661/84798845-0493ca00-b02e-11ea-8a2c-f488ed901161.jpg
---

一般用Pytorch编程训练模型肯定是要用GPU，多GPU有时候会一直出问题，这里记录一下。

## Pytorch用GPU计算

可以用Python的方法把程序发送到GPU：

```python
os.environ["CUDA_VISIBLE_DEVICES"] = "2" # 用第三个显卡来计算
 
os.environ["CUDA_VISIBLE_DEVICES"] = "0，1，2" # 用第三个显卡来计算   
```

注意这种方法只能用到一张卡根据我的测试，不能并行计算，要并行计算的话需要一下代码：



```python
# 用三张显卡并行的跑数据
model_cuda = torch.nn.DataParallel(model.cuda(), device_ids=(0,1,2))
# batch_size的设置
batch_size = origin_batch_size * len(cfg.GPUS)
```

---

注意，一般情况下不用`os.environ`的话，所有的初始张量、模型都会加载在显卡0，故此时如果0显卡被占满会一直提示`CUDA OUT OF MEMORY` 错误。

---

## 第二次更新

Pytorch一般情况主GPU是第一块显卡，可以用以下命令来指定主显卡设备：

```python
torch.cuda.set_device(2)  # 指定GPU2伟主要计算GPU
```

建议用这个命令代替python命令。

---

## 第三次更新

### **1.直接终端中设定：**

```python
CUDA_VISIBLE_DEVICES=1 python my_script.py
```

### **2. python代码中设定：**

```python
import os
os.environ["CUDA_VISIBLE_DEVICES"] = "2"
```

### **3. 使用函数 set_device**

```python
import torch
torch.cuda.set_device(id)
```

官方建议使用 CUDA_VISIBLE_DEVICES

