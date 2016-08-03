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
- [x] Volley


<!--more-->
## ButterKnife注解

**网址**： https://github.com/JakeWharton/butterknife

**注意**：如果想要在lib/app中使用Butterknife库，则需要在当前module的build.gradle中添加compile信息;
如果你在lib库的build.gradle中引用了Butterknife的compile信息，
然后想要在app中直接使用Butterknife，这样的结果是注解失败；就会出现NullpointException;
`https://www.google.com/search?q=NullPointerException+butterknife`

**AS插件**：Android Butterknife Zelezny
在使用的时候，注意，把光标放置在`R.layout.layout_other`上面，点击`Alt+Insert`，选择`Generate ButterKnife Injections`；


## Volley
### 步骤
- 依据application上下文，初始化volley组件；
- 配置参数和请求数据；
- 添加到请求队列；
- 结果处理；

### 注意
一般情况下，用get和post两种请求方式；
post请求使用：StringRequest对象；
get请求使用：JsonObjectRequest对象；

### 外部链接
- [android-volley](https://github.com/mcxiaoke/android-volley)
- [Android库Volley的使用介绍](http://bxbxbai.github.io/2014/09/14/android-working-with-volley/)