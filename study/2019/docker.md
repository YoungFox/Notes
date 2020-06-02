##Dcoker 属于 Linux容器的一种封装，提供简单易用的容器使用接口

###体验ubuntu
```
docker container run -it ubuntu bash
```

```
#列出本机正在运行的容器
$ docker container ls
#列出本机所有的容器，包括终止运行的容器
$docker container ls --all
```


```
docker build -t xx .
```

```
docekr images
```

docker 可以启用负载均衡

```
 replicas: 5
```
5个实例

##docker属于操作系统层面的虚拟技术

通过定制应用的docker镜像，可以实现持续集成、交付、部署。

docker三个基本概念（整个生命周期）：
镜像
容器
仓库

数据卷（data volume）

```
#进入相应镜像进行bash操作
docker run -it --rm ubuntu:latest bash
```


```
#清除虚悬镜像
docker image ls -f dangling=true
docker image prune
```

##Dockerfile
每个指令都会建立一层

RUN:最常用的指令之一

COPY\ADD:尽量用COPY,只在需要解压的地方用ADD



停止所有容器
```
docker stop $(docker ps -aq)
```

删除所有容器
```
docker rm $(docker ps -aq)
```

删除所有镜像

```
docker rmi $(docker images -q)
```


```
## List Docker CLI commands
docker
docker container --help

## Display Docker version and info
docker --version
docker version
docker info

## Execute Docker imagen
docker run hello-world

## List Docker images
docker image ls

## List Docker containers (running, all, all in quiet mode)
docker container ls
docker container ls --all
docker container ls -aq


docker build -t friendlyhello .  # Create image using this directory's Dockerfile
docker run -p 4000:80 friendlyhello  # Run "friendlyname" mapping port 4000 to 80
docker run -d -p 4000:80 friendlyhello         # Same thing, but in detached mode
docker container ls                                # List all running containers
docker container ls -a             # List all containers, even those not running
docker container stop <hash>           # Gracefully stop the specified container
docker container kill <hash>         # Force shutdown of the specified container
docker container rm <hash>        # Remove specified container from this machine
docker container rm $(docker container ls -a -q)         # Remove all containers
docker image ls -a                             # List all images on this machine
docker image rm <image id>            # Remove specified image from this machine
docker image rm $(docker image ls -a -q)   # Remove all images from this machine
docker login             # Log in this CLI session using your Docker credentials
docker tag <image> username/repository:tag  # Tag <image> for upload to registry
docker push username/repository:tag            # Upload tagged image to registry
docker run username/repository:tag                   # Run image from a registry
```

###Swarms



###App development best practices

