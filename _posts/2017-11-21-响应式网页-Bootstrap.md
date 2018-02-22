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

##### IE浏览器的兼容性问题：
```$xslt
X-UA-Compitable:  Cross-UserAgent-Compatible，该元标签只有IE浏览器支持。
<meta http-equiv="X-UA-Compatible" content="IE=edge">
      设置IE的兼容模式为edge——最新版，尽可能向行业标准看齐。
```

### 3.Bootstrap全局CSS样式

#### 1.CSS Reset

##### Bootstrap默认提供了很多的样式重置
```
* { box-sizing: border-box; }
body { font ...; color: #333; background: ...; margin: 0;}
h1 { font-size: ;  margin-top: 20px;  margin-bottom: 10px;}
h2 { font-size: ;  margin-top: 20px;  margin-bottom: 10px;}
h3 { font-size: ;  margin-top: 20px;  margin-bottom: 10px;}
h4 { font-size: ;  margin-top: 10px;  margin-bottom: 10px;} 		
h5 { font-size: ;  margin-top: 10px;  margin-bottom: 10px;} 	
h6 { font-size: ;  margin-top: 10px;  margin-bottom: 10px;} 	
a { color:;  text-decoration: ;}
img { border: 0;  vertical-align: middle; }
p { margin-bottom:10px; }
......
```

##### 重新设置了CSS3盒子模型的计算方法，将`box-sizing`的值由默认值`content-box`改为`border-box`。
```$xslt
content-box: 一个盒子的总宽度=margin+border+padding+width
border-box: 一个盒子的总宽度=margin+width
```

#### 2.Bootstrap全局CSS样式——按钮
```text
.btn { padding:;  border: ;}
.btn-default { color:;  background:;  border-color:;}
----------------------
.btn-danger
.btn-success
.btn-warning
.btn-info
.btn-primary
---------------------
.btn-lg
.btn-sm
.btn-xs
----------------------
.btn-block
----------------------
.pull-left { float: left; }
.pull-right { float: right; }
```

#### 3.Bootstrap全局CSS样式——图片
```text
.img-rounded
.img-circle
.img-thumbnail	#缩略图片
.img-responsive  #响应式图片
```

#### 4.Bootstrap全局CSS样式——排版和代码——仅作了解
```text
 .text-danger
 .text-success
 .text.warning
 .text-info
 .text-primary
--------
 .bg-danger
 .bg-success
 .bg-warning
 .bg-info
 .bg-primary
--------
 .text-left
 .text-right
 .text-center
 .text-justify  #文本两端调整对齐
--------
 .text-uppercase  
 .text-lowercase
 .text-capitalize
--------
 .list-unstyled
 .list-inline    
```

#### 5.Bootstrap全局CSS样式——表格
```text
.table
.table-bordered		带边框的表格
.table-responsive		响应式表格  注意：使用在table的父元素上，而不是table上
.table-striped		隔行变色的表格
.table-hover			带悬停效果的表格
```

#### 6.Bootstrap全局CSS样式——栅格布局系统——重点

##### Web开发中页面布局可以采用的方式：
```$xslt
(1)使用TABLE做布局
  优势：简单不易出错  不足：加载效率
(2)使用DIV+CSS做布局
  优势：加载速度快、灵活	 不足：不易控制
(3)使用Bootstrap提供的栅格(Grid Layout)布局系统
  优势：加载速度快、灵活、支持响应式功能、容易控制（有行/列的概念，但使用DIV+CSS实现） 
```
##### 栅格布局系统的特点：
```text
(1)所有的行必须放在容器中： .container或.container-fluid
(2)分为多行(row)，一行中平均分为12列(col)
(3)网页内容只能放在列(col)中，不能直接放在行(row)
(4)可以在col中再嵌套row
(5)col分为四大类： col-xs   col-sm    col-md   col-lg
(6)col-md-*  *值可为1~12，值就为某个列的宽度(  */12  )
(7)可以为一个列指定不同屏幕下的不同宽度
(8) col-lg-*  只对大PC屏幕有效
    col-md-*   对普通PC和大PC屏幕都有效
    col-sm-*   对平板、PC、大PC屏幕都有效
    col-xs-*   对手机、平板、PC大PC屏幕都有效
(9) .hidden-lg    当前列只在大PC屏幕下隐藏
    .hidden-md	当前列只在PC屏幕下隐藏
    .hidden-sm	当前列只在平板屏幕下隐藏
    .hidden-xs	当前列只在手机屏幕下隐藏
(10).col-md-offset-1~12  向右的偏移
(11).col-md-push-*/.col-md-pull-* 向右或向左的偏移
```
###### `col-md-push-*`和`col-md-offset-*`的区别？
```text
实现方式的区别：col-md-offset-*，是利用margin-left实现的，col-md-push-*/col-md-pull-*是利用相对定位实现的。
效果的区别，col-md-offset-*只能向右便宜，因为实现方式就是margin-left，而push/pull因为是相对定位，既可以左偏移也可以右偏移
还有一点，如果一行的偏移量+实际的宽度综合超过12，col-md-offset会换行显示，也是因为margin，而push/pull只会一部分不可见（超出容器），因为是相对自身定位。
从功能上来看，push和pull可以用来给元素换位置，比较灵活。
```
###### `.container`的宽度问题：
```$xslt
当屏幕宽度>1200px（超大PC显示器-lg）：    容器宽1170px
当屏幕宽度>992px（普通PC显示器-md）:    容器宽970px
当屏幕宽度>768px（平板显示器-sm）:        容器宽750px
当屏幕宽度<768px（手机显示器-xs）:         容器宽auto
.container-fluid的宽度： width: auto; + before + after
```
###### 面试题：Bootstrap布局系统中容器的特点？
```$xslt
(1)宽度做了媒体查询。
(2)添加了前置和后置内容生成，可以防止子元素的越界、浮动造成的影响。
```

