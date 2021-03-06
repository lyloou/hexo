---
title: ubuntu软件
sticky: 10
date: 2016-09-26 17:16:15
toc: true
comments: true
tags:
- linux
- ubuntu
---


- synpase（快速启动）
- vlc（多媒体播放器）
- wiz
- chrome
- vscode
- idea
- emacs
- shadowsocks
- proxychains
- privoxy
```sh
# vim /etc/privoxy/config
# 添加下面这一行
forward-socks5 / 0.0.0.0:1080 .

#启动
/etc/init.d/privoxy restart

# 测试
curl  -x 127.0.0.1:8118 http://www.google.com
```
- fcitx+五笔+english
- calibre（电子书阅读器）
- caja（文件管理器）
- 红移（色温调节工具）
- workrave（定时提醒）
- terminal
  [Terminator – Multiple GNOME terminals in one window | Ubuntu Geek](http://www.ubuntugeek.com/terminator-multiple-gnome-terminals-in-one-window.html)
  [安装 Terminator：一个支持多终端的终端-软件 ◆ 分享|Linux.中国-开源社区](https://linux.cn/article-2978-1.html)
- tmux
- zsh
- oh my zsh
```sh
# https://github.com/robbyrussell/oh-my-zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```
- catfish 文件搜索
- variety 壁纸切换
- git-cola


## How to set socks5 proxy in the terminal (在终端中使用代理)
```sh
# install proxychains
sudo apt install proxychains
sudo proxychains apt-get update

# now you can config your proxy in /etc/proxychains.conf
socks5 127.0.0.1 1080
```

## 截图软件 shutter
1. `sudo add-apt-repository ppa:shutter/ppa1`
2. `sudo apt-get update`  
3. `sudo apt-get install shutter1`
4. 设置快捷键 keyboard -> shortcut -> `shutter -s` -> Ctrl+Alt+A -> ok
- [Ubuntu 安装截图工具Shutter，并设置快捷键 Ctrl+Alt+A_Linux教程_Linux公社-Linux系统门户网站](http://www.linuxidc.com/Linux/2015-07/119753.htm)

## 卸载软件
1. 查找安装名称：`dpkg -l | grep package_name`
2. 卸载`sudo apt-get remove package_name`, 具体输入`apt-get`命令查看

## 本地安装
以安装网易云音乐为例
1. 从官网下载deb安装文件
2. 执行下列命令
```sh
$ sudo dpkg -i netease*.dbg
$ sudo apt -f install
```

## 去除chrome的`输入密码以解锁密码环`提示
- 终端输入`seahorse`
- 右键删除 `登录`
- 退出 chrome
- 提示输入密码时，不输入任何内容，直接按下一步。
> [解决打开Chrome出现 输入密码以解锁您的登录密钥环 - Android/Linux的专栏 - 博客频道 - CSDN.NET](http://blog.csdn.net/kangear/article/details/20789451)

## 安装WenQuanYi Zen Hei 字体
1. download file: wqy-zenhei-0.9.45.deb
2. install: dpkg -i wqy-zenhei-0.9.45.deb


## fcitx 五笔输入法
### 安装 fcitx
`sudo apt-get install fcitx fcitx-table-wubi fcitx-tools -y`

### 启用自动调频
修改配置文件 /usr/share/fcitx/table/wbx.conf
```
AdjustOrder=AdjustFreq
```

### 不能正常打出中文标点
修改配置文件 /usr/share/fcitx/addon/fcitx-fullwidth-char.conf
```
Priority=80
```
### 重启输入法
`fcitx -r`

- [linux 安装与配置 fcitx 五笔输入法](https://zhuanlan.zhihu.com/p/28586200)