### css的标识符有哪些
在CSS标识符命名中可以使用包含字符(a-zA-Z0-9)和ISO 10646字符字符集中的字符,也可以使用连字符(-)和下划线(_);   
同时，起始部分不能是数字,或两个连字符"-"或一个"-"连字符后跟一个数字。   
标识符也可以包含转义字符和任何ISO 10646字符数字代码。

### 哪些属性可以继承
https://www.w3.org/TR/CSS21/propidx.html   
http://stackoverflow.com/questions/5612302/which-css-properties-are-inherited

### 优先级
优先级逐级增加的：
+ 元素(类型)选择器（例如：h1）和 伪元素选择器（例如：:before）
+ 类选择器 (例如：.example)，属性选择器（例如：[type="radio"]），伪类选择器（例如：:hover）
+ ID选择器（例如：#example）  

通用选择器(*),组合符合 (+, >, ~, ' ')  和 否定伪类(:not()) 不会影响优先级（但是，在 :not() 内部声明的选择器是会影响优先级的）。

>给元素添加的内联样式 (例如, style="font-weight:bold") 总会覆盖外部样式表的任何样式 ，因此可看作是具有最高的优先级。

### 内联和important哪个级别高
当在一个样式声明上使用 !important 规则时，该样式声明会覆盖CSS中任何其他的声明。即使是内联样式，也会被覆盖。

### IE盒子模型和标准W3C盒子模型
ie的width包括：padding\border。标准的width不包括：padding\border

### css预处理器区别
[StylusStylus、Sass、less](http://www.w3cplus.com/css/css-preprocessor-sass-vs-less-stylus-2.html)
+ CSS预处理器定义了一种新的语言，其基本思想是，用一种专门的编程语言，为CSS增加了一些编程的特性，将CSS作为目标生成文件，然后开发者就只要使用这种语言进行编码工作。通俗的说，CSS预处理器用一种专门的编程语言，进行Web页面样式设计，然后再编译成正常的CSS文件，以供项目使用。著作权归作者所有。

+ 三者都是开源项目；
+ Sass诞生是最早也是最成熟的CSS预处理器，有Ruby社区和Compass支持；Stylus早期服务器Node JS项目，在该社区得到一定支持者；LESS出现于2009年，支持者远超于Ruby和Node JS社区；
Sass和LESS语法较为严谨、严密，而Stylus语法相对散漫，其中LESS学习起来更快一些，因为他更像CSS的标准；
+ Sass和LESS相互影响较大，其中Sass受LESS影响，已经进化到了全面兼容CSS的SCSS；
+ Sass和LESS都有第三方工具提供转译，特别是Sass和Compass是绝配；
+ Sass、LESS和Stylus都具有变量、作用域、混合、嵌套、继承、运算符、颜色函数、导入和注释等基本特性，而且以“变量”、“混合”、“嵌套”、“继承”和“颜色函数”称为五大基本特性，各自特性实现功能基本相似，只是使用规则上有所不同；
+ Sass和Stylus具有类似于语言处理的能力，比如说条件语句、循环语句等，而LESS需要通过When等关键词模拟这些功能，在这一方面略逊一层；

### CSS框架
Bootstrap,PureCSS,Foundation

### 栅格系统
+ 在一个有限的、固定的平面上，用水平线和垂直线（虚拟的线，“参考线”），将平面划分成有规律的一系列“格子”（虚拟的格子），并依托这些格子、或以格子的边线为基准线，来进行有规律的版面布局。

### 如何实现响应式布局
+ 确定需要兼容的设备类型、屏幕尺寸
+ 利用css3的media query媒体查询功能
> 一个普通的自适应显示的三栏网页，当你用不同的终端来查看这个页面的时候，他会根据几种终端来显示不同的样式，在电脑上是三列，在pad上应该也是 三列，在大屏手机上是三行，在屏幕小于320的手机上只显示主要内容，隐藏掉了次要元素。

### 媒体查询
> CSS媒体查询允许我们基于浏览网站的设备的特性来应用不同的样式申明

+ 语法
```
@media mediatype and|not|only (media feature) {
    CSS-Code;
}
```
+ mediatype：包括：
> 
1.print		用于打印机和打印预览
2.screen	用于电脑屏幕，平板电脑，智能手机等。
3.speech	应用于屏幕阅读器等发声设备

+ media feature包括:
> 
1.device-height	定义输出设备的屏幕可见高度。
2.device-width	定义输出设备的屏幕可见宽度。
3.max-width	定义输出设备中的页面最大可见区域宽度。
4.max-height	定义输出设备中的页面最大可见区域高度。
5.min-height	定义输出设备中的页面最小可见区域高度。
6.min-width	定义输出设备中的页面最小可见区域宽度。
7.min-resolution	定义设备的最小分辨率。
8.max-resolution	定义设备的最大分辨率。

### CSS Flexbox或者Grid specs

### 垂直居中
http://www.ydcss.com/archives/497

### 实现1px的border，要求在不同的分辨率的设备上都是1px
+ [Retina屏的移动设备如何实现真正1px的线？](http://jinlong.github.io/2015/05/24/css-retina-hairlines/)
+ 所谓“Retina”是一种显示技术，可以将更多的像素点压缩至一块屏幕里，从而达到更高的分辨率并提高屏幕显示的细腻程度。

+ 原理是把原先元素的 border 去掉，然后利用 :before 或者 :after 重做 border ，并 transform 的 scale 缩小一半，原先的元素相对定位，新做的 border 绝对定位
```
.hairlines li{
    position: relative;
    border:none;
}
.hairlines li:after{
    content: '';
    position: absolute;
    left: 0;
    background: #000;
    width: 100%;
    height: 1px;
    -webkit-transform: scaleY(0.5);
            transform: scaleY(0.5);
    -webkit-transform-origin: 0 0;
            transform-origin: 0 0;
}
```


### rem和em的区别

+ px像素（Pixel）。相对长度单位。像素px是相对于显示器屏幕分辨率而言的。
+ em: 是相对长度单位。相对于当前对象内文本的字体尺寸。如当前对行内文本的字体尺寸未被人为设置，则相对于浏览器的默认字体尺寸。1. em的值并不是固定的； em会继承父级元素的字体大小。
+ rem是CSS3新增的一个相对单位。

> 相对性
单位em是相对于父元素的，如果父元素没有设置字体大小，那就会追溯到body。
单位rem是相对于根元素（html）




