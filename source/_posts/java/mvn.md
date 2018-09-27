---
title: maven
date: 2018/07/02 20:53
toc: true
comments: true
tags:
- java
---

## [【原创】Nexus搭建Maven私服](https://www.cnblogs.com/dreamroute/p/5440419.html)
https://help.sonatype.com/repomanager2/installing-and-running/running

注意访问网址是： http://localhost:8081/nexus/

学习建议：mvn这个东西，就是难者不会，会者不难。基本上按照这样一个路线就问题不大，基本使用 => 了解继承/聚合 => 了解jar包冲突机制，并解决冲突 =>了解mvn的3个默认声明周期 ，生命周期的各个阶段phase ，各个阶段的目标goal => mvn的插件开发 => Nexus私服搭建及其使用。大致这样一个过程下来，就能非常熟悉mvn，如果在稍微看看mvn的源码，大致看一看，基本上可以说是精通mvn了。



- [使用Maven管理Java项目 - 大梦初晓 - SegmentFault 思否](https://segmentfault.com/a/1190000003044418)
- [理解Maven中的SNAPSHOT版本和正式版本 - 黄博文的地盘](http://www.huangbowen.net/blog/2016/01/29/understand-official-version-and-snapshot-version-in-maven/)
- [Maven - 快照 - Maven 教程 - 极客学院Wiki](http://wiki.jikexueyuan.com/project/maven/snapshots.html)
快照 vs 版本
对于版本，Maven 一旦下载了指定的版本（例如 data-service:1.0），它将不会尝试从仓库里再次下载一个新的 1.0 版本。想要下载新的代码，数据服务版本需要被升级到 1.1。
对于快照，每次用户接口团队构建他们的项目时，Maven 将自动获取最新的快照（data-service:1.0-SNAPSHOT）。
