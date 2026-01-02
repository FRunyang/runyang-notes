---
title: 计算机网络-IP地址&端口
date: 2020-08-23 23:59:52
tags:
  - 计算机网络
cover: https://xvp.imgix.net/assets/og/customer_tools/ip_checker-05b5b63c1a0d003d8cf209ec3f489fa7b96d15b8550250eb76aba6ec9092216f.jpg
---

## IP 地址

ip地址作为计算机的唯一标识符，每个计算机有唯一的IP地址。

**IPV4** 用 **32位(bit)**表示ip地址，也就是**4字节（byte）**.

为了便于表示，用 **a.b.c.d** 表示。每个二进制都为8bit，十进制为**0~255**.  
$$
2^8=255
$$

```python
 127.0.0.1 //本机ip
 localhost//本机
```

根据最高位地址划分为ABCDE类。

**IPV6** 用  8 组，每组16位（bit）表示ip地址，一共128位



## 端口号

端口号是计算机之间通信时，每个通信软件有固定的端口号。例如qq，不同计算机上qq的端口号相同，消息才得以互通。

长度16位，**0~65535**

1000以下已经分配。

```python
80 为www服务端口
3306 mysql服务端口
8080 www代理服务
127.0.0.1 //本机ip
localhost//本机
```

