---
title: 自己的域名与github绑定
date: 2020-02-07T00:07:21+08:00
tags:
  - Website
  - blog
cover: https://user-images.githubusercontent.com/60562661/73957566-7ef66400-4941-11ea-87ee-e9c53fdbc305.png
---

*博客系列教程
[[拥有自己优雅的图床]]
[[MyBlog-Hexo快速搭建]]
[[hexo-blog搭建2-主题相关]]
[[hugo_blog搭建部署笔记]]




一般情况下用github托管的博客很方便，但是域名访问只能用 https://xxxx.github.io来访问，这时候就有与自己的域名绑定的问题，即自己的域名指向github地址。（以腾讯云为例）

![](https://user-images.githubusercontent.com/60562661/73957566-7ef66400-4941-11ea-87ee-e9c53fdbc305.png)



## 准备工作

开始操作前，确保自己已经有：

- **可用**的域名：注意不需要备案（我的是这样），但是大多数需要实名认证
- 有自己的**github**项目地址，确保可以访问



## 域名解析

进入腾讯云控制台，在自己的域名解析处设置如下：

![](https://user-images.githubusercontent.com/60562661/73957562-7dc53700-4941-11ea-81f5-472730958808.png)

这里要注意两点：

- 记录类型选择 **CNAME**
- 记录值为自己的github项目地址（**github域名**）

此时如果解析成功，**ping**一下测试：

![](https://user-images.githubusercontent.com/60562661/73957564-7e5dcd80-4941-11ea-93c1-501060db97b2.png)



## github仓库设置

进入github项目仓库设置，往下翻在 Github Page 中自定义地址写自己的域名 然后保存，此时主页会自动生成 CNAME 文件，如下图：

![](https://user-images.githubusercontent.com/60562661/73957559-7c940a00-4941-11ea-8f4c-b56ac851d659.png)

## 注意

### 等待时间

等待10-15min，就可以通过自己的域名来访问了。注意能ping通说明已经成功，此时就不要频繁修改设置了，影响同步 时间

### 普适性

以上流程在hugo博客上毫无问题，原因是hugo博客推送到服务器是推送public中的内容，而CNAME在根目录并不会影响；

但是在hexo博客上就有问题了，我查了一下发现如果直接在gtihub直接指定，会在github仓库上直接生成CNAME文件，而这时候有个问题就是在写文章同步的话，本地并没有CNAME文件，会直接覆盖掉已经生成的CNAME 文件，此时指定的域名就不生效了。因此有了以下的章节。



## Hexo博客绑定域名

首先在本地 博客根目录中source文件夹下新建一个CNAME文件，内容就是自己的域名，然后再按照上面去github指定。