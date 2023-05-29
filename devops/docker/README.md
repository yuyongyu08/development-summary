---
description: 快速入门
---

# Docker

1、安装

```bash
brew cask install docker
```



2、查看版本

```bash
docker -v
```

3、打包前端工程

```bash
vue create docker-demo  
```

```bash
yarn
```

```
yarn build
```



4、新增nginx配置文件

```
touch default.conf  
```

写入：

```
server {
    listen       80;
    server_name  localhost;

    #charset koi8-r;
    access_log  /var/log/nginx/host.access.log  main;
    error_log  /var/log/nginx/error.log  error;

    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }

    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }
}
```



5、新建Dockerfile

```
touch Dockerfile
```

写入：

```
FROM nginx  
COPY dist/ /usr/share/nginx/html/  
COPY default.conf /etc/nginx/conf.d/default.conf  
```



6、构建镜像

```
docker build -t test-docker-demo . 
```



7、运行镜像生成容器

```
docker run -d -p 3000:80 --name docker-vue-demo test-docker-demo 
```



8、访问项目

打开http://localhost:3000





9、发布镜像





### Q\&A

1. 各种教程总是用虚拟机类比docker，两者之间的区别和联系是什么？



2. Q：如何理解docker的所谓“容器化”部署？镜像是运行在哪里？



3. Q：docker是为了解决环境不一致的问题，但开发阶段并不会用docker，如何确定镜像中的环境（Dockerfile如何写）？



参考：

* [https://mp.weixin.qq.com/s/oEygasL-5owZ5b8mV6uMTw](https://mp.weixin.qq.com/s/oEygasL-5owZ5b8mV6uMTw)
* [https://docs.docker.com](https://docs.docker.com/get-started/overview/)



