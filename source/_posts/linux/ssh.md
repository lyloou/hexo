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

## [How to enter ssh password using bash? ](https://stackoverflow.com/questions/16928004/how-to-enter-ssh-password-using-bash)

> Create a new keypair: (go with the defaults)
> `ssh-keygen`

> Copy the public key to the server: (password for the last time)
> `ssh-copy-id user@my.server.com`

> From now on the server should recognize your key and not ask you for the password anymore:
> `ssh user@my.server.com`