https://kubernetes.io/zh/docs/tutorials/

https://yeasy.gitbooks.io/docker_practice/kubernetes/

https://kubernetes.io/docs/tutorials/hello-minikube/

##Kubernetes集群

集群由两种类型的资源组成

1. 一个Master是集群的调度节点
2. Nodes是应用程序实际运行的工作节点

##Depoyments

##Pods
A Pod is a group of one or more application containers (such as Docker or rkt) and includes shared storage (volumes), IP address and information about how to run them.

##Node
A node is a worker machine in Kubernetes and may be a VM or physical machine, depending on the cluster. Multiple Pods can run on one Node.

![Pods&Node](./module_03_nodes.svg)


## 镜像部署到kubernetes

1、docker stack方式

```
docker stack deploy --orchestrator kubernetes --compose-file docker-compose.yml mystack
```

```
kubectl get svc
```

cluster是docker的容器调度解决方案


## 一些命令


```
kubectl -n k8s01 get svc

kubectl config  view --minify

kubectl get node -o yaml
```
