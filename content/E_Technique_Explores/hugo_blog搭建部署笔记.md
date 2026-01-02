---
title: Hugo_blog搭建部署笔记
date: 2020-02-02T20:32:27+08:00
tags:
  - blog
cover: https://user-images.githubusercontent.com/60562661/73609078-10459d80-4605-11ea-93b4-d26fa0f93625.png
---
*博客系列教程
[[拥有自己优雅的图床]]
[[MyBlog-Hexo快速搭建]]
[[hexo-blog搭建2-主题相关]]
[[hugo_blog搭建部署笔记]]





之前一直用的  Hexo Blog ,奈何写出来太丑了，不习惯，部署起来也比较麻烦，就找到了新的好看的，还真的是好看是第一生产力！hugo部署过程如下。



![hugo](https://user-images.githubusercontent.com/60562661/73609078-10459d80-4605-11ea-93b4-d26fa0f93625.png)





## 描述版：

#### 1.安装 hugo （有很多方法，可以到官方网站看一下，我是采用chocolate来安装的）

`choco install hugo`

#### 2.检测go语言是否安装成功

`hugo version`

#### 3.开始建站,建立一个 myblog 站点（博客的根目录）

`hugo new site myblog`

#### 4.安装hugo博客主题 官网 https://themes.gohugo.io/,每个主题有对应的方式，我以我自己的为例,此时目录在博客的根目录

`git clone https://github.com/flysnow-org/maupassant-hugo themes/maupassant`

#### 5.写一篇新博客，位于content/post/

`hugo new post/Hello,world.md`

#### 6.启动本地调试，此时位于根目录

`hugo server --buildDrafts`

#### 7.新建github仓库，这个比较容易，自己解决

#### 8.关联到GitHub,此步骤会生成public文件夹

`hugo --themes=maupassant --baseURL="https://huaqi19.github.io/"`

#### 9.将 public 文件夹内容推送到空的github仓库中

此处步骤省略，如何推送可以参考我的上一篇博客  git推送文件

#### 10.更新博客

`hugo -D`

#### 至此博客搭建完成，主题配置请自行研究



## 代码版：

```bash
# 1.安装 hugo （有很多方法，可以到官方网站看一下，我是采用chocolate来安装的）
choco install hugo

# 2.检测go语言是否安装成功
hugo version

# 3.开始建站,建立一个 myblog 站点（博客的根目录）
hugo new site myblog

# 4.安装hugo博客主题 官网 https://themes.gohugo.io/
# 每个主题有对应的方式，我以我自己的为例
# 此时目录在博客的根目录
git clone https://github.com/flysnow-org/maupassant-hugo themes/maupassant

# 5.写一篇新博客，位于content/post/
hugo new post/Hello,world.md

# 6.启动本地调试，此时位于根目录
hugo server --buildDrafts

# 7.新建github仓库，这个比较容易，自己解决

# 8.关联到GitHub,此步骤会生成public文件夹
hugo --themes=maupassant --baseURL="https://huaqi19.github.io/"

# 9.将 public 文件夹内容推送到空的github仓库中
# 此处步骤省略，如何推送可以参考我的上一篇博客  git推送文件

# 10.更新博客
hugo -D

# 至此博客搭建完成，主题配置请自行研究

```

 