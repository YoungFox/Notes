## Minikube

Minikube is a tool that makes it easy to run Kubernetes locally. Minikube runs a single-node Kubernetes cluster inside a Virtual Machine (VM) on your laptop for users looking to try out Kubernetes or develop with it day-to-day.

Minikube 是一个可以在本地轻松运行 Kubernetes 的工具。Minikube 会在您的笔记本电脑中的虚拟机上运行一个单节点的 Kubernetes 集群，以便用户对 Kubernetes 进行试用或者在之上进行 Kubernetes 的日常开发。

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
#停止集群。该命令会关闭minikube虚拟机，但将保留所有集群状态和数据。再次启动集群将恢复到之前的状态。

minikube stop

#or 
#删除集群。该命令将关闭并删除minikube虚拟机。没有数据或状态会被保留下来。
minikube delete
```
