---
title: Pytorch Dataloader 用法
date: 2020-07-09 14:41:13
tags:
  - pytorch编程
  - Code
cover: https://user-images.githubusercontent.com/60562661/87008701-bb7f0200-c1f6-11ea-8177-1e4a76b83143.jpg
---



## DataLoder

Pytorch在训练前一步数据读取时，要使用 `DataLoader` 加载数据, 可以`shuffle`  、多线程读取等。记录一下如何使用。

> 自黑一下，之前我写的第一个工程，完全没写DataLoader，直接把原图，标签放在两个大列表里面来循环，😂🤣，所以当时16g内存都直接溢出😆，所以说不写DataLoader也不是不可以，就是有点不可描述



## 使用步骤

### 定义Dataset

```python
torch.utils.data.Dataset 
```

首先自定义`dataset`类，以上述`Dataset`为父类，必须重写`__getitem__()` 方法，即获取数据逻辑；

可选重写`__len()__`方法，获取数据长度信息。

类似如下，是我们最近做的一个研究中`Dataset` 片段，重点关注它`return`的结果。

```python
import torch.utils.data.Dataset 

# 定义 Dataset
class JointsDataset(Dataset):
    def __init__(self, ........):
        pass
    def __len__(self, ):
        return len(self.db)
    def __getitem__(self, idx):
        '''
        省略代码块
        '''
        return input_data_numpy, input_sup_A_data_numpy, input_sup_B_data_numpy, target_heatmaps, target_weight, meta
```



### 创建 DataLoader

先看一下Dataloader类定义

```python
torch.utils.data.DataLoader(dataset, batch_size=1, shuffle=False, sampler=None, batch_sampler=None, num_workers=0, collate_fn=None, pin_memory=False, drop_last=False, timeout=0, worker_init_fn=None, multiprocessing_context=None)
```

一般用的几个参数：

- dataset 为上述的自定义的类
- batch_size 
- shuffle 打乱数据
- num_workers 多线程
- pin_memory 更快的发送数据到显存 （不太清楚）

```python
train_dataset = JointsDataset(
        cfg, cfg.DATASET.ROOT, cfg.DATASET.TRAIN_SET, True,
        cfg.DATASET.TRAIN_NPY_DIR,
        transform=transforms.Compose([
            transforms.ToTensor(),
            normalize,
        ])
    )

train_loader = torch.utils.data.DataLoader(
        train_dataset,
        batch_size=cfg.TRAIN.BATCH_SIZE_PER_GPU * len(cfg.GPUS),
        shuffle=cfg.TRAIN.SHUFFLE,
        num_workers=cfg.WORKERS,
        pin_memory=cfg.PIN_MEMORY
    )
```



### 迭代获取数据

```python
for i, (input, input_sup_A, input_sup_B, target, target_weight, meta) in enumerate(train_loader):
    pass
```

关于获取的数据可以看到和自定义`dataset`类`__getitem()__`方法返回的东西是一样的。

---

总结一下，定义`dataset`, 创建`dataloder`, 迭代获取进行训练。

