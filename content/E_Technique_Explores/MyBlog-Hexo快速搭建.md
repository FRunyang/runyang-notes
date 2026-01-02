---
title: Hexo_blog搭建部署笔记
date: 2020-02-05T20:32:27+08:00
tags:
  - blog
cover: https://user-images.githubusercontent.com/60562661/74099115-239fbe00-4b5b-11ea-8dbf-aa50c6e7568c.png
---

*博客系列教程
[[拥有自己优雅的图床]]
[[MyBlog-Hexo快速搭建]]
[[hexo-blog搭建2-主题相关]]
[[hugo_blog搭建部署笔记]]


## 安装环境

**NodeJS** + **hexo** + **git**, 这三个安装教程可以自行百度到，很多博客里也有，这里便不再赘述



## 搭建博客

### 初始化

```bash
hexo init
```

### 写一篇新博客

```bash
hexo new "helloworld" #此时在source/_posts下会生成文章
```

### 运行测试

```bash
hexo s 
```

**此时基本搭建完成**



## 部署到github

### 安装deploy插件

```bash
npm install --save hexo-deployer-git
```

### 新建github仓库

这步比较简单，可以自己查查如何新建

### 修改全局配置文件  _config.yml：

```yml
deploy:
  type: git
  repo: https://github.com/fryddup/fryddup.github.io.git #自己的仓库地址
  branch: master
```

### 推到远程服务器

```bash
hexo -d
```

此时可以通过 https://huaqi.blue 来访问我的博客

---

## 注意

每次写完博客 hexo clean  hexo g 两步必不可少，然后在 hexo d

![](C:\Users\33196\Desktop\0.png)