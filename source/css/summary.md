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
StylusStylus、Sass、less

### CSS框架
Bootstrap,PureCSS,Foundation

### 栅格系统

### 媒体查询

### CSS Flexbox或者Grid specs

### 垂直居中
http://www.ydcss.com/archives/497

### 如何实现响应式布局

### 实现1px的border，要求在不同的分辨率的设备上都是1px

### rem和em的区别






