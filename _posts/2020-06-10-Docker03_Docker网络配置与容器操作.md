---
title: Docker03_Docker网络配置
layout: post
tags: Docker_Flask
categories: ''

---
# Docker网络配置

[Docker高级网络配置快速配置指南](http://www.dockerinfo.net/644.html)

## 1.阿里云镜像配置

```
sudo mkdir -p /etc/docker

sudo tee /etc/docker/daemon.json <<-'EOF'

{ 

 "registry-mirrors": ["https://lnwifaa6.mirror.aliyuncs.com"] 

}

EOF

sudo systemctl daemon-reload 

sudo systemctl restart docker
```



## 2.域名 （**Domain Name**）、主机和服务商

域名是用来标记一个网站的名字

网址 = www. + 域名 ， 如百度的域名为 baidu.com：

```
www.baidu.com
```



1. TCP/IP协议

应用层： **HTTP** ， DNS  ,  FTP  ,  SMTP ,TELNET

传输层：**TCP** , UDP

网络层：**IP** ,ICMP, ARP, RARP

接口层：各种物理通信接口



<img src="images\image-20200629162246567.png" alt="image-20200629162246567" style="zoom:50%;" />

2.IP协议 【Internet Protocol】

IPv4使用32位地址，以点分十进制表示，如192.168.0.1

```
127.0.0.1 ：      本机

192.168. *. *    局域网

10.* .* . *      内部网
```

IPv6采用128位地址，写成8个16位无符号证书，以冒号隔开，如

```
CDCD:910A:2222:5498:8475:1111:3900:2020
```

3.TCP/UDP协议

TCP,    Transmission Control Protocol （传输控制协议）

```
三次握手建立连接 -> 可靠性传输 -> 连接中止
```

UDP，User Datagram Protocol (用户数据报协议)

```
无连接(无三次握手）、不可靠、快速传输
```

4.DNS,DHCP

DNS,   Domain Name System  (域名解析系统)

DHCP ,Dynamic Host Configuration Protocol(动态主机配置协议)

5.FTP

File ，File Transfer Protocol（文件传输协议）

默认 端口 21，基于TCP传输协议；用于文件（如视频等）传输

6.HTTP协议

HTTP,  Hypertext Transfer Protocol 超文本传输协议

默认端口为80

​	6.1 http请求



## 3.docker四种网络模式区别

1.host模式
host表示容器共享宿主机的ip和端口号。容器中不会虚拟自己的网卡和ip，当你查看容器ip的时候，其实是宿主机的ip。
如：创建nginx容器

```dockerfile
docker run -tid --net=host --name nginx nginx:1.13.12
```

你访问主机的http://ip:80其实就是容器的80端口，不用做端口映射了。

2.Container模式(未测试)
container是共享容器ip地址和端口

```dockerfile
docker run -tid --net=container:nginx --name mysql mysql:5.7
```

3.None模式s
使用none模式时容器没有网卡、IP、路由等信息。需要我们自己为Docker容器添加网卡、配置IP等

```
docker run -tid --net=none --name nginx2 nginx:1.13.12
```

4.bridge模式
bridge模式是docker默认的网络模式，这种模式容器直接可以互相通讯，但无法和宿主机通讯。

注：bridge不支持自定义容器ip
如： 

```
docker run -itd --net bridge --ip 172.18.0.10 nginx:latest /bin/bash
```

会报错：

```
docker: Error response from daemon: User specified IP address is supported on user defined networks only.
```

跨主机通信：
直接路由方式、桥接方式（如pipework）、Overlay隧道方式（如flannel、ovs+gre）

# Docker容器操作

## 1.容器重命名

```dockerfile
docker rename <my_container> <my_new_container>
```

