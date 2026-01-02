> The TEI module presents a different paradigm to learn temporal features by decoupling the modeling of channel correlation and temporal interaction.
> [[基于互信息的时序差分学习|差分建模]]

**Code：未开源**

![[Pasted image 20240326173439.png]]

网络包含两个模块：

- **Motion Enhanced Module（MEM）** 相当于提了一个结合difference的通道Attention模块，用另外一帧对当前帧重新进行权重调整；
- **Temporal Interaction Module（TIM）**对不同帧进行channel-wise的融合 **[感觉channel方向融合1*1卷积并不是最佳选择，例如分析optical flow 和 Deformable Convolution的那篇]**

综合一下就是先根据邻居帧对当前帧进行调整，然后再融合