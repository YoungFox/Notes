首先修改wayne/hack/docker-compose/conf/config.js中的localhostip

如果镜像拉不下来，有可能是配置中的镜像已经在hub上删除了，需要手动修改docker-compose.yaml中的配置

查看k8s集群serverapi的时候

```
kubectl  config  view --minify
```

会发现有些证书、key之类的信息，都是绝对路径

需要在docker-compose.yaml中修改volumes，将这些文件挂载进镜像，否则启动不了

在前台配置部署的时候，镜像地址形如

```
yangwenliang/node:01
```