---
layout: post
title: 22.SERVER & HTTP
date: 2017-11-12
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

PHP是类似于javascript语言的适用于服务器端的脚本语言，PHP文件不能以本地文件打开，应该运行在服务器端。

PHP页面是动态页面，可以根据用户的操作，动态变化。而HTML页面内是静态页面，加载的静态资源。

#### PHP语法

(1)常量与变量

常量使用const关键字定义：`const 常量名 = 值`

变量使用"$"符号：`$变量名 = 值`

(2)数据类型
```
四种标量类型
    * boolean - 布尔类型
    * integer - 数值类型(整型)
    * float/double - 数值类型(浮点型)
    * string - 字符串
        * '' - 定义固定字符串 : 性能比较高
        * "" - 可以识别变量名的 : 性能相对低(有匹配的过程)
两种复合类型
    * array - 数组
    * object - 对象
两种特殊类型
    * resource - 资源
        * 作用 - 用于保存外部资源的一个引用
        * 使用场景 - 在文件上传中,保存上传的文件
    * NULL
```

(3)运算符

PHP语言的运算符基本与JavaScript的保持一致，只有字符串拼接时使用的`.`,不是`+`。

(4)循环结构
```
* while
* do...while
* for
* foreach
   foreach(数组 as key => value){}
```

(5)分支结构
```
if...else if...else
----
switch...case
```

#### PHP预定义

预定义变量
```
* $_GET - 接收客户端以请求类型为GET方法发送的数据内容
* $_POST - 接收客户端以请求类型为POST方法发送的数据内容
* $_REQUEST - $_GET、$_POST等
* $_FILES - 专门用于文件上传
* $_COOKIE - 接收客户端保存的Cookie数据
```

预定义函数 - 数据库扩展

#### PHP连接MySQL数据库

(1)过程化风格
```
建立与MySQL数据库的连接
    $conn = mysqli_connect(host,username,passwd,dbname,port); - 返回数据库的连接对象
定义SQL语句
         $sql = "";
发送SQL语句 - MySQL数据库
    $result = mysqli_query($conn,$sql); - 返回执行SQL语句的结果
(可选)解析结果集对象
    * 结果集对象 - mysqli_result对象
关闭与MySQL数据库的连接
         mysqli_close($conn)
```
(2)面向对象风格
```
创建mysqli或mysql对象
    $mysqli = new mysqli(host,username,passwd,dbname,port);
        相当于与MySQL数据库建立连接
定义SQL语句
    $sql="";
调用mysqli对象的query()方法,向MySQL数据库发送SQL语句
         $mysqli->query($sql);
如果SELECT语句,解析mysqli_result对象
调用mysqli对象的close()方法,关闭与MySQL的连接
```
中文乱码问题

       * 执行mysqli_query($conn,'SET NAMES UTF8');
       * 执行$mysqli->query('SET NAMES UTF8');

(3)结果集对象的解析（执行SELECT语句）
```
属性
    * num_rows - 记录数量
    * field_count - 字段数量
方法
    * mysqli_fetch_array(结果集对象) - 返回数组
    * mysqli_fetch_object(结果集对象) - 返回object
```

### 4.HTTP协议

URL概念：
```
URL - 统一资源定位符
URI - 统一资源标识符
* URL与URI的区别
    所有的URL都是URI,但URI不一定是URL
```

完整的URL包括以下几个部分：<br>
网络协议:IP地址(虚拟地址):端口号/路径;参数?查询数据#锚点<br>
http://127.0.0.1:8080/HTTP;JSESSION=123123213?key=value#mylink

#### 网络协议

网络协议是指客户端和服务器端之间的协议。

目前主流的协议为`http协议`-https加密协议、`socket协议`-H5的web socket、`ftp协议、pop3协议`等。

#### HTTP协议

http协议多用于B/S架构。目前最新版本为2.0，主流版本为1.1版本。

http协议的一些问题
```
短连接
    * 每次客户端与服务器端交互时,先建立连接,交互完毕后,关闭链接
无状态
    * 服务器端只能记得住当次请求状态
```

#### HTTP之请求消息Request

- `GET请求方式`

![](/images/posts/http/get.png)

<strong>第一部分：请求行，用来说明请求类型,要访问的资源以及所使用的HTTP版本.</strong>

GET说明请求类型为GET,[server.php]为要访问的资源，该行的最后一部分说明使用的是HTTP1.1版本。

<strong>第二部分：请求头部，紧接着请求行（即第一行）之后的部分，用来说明服务器要使用的附加信息</strong>

