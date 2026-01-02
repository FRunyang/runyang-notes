---
title: Git常用操作整合
date: 2020-02-02T20:31:30+08:00
tags:
  - git
cover: https://user-images.githubusercontent.com/60562661/73609075-07ed6280-4605-11ea-9971-35fe0663a9e0.jpg
---

*git相关
[[git推送文件]]
[[git错误与代理相关]]

github远程托管文件 非常的方便。git操作种比较多的就是本地文件推送到远程，仓库等。而我一直也是没有搞明白，github本地文件远程推送是如何操作的，以至于今天卡了很久，来记录一下。



![git](https://user-images.githubusercontent.com/60562661/73609075-07ed6280-4605-11ea-9971-35fe0663a9e0.jpg)

## git推送本地文件

### 一般流程

**Note **:  默认远程仓库是空的

```bash
# 1.新建远程仓库 ，这个可以自己去查阅，很容易

# 2.把本地需要推送的文件夹设置为git仓库
git init

# 3.添加文件
git add .

# 4.提交文件
git commit -m 'first_commit'

# 5.添加镜像源
git remote add origin https://github.com/fryddup/fryddup.github.io.git

# 6.推送文件
git push -u origin master
```



### 同步问题

以上代码即可实现本地文件推送到远程，但是注意当仓库不是空的，仓库有改动，应当如下操作：

```bash
git add .

git commit -m 'first_commit'

git pull  #注意，此命令即是远程文件同步到本地。

git push -u origin master
```



## git 代理相关

### 设置代理

```bash
git config --global http.proxy 'socks5://127.0.0.1:1080' 
git config --global https.proxy 'socks5://127.0.0.1:1080'
```



### 查看代理

```bash
git config --global --get http.proxy
git config --global --get https.proxy
```



### 取消代理

```bash
git config --global --unset http.proxy
git config --global --unset https.proxy
```



## 踩坑

新建仓库，新建`README.md`，本地 add，commit 之后，push遇到了如下错误：

```bash
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'https://github.com/tzwx/DeepLearning.git'
```

1. `git pull origin master --allow-unrelated-histories //把远程仓库和本地同步，消除差异`
2. `git push -u origin master`



git其他操作、问题以后遇到了再补充**

