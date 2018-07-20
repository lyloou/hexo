
## [Docker中文教程_Docker开发中文手册[PDF]下载-极客学院Wiki](http://wiki.jikexueyuan.com/project/docker/)

`-d`: 标示是让docker容器在后台运行。
`-P`: 标示Docker所需的端口映射从主机映射到我们的容器内。
`-t`: 表示在新容器内指定一个伪终端或终端，
`-i`: 表示允许我们对容器内的STDIN进行交互。
`-p`: 标识来指定容器端口绑定到主机端口
      > `sudo docker run -d -p 5000:5000 training/webapp python app.py`
      > `sudo ocker port nostalgic_morse 5000`
      > https://wiki.jikexueyuan.com/project/docker/userguide/dockerlinks.html


```sh
sudo docker run -t -i training/sinatra /bin/bash
sudo docker commit -m="Added json gem" -a="Lou Li" \
    9e4dcef3e152 lyloou/sinatra:v2
    4f177bd27a9ff0f6dc2a830403925b5360bfe0b93d476f7fc3231110e7f71b1c
```

```sh
sudo docker build -t="lyloou/sinatra:v2" .
sudo docker tag 5db5f8471261 lyloou/sinatra:devel
sudo docker push lyloou/sinatra
sudo docker rmi lyloou/sinatra
```

```sh
# http://wiki.jikexueyuan.com/project/docker/examples/nodejs_web_app.html
# run in background
sudo docker run -p 49161:8080 -d lyloou/centos-node-hello:latest

# https://askubuntu.com/questions/505506/how-to-get-bash-or-ssh-into-a-running-container-in-background-mode
sudo docker exec -it f3b /bin/bash 
```