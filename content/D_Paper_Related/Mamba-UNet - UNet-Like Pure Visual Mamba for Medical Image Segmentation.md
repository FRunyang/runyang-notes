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

**Title:** Mamba-UNet: UNet-Like Pure Visual Mamba for Medical Image Segmentation
**Authors:** ZiyangWang, Jian-QingZheng, YichiZhang, GeCui, LeiLi
**期刊:**  
**类别:** preprint 
**Level:**  

>- **Url**: [Open online](http://arxiv.org/abs/2402.05079)
>- **zotero entry**: [Full Text PDF](zotero://select/library/items/XLY3WZTC)
>- **open pdf**: [zotero](zotero://select/library/items/A9XPH8RR)
---

# Abstract:
In recent advancements in medical image analysis, Convolutional Neural Networks (CNN) and Vision Transformers (ViT) have set significant benchmarks. While the former excels in capturing local features through its convolution operations, the latter achieves remarkable global context understanding by leveraging self-attention mechanisms. However, both architectures exhibit limitations in efficiently modeling long-range dependencies within medical images, which is a critical aspect for precise segmentation. Inspired by the Mamba architecture, known for its proficiency in handling long sequences and global contextual information with enhanced computational efficiency as a State Space Model (SSM), we propose Mamba-UNet, a novel architecture that synergizes the U-Net in medical image segmentation with Mamba's capability. Mamba-UNet adopts a pure Visual Mamba (VMamba)-based encoder-decoder structure, infused with skip connections to preserve spatial information across different scales of the network. This design facilitates a comprehensive feature learning process, capturing intricate details and broader semantic contexts within medical images. We introduce a novel integration mechanism within the VMamba blocks to ensure seamless connectivity and information flow between the encoder and decoder paths, enhancing the segmentation performance. We conducted experiments on publicly available MRI cardiac multi-structures segmentation dataset. The results show that Mamba-UNet outperforms UNet, Swin-UNet in medical image segmentation under the same hyper-parameter setting. The source code and baseline implementations are available.


# 概要

Code：[https://github.com/ziyangwang007/Mamba-UNet](https://github.com/ziyangwang007/Mamba-UNet)

纯 Mamba 结构

*以 SwinUNet 结构为模板，替换了其中的 building block， 用 SS2D，来源于（VMamba）。*

# 方法

![[Pasted image 20240402145424.png]]

![[Pasted image 20240402145415.png]]


## Imported: 2024-04-02 2:52 下午

