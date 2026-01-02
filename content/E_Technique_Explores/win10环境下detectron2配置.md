---
date: 2020-02-18 21:41:17
tags:
  - 环境
cover: https://user-images.githubusercontent.com/60562661/74744265-eba42380-529c-11ea-930b-dbccc853bcd8.jpg
---



最强目标检测平台Detectron2 ，基于PyTorch完全重构，windows上很不友好，很难配置，配置好就算装好这个库依然不能使用`nms`,回头再想办法解决。安装过程曲折，记录一哈。

<img src="https://user-images.githubusercontent.com/60562661/74744277-ee067d80-529c-11ea-8e3c-40dbae5c9348.jpg" style="zoom:50%;" />

http://www.luyixian.cn/news_show_240401.aspx我主要参考的这个链接

https://github.com/conansherry/detectron2 这个链接在我踩坑也不可或缺

我自己电脑是cuda9.0,cudnn7,上面第二个链接要墙置换成cuda10，很难搞，所以我就按第一个来



## 安装依赖

依赖的库：`pytorch1.3` `opencv`  `pycocotools`  `fvcore`，其中最后两个安装不同于以往，这里提一下。

`pip install git+https://github.com/facebookresearch/fvcore`

`pip install 'git+https://github.com/cocodataset/cocoapi.git#subdirectory=PythonAPI'`

其中，pycocotools安装很是麻烦，这个命令可能不会成功，所以需要自己探索一下，装不好可以评论留言找我要。

## 确认gcc>=4.9

`gcc --version`

## 修改lib文件

```bat
file1: 
  {your evn path}\Lib\site-packages\torch\include\torch\csrc\jit\argument_spec.h
  example:
  {C:\Miniconda3\envs\py36}\Lib\site-packages\torch\include\torch\csrc\jit\argument_spec.h(190)
    static constexpr size_t DEPTH_LIMIT = 128;
      change to -->
    static const size_t DEPTH_LIMIT = 128;
file2: 
  {your evn path}\Lib\site-packages\torch\include\pybind11\cast.h
  example:
  {C:\Miniconda3\envs\py36}\Lib\site-packages\torch\include\pybind11\cast.h(1449)
    explicit operator type&() { return *(this->value); }
      change to -->
    explicit operator type&() { return *((type*)this->value); }
```

## 克隆检测器并安装

```python
git clone https://github.com/facebookresearch/detectron2.git
cd detectron2
python setup.py build develop
```

这期间提示缺少什么 就补什么就行。

至此安装完成，`pip list` 可以看到 `detectron2` 这个包

## 踩坑

按着第一个链接教程搞，编译一直出错，各种莫名其妙的错误，编译不成功；然后我按照第二个教程修改了文件，就成功安装了。

不同电脑环境不同，可能是环境问题导致。这个可能也只适用于我自己的电脑。

