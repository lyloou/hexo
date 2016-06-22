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

### 跑马灯效果不生效
需要在代码中设置`tv.setSelected(true)`
> [TextView Marquee not working](http://stackoverflow.com/questions/3332924/textview-marquee-not-working)


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

### 添加空白
- 在ListView的顶部和底部添加空白（见外部链接）
- 在Item之间添加空白（通过Divider的方式）

#### 代码
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/alarm_bg"
    android:orientation="vertical">

    <ListView
        android:id="@+id/lv_main"
        android:layout_width="match_parent"
        android:layout_height="match_parent"

        android:paddingTop="16dp"
        android:paddingBottom="16dp"
        android:clipToPadding="false"

        android:scrollbars="none"
        android:divider="@android:color/transparent"
        android:dividerHeight="10dp"
        />
</LinearLayout>
```

#### 外部链接
- [Add margin above top ListView item (and below last) in Android](http://stackoverflow.com/questions/6288167/add-margin-above-top-listview-item-and-below-last-in-android)
- [Spacing between listView Items Android](http://stackoverflow.com/questions/4984313/spacing-between-listview-items-android)