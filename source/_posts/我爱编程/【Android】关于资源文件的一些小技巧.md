---
title: 【Android】关于资源文件的一些小技巧
date: 2016-06-?? 08:59:00
categories:
- 我爱编程
tags:
- Android
- string

---

## 摘要：
主要内容：
本文介绍了资源文件中的一些使用技巧。

任务列表：
- [ ]


<!--more-->
## 说明
- 所有的资源文件，都可以放在同一个`<resources>`标签下面，例如：`color`、`declare-styleable`、`dimen`、`integer`、`item`
、`string`、`style`。


## string标签
使用`translatable="false"`标签可以让内容直接嵌入到引用的地方，而不做翻译处理。
 * 举例来说，下面的用法就可以将`android.support.design.widget.AppBarLayout$ScrollingViewBehavior`直接嵌入到了`ScrollView`。

 ``` xml
 <ScrollView
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    app:layout_behavior="@string/appbar_scrolling_view_behavior">
 ```

 ``` xml
 <string name="appbar_scrolling_view_behavior" translatable="false">android.support.design.widget.AppBarLayout$ScrollingViewBehavior</string>
 ```

- 另一种方案：
> It's the ignore attribute of the tools namespace in your strings file, as follows:
``` xml
<?xml version="1.0" encoding="utf-8"?>
<resources
  xmlns:tools="http://schemas.android.com/tools"
  tools:ignore="MissingTranslation" >
  <!-- your strings here; no need now for the translatable attribute -->
</resources>
```

### 使用场合
不希望字符串被翻译。

### 外部链接
- [Non-translatable Strings](http://tools.android.com/recent/non-translatablestrings)
- [What is the purpose of using translatable in Android strings?](http://stackoverflow.com/questions/3925072/what-is-the-purpose-of-using-translatable-in-android-strings/13688979)
- [Avoid Android Lint complains about not-translated string](http://stackoverflow.com/questions/12590739/avoid-android-lint-complains-about-not-translated-string)
> If you don't want a string to be translated, you should only define it in the "base values/folder", which means do not enter the string in the translated values/folder.
