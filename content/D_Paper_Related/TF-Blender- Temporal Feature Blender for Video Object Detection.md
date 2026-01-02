
> 一种新的多帧特征聚合方式，更充分的对每帧进行增强；建模当前帧与其他帧的关系权重

[GitHub - goodproj13/TF-Blender](https://github.com/goodproj13/TF-Blender)

Despite achieving improvements in detection, existing methods focus on the selection of **higher-level video frames for aggregation** rather than modeling **lower-level temporal relations to increase the feature representation.**

![[Pasted image 20240326174027.png]]

**三个步骤：**

- 建模当前帧与每个辅助帧的时序关系；
- 建模每个辅助帧与其他辅助帧的关系以增强该辅助帧；
- 组合上述结果进行特征聚合

![[Pasted image 20240326174046.png]]

---

感觉有点工程化，充分建模各种相关关系；称为“Temporal Relation”