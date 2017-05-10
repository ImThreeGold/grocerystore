### 1. 幻灯效果页面
container宽度按实际情况确定，overflow:hidden
content 宽度=container宽*img的个数
切换img时，对每一个img使用transition过渡动画，位置使用transform: translate3d
```html
<div class="container">
	<div class="conent">
		<img><img>
	<div>
<div>
```

### 2. 浏览器的URL中获取查询字符串参数

### 3. 数组去重手写代码

```js
var isFunction = function (fn) {
	return Object.prototype.toString.call(fn) === '[object Function]';
}

Array.prototype.distinct = function (keyThunk) {
	var arr = this;
	var dic = {};
	var result = [];
	keyThunk = isFunction(keyThunk) ? keyThunk : function (val) {
		return typeof (val) + val;
	}
	var hasUnderfined = false;
	var hasNull = false;
	for (var i = 0; i < arr.length; i++) {
		var type = typeof (arr[i]);
		if (arr[i] === null) {
			if (hasNull == true) {
				continue;
			}
			hasNull = true;
		}
		if (type === "undefined") {
			if (hasUnderfined) {
				continue;
			}
			hasUnderfined = true;
		}
		var key = keyThunk(arr[i]);
		if (!dic[key]) {
			dic[key] = arr[i];
			result.push(arr[i]);
		}
	}
	return result;
}

var arr = [{ val: 1 }, { val: 1 }, { val: 3 }];
console.log(arr.distinct().map(function (val) {
	return val.val
}));//[1]
console.log(arr.distinct(function (val) {
	return val.val;
}).map(function (val) {
	return val.val;
})) [1,3]
```

### 4. linux指令熟悉吗？查看磁盘大小的指令是哪个？
> du -h


