---
date: 2024-03-22T21:47:00
aliases:
  - ConvNext
tags:
  - CNN
  - 环境
---

大致按照官方文档来，此处主要是针对**ConvNext**的个性化：

[ConvNeXt/object_detection at main · FRunyang/ConvNeXt](https://github.com/FRunyang/ConvNeXt/tree/main/object_detection)

[GitHub - SwinTransformer/Swin-Transformer-Object-Detection at 6a979e2164e3fb0de0ca2546545013a4d71b2f7d](https://github.com/SwinTransformer/Swin-Transformer-Object-Detection/tree/6a979e2164e3fb0de0ca2546545013a4d71b2f7d)

[GitHub - open-mmlab/mmdetection: OpenMMLab Detection Toolbox and Benchmark](https://github.com/open-mmlab/mmdetection)

ConvNext模型的检测部分使用的SwinTransformer的Detection代码，SwinTransformer的 Detection又是机遇MMDetction的，所以环境配置主要是配置MMDetction。

---

[mmdetection/get_started.md at master · open-mmlab/mmdetection](https://github.com/open-mmlab/mmdetection/blob/master/docs/en/get_started.md/#Installation)

这个过程中碰到的几个坑：

- mmcv版本要求在1.3.1-1.7.0之间，所以可以直接安装 mmcvfull = 1.3.1

[Installation - mmcv 1.6.1 documentation](https://mmcv.readthedocs.io/en/latest/get_started/installation.html)

- 安装mmdetection用`pip install mmdet`，安装完之后在`{dir/requiremets}`里面的一些依赖也要安装一下，然后在根目录执行`pip install -v -e .`，**不然会出现注册器xxxx一堆报错，命令行无法运行。**
- ConvNext模型输出的结果是列表，[0]看起来是80类的box，[1]是分割的边界。因为是80类，所以推测是COCO数据集的检测类别，按照COCO的逻辑第0类即[0][0]为人物的box数据.