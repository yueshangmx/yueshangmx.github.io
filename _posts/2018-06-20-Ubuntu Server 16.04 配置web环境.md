---
layout: post
title: Ubuntu服务器web环境搭建
date: 2018-06-20
description: "Ubuntu，Apache，php，mysqli，"
tags: 笔记   
---


### Apache2
- 1.在终端输入更新检查命令，
```text
sudo apt-get update
```
- 2.在更新完成后（如果不想检查更新，也可直接输入此步）输入：
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
![](/images/posts/server/ub-mysql.png)<br>
![](/images/posts/server/ub-mysql-2.png)<br>
![](/images/posts/server/ub-mysql-3.png)

然后apt update更新一下<br>
![](/images/posts/server/apt-update.png)

安装MySQL8.0
```text
sudo apt install mysql-server
```
![](/images/posts/server/ub-install-mysql.png)

安装过程中出现如下界面要求用户输入MySQL密码<br>
![](/images/posts/server/set-passwd.png)

这里注意一下，由于MySQL8.0采用了新的加密方式，正是因为这个加密方式才导致phpmyadmin和一些图形管理工具登录不了MySQL，所以我们这里选择采用5.x的加密方式。

![](/images/posts/server/set-passwd-2.png)

最后在终端登录mysql可以看到MySQL版本号为8.0！！
```text
sudo /etc/init.d/mysql start #启动mysql服务
mysql -u root -p
```
![](/images/posts/server/mysql-version.png)



### PHP7.2

1.添加PHP7.2的源并安装
```text
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
sudo apt-get install -y php7.2
```
![](/images/posts/server/ub-install-php.png)

然后再安装你需要的模块
```text
sudo apt-get install php7.2-mysql php7.2-curl php7.2-json php7.2-cgi php7.2-xsl
```

安装完成之后再web跟目录创建一个info.php文件，输入
```text
<?php 
  phpinfo() 
?>
```
然后打开http://127.0.0.1/info.php,你就可以看到下面的界面

![](/images/posts/server/phpinfo.png)

### 安装phpmyadmin
```text
sudo apt-get install phpmyadmin
```
安装过程会让输入数据库密码

安装完之后设置一下软连接
```text
sudo ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin
```