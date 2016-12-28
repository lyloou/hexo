---
title: Fragment常用技巧
date: 2016-08-04 09:05:40
toc: true
tags:
- Android
---

## Fragment中监听返回键
``` java
//主界面获取焦点,用来监听返回键
private void getFocus() {
    View view = getView();
    if (view == null) {
        return;
    }

    view.setFocusableInTouchMode(true);
    view.requestFocus();
    view.setOnKeyListener(new View.OnKeyListener() {
        @Override
        public boolean onKey(View v, int keyCode, KeyEvent event) {
            if (event.getAction() == KeyEvent.ACTION_UP && keyCode == KeyEvent.KEYCODE_BACK) {
                // 监听到返回按钮点击事件
                if (mCbControlSelectAll.getVisibility() == View.VISIBLE) {
                    sync(false);
                    return true;
                }
            }
            return false;
        }
    });
}
```
### 外部链接
- [Android必知必会-Fragment监听返回键事件](http://blog.csdn.net/ys743276112/article/details/51205227)