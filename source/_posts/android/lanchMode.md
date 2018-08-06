---
title: Android启动屏和引导页
date: 2018-08-06 20:04:15
toc: true
comments: true
tags:
- android
---

## the weird launch mode
```
https://stackoverflow.com/questions/9363200/android-singletask-singletop-and-home-button
The behaviour of activity back stack becomes quit weird when define main activity with singleTask at the same time:

    <activity android:name=".MainActivity"
        android:launchMode="singleTask">
        <intent-filter>
            <action android:name="android.intent.action.MAIN" />
            <category android:name="android.intent.category.LAUNCHER" />
        </intent-filter>
    </activity>
    
What even worse is there is no clear explanation in the official dev guide regarding to this special use case. Some sections related to this topic are even self-contradictory.

Try using launchMode="standard" on your MainActivity A, and launchMode="singleTask" on your Activity B, which will give the expect behaviour you described.
```