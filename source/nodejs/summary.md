# nodejs

### 1、node启动80端口服务，输出hello world

```
    var http = require('http');
    http.createServer(function(request, response){
        response.writeHead(200, {'Content-Type': 'text/plain'});
        response.end('Hello World Hello Wirld.\nOne Change.One restart\n');
    }).listen(80);
    console.log("server running at http://localhost:80/");
```