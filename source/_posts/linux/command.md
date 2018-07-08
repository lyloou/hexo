---
title: linux常用命令
date: 2016-11-27 17:16:15
toc: true
comments: true
tags:
- linux
---

## 定时关机
http://os.51cto.com/art/201108/287974.htm
```sh
shutdown -h 22:30 # 在指定时间关机
shutdown -h 30 #30分钟后关机
```

## history之后执行指定行的命令
> `$ history // 查看命令历史`  
> `$ !334  //表示执行第334行的命令`

## 在命令行中用默认程序打开文件
`xdg-open { file | URL }`
> [Ubuntu下用命令行快速打开各类型文件(转)-bough22-ChinaUnix博客](http://blog.chinaunix.net/uid-27025492-id-3376626.html)

## ps 查看运行的进程
`ps -aux | grep vim`

## Ubuntu 系统强制关闭进程。
> $ps -aux | grep [应用名]  # 抓取指定应用的进程信息，几下 应用的pid
> $kill -9 [应用的pid]

## tail
查看实时日志： tail -fn 100 log_file_name.out
```sh
tail --help
-f: `--follow[HOW]` Output appended data as the file grows;
-n: `--lines=[+]NUM` Output the last NUM lines, instead of the last 10;
```
## sed
https://coolshell.cn/articles/9104.html
```
sed -i "s/'proxy.*/'proxy': 'http://proxy.lyloou.com'/g" eros.dev.js
```

## nohub
用途：不挂断地运行命令。
语法：nohup Command [ Arg … ] [　& ]
描述：nohup 命令运行由 Command 参数和任何相关的 Arg 参数指定的命令，忽略所有挂断（SIGHUP）信号。在注销后使用 nohup 命令运行后台中的程序。要运行后台中的 nohup 命令，添加 & （ 表示”and”的符号）到命令的尾部。
http://www.cnblogs.com/allenblogs/archive/2011/05/19/2051136.html

## 在某目录及其子目录下所有文件的最前面添加几行文字
```sh
grep -rl '' tmpdir\ | xargs sed -i "1 i hi 你好吗\n 你知道我是谁吗\n 是的，是我\n"
```
- [linux - Find and replace with sed in directory and sub directories - Stack Overflow](https://stackoverflow.com/questions/6758963/find-and-replace-with-sed-in-directory-and-sub-directories)

## lsof -i 8088

## 通过域名查看ip
- ping的方式：`ping lyloou.com`
- nslookup方式： `nslookup lyloou.com`