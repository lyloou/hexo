---
title: cordova的坑
date: 2016.12.29 16:40
toc: true
comments: true
tags:
- cordova
---

运行环境
```
java: jdk1.8
cordova: 6.4.0

```

通过`cordova build android`的方式自动编译打包程序时，
Manifest文件会被重新生成。

我给第一个Activity设置了屏幕不反旋转的属性`android:screenOrientation="portrait"`，但是自动生成的过程中，总会将这行代码自动删除了。

解决办法是：找一个不含该属性的Activity放在第一个位置。

