---
layout: post
title: 11.JavaScript的Math、Date对象
date: 2017-08-27
description: "JavaScript，Math，Date，API，JS对象"
tags: 笔记   
---

### Math
Math对象：专门执行数学计算的对象，封装了数学计算中常用的常量。

- 1.取整: 3种
```
上取整：Math.ceil(n)
下取整：Math.floor(n)
四舍五入取整：Math.round(n)
   
	round vs toFixed
toFixed： Number对象——按任意小数位数，返回的是字符串
round：  Math对象——只能取整数，返回数字
```
- 2.乘方/开平方
```
乘方：Math.pow(n,m)：计算n的m次方
开平方：Math.sqrt(n)：计算n的平方根
```
- 3.取最大值和最小值
```
最大值：Math.max(a,b,c…);
最小值：Math.min(a,b,c…);
`固定套路：变相实现获取数组中的最大值，获取最小值同理`
Math.max.apply(Math,arr)==》相当于Math.max(arr[0],arr[1]......)
```
- 4.随机数
```
Math.random()，0<=n<1
任意min到max之间取一个随机整数
parseInt(Math.random()*(max-min+1)+min)
```

### Date
Date对象: 封装了一个时间点，提供了对时间和日期的操作API。Date中封装了 从1970年1月1日0点0分0秒至今的毫秒数。

- 1.创建Date对象方法：4种
```
（1）var now=new Date(); ——创建一个新日期对象同时，保存客户端当前时间点的毫秒数。——获得当前时间
自定义时间对象：
（2）var time=new Date(“xxxx/xx/xx [xx:xx:xx]”);
（3）var time=new Date(年,月-1,日[,时,分,秒]);
	date.getTime()：获得日期对象中的毫秒数
（4）复制日期对象
      var date1=new Date();
      var date2=new Date(date1.getTime());  //new Date(毫秒数)
      date2.setXXX(date2.getXXX()+-n)
```
- Date API
```
Date();		#返回当日的日期和时间。 
获取：
getDate();	#从 Date 对象返回一个月中的某一天 (1 ~ 31)。 
getDay();	#从 Date 对象返回一周中的某一天 (0 ~ 6)。 
getMonth();	#从 Date 对象返回月份 (0 ~ 11)。 
getFullYear();	#从 Date 对象以四位数字返回年份。  
getHours();	#返回 Date 对象的小时 (0 ~ 23)。 
getMinutes();	#返回 Date 对象的分钟 (0 ~ 59)。 
getSeconds();	#返回 Date 对象的秒数 (0 ~ 59)。 
getMilliseconds();	#返回 Date 对象的毫秒(0 ~ 999)。 
getTime();	#返回 1970 年 1 月 1 日至今的毫秒数。
设置：
setDate();	#设置 Date 对象中月的某一天 (1 ~ 31)。 
setMonth();	#设置 Date 对象中月份 (0 ~ 11)。 
setFullYear();	#设置 Date 对象中的年份（四位数字）。 
setHours();	#设置 Date 对象中的小时 (0 ~ 23)。 
setMinutes();	#设置 Date 对象中的分钟 (0 ~ 59)。 
setSeconds();	#设置 Date 对象中的秒钟 (0 ~ 59)。 
setMilliseconds();	#设置 Date 对象中的毫秒 (0 ~ 999)。 
setTime();	#以毫秒设置 Date 对象。 
```
`每个分量都有一对儿get/set方法`

`星期没有set方法！`

`只有月中的日从1开始到31结束; 其它分量都是从0开始到减1结束`

日期的计算：<br>
　　1. 两日期对象直接相减，结果是毫秒差！<br>
　　2. 对任意分量做加减：先用get取出来,计算后，再set放回去。<br>

*直接修改原日期对象 - `date.setXXX(date.getXXX()+-n)`

日期转字符API
```
1. date.toLocaleString(); 转为完整日期字符串
2. date.toLocaleDateString(); 仅转为日期部分
3. date.toLocaleTimeString(); 仅转为时间部分   
```


