---
share: "true"
title: docker命令
date: 2025-09-13
tags:
  - docer
categories: 
---

## 1. 基础命令

```
docker --version                      # 查看 Docker 版本
docker info                           # 查看系统 Docker 信息，包括容器、镜像、存储驱动等
```


## 2. 镜像 (Images)

```
docker search ubuntu                  # 在 Docker Hub 搜索 ubuntu 镜像
docker pull ubuntu:20.04              # 拉取 ubuntu:20.04 镜像（未指定版本默认 latest）
docker images                         # 查看本地所有镜像
docker rmi ubuntu:20.04               # 删除本地 ubuntu:20.04 镜像
```


## 3. 容器 (Containers)

```
docker run -it --name myubuntu ubuntu:20.04 /bin/bash  
# -it：交互模式，进入容器终端  
# --name：指定容器名称  
# ubuntu:20.04：镜像名  
# /bin/bash：启动后进入 bash  

docker run -d --name mynginx -p 8080:80 nginx  
# -d：后台运行容器  
# --name：指定容器名称  
# -p 8080:80：映射宿主机 8080 端口到容器 80 端口  
# nginx：使用 nginx 镜像  

docker ps                             # 查看正在运行的容器
docker ps -a                          # 查看所有容器（包括已停止的）
docker stop mynginx                   # 停止容器 mynginx
docker start mynginx                  # 启动容器 mynginx
docker rm mynginx                     # 删除容器 mynginx
```


## 4. 容器操作

```
docker exec -it myubuntu /bin/bash    # 进入正在运行的容器 myubuntu，打开 bash 交互
docker logs mynginx                   # 查看容器 mynginx 的日志输出
docker exec myubuntu ls /home         # 在容器 myubuntu 内执行 ls /home 命令
```


## 5. 数据卷 (Volumes)

```
docker volume create mydata           # 创建一个数据卷 mydata
docker volume ls                      # 查看所有数据卷
docker run -d --name mysql -v mydata:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 mysql:8.0  
# -d：后台运行  
# --name mysql：容器名称  
# -v mydata:/var/lib/mysql：挂载数据卷 mydata 到容器 /var/lib/mysql  
# -e MYSQL_ROOT_PASSWORD=123456：设置 MySQL root 用户密码  
# mysql:8.0：使用 mysql 8.0 镜像  
```

## 6. 网络 (Networks)

```
docker network ls                     # 查看所有 Docker 网络
docker network create mynet           # 创建一个自定义网络 mynet
docker run -d --name app --network mynet nginx  
# 运行一个容器 app  
# --network mynet：指定加入 mynet 网络  
# nginx：使用 nginx 镜像  
```

## 7. 构建镜像

```
docker build -t myapp:1.0 .           
# -t myapp:1.0：为镜像命名并指定版本号  
# . ：Dockerfile 所在目录（当前目录）  

docker history myapp:1.0              # 查看 myapp:1.0 镜像的构建历史
```
## 8. 清理命令

```
docker system prune -a                
# 清理未使用的容器、网络、镜像（加 -a 会删除未被使用的所有镜像）
```
