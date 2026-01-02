---
date: 2024-02
tags:
  - Mamba
---
>Mamba-UNet 系列论文：
>[[U-shaped Vision Mamba for Single Image Dehazing]]
>[[Mamba-UNet - UNet-Like Pure Visual Mamba for Medical Image Segmentation]]
>[[U-Mamba - Enhancing Long-range Dependency for Biomedical Image Segmentation]]
# 论文信息

**Title:** U-shaped Vision Mamba for Single Image Dehazing
**Authors:** ZhuoranZheng, ChenWu
**期刊:**  
**类别:** preprint 
**Level:**  

>- **Url**: [Open online](http://arxiv.org/abs/2402.04139)
>- **zotero entry**: [Full Text PDF](zotero://select/library/items/YNGVV7EW)
>- **open pdf**: [zotero](zotero://select/library/items/WFGXBEG2)
---

# Abstract:
Currently, Transformer is the most popular architecture for image dehazing, but due to its large computational complexity, its ability to handle long-range dependency is limited on resource-constrained devices. To tackle this challenge, we introduce the U-shaped Vision Mamba (UVM-Net), an efficient single-image dehazing network. Inspired by the State Space Sequence Models (SSMs), a new deep sequence model known for its power to handle long sequences, we design a Bi-SSM block that integrates the local feature extraction ability of the convolutional layer with the ability of the SSM to capture long-range dependencies. Extensive experimental results demonstrate the effectiveness of our method. Our method provides a more highly efficient idea of long-range dependency modeling for image dehazing as well as other image restoration tasks. The URL of the code is \url{https://github.com/zzr-idam/UVM-Net}. Our method takes only \textbf{0.009} seconds to infer a $325 \times 325$ resolution image (100FPS) without I/O handling time.


# 概要

Code: https://github.com/zzr-idam/UVM-Net

用 UNet形状包裹起来的Mamba 网络，首次提出用于去雾的 vision mamba。

*CNN+SSM，局部特征+全局依赖性*
# 方法

![[Pasted image 20240402134833.png]]


## Imported: 2024-04-02 1:45 下午

