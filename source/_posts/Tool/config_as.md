---
title: 【Tool】Android Studio配置
date: 2016-05-26 17:16:15
categories:
- Tool
tags:
- AS
---


## 摘要：
主要内容：
本文介绍了个人的Android Studio配置，包括主题、插件等；

<!--more-->

## 用途
- 编写Android代码；
- 写hexo上的文章；

## 我的AS配置
- [setting.jar](https://github.com/lyloou/lou/tree/master/tools)

## 快捷键
- **!j**
> 25. Sublime Text式的多处选择（Sublime Text Multi Selection）
>  描述：这个功能超级赞！该操作会识别当前选中字符串，选择下一个同样的字符串，并且添加一个光标。这意味着你可以在同一个文件里拥有多个光标，你可以同时在所有光标处输入任何东西。
>  快捷键：Ctrl + G(OS X)、Alt + Ｊ（Windows、Linux）

- **!+insert**
> 29. 列选择/块选择（Column Selection）
> 描述：正常选择时，当你向下选择时，会直接将当前行到行尾都选中，而块选择模式下，则是根据鼠标选中的矩形区域来选择。
> 调用：按住Alt，然后拖动鼠标选择。
> 开启/关闭块选择：Menu → Edit → Column Selection Mode
> 快捷键：切换块选择模式：Cmd + Shift + 8(OS X)、Shift + Alt + Insert﻿(Windows/Linux);

- **!q** 上下文信息；
- **^!m** 提取方法；
- **^!p** 提取参数（window快捷键冲突）；
- **^!n** 内置(inline)，提取的反操作；
- **^+j** 合并行和文本；
- **^!t** 包裹代码（Surround With）；
- **^+delete** 移除包裹代码（包裹代码的反操作）；



## Theme
- Darcula + Sublime Text 2

## Plugin
- .ignore
- Markdown support

## 提升Gradle编译速度
- 设置代理
``` gradle
# gradle.properties中添加
# 举例ShadowSocket
systemProp.http.proxyHost=127.0.0.1
systemProp.http.proxyPort=1080
systemProp.https.proxyHost=127.0.0.1
systemProp.https.proxyPort=1080
```
- 设置中启用离线状态
- 启用守护进程
``` gradle
# gradle.properties中添加
org.gradle.jvmargs=-Xmx2048m -XX:MaxPermSize=512m -XX:+HeapDumpOnOutOfMemoryError -Dfile.encoding=UTF-8
org.gradle.parallel=true
org.gradle.daemon=true
```
- 编译SDK使用21以上

### 外部链接
- [知道Android 中Gradle 的这些技巧，提升编译构建速度](http://tikitoo.github.io/2016/05/26/android-studio-gradle-build-run-faster/)
- [Android Studio 小技巧合集](http://jaeger.itscoder.com/android/2016/02/14/android-studio-tips.html)