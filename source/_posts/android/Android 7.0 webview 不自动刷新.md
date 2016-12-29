---
title: Android 7.0 webview 不自动刷新
date: 2016.12.29 16:38
toc: true
comments: true
tags:
- android
---

当webview所在的activity采用了以下主题时，Android7.0设备将无法正常运行：
``` xml
    <style name="WelcomeBg" parent="@android:style/Theme.DeviceDefault.NoActionBar">
        <item name="android:windowIsTranslucent">false</item>
        <item name="android:windowNoTitle">true</item>
        <item name="android:windowActionBar">false</item>
        <item name="android:windowBackground">@null</item>
    </style>
```

之所以有这样的改变，目的是想要提升启动Activity的性能，哪里知道7.0之后会遇到无法正常渲染WebView的问题。


解决办法是：
直接使用默认主题，而不再对其包装：
``` xml
@android:style/Theme.DeviceDefault.NoActionBar
```

