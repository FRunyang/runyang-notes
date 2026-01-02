---
date: 2024-04-01T00:00:00
aliases:
  - Mamba
tags:
  - Mamba
---
> Mamba Backbone 系列论文
> [[Vision Mamba - Efficient Visual Representation Learning with Bidirectional State Space Model]]
> [[VMamba - Visual State Space Model]]
# 论文信息

**Title:** Vision Mamba: Efficient Visual Representation Learning with Bidirectional State Space Model
**Authors:** LianghuiZhu, BenchengLiao, QianZhang, XinlongWang, WenyuLiu, XinggangWang
**期刊:**  
**类别:** preprint 
**Level:**  

>- **Url**: [Open online](http://arxiv.org/abs/2401.09417)
>- **zotero entry**: [Full Text PDF](zotero://select/library/items/YT7PQZN3)
>- **open pdf**: [zotero](zotero://select/library/items/9TFAA8TP)
---

# Abstract:
Recently the state space models (SSMs) with efficient hardware-aware designs, i.e., the Mamba deep learning model, have shown great potential for long sequence modeling. Meanwhile building efficient and generic vision backbones purely upon SSMs is an appealing direction. However, representing visual data is challenging for SSMs due to the position-sensitivity of visual data and the requirement of global context for visual understanding. In this paper, we show that the reliance on self-attention for visual representation learning is not necessary and propose a new generic vision backbone with bidirectional Mamba blocks (Vim), which marks the image sequences with position embeddings and compresses the visual representation with bidirectional state space models. On ImageNet classification, COCO object detection, and ADE20k semantic segmentation tasks, Vim achieves higher performance compared to well-established vision transformers like DeiT, while also demonstrating significantly improved computation & memory efficiency. For example, Vim is 2.8$\times$ faster than DeiT and saves 86.8% GPU memory when performing batch inference to extract features on images with a resolution of 1248$\times$1248. The results demonstrate that Vim is capable of overcoming the computation & memory constraints on performing Transformer-style understanding for high-resolution images and it has great potential to be the next-generation backbone for vision foundation models. Code is available at https://github.com/hustvl/Vim.


# 概要

Code： https://github.com/hustvl/Vim

提出纯 SSM Backbone，主要包括**两个重点设计**：
- *双向 Mamba 建模，相当于前向处理输入 + 逆向处理输入* -- 原始的只能单向处理
- *给 visual token 加上了位置编码，实现位置感知* -- 原始 mamba 处理一位数据，不能感知位置

# 方法

Image2Token -> Mamba Encoder -> MLP Projection

![[Pasted image 20240402132122.png]]

**几个重要影响性能的：**
- SSM 之前的`Conv1D`很重要
- 分类 Token 放到中间效果好

![[Pasted image 20240402132408.png]]
## Imported: 2024-04-01 4:06 下午
