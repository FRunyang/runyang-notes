---
date: 
tags:
  - Pose-Estimation
aliases:
  - 测试期间个性化
---
## 论文 《Test-Time Personalization with a Transformer for Human Pose Estimation》

使用自监督方法，在测试期间可以train一下以适应测试集。

### 启发与改进：

- 自监督学习与姿态估计结合，本文用的是姿态到图像的重建任务；可以结合 human parsing 任务到图像重建，观察其特征对姿态估计的作用
- 使用多个自监督任务与姿态估计结合，看看是否有提升
- 自监督任务可以由多个 KeyPoints 获 **parsing 的body特征转换为最终关键点**
- 本篇论文使用**Tranformer**来进行自监督的结果到最终结果的转换，**可以替换成可形变卷积，应该会提点**