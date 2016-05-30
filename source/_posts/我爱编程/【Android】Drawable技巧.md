---
title: 【Android】Drawable技巧
date: 2016-05-30 08:59:00
categories:
- 我爱编程
tags:
- Android
- Drawable
---

## 摘要：
主要内容：
本文介绍了我使用Drawable的个人经验总结。

任务列表：
- [ ]


<!--more-->

## 让Selector中的图片居右对齐
抛出问题：
实现如图的效果和功能，当选中时后面有一个对勾，当非选中时没有对勾，点击「发送」的时候给所有选中的item发送消息。
![让Selector中的图片居右对齐](/images/20160530/drawable_01.jpg "让Selector中的图片居右对齐");

复杂的做法是：
通过自定义一个实体类，每个对象都有一个名称属性和一个表示是否是选中状态属性；
给ListView设置item监听，点击item的时候，改变其状态然后刷新列表 ……

简单的做法：
因为这里只是为了获取到所有选中的item，并没有其他的功能需求，我们可以充分利用ListView的choice功能，
（即通过设置ListView的多选模式`android:choiceMode="multipleChoice"`）；

为了使用简单的做法，我们可能会遇到这样的问题：在哪里设置选中和没选中两种状态；
解决办法就是给item的根布局设置selector，根据是否处于激活状态来区分；

```
<!-- layout/item_lv-->
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:background="@drawable/llyt_bg_selector"
    android:orientation="vertical"
    android:paddingBottom="8dp"
    android:paddingTop="8dp" >
    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="浩南"/>
</LinearLayout>
```

如何让selector中的图片居右对齐：
简单来说，就是利用bitmap标签的gravity属性和titleMode属性来控制。
```
<!-- drawable/llyt_bg_selector.xml -->
<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:state_activated="true">
        <bitmap android:src="@drawable/img_checked"
            android:tileMode="disabled"
            android:dither="true"
            android:antialias="true"
            android:gravity="end|center_vertical"/>
    </item>
</selector>
```

如何获取所有选中的条目：
```
SparseBooleanArray sba = listView.getCheckedItemPositions();
ArrayList<Friend> checkedLists = new ArrayList<>();

for (int i = 0; i < friendAdapter.getCount(); i++) {
    if (sba.get(i)) {
        checkedLists.add(adapter.getItem(i));
    }
}
Log.e("Lou", "Get checked items :" + checkedLists);
```


还有一种思路：
通过「点9」图来实现让图片居右对齐的目的；

外部链接：
- [Explanation of state_activated, state_selected, state_pressed, state_focused for ListView](http://stackoverflow.com/questions/13634259/explanation-of-state-activated-state-selected-state-pressed-state-focused-for)


## 背景图片平铺
```
<?xml version="1.0" encoding="utf-8"?>
<bitmap xmlns:android="http://schemas.android.com/apk/res/android"
    android:src="@drawable/stripes"
    android:tileMode="repeat" />
```

## 推荐教程
- [KStyle是一个Android的样式开发的学习项目。](https://github.com/keeganlee/kstyle)