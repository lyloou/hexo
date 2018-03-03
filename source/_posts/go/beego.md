---
title: Go
date: 2017.11.08 17:12
toc: true
comments: true
tags:
- go
- beego
---

Go语言里面提供了一个完善的net/http包，通过http包可以很方便的就搭建起来一个可以运行的Web服务。
同时使用这个包能很简单地对Web的路由，静态文件，模版，cookie等数据进行设置和操作。

万变不离其宗，Go的Web服务工作也离不开我们第一小节介绍的Web工作方式。

Go为了实现高并发和高性能, 使用了goroutines来处理Conn的读写事件, 这样每个请求都能保持独立，相互不会阻塞，可以高效的响应网络事件。这是Go高效的保证。
https://github.com/astaxie/build-web-application-with-golang/blob/master/zh/03.4.md


## 分页
```go
o := orm.NewOrm()
qs = o.QueryTable("user");
var pageSize = 50 // 一页50条
var pageNo = 3 // 准备取第三页
// qs.Limit("[取多少个]","[偏移行数]");
qs = qs.Limit(pageSize, pageNo*pageSize)
```
- [Mysql 分页语句Limit用法 - 柳北风儿~~~~~~~欲宇仙炅 - ITeye博客](http://qimo601.iteye.com/blog/1634748)