### Bootstrap 4
`此处学习的还是v3版本,Bootstrap 于2018年年初发布了最新的4.0版本，Bootstrap 4 几乎是对整个项目进行了重写，从 v3 升级到 v4 应该注意的地方如下[摘自网络]`

##### 1.支持的浏览器

- v4 现在放弃了对 IE8 以及 iOS 6 的支持，现在仅仅支持 IE9 以上 以及 iOS 7 以上版本的浏览器。如果对于其中需要用到以前的浏览器，那么请使用 v3.
- 添加了对 Android v5.0 Lollipop 浏览器和 web 视图的官方支持。早期版本的 Android 浏览器和 web 视图仍然只有非官方支持

##### 2.全局变化

- 对于 CSS 文件，从 LESS 切换到了 SCSS.
- 对于主要的 CSS 单元，从 px 切换到了 rem.
- 媒体查询现在是在 ems 中而不是 pxs 中。
- 全局字体大小从 14px 增加到了 16px。
- 为 ~ 480px 及其以下添加了一个新的网格层。
- 通过 SCSS 变量，可以使用可配置的选项来替换单独的可选主题 (例如，$enable-gradients: true)。

##### 3.组件
- 对于该包罗万象的新的组件，丢弃了面板，缩略图以及wells。
- 丢弃了 Glyphicons 图标字体。
- 丢弃了 Affix jQuery 插件。相反，我们推荐使用 position: sticky。如果想要查看 HTML5，请点击该这里，查看详细具体的填充代码建议。
- 重构几乎所有的组件来使用更多的 unnested 的类而不是子选择器。

##### 4.Misc

- Bootstrap 不再支持非响应的用法。
- 丢弃了在线定制器功能，支持更广泛的安装文件以及自定义的工程。

#### 组件上的差别

##### 5.重启

对于 Bootstrap 4 有一个新的部分——重启，即一个新的样式表，基于标准化的基础上再添加上我们自定义的重置样式。当使用 Element 对象的时候我们才会用到选择器——在这里没有类。它使用更模块化的方法将我们重置的样式和组件样式进行分离。它们包括了一些最重要重置比如一些边框尺寸，边界的变化，许多元素从 rem 移动到 em 单元，链接样式，还有许多 element 对象中的变化。

##### 6.版式

- 将所有的 `.text- utilities` 移动到了 `_utilities.scss` 文件。
- 完全删除了 `.page-header` 类。
- `.dl-horizontal` 现在需要网格类，增加了列宽的灵活性。
- 将自定义的`<blockquote>`样式移动到了类——`.blockquote` 和 `.blockquote-reverse` 修饰符中。

##### 7.表格

- 几乎所有实例的 > 符号都被删除了，意味着嵌套的表格现在将自动继承他们的父母的样式。这大大简化了我们的选择器和潜在的自定义设置。
- 响应表不再需要包装元素。相反，仅仅只需要把 `.table-responsive` 放在 `<table>` 即可。
- 考虑一致性，将 `.table-condensed` 重命名为 `.table-sm`。
- 添加了一个新的 `.table-inverse` 选项。
- 添加了一个新的 `.table-reflow` 选项。
- 添加了表头修饰符：`.thead-default` 和 `.thead-inverse`。 

##### 8.表单

- 将重置元素移动到了 `_reboot.scss` 文件夹。
- 分别将 `.input-lg` 和 `.input-sm` 重命名为 `.form-control-lg` 和 `.form-control-sm`。
- 为了简单起见，现在删除了 `.form-group-*` 类，现在使用 `.form-control-*` 类。
- 水平表单的检修：取消了 `.form-horizontal` 类的要求。
- `.form-group` 类现在不再和 `.row` 混合，所以它现在需要网格布局。
- 将一个新的 `.form-control-label` 类添加到了带有 `.form-controls` 的垂直中心标签中。

##### 9.网格系统

添加了新的 ~ 480px 网格断点，意味着现在有五个总层。

##### 10.按钮和按钮组

- 完全删除了 `.btn-xs` 类。
- 完全删除了 `.btn-group-xs` 类。 

##### 11.导航(Navs)

