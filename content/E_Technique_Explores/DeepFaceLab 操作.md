---
date: 2024-03-22T23:24:00
tags:
  - 换脸
  - 软件
aliases:
  - 换脸操作
---


一些资料：

## 1. 目录结构

```python
# 文件目录结构

target_image_dir = "/workspace/data_dst" # 

source_image_dir = "/workspace/data_src" # 谁被替换就是dst，替换来源是src

# === 图片命名：00001.jpg (%5d) ===

```

## 2. 操作流程

1)初始化文件夹（点击后将清空workspace文件夹）

2. src视频转图片
    
3. dst视频转图片.bat
    

**a) full face**

(简称F脸，额头部分有些许被裁到)

**b) whole face**

(简称WF脸，范围更大，整个额头都取了，兼容WF和F脸模型)

**c) head**

(不常用，给高玩做avatar用，萌新用不到)

4. 提取src头像.bat

4.1) 查看src头像.bat 删除错误的图片

5. dst头像提取.bat

5.1) 查看dst头像.bat 删除错误的图片

6. 训练SAEHD模型.bat

一般加载现有模型，然后预训练选择N

7. 应用SAEHD模型
    
8. 合成 MP4 视频 merged to mp4
    

## 3. 总结

- src有眼镜则支持不好
- dst有眼镜需要手动调整区域