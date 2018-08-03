---
title: vim
date: 2018-07-30 09:07:15
toc: true
comments: true
tags:
- linux
- vim
---


## 在 vim 中编辑上一条命令
```sh
fc 
```

## 当你在vi中修改了半天配置文件,然后发现没有写权限,没有比这更令人感到挫败了,此时你需要这条命令。
```sh
:w !sudo tee %
# or
:w ! sudo tee %

# occur error 
:w! sudo tee %
```
