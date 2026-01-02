---
title: python-库-you-get下载视频
date: 2020-07-04 23:37:11
tags:
  - python库
cover: https://user-images.githubusercontent.com/60562661/86516565-3f7e6600-be54-11ea-9520-006bd3deedf0.jpg
---

You-get 是一个可以下载很多在线视频的使用的Python库，我最近主要利用这个库来下载bilibili的视频，下面做一些使用的简单记录。

## 基本使用

### 安装

和其他python库安装相同，直接使用pip即可。

```python
activate deep  # 激活当前环境
pip install you-get  # 安装you-get库
```

### 使用

1. 分析视频信息

```python
you-get -i url # url 为视频链接地址

# for example
you-get -i you-get -i https://www.bilibili.com/video/BV1ST4y1E7FW?from=search&seid=13389194302262225891
'''
输出信息：
site:                Bilibili
title:               【4k60帧】真正的奥利给，“后浪风”演讲——看见的力量
streams:             # Available quality and codecs
    [ DASH ] ____________________________________
    - format:        dash-flv
      container:     mp4
      quality:       高清 1080P
      size:          46.7 MiB (48993131 bytes)
    # download-with: you-get --format=dash-flv [URL]

    - format:        dash-flv720
      container:     mp4
      quality:       高清 720P
      size:          32.3 MiB (33909997 bytes)
    # download-with: you-get --format=dash-flv720 [URL]

    - format:        dash-flv480
      container:     mp4
      quality:       清晰 480P
      size:          16.4 MiB (17216475 bytes)
    # download-with: you-get --format=dash-flv480 [URL]

    - format:        dash-flv360
      container:     mp4
      quality:       流畅 360P
      size:          11.4 MiB (11943322 bytes)
    # download-with: you-get --format=dash-flv360 [URL]

    [ DEFAULT ] _________________________________
    - format:        flv
      container:     flv
      quality:       高清 1080P
      size:          75.9 MiB (79590049 bytes)
    # download-with: you-get --format=flv [URL]

    - format:        flv720
      container:     flv
      quality:       高清 720P
      size:          51.8 MiB (54269960 bytes)
    # download-with: you-get --format=flv720 [URL]

    - format:        flv480
      container:     flv
      quality:       清晰 480P
      size:          25.2 MiB (26397350 bytes)
    # download-with: you-get --format=flv480 [URL]

    - format:        flv360
      container:     flv
      quality:       流畅 360P
      size:          11.5 MiB (12080563 bytes)
    # download-with: you-get --format=flv360 [URL]

'seid' 不是内部或外部命令，也不是可运行的程序
或批处理文件。

'''
    
```



2. 下载视频

```python
# download
you-get https://www.bilibili.com/video/BV1ST4y1E7FW?\from=search&seid=13389194302262225891

# 指定路径 -o
you-get  -o z:/video https://www.bilibili.com/video/BV1ST4y1E7FW?\from=search&seid=13389194302262225891

# 指定分辨率 -format

you-get -format==flv720 https://www.bilibili.com/video/BV1ST4y1E7FW?\from=search&seid=13389194302262225891
```

## 注意的问题

我是`win10 Home`版系统，会遇到问题：

**'seid' 不是内部或外部命令，也不是可运行的程序或批处理文件。**

**解决方案：**

将 `&seid=` 替换为`3D` 即可

一条完整的下载视频命令：

```python
you-get  -o z:/video -format==flv720 https://www.bilibili.com/video/BV1ST4y1E7FW?\from=search&seid=13389194302262225891
```

