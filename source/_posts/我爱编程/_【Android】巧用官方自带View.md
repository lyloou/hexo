---
title: 【Android】巧用官方自带View
date: 2016-05-27 10:54:32
categories:
- 我爱编程
tags:
- Android
- View
---

## 摘要：
主要内容：


任务列表：
- [ ] TextView
- [x] EditText


<!--more-->

## EditText
定位光标位置：
```
String name = "Lou";
EditText et = (EditText)findViewById(R.id.et_name);
et.setSelection(name.length()); // 将光标至于文字最后
```

使光标颜色和文字颜色保持一致（EditText不显示光标问题）：
```
<!-- 有的时候发现EditText里的光标无法显示的问题，很可能是光标的颜色和背景重合了，可以通过设置光标的颜色属性来让其显示 -->
<!-- 在EditText标签中添加如下属性 -->
android:textCursorDrawable="@null"
```


## 外部链接
- [修改EditText的光标颜色](http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2013/0216/858.html)
- [Set EditText cursor color](http://stackoverflow.com/questions/7238450/set-edittext-cursor-color)