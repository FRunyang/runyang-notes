---
date: 
aliases:
  - GLobal Sequence
tags:
  - Pose-Estimation
---

短期内遮挡严重，用全局信息去做：

1. 取一个长序列，使用一个Transformer中的Encoder对每帧进行编码（显式输入帧号作为位置编码），得到一个Vector
2. 用当前帧的编码与其他帧计算相似度，作为每帧的概率
3. 取Top N相似的帧，对其特征进行融合
4. 动态Conv作为解码器，以当前帧作为模板，生成不同尺寸的卷积核，到聚合的特征中进行卷积操作，最终聚合得到heatmap预测

---

以上实现存在问题，分析：

- stage1的特征过于浅层，直接进行融合后，直接用动态卷积计算heatmap网络层过浅

进行改进：

- stage1 融合之后，输入后续HRNet进行训练（正在训练）

---

改进二：

- 为了快速出效果，在stage3特征进行融合；
- 初步融合之后，使用边界attention操作为当前帧补充信息；
- 随后使用卷积+动态卷积进行解码

---

# TOMM论文 《GLPose: Global-Local Representation Learning for Human Pose Estimation》已录用。