---
title: Docker02_Dockerfile编写
layout: post
tags: Docker_Flask
categories: ''

---
# Dockerfile编写

[TOC]

### 1.格式

1. ‘ #’ 为注释
2. 指令为大写，内容为小写

### 2.流程

1. docker从基础镜像运行一个容器

2. 执行一条命令并对容器作出修改

3. 执行类似docker commit的操作提交一个新的镜像层

4. docker再基于刚提交的运行一个新容器

5. 执行dockfile中的下一条指令，直到运行完所有的指令

   

   #### dockerfile面向开发，docker镜像成为交付标准，docker容器涉及部署和运维

   <img src="C:\Users\zheng\AppData\Roaming\Typora\typora-user-images\image-20200619141630235.png" alt="image-20200619141630235" style="zoom: 50%;" />

### 3.核心Dockerfile指令

**FROM**
后面放基础镜像，参数是镜像。必须是dockerfile中的第一条非注释指令。

```dockerfile
FROM  scratch
```

**MAINTAINER**
指定镜像的作者信息，包含镜像的所有者和联系信息。

```dockerfile
MAINTAINER zhengkan<zhengkan1993@gmail.com>
```

**RUN**

1. shell模式
   `RUN /bin/sh -c command `例如：`RUN echo hello`
2. exec模式
   `RUN ["executable","arg1","arg2"] `可以用来指定其他形式的shell运行指令。
   例如：`RUN["/bin/bash","-c","echo hello"]`

**EXPOSE**
指定运行该镜像的容器使用的端口。

处于安全考虑，docker并不会打开该端口，而是使用run命令手动的添加对端口的映射。

**CMD**
用来提供容器运行的默认命令。命令可以被docker run中的指令所覆盖。

即只运行dockerfile中最后一个CMD

- exec模式：`CMD["executable","arg1","arg2"]`

- shell模式：`CMD command arg1,arg2`

  ```dockerfile
  FROM centos
  RUN yum install -y curl
  CMD ['curl','-s','http://ip.cn']
  ```

**ENTRYPOINT**

与CMD功能一样，但是：

不会被docker run命令中的命指令所覆盖，有它就用它。

- exec模式：`ENTRYPOINT["executable","arg1","arg2"]`

- shell模式：`ENTRYPOINTcommand arg1,arg2`

  ```dockerfile
  FROM centos
  RUN yum install -y curl
  CMD ['curl','-s','http://ip.cn']
  ENTRYPOINT -i
  ```

  相当于将 -i 命令插入到 中，如果使用CMD添加-i功能，会被覆盖，不能成功添加；使用ENTRYPOINT可以直接加入并实现。

  ```
  curl -s -i  http://ip.cn
  ```

**ADD**

```dockerfile
ADD ["SRC","DEST"]
ADD /predict_sales /task01
```

- [x] 拷贝+解压缩

  【相当于把SRC文件夹内的内容copy到DEST文件夹中】，比copy命令强大


  注：src可以是本地也可以是远程的文件，dest必须是镜像中的绝对路径

**COPY**

```
COPY["SRC","DEST"]
COPY /predict_sales /task01
```

docker cp 命令用于容器与主机之间的数据拷贝

- 将主机 /www/runoob 目录拷贝到容器 96f7f14e99ab 的 /www 目录下

```jsx
docker cp /www/runoob 96f7f14e99ab:/www/
```

- 将容器 96f7f14e99ab 的 /www 目录拷贝到主机的 /tmp 目录中

```jsx
docker cp 96f7f14e99ab:/www /tmp/
```

- [x] 只是拷贝

**>>>对比ADD和COPY<<< **
ADD包含类似tar的解压功能；
如果单纯复制文件，Docker推荐使用COPY。

**VOLUME**

容器数据卷，用于数据的保存和持久化

```dockerfile
VOLUME ["/data"]
```

向镜像创建的容器添加卷，一个卷可以存在多个容器的特定目录，类似于公共的文件。

在用 `docker run` 命令的时候, 使用 `-v` (`volume` 缩写) 标记来**创建一个数据卷并挂载到容器里**. 

在一次 `run` 中多次使用可以挂载多个数据卷

```dockerfile
$ docker run -it -v /宿主机绝对路径:/容器内目录 <image_name>
```

主要可用于主机与宿主机的数据同步，步骤如下：

1. 容器先停止退出，使用docker stop containerID

2. 主机修改a.blog

3. 容器重启进入docker start containerID

