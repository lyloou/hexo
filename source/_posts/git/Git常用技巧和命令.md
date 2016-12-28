---
title: Git常用技巧和命令
date: 2016-07-12 08:17:25
tags:
- Git
---
## 关键字
`Git` `GitHub` `版本控制`

## 摘要：
本文介绍了版本控制的常用技巧和命令等内容；


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
- 远程主机改名： `git remote rename <原主机名> <新主机名>`
- 使用其他主机名： `git clone -o otherName <网址>`
- 删除远程主机： `git remote rm <主机名>`
- 显示远程主机详细信息： `git remote show <主机名>`


- 创建远程origin的dev分支到本地：`git checkout -b dev origin/dev`
- 指定本地dev分支与远程origin/dev分支的链接：`git branch --set-upstream dev origin/dev`
- 提交到远程仓库： `git push -u origin master`
  > 由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令（`git push origin master`）。
  http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013752340242354807e192f02a44359908df8a5643103a000

- 修改提交信息：`git commit --amend`

- 查看图形log：`git log --graph`
- `git log --pretty=oneline`
- 查看分支合并情况：`git log --graph --pretty=oneline --abbrev-commit`

- 移除远程仓库中已有的文件： `git rm test.xml`
- 丢弃工作区的修改： `git checkout -- test.xml`，其中`--`很重要，没有这个`--`，就变成了“切换到另一个分支”。

- 取消添加（git add .）的命令：`git reset HEAD test.xml`

- 将HEAD指向到某个版本： `git reset --hard commit_id`
- 重返未来，用`git reflog`查看命令历史，以便回到未来的那个版本。

- 查看工作区和版本库最新版本的区别： `git diff HEAD -- test.xml`

- 删除远程文件夹或文件（展示要删除的文件，不是真的删除）： `git rm -r -n --cached dir2`
- 删除远程文件夹或文件： `git rm -r --cached dir2`
  http://www.zicheng.net/article/982018.htm



## 配置别名
``` js
// 显示漂亮的分支日志：git lg
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```
---

NOTE: 配置Git的时候，加上--global是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用。

NOTE: 可以通过配置`~/.gitconfig`文件来删除和修改配置


## 外部链接
- [git-ssh 配置和使用](https://segmentfault.com/a/1190000002645623)
- 《GitHub入门与实践》
- [10组最常用Git命令](http://mp.weixin.qq.com/s?__biz=MzA4MjU5NTY0NA==&mid=401074259&idx=1&sn=6e69ce5338eb5d9212953068165c1cd0&mpshare=1&scene=23&srcid=1122laeBDuW58x2VncUQ44xs)
- [Git教程-廖雪峰](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
- [Git远程操作详解](http://www.ruanyifeng.com/blog/2014/06/git_remote.html)
