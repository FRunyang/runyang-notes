---
date: 2024-03-22T21:08:00
aliases:
  - 隐式表示
tags:
  - Pose-Estimation
---
### 图像的隐式表示可以表征任意分辨率的图像/特征：

对于Feature-Level的表示

![[Pasted image 20240322210920.png]]

主要是训练一个解码器 f , 对于原始feature map的xq位置，z_表示它的latent code（即特征的值），x_表示2d坐标（每个element都分配一个2d坐标）

---
### 后续在学习学习这个方向 感觉很容易用到姿态估计