从第二行起为请求头部
```
Accept - 表示服务器端接受的MIME类型
Accept-Encoding - 表示服务器端是否接受压缩
    * gzip - 是指一种服务器端的压缩格式
    * 问题 - 客户端请求的数据内容越大
        * 对网络带宽的要求越高,流量占用大
        * 用户体验不好 - 速度慢、对服务器造成的压力大
Accept-Language - 表示服务器端接受的语言
    * zh-CN - 简体中文
    * zh-TW - 繁体中文
    * zh - 中文
    * us - 英文
Connection - 表示当前的连接状态
	   * keep-alive - 表示保持连接
Host - 表示当前电脑的地址(IP:端口号)
Referer - 表示当前的请求来源于哪里
	   http://127.0.0.1/6.server/day03/index.html - 实现防盗链接
User-Agent - 获取用户的浏览器信息
	   Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/64.0.3282.119 Safari/537.36
Cookie - 将Cookie自动携带请求头
```
<strong>第三部分：请求数据也叫主体，可以添加任意的其他数据。</strong>

这个例子的请求数据为`user:123`。


- `POST请求方式`

![](/images/posts/http/post.png)

第一部分：请求行，第一行明了是post请求，以及http1.1版本。

第二部分：请求头部。
```
Cache-Control - 缓存控制
    * max-age=0 - 设置缓存最大活动周期
        * 0 - 表示没有缓存
        * 设置缓存保存的最大时间的单位为毫秒/秒
Content-Length - 请求数据的长度(大小)
Content-Type - 请求的MIME类型
    * application/x-www-form-urlencoded
        * <form>元素提交请求时默认的类型
        * 一般文件上传时,类型一定这种格式
```

第三部分：请求数据。

- `响应(Response)协议`

![](/images/posts/http/response.png)
```
响应行 - HTTP/1.1 200 OK
    * 状态码
    * 协议版本
响应头
    * Connection - 表示当前的连接状态
        * keep-alive - 表示保持连接
    * Content-Length - 响应数据的长度(大小)
    * Content-Type - 响应数据的MIME类型
        * 一般情况下 - text/html格式
        * 设置响应页面编码 - charset=UTF-8
    * Date - 响应的日期时间
        Sat, 03 Feb 2018 10:02:57 GMT
        yyyy-MM-dd hh:mm:ss
        yyyy年MM月dd日 hh:mm:ss
    * Keep-Alive - 设置保持连接的超时和最大存活时间
        * timeout=5, max=99
        * 一般都是在Connection的值设置为keep-alive时
    * Server - 响应服务器端的信息
        Apache/2.4.10 (Win32) OpenSSL/1.0.1i PHP/5.6.3
响应体
     * 服务器端向客户端进行响应的数据内容
```




### 5.扩展内容
#### 请求类型 - 请求类型至少有七种(面试题)
```
* GET - 最常使用的
* POST - 最常使用的
* HEAD
* PUT
* DELETE
* OPTIONS
* TRACE
```

#### 状态码
```
状态代码有三位数字组成，第一个数字定义了响应的类别，共分五种类别:
---
1xx：指示信息--表示请求已接收，继续处理
2xx：成功--表示请求已被成功接收、理解、接受
3xx：重定向--要完成请求必须进行更进一步的操作
4xx：客户端错误--请求有语法错误或请求无法实现
5xx：服务器端错误--服务器未能实现合法的请求

常见状态码：
200 OK                        //客户端请求成功
400 Bad Request               //客户端请求有语法错误，不能被服务器所理解
401 Unauthorized              //请求未经授权，这个状态代码必须和WWW-Authenticate报头域一起使用
403 Forbidden                 //服务器收到请求，但是拒绝提供服务
404 Not Found                 //请求资源不存在，eg：输入了错误的URL
500 Internal Server Error     //服务器发生不可预期的错误
503 Server Unavailable        //服务器当前不能处理客户端的请求，一段时间后可能恢复正常
```
更多<a href="http://www.runoob.com/http/http-status-codes.html" target="_blank">状态码</a>

#### MIME类型
```
常见的MIME类型
    * html - text/html
    * htm  - text/html
    * xhtml- application/xhtml+xml
    * css  - text/css
    * js   - application/javascript text/javascript
    * json - application/json
    * jpg  - image/jpeg
    * jpeg - image/jpeg
    * png  - image/png
    * text - text/plain
    * webm - video/webm
    * mp4  - video/mp4
```

####  GET与POST请求方式的请求协议的区别
```
GET请求方式
    * 请求行
        * 请求类型 - GET
        * 请求地址 - URL?请求参数
    * 请求体 - 空
POST请求方式
    * 请求行
        * 请求类型 - POST
        * 请求地址 - URL
    * 请求体
        * 请求参数
```
请求参数
```
GET请求类型
    * 将请求数据 - URL?key=value(浏览器地址栏) - 安全相对比较低
    * 请求地址的长度是有限制的 - 请求数据内容过多
    * 如果请求数据中包含中文的话,需要转码的 - 容易出现中文乱码问题
POST请求类型
    * 浏览器地址栏URL,不包含请求类型 - 安全相对比较高
    * 请求数据在请求体中 - 对请求数据的大小(长度)没有要求
    * 如果请求数据中包含中文的话,可以不转码 - 相对来讲对于中文的处理比较好
```