---
title: vim
date: 2018-07-30 09:07:15
toc: true
comments: true
tags:
- linux
- vim
---


## 用vim编辑上一次输入的命令
```sh
fc 
```

## [当你在vi中修改了半天配置文件,然后发现没有写权限,没有比这更令人感到挫败了,此时你需要这条命令。](http://mingxinglai.com/cn/2012/08/you-had-better-know-instruction/)
```sh
:w !sudo tee %
# or
:w ! sudo tee %

# occur error 
:w! sudo tee %
```
