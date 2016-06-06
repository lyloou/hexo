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




## TextView
### 字符串资源里的变量替换
在xml中定位占位符（其中`1`表示第一个变量，多个变量递增表示）
```
<!-- values/strings.xml -->
<string name="replace_str">你好，%1$s：欢迎您！</string>
```

java代码中动态指定`%1$s`处的值
```
String str = getString(R.string.replace_str, "小明");
```

### 使用HTML格式化文本
```
textView.setText(Html.fromHtml(HTML_STR));
```
### 外部链接
- [TextView实战之你真的懂我么？](http://blog.csdn.net/sdkfjksf/article/details/51317204)










---

## EditText
### 定位光标位置：
```
String name = "Lou";
EditText et = (EditText)findViewById(R.id.et_name);
et.setSelection(name.length()); // 将光标至于文字最后
```

### 使光标颜色和文字颜色保持一致（EditText不显示光标问题）：
```
<!-- 有的时候发现EditText里的光标无法显示的问题，很可能是光标的颜色和背景重合了，可以通过设置光标的颜色属性来让其显示 -->
<!-- 在EditText标签中添加如下属性 -->
android:textCursorDrawable="@null"
```

### 外部链接
- [修改EditText的光标颜色](http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2013/0216/858.html)
- [Set EditText cursor color](http://stackoverflow.com/questions/7238450/set-edittext-cursor-color)


---
## ListView
ListView中不可见的元素，其对应的view为null。这是容易理解的，性能优化。
（在updateItem的时候要做两方面的处理，即数据(updateItemData)和视图(updateItemView)）