- 删除了几乎所有的 `>` 符号，通过使用非嵌套类来实现更简单的样式。
- 我们现在直接使用单独的 `.navs`, `.nav-items`, 和 `.nav-links` 类而不是像 `.nav > li > a` 这样的 HTML 特定的符号。

##### 12.分页(Pager)

分别将 `.previous` 和 `.next` 重命名为 `.pager-prev` 和 `.pager-next`.

##### 13.Panels, thumbnails, 和 wells

- 对于新的 card 组件，他们几乎全部被删除了。
- `.panel` 改为 `.card` 将 `.panel-default` 删除并且不进行替换
- `.panel-heading` 改为 `.card-header` 
- `.panel-title` 改为 `.card-title` 
- `.panel-body` 改为 `.card-block` 
- `.panel-footer` 改为 `.card-footer`
- `.panel-primary` 改为 `.card-primary` 
- `.panel-success` 改为 `.card-success` 
- `.panel-info` 改为 `.card-info`
- `.panel-warning` 改为 `.card-warning`
- `.panel-danger` 改为 `.card-danger`

##### 14.轮播(Carousel)

- 将 .item 更名为 .carousel-item.

#### 新的部分

我们已经添加了以及改变了一些现有的组件。如下是新的或更新的样式。

组件|描述
--|--
Cards|一个新的、 更灵活的组件，它用来来取代 v3 中的的panels, thumbnails, 和 wells。
新导航栏|用一个新的、 更简单的组件替换以前的导航栏。
新进度栏|用现在的 `<progress>` 元素替换旧的 `.progress` `< div >`。
新的变形的表|添加 `.table-inverse`, 表头选项, 用 `.table-sm`, 和 `.table-reflow` 替换 `.table-condensed`

#### 移除的部分

`Panels, thumbnails, wells 和 Justified navs`

#### 响应程序

##### 下述已弃用的变量在 V4.0.0 被移除了:

- `@screen-phone`、 `@screen-tablet`、 `@screen-desktop`、 `@screen-lg-desktop`。相反的，使用更多抽象的 `$screen-{xs、 sm、 md、 lg、 xl}-*` 变量。
- `@screen-sm`，`@screen-md`，`@screen-lg`.相反，使用更明确地命名的变量 `$screen-{xs，sm，md，lg，xl}-min` 。
- `@screen-xs`，`@screen-xs-min`。这些额外的小断点有没有下限，因此，这些变量在逻辑上是荒谬的。根据 `$screen-xs-max` 改写你的表达式。

##### 响应实用程序类也已经进行了彻底翻新。

- 这些类（`.hidden-xs` `.hidden-sm` `.hidden-md` `.hidden-lg` `.visible-xs-block` `.visible-xs-inline` `.visible-xs-inline-block` `.visible-sm-block` `.visible-sm-inline` `.visible-sm-inline-block` `.visible-md-block` `.visible-md-inline` `.visible-md-inline-block` `.visible-lg-block` `.visible-lg-inline` `.visible-lg-inline-block`）都被删除了。
- 它们被 `.hidden-xs-up` `.hidden-xs-down` `.hidden-sm-up` `.hidden-sm-down` `.hidden-md-up` `.hidden-md-down` `.hidden-lg-up` `.hidden-lg-down` 进行了替换。

当视区是在给定的断点或更大的范围内 `.hidden-*-up` 类将隐藏元素 (例如`.hidden-md-up` 会隐藏中型、 大型，和特大型设备上的元素)。

当视区是在给定的断点或更小的范围内 `.hidden-*-down` 类将隐藏元素 (例如`.hidden-md-down` 会隐藏超小尺寸、 中小型，和小型设备上的元素)。

当你想要让一个元素可见，你仅仅需要不把它隐藏在这样的屏幕尺寸下，而不是使用显示的 `.visible-*` 类。你可以结合一个 `.hidden-*-up` 类和一个 `.hidden-*-down` 类来在给定的时间间隔的屏幕尺寸上显示元素(如`.hidden-sm-down` `.hidden-xl-up` 仅在中型和大型的设备上显示元素)。

<strong>请注意</strong>，在 v4 中对网格断点进行更改意味着你需要让一个断点更大来实现相同的结果 (例如 和 `.hidden-md-down` 相比 `.hidden-lg-down` 和 `hidden-md` 更相似)。在一些不常见情况下，比如在元素的可见性不能表示为一个单一的连续范围的视区大小的时候，新的响应实用程序类不要试图去容纳它；相反的，您需要在这种情况下使用自定义的 CSS。

#### 使用 Misc 来确定优先级

为视网膜显示器媒体查询删除 `min--moz-device-pixel-ratio` 黑客错误。 删除了 `.hidden` 和 `.show`，因为它在 `jQuery` 的 `$(...).hide()`拥有接口. 因为 IE 9 + 支持 `:disabled`，所以将 `[disabled]` 按钮改成了 `:disabled` 。然而 `fieldset[disabled]` 仍然是必要的，因为本机禁用字段在 IE11 中仍然会存在问题。