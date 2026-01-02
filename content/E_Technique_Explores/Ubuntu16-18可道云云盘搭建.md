---
title: Ubuntu16/18可道云云盘搭建
date: 2020-08-06 00:05:30
tags:
  - Cloud
cover: https://user-images.githubusercontent.com/60562661/73954603-02618680-493d-11ea-9ebd-b33ee3002b8e.png
---
> [[从0开始搭建私人云盘]]


实验室有自己有一台主机闲置，想着闲置太浪费，但是一直不会用。所以就把这个主机当成一个web服务器😝，这个主机系统是**Ubuntu18.04**， **Ubuntu16.04也已经测试**。



### 安装 apache2

```shell
// 下载安装
sudo apt-get update
sudo apt-get install apache2
// 防火墙
sudo ufw allow 'Apache Full'
//启动
sudo ufw enable
```

Apache2服务启动后，可以输入本机ip看到对应的页面表示安装成功。

参考链接：https://www.cnblogs.com/lfri/p/10522392.html

### 安装mysql和php

```shell
 sudo apt-get install php-mysql
 sudo apt-get install phpmyadmin
```

### 安装可道云

下载可道云源码，解压到：

```shell
/var/www/html/cloud
```

就可以通过ip来访问：**10.21.7.216/cloud**

![](https://user-images.githubusercontent.com/60562661/89437771-94c2d580-d77a-11ea-83c1-ff81522c5fdd.png)