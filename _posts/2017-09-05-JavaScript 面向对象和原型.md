---
layout: post
title: 13.JavaScrip 面向对象和原型
date: 2017-09-05
description: "JavaScript，面向对象，原型，继承"
tags: 笔记   
---

### 1.面向对象
在程序中，都是用一个对象来描述现实中一个具体的东西。

现实中的东西：都包含属性：描述一个东西特点的变量，一个值; 功能：东西可以执行的操作。

什么是对象：封装多个数据和方法的存储空间；

什么是自定义对象：封装现实中一个东西的属性和功能的存储空间；现实中东西的属性会成为对象中的属性变量，现实中东西的功能，会成为对象中的方法（函数）。

```
面向对象三大特点：封装 继承 多态
	封装：将描述同一个东西的属性和方法，定义在一个对象中
	继承：父对象中的属性和方法，子对象可直接使用。
	多态：同一个对象，在不同情况下，呈现不同的状态。
		重载：统一方法名，传入参数不同，执行不同的操作。
		重写：子对象觉得父对象的成员不好用，可自己定义一个，覆盖父对象的成员。
```

### 2.创建自定义对象
- (1)对象直接量
```
var obj={"属性名1":值1,
	"属性名2":值2,
	......	
	"方法名",function(){...this.属性名...}
};
```
JS中一切都是对象，所有对象的底层，都是hash数组。

访问对象的属性：`obj.属性名`或者`obj["属性名"]`

<font color="#f00">注意：访问对象中不存在的属性 ==> 访问数组中不存在的下标——不会出错，返回undefined；强行给不存在的属性赋值，不会报错！ js会自动创建同名属性</font>

如何判断某个对象是否包含指定成员
```
1) obj.hasOwnProperty(“成员名”)；
　　如果找到，返回true ； 否则返回false！
2) "属性名" in 对象
　　如果找到，返回true ； 否则返回false！
3) 直接使用obj.属性名 作为条件
　　if(arr.indexOf===undefined) 
　　　　何时省略：判断方法是否存在时，可省略===undefined
		  如果确定属性值一定不是null，0，""，NaN也可以省略
	如果不包含，返回undefined --> false
	如果包含，返回值或function -->true
```
this关键字：在方法中，若要访问当前对象自己，要使用this关键字,知道正在调用方法的对象。

`this和定义在哪无关！仅和调用时使用的对象有关！`<br>
`所有无主(不用var赋值的变量，匿名函数)都是window的`

`面试题`
```javascript
//鄙视题　　//this-->window
var a=2;	
function fun(){		//地址0x1011	
　　console.log(this.a);
}
//this-->window
 var o={a:3,fun:fun};	//this-->o
	  				//0x1011
var p={a:4};			//this-->p
o.fun();  //this-->o  function里的this.a相当于o.a,输出是3
	  
(p.fun=o.fun)();	//2
//p.fun=0x1011
//p={a:4,fun:0x1011}
//返回o.fun中的值！0x1011
//(0x1011)() ==> 匿名函数自调
/*赋值表达式的结果相当于等号右侧表达式的值*/
p.fun();	//4
```

- (2)new方法
```
var obj=new Object();  //创建一个空对象
obj.属性名=值;
obj.方法名=function(){...this.属性名...}
```
- (3)利用构造函数，反复创建相同结构的对象

构造函数：描述一类对象的结构的特殊函数

