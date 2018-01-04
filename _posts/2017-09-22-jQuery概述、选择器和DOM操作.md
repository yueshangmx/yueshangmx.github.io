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
1.选择器 - 是jQuery的根基
![](/images/posts/jquery/jquery-selector.png)

