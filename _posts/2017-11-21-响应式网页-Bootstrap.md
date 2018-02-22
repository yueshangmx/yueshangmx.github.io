---
layout: post
title: 24.Bootstrap响应式网页
date: 2017-11-21
description: "响应式网页，Bootstrap，viewport"
tags: 笔记   
---

### 1.响应式网页
#### 1.响应式/自适应网页：一个页面，可以在各种不同的设备下浏览，都有不错的浏览体验。

<strong>响应式网页的特点：</strong>
```
(1)流式布局
(2)可伸缩的图片和字体(浏览器默认字体是16px，门户网站14px，移动端10px)
(3)CSS3 Media Query
```

#### 2.如何编写响应式网页
```$xslt
(1)设置viewport元标签
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
(2)避免使用绝对单位(px)，用相对单位代替(%、auto、em等)
(3)使用流式定位：float
(4)图片大小实现自适应：
  img {  max-width: 100%;  }
  会随着容器的改变而改变，且不会超过图片自身原始大小，防止失真。
(5)根据浏览器屏幕的特征，有选择性的执行某些CSS样式——CSS3媒体查询技术(Media Query)
```
#### 3.如何测试响应式网页
```$xslt
(1)使用真实物理设备——效果可靠但任务量太大
  只要手机/平板/PC在同一个局域网/互联网即可测试。
(2)使用第三方测试/模拟软件——效果有待进一步的验证
(3)使用Chrome自带的浏览器模拟器测试
  优势：可以模拟常见的设备、网速、经纬度、加速度....
  不足：效果有待进一步的验证
```

#### 4.CSS3提供的Media Query技术
`作用`：根据客户端浏览设备的特性，有选择性的执行部分CSS

`Media`：指浏览网页的设备，如screen(pc/pad/phone)、print、tv、projection、屏幕阅读器.....

`Query`：查询出当前浏览设备的特性，如类型、宽度、高度、分辨率、色彩位深、方向Orientation(Landscape/Portrait)，根据这些特性，执行特定的CSS样式。

CSS3MediaQuery有两种用法：
```$xslt
(1)根据媒体的特性，执行不同的外部CSS：
  <link media="screen and (min-width:768px) and (max-width: 990px)" rel="stylesheet" href="xx.css">
  不足：客户端会不管媒体特性，请求所有的CSS文件。
----
(2)根据媒体的特性，执行某段CSS中的部分内容：
  @media screen and (min-width:768px) and (max-width:990px) {
    h1 {  ...  }
    .box {  ...  }
  }
```

### 2.Twitter Bootstrap
`Bootstrap( bootcss.com )是一个框架HTML/CSS/JS框架，适用于移动设备优先的响应式网页。`

Bootstrap分为五部分：
```
(1)起步(Startup)
(2)全局CSS样式(Global CSS)
(3)组件(Component)
(4)插件(Plugin)
(5)定制(Customize)
```
##### 实际开发中，html标签通常会添加`lang`属性，其作用是：

`(1)告诉浏览器翻译时如何确定当前网页的基础语言` 

`(2)告诉读屏软件当前页面的基础发音`
