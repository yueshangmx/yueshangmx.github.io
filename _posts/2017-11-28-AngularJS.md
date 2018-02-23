---
layout: post
title: 25.AngularJS
date: 2017-11-28
description: "AngularJS"
tags: 笔记   
---

### 1.前言
`jQuery`是一个JS函数库，操作思路仍然是DOM操作思路：先查找元素，再操作元素。

`jQueryUI`是一个HTML组件库，简化了HTML/CSS的编写。

`Bootstrap`是一个CSS框架，主要提供了响应式布局、HTML组件、CSSReset。

`AngularJS`是一个JS框架，彻底颠覆了传统的DOM操作，所有的关注点集中在业务数据上，而不是DOM树。适用于以数据操作为主的SPA(Single Page Application)应用。

### 2.软件设计原则

- (1)避免重复原则
- (2)KISS原则，代码越简单越傻瓜越少
- (3)YAGNI原则，不创建不需要的代码
- (4)开闭原则，不让别人修改自己的代码，但可以扩展它
- (5)单一责任原则
- (6)高聚合低耦合原则，组件内部的逻辑关系越紧密越好，组件和组件之间关系越少越好。
- (7)最少知识法则/迪米特法则，司机不必知道如何造汽车。


### 3.设计模式
`设计模式`（Design pattern）是一套被反复使用、多数人知晓的、经过分类编目的、代码设计经验的总结。使用设计模式是为了可重用代码、让代码更容易被他人理解、保证代码可靠性。

23+1种设计模式;　　+1的那种设计模式：MVC模式

```text
modal：  模态框
model：  模型
module： 模块
```

### 4.MVC设计模式
MVC模式根据逻辑关系，把前端项目的代码分为三个层次：
```text
（1）Model：模型，就是业务数据，前端项目中就是JS变量；
（2）View：视图，就是业务数据在用户面前的展现，前端项目中就是HTML
（3）Controller：控制器，负责业务数据的增删改查，前端项目中就是function
```
![](/images/posts/angular/mvc.png)

### 5.AngularJS
#### 1.概述

AngularJS诞生于2009年，由Misko Hevery 等人创建，后为Google所收购。所有的操作思路都以“业务数据”为关注点，彻底颠覆了传统的DOM操作。适用于以数据的CRUD操作为主的SPA应用。

#### 2.AngularJS的四大特性
```text
(1)MVC设计模式
(2)双向数据绑定
(3)依赖注入
(4)模块化设计
```

#### 3.Angular表达式
```text
语法：{{ 表达式 }}
含义：Angular会计算表达式的值，输出在当前位置。
```

#### 4.Angular表达式可以执行哪些运算？
```text
(1)算数运算？        + - * / % 都可以，唯独不能自增/自减
(2)比较运算？        > < 都可以
(3)逻辑运算？        && || ! 都可以
(4)三目运算？                    可以
(5)调用字符串对象的成员方法？      可以
(6)使用直接量表示法创建对象？      可以
(7)可以使用数组吗？               可以
(8)使用new关键字创建对象？        不可以！不允许使用new和var关键字
(9)调用ES全局函数？              不可以
```

##### JavaScript中对象的分类：
```text
(1)ECMAScript标准对象  Global String Date RegExp Array Object ...
  可以在任一个js解释器中使用
(2)宿主对象：  
    DOM:  Node  Element   Attribute ....
    BOM:  window document  ....
  只能在浏览器中的js解释器中使用，不能在独立的服务器端js解释器(如NodeJS)中使用
(3)用户自定义对象
```

#### 5.AngularJS ng模块提供的指令(directive)

##### (1)ngApp：启动一个Angular应用——只有Angular应用中的表达式才会被Angular执行。
```text
用法： <ANY ng-app>
注意：angular应用的范围仅限于声明它的元素范围；且默认情况下一个HTML中不允许声明多个ngApp元素。
```

##### (2)ngInit：声明模型变量(Model)——不是局部变量
````text
用法： <ANY ng-init="变量名=值; 变量名=值;">
注意：ngInit声明变量不能声明var关键字！声明的变量可以在Angular表达式中进行输出
````

##### (3)ngBind: 计算一个表达式的值，输出为当前元素的innerHTML
````text
用法： 	<ANY ng-bind="表达式"></ANY>
        <ANY class="ng-bind: 表达式;'></ANY>
说明：ngBind指令作用与{{}}表达式基本类似，只是可以防止用户在一瞬间看到{{}}。ngBind指令计算完成表达式的值，会替换当前元素的innerHTML.
````

##### (4)ngController：调用Controller创建函数，实例化一个控制器对象，指定其作用范围
```text
用法： <ANY ng-controller="控制器名">...</ANY>
```

##### (5)ngRepeat：用于在View实现循环输出
```text
用法： <ANY ng-repeat="变量名 in 集合对象"></ANY>
含义：对于集合对象中的每一个元素，依次赋值给指定的变量名，对每次赋值都输出一遍当前元素。
```

##### (6)ngIf：用于在View实现判断输出，为false就不输出了
```text
用法： <ANY ng-if="布尔表达式">
含义： 若布尔表达式为true则输出当前元素；否则当前元素在DOM树不存在
```