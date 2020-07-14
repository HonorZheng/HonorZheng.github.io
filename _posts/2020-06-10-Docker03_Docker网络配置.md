---
title: Docker03_Docker网络配置
layout: post
tags: Docker_Flask
categories: ''

---
# Docker网络配置

###### [Docker高级网络配置快速配置指南](http://www.dockerinfo.net/644.html)

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



### 2.域名 （**Domain Name**）、主机和服务商

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



<img src="C:\Users\zheng\AppData\Roaming\Typora\typora-user-images\image-20200629162246567.png" alt="image-20200629162246567" style="zoom:50%;" />

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



未完待续...



