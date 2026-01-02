---
tags:
  - Disentanglement
aliases:
  - 特征解耦
---

> 做年龄无关的人脸识别 age-invariant face recognition (AIFR)，需要将人脸表征分解为 identity-dependent & age-dependent components，解纠缠学习这两部分特征，且用互信息来监督学习到的特征；然后只使用身份特征进行人脸识别。
> [[基于互信息的时序差分学习|差分建模]]

- We obtain the age-related features through a FC layer from the initial features, and the identity-related features are obtained from the subtract between initial features and age-related features. **用减法得到解纠缠的特征表示**
- 互信息估计时，使用Contrastive Log-ratio Upper Bound (CLUB)，估计互信息的上界来进行最小化
- 可以画特征解纠缠前后的分布图来证明解纠缠学习效果

![[Pasted image 20240326174328.png]]

![[Pasted image 20240326174342.png]]