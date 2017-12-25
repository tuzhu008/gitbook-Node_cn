# Connect

[![NPM Version][npm-image]][npm-url]
[![NPM Downloads][downloads-image]][downloads-url]
[![Build Status][travis-image]][travis-url]
[![Test Coverage][coveralls-image]][coveralls-url]

  Connect 是一个适用于 [node](http://nodejs.org) 的可扩展 HTTP 服务器框架，使用的是称为 _中间件_ 的“插件”。

```js
var connect = require('connect');
var http = require('http');

var app = connect();

// gzip/deflate 发出响应（outgoing responses）
var compression = require('compression');
app.use(compression());

// 在浏览器 cookie 存储会话状态
var cookieSession = require('cookie-session');
app.use(cookieSession({
    keys: ['secret1', 'secret2']
}));

// 将经过编码的请求体解析到 req.body中
var bodyParser = require('body-parser');
app.use(bodyParser.urlencoded({extended: false}));

// 对所有请求作出应答。
app.use(function(req, res){
  res.end('Hello from Connect!\n');
});

// 创建node.js http 服务器，并监听端口
http.createServer(app).listen(3000);
```

## 开始

Connect 是一个简单的框架，可以将各种“中间件”粘合在一起处理请求。

### 安装

```sh
$ npm install connect
```

### 创建一个 app

主要的组件是 Connect "app"。它将存储所有被添加的中间件，它本身是一个函数。

```js
var app = connect();
```

### 使用中间件

Connect 的核心是 "using" 中间件。中间件被作为“堆栈”添加，其中传入的请求将逐个地执行每个中间件，直到一个中间件在它内部不再调用 `next()`。

```js
app.use(function middleware1(req, res, next) {
  // 中间件 1
  next();
});
app.use(function middleware2(req, res, next) {
  // 中间件 2
  next();
});
```

### Mount middleware

`.use()` 方法还使用一个可选的路径字符串，该字符串与传入请求 URL 的开头相匹配。这允许进行基路由。

```js
app.use('/foo', function fooMiddleware(req, res, next) {
  // req.url 以 "/foo" 开头
  next();
});
app.use('/bar', function barMiddleware(req, res, next) {
  // req.url 以 "/bar" 开头
  next();
});
```

### 错误中间件

有一些特殊的“错误处理”中间件。
这里有一些中间件，其中的函数恰好有4个参数。
当中间件将一个错误传递给 `next`时，该应用程序将继续寻找在该中间件之后声明的错误中间件并调用它，
这会跳过出错的中间件之上的任何错误中间件和它下面的任何非错误中间件。

> **[info] 「译者注」：**
>
> 在出现错误时，查找错误处理的中间件这个操作是从当前发生错误的中间件开始的。在它之前的错误中间件以及之后的非错误中间件都会被忽略。


```js
// 常规的中间件
app.use(function (req, res, next) {
  // 出现错误
  next(new Error('boom!'));
});

// 用于处理发生的错误的错误中间件
// 这个错误发生在错误中间件之前声明的中间件中
app.use(function onerror(err, req, res, next) {
  // an error occurred!
});
```

### 从 app 创建服务器

最后一步是在服务器中实际使用 Connect app。
`.listen()` 方法是启动 HTTP 服务器的一种便捷方式(与 Node.js 中运行 `http.Server` 的 `listen` 方法相同)。

```js
var server = app.listen(port);
```

这个 app 本身就是一个有三个参数的函数， 所以在 Node.js 中它可以被传递给  `.createServer()`。

```js
var server = http.createServer(app);
```

## 中间件

这些中间件和库得到了 Connect/Express 团队的正式支持:

  - [body-parser](https://www.npmjs.com/package/body-parser) - previous `bodyParser`, `json`, and `urlencoded`. You may also be interested in:
    - [body](https://www.npmjs.com/package/body)
    - [co-body](https://www.npmjs.com/package/co-body)
    - [raw-body](https://www.npmjs.com/package/raw-body)
  - [compression](https://www.npmjs.com/package/compression) - previously `compress`
  - [connect-timeout](https://www.npmjs.com/package/connect-timeout) - previously `timeout`
  - [cookie-parser](https://www.npmjs.com/package/cookie-parser) - previously `cookieParser`
  - [cookie-session](https://www.npmjs.com/package/cookie-session) - previously `cookieSession`
  - [csurf](https://www.npmjs.com/package/csurf) - previously `csrf`
  - [errorhandler](https://www.npmjs.com/package/errorhandler) - previously `error-handler`
  - [express-session](https://www.npmjs.com/package/express-session) - previously `session`
  - [method-override](https://www.npmjs.com/package/method-override) - previously `method-override`
  - [morgan](https://www.npmjs.com/package/morgan) - previously `logger`
  - [response-time](https://www.npmjs.com/package/response-time) - previously `response-time`
  - [serve-favicon](https://www.npmjs.com/package/serve-favicon) - previously `favicon`
  - [serve-index](https://www.npmjs.com/package/serve-index) - previously `directory`
  - [serve-static](https://www.npmjs.com/package/serve-static) - previously `static`
  - [vhost](https://www.npmjs.com/package/vhost) - previously `vhost`

它们中的大多数都是 Connect 2.x 内置中间件的确切端口（也就是这些内置中间件使用了这些库）。主要的例外是 `cookie-session`。


以前包含的一些中间件不再被 Connect/express 团队支持，取而代之的是一个替代模块，或者应该被一个更好的模块所取代。使用其中一个替代方案:

  - `cookieParser`
    - [cookies](https://www.npmjs.com/package/cookies) and [keygrip](https://www.npmjs.com/package/keygrip)
  - `limit`
    - [raw-body](https://www.npmjs.com/package/raw-body)
  - `multipart`
    - [connect-multiparty](https://www.npmjs.com/package/connect-multiparty)
    - [connect-busboy](https://www.npmjs.com/package/connect-busboy)
  - `query`
    - [qs](https://www.npmjs.com/package/qs)
  - `staticCache`
    - [st](https://www.npmjs.com/package/st)
    - [connect-static](https://www.npmjs.com/package/connect-static)

查看 [http-framework](https://github.com/Raynos/http-framework/wiki/Modules)获取其他兼容的中间件!

## API

Connect API 信奉极简主义，足以创建一个 app 并添加一个中间件链。

当 `connect` 被加载时，返回一个函数，这个函数将在被调用时构造一个新的 app。


```js
// 加载模块
var connect = require('connect')

// 创建 app
var app = connect()
```

### app(req, res[, next])

 `app` 本身是一个函数。这只不过是 `app.handle` 的别名。

### app.handle(req, res[, out])

调用该函数将针对给定的 Node.js http 请求(`req`)和响应(`res`)对象运行中间件堆栈。
如果请求(或错误)没有由中间件堆栈处理，则可以提供一个可选的 `out` 函数。

### app.listen([...])

启动 app 监听请求。该方法将在内部创建一个 Node.js HTTP 服务器并调用 `.listen()`。

在 Node.js 运行的版本中，这是 `server.listen()` 方法的一个别名，所以可以参考 Node.js 文档来获取所有不同的变种。
最常见的签名是 [`app.listen(port)`](https://nodejs.org/dist/latest-v6.x/docs/api/http.html#http_server_listen_port_hostname_backlog_callback).

### app.use(fn)

在 app 中使用一个函数，该函数表示一个中间件。该函数将根据调用 `app.use` 的顺序为每个请求调用。这个函数有三个参数:

```js
app.use(function (req, res, next) {
  // req 是 Node.js http 请求对象
  // res 是 Node.js http 响应对象
  // next 是一个函数，用来调用下一个中间件
})
```

除了计划函数之外，`fn` 参数也可以是一个 Node.js  HTTP 服务器实例或另一个 Connect app 实例。

### app.use(route, fn)

在 app 中使用一个函数，该函数表示一个中间件。
该函数将为以给定 `route` 字符串开头的 URL (`req.url` 属性) 的请求调用，按照调用 `app.use` 的顺序。
这个函数有三个参数:


```js
app.use('/foo', function (req, res, next) {
  // req 是 Node.js http 请求对象
  // res 是 Node.js http 响应对象
  // next 是一个函数，用来调用下一个中间件
})
```

除了计划函数之外，`fn` 参数也可以是一个 Node.js  HTTP 服务器实例或另一个 Connect app 实例。


`route` 总是在路径分隔符(`/`)或点(`.`)字符终止。
这意味着给定的路由 `/foo/` 和 `/foo`是相同的，它们都将匹配 URL `/foo`、`/foo/`、 `/foo/bar`和 `/foo.bar` 的请求。但不匹配 URL `/foobar` 的请求。

 `route` 与不区分大小写的 manor 相匹配。

为了使中间件更容易编写，以不确定 `route` 的方式，当 `fn` 被调用时，`req.url` 将被修改，以删除 `route` 部分(原始的内容将作为 `req.originalUrl` )。例如，如果在路由 `/foo` 使用 `fn`，则对 `/foo/bar` 的请求将使用 `req.url === '/bar'` 和 `req.originalUrl === '/foo/bar'` 调用 `fn`。


## 运行测试

```bash
npm install
npm test
```

## People

如果没有所有的人参与，Connect 项目就不一样了。

Connect 的原始作者是 [TJ Holowaychuk](https://github.com/tj) [![TJ's Gratipay][gratipay-image-visionmedia]][gratipay-url-visionmedia]

当前的主要维护人员是 [Douglas Christopher Wilson](https://github.com/dougwilson) [![Doug's Gratipay][gratipay-image-dougwilson]][gratipay-url-dougwilson]

[所有贡献者的列表](https://github.comsenchalabs/connect/graphs/contributors)

## Node 兼容性

  - Connect `< 1.x` - node `0.2`
  - Connect `1.x` - node `0.4`
  - Connect `< 2.8` - node `0.6`
  - Connect `>= 2.8 < 3` - node `0.8`
  - Connect `>= 3` - node `0.10`, `0.12`, `4.x`, `5.x`, `6.x`, `7.x`, `8.x`; io.js `1.x`, `2.x`, `3.x`

## 许可

[MIT](LICENSE)

[npm-image]: https://img.shields.io/npm/v/connect.svg
[npm-url]: https://npmjs.org/package/connect
[travis-image]: https://img.shields.io/travis/senchalabs/connect/master.svg
[travis-url]: https://travis-ci.org/senchalabs/connect
[coveralls-image]: https://img.shields.io/coveralls/senchalabs/connect/master.svg
[coveralls-url]: https://coveralls.io/r/senchalabs/connect
[downloads-image]: https://img.shields.io/npm/dm/connect.svg
[downloads-url]: https://npmjs.org/package/connect
[gratipay-image-dougwilson]: https://img.shields.io/gratipay/dougwilson.svg
[gratipay-url-dougwilson]: https://www.gratipay.com/dougwilson/
[gratipay-image-visionmedia]: https://img.shields.io/gratipay/visionmedia.svg
[gratipay-url-visionmedia]: https://www.gratipay.com/visionmedia/
