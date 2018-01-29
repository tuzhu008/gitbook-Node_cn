<p align="center">
  <img src="https://raw.github.com/nodejitsu/node-http-proxy/master/doc/logo.png"/>
</p>

node-http-proxy
=======

<p align="left">
 <a href="https://travis-ci.org/nodejitsu/node-http-proxy" target="_blank">
  <img src="https://travis-ci.org/nodejitsu/node-http-proxy.png"/></a>&nbsp;&nbsp;
 <a href="https://coveralls.io/r/nodejitsu/node-http-proxy" target="_blank">
  <img src="https://coveralls.io/repos/nodejitsu/node-http-proxy/badge.png"/></a>
</p>

`node-http-proxy` 是一个支持 websockets 的 HTTP 可编程代理库。
它适合于实现诸如反向代理和负载平衡器之类的组件。


### Table of Contents
  * [Installation](#installation)
  * [Upgrading from 0.8.x ?](#upgrading-from-08x-)
  * [Core Concept](#core-concept)
  * [Use Cases](#use-cases)
    * [Setup a basic stand-alone proxy server](#setup-a-basic-stand-alone-proxy-server)
    * [Setup a stand-alone proxy server with custom server logic](#setup-a-stand-alone-proxy-server-with-custom-server-logic)
    * [Setup a stand-alone proxy server with proxy request header re-writing](#setup-a-stand-alone-proxy-server-with-proxy-request-header-re-writing)
    * [Modify a response from a proxied server](#modify-a-response-from-a-proxied-server)
    * [Setup a stand-alone proxy server with latency](#setup-a-stand-alone-proxy-server-with-latency)
    * [Using HTTPS](#using-https)
    * [Proxying WebSockets](#proxying-websockets)
  * [Options](#options)
  * [Listening for proxy events](#listening-for-proxy-events)
  * [Shutdown](#shutdown)
  * [Miscellaneous](#miscellaneous)
    * [Test](#test)
    * [ProxyTable API](#proxytable-api)
    * [Logo](#logo)
  * [Contributing and Issues](#contributing-and-issues)
  * [License](#license)

###

`npm install http-proxy --save`

**[回到顶部](#table-of-contents)**

### 从 0.8.x 升级?

点击[这里](https://github.com/nodejitsu/node-http-proxy/blob/master/UPGRADING.md)

**[回到顶部](#table-of-contents)**

### 核心概念

`createProxyServer` 用于创建一个新的代理，
它接受一个 `options` 对象作为其参数([有效属性可参见](https://github.com/nodejitsu/node-http-proxy/blob/master/lib/http-proxy.js#L22-L50))

```javascript
var httpProxy = require('http-proxy');

var proxy = httpProxy.createProxyServer(options); // See (†)
```

除非在对象上调用 listen(..)，否则不会创建一个 web 服务器。见下文。

可以使用下面四种方法来返回对象：

* web `req, res, [options]` (用于代理常规的 HTTP(S) 请求)
* ws `req, socket, head, [options]` (用于代理 WS(S) 请求)
* listen `port` (一个函数，为了方便，它将对象包装在 web 服务器中)
* close `[callback]` (一个关闭内部网络服务器的函数，停止监听给定端口)

然后通过调用这些函数来代理请求

```javascript
http.createServer(function(req, res) {
  proxy.web(req, res, { target: 'http://mytarget.com:8080' });
});
```

可以使用事件发送器 API 来监听错误

```javascript
proxy.on('error', function(e) {
  ...
});
```

或使用回调 API

```javascript
proxy.web(req, res, { target: 'http://mytarget.com:8080' }, function(e) { ... });
```

当一个请求被代理时，它会遵循两个不同的管道(pipelines)([这里可用](https://github.com/nodejitsu/node-http-proxy/blob/master/lib/http-proxy/passes))，它将同时对 `req` 和 `res` 对象进行转换。
第一个管道(传入)负责创建和处理连接客户端到目标的流。
第二个管道(传出)负责创建和操作流，从您的目标，将数据返回给客户端。

**[回到顶部](#table-of-contents)**

### 用例

#### 设置一个基本的独立代理服务器

```js
var http = require('http'),
    httpProxy = require('http-proxy');
//
// 创建 proxy 服务器，并在 options 中设置 target
//
httpProxy.createProxyServer({target:'http://localhost:9000'}).listen(8000); // See (†)

//
// 创建 target 服务器
//
http.createServer(function (req, res) {
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.write('request successfully proxied!' + '\n' + JSON.stringify(req.headers, true, 2));
  res.end();
}).listen(9000);
```
†调用 `listen(..)` 触发 web 服务器的创建。否则，只是创建了代理实例。

**[回到顶部](#table-of-contents)**

#### 使用自定义的服务器逻辑来设置一个独立的代理

这个示例展示了如何使用自己的 HTTP 服务器来代理请求，还可以使用自己的逻辑来处理请求。

```js
var http = require('http'),
    httpProxy = require('http-proxy');

//
// 创建一个带有自定义应用程序逻辑的代理服务器
//
var proxy = httpProxy.createProxyServer({});

//
// 创建一个自定义服务器并
//调用 `proxy.web()` 来代理到目标的 web 请求
// 也可以使用 `proxy.ws()` 来代理一个 websockets 请求
//

var server = http.createServer(function(req, res) {
  // 可以在这里定义自定义的逻辑来爱处理这个请求
  // 然后代理这些请求
  proxy.web(req, res, { target: 'http://127.0.0.1:5060' });
});

console.log("listening on port 5050")
server.listen(5050);
```

**[回到顶部](#table-of-contents)**

#### 设置一个带有请求头重写的独立代理服务器

这个示例展示了如何使用您自己的 HTTP 服务器来代理一个请求，该服务器通过添加一个特殊的头来修改传出的代理请求。

```js
var http = require('http'),
    httpProxy = require('http-proxy');

//
// 创建一个带有自定义应用程序逻辑的代理服务器
//
var proxy = httpProxy.createProxyServer({});

//要在数据被发送之前修改代理连接，可以监听 'proxyReq' 事件
// 当事件被触发时，你将收到下面的参数：
// (http.ClientRequest proxyReq, http.IncomingMessage req,
//  http.ServerResponse res, Object options)。
// 当需要在到目标的代理连接被创建之前修改代理请求，这个机制是很有用的
proxy.on('proxyReq', function(proxyReq, req, res, options) {
  proxyReq.setHeader('X-Special-Proxy-Header', 'foobar');
});

var server = http.createServer(function(req, res) {
  // 可以在这里定义自定义的逻辑来爱处理这个请求
  // 然后代理这些请求
  proxy.web(req, res, {
    target: 'http://127.0.0.1:5060'
  });
});

console.log("listening on port 5050")
server.listen(5050);
```

**[回到顶部](#table-of-contents)**

#### 修改来自代理服务器的响应

有时，当您从原始服务器收到 HTML/XML 文档时，您希望在转发它之前修改它。

[Harmon](https://github.com/No9/harmon) 允许你以流的方式来做这件事，这样就可以将代理的压力保持在最低限度。

**[回到顶部](#table-of-contents)**

#### 设置一个具有延迟的独立代理服务器

```js
var http = require('http'),
    httpProxy = require('http-proxy');

//
// 创建一个带有延迟的代理服务器
//
var proxy = httpProxy.createProxyServer();

//
// 创建服务器，使操作等待一段时间，然后代理请求
//
http.createServer(function (req, res) {
  // 这将模拟执行 500 毫秒后执行的操作
  setTimeout(function () {
    proxy.web(req, res, {
      target: 'http://localhost:9008'
    });
  }, 500);
}).listen(8008);

//
// 创建目标服务器
//
http.createServer(function (req, res) {
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.write('request successfully proxied to: ' + req.url + '\n' + JSON.stringify(req.headers, true, 2));
  res.end();
}).listen(9008);
```

**[回到顶部](#table-of-contents)**

#### 使用 HTTPS

您可以激活安全 SSL 证书的验证到目标连接(避免自签署的证书)，只需在选项中设置 `secure: true`。

##### HTTPS -> HTTP

```js
//
// 在 HTTP 服务器前面创建 HTTPS 代理服务器
//
httpProxy.createServer({
  target: {
    host: 'localhost',
    port: 9009
  },
  ssl: {
    key: fs.readFileSync('valid-ssl-key.pem', 'utf8'),
    cert: fs.readFileSync('valid-ssl-cert.pem', 'utf8')
  }
}).listen(8009);
```

##### HTTPS -> HTTPS

```js
//
// 创建代理服务器监听端口 443
//
httpProxy.createServer({
  ssl: {
    key: fs.readFileSync('valid-ssl-key.pem', 'utf8'),
    cert: fs.readFileSync('valid-ssl-cert.pem', 'utf8')
  },
  target: 'https://localhost:9010',
  secure: true // 这取决于你的需求，可以为 false。
}).listen(443);
```

**[回到顶部](#table-of-contents)**

#### 代理 WebSockets

可以在选项中使用 `ws:true` 激活对代理的 websocket 支持。

```js
//
// 为 websockets 创建代理服务器
//
httpProxy.createServer({
  target: 'ws://localhost:9014',
  ws: true
}).listen(8014);
```

只需要调用 `ws(req, socket, head)` 方法就可以代理 websocket 请求。

```js
//
// 设置服务器来代理标准 HTTP 请求
//
var proxy = new httpProxy.createProxyServer({
  target: {
    host: 'localhost',
    port: 9015
  }
});
var proxyServer = http.createServer(function (req, res) {
  proxy.web(req, res);
});

//
// 监听 `upgrade` 时间，并代理 WebSocket 请求
//
proxyServer.on('upgrade', function (req, socket, head) {
  proxy.ws(req, socket, head);
});

proxyServer.listen(8015);
```

**[回到顶部](#table-of-contents)**

### 选项

`httpProxy.createProxyServer` 支持以下选项：

*  **target**: url string to be parsed with the url module
*  **forward**: url string to be parsed with the url module
*  **agent**: object to be passed to http(s).request (see Node's [https agent](http://nodejs.org/api/https.html#https_class_https_agent) and [http agent](http://nodejs.org/api/http.html#http_class_http_agent) objects)
*  **ssl**: object to be passed to https.createServer()
*  **ws**: true/false, if you want to proxy websockets
*  **xfwd**: true/false, adds x-forward headers
*  **secure**: true/false, if you want to verify the SSL Certs
*  **toProxy**: true/false, passes the absolute URL as the `path` (useful for proxying to proxies)
*  **prependPath**: true/false, Default: true - specify whether you want to prepend the target's path to the proxy path
*  **ignorePath**: true/false, Default: false - specify whether you want to ignore the proxy path of the incoming request (note: you will have to append / manually if required).
*  **localAddress**: Local interface string to bind for outgoing connections
*  **changeOrigin**: true/false, Default: false - changes the origin of the host header to the target URL
*  **preserveHeaderKeyCase**: true/false, Default: false - specify whether you want to keep letter case of response header key
*  **auth**: Basic authentication i.e. 'user:password' to compute an Authorization header.
*  **hostRewrite**: rewrites the location hostname on (201/301/302/307/308) redirects.
*  **autoRewrite**: rewrites the location host/port on (201/301/302/307/308) redirects based on requested host/port. Default: false.
*  **protocolRewrite**: rewrites the location protocol on (201/301/302/307/308) redirects to 'http' or 'https'. Default: null.
*  **cookieDomainRewrite**: rewrites domain of `set-cookie` headers. Possible values:
   * `false` (default): disable cookie rewriting
   * String: new domain, for example `cookieDomainRewrite: "new.domain"`. To remove the domain, use `cookieDomainRewrite: ""`.
   * Object: mapping of domains to new domains, use `"*"` to match all domains.
     For example keep one domain unchanged, rewrite one domain and remove other domains:
     ```
     cookieDomainRewrite: {
       "unchanged.domain": "unchanged.domain",
       "old.domain": "new.domain",
       "*": ""
     }
     ```
*  **headers**: object with extra headers to be added to target requests.
*  **proxyTimeout**: timeout (in millis) when proxy receives no response from target

**注意:**
`options.ws` 和 `options.ssl` 是可选的。
`options.target` 和 `options.forward` 不能同时缺失

如果使用 `proxyServer.listen` 方法，以下选项也适用:

 *  **ssl**: 对象被传递到  https.createServer()
 *  **ws**: true/false，如果你想要代理 websockets

**[回到顶部](#table-of-contents)**

### 监听代理事件

* `error`: The error event is emitted if the request to the target fail. **We do not do any error handling of messages passed between client and proxy, and messages passed between proxy and target, so it is recommended that you listen on errors and handle them.**
* `proxyReq`: This event is emitted before the data is sent. It gives you a chance to alter the proxyReq request object. Applies to "web" connections
* `proxyReqWs`: This event is emitted before the data is sent. It gives you a chance to alter the proxyReq request object. Applies to "websocket" connections
* `proxyRes`: This event is emitted if the request to the target got a response.
* `open`: This event is emitted once the proxy websocket was created and piped into the target websocket.
* `close`: This event is emitted once the proxy websocket was closed.
* (DEPRECATED) `proxySocket`: Deprecated in favor of `open`.

```js
var httpProxy = require('http-proxy');
// Error 示例
//
// 带有损坏的目标的代理服务器
//
var proxy = httpProxy.createServer({
  target:'http://localhost:9005'
});

proxy.listen(8005);

//
// Listen for the `error` event on `proxy`.
proxy.on('error', function (err, req, res) {
  res.writeHead(500, {
    'Content-Type': 'text/plain'
  });

  res.end('Something went wrong. And we are reporting a custom error message.');
});

//
// Listen for the `proxyRes` event on `proxy`.
//
proxy.on('proxyRes', function (proxyRes, req, res) {
  console.log('RAW Response from the target', JSON.stringify(proxyRes.headers, true, 2));
});

//
// Listen for the `open` event on `proxy`.
//
proxy.on('open', function (proxySocket) {
  // listen for messages coming FROM the target here
  proxySocket.on('data', hybiParseAndLogMessage);
});

//
// Listen for the `close` event on `proxy`.
//
proxy.on('close', function (res, socket, head) {
  // view disconnected websocket connections
  console.log('Client disconnected');
});
```

**[回到顶部](#table-of-contents)**

### 关闭

* 当在另一个程序中测试或运行服务器时，可能需要关闭代理。
* 这将阻止代理接受新的连接。

```js
var proxy = new httpProxy.createProxyServer({
  target: {
    host: 'localhost',
    port: 1337
  }
});

proxy.close();
```

**[回到顶部](#table-of-contents)**

### 其他

#### ProxyTable API

通过附加[模块](https://github.com/donasaur/http-proxy-rules)，proxy table API 是可用的，它允许你定义一组规则来将匹配的路由转换成反向代理将与之交流的目标路由。

#### 测试

```
$ npm test
```

#### Logo

Logo 由 [Diego Pasquali](http://dribbble.com/diegopq) 设计

**[回到顶部](#table-of-contents)**

### 贡献和问题

* Read carefully our [Code Of Conduct](https://github.com/nodejitsu/node-http-proxy/blob/master/CODE_OF_CONDUCT.md)
* Search on Google/Github
* If you can't find anything, open an issue
* If you feel comfortable about fixing the issue, fork the repo
* Commit to your local branch (which must be different from `master`)
* Submit your Pull Request (be sure to include tests and update documentation)

**[回到顶部](#table-of-contents)**

### License

>The MIT License (MIT)
>
>Copyright (c) 2010 - 2016 Charlie Robbins, Jarrett Cruger & the Contributors.
>
>Permission is hereby granted, free of charge, to any person obtaining a copy
>of this software and associated documentation files (the "Software"), to deal
>in the Software without restriction, including without limitation the rights
>to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
>copies of the Software, and to permit persons to whom the Software is
>furnished to do so, subject to the following conditions:
>
>The above copyright notice and this permission notice shall be included in
>all copies or substantial portions of the Software.
>
>THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
>IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
>FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
>AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
>LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
>OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
>THE SOFTWARE.
