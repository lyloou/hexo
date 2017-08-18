---
title: Android中不常见问题及解答
date: 2016-07-19 09:23:17
toc: true
tags:
- Android
---

> 本文介绍了Android中的一些不常见的问题及解答；


## UnsupportedOperationException at java.util.AbstractList.remove(AbstractList.java:638)
【问题场景】
- 在给`RecyclerView.Adapter`传递数据源的时候，
我传递进去了`Arrays.asList`构成的列表，在调用`lists.remove()`方法删除某个元素的时候，出现了这个异常；

【解答】
- 我使用了`Arrays.asList()`方法，通过查看源码知道，这个方法调用了`Arras.ArrayList(E[])`来构建列表，
而这个列表是`final`的，不可modify的，所以会出现`UnsupportedOperationException`异常；
- 解决办法1：使用`new ArrayList<>();`的方式来新建列表，而不是`Arrays.asList`或数组的方式；
- 解决方法2：new ArrayList<>(Arrays.asList("1","2")); // 即封装下就可；

【外部链接】
- [Unable to modify ArrayAdapter in ListView: UnsupportedOperationException](http://stackoverflow.com/questions/3200551/unable-to-modify-arrayadapter-in-listview-unsupportedoperationexception)


## App响应外部指定格式的链接（类似：http, https, tel, mailto）
主要步骤是，配置、使用、获取数据；  
```html
在自定义的 webview中点击<a href="renrenyoupin://...">链接，可以跳转到app。
在系统浏览器中（魅族）打开一个页面，页面中包含<a href="renrenyoupin://...">链接，可以跳转
在chrome浏览器中打开一个页面，页面中包含<a href="renrenyoupin://...">链接，可以跳转
在qq浏览器中打开一个页面，页面中包含<a href="renrenyoupin://...">链接，可以跳转

直接通过浏览器的地址栏输入，不可以跳转到app。
微信对话中点击，不可以跳转app。
qq对话中点击，不可以跳转app。

app没有安装的时候，点击链接都没有任何反应。
```

```xml
<activity android:name=".MainActivity">
    <intent-filter>
        <action android:name="android.intent.action.MAIN"/>
        <category android:name="android.intent.category.LAUNCHER"/>
    </intent-filter>

    <!-- 必要的 -->
    <intent-filter>
        <action android:name="android.intent.action.VIEW"/>
        <category android:name="android.intent.category.DEFAULT"/>
        <category android:name="android.intent.category.BROWSABLE"/>
        <data
            android:host="lou.app"
            android:pathPrefix="/openwith"
            android:scheme="lyloou"/>
    </intent-filter>
</activity>
```

``` html
<!-- 在html中使用 -->
<!-- 
    如果把html代码放在了 WebView中，如果设置了setWebViewClient()，
    其中重写的方法不要拦截，否则app无法响应； （即，重写shouldOverrideUrlLoading方法时需要小心，不设置webviewClient为妙）
-->
<a href="lyloou://lou.app/openwith?name=zhangsan&age=26">启动应用程序</a>
```

```java
// 获取数据
private void getData() {
    Intent i_getvalue = getIntent();
    String action = i_getvalue.getAction();

    if (Intent.ACTION_VIEW.equals(action)) {
        Uri uri = i_getvalue.getData();
        if (uri != null) {
            String name = uri.getQueryParameter("name");
            String age = uri.getQueryParameter("age");
            Log.i(TAG, "getData: name=" + name);
            Log.i(TAG, "getData: age=" + age);
        }
    }
}
```

参考资料：  
- [android实现通过浏览器点击链接打开本地应用（APP）并拿到浏览器传递的数据 - 极客公园 - CSDN博客](http://blog.csdn.net/geekpark/article/details/16118457)
