---
title: 宝塔面板+Centos7.6搭建hexo
date: 2020-10-30 15:36:43
tags:
categories: Hexo
comments: false
--- 
# Centos利用宝塔面板搭建Hexo
<!-- more -->
## 第一步 Centos7.6 搭建宝塔面板
```bash
yum install -y wget && wget -O install.sh http://download.bt.cn/install/install_6.0.sh && sh install.sh
```
###宝塔面板默认安装Nginx

## 第二部 安装git 
```bash
yum install git 
```

## 第三步 利用宝塔面板安装 Node.js Npm
![avatar](https://s1.ax1x.com/2020/10/30/BtUkNR.png)
安装好后 PM2管理器后 我们就装好了 Node.js Npm
可以重启下服务器 用以下命令查看
```bash
node -v 
npm -v 
```
## 第四步 进入控制台 在home目录新建一个Hexo
```bash
npm install -g hexo-cli //安装hexo
hexo init blog
cd blog
npm install
hexo cl&&hexo g
```
## 第四步 宝塔面板-网站 选择hexo blog 目录 中的  public
[![Btd6nU.png](https://s1.ax1x.com/2020/10/30/Btd6nU.png)](https://imgchr.com/i/Btd6nU)