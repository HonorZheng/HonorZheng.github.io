---
title: Docker02_Dockerfile编写
layout: post
tags: Docker_Flask
categories: ''

---
Dockerfile编写



[docker---Dockerfile编写] 

https://www.cnblogs.com/zpcoding/p/11450686.html#_label0_0

https://zhuanlan.zhihu.com/p/45625808

### 格式

1. ‘ #’ 为注释
2. 指令为大写，内容为小写

流程

1. docker从基础镜像运行一个容器
2. 执行一条命令并对容器作出修改
3. 执行类似docker commit的操作提交一个新的镜像层
4. docker再基于刚提交的运行一个新容器
5. 执行dockfile中的下一条指令，直到运行完所有的指令

### 核心Dockerfile指令

* USER / WORKDIR指令

* ADD/EXPOSR指令

  ADD将本地文件到镜像中

  

* RUN/ENV 指令

  

**FROM**
参数是镜像。必须是dockerfile中的第一条非注释指令。

**MAINTAINER**
指定镜像的作者信息，包含镜像的所有者和联系信息。

**RUN**

1. shell模式
   `RUN /bin/sh -c command `例如：`RUN echo hello`
2. exec模式
   `RUN ["executable","arg1","arg2"] `可以用来指定其他形式的shell运行指令。
   例如：`RUN["/bin/bash","-c","echo hello"]`

**EXPOSE**
指定运行该镜像的容器使用的端口，处于安全考虑，docker并不会打开该端口，而是使用run命令手动的添加对端口的映射。

**CMD**
用来提供容器运行的默认命令。命令可以被docker run中的指令所覆盖。

- exec模式：`CMD["executable","arg1","arg2"]`
- shell模式：`CMD command arg1,arg2`

**ENTRYPOINT**
不会被docker run命令中的命指令所覆盖。

- exec模式：`ENTRYPOINT["executable","arg1","arg2"]`
- shell模式：`ENTRYPOINTcommand arg1,arg2`

**ADD**
`ADD["SRC","DEST"]`
注：src可以是本地也可以是远程的文件，dest必须是镜像中的绝对路径

**COPY**
`COPY["SRC","DEST"]`

**对比ADD和COPY ：**
ADD包含类似tar的解压功能；
如果单纯复制文件，Docker推荐使用COPY。

**VOLUME**
`VOLUME["/data"]`
向镜像创建的容器添加卷，一个卷可以存在多个容器的特定目录，类似于公共的文件。

**WORKDIR**
`WORKDIR /PATH`
指定工作目录。

**ENV**
`ENV<key>=<value>`
一般用于指定环境变量。

**USER USER daemon**
指定镜像为某个用户/用户组运行。默认使用root用户。

**ONBUILD**
`ONBUILD [INSTRUCTION]`
为镜像添加触发器，当一个镜像作为其他镜像的基础镜像时，触发器会执行。在子镜像构建时，插入触发器中的指令。

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







