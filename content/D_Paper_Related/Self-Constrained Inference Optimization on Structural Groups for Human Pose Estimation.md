> 做图片姿态估计，针对 `人体关节的结构化约束` & `高低置信度关键点预测` 提出解决方案。
> [[关节结构化约束|结构化]]



**Motivation & 基本观点**:

- We observe that human poses exhibit strong group-wise structural correlation and spatial coupling between keypoints due to the biological constraints of different body parts. This group-wise structural correlation can be explored to improve the accuracy and robustness of human pose estimation.

**代码未开源**

![[Pasted image 20240326172341.png]]

## 要点：

整体方法可以分为两部分，分别从训练和测试阶段进行理解比较方便，前提是先进行关键点分组。

- **关节分组**：
    - 按人体结构对关节进行分组，划分为6组，每组4个关节
    - 手动划分置信度高低的点：在每个组内靠近躯干的点认为是base的点，一个边缘的点认为是端点 terminal keypoints

![[Pasted image 20240326172404.png]]

- **Training:** 用 `prediction-verification` 网络结构来学习关节内部结构化关系
    - 首先基于HRNET拿到初始的 `heatmap` & `features`
    - **训练预测网络**：以一个关节组为例，用三个**base**关节的heatmap以及feature输入预测网络，推理出**terminal** 关节的heatmap；把预测网络的输出与其他输入堆叠作为验证网络的输入，来预测`第一个base关节的heatmap，这样可以形成一个闭环，同时约束两个网络的输出；训练期间冻结验证网络
    - **训练验证网络**：反一下上述过程就行，先验证再预测，loss约束从pipeline图可以看到
- **Testing**：在推理期间优化低置信度的关键点（就是优化Terminal Keypoint）
    - 送来一组测试sample，先用预测网络预测出关节组里面端点的heatmap
    - 划定一个范围，对heatmap加上扰动，进行采样，
    - 将该heatmap以及相应的输入输入到验证网络进行反向预测，得到第一个base关节的heatmap，优化即保证将所选择的预测的terminal关节的heatmap输入验证网络后所得结果能与HRNet预测的初始的结果loss最小
    - Here, the basic idea is that: if the prediction X D becomes accurate during local search, then, using it as the input, the verification network should be able to accurately predict the high-confidence keypoint H A , which implies that the self-constraint loss || H A − H A || 2 on the high-confidence keypoint X A should be small.

## 反思

- 这篇论文整体挺复杂的，所提的这种cycle-like的学习方法来学习关节关系比较有趣，但是论文的说法** `Self-Constrained Learning`** 与一般的自监督学习并不一样
- heatmap加上扰动再重采样这个做法确实不错，看上去可以实现测试期间的优化
- 有个问题是直接自己定义好了低置信度的关节，这篇论文避开了这个关键问题。按理来说应该每次都能判断出哪些预测的关节精度较低，而不是手动定义，这个可以作为后续扩展方向