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


### 2.JQuery Mobile 概述

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

### 3.JQM提供的组件

#### (1)页面跳转和过场动画

- (1)页面跳转可以使用`<a>`、`<button>`、`<input type="button">`等元素，推荐使用`<a>`——会自动添加过场动画。
- (2) 可以跳转到外部的完整HTML页面；也可以跳转到当前HTML中的另一个Page，

##### jQM为页面切换添加了非常丰富的过渡动画
```textmate
使用方法：
  <a href="目标页面" data-transition="动画效果名称">
可用的动画效果有：
  fade、pop、slide、slideup、slidedown、slidefade、turn、flip、flow、none
```

#### (2)按钮（Buttons)
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

#### (3)导航条(navbar)

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

#### (4)Loader(加载器)
```textmate
显示"加载中"图片：  $.mobile.loading('show');
隐藏"加载中"图片：  $.mobile.loading('hide');
```

#### (5)Panel(面板)
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
##### 关于jqm Page的切换
```text
(1)一个HTML声明多个Page
    不足：即使不显示的Page，初始时也会被客户端请求下来。
(2)一个HTML只声明一个Page，通过超链接进行页面跳转
    1)jQM已经完全改写了超链接的默认行为——把同步请求转为异步AJAX请求
    2)异步请求得到的HTML页面，只会保留其中的第一个Page，添加到当前DOM树上；其它所有内容全部删除！
    3)推荐一个项目中只有起始页是完整的HTML页面，其它被跳转到的页面都是HTML片段——只包含一个PAGE的声明。
    4)注意：基于上面的原因，jQM项目中所有的HTML页面中元素的id应该是全局唯一的！
```

#### (6)折叠组件(Collapsible)和手风琴效果(CollapsibleSet)
```textmate
折叠组件：
  <div data-role="collapsible">
    <h3>标题字</h3>
    <div>折叠的内容</div>
  </div>
折叠组件集合——手风琴效果
  <div data-role="collapsibleset">
    <div data-role="collapsible"></div>
    <div data-role="collapsible"></div>
  </div>
```

#### (7)网格布局系统——Grids
```text
(1)jqm提供的布局系统没有预定义margin或padding
(2)jqm中的"行"分为五种：  
  默认				一行中只有一列，列宽100%
  .ui-grid-a			一行中有二列并等分，列宽50%
  .ui-grid-b			一行中有三列并等分，列宽33%
  .ui-grid-c			一行中有四列并等分，列宽25%
  .ui-grid-d			一行中有五列并等分，列宽20%
(3)jqm一行中列依次排序为：
  第一列：  .ui-block-a
  第二列：  .ui-block-b
  第三列：  .ui-block-c
  第四列：  .ui-block-d
  第五列：  .ui-block-e
(4)jqm中所有的.ui-block-a必须重起一行。
(5)jqm中一行默认只能等分为N列，若想不等分，只能自定义样式。
(6)列中若放置<button>则默认填满整列；若是超链接或INPUT按钮，默认会添加左右margin:5px;
```

#### (8)响应式表格——table

真正的响应式表格有两种：
```text
(1)回流(reflow)模式的响应式表格
  <table data-role="table" class="ui-responsive" data-mode="reflow">
  ...
  </table>
屏幕够宽时显示效果与普通表格相同；不够宽时每一行数据都会独立显示。
----
(2)列切换(column toggle)模式的响应式表格
  <table data-role="table" class="ui-responsive" data-mode="columntoggle">
    <thead>
      <tr>
        <th>必须显示的列</th>
        <th data-priority="6">优先级最低(最先被隐藏)的列</th>
        <th data-priority="5">优先级次低(次先被隐藏)的列</th>
        ...
        <th data-priority="1">优先级最高(最后被隐藏)的列</th>
      </tr>
    </thead>
  </table>
```

#### (9)ListView（列表组）
```html
<ul/ol  data-role="listview">
  <li>...</li>
</ul/ol>
```

#### (10)表单组件
```text
TextInput组件：
  单行文本输入域:
    <form>
       <label for="text-1">Text input:</label>
       <input type="text" name="text-1" id="text-1" value="">
       <label for="text-3">Text input: data-clear-btn="true"</label>
       <input type="text" data-clear-btn="true" name="text-3" id="text-3" value="">
    </form>
  多行文本输入域:
    <form>
        <label for="textarea-1">Textarea:</label>
        <textarea name="textarea-1" id="textarea-1"></textarea>
    </form>
  下拉框:
    <form>
         <label for="date-1">Date: data-clear-btn="false"</label>
         <input type="date" data-clear-btn="false" name="date-1" id="date-1" value="">
    </form>
----
特殊的Form控件：
  滑块控件：
    <input type="range">
  开关控件：
    <select data-role="slider">
      <option></option>
      <option></option>
    </select>
  单选按钮组：
    <fieldset data-role="controlgroup" data-type="vertical/horizontal">
      <legend>提示文字</legend>
      <input type="radio">
      <label></label>
    </fieldset>
  复选按钮组：
    <fieldset data-role="controlgroup" data-type="vertical/horizontal">
      <legend>提示文字</legend>
      <input type="checkbox">
      <label></label>
    </fieldset>
```

### 4.JQM扩展了标准的事件
```text
orientationchange:	浏览设备的方向改变
pagebeforeload: jQM使用AJAX异步加载一个Page之前
pageload: jQM使用AJAX异步加载一个Page
pagebeforecreate: jQM Page创建之前——挂到DOM树之前
pagecreate：jQM Page被创建——挂到DOM树
pageinit：jQM Page开始初始化——挂到DOM树后开始初始化
pagechange: jQM 当前Page发生改变，且切换动画完成之后
swipe：手指在屏幕上滑动
swipeleft：手指在屏幕向左滑动
swiperight: 手指在屏幕向右滑动
tap: 手指在屏幕上轻击一下
taphold：手指在屏幕上敲击并保持一小段时间
----
----
提示：上述事件监听函数的绑定不能直接写在HTML中，只能使用jQuery提供的事件绑定函数来实现：
$(...).on('swipeleft', fn);
----
----
面试题：jQM中提供的几个page相关事件触发顺序：
   pagebeforeload -> pageload -> pagebeforecreate -> pagecreate ->pageinit -> pagechange
```
