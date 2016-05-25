
### 文档管理工具
名称：Android Studio

### 教程、文档、API
网址：`https://hexo.io`
安装hexo教程（需要VPN）：`https://hexo.io/zh-cn/docs/`

### 主题
名称：NexT
网址：`http://theme-next.iissnan.com/`

<!--more-->
### 问题列表
#### Error Local hexo not found
具体描述：从github上直接克隆下来的源码，执行`hexo s`会出现错误：
    > Error Local hexo not found in /XXX
    > Error Try running: 'npm install hexo --save'

原因分析：`.gitignore`文件中忽略了`node_modules`文件，所以从github上的克隆的源码中不存在此文件；    

解决方案：重新执行`npm install`命令即可；

扩展：执行 `npm install`可能会出现失败的警告，有可能是npm版本问题：


外部连接：
    * [用Hexo写博客 - ERROR Local hexo not found in xxx](http://blog.csdn.net/burststar/article/details/45115905)
    * [npm WARN optional dep failed, continuing fsevents@1.0.6](https://github.com/foreverjs/forever/issues/788)


#### add Read More
外部连接：[Hexo自动添加ReadMore标记](http://twiceyuan.com/2014/05/25/hexo%E8%87%AA%E5%8A%A8%E6%B7%BB%E5%8A%A0readmore%E6%A0%87%E8%AE%B0/)

> 
（解决问题的方法：将错误日志中的关键部分择取关键字交给Google；）