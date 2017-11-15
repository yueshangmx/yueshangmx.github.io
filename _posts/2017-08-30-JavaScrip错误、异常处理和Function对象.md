---
layout: post
title: 12.JavaScrip错误、异常处理和Function对象
date: 2017-08-30
description: "JavaScript，闭包，try Catch，Function 对象"
tags: 笔记   
---

### 1.错误/异常处理
在JS中，程序一旦出错，就会自动创建一个Error类型对象。共有6种：
```
SyntaxError：	#语法错误
ReferenceError：#引用错误，找不到变量或对象
TypeError：	#类型错误，错误的使用了对象中的方法时
RangeError：	#范围错误，参数超出范围。
EvalError：	#调用eval函数时错误
URLError：	#URL错误
```
如何处理错误：tryCatch块
```
try{
	可能出错的代码段;
}catch(err){ /*仅在发生错误时才执行，一旦发生错误，err中就会自动存入Error对象*/
	程序出错事，执行的代码;
	/*1.记录/显示错误的信息*/
	/*2.继续向调用者抛出异常*/
}[finally{		//[]表示可有可无
	无论对错，一定都会执行的代码段
	/*释放资源*/
}];
```

正常的web应用，应该在程序发生错误时，保证程序不退出或者正常退出。所以，我们需要将某段可能会出现错误的代码段，用try Catch块包裹。

对于可以预见的错误，尽量舒勇if...else结果规避，只有无法预料的错误，采用tryCatch。

tryCatch可以用于：解决浏览器兼容性问题；也可以用于抛出自定义异常，预防他人错误使用自己的定义的方法。例如：
```
try{
    new XMLHttpRequest();
    document.write("支持XMLHttpRequest对象");
}catch(err){
    document.write("<h1 style='color:red'>不支持XMLHttpRequest对象</h1>");
}
/*上述代码，如果浏览器不支持XMLHttpRequest对象，就会创建一个Error对象，但是创建后并未使用。*/
/*有经验的开发人员会用刚下面的代码代替*/
if(XMLHttpRequest){
    document.write("<h1 style='color:green'>支持XMLHttpRequest对象</h1>");
}else{
    document.write("<h1 style='color:red'>不支持XMLHttpRequest对象</h1>");
}
```

### 2.Function对象
Function对象：JavaScript中一切都是对象，连函数也是对象，函数名其实是引用函数定义对象的变量。

- 1.arguments对象：函数对象，自动创建的专门接收所有参数值的类数组对象。
```
arguments对象会自动接收函数对象传入的所有参数，本身是一个类数组对象。
arguments[i]：	  #获得传入的下标为i的参数值，
arguments.length：#获得传入的参数个数。
```

重载：程序中可定义多个相同方法名，不同参数列表的函数。调用者不必区分每个函数的参数，执行时，程序根据传入的参数个数，自动判断选择哪个函数执行。

JavaScript语法不支持重载！但是可用arguments对象模拟重载效果。

- 2.function对象的本质

(1) 创建函数对象：3种
```
1). 声明方式： 	
    function 函数名(参数){
        函数体;
        return 返回值;
    }
/*函数名和定义都被提前，定义在调用前后都可以*/
----
2). 函数直接量：	
    var 函数名=function(参数){
        函数体；
        return 返回值；
    }
/*仅函数名变量声明会提前，函数定义留在本地，必须定义在调用之前*/
----
3). 使用new创建函数类型对象：——了解
    var 函数名=new Function("a","b",……,"函数体");
```
(2) 内存中的函数对象
```
创建函数对象时：同时创建2个对象：
		函数对象：函数的定义
		作用域链对象：保存函数对象可用的变量位置的对象(栈)。
			      默认第一项指向window对象
----
调用函数时：又会创建1个新对象：
		活动对象：专门保存局部变量的对象
		在作用域链对象中追加指向活动对象的引用
----
调用后：作用域链中活动对象的引用出栈，活动对象因无人引用被释放。
```
(3) 匿名函数：定义时不指定函数名的函数。

```
2大用途:
----
1) 匿名函数自调：定义完，立即执行，执行完立刻释放。
   何时使用：只有确定函数只执行一次时！
   如何自调：	
    (function(参数){
        函数体;
    })(参数值);
/*自调：定义在哪，就在哪执行，不提前*/
----
2) 匿名函数回调：先将函数作为对象传递给另一个函数，由另一个函数自主决定在需要时调用。
    何时使用：只要将一个函数对象传递给其他方法调用时，用匿名函数。
    如何回调：直接将匿名函数的声明传入另一个函数中。
```
看下面的例子：命名函数
```javascript
var a;
/*----------1.png----------*/
function fun(a){	//此处的a是局部变量
    a++;
    console.log(a);
}
/*----------2.png----------*/
a=100;
/*----------3.----------png*/
fun(a);/*----------4.png----------*/
/*----------5.png----------*/
```
上述案例在内存中的执行过程如下图：<br>
1.![](/images/posts/JavaScript/namedFun/1.png)
2.![](/images/posts/JavaScript/namedFun/2.png)
3.![](/images/posts/JavaScript/namedFun/3.png)
4.![](/images/posts/JavaScript/namedFun/4.png)
5.![](/images/posts/JavaScript/namedFun/5.png)

匿名函数过程：
```javascript
var a=100;
(function(a){
    a++;
    console.log(a);
})(a);
```
内存中的执行过程为：
1.![](/images/posts/JavaScript/anonyFun/1.png)
2.![](/images/posts/JavaScript/anonyFun/2.png)
3.![](/images/posts/JavaScript/anonyFun/3.png)
4.![](/images/posts/JavaScript/anonyFun/4.png)

(4) 闭包
```
局部变量和全局变量缺陷:
    全局变量：容易全局污染（谁都可以修改）
    局部变量：无法共享，不能长久保存。
----
既可以共享，长久保存，又不会全局污染——闭包。
闭包三特点：
 (1) 定义外层函数，封装被保护的局部变量
 (2) 定义内层函数，执行对外层函数局部变量的操作
 (3) 外层函数返回内层函数的对象，并且外层函数被调用，结果被保存在全局变量中

```
看如下案例：
```javascript
//定义一个取号机函数
//  每调用一次，顺序生成一个永不重复的序号
        function outer(){var n=1;function inner(){return n++;}
            return inner;
        }
        //ICBC
        var getNum=outer();
        //getNum-->function inner(){ return n++;}
        console.log(getNum()); //1
        console.log(getNum()); //2
        var n=100; //假设有全局污染
        console.log(getNum()); //3 不受干扰
        console.log(getNum()); //4
        //CMCC
        var getNumCMCC=outer();
        console.log(getNumCMCC()); //1
        console.log(getNumCMCC()); //2
        var n=100; //假设有全局污染
        console.log(getNumCMCC()); //3 不受干扰
        console.log(getNumCMCC()); //4
```
上述案例执行过程如下所示：
1.![](/images/posts/JavaScript/closure/1.png)
2.![](/images/posts/JavaScript/closure/2.png)
3.![](/images/posts/JavaScript/closure/3.png)
4.![](/images/posts/JavaScript/closure/4.png)
5.![](/images/posts/JavaScript/closure/5.png)

