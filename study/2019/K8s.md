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

## Minikube

Minikube is a lightweight Kubernetes implementation that creates a VM on your local machine and deploys a simple cluster containing only one node.

### Hello Minikube
1. Before you begin

minikube-server-js
```
var http = require('http');

var handleRequest = function(request, response) {
  console.log('Received request for URL: ' + request.url);
  response.writeHead(200);
  response.end('Hello World!');
};
var www = http.createServer(handleRequest);
www.listen(8080);
```

minikube/Dockerfile 
```
FROM node:6.14.2
EXPOSE 8080
COPY server.js .
CMD node server.js

```

2. Create a Minikube cluster

```
minikube dashboard
```

3. Create a Deployment

```
#默认从远程库拉取镜像，可以修改配置改为本地，目前还不知道哪里改....
kubectl create deployment hello-node --image=gcr.io/hello-minikube-zero-install/hello-node
```
4. Create a Service

```
kubectl expose deployment hello-node --type=LoadBalancer --port=8080

#访问服务
minikube service hello-node
```

5. Clean up
```
kubectl delete service hello-node
kubectl delete deployment hello-node

#or

minikube stop

#or 

minikube delete
```

## 镜像部署到kubernetes

1、docker stack方式

```
docker stack deploy --orchestrator kubernetes --compose-file docker-compose.yml mystack
```

```
kubectl get svc
```

cluster是docker的容器调度解决方案
