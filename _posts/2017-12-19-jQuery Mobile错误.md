---
layout: post
title: jQuery Mobile和jQuery版本不匹配出错
date: 2017-12-15
description: "JavaScript，jQuery，jQuery Mobile"
tags: 笔记   
---

### jQuery mobile报错 Uncaught TypeError: Cannot read property 'concat' of undefined

写一个jQuery mobile的简单demo
```
<!doctype html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width,initial-scale=1.0,user-scalable=no">
  <title>JQM demo</title>
  <link rel="stylesheet" href="jqm/jquery.mobile-1.4.5.css">
  <script src="js/jquery-3.2.1.js"></script>
  <script src="jqm/jquery.mobile-1.4.5.js"></script>
</head>
<body>
<div data-role="page">
  <div data-role="header">
    <h2>Page Title</h2>
  </div>
  <div class="ui-content">
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis eum iste molestias natus perferendis recusandae reprehenderit sunt suscipit! Consequatur dolores dolorum earum enim incidunt pariatur quis quo repudiandae soluta voluptatem?</p>
  </div>
  <div data-role="footer">
    <h4>Page Footer</h4>
  </div>
</div>
</body>
</html>
```

用浏览器打开，发现没有样式，模拟手机也一样，打开控制台发现报了一个错误
![](/images/posts/errimg/jqmerr.png)

查了一下，是因为jQuery Mobile和jQuery的版本不匹配，我当前的jQuery mobile的版本是1.4.5，jQuery用的版本是3.2.1， jQuery重新下2版本以下的试试，我下了1.11.3是可行的