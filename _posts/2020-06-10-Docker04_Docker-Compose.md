---
title: Docker03_Docker网络配置
layout: post
tags: Docker_Flask
categories: ''

---
# Docker-Compose

docker compose同一个服务器上开启多个微服务，并实现集群管理。

## 1. 安装docker compose

```linux
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

国内镜像
sudo curl -L "https://get.daocloud.io/docker/compose/releases/download/1.25.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

```

将可执行权限应用于二进制文件：

```
$ sudo chmod +x /usr/local/bin/docker-compose
```

创建软链：

```
$ sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

测试是否安装成功：

```
$ docker-compose --version
cker-compose version 1.24.1, build 4667896b
```

**注意**： 对于 alpine，需要以下依赖包： py-pip，python-dev，libffi-dev，openssl-dev，gcc，libc-dev，和 make。

## 2. Docker compose 的意义

Docker Compose实际就是一个yml批处理文件，用来管理多个容器

Dockerfile相对于镜像，犹如docker-compose.yml相对于项目集群

<img src="images\image-20200711084748151.png" alt="image-20200711084748151" style="zoom: 67%;" />

1. yml文件默认的名字为：docker-compose.yml
2. yml包含三大概念：Services、Networks、Volumes
   一个service代表一个container（这个container可以从docker hub上拉取的image创建也可以用Dockerfile build出来的image创建）
3. service的启动类似docker run，我们可以给其指定network和volume
   

## 3. yml文件的格式与写法

前提：我们本地需要有mysql和wordpress这两个镜像

```
version: '3'                 # docker文件版本格式

services:

  wordpress:                 # docker服务器名
    image: wordpress		# docker镜像
    ports:
      - 8080:80
    environment:
      WORDPRESS_DB_HOST: mysql
      WORDPRESS_DB_PASSWORD: root
    networks:
      - my-bridge

  mysql:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: wordpress
    volumes:
      - mysql-data:/var/lib/mysql
    networks:
      - my-bridge

volumes:
  mysql-data:

networks:
  my-bridge:
    driver: bridge

```

## 4. Docker-Compose启动容器

安装好Docker-Compose
新建文件夹（例如Demo）
创建docker-compose.yml文件 并且copy上述内容到该yml文件中 就可以完成wordpress博客系统的搭建

```
docker-compose up
```

注意：docker-compose up启动要保证该目录下的yml文件名称为docker-compose.yml，若为其他 xxx.yml，启动命令则需要改成

    docker-compose -f xxx.yml up
---

Docker-Compose的基本操作

#启动yml文件对应的contianers 如果yml文件被命名为docker-compose.yml则 -f [yml fileName]则不用写

```
docker-compose -f [yml fileName] start 
```

#停止yml文件对应启动的contianers

```
docker-compose -f [yml fileName] stop
```

#删除yml文件创建的 包含containers和networks等

```
docker-compose -f [yml fileName] down
```



## 5. Docker-Compose部署一个简单的python flask程序

### 5.1 Python程序如下app.py

```
from flask import Flask
from redis import Redis
import os
import socket

app = Flask(__name__)
redis = Redis(host=os.environ.get('REDIS_HOST', '127.0.0.1'), port=6379)


@app.route('/')
def hello():
    redis.incr('hits')
    return 'Hello Container World! I have been seen %s times and my hostname is %s.\n' % (redis.get('hits'),socket.gethostname())

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000, debug=True)
```

### 5.2:Dockerfile如下

```
FROM python:2.7
LABEL maintaner="Peng Xiao xiaoquwl@gmail.com"
COPY . /app
WORKDIR /app
RUN pip install flask redis
EXPOSE 5000
CMD [ "python", "app.py" ]
```

### 5.3：yml文件如下 命名为docker-compose.yml

```
version: "3"

services:

  redis:
    image: redis

  web:
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - 8080:5000 #将docker contianer的5000端口映射到本地的8080端口
    environment:
      REDIS_HOST: redis
```

### 5.4:linux上的部署

1. 将上述三个文件copy到linux机器下（新建一个目录用来存放这三个文件）
2. 执行docker-compose up -d (后台运行这些containers)
3. ie输入[http://IP:8080/](http://114.115.209.142:8080/) 可以访问到该app