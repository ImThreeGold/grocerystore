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

## element.addEventListener和element.onclick的区别
+ element.onclick 相当于在标签上写onclick，作用于标签；element.addEventListener则是通过DOM接口绑定事件
+ 一个html文档的解析是有顺序的，先解析标签项，再解析DOM项，element.onclick事实上相当于写在标签上，
通过标签的onclick属性输入到文档，然后由文档解析成事件的。而后者，要在文档解析完成以后，
通过文档的dom接口去绑定的事件，虽然结果是一样的，都是click事件，但是过程是不同的。

## addEventListener第三个参数作用？
+ element.addEventListener(event, function, useCapture)
+ event：事件名，不要使用on前缀
+ function：指定要事件触发时执行的函数。 
+ useCapture：布尔值，指定事件是否在捕获或冒泡阶段执行。true - 事件句柄在捕获阶段执行；false- 默认。事件句柄在冒泡阶段执行
+ “事件流”的概念：侦听器在侦听时有三个阶段：捕获阶段、目标阶段和冒泡阶段。顺序为：捕获阶段（根节点到子节点检查是否调用了监听函数）→目标阶段（目标本身）→冒泡阶段（目标本身到根节点）。此处的参数确定侦听器是运行于捕获阶段、目标阶段还是冒泡阶段。 如果将 useCapture 设置为 true，则侦听器只在捕获阶段处理事件，而不在目标或冒泡阶段处理事件。 如果useCapture 为 false，则侦听器只在目标或冒泡阶段处理事件。

## addEventListener和attachEvent区别？
+ 关于标准：addEventListener是W3C标准，支持所有浏览器；attachEvent非W3C标准且只支持IE浏览器
+ 关于参数:attachEvent两个参数，事件名（带on的那种）+处理方法；addEventListener三个参数：事件名（不带on的那种）+处理方法+useCapture（true - 事件句柄在捕获阶段执行；false- 默认。事件句柄在冒泡阶段执行）
+ 关于执行顺序：attachEvent：后绑定的先执行。addEventListener：先绑定的先执行

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
+ 删除：需要两个参数，要删除的第一项的位置和要删除的项数。
+ 插入：需要三个参数：起始位置、0（要删除的项数）和要插入的项
+ 替换：需要三个参数：起始位置、要删除的项数和要插入的任意数量的项。