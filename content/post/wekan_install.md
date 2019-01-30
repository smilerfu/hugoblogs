---
title: "Wekan 安装"
date: 2019-01-30T01:39:00+08:00
lastmod: 2019-01-30T01:39:00+08:00
keywords: []
description: ""
tags: []
categories: ["Wekan"]
author: ""

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: false
toc: false
autoCollapseToc: false
# You can also define another contentCopyright. e.g. contentCopyright: "This is another copyright."
contentCopyright: false
reward: false
mathjax: false
---

<!--more-->

Wekan Wiki:https://github.com/wekan/wekan/wiki

##### 安装Docker
```shell
curl -sSL https://get.docker.com/ | sh
```

##### 安装git
```shell
yum install git
```

##### 检出wekan-mongodb
检出路径:/usr/local/wekan-mongodb
```shell
cd /usr/local
git clone https://github.com/wekan/wekan-mongodb.git
```

##### 安装docker-compose
文档: https://docs.docker.com/compose/install/
安装路径:/usr/local/bin/docker-compose(备注:docker-compose不是目录，而是可执行文件)
1.下载最新版本
```shell
sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
2.设置可执行权限
```shell
sudo chmod +x /usr/local/bin/docker-compose
```
3.设置外链
```shell
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

##### 启动Wekan
1.切换到wekan-mongodb的检出路径
```shell
cd /usr/local/wekan-mongodb
```
2.启动wekan
a)后台启动
```shell
docker-compose up -d
```
b)在当前控制台启动，ctrl-c 退出
```shell
docker-compose up
```
##### 访问
通过服务器ip:80可以访问

##### 问题
1.点击卡片跳转到localhost，无法打开
修改 wekan-mongodb 目录下的docker-compost.yml配置文件，services-wekan-environment-ROOT_URL
修改成部署机子的ip地址即可


