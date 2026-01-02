---
date: 2024-03
---

# 论文信息

**Title:** VM-UNET-V2 Rethinking Vision Mamba UNet for Medical Image Segmentation
**Authors:** MingyaZhang, YueYu, LimeiGu, TingshengLin, XianpingTao
**期刊:**  
**类别:** preprint 
**Level:**  

>- **Url**: [Open online](http://arxiv.org/abs/2403.09157)
>- **zotero entry**: [Full Text PDF](zotero://select/library/items/X3GDWENY)
>- **open pdf**: [zotero](zotero://select/library/items/KBEELLHD)
---

# Abstract:
In the field of medical image segmentation, models based on both CNN and Transformer have been thoroughly investigated. However, CNNs have limited modeling capabilities for long-range dependencies, making it challenging to exploit the semantic information within images fully. On the other hand, the quadratic computational complexity poses a challenge for Transformers. Recently, State Space Models (SSMs), such as Mamba, have been recognized as a promising method. They not only demonstrate superior performance in modeling long-range interactions, but also preserve a linear computational complexity. Inspired by the Mamba architecture, We proposed Vison Mamba-UNetV2, the Visual State Space (VSS) Block is introduced to capture extensive contextual information, the Semantics and Detail Infusion (SDI) is introduced to augment the infusion of low-level and high-level features. We conduct comprehensive experiments on the ISIC17, ISIC18, CVC-300, CVC-ClinicDB, Kvasir, CVC-ColonDB and ETIS-LaribPolypDB public datasets. The results indicate that VM-UNetV2 exhibits competitive performance in medical image segmentation tasks. Our code is available at https://github.com/nobodyplayer1/VM-UNetV2.


# 概要

前置工作：[[VM-UNet - Vision Mamba UNet for Medical Image Segmentation]]

改进：加了一个SDI 模块，类似于 HRNet 的融合

![[Pasted image 20240409195206.png]]
# 方法

![[Pasted image 20240409195152.png]]


## Imported: 2024-04-09 7:44 晚上

