---
title: ssh
date: 2016-11-26 17:16:15
toc: true
comments: true
tags:
- linux
---

## 将本地的文本文件保存到远程服务端中
```sh
cat ~/.ssh/id_rsa.pub | ssh user@123.45.56.78 "mkdir -p ~/.ssh && cat >>  ~/.ssh/authorized_keys"
https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys--2
```

