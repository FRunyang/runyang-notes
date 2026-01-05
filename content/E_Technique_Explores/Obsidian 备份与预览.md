---
tags:
  - blog
  - 备份
date: 2026-01-05T20:30:00
---
> Obsidian 笔记方便预览与备份的方法

##  关于笔记备份，可以使用Github进行备份。 
 
##  但是笔记预览，用网页端浏览，可以用quartz 库进行。

其基本流程如下：
###  初始化 Quartz

- `git clone https://github.com/jackyzha0/quartz.git my-notes cd my-notes npm install`

 - 把 Obsidian 笔记 放进 content 目录下


- 本地预览  `npx quartz build --serve`

浏览器打开：`http://localhost:8080`

之后可以挂到 Github，用 Github Pgae 看

## 常用命令

npx quartz build

yrunyangfeng@YRunyangdeMacBook-Pro quartz-site %

rsync -av --delete \

/Users/yrunyangfeng/Documents/Konwledge/ \

./content/