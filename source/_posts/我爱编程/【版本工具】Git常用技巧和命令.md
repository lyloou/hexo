---
title: 【版本工具】Git常用技巧和命令
date: 2016-07-12 08:17:25
categories:
- 我爱编程
tags:
- Git
---
## 关键字
`Git` `GitHub` `版本控制`

## 摘要：
> 主要内容：
本文介绍了版本控制的常用技巧和命令等内容；


<!--more-->
## 配置及初始化
### 【设置用户名和邮箱】
```
$ git config --global user.name "Lou"
$ git config --global user.email "lyloou6@gmail.com"
```

### 【查看用户的配置信息】
```
$ git config user.name
$ git config user.email
```

### 【生成密钥】
密钥是上传到远程库的凭证，是本地与远程库的桥梁；
```
$ ssh-keygen -t rsa -C "lyloou6@gmail.com"
```

### 【测试连通性】
```
ssh -T git@github.com
```

---
## 使用过程中的常用命令
- 添加到版本控制: `git add filename.md`
- 添加描述并提交： `git commit -m "first init"`

- 移除远程仓库： `git remote remove origin`
- 添加远程仓库： `git remote add origin git@github.com:lyloou/lou.git`
- 提交到远程仓库： `git push -u origin master`


---
## 外部链接
- [git-ssh 配置和使用](https://segmentfault.com/a/1190000002645623)

