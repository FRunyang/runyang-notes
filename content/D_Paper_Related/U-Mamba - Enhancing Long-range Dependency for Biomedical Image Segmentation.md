---
date: 2024-01
tags:
  - Mamba
---
>Mamba-UNet 系列论文：
>[[U-shaped Vision Mamba for Single Image Dehazing]]
>[[Mamba-UNet - UNet-Like Pure Visual Mamba for Medical Image Segmentation]]
>[[U-Mamba - Enhancing Long-range Dependency for Biomedical Image Segmentation]]


# 论文信息

**Title:** U-Mamba: Enhancing Long-range Dependency for Biomedical Image Segmentation
**Authors:** JunMa, FeifeiLi, BoWang
**期刊:**  
**类别:** preprint 
**Level:**  

>- **Url**: [Open online](http://arxiv.org/abs/2401.04722)
>- **zotero entry**: [Full Text PDF](zotero://select/library/items/WBYX2GH6)
>- **open pdf**: [zotero](zotero://select/library/items/CUK7DC4Q)
---

# Abstract:
Convolutional Neural Networks (CNNs) and Transformers have been the most popular architectures for biomedical image segmentation, but both of them have limited ability to handle long-range dependencies because of inherent locality or computational complexity. To address this challenge, we introduce U-Mamba, a general-purpose network for biomedical image segmentation. Inspired by the State Space Sequence Models (SSMs), a new family of deep sequence models known for their strong capability in handling long sequences, we design a hybrid CNN-SSM block that integrates the local feature extraction power of convolutional layers with the abilities of SSMs for capturing the long-range dependency. Moreover, U-Mamba enjoys a self-configuring mechanism, allowing it to automatically adapt to various datasets without manual intervention. We conduct extensive experiments on four diverse tasks, including the 3D abdominal organ segmentation in CT and MR images, instrument segmentation in endoscopy images, and cell segmentation in microscopy images. The results reveal that U-Mamba outperforms state-of-the-art CNN-based and Transformer-based segmentation networks across all tasks. This opens new avenues for efficient long-range dependency modeling in biomedical image analysis. The code, models, and data are publicly available at https://wanglab.ai/u-mamba.html.


# 概要

Code: https://wanglab.ai/u-mamba.html

*这篇是首次 Mamba + Unet (CNN)，应用于医学图像分割。学习局部特征+长距离依赖。*

# 方法

![[Pasted image 20240402142841.png]]


## Imported: 2024-04-02 2:26 下午

