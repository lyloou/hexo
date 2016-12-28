---
title: Android中巧用官方自带View
date: 2016-05-27 10:54:32
toc: true
tags:
- Android
---

## TextView
### 字符串资源里的变量替换
在xml中定位占位符（其中`1`表示第一个变量，多个变量递增表示）
``` xml
<!-- values/strings.xml -->
<string name="replace_str">你好，%1$s：欢迎您！</string>
```

java代码中动态指定`%1$s`处的值
``` java
String str = getString(R.string.replace_str, "小明");
```

### 使用HTML格式化文本
``` java
textView.setText(Html.fromHtml(HTML_STR));
```

### 跑马灯效果不生效
需要在代码中设置`tv.setSelected(true)`
> [TextView Marquee not working](http://stackoverflow.com/questions/3332924/textview-marquee-not-working)


### 外部链接
- [TextView实战之你真的懂我么？](http://blog.csdn.net/sdkfjksf/article/details/51317204)


## ImageView
### 交叉使用mipmap和drawable
钻牛角尖：先必须获取到之前的Drawable，然后将这个Drawable进行转换，然后进行图片替换；
解决思路：通过覆盖的单向方式，而不用知道之前是图片资源还是Drawable资源。

``` java
ImageView ivMain = findViewById(R.id.iv_main);
if(满足条件){
  ivMain.setBackgroundResource(R.id.selected);
} else {
  ivMain.setBackgroundResource(R.id.unselected);
}
```

### ImageView加载GIF图片
代码
``` java
ImageView iv = (ImageView) findViewById(R.id.vp_iv);
Glide
  .with(this)
  .load("https://i.imgur.com/l9lffwf.gif")
  .into(iv);
```
外部链接
- [Glide](https://github.com/bumptech/glide)

### 加载网络图片
代码
``` java
Picasso
  .with(this)
  .load("https://i.imgur.com/l9lffwf.gif")
  .placeholder(R.mipmap.ic_launcher)
  .into(iv);
```
外部链接
- [Picasso](https://github.com/square/picasso)







---

## EditText
### 定位光标位置：
``` java
String name = "Lou";
EditText et = (EditText)findViewById(R.id.et_name);
et.setSelection(name.length()); // 将光标至于文字最后
```

### 使光标颜色和文字颜色保持一致（EditText不显示光标问题）：
``` xml
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
``` xml
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





---
## 修改DatePicker日期选择器默认样式（同理适用于TimePicker）
### 效果图
![DatePicker](https://github.com/lyloou/hexo/blob/master/source/images/20160706/date_picker.jpg?raw=true)
### 代码
``` xml
<!-- 使用Holo样式 -->
<DatePicker
        android:id="@+id/dialog_personal_birth_dp"
        style="@android:style/Widget.Holo.DatePicker"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>
```

``` java
private String mBirth = "1981.12.11";
final DatePicker dp = dialogBirth.getView(R.id.dialog_personal_birth_dp);
dp.setCalendarViewShown(false); // 不要显示Calendar视图
Uview.changeTimePickerSepColor(dp, Color.DKGRAY); // 修改分割线样式
String[] birth = mBirth.split("\\.");
dp.init(Integer.parseInt(birth[0]),
        Integer.parseInt(birth[1]) - 1,
        Integer.parseInt(birth[2]),
        null);
```

``` java
//: Uview.java
public static void changeTimePickerSepColor(ViewGroup group, int color) {
    for (NumberPicker np : getNumberPickers(group)) {
        changeNumberPickerSepColor(np, color);
    }
}


private static List<NumberPicker> getNumberPickers(ViewGroup group) {
    List<NumberPicker> lists = new ArrayList<NumberPicker>();
    if (group == null) {
        return lists;
    }

    for (int i = 0; i < group.getChildCount(); i++) {
        View v = group.getChildAt(i);
        if (v instanceof NumberPicker) {
            lists.add((NumberPicker) v);
        } else if (v instanceof LinearLayout) {
            List<NumberPicker> ls = getNumberPickers((ViewGroup) v);
            if (ls.size() > 0) {
                return ls;
            }
        }
    }
    return lists;
}

public static void changeNumberPickerSepColor(NumberPicker np, int color) {
    Field[] pickerFields = NumberPicker.class.getDeclaredFields();
    for (Field f : pickerFields) {
        if (f.getName().equals("mSelectionDivider")) {
            try {
                f.setAccessible(true);
                f.set(np, new ColorDrawable(color));
            } catch (Exception e) {
                e.printStackTrace();
            }
            break;
        }
    }

    // 分割线粗细
    for (Field f : pickerFields) {
        if (f.getName().equals("mSelectionDividerHeight")) {
            try {
                f.setAccessible(true);
                f.set(np, 1);
            } catch (Exception e) {
                e.printStackTrace();
            }
            break;
        }
    }
}
```
