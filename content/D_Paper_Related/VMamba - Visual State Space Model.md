---
date: 2024-01
tags:
  - Mamba
---
> Mamba Backbone 系列论文
> [[Vision Mamba - Efficient Visual Representation Learning with Bidirectional State Space Model]]
> [[VMamba - Visual State Space Model]]
# 论文信息

**Title:** VMamba: Visual State Space Model
**Authors:** YueLiu, YunjieTian, YuzhongZhao, HongtianYu, LingxiXie, YaoweiWang, QixiangYe, YunfanLiu
**期刊:**  
**类别:** preprint 
**Level:**  

>- **Url**: [Open online](http://arxiv.org/abs/2401.10166)
>- **zotero entry**: [Liu 等 - 2024 - VMamba Visual State Space Model.pdf](zotero://select/library/items/E8GD9P3C)
>- **open pdf**: [zotero](zotero://select/library/items/NPD335AA)
---

# Abstract:
Convolutional Neural Networks (CNNs) and Vision Transformers (ViTs) stand as the two most popular foundation models for visual representation learning. While CNNs exhibit remarkable scalability with linear complexity w.r.t. image resolution, ViTs surpass them in fitting capabilities despite contending with quadratic complexity. A closer inspection reveals that ViTs achieve superior visual modeling performance through the incorporation of global receptive fields and dynamic weights. This observation motivates us to propose a novel architecture that inherits these components while enhancing computational efficiency. To this end, we draw inspiration from the recently introduced state space model and propose the Visual State Space Model (VMamba), which achieves linear complexity without sacrificing global receptive fields. To address the encountered direction-sensitive issue, we introduce the Cross-Scan Module (CSM) to traverse the spatial domain and convert any non-causal visual image into order patch sequences. Extensive experimental results substantiate that VMamba not only demonstrates promising capabilities across various visual perception tasks, but also exhibits more pronounced advantages over established benchmarks as the image resolution increases. Source code has been available at https://github.com/MzeroMiko/VMamba.


# 概要

这篇也是做视觉表征学习的 Backbone， 类似前面的 Vision Mamba。

**一个重点创新：图像是非因果性的，不能直视从前到后scan 一遍去建模。所以提出 4 个方向建模法，也就是 Cross-Scan Module (CSM)：****


![[Pasted image 20240402155714.png]]

![[Pasted image 20240402155724.png]]

# 方法

![[Pasted image 20240402155826.png]]

结构类似于 SwinTransformer

## Imported: 2024-04-02 3:43 下午

