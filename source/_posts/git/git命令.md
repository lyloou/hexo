---
title: git命令
date: 2016-07-12 08:17:25
toc: true
comments: true
tags:
- git
---

## 基本操作
### C
- 添加到版本控制: `git add filename.md`
- 添加描述并提交： `git commit -m "first init"`

### R 
- 查看图形log：`git log --graph`
- 查看单行log：`git log --pretty=oneline`
- 查看分支合并情况：`git log --graph --pretty=oneline --abbrev-commit`
- 查看工作区和版本库最新版本的区别： `git diff HEAD -- test.xml`

### U
- 修改提交信息：`git commit --amend`
- 取消添加（git add .）的命令：`git reset HEAD test.xml`

### D
- 移除工作空间的文件： `git rm test.xml`
- 丢弃工作区的修改： `git checkout -- test.xml`，其中`--`很重要，没有这个`--`，就变成了“切换到另一个分支”。

### RESET
- 将HEAD指向到某个版本： `git reset --hard commit_id`
- 重返未来，用`git reflog`查看命令历史，以便回到未来的那个版本。
- git reset 后丢弃远程的提交
  > [github - git 怎样删除远程仓库的某次错误提交？ - SegmentFault](https://segmentfault.com/q/1010000002898735)
    ```bash
    git log # 获取log的某次提交commit id
    git reset --hard 0301382 # 回退到0301382
    git push --force # 强制推送到服务器端
    ```
    

## 远程仓库
- 移除远程仓库： `git remote remove origin`
- 添加远程仓库： `git remote add origin git@github.com:lyloou/lou.git`
- 远程主机改名： `git remote rename <原主机名> <新主机名>`
- 删除远程主机： `git remote rm <主机名>`
- 显示远程主机详细信息： `git remote show <主机名>`
- 提交到远程仓库： `git push -u origin master`
  > 由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的
  master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令
  （`git push origin master`）。http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013752340242354807e192f02a44359908df8a5643103a000
- 删除远程文件夹或文件，但是本地还保留着： `git rm -r --cached dir2` (`-r`参数，表示递归删除文件夹的内容)
  > https://stackoverflow.com/questions/1274057/how-to-make-git-forget-about-a-file-that-was-tracked-but-is-now-in-gitignore
- 删除远程文件夹或文件，但是本地还保留着（展示要删除的文件，不是真的删除）： `git rm -r -n --cached dir2`

## 分支
## delete a git branch both locally and remotely.

### 本地分支
- 删除本地分支：`git branch -d {the_local_branch}`
  > (https://stackoverflow.com/questions/2003505/how-do-i-delete-a-git-branch-both-locally-and-remotely)

### 远程分支
- 添加本地分支到远程分支，并关联：`git push -u origin develop`
  > https://stackoverflow.com/questions/2765421/how-do-i-push-a-new-local-branch-to-a-remote-git-repository-and-track-it-too
- 创建远程origin的dev分支到本地：`git checkout -b dev origin/dev`
- 指定本地dev分支与远程origin/dev分支的链接：`git branch --set-upstream dev origin/dev`
- `git clone`默认会把远程仓库整个克隆下来，但只会创建`master`分支，如果远程还有其他分支，可以通过下面的方式clone分支。
  * 将远程分支获取至本地仓库：git checkout -b python_mail.skin origin/python_mail.skin
  * 使用-t参数，它默认会在本地建立一个和远程分支名字一样的分支：git checkout -t origin/python_mail.skin
  * [git clone 远程分支 - xqs83的专栏 - 博客频道 - CSDN.NET](http://blog.csdn.net/xqs83/article/details/7382074)
- 在`git pull`之前，本地分支关联远程分支：`git branch --set-upstream feature-A origin/feature-A`
  * [git新建本地分支自动与远程分支关联 - xqs83的专栏 - 博客频道 - CSDN.NET](http://blog.csdn.net/xqs83/article/details/17361201)
- 提交分支：`git push origin feature-A:feature-A`  
- 删除远程分支：`git push origin :feature-A`
- 删除远程分支：`git push --delete {the_remote_branch}` 
  
## remove untracked files
```bash
$ git clean -d -f
$ git clean --help
```
> [branch - How to remove local (untracked) files from the current Git working tree? - Stack Overflow](https://stackoverflow.com/questions/61212/how-to-remove-local-untracked-files-from-the-current-git-working-tree)


## 参考链接
- 《GitHub入门与实践》
- [10组最常用Git命令](http://mp.weixin.qq.com/s?__biz=MzA4MjU5NTY0NA==&mid=401074259&idx=1&sn=6e69ce5338eb5d9212953068165c1cd0&mpshare=1&scene=23&srcid=1122laeBDuW58x2VncUQ44xs)
- [Git教程-廖雪峰](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
- [Git远程操作详解](http://www.ruanyifeng.com/blog/2014/06/git_remote.html)
