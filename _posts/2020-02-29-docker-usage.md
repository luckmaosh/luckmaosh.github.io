docker使用

第一个命令
 docker run hello-world
 
 第二个命令

```
  ~ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              fce289e99eb9        14 months ago       1.84kB

```
怎么理解这几个参数？

- repository：仓库名字
- tag：标签或者版本
- image id：每个版本的镜像会有一个自己的id

## docker ps
列出容器，容器是运行中的镜像

```
➜  ~ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

