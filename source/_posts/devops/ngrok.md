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
read -p "Input your domain name:" DOMAIN
if [ "$DOMAIN" = "" ];then
    echo Please input your domain name.
    exit 0
fi

resultFileName=ngrok_`echo ${DOMAIN} | sed 's/\./_/g'`

currentPwd=$(pwd)
echo current path: $currentPwd
go get github.com/inconshreveable/ngrok
cd $GOPATH/src/github.com/inconshreveable/ngrok
git clean -df
git checkout -- .

openssl genrsa -out rootCA.key 2048
openssl req -x509 -new -nodes -key rootCA.key -subj "/CN=$DOMAIN" -days 5000 -out rootCA.pem
openssl genrsa -out device.key 2048
openssl req -new -key device.key -subj "/CN=$DOMAIN" -out device.csr
openssl x509 -req -in device.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out device.crt -days 5000

cp rootCA.pem assets/client/tls/ngrokroot.crt
cp device.crt assets/server/tls/snakeoil.crt
cp device.key assets/server/tls/snakeoil.key

make release-server
GOOS=linux GOARCH=amd64 make release-client
GOOS=windows GOARCH=amd64 make release-client
GOOS=linux GOARCH=arm make release-client
GOOS=darwin GOARCH=amd64 make release-client

mkdir -p bin/tls
mkdir -p bin/out

cp device.crt bin/tls/snakeoil.crt
cp device.key bin/tls/snakeoil.key
echo 'nohup ./ngrokd -tlsKey="tls/snakeoil.key" -tlsCrt="tls/snakeoil.crt" -domain='"$DOMAIN"' -httpAddr=":80" -httpsAddr=":443" > out/nohupd.out 2>&1 &' > ./bin/start.sh
chmod +x ./bin/start.sh
echo "server_addr: $DOMAIN:4443" > ./bin/ngrok.cfg
echo "trust_host_root_certs: false" >> ./bin/ngrok.cfg
echo 'nohup ./ngrok -config=./ngrok.cfg -subdomain=blog -proto=http 8078 > out/nohup_blog.out 2>&1 &' > ./bin/ngrok_blog.sh
chmod +x ./bin/ngrok_blog.sh

mv bin ${resultFileName}
tar -zcvf ${resultFileName}.tar.gz ${resultFileName}
mv ${resultFileName}.tar.gz $currentPwd/${resultFileName}.tar.gz
git clean -df
git checkout -- .
echo ok! result: ${resultFileName}.tar.gz
```
- 运行 `sh build_ngrok.sh`
- 根据提示输入已经配置好的域名，例如：ngrok.lyloou.com
- 在域名对应的服务器上运行：`./start.sh` （这样，服务器端就完成了）

## 打包和解压
tar -zcvf ngrok_lyloou_com.tar.gz bin
tar -zxvf ngrok_lyloou_com.tar.gz

## 下载
realpath ngrok_lyloou_com.tar.gz # 获取文件路径
scp root@170.10.0.100:/root/t/ngrok_lyloou_com.tar.gz ngrok_lyloou_com.tar.gz # 从服务器拉取文件

## 运行服务器（已经在上面的`build_ngrok.sh`中配置过了）
```sh
#!/bin/sh
./ngrokd -domain="ngrok.lyloou.com" -httpAddr=":80" -httpsAddr=":443" 

## 或者后台运行
mkdir out
chmod +x ngrokd
nohup ./ngrokd -domain="ngrok.lyloou.com" -httpAddr=":80" -httpsAddr=":443"  > out/nohup_log.out 2>&1 &
```

## 运行客户端（在上面的`build_ngrok.sh`中配置并生成了一个案例`ngrok_blog.sh`）
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