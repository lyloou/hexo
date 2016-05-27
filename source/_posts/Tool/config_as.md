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

## Theme
- Darcula + Sublime Text 2

## Plugin
- .ignore
- IDEA Mind Map
- Markdown support

## 提升Gradle编译速度
- 设置代理
```
# gradle.properties中添加
# 举例ShadowSocket
systemProp.http.proxyHost=127.0.0.1
systemProp.http.proxyPort=1080
systemProp.https.proxyHost=127.0.0.1
systemProp.https.proxyPort=1080
```
- 设置中启用离线状态
- 启用守护进程
```
# gradle.properties中添加
org.gradle.jvmargs=-Xmx2048m -XX:MaxPermSize=512m -XX:+HeapDumpOnOutOfMemoryError -Dfile.encoding=UTF-8
org.gradle.parallel=true
org.gradle.daemon=true
```
- 编译SDK使用21以上

### 外部链接
- [知道Android 中Gradle 的这些技巧，提升编译构建速度](http://tikitoo.github.io/2016/05/26/android-studio-gradle-build-run-faster/)