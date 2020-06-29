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



