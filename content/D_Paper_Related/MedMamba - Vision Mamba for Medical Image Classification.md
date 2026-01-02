---
date: 2024-03
---

# 论文信息

**Title:** MedMamba: Vision Mamba for Medical Image Classification
**Authors:** YubiaoYue, ZhenzhangLi
**期刊:**  
**类别:** preprint 
**Level:**  

>- **Url**: [Open online](http://arxiv.org/abs/2403.03849)
>- **zotero entry**: [Full Text PDF](zotero://select/library/items/6MXP2B3A)
>- **open pdf**: [zotero](zotero://select/library/items/RQTR9G2Q)
---

# Abstract:
Medical image classification is a very fundamental and crucial task in the field of computer vision. These years, CNN-based and Transformer-based models have been widely used to classify various medical images. Unfortunately, The limitation of CNNs in long-range modeling capabilities prevents them from effectively extracting features in medical images, while Transformers are hampered by their quadratic computational complexity. Recent research has shown that the state space model (SSM) represented by Mamba can efficiently model long-range interactions while maintaining linear computational complexity. Inspired by this, we propose Vision Mamba for medical image classification (MedMamba). More specifically, we introduce a novel Conv-SSM module. Conv-SSM combines the local feature extraction ability of convolutional layers with the ability of SSM to capture long-range dependency, thereby modeling medical images with different modalities. To demonstrate the potential of MedMamba, we conducted extensive experiments using 14 publicly available medical datasets with different imaging techniques and two private datasets built by ourselves. Extensive experimental results demonstrate that the proposed MedMamba performs well in detecting lesions in various medical images. To the best of our knowledge, this is the first Vision Mamba tailored for medical image classification. The purpose of this work is to establish a new baseline for medical image classification tasks and provide valuable insights for the future development of more efficient and effective SSM-based artificial intelligence algorithms and application systems in the medical. Source code has been available at https://github.com/YubiaoYue/MedMamba.


# 概要

用 `Mamba` 做分类。感觉 Mamba 在医学图像很火 [这个领域比较水吧]

SSM 用的 SS2D 模型，感觉这个很适合做基础模块 [[VMamba - Visual State Space Model]]
# 方法

![[Pasted image 20240413112730.png]]


## Imported: 2024-04-13 11:24 上午

