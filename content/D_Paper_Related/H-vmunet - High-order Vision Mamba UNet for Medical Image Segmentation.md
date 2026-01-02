---
date: 2024-03
---

# 论文信息

**Title:** H-vmunet: High-order Vision Mamba UNet for Medical Image Segmentation
**Authors:** RenkaiWu, YinghaoLiu, PengchenLiang, QingChang
**期刊:**  
**类别:** preprint 
**Level:**  

>- **Url**: [Open online](http://arxiv.org/abs/2403.13642)
>- **zotero entry**: [Full Text PDF](zotero://select/library/items/3CRKMAS8)
>- **open pdf**: [zotero](zotero://select/library/items/MTQ67WM5)
---

# Abstract:
In the field of medical image segmentation, variant models based on Convolutional Neural Networks (CNNs) and Visual Transformers (ViTs) as the base modules have been very widely developed and applied. However, CNNs are often limited in their ability to deal with long sequences of information, while the low sensitivity of ViTs to local feature information and the problem of secondary computational complexity limit their development. Recently, the emergence of state-space models (SSMs), especially 2D-selective-scan (SS2D), has had an impact on the longtime dominance of traditional CNNs and ViTs as the foundational modules of visual neural networks. In this paper, we extend the adaptability of SS2D by proposing a High-order Vision Mamba UNet (H-vmunet) for medical image segmentation. Among them, the proposed High-order 2D-selective-scan (H-SS2D) progressively reduces the introduction of redundant information during SS2D operations through higher-order interactions. In addition, the proposed Local-SS2D module improves the learning ability of local features of SS2D at each order of interaction. We conducted comparison and ablation experiments on three publicly available medical image datasets (ISIC2017, Spleen, and CVC-ClinicDB), and the results all demonstrate the strong competitiveness of H-vmunet in medical image segmentation tasks. The code is available from https://github.com/wurenkai/H-vmunet .


# 概要

UNET SS2D 有个 **High-order 的 SSM Block**
# 方法
![[Pasted image 20240413113125.png]]


![[Pasted image 20240413113602.png]]
## Imported: 2024-04-13 11:25 上午

