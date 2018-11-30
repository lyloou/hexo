---
title: ngrok搭建
date: 2018-11-30 10:39:51
toc: true
comments: true
tags:
- devops
---


## 配置域名（需支持泛域名功能）

| 子域名 | 记录类型 | 线路类型 | 记录值|
| ----- | ------- | ------ | ----- |
| ngrok | A记录    |通用  | 170.10.10.100 |
| *.ngrok | A记录    |通用  | 170.10.10.100 |

## 安装git
...

## 安装并配置好go
- https://github.com/golang/go/wiki/Ubuntu
```
sudo add-apt-repository ppa:gophers/archive
sudo apt-get update
sudo apt-get install golang-1.10-go -y

mkdir -p $HOME/c
mkdir -p $HOME/w
ln -sf /usr/lib/go-1.10 $HOME/c/go
```

```ini
export GOROOT=$HOME/c/go
export GOPATH=$HOME/w/go
export PATH=$GOROOT/bin:${GOPATH}/bin:$PATH
```

## 编译生成目标文件
创建并进入临时目录：`mkdir $HOME/t && cd $_`
创建文件`build_ngrok.sh`加入以下内容
```sh
#!/bin/sh
DOMAIN_NAME=ngrok.lyloou.com  # 修改为你自己的域名

go get github.com/inconshreveable/ngrok
cd $GOPATH/src/github.com/inconshreveable/ngrok
cd ngrok
openssl genrsa -out rootCA.key 2048
openssl req -x509 -new -nodes -key rootCA.key -subj "/CN=$DOMAIN_NAME" -days 5000 -out rootCA.pem
openssl genrsa -out device.key 2048
openssl req -new -key device.key -subj "/CN=$DOMAIN_NAME" -out device.csr
openssl x509 -req -in device.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out device.crt -days 5000

cp rootCA.pem assets/client/tls/ngrokroot.crt
cp device.crt assets/server/tls/snakeoil.crt
cp device.key assets/server/tls/snakeoil.key

make release-server
GOOS=linux GOARCH=amd64 make release-client
GOOS=windows GOARCH=amd64 make release-client
GOOS=linux GOARCH=arm make release-client
tar -zcvf ngrok_bin.tar.gz $GOPATH/src/github.com/inconshreveable/ngrok/bin
```
运行 `sh build_ngrok.sh`

## 打包
tar -zcvf ngrok_bin.tar.gz bin

## 下载
scp root@170.10.0.100:/root/t/ngrok_bin.tar.gz ngrok_bin.tar.gz

## 运行服务器
```sh
#!/bin/sh
./ngrokd -domain="ngrok.lyloou.com" -httpAddr=":80" -httpsAddr=":443" 

## 或者后台运行
mkdir out
chmod +x ngrokd
nohup ./ngrokd -domain="ngrok.lyloou.com" -httpAddr=":80" -httpsAddr=":443"  > out/nohup_log.out 2>&1 &
```

## 运行客户端
添加配置ngrok.cfg：
```sh
server_addr: "ngrok.lyloou.com:4443"
trust_host_root_certs: false
```

```sh
#!/bin/sh
nohup ./ngrok -config=./ngrok.cfg -subdomain=lou -proto=http 80 > out/nohup_lou.out 2>&1 &
```



## 参考资料
- [从零教你搭建ngrok服务](https://morongs.github.io/2016/12/28/dajian-ngrok/)
- [Ubuntu下编译安装ngrok](https://blog.csdn.net/cloume/article/details/51209493)