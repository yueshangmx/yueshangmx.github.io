---
layout: post
title: 19.jQuery概述、选择器和DOM操作
date: 2017-09-22
description: "jQuery，JS类库，jQuery选择器"
tags: 笔记   
---

### 1.jQuery概述

JavaScript类库：为了简化JavaScript开发、预定义了很多对象(属性和方法)和函数，并且兼容各大浏览器的js库。

jQuery就是一个JS类库。目前最新版本是jquery-3.2.1。

jQuery包含四个部分：
```
jQuery - Web版本(最主要)
jQuery UI(User Interface) - 集成UI内容
jQuery Mobile - 移动版本(WebApp)
QUnit - 用于测试
```

如何使用jQuery：
```
* 在HTML页面中引入jQuery文件
* 使用jQuery的选择器定位(获取)页面元素
* 利用jQuery的API方法完成需求
```

### 2.基本内容

jQuery的工厂函数：`$(selector)`，此函数返回一个jquery对象。

一般情况下，定义jQuery对象时，在变量前加一个"$"符号，用于区别DOM对象。

DOM对象和jQuery对象：
```
DOM对象 - 通过DOM获取的元素,称之为DOM对象
jQuery对象 - 通过jQuery包装DOM后产生的对象
  * jQuery对象的底层还是DOM对象
```

DOM对象与jQuery对象的转换:
```
DOM对象转换为jQuery对象
  * $(DOM对象)
jQuery对象转换为DOM对象
  * jQuery对象是数组对象 - 角标
  * jQuery对象提供get(index)方法
     * 注意 - DOM对象与jQuery对象之间不能相互调用
```

### 3.jQuery选择器
选择器 - 是jQuery的根基
![](/images/posts/jquery/jquery-selector.png)

### 4.jQuery的DOM操作
- 1.基本操作
```
html() - 类似于原生DOM的innerHTML属性
    获取 - html()
    设置 - html(html代码)
val() - 类似于原生DOM的value属性
    获取 - val()
    设置 - val(value)
text() - 类似于原生DOM的textContent属性
    获取 - text()
    设置 - text(文本内容)
attr() - 获取或设置指定元素的属性
    获取 - attr(attrName) - 类似于getAttribute()
    设置 - attr(attrName,attrValue) - 类似于setAttribute()
removeAttr(attrName) - 类似于removeAttribute()
```

- 2.样式操作

```
attr("class",classValue) - 设置 
addClass() - 追加样式
removeClass() - 删除样式
    * 不传参 - 删除所有样式
    * 传参 - 删除指定样式
toggleClass() - 切换样式
    * 只接受一个参数,是在没有样式与指定样式之间切换
hasClass() - 判断样式
    * 判断指定元素是否包含指定样式
----
css() - 操作样式
  css(name)  -  获取样式
  css(name,value) - 设置单一样式
  css({     - 一次设置多种样式
    name: value,
    name: value,
    ...
  })
```

- 3.遍历节点

```
parent() - 获取指定节点的父节点
children() - 获取指定节点的所有子节点
next() - 获取指定节点的下一个兄弟节点
prev() - 获取指定节点的上一个兄弟节点
siblings() - 获取指定节点的所有兄弟节点
find(expr) - 在指定节点中查找指定内容
  * 注意 - 查找指定节点的后代节点
```
Demo：
```
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>jQuery中的DOM操作-遍历节点</title>
  <script src="jquery-3.2.1.js"></script>
</head>

<body>
<ul id="city">
  <li id="bj" name="beijing">北京
    <ul>
      <li>大兴区</li>
      <li>朝阳区</li>
      <li>海淀区</li>
    </ul>
  </li>
  <li id="tj" name="tianjin">天津</li>
  <li id="nj" name="nanjing">南京</li>
  <li id="sh" name="shanghai">上海</li>
  <li id="cq" name="chongqin">重庆</li>
</ul>
</body>
<script>
  //获取南京节点的父节点
  console.log($("#nj").parent().attr("id"));

  //获取id为city下的所有子节点的个数
  console.log($("#city").children().length);

  //获取南京节点的上一个兄弟和下一个兄弟节点
  console.log($("#nj").prev().attr("name"));
  console.log($("#nj").next().attr("name"));

  //获取难进节点所有兄弟节点
  console.log($("#nj").siblings().length);

  //find()——获取city下所有li的个数
  console.log($("#city").find("li").length);

</script>
</html>
```

- 4.创建节点

```
元素节点 - $(HTML代码)
文本节点 - text()
属性节点 - attr()
```
Demo:
```
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>jQuery中的DOM-创建节点</title>
  <script src="jquery-3.2.1.js"></script>
</head>

<body>
<ul id="city">
  <li id="bj" name="beijing">北京</li>
  <li id="tj" name="tianjin">天津</li>
  <li id="nj" name="nanjing">南京</li>
  <li id="sh" name="shanghai">上海</li>
</ul>
</body>
<script type="text/javascript">
  //为city节点增加<li id="cq" name="chongqin">重庆</li>子节点

  /*原生DOM操作
  var li =document.createElement("li");
  li.setAttribute("id","cq");
  li.setAttribute("name","chongqin");
  li.innerHTML="重庆";
  $('#city')[0].appendChild(li);*/

  //jQuery操作
  var $li = $("<li></li>");
  $li.attr("id", 'cq').attr("name", "chongqin");
  $li.text('重庆');
  $("#city").append($li);

  /*或者一步到位
  $("#city").append('<li id="cq" name="chongqin">重庆</li>');*/
</script>
</html>
```

- 5.删除节点

```
remove() - 删除自身及后代节点
empty() - (清空)删除后代节点,但保留自身节点
```
Demo:
```
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>05.jQuery中的DOM-删除节点</title>
  <script src="jquery-3.2.1.js"></script>
</head>

<body>
<ul id="city">
  <li id="bj" name="beijing">北京
    <ul>
      <li>大兴区</li>
      <li>朝阳区</li>
      <li>海淀区</li>
    </ul>
  </li>
  <li id="tj" name="tianjin">天津
    <ul>
      <li>塘沽</li>
    </ul>
  </li>
  <li id="nj" name="nanjing">南京</li>
  <li id="sh" name="shanghai">上海</li>
  <li id="cq" name="chongqin">重庆</li>
</ul>
</body>
<script>
  //删除北京节点
  $("#bj").remove();

  //删除天津节点
  $("#tj").empty();
</script>
</html>
```