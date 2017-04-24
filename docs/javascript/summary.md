## 事件代理

## this
this永远指向函数运行时所在的对象，而不是函数被创建时所在的对象。

## 闭包

## Function.prototype.bind


## ”attribute”和”property”的区别是什么？

## deferred对象

## 对象
+ 本地对象
  Object、Function、Array、String、Boolean、Number、Date、RegExp、Error、EvalError、RangeError、ReferenceError、SyntaxError、TypeError、URIError
+ 内置对象
  Global 和 Math
+ 宿主对象
  BOM和DOM
> 本地对象和内置对象概念好像

## addeventlistener和onclick的区别

## addEventListener第三个参数作用，和attachEvent区别

## use strict是什么意思

除了正常运行模式，ECMAscript 5添加了第二种运行模式："严格模式"（strict mode）。   
顾名思义，这种模式使得Javascript在更严格的条件下运行。 [Javascript严格模式详解](http://www.ruanyifeng.com/blog/2013/01/javascript_strict_mode.html)  

设立"严格模式"的目的，主要有以下几个：
+ 消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为;
+ 消除代码运行的一些不安全之处，保证代码运行的安全；
+ 提高编译器效率，增加运行速度；
+ 为未来新版本的Javascript做好铺垫。



## 说出数组的5个方法
+ 参考：http://www.cnblogs.com/moqiutao/p/5093861.html
+ ArrayObj.push()：就是向数组末尾添加新的元素，返回的是数组新的长度。
+ ArrayObj.pop()：就是向数组中删除数组最后一个元素并且返回该元素。如果数组为空就返回undefined。
+ ArrayObj.shift():方法用于把数组中的第一个元素删除，并返回第一个元素的值。
如果数组是空的，则shift() 方法不进行任何操作，返回undefined。请注意，该方法不创建新数组，而是直接修改原来的数组。该方法会改变数组的长度。
+ ArrayObj.unshift() ：该方法可把它的参数顺序添加到数组的头部。它直接修改了数组，而不是创建一个新的数组。返回的是新数组的长度。 
unshift()在IE6，IE7下，数据有添加成功，但返回值却是undefined.
+ reverse()方法会对反转数组项的顺序，返回值是经过排序之后的数组。
+ sort()方法按升序排列数组，返回值是经过排序之后的数组。
+ concat() 方法用于连接两个或多个数组。该方法不会改变现有的数组，而仅仅会返回被连接数组的一个副本。
+ join() :方法用于把数组中的所有元素放入一个字符串。元素是通过指定的分隔符进行分隔的。返回一个字符串。
+ slice(start, end); slice()方法返回从参数指定位置开始到当前数组末尾的所有项。如果有两个参数，该方法返回起死和结束位置之间的项，但不包括结束位置的项。
+ splice（）有删除，插入，替换的功能
	>删除：需要两个参数，要删除的第一项的位置和要删除的项数。
	>插入：需要三个参数：起始位置、0（要删除的项数）和要插入的项
	>替换：需要三个参数：起始位置、要删除的项数和要插入的任意数量的项。