4. 查看主机修改过的a.log

   

   **容器和宿主机之间数据共享**

   在容器中修改文件内容, 宿主机中可以发现文件内容发生改变. **“可读可写”**

   **容器停止退出后, 宿主机修改后数据是否同步?**

   同步

   **文件操作权限**

   ```
   $ docker run -it -v /宿主机绝对路径:/容器内目录:权限 <image_name>
   ```

   举个🌰子

   ```
   $ docker run -it -v /hostDataV:/containerDataV:ro <image_name>
   ```

   `ro` - Read Only, 只读

   在 container 中 执行 `touch container.txt` 会返回错误信息
   
   --------------------------------------------------------------
   
   ## Docker 挂载目录
   
   挂载目录后镜像内就可以共享宿主机里的文件
   
   通过 run -v 参数指定挂载目录(格式：宿主机目录:镜像内挂载目录)，如果宿主机目录不存在则创建
   
   Centos7 中本地挂载的目录在容器中没有执行权限，通过 --privileged=true 给容器加特权
   
   下面以 centos 镜像为例：
   
   1. 通过 Centos 镜像运行一个容器，并设置挂载目录
   
   
   
   ```kotlin
   docker run -it -v /home/linyuan/Downloads/data:/data centos
   ```
   
   1. 此时可看到宿主机上 /home/linyuan/Downloads 文件夹下多出了 /data 目录
   
   2. 因为通过 -it 参数，已进入容器内部，通过 ls -a 命令查看文件夹，可看见多出 /data 目录，通过 cd 命令进入文件夹下并新建文件 touch a.txt
   
   3. 可看见宿主机 /data 目录也会存在该文件
   
      --------------------------------------------------------------

**WORKDIR**

```dockerfile
WORKDIR /PATH
WORKDIR $MY_PATH
```

指定登录后的工作目录。

**ENV**

```dockerfile
ENV <key>=<value>
ENV $MY_PATH/workdir
```

一般用于指定环境变量。

**USER USER daemon**
指定镜像为某个用户/用户组运行。默认使用root用户。

**ONBUILD**
`ONBUILD [INSTRUCTION]`
为镜像添加触发器，当一个镜像作为其他镜像的基础镜像时，触发器会执行。

在子镜像构建时，插入触发器中的指令。

**4.3.4 Dockerfile的构建过程**

**docker history IMAGE**
查看镜像的构建过程

下面是容器具体的构建过程：

1. 从基础镜像**运行一个容器**（使用FROM指令指定的镜像名）。
2. 执行一条指令，对容器做出**修改。**
3. 执行类似docker commit的操作，**提交**一个**新的镜像层。**
4. **再**基于刚提交的镜像**运行一个容器。**
5. 执行Dockerfile中的下一条指令，直至所有指令执行完毕。

可以简单理解为一个递归的过程，结束条件是Dockerfile指令执行完。在Dockerfile的构建中，难免遇到一些错误，可以根据生成的每一步的镜像id生成容器调试，查找错误。

**4.3.5 构建缓存**

再次构建相同镜像时，就可以使用之前的缓存，提高构建速度。
如果不使用缓存可以：`docker build --no-cache`



### 4.案例解析

* 案例一 ：建立镜像

```dockerfile
FROM centos
ENV MYPATH 	/usr/local	# 设定MYPATH
WORKDIR $MYPATH         # 引用MYPATH
RUN yum -y install vim
RUN yum -y install net-tools
EXPOSE 80
CMD /bin/bash

```

* 案例二 

```dockerfile
FROM centos
RUN yum install -y curl
CMD ["curl","-s","http://ip.cn"]
```

**ps ：注意选择文件运行**

```
docker build -f Dockerfile02 -t myip .
```

* 案例三：ONBUILD命令

dockerfile1文件如下

```dockerfile
FROM centos
RUN yum install -y curl
CMD ["curl","-s","http://ip.cn"]
ONBUILD RUN echo "father onbuild ----886"
```

1.构建镜像 docker build -f dockerfile1 -t myip-father，生成镜像myip-father

2.编写dockerfile2,继承myip-father镜像

```dockerfile
FROM myip-father
RUN yum install -y curl
CMD ["curl","-s","http://ip.cn"]
```

 3.运行时，就会触发 “father onbuild ----886”命令



### 5.参考资料[docker---Dockerfile编写] 

https://www.cnblogs.com/zpcoding/p/11450686.html#_label0_0

https://zhuanlan.zhihu.com/p/45625808

https://zhenye-na.github.io/2019/09/29/docker-practical-guide.html 【写的很好】

视频参考https://www.bilibili.com/video/BV1Vs411E7AR?from=search&seid=1856349726122122768