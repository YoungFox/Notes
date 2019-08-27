管理服务之用

后台运行

```
docker-compose up -d
```

查看环境变量

```
docker-compose run web env
```


When you set the same environment variable in multiple files, here’s the priority used by Compose to choose which value to use:

1. Compose file
2. Shell environment variables
3. Environment file
4. Dockerfile
5. Variable is not defined


production config

1. Removing any volume bindings for application code, so that code stays inside the container and can’t be changed from outside
2. Binding to different ports on the host
3. Setting environment variables differently, such as when you need to decrease the verbosity of logging, or to enable email sending)
4. Specifying a restart policy like restart: always to avoid downtime
5. Adding extra services such as a log aggregator


```
docker stack ls                                            # List stacks or apps
docker stack deploy -c <composefile> <appname>  # Run the specified Compose file
docker service ls                 # List running services associated with an app
docker service ps <service>                  # List tasks associated with an app
docker inspect <task or container>                   # Inspect task or container
docker container ls -q                                      # List container IDs
docker stack rm <appname>                             # Tear down an application
docker swarm leave --force      # Take down a single node swarm from the manager
```