定义构造函数
```javascript
function 构造函数名(属性参数,……){
　　this.属性名=属性参数;
　　if(!构造函数名.prototype.方法名){	
　　　　构造函数名.prototype.方法名=function(){
　　　　　　...this.属性名
　　　　}
　　}
}

```
利用构造函数创建对象
```
var obj=new 构造函数名|类型名(属性值1,...)
new：	①创建一个空对象 new obj={}
	②利用空对象调用构造函数;构造函数在空对象中添加属性和方法
	③设置新对象的__proto__指向构造函数的prototype属性
	④返回新对象的地址
```
### 3.原型、原型链、继承
```
原型：保存所有子对象共有属性和方法的对象！
　　所有函数都有prototype，指向自己的原型对象，
　　所有对象都有__proto__，指向自己父级原型对象。
　　所有原型对象都有constructor，指向原型对应的构造函数
```
```
原型链：所有父子级对象间由__proto__形成的多级引用关系。——>也有叫多级继承
```
原型相关的API：
```
(1)判断自有属性和共有属性：
　　1）判断自有：obj.hasOwnProperty(“属性名”)；
　　2）判断原型链上的属性：3种
　　　　判断不包含：if(!(“属性名” in obj))	#此处obj应该是对象的原型
	　　　　　　if(obj.属性名===undefined)
	　　　　　　if(!obj.属性名)
　　3）仅判断共有：必须满足两个条件
　　　　！obj.hasOwnProperty(“属性名”)&& “属性名” in obj
```
![](/images/posts/JavaScript/prototype/pdgyzysx.png)
```
(2) 获得任意对象的原型
　　obj.__proto__		不推荐用
　　Object.getPrototypeOf(obj)
```
```
(3) 判断父对象是都在子对象的原型链上
　　父对象.isPrototypeOf(子对象);
```
```
****检测一个对象是不是数组类型：4种
　　（1）Array.prototype.isPrototypeOf(obj);
　　（2）obj instanceof Array				#obj是不是构造函数Array的实例
　　（3）obj.constructor==Array;				#仅判断直接父级
　　（4）利用当前对象，强行调用原始的toString方法
　　　　Object.prototype.toString.call(obj)==”[object Array]”  #此处call也可用apply替换

```

js中一切继承都是用原型对象实现的！

原型对象：每个函数对象都有一个原型对象 prototype；构造函数的原型对象负责保存所有子对象共享的成员

所有子对象共享的方法，都应定义在构造函数的原型对象中。——避免重复定义对象，浪费内存。

```
扩展对象的属性：2种
　　（1）扩展共有属性：通过构造函数.prototype添加的属性
　　（2）扩展自有属性：通过某一个具体子对象添加的属性
判断自由属性或共有属性：
　　（1）判断自有属性：obj.hasOwnProperty("属性名");
　　（2）判断共有属性："属性名" in obj && !obj.hasOwnProperty("属性名")	#在原型关系中包含且子对象自己没有
　　　　[in的范围包括共有属性和自有属性，所有判断共有属性只有in不行]
删除属性： delete 对象.属性名
　　*仅能删除当前对象自己的属性，无法删除共有属性
```
- 为什么要继承：代码重用！节省内存空间！

```
(1)直接继承对象：想方设法修改对象的__proto__属性——3种方式：1_inherit.html
　　1)仅修改一个对象的__proto__
	Object.setPrototypeOf(子对象,父对象)
　　2)通过修改构造函数的原型对象，实现批量修改后续子对象的继承关系。
	构造函数.prototype=父对象;		
　　　强调：仅影响之后创建的对象的继承关系，之前创建的对象依然继承旧构造函数.prototype
　　3) var obj=Object.create(父对象[,{属性列表}])  #红色中括号内可以省略
	创建一个空对象，继承父对象中的属性。
	继承同时可再扩展属性和方法
(2)仅继承结构： 模拟Java中的继承
　　function 父类型构造函数(属性参数1,属性参数2){
　　　　this.属性1=属性参数1;
　　　　this.属性2=属性参数2;
　　}
　　function 子类型构造函数(属性参数1,属性参数2,属性参数3){
　　　　父类型构造函数.call(this,属性参数1,属性参数2);
　　　　this.属性3=属性参数3；
　　}
　　var obj=new 子类型构造函数(值1，值2，值3);
```

看下面的例子
```
/*创建2个对象，分别描述李雷和韩梅梅:
	李雷: sname:"Li Lei",age:12
	韩梅梅: sname:"Han Meimei",age:11
	都可以做自我介绍:intrSelf()
*/
		/*先定义构造函数*/
		function Student(sname,age){
			this.sname=sname;
			this.age=age;
		}
		//在构造函数原型对象中定义公共方法
		Student.prototype.intrSelf=function(){
			alert("I'm "+this.sname+",I'm "+this.age);
		}
		
		var lilei=new Student("Li Lei",12);
		var hmm=new Student("Hai Meimei",11);
		//在构造函数原型对象中定义公共属性
		Student.prototype.money=100;
		console.log(lilei.money);
			//现在当前对象本地找，找不到再去原型，原型中也没有，反返undefined
		console.log(hmm.money);
		
		
		Student.prototype.money-=20;
		console.log(lilei.money);
		console.log(hmm.money);
		if(!(hmm.hasOwnProperty("money"))&&("money" in hmm)){
			hmm.money=10;	//仅为hmm添加自有属性
			hmm.charge=20;
		 }
		console.log(lilei.charge); //undefined
```
![](/images/posts/JavaScript/prototype/prototype.png)
