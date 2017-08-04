
## 症状
用cordova生成的app，其中的assets文件夹中保存的是前端文件`www`。如果修改前端代码，  
覆盖安装app后，其前端代码未生效（原生代码是生效了的）。

## 解决办法
1. 在activity中调用 `getAssets()`方法；
2. 更新版本号；（对于有些机型来说，相同version的app不会更新assets文件，也不可降级覆盖安装。）

相信通过上面两个步骤可以解决掉大部分机型的覆盖安装问题；

> open file with `context.getAssets()` on each startup of the app, when upgrade the app,  
first launch it and after that check if file has change.
Its seems that until you access the file, it is not extracted from the apk to  
`/data/data/<your-package>/`

- [Android Asset file not upgraded on app upgrade](https://stackoverflow.com/questions/30651788/android-asset-file-not-upgraded-on-app-upgrade)
- [Assets not replaced by version upgrade?](https://stackoverflow.com/questions/33469330/assets-not-replaced-by-version-upgrade)
- [android开发，assets下面的资源文件不会变化/改动](http://www.cnblogs.com/feijian/p/4424923.html)