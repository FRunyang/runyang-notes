---
title: hexo_blog搭建2-主题相关
date: 2020-02-09 23:19:52
tags:
  - blog
cover: https://user-images.githubusercontent.com/60562661/74105856-93826880-4b9c-11ea-8629-4b1b724d54f4.png
---
*博客系列教程
[[拥有自己优雅的图床]]
[[MyBlog-Hexo快速搭建]]
[[hexo-blog搭建2-主题相关]]
[[hugo_blog搭建部署笔记]]



我的这个版本博客是基于Hexo搭建的，主题采用的是 <a href="https://jerryc.me/posts/21cfbf15/#">Butterfly</a>，在这个网址有详细的安装配置教程。 这个主题我非非常喜欢，看了很多的主题就相中了这款。然而配置也是花了我整整一天，可能还算是比较顺利把！配置过程中有的地方安装文档讲的不是很详细，我自己也踩坑了，来记录一下！

 ![](https://user-images.githubusercontent.com/60562661/74105856-93826880-4b9c-11ea-8629-4b1b724d54f4.png)





## 添加 Gallery（相册）

### 新建页面

```bash
hexo new page gallery #此时会在source目录下产生gallery/index.md
```

打开来编辑这个md文件，有两点要注意的：

- 开头的 **type: "gallery"**   不能出错
- 内容格式 按照  **{% gallery %}  img1  img2  img3 {% endgallery %}**    来写

![](https://user-images.githubusercontent.com/60562661/74105571-12c26d00-4b9a-11ea-8e58-9cb4520896fd.png)

### 添加导航栏

在 butterfly.yml 文件的menu下照着之前的添加相册，如下图

![](https://user-images.githubusercontent.com/60562661/74105539-d5f67600-4b99-11ea-83f1-f856a034b9b3.png)

至此，相册添加结束



## 添加本地搜索

### 安装hexo本地搜索的插件

```bash
npm install hexo-generator-searchdb --save
```

### 配置全局的config文件

![](https://user-images.githubusercontent.com/60562661/74105544-da229380-4b99-11ea-8ba8-7715f23704b9.png)

### 配置butterfly文件

这里的配置和官方教程一样，不再赘述

### 踩坑

我自己在这里一直配置不好，刚开始发现是找不到 search.xml 文件，后来我在博客插件目录找到了，然后改上图的path，这样在本地启动blog是可以搜索的，但是推送到远程就不行了，后面我重装了插件，path改成默认路径,然后 `hexo clean`  `hexo g` `hexo d`  就很神奇的在github仓库生成了search.xml文件，也就随之可以用了，具体原理我还没搞明白，以后明白了再更新。



## 添加评论

我用的是 Valine 评论系统，这个很容易搭建起来，大致描述一下流程：

### 配置 valine

1. 注册 https://www.leancloud.cn/ 在这个网站注册账号，然后进行实名认证

2. 创建一个应用

3. 进入设置页面，在应用keys中可以看到自己的 **AppID** **AppKey**   等会儿会用到

4. **在安全中心页面 web安全域名写入自己的博客域名**（这一步很重要，我就是一开始在这里栽了）

   **至此，valine配置结束**

### 配置主题文件

这里的流程和官方教程一样，很容易，自己直接会明白

**我在这里卡住是因为写 APPID APPKey出了问题，卡了很久才发现**

然后重新更新生成就有了评论功能！