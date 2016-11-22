---
title: Android中巧用官方自带View —— WebView
date: 2016.08.04 08:42:57
toc: true
tags:
- Android
---



获取WebView的点击元素
===================
可以通过搜索关键字：`HitTestResult getHitTestResult`来知道更多内容；

注意：X5WebView，来源于腾讯TBS系统，是另外一个继承体系（可以通过打印`view.getClass()`的方式查看其继承体系）
``` java
private void setLongClick(final View view) {
    //长按点击事件
    view.setOnLongClickListener(new View.OnLongClickListener() {
        @Override
        public boolean onLongClick(View v) {
            //响应长按事件（如果webview继承自安卓原生系统）
            if (view instanceof WebView) {
                WebView.HitTestResult result = ((WebView) view).getHitTestResult();
                if (result != null) {
                    int type = result.getType();
                    //判断点击类型如果是图片
                    if (type == WebView.HitTestResult.IMAGE_TYPE || type == WebView.HitTestResult.SRC_IMAGE_ANCHOR_TYPE) {
                        //弹出对话框
                        showDialog(result.getExtra());
                    }
                }
            } else if (view instanceof X5WebView) {
                //响应长按事件（如果webview继承自腾讯的TBS系统）
                Log.i(TAG, "onLongClick: x5");
                com.tencent.smtt.sdk.WebView.HitTestResult hitTestResult = ((X5WebView) view).getHitTestResult();
                if (hitTestResult != null) {
                    int type = hitTestResult.getType();
                    if (type == X5WebView.HitTestResult.IMAGE_TYPE || type == X5WebView.HitTestResult.SRC_IMAGE_ANCHOR_TYPE) {
                        showDialog(hitTestResult.getExtra());
                    }
                }
            }
            return false;
        }
    });
}
```

参考资料
========

- [获取Android webview的点击元素](http://www.cnblogs.com/classloader/p/5302784.html)
- [](https://developer.android.com/reference/android/webkit/WebView.HitTestResult.html)
