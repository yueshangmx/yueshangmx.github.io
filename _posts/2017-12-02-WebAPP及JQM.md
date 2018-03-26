---
layout: post
title: 26.WebAPP及jQuery Mobile
date: 2017-12-02
description: "WebAPP，JQM，jQuery Mobile"
tags: 笔记   
---

### 1.WebAPP

WebApp：指使用HTML5编写的移动Web应用。一个WebApp几乎可以不加修改的运行在PC、Android、iOS等平台。

- 优势：一套代码到处运行。
- 劣势：某些底层功能缺失，运行速度不如原生App。


#### Android开发环境的搭建

- (1)下载并安装配置Java程序的运行环境——JDK（JavaDevelopmentKit）
- (2)下载并解压缩Android应用的开发环境 —— 由于ADT已经不在更新，这里推荐使用[Android Studio](http://www.android-studio.org/index.php/component/content/category/88-download)。
- (3)启动Android Studio,新建一个android studio项目
![](/images/posts/webapp/1.png)
![](/images/posts/webapp/2.PNG)
![](/images/posts/webapp/3.PNG)
![](/images/posts/webapp/4.PNG)
![](/images/posts/webapp/5.PNG)
![](/images/posts/webapp/6.PNG)
- (4)新建一个android虚拟机
![](/images/posts/webapp/avd.png)
![](/images/posts/webapp/avd-1.PNG)
![](/images/posts/webapp/avd-2.PNG)
![](/images/posts/webapp/avd-3.PNG)
![](/images/posts/webapp/avd-4.PNG)
![](/images/posts/webapp/avd-5.PNG)


### 2.JQuery Mobile

#### 框架整理
- (1)jQuery是一个JS函数库，简化了DOM&AJAX操作，本质与DOM相同   WriteLess，DoMore。
- (2)jQueryUI是一个HTML组件库，丰富了HTML的功能。
- (3)Twitter Bootstrap是一个HTML/CSS/JS框架，简化了响应式网页的编写，提供了栅格系统+CSSReset+HTML组件。
- (4)Google AngularJS是一个JS框架，改变了网页的编写方式，适用于以数据操作为主的SPA应用。(已逐渐被Vue和react等框架代替)
- (5)jQuery Mobile是一个HTML组件库，适用于移动App的开发。


#### (1)JQM主要内容

JQM主要内容可以分为四个部分：

- (1)页面&导航
- (2)CSS框架
- (3)组件
- (4)表单组件

#### (2)使用JQM步骤
```textmate
(1)项目中引入jquery 1.8+
(2)项目中创建jqm目录，引入jqm必需资源文件
  jquery-mobile.css
  jquery-mobile.js
  images/....
(3)创建HTML页面，引入必需的css和js
(4)body中的data-role="page" 元素
```

##### 提示

- (1)jQM的HTML文件中，body中必须至少有一个Page,若用户未提供，jqm自动添加；
- (2)body中可以声明多个Page，但默认只有第一个可以显示。
- (3)jQM中所有的网页内容不能直接置于body中，必须置于Page中。
- (4)jQM中所有的样式都是通过预定义的class来设置的，开发者可以直接指定元素的class，也可以为元素指定data-*扩展属性来实现让jqm添加class的功能。

#### (3)页面跳转和过场动画

- (1)页面跳转可以使用<a>、<button>、<input type="button">等元素，推荐使用<a>——会自动添加过场动画。
- (2) 可以跳转到外部的完整HTML页面；也可以跳转到当前HTML中的另一个Page，

##### jQM为页面切换添加了非常丰富的过渡动画
```textmate
使用方法：
  <a href="目标页面" data-transition="动画效果名称">
可用的动画效果有：
  fade、pop、slide、slideup、slidedown、slidefade、turn、flip、flow、none
```

#### (4)按钮（Buttons)
```textmate
(1)可以使用A、BUTTON、INPUT元素实现按钮的样式
(2)可以使用data-role="button"属性实现按钮样式；也可以指定class实现按钮样式，如.ui-btn .ui-corner-all .ui-shadow
(3)按钮默认是块级显示，可以使用.ui-btn-inline实现行内按钮
(4)按钮上可以有文字和图标；若存在图标，必须指定与文字的位置关系；可选值：
    .ui-btn-icon-left
    .ui-btn-icon-right
    .ui-btn-icon-bottom
    .ui-btn-icon-top
    .ui-btn-icon-notext
(5)按钮可以置于Page的Header中
Header中的第一个按钮默认处于左侧，第二个默认处于右侧，一般只放两个。
  <div data-role="header">
    <a href="#">文字</a>    /*默认就是按钮效果*/
  </div>
```

#### (5)导航条(navbar)

```textmate
基本结构：
  <div data-role="navbar">
    <ul>
      <li><a href="#"></a></li>
      <li><a href="#"></a></li>
    </ul>
  </div>
----
说明：
(1)导航条中一般最多只能有5个项目，超过5个会在一行中只显示2个；
(2)导航条可以出现在Page的Header、Main、Footer中；
(3)处于Header和Footer中navbar默认会占满整行，并和标题字错开。
```

#### (6)Loader(加载器)
```textmate
显示"加载中"图片：  $.mobile.loading('show');
隐藏"加载中"图片：  $.mobile.loading('hide');
```

#### (7)Panel(面板)
```textmate
注意：面板在目前版本的jqm中只能放在Page中，Header之前或Footer之后
  <div data-role="page">
    <div data-role="panel" id="p1">...</div>
    <div data-role="header">...</div>
    <div><a href="#面板ID">打开面板</a></div>
    <div data-role="footer">...</div>
  </div>
面板组件可以指定出现位置：  data-position="left / right"
以及打开方式：data-display="reveal / overlay / push"
```