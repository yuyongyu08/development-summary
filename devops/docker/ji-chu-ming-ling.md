# 基础命令

## 一、镜像

### 查看镜像

```
docker images
```

### 构建镜像

```
docker build -t rory-docker-demo-2023-05-25 . 
```

`-t`：镜像名

`.`：构建目录，Dockerfile在此目录中

### 运行镜像

```
 docker run -d -p 3000:80 --name rory-docker-demo-test rory-docker-demo-2023-05-25 
```

`-d`：后台运行

`-p`：端口映射

`--name`： 容器名称

### 删除镜像

```
docker rmi [镜像名]
```

## 二、容器

### 查看容器

* 运行中的

```
docker ps
```

* 所有的

```
docker ps -a
```

### 启动容器

```
docker start [容器名]
```

### 停止容器

```
docker stop [容器名]
```

### 删除容器

```
docker rm [容器名]
```

















参考：

* [https://docs.docker.com/reference/](https://docs.docker.com/reference/)





























