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

### 5.AngularJS 概述

AngularJS诞生于2009年，由Misko Hevery 等人创建，后为Google所收购。所有的操作思路都以“业务数据”为关注点，彻底颠覆了传统的DOM操作。适用于以数据的CRUD操作为主的SPA应用。

#### 1.AngularJS的四大特性
```text
(1)MVC设计模式
(2)双向数据绑定
(3)依赖注入
(4)模块化设计
```

#### 2.Angular表达式
```text
语法：{{ 表达式 }}
含义：Angular会计算表达式的值，输出在当前位置。
```

#### 3.Angular表达式可以执行哪些运算？
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

##### 4.JavaScript中对象的分类：
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
##### (7)其他一些指令
```text
(7)ngClick： 为元素绑定单击事件的监听函数——只能是Model函数($scope.函数名=function(){})，不能是全局函数
(8)ngMouseOver: 鼠标覆盖移动
(9)ngSrc: 为IMG标签指定src属性，但可以防止404请求错误
(10)ngShow:  若赋值为true，则display:block；否则display:none;
(11)ngHide:  若赋值为true，则display:none；否则display:block;
```

#### 6.ng模块中提供的service组件
```text
(1)$rootScope	  用于在所有的控制器间共享数据的服务
(2)$interval      周期性定时器服务
(3)$timeout       一次性定时器服务
```
<strong>面试题：$interval和window.setInterval()的区别？</strong>
```text
$interval修改的任何Model数据，底层会立即遍历一遍$digest队列；
setInterval()即使修改了Model数据，也不会遍历$digest队列；
```

#### 7.AngularJS中声明模型数据的方式

##### (1)使用ngInit指令来声明Model数据
```text
<ANY ng-init="变量名=值;">
说明：此方式将Model声明在View中，严重违反了MVC模型的分工，不推荐使用
```

##### (2)使用Controller对象创建Model数据——符合MVC模型分工
```text
新版本的AngularJS中创建Model的语法：
ngApp=>Module=>Controller=>Model
1)声明一个AngularJS的应用程序： ngApp
2)创建一个自定义的模块：	angular.module('模块名', [依赖列表])
3)在应用中注册自定义模块：  ng-app="模块名"
4)在模块中声明Controller函数
5)在View中指定Controller对象的作用范围——调用控制器创建函数
6)在Controller中声明Model数据
```

<strong>面试题： AngularJS与jQuery的关系？</strong>
```text
jQuery操作思路：先找元素，再操作元素   $(....).xxx();
AngularJS操作思路：创建业务数据、绑定数据、维护数据
----
AngularJS已经把底层/低级的DOM操作，为开发者封装起来了;
  AngularJS在加载时会查看当前页面是否已经加载了jquery.js(就是判断window.jQuery是否存在)，
  若存在,则所有的DOM操作全都使用jQuery提供的方法；
  若不存在，则anglarJS会使用自定义的jQuery精简版本——jqLite——只有jQuery的核心方法。
```

#### 8.控制器的作用范围/作用域
```text
(1)每次调用ngController都会创建一个新的Controller对象
(2)每个Controller对象都有唯一的$scope对象
(3)$scope就表示当前控制器对象的有效范围/作用域
(4)声明在某个$scope中模型数据，一般情况下不能被其他的控制器所使用。
(5)若想在多个控制器间共享/传递数据，可以声明在根作用域中——$rootScope—每个Angular应用(ngApp)只有一个唯一的$rootScope对象 
(6)控制器的本质用途：用于划分一个大型页面中的不同的DIV块——每个这样的块中都有自己专用的数据，以及可以与其他块共享的数据。
```

### 6.AngularJS四大特性之二——双向数据绑定

#### (1)方向1：Model绑定到View
```text
Model绑定到View，此后不论何时只要Model发生改变，View会自动立即同步更新。
实现方法：{{ }}、ngBind、ngIf、ngRepeat、ngShow、ngChecked ... 等等几乎所有的显示数据的指令都实现了方向1的绑定。
```

#### (2)方向2：View绑定到Model
```text
View绑定到Model，把视图中用户可以修改的HTML元素——即表单控件——的值绑定到一个Model变量上。此后，不论何时只要用户修改了表单控件的值，后台模型变量的值会立即随之改变。
实现方法：只有ngModel指令可以！ 为了监视到Model变量真的被改变了，可以使用$scope.$watch()函数对Model数据的值进行监视。
  单行文本输入域，ngMode可以把value属性值绑定到Model变量
  复选框，ngModel可以把true/false值绑定到Model变量
  单选框，ngModel可以把当前选中的单选框的value值绑定到Model变量
  下拉框，ngModel可以把当前选中的option的value值绑定到Model变量
```

### 7.AngularJS四大特性之三——依赖注入
`依赖(Dependency)`：若某个函数调用时需要其它的对象作为形参，就此函数依赖于形参对象。
```
function Driver( car ){		//司机依赖于一个car对象
 	car.start();
  car.run();
  car.stop();
}
```
#### 1.如何解决依赖关系
 
##### (1)主动创建方式
```
var c1 = new Car();	//主动创建依赖对象
var d1 = new Driver( c1 );  //传递依赖对象
```

##### (2)被动注入(Injection)方式
```
module.controller('控制器', function($scope, $interval){...});
```
Angular中的ngController指令在实例化控制器对象时，会根据指定的形参名，创建出控制器所依赖的对象，并注入给控制器对象——依赖注入（Dependency Injection，DI）现象。

##### 注意
```text
(1)Angular在创建控制器对象时，会根据形参列表中的每个形参的名称来创建依赖的对象，故控制器声明函数不能声明Angular无法识别的形参名——Angular只提供了这一种依赖注入方式——根据形参名来注入依赖的对象！
(2)若项目JS文件使用了类似yuicompressor等压缩程序，默认会把函数的形参名精简为一个字母的形式，会导致Angular的依赖注入失败！
  解决办法：
    module.controller('控制器名', ['$scope','$interval','$http',function(aaa,bbb,ccc){...}]);
```

#### 3.可以被注入的对象 — 所有的service/provider对象都可以被注入
```text
(1)$rootScope：在多个控制器间共享数据的服务
(2)$interval：提供周期性定时器服务
(3)$timeout：
(4)$log：提供五个基本的日志输出服务
(5)$http：提供异步HTTP请求（AJAX）服务
  用法： $http({method: 'GET',url: 'Url'}).
        then(function success(response) {
              // 请求成功执行代码
          }, function error(response) {
              // 请求失败执行代码
        });
  简化版：	$http.get('Url', config).then(success, error);
          $http.post('Url', data, config).then(success, error);
(6)$location
```

#### 4.ng模块中提供的过滤器(filter)

Filter: 把Model数据在显示时以某种特定的格式呈现。
```text
(1)lowercase
  {{ 表达式 | lowercase }}
(2)uppercase
  {{ 表达式 | uppercase }}
(3)number
  {{ 表达式 | number }}
  {{ 表达式 | number : 小数位数 }}
(4)currency
  {{ 表达式 | currency }}
  {{ 表达式 | currency : '货币符号' }}
(5)date
  {{ 表达式 | date }}    	默认格式： Sep 1, 2015
  {{ 表达式 | date : '日期时间格式'}}
```
