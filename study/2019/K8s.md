本地安装kubernetes

https://docs.docker.com/docker-for-mac/#kubernetes

镜像部署到kubernetes

1、docker stack方式

```
docker stack deploy --orchestrator kubernetes --compose-file docker-compose.yml mystack
```

```
kubectl get svc
```

cluster是docker的容器调度解决方案

2、