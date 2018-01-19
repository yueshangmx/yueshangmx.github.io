---
layout: post
title: WebView加载本地、远程HTML文件是黑屏、白屏的解决办法
date: 2018-01-19
description: "Webapp、WebView"
tags: 笔记   
---

### 关于安卓webview加载网页黑屏、部分黑屏或blank的解决方法

很多朋友在利用安卓的webview加载网页的时候 可能会出现黑屏现象

这种情况出现在Android4.4版本以上比较多 第一点的版本可能是blank空白。

然后 有些朋友会在不断的修改webview的一些参数设置 

网上见的比较多的就是添加这一句代码
```java
webview.getSettings().setJavaScriptEnabled(true); 
```
或者 修改webview控件以及它所在的LinearLayout的layout_width和layout_height属性值为"fill_parent"；

或者对网页的图文进行异步加载 先在load前利用webview.getSettings().setBlockNetworkImage(true);方法对图片进行阻塞，待文字加载完毕后，再在onPageFinished(WebView view, String url) 方法中取消图片阻塞。

这些方法我都试过了一遍 但发现都没有达到很好的效果 实际上 非常简单 那就是在MainActivity.java文件中添加一句代码
```
webView.setLayerType(View.LAYER_TYPE_SOFTWARE, null);
从网上搜索，这似乎是因为硬件加速canvas渲染不支持Chromium WebView，
这一行代码可以关闭硬件加速的canvas。大家不妨试试，有什么错误的请指正。
如果还是不行的话 我觉得只能修改网页body标签的css样式 让背景为白色了
```