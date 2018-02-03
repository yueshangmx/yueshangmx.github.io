---
layout: post
title: 22.SERVER & HTTP
date: 2017-11-02
description: "server，服务器，HTTP，PHP"
tags: 笔记   
---

### 1.服务器server
#### 1.服务器的分类

- 硬件服务器 - PC机<br>
       * 电脑硬件 - PC机/小型机/刀片机/中型机/大型机/超级计算机<br>
       * 小型机 - IBM(AIX)/HP/联想(Linux)
- 软件服务器 - 中间件<br>
       * 为了运行Web应用的一种软件

#### 2.软件架构
```
B/S - 浏览器(browser)/服务器端(server)
  互联网-企业级(网易、腾讯、百度等)
  企业级 - 银行系统、医院系统等
  好处-软件升级 - 服务器端的升级
----
C/S - 客户端(client)/服务器端(server)
  先出现,例如QQ、Email等
  原因 - 网络带宽/电脑硬件普遍偏低
  问题:软件升级 - 客户端\服务器端都要升级
```

#### 3.XAMPP搭建本地软件服务器（Apache、MySQL）

访问：`http://localhost:端口号`或者`http://127.0.0.1:端口号`

#### 4.MySQL - 数据库服务器

MySQL默认端口 - 3306

命令行方式登录(打开)数据库
```
登录数据库 - mysql -u用户名 -p密码
退出数据库 - exit;
```

### 2.数据库
数据库 - 数据仓库,用于存储或操作数据内容

数据库分为`关系型数据库`和`非关系型数据库`
```
关系型数据库(SQL) - 是目前主流数据库
  * 是以表(行和列)的形式存储数据
  主流产品：
    Oracle - 甲骨文(Oracle)公司的产品: 企业级开发98%市场份额都是使用这款产品
    MySQL - 甲骨文(Oracle)公司的产品: 互联网开发98%市场份额都是使用这款产品
    SQL Server - 微软公司推出的:  只提供Windows操作系统版本
----
非关系型数据库(NoSQL) - 是新潮流数据库
  * 是以文档方式存储数据
  * 是以key:value形式存储数据
  主流产品：mongoDB - JSON格式
```

#### SQL语言
```
* DDL - 数据定义语言(数据库+表)
* DCL - 数据控制语言(权限)
* DQL - 数据查询语言
* DML - 数据操作语言
----
注意
  * SQL语言并不区分大小写(官方建议大写)
  * SQL语句编写完毕后,一定增加";"结束符
  * 命令行中SQL语言使用字符串时,建议使用单引号'
```
- DDL(了解)<br>
(1) 数据库操作

```
创建数据库
    CREATE DATABASE 数据库名称 DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
查看数据库
    SHOW DATABASES;
修改数据库
    ALTER DATABASE 数据库名称 CHARACTER SET utf8;
删除数据库
    DROP DATABASE 数据库名称;
使用(切换)数据库
    USE 数据库名称;
----
* 注意
    * 数据库一旦被创建,很少修改或删除
    * 创建、查看和切换数据库
```
(2) 数据表操作

1) 数据类型
```
数值(Number)数据类型
    * INT - 整数
    * FLOAT/DOUBLE - 浮点型(小数)
    * DECIMAL - 精确值(金额等)
日期(Date)数据类型
    * DATE - 日期(默认格式:yyyy-MM-dd)
    * DATETIME - 日期时间(yyyy-MM-dd hh:mm:ss)
    * TIMESTAMP - 时间戳(标识:唯一)
字符串(String)数据类型
    * CHAR - 长度固定的字符串
    * 定义一个字符串的长度为10,实际存储的内容为"abc",未被字符占用的位置会以空格补位
    * VARCHAR - 长度可变的字符串
    * 定义一个字符串的长度为10,实际存储的内容为"abcde"
```
2) 表操作
```
创建数据表
    CREATE TABLE (
        字段名称1  数据类型,
        字段名称2  数据类型,
        ...
    );
    * 主键约束 - PRIMARY KEY：作用 - 唯一,不可重复
    * 主键自增约束 - AUTO_INCREMENT：作为主键的字段,自增
删除数据表
    DROP TABLE 表名;
查看表结构
    DESC 表名;
```

- DML(增删改)

```
插入(新增)数据
    用法一: INSERT INTO 表名 VALUES(字段值1,字段值2,...);
      * 注意
	    * 当前表具有多少字段,VALUES输入多少字段值
	    * 如果哪个字段是主键自增的话,使用NULL补位
    用法二: INSERT INTO 表名(字段名1,字段名2,...) VALUES(字段值1,字段值2,...)
      * 注意
	    * 表名后定义多少字段,VALUES后输入多少字段
	    * 当前数据表的字段是允许为空的
----
更新(修改)数据
    用法一 : UPDATE 表名 SET 字段名=字段值;
        * 注意 - 修改所有数据(指定字段值)
    用法二 : UPDATE 表名 SET 字段名=字段值 WHERE 字段名=字段值;
	    * SET后面的"字段名=字段值",为设置的值
	    * WHERE后面的"字段名=字段值",为查询的值
    用法三 : UPDATE 表名 SET 字段名1=字段值1,字段名2=字段值2 WHERE 字段名=字段值;
----
删除数据
    用法一 : DELETE FROM 表名;
        * 注意 - 删除指定表中所有数据
    用法二 : DELETE FROM 表名 WHERE 字段名=字段值;
        * 问题: 实际的开发中基本不使用DELETE语句,以防用户反悔
    * SQL操作(删除)
      物理删除 - 执行DELETE语句
      逻辑删除
        * 简单来说,对于用户来讲是删除的,对于实际来讲并没有删除
        * 为指定表,增加一个字段(state/status),表示当前这条记录是什么状态
          * 值为1的话,表示这条记录是正常的;值为0的话,表示这条记录是删除的
```
- DQL(查)

```
基本查询 - 新版本一样
    用法一 : SELECT * FROM 表名;
    用法二 : SELECT 字段名1,字段名2,... FROM 表名;
条件基本查询
    用法 : SELECT * FROM 表名 WHERE 字段名=字段值;
复杂条件查询
    * AND - 表示多个条件同时满足
    * OR - 表示其中一个条件满足
    * IN(SET) - 表示一个字段包含多个值
       * SET - 多个值,之间使用","
    * = - 表示字段值为指定值
    * BTWEEN AND - 等于 >= AND <=
    * IS NULL - 匹配NULL值
排序查询 - ORDER BY 字段名
    * ASC - 正序排序,默认值
    * DESC - 倒序排序
    SELECT * FROM 表名 WHERE 条件 ORDER BY 字段名;
```

### 3.PHP语言