
### 1. http状态码
[HTTP状态码详解](http://www.daqianduan.com/4280.html)

| 状态代码 |            状态信息            |                                       含义 |
| ---- | :------------------------: | ---------------------------------------: |
| 100  |          Continue          |               初始的请求已经接受，客户应当继续发送请求的其余部分。 |
| 200  |             OK             |               一切正常，对GET和POST请求的应答文档跟在后面。 |
| 201  |          Created           |            服务器已经创建了文档，Location头给出了它的URL。 |
| 202  |          Accepted          |                          已经接受请求，但处理尚未完成。 |
| 301  |     Moved Permanently      | 客户请求的文档在其他地方，新的URL在Location头中给出，浏览器应该自动地访问新的URL。 |
| 302  |           Found            |        类似于301，但新的URL应该被视为临时性的替代，而不是永久性的。 |
| 304  |        Not Modified        |                 服务器告 诉客户，原来缓冲的文档还可以继续使用。 |
| 400  |        Bad Request         |                                请求出现语法错误。 |
| 401  |        Unauthorized        |                      客户试图未经授权访问受密码保护的页面。 |
| 403  |         Forbidden          | 资源不可用。服务器理解客户的请求，但拒绝处理它。通常由于服务器上文件或目录的权限设置导致。 |
| 404  |         Not Found          |                  无法找到指定位置的资源。这也是一个常用的应答。 |
| 405  |     Method Not Allowed     | 请求方法（GET、POST、HEAD、DELETE、PUT、TRACE等）对指定的资源不适用 |
| 500  |   Internal Server Error    |                 服务器遇到了意料不到的情况，不能完成客户的请求。 |
| 505  | HTTP Version Not Supported |                      服务器不支持请求中所指明的HTTP版本 |


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
> 不能很好的发现错误，并进行处理。

+  使用 CORS 实现跨域调用

+  Cross-Origin Resource Sharing（CORS）跨域资源共享是一份浏览器技术的规范，提供了 Web 服务从不同域传来沙盒脚本的方法，以避开浏览器的同源策略，是 JSONP 模式的现代版。与 JSONP 不同，CORS 除了 GET 要求方法以外也支持其他的 HTTP 要求。用 CORS 可以让网页设计师用一般的 XMLHttpRequest，这种方式的错误处理比 JSONP 要来的好。另一方面，JSONP 可以在不支持 CORS 的老旧浏览器上运作。现代的浏览器都支持 CORS。

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

> CORS 除了 GET 方法外，也支持其它的 HTTP 请求方法如 POST、 PUT 等。
> CORS 可以使用 XmlHttpRequest 进行传输，所以它的错误处理方式比 JSONP 好。
> JSONP 可以在不支持 CORS 的老旧浏览器上运作。

+ 一些其它的跨域调用方式

+ window.name

> window对象有个name属性，该属性有个特征：即在一个窗口 (window) 的生命周期内，窗口载入的所有的页面都是共享一个 window.name 的，每个页面对 window.name 都有读写的权限，window.name 是持久存在一个窗口载入过的所有页面中的，并不会因新页面的载入而进行重置。

+ window.postMessage()

> 这个方法是 HTML5 的一个新特性，可以用来向其他所有的 window 对象发送消息。需要注意的是我们必须要保证所有的脚本执行完才发送 MessageEvent，如果在函数执行的过程中调用了他，就会让后面的函数超时无法执行。

### 3.get和post区别

[99%的人理解错 HTTP 中 GET 与 POST 的区别](http://www.oschina.net/news/77354/http-get-post-different)

| 描述        |                   GET                    |                   POST                   |
| --------- | :--------------------------------------: | :--------------------------------------: |
| 历史        |         参数会被存在浏览器历史中，因为作为URL的一部分         |                不存在浏览器历史中                 |
| 书签        |                 可以书签可收藏                  |                   不可以                    |
| 后退按钮/重复提交 |         请求可以再次执行，如果有浏览器缓存则不会再次提交         |              浏览器一般会询问是否重复提交              |
| 编码类型      |    application/x-www-form-urlencoded     | multipart/form-data 、 application/x-www-form-urlencoded 、 multipart（二进制数据） |
| 参数        |    有限制，数据会放到URL上。建议使用2K以内，有些服务器支持到64K    |              没有限制，甚至可以上传文件               |
| 攻击        |                 比较容易被攻击                  |                   不容易                    |
| 对表单数据类型限制 |               有，只允许ASCII字符               |               没有，二进制数据也可以                |
| 安全        |           没有POST安全，因为数据放在URL上            |                 比GET安全些                  |
| 数据长度限制    | 数据放在URL上，URL长度有限制。一般URL限制2048个字符，但是不同浏览器和服务器有差异 |                   没有限制                   |
| 可用性       |             密码和敏感的信息是不使用GET的             |             密码和敏感的信息可以使用GET的             |
| 可以性       |           对所有人可见的，因为信息显示在URL上            |                信息不显示在URL上                |
| 缓存的       |                    可以                    |                   不可以                    |

[详细比较](http://www.diffen.com/difference/GET-vs-POST-HTTP-Requests)

业界不成文的规定是，（大多数）浏览器通常都会限制url长度在2K个字节，而（大多数）服务器最多处理64K大小的url。所以get请求因为浏览器和服务端限制导致传参有限制。post理论上参数大小无限制，取决于服务器端设置及内存大小

+ GET产生一个TCP数据包；POST产生两个TCP数据包。
对于GET方式的请求，浏览器会把http header和data一并发送出去，服务器响应200（返回数据）.
而对于POST，浏览器先发送header，服务器响应100 continue，浏览器再发送data，服务器响应200 ok（返回数据）。

### 4. cookie和session是什么，作用，区别，安全性，大小限制

具体来说cookie机制采用的是在客户端保持状态的方案，而session机制采用的是在服务器端保持状态的方案。
cookie 和session 的区别：
+ cookie数据存放在客户的浏览器上，session数据放在服务器上。
+ cookie不是很安全，别人可以分析存放在本地的COOKIE并进行COOKIE欺骗考虑到安全应当使用session。
+ session会在一定时间内保存在服务器上。当访问增多，会比较占用你服务器的性能考虑到减轻服务器性能方面，应当使用COOKIE。
+ 单个cookie保存的数据不能超过4K，很多浏览器都限制一个站点最多保存20个cookie。

















