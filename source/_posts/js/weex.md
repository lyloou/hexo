## [WEEX 使用navigator跳转Android系统出现ActivityNotFoundException报错](https://blog.csdn.net/violetjack0808/article/details/74390249)
```xml
<intent-filter>
    <action android:name="com.taobao.android.intent.action.WEEX"/>

    <category android:name="android.intent.category.DEFAULT"/>
    <category android:name="com.taobao.android.intent.category.WEEX"/>
    <action android:name="android.intent.action.VIEW"/>

    <data android:scheme="http"/>
    <data android:scheme="https"/>
    <data android:scheme="file"/>
    <data android:scheme="wxpage" />
</intent-filter>
```
```java
 String navUrl = getIntent().getData().toString();
```

## 需要一个`mContainer`来容纳已经过渲染的`wxview`

读源码啊: 源码是通过`weex platform add android`来获得的。

```xml
<!-- activity_wxpage.xml -->
<FrameLayout
    android:id="@+id/container"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#ffffff">

</FrameLayout>
```

```java

// AbsWeexActivity.java
@Override
public void onViewCreated(WXSDKInstance wxsdkInstance, View view) {
    if (mContainer != null) {
        mContainer.removeAllViews();
        mContainer.addView(view); // mContainer是用来容纳wxview的viewgroup
    }
}


```