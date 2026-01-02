> 偏向做网络结构设计，与SENet有点类似，做cross-frame的通道attention，同时有点像Residual Step Block，聚合多帧信息，总体来说网络结构一般新
> [[基于互信息的时序差分学习|差分建模]]

**Code：未开源**

- 聚合Temporal 信息会用一个 **1D Conv** ，在通道方向聚合，这个操作可以学习
![[Pasted image 20240326173340.png]]