---
title: adb相关
date: 2017-08-14 15:56:55
tags:
- android
---

## 判断当前界面的所属 activity
```sh
adb shell dumpsys activity # 加上 -h 可以获取帮助信息
adb shell dumpsys activity top
adb shell dumpsys activity top | findstr ACTIVITY
```
- [移动测试基础 android 中 dumpsys 命令使用](https://testerhome.com/topics/1462)


## 启动程序
```sh
adb shell am start -n com.tencent.mm/.ui.LauncherUI
```

## 停止程序
```sh
adb shell am force-stop com.tencent.mm
```
