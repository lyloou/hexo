---
title: 【Android】Context上下文
date: 2016-06-02 09:10:02
toc: true
categories:
tags:
---

## 摘要：
主要内容：

任务列表：
- [x] mContext
- [x] BroadcastReceiver


<!--more-->


## 添加`mContext`
- 在Activity和Fragment中，经常需要用到上下文信息；
虽然通过`类名.this`的方式虽然也可以，但是`mContext`将更方便易懂，尤其是将代码拷贝来拷贝去时；

- 将`mContext`声明在基类中（例如：`BaseActivity`、`BaseFragment`）：
``` java
protected Activity mContext;
```

在BaseActivity的`onCreate`方法中添加：
``` java
mContext = this;
```

或者在BaseFragment中的`onCreate`中添加：
``` java
mContext = getActivity();
```
这样所有继承自`BaseActivity`和`BaseFragment`的类，均可以直接使用`mContext`了；

- 扩展：类似的方法，可以让所有的子类直接使用`TAG`，而不需要在自己的类中声明和初始化；
在`BaseActivity`中添加：
``` java
protected final String TAG = getClass().getSimpleName();
```

### 外部链接
- [Context, What Context?](https://possiblemobile.com/2013/06/context/)


## BroadcastReceiver
- 广播是一种可以跨进程的通信方式。（引用自：《第一行代码》p199）

> 需要注意的是，不要在`onReceiver()`中添加过多的逻辑或进行任何耗时操作，因为在广播接收器中是不允许开启线程的，
当`onReceiver()`方法运行了较长时间而没有结束时，程序就会报错。因此，广播接收器更多的是扮演一种打开其他组件的角色，
比如创建一条状态栏通知，或者启动一个服务等。（引用自：《第一行代码》p196）