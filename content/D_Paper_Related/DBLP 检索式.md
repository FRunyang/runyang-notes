---
date: 2024-03-22T21:27:00
aliases:
  - dblp
---


> 批量搜索指定期刊、日期、关键词的论文

**经常可以使用的匹配方法有：标题，作者，期刊（或会议）名称，年份，其对应的检索词分别为：title，author，venue和year。**

如果某项关键字可能包含多个单词的时候，包括下列情况：

1、默认单词用空格间隔，表示单词同时出现，但是顺序无关，也可以使用下划线_分隔单词，如：

```
title:voting_election	
title:voting election	
```

2、如果需要表达或的关系，可以使用|分隔单词，如：

```
author:zhang|wang	
```

3、如果需要单词精确匹配，可以在词尾添加$，如：

```
graph$
```

4、组合检索

```
title:verifiable_privacy_voting year:2019 venue:comput author:zhang_thomas
```

检索目标 题目包含三个单词：verfifiable, privacy和voting；文献属于2019年；期刊或会议名称包含comput单词（需要注意，有些期刊和会议使用了简称，所以事先最好搞清楚目标期刊在dblp的简称是什么）；作者包括了zhang和thomas两个单词