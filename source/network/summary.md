### 1. http状态码


### 2. 如何解决跨域，允许跨域设置头部的内容是什么

+ JSONP:JSONP 是 JSON 的一种使用模式，可以解决主流浏览器的跨域数据访问问题。其原理是根据 XmlHttpRequest 对象受到同源策略的影响，而` <script> `标签元素却不受同源策略影响，可以加载跨域服务器上的脚本，网页可以从其他来源动态产生 JSON 资料。用 JSONP 获取的不是 JSON 数据，而是可以直接运行的 JavaScript 语句。

+ 使用 jQuery 集成的 $.ajax 实现 JSONP 跨域调用

客户端
```js
$.ajax({
        url: 'http://localhost:3001/ajax/deal',
        data: data,
        dataType: 'jsonp',
        cache: false,
        timeout: 5000,
        // jsonp 字段含义为服务器通过什么字段获取回调函数的名称
        jsonp: 'callback',
        // 声明本地回调函数的名称，jquery 默认随机生成一个函数名称
        jsonpCallback: 'jsonpCallback',
        success: function(data) {
            console.log("ajax success callback: " + data.name)
        },
        error: function(jqXHR, textStatus, errorThrown) {
            console.log(textStatus + ' ' + errorThrown);
        }
    });
```
服务端
```js
app.get('/ajax/deal', function(req, res) {
    console.log("server accept: ", req.query.name, req.query.id)
    var data = "{" + "name:'" + req.query.name + " - server 3001 process'," + "id:'" + req.query.id + " - server 3001 process'" +"}"
    var callback = req.query.callback
    var jsonp = callback + '(' + data + ')'
    console.log(jsonp)
    res.send(jsonp)
    res.end()
})
```
+ 使用 `<script>	` 标签原生实现 JSONP

+ JSONP的不足：
> 只能使用 GET 方法发起请求，这是由于 script 标签自身的限制决定的。
不能很好的发现错误，并进行处理。

+  使用 CORS 实现跨域调用

+ Cross-Origin Resource Sharing（CORS）跨域资源共享是一份浏览器技术的规范，提供了 Web 服务从不同域传来沙盒脚本的方法，以避开浏览器的同源策略，是 JSONP 模式的现代版。与 JSONP 不同，CORS 除了 GET 要求方法以外也支持其他的 HTTP 要求。用 CORS 可以让网页设计师用一般的 XMLHttpRequest，这种方式的错误处理比 JSONP 要来的好。另一方面，JSONP 可以在不支持 CORS 的老旧浏览器上运作。现代的浏览器都支持 CORS。

服务端：
```js
app.post('/cors', function(req, res) {
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    res.header("Access-Control-Allow-Methods", "PUT,POST,GET,DELETE,OPTIONS");
    res.header("X-Powered-By", ' 3.2.1')
    res.header("Content-Type", "application/json;charset=utf-8");
    var data = {
        name: req.body.name + ' - server 3001 cors process',
        id: req.body.id + ' - server 3001 cors process'
    }
    console.log(data)
    res.send(data)
    res.end()
})
```

+ CORS 与 JSONP 的对比

+ CORS 除了 GET 方法外，也支持其它的 HTTP 请求方法如 POST、 PUT 等。
+ CORS 可以使用 XmlHttpRequest 进行传输，所以它的错误处理方式比 JSONP 好。
+ JSONP 可以在不支持 CORS 的老旧浏览器上运作。

+ 一些其它的跨域调用方式

+ window.name

> window对象有个name属性，该属性有个特征：即在一个窗口 (window) 的生命周期内，窗口载入的所有的页面都是共享一个 window.name 的，每个页面对 window.name 都有读写的权限，window.name 是持久存在一个窗口载入过的所有页面中的，并不会因新页面的载入而进行重置。

+ window.postMessage()

> 这个方法是 HTML5 的一个新特性，可以用来向其他所有的 window 对象发送消息。需要注意的是我们必须要保证所有的脚本执行完才发送 MessageEvent，如果在函数执行的过程中调用了他，就会让后面的函数超时无法执行。











