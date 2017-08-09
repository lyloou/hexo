---
title: cordova相关
date: 2016.12.29 16:40
toc: true
comments: true
tags:
- cordova
---

## 一个坑
运行环境
```
java: jdk1.8
cordova: 6.4.0
```

通过`cordova build android`的方式自动编译打包程序时，
Manifest文件会被重新生成。

我给第一个Activity设置了屏幕不反旋转的属性`android:screenOrientation="portrait"`，但是自动生成的过程中，总会将这行代码自动删除了。

解决办法是：找一个不含该属性的Activity放在第一个位置。

## cordova 后台切换到前台触发back返回按键
问题描述：  
现在app处在前台，这时候来了一个qq消息或者微信消息，点击通知后再次回来app的时候，会触发返回按键
这样就有可能会莫名其妙地将之前的编辑操作给毁掉了。

解决办法：  
思路是这样的，当离开app的时候，设置一个标志表示现在处于后台了，
当再次返回来的时候，先检测之前的标志是否在后台，如果是，则不处理返回按键的逻辑；
如果不是，则正常执行返回按键的逻辑。

```js
var isAppInFront = true;

document.addEventListener('pause', function(){
    isAppInFront = false;
}, false);

document.addEventListener('resume', function(){
    setTimeout(function(){
        isAppInFront = true;
    }, 200) // 注意需要延时，否则拿到的标志一直是true
}, false);

document.addEventListener('backbutton', function(){
    // 程序不在前台运行，不响应
    if(!isAppInFront) return;

    // 其他点按返回按键的逻辑
}
```
参考资料：  
- [javascript - how to check app running in foreground or background in ionic/cordova/phonegap - Stack Overflow](https://stackoverflow.com/questions/29606012/how-to-check-app-running-in-foreground-or-background-in-ionic-cordova-phonegap)

## 常用命令
卸载 cordova: `npm uninstall -g cordova`
安装 cordova: `npm install -g cordova`
安装指定版本 cordova: `npm install -g cordova@6.4.0`
