## docker

start

- run: 在没有容器运行的情况下,创建容器并运行,并启动进程.
- exec: 在现有容器中运行命令
- -i: 标准输入始终打开
- -t: 分配一个伪终端并绑定在容器标准输入上

## 查看当前启动的 docker 及状态

docker ps -a

## 退出但不关闭容器

Ctrl+P+Q

## 查看镜像列表 

docker images

在后台启动 docker,镜像名名称是 [镜像名],进程其名为[进程名],启动 bash 程序, 并把容器内的 22 映射到宿主机的 2222, 80 映射到1180, 1234,映射到 1234,8889 映射到 7779
docker run -d  -t -i -v /data/:/data/ -p 2222:22 -p 1180:80 -p 1234:1234 -p 7779:8889  --privileged ycs.cxx11 --name lbdev  /bin/bash

docker run -d -t -i -v /data/:/data/ -p 2222:22 -p 1180:80 -p 1234:1234 -p 7779:8889  --privileged --name lbdev ycs.cxx11.1:latest /bin/bash





在后台启动一个容器，并将容器内的 80 端口映射到宿主机的 31230 端口,22 映射到 2222 端口

-p 1180:80

docker attach xx


ln -sf /data/libin8 /home/libin8
useradd -u  {id} libin8
cp -r /tmp/tmp1/libin8/.bash* /home/libin8/
chown -R libin8:libin8 /home/libin8
passwd libin8
visudo

## 常用命令

docker exec -it lcsd_statistic_1 bash