---
tags:
  - Transformer
date: 2024-03-26T17:41:00
---

[GitHub - zengwang430521/TCFormer: The codes for TCFormer in paper: Not All Tokens Are Equal: Human-centric Visual Analysis via Token Clustering Transformer](https://github.com/zengwang430521/TCFormer)

> VIT中的Token一般是图像patch转换来的，所有token比重相同，本文提出基于聚类的Token，自适应调整Token的shape， size

- Clustering-based Token Merge (CTM) Block generates vision tokens of various locations, sizes, and shapes for each image by progressive clustering and merging tokens.
- Multi-stage Token Aggregation (MTA) head aggregates token features in multiple stages

---

- 在Transformer Block 中去掉了位置编码，使用 depth-wise 卷积层来获得位置特征
- 聚类算法
- Whole Body Pose Estimation