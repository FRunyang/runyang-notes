---
date: 2024-02
---

# 论文信息

**Title:** VM-UNet: Vision Mamba UNet for Medical Image Segmentation
**Authors:** JiachengRuan, SunchengXiang
**期刊:**  
**类别:** preprint 
**Level:**  

>- **Url**: [Open online](http://arxiv.org/abs/2402.02491)
>- **zotero entry**: [Full Text PDF](zotero://select/library/items/6DC6C6RW)
>- **open pdf**: [zotero](zotero://select/library/items/TDM2Y37D)
---

# Abstract:
In the realm of medical image segmentation, both CNN-based and Transformer-based models have been extensively explored. However, CNNs exhibit limitations in long-range modeling capabilities, whereas Transformers are hampered by their quadratic computational complexity. Recently, State Space Models (SSMs), exemplified by Mamba, have emerged as a promising approach. They not only excel in modeling long-range interactions but also maintain a linear computational complexity. In this paper, leveraging state space models, we propose a U-shape architecture model for medical image segmentation, named Vision Mamba UNet (VM-UNet). Specifically, the Visual State Space (VSS) block is introduced as the foundation block to capture extensive contextual information, and an asymmetrical encoder-decoder structure is constructed. We conduct comprehensive experiments on the ISIC17, ISIC18, and Synapse datasets, and the results indicate that VM-UNet performs competitively in medical image segmentation tasks. To our best knowledge, this is the first medical image segmentation model constructed based on the pure SSM-based model. We aim to establish a baseline and provide valuable insights for the future development of more efficient and effective SSM-based segmentation systems. Our code is available at https://github.com/JCruan519/VM-UNet.


# 概要

VSSBlock [[Vision Mamba - Efficient Visual Representation Learning with Bidirectional State Space Model]] + UNet
# 方法

没有什么新的
![[Pasted image 20240409195128.png]]
## Imported: 2024-04-02 11:07 晚上

