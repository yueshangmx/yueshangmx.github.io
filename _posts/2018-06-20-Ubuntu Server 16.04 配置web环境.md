---
layout: post
title: Centos服务器web环境搭建
date: 2018-06-10
description: "centos，Apache，php，mysqli，"
tags: 笔记   
---


### Apache2
- 1.在终端输入更新检查命令，
```text
sudo apt-get update
```
- 2. 在更新完成后（如果不想检查更新，也可直接输入此步）输入：
```text
sudo apt-get install apache2
```

- 3.完成后，在浏览器输入https://localhost 或者127.0.0.1，如果顺利跳出Apache版本网页，即代表安装成功

- 4.停止服务：
```text
sudo /etc/init.d/apache2 stop
```

- 5.Apache的默认文档目录
```text
web根目录  /var/www
配置文件   /etc/apache2/apache2.conf
```

### MySql8.0

- [MySql8官方提供的教程](https://dev.mysql.com/doc/mysql-apt-repo-quick-guide/en/).

直接使用apt install mysql-server安装,默认会安装MySQL 5.7，要安装MySQL8，需要到[MySQL官方网站](http://dev.mysql.com/downloads/repo/apt/)下载一个mysql-apt-config_0.*.****_all.deb

或者直接在服务器使用wget下载
```text
wget https://dev.mysql.com/get/mysql-apt-config_0.8.10-1_all.deb
```
使用
```text
sudo dpkg -i mysql-apt-config_0.*.****_all.deb
```
安装执行，选择MySQL8.0，OK。<br>
![](/images/posts/server/ub-mysql.png)

然后apt update更新一下<br>
![](/images/posts/server/apt-update.png)

安装MySQL8.0
```text
sudo apt install mysql-server
```
