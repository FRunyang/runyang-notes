---
title: git错误与代理相关
date: 2020-06-06 10:21:40
tags: ["git"]
categories: ["技术","Git"]
cover: https://user-images.githubusercontent.com/60562661/73609075-07ed6280-4605-11ea-9971-35fe0663a9e0.jpg
---
*git相关
[[git推送文件]]
[[git错误与代理相关]]


前一篇文章，我写到了git代理设置相关的东西,实际上应该根据自己的vpn选择开哪一种代理。`ssr`用sock5代理是可以的，但是`clash`就行不通，需要把git代理取消，然后设置成http代理。

代理的端口号要根据vpn来设置，并不是通用的。

我自己的git突然不能用，错误大致如下：

`OpenSSL......Error443`

解决如下：

```bash
git config --global --unset http.proxy
git config --global --unset https.proxy

#设置 http代理
git config --global https.proxy http://127.0.0.1:根据vpn选择端口号

git config --global https.proxy https://127.0.0.1:根据vpn选择端口号
```

---

`Error 403  request denail`

该错误表示登录错了账号，拒绝推送，我自己也是记混了git账号，所以出现了这个问题。

---

另外，安利一款梯子：`Clash`

- 自动选择节点
- 界面舒适