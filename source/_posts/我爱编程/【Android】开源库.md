---
title: 【Android】开源库
date: 2016-07-21 17:09:58
toc: true
categories:
- 我爱编程
tags:
- Android
---

## 关键字

## 摘要：
> 本文介绍了开源库的相关内容；

任务列表：
- [x] ButterKnife


<!--more-->
## ButterKnife注解

**网址**： https://github.com/JakeWharton/butterknife

**注意**：如果想要在lib/app中使用Butterknife库，则需要在当前module的build.gradle中添加compile信息;
如果你在lib库的build.gradle中引用了Butterknife的compile信息，
然后想要在app中直接使用Butterknife，这样的结果是注解失败；就会出现NullpointException;
`https://www.google.com/search?q=NullPointerException+butterknife`