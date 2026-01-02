> 学习时序差分特征作动作识别，网络结构平平无奇，很朴素，但是复杂
> [[基于互信息的时序差分学习|差分建模]]

**Code Link： [https://github.com/MCG-NJU/TDN**](https://github.com/MCG-NJU/TDN**)

[GitHub - MCG-NJU/TDN: [CVPR 2021] TDN: Temporal Difference Networks for Efficient Action Recognition](https://github.com/MCG-NJU/TDN)

- 时序差分建模网络，输入为图片的差，捕获视频的运动表征 （直接concat连续帧效果一般般）*
- 分别建模 **外观** + **运动表征** ， 用相加操作融合*
- 短期运动模式加长期的
- 稀疏采样，把视频分成多个segment，每个片段随机取一帧，以此采样多帧

![[Pasted image 20240326172919.png]]