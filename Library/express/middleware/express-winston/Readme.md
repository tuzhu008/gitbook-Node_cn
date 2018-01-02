# express-winston
[![Monthly Downloads](https://img.shields.io/npm/dm/express-winston.svg)](https://www.npmjs.com/package/express-winston) [![Build Status](https://secure.travis-ci.org/bithavoc/express-winston.png)](http://travis-ci.org/bithavoc/express-winston)

> [winston](https://github.com/winstonjs/winston) middleware for express.js

## 安装

```
npm install winston express-winston
```

(支持 node >= 0.10)

## 用法

express-winston 为您的 express.js 应用程序的请求和错误日志记录提供中间件。它使用 “白名单” 从请求和 (new in 0.2.x) 响应对象中选择属性。


要使用 express-winston，您需要将以下内容添加到您的应用程序中：

In `package.json`:

```
{
  "dependencies": {
    "...": "...",
    "winston": "^2.0.0",
    "express-winston": "^2.0.0",
    "...": "..."
  }
}
```

在 `server.js` 中(或任何你需要的地方):

```
var winston = require('winston'),
    expressWinston = require('express-winston');
```

### 请求记录

使用 `expressWinston.logger(options)` 创建一个中间件来记录你的 HTTP 请求。

``` js
    var router = require('./my-express-router');

    app.use(expressWinston.logger({
      transports: [
        new winston.transports.Console({
          json: true,
          colorize: true
        })
      ],
      meta: true, // 可选: 控制是否要记录有关请求的元数据 (默认为 true)
      msg: "HTTP {{req.method}} {{req.url}}", // 可选: 定制默认日志消息. 例如 "{{res.statusCode}} {{req.method}} {{res.responseTime}}ms {{req.url}}"
      expressFormat: true, // 使用默认的 Express/morgan 请求格式化。如果为 true 则启用，将覆盖任何消息。只会输出 colorize 设置为 true的颜色
      colorize: false, // 使用 Express/morgan 颜色调色板为文本和状态码着色 (text: gray, status: 默认为 green, 3XX cyan, 4XX yellow, 5XX red).
      ignoreRoute: function (req, res) { return false; } // 可选: 允许根据请求 和/或 响应跳过一些日志消息
    }));

    app.use(router); // 注意路由器如何在记录器之后。
```

#### 选项

``` js
    transports: [<WinstonTransport>], // list of all winston transports instances to use.
    winstonInstance: <WinstonLogger>, // a winston logger instance. If this is provided the transports option is ignored.
    level: String or function(req, res) { return String; }, // log level to use, the default is "info". Assign a  function to dynamically set the level based on request and response, or a string to statically set it always at that level. statusLevels must be false for this setting to be used.
    msg: String // customize the default logging message. E.g. "{{res.statusCode}} {{req.method}} {{res.responseTime}}ms {{req.url}}", "HTTP {{req.method}} {{req.url}}".
    expressFormat: Boolean, // Use the default Express/morgan request formatting. Enabling this will override any msg if true. Will only output colors when colorize set to true
    colorize: Boolean, // Color the text and status code, using the Express/morgan color palette (text: gray, status: default green, 3XX cyan, 4XX yellow, 5XX red).
    meta: Boolean, // control whether you want to log the meta data about the request (default to true).
    baseMeta: Object, // default meta data to be added to log, this will be merged with the meta data.
    metaField: String, // if defined, the meta data will be added in this field instead of the meta root object.
    statusLevels: Boolean or Object // different HTTP status codes caused log messages to be logged at different levels (info/warn/error), the default is false. Use an object to control the levels various status codes are logged at. Using an object for statusLevels overrides any setting of options.level.
    ignoreRoute: function (req, res) { return false; } // A function to determine if logging is skipped, defaults to returning false. Called _before_ any later middleware.
    skip: function(req, res) { return false; } // A function to determine if logging is skipped, defaults to returning false. Called _after_ response has already been sent.
    requestFilter: function (req, propName) { return req[propName]; } // A function to filter/return request values, defaults to returning all values allowed by whitelist. If the function returns undefined, the key/value will not be included in the meta.
    responseFilter: function (res, propName) { return res[propName]; } // A function to filter/return response values, defaults to returning all values allowed by whitelist. If the function returns undefined, the key/value will not be included in the meta.
    requestWhitelist: [String] // Array of request properties to log. Overrides global requestWhitelist for this instance
    responseWhitelist: [String] // Array of response properties to log. Overrides global responseWhitelist for this instance
    bodyWhitelist: [String] // Array of body properties to log. Overrides global bodyWhitelist for this instance
    bodyBlacklist: [String] // Array of body properties to omit from logs. Overrides global bodyBlacklist for this instance
    ignoredRoutes: [String] // Array of paths to ignore/skip logging. Overrides global ignoredRoutes for this instance
    dynamicMeta: function(req, res) { return [Object]; } // Extract additional meta data from request or response (typically req.user data if using passport). meta must be true for this function to be activated

```

### 错误日志

使用 `expressWinston.errorLogger(options)` 创建一个中间件来记录管道（pipeline）错误。

``` js
    var router = require('./my-express-router');

    app.use(router); // 请注意路由器在前面
    app.use(expressWinston.errorLogger({
      transports: [
        new winston.transports.Console({
          json: true,
          colorize: true
        })
      ]
    }));
```

日志记录器需要在 express 路由器(`app.router)`)之后添加，并在您的自定义错误处理程序(`express.handler`)之前添加。由于 express-winston 只会记录错误而不**处理**它们，所以您仍然可以使用您的自定义错误处理程序，如 `express.handler`，请确保在您的任何处理程序之前将日志记录器放在前面。

#### 选项

``` js
    transports: [<WinstonTransport>], // list of all winston transports instances to use.
    winstonInstance: <WinstonLogger>, // a winston logger instance. If this is provided the transports option is ignored
    msg: String // customize the default logging message. E.g. "{{err.message}} {{res.statusCode}} {{req.method}}".
    baseMeta: Object, // default meta data to be added to log, this will be merged with the error data.
    metaField: String, // if defined, the meta data will be added in this field instead of the meta root object.
    requestFilter: function (req, propName) { return req[propName]; } // A function to filter/return request values, defaults to returning all values allowed by whitelist. If the function returns undefined, the key/value will not be included in the meta.
    requestWhitelist: [String] // Array of request properties to log. Overrides global requestWhitelist for this instance
    level: String or function(req, res, err) { return String; }// custom log level for errors (default is 'error'). Assign a function to dynamically set the log level based on request, response, and the exact error.
    dynamicMeta: function(req, res, err) { return [Object]; } // Extract additional meta data from request or response (typically req.user data if using passport). meta must be true for this function to be activated
```

要使用 winston 的现有传输，将 `transports` 设置为 `winston.default.transports` 对象的值（键-值）。下面的例子，通过使用 [underscore.js](https://github.com/jashkenas/underscore) 来完成：`transports：_.values（winston.default.transports）`。

或者，如果您在其他地方使用 winston 记录器实例，并且已经设置了 `levels` 和 `transports`，则使用 `winstonInstance` 选项将该实例传递到 expressWinston。 然后 `transports` 选项被忽略。


## 示例

``` js
    var express = require('express');
    var expressWinston = require('express-winston');
    var winston = require('winston'); // for transports.Console
    var app = module.exports = express();

    app.use(express.bodyParser());
    app.use(express.methodOverride());

    // Let's make our express `Router` first.
    var router = express.Router();
    router.get('/error', function(req, res, next) {
      // here we cause an error in the pipeline so we see express-winston in action.
      return next(new Error("This is an error and it should be logged to the console"));
    });

    app.get('/', function(req, res, next) {
      res.write('This is a normal request, it should be logged to the console too');
      res.end();
    });

    // express-winston logger makes sense BEFORE the router.
    app.use(expressWinston.logger({
      transports: [
        new winston.transports.Console({
          json: true,
          colorize: true
        })
      ]
    }));

    // Now we can tell the app to use our routing code:
    app.use(router);

    // express-winston errorLogger makes sense AFTER the router.
    app.use(expressWinston.errorLogger({
      transports: [
        new winston.transports.Console({
          json: true,
          colorize: true
        })
      ]
    }));

    // Optionally you can include your custom error handler after the logging.
    app.use(express.errorLogger({
      dumpExceptions: true,
      showStack: true
    }));

    app.listen(3000, function(){
      console.log("express-winston demo listening on port %d in %s mode", this.address().port, app.settings.env);
    });
```


浏览 `/` 会看到像这样的常规 HTTP 日志记录：

```
    {
      "req": {
        "httpVersion": "1.1",
        "headers": {
          "host": "localhost:3000",
          "connection": "keep-alive",
          "accept": "*/*",
          "user-agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_4) AppleWebKit/536.11 (KHTML, like Gecko) Chrome/20.0.1132.57 Safari/536.11",
          "accept-encoding": "gzip,deflate,sdch",
          "accept-language": "en-US,en;q=0.8,es-419;q=0.6,es;q=0.4",
          "accept-charset": "ISO-8859-1,utf-8;q=0.7,*;q=0.3",
          "cookie": "connect.sid=nGspCCSzH1qxwNTWYAoexI23.seE%2B6Whmcwd"
        },
        "url": "/",
        "method": "GET",
        "originalUrl": "/",
        "query": {}
      },
      "res": {
        "statusCode": 200
      },
      "responseTime" : 12,
      "level": "info",
      "message": "HTTP GET /favicon.ico"
    }
```

浏览 `/error` 会向你展示 express-winston 如何处理和记录 express 管道中的错误，如下所示：

```
    {
      "date": "Thu Jul 19 2012 23:39:44 GMT-0500 (COT)",
      "process": {
        "pid": 35719,
        "uid": 501,
        "gid": 20,
        "cwd": "/Users/thepumpkin/Projects/testExpressWinston",
        "execPath": "/usr/local/bin/node",
        "version": "v0.6.18",
        "argv": [
          "node",
          "/Users/thepumpkin/Projects/testExpressWinston/app.js"
        ],
        "memoryUsage": {
          "rss": 14749696,
          "heapTotal": 7033664,
          "heapUsed": 5213280
        }
      },
      "os": {
        "loadavg": [
          1.95068359375,
          1.5166015625,
          1.38671875
        ],
        "uptime": 498086
      },
      "trace": [
        ...,
        {
          "column": 3,
          "file": "Object].log (/Users/thepumpkin/Projects/testExpressWinston/node_modules/winston/lib/winston/transports/console.js",
          "function": "[object",
          "line": 87,
          "method": null,
          "native": false
        }
      ],
      "stack": [
        "Error: This is an error and it should be logged to the console",
        "    at /Users/thepumpkin/Projects/testExpressWinston/app.js:39:15",
        "    at callbacks (/Users/thepumpkin/Projects/testExpressWinston/node_modules/express/lib/router/index.js:272:11)",
        "    at param (/Users/thepumpkin/Projects/testExpressWinston/node_modules/express/lib/router/index.js:246:11)",
        "    at pass (/Users/thepumpkin/Projects/testExpressWinston/node_modules/express/lib/router/index.js:253:5)",
        "    at Router._dispatch (/Users/thepumpkin/Projects/testExpressWinston/node_modules/express/lib/router/index.js:280:4)",
        "    at Object.handle (/Users/thepumpkin/Projects/testExpressWinston/node_modules/express/lib/router/index.js:45:10)",
        "    at next (/Users/thepumpkin/Projects/testExpressWinston/node_modules/express/node_modules/connect/lib/http.js:204:15)",
        "    at done (/Users/thepumpkin/Dropbox/Projects/express-winston/index.js:91:14)",
        "    at /Users/thepumpkin/Dropbox/Projects/express-winston/node_modules/async/lib/async.js:94:25",
        "    at [object Object].log (/Users/thepumpkin/Projects/testExpressWinston/node_modules/winston/lib/winston/transports/console.js:87:3)"
      ],
      "req": {
        "httpVersion": "1.1",
        "headers": {
          "host": "localhost:3000",
          "connection": "keep-alive",
          "cache-control": "max-age=0",
          "user-agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_4) AppleWebKit/536.11 (KHTML, like Gecko) Chrome/20.0.1132.57 Safari/536.11",
          "accept": "text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8",
          "accept-encoding": "gzip,deflate,sdch",
          "accept-language": "en-US,en;q=0.8,es-419;q=0.6,es;q=0.4",
          "accept-charset": "ISO-8859-1,utf-8;q=0.7,*;q=0.3",
          "cookie": "connect.sid=nGspCCSzH1qxwNTWYAoexI23.seE%2B6WhmcwdzFEjqhMDuIIl3mAUY7dT4vn%2BkWvRPhZc"
        },
        "url": "/error",
        "method": "GET",
        "originalUrl": "/error",
        "query": {}
      },
      "level": "error",
      "message": "middlewareError"
    }
```

## 全局白名单和黑名单

Express-winston 暴露了三个白名单，控制了被记录的 `request`, `body`, 和 `response 的属性：

* `requestWhitelist`
* `bodyWhitelist`, `bodyBlacklist`
* `responseWhitelist`

例如, `requestWhitelist` 默认为:

```
['url', 'headers', 'method', 'httpVersion', 'originalUrl', 'query'];
```

只有上面这些请求对象的属性才会被记录下来。根据需要设置或修改白名单。

例如，要包含会话属性(会话数据)，在 logger 设置过程中添加以下内容:

```js
expressWinston.requestWhitelist.push('session');
```

黑名单会排除某些属性，并保留所有其他属性。如果同时设置了 `bodyWhitelist` 和 `bodyBlacklist` ，那么被黑名单排除的属性即使出现在白名单里照样还是会被排除。

示例:

```js
expressWinston.bodyBlacklist.push('secretid', 'secretproperty');
```

注意，您可以记录整个请求和/或响应主体:

```js
  expressWinston.requestWhitelist.push('body');
  expressWinston.responseWhitelist.push('body');
```

## 指定路由的白名单和黑名单


版本 0.2.x 中新增的功能是在路由中添加白名单元素。 express-winston 添加一个 `_routeWhitelists` 对象到 `req`uest，包含`.body`，`.req` 和 `.res` 属性，您可以在其中设置一个包含在日志中的“白名单”参数数组， 明确到有问题的路由：

``` js
    router.post('/user/register', function(req, res, next) {
      req._routeWhitelists.body = ['username', 'email', 'age']; // But not 'password' or 'confirm-password' or 'top-secret'
      req._routeWhitelists.res = ['_headers'];
    });
```

Post to `/user/register` would give you something like the following:

```
    {
      "req": {
        "httpVersion": "1.1",
        "headers": {
          "host": "localhost:3000",
          "connection": "keep-alive",
          "accept": "*/*",
          "user-agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_4) AppleWebKit/536.11 (KHTML, like Gecko) Chrome/20.0.1132.57 Safari/536.11",
          "accept-encoding": "gzip,deflate,sdch",
          "accept-language": "en-US,en;q=0.8,es-419;q=0.6,es;q=0.4",
          "accept-charset": "ISO-8859-1,utf-8;q=0.7,*;q=0.3",
          "cookie": "connect.sid=nGspCCSzH1qxwNTWYAoexI23.seE%2B6Whmcwd"
        },
        "url": "/",
        "method": "GET",
        "originalUrl": "/",
        "query": {},
        "body": {
          "username": "foo",
          "email": "foo@bar.com",
          "age": "72"
        }
      },
      "res": {
        "statusCode": 200
      },
      "responseTime" : 12,
      "level": "info",
      "message": "HTTP GET /favicon.ico"
    }
```

黑名单仅支持 `body` 属性。


``` js
    router.post('/user/register', function(req, res, next) {
      req._routeWhitelists.body = ['username', 'email', 'age']; // But not 'password' or 'confirm-password' or 'top-secret'
      req._routeBlacklists.body = ['username', 'password', 'confirm-password', 'top-secret'];
      req._routeWhitelists.res = ['_headers'];
    });
```

If both `req._bodyWhitelist.body` and `req._bodyBlacklist.body` are set the result will be the white listed properties
excluding any black listed ones. In the above example, only 'email' and 'age' would be included.


## 自定义状态等级

如果您将 `statusLevels` 设置为 `true` ，那么 express-winston 将在 `info` 级别上记录下 400 个响应，将 500 个响应作为警告，并将 500 + 个响应作为错误。要更改这些级别，请指定以下对象
```json
  "statusLevels": {
    "success": "debug",
    "warn": "debug",
    "error": "info"
  }
```

## 动态状态等级

如果您将 `statusLevels` 设置为 `false`，并分配一个函数作为 `level`，那么您可以为任何场景定制日志级别。

```js
  statusLevels: false // default value
  level: function (req, res) {
    var level = "";
    if (res.statusCode >= 100) { level = "info"; }
    if (res.statusCode >= 400) { level = "warn"; }
    if (res.statusCode >= 500) { level = "error"; }
    // Ops is worried about hacking attempts so make Unauthorized and Forbidden critical
    if (res.statusCode == 401 || res.statusCode == 403) { level = "critical"; }
    // No one should be using the old path, so always warn for those
    if (req.path === "/v1" && level === "info") { level = "warn"; }
    return level;
  }
```


## 来自请求或响应的动态元数据

如果设置了 `dynamicMeta` 函数，则可以从请求或响应对象中提取其他元数据字段。
该函数可以用来选择请求或响应体中的相关元素，而不需要将它们作为一个整体进行记录，或者像用户提出请求的那样提取运行时数据。 下面的例子记录了 Passport 认证中间件分配的用户名和角色。

```js
   meta: true,
   dynamicMeta: function(req, res) {
     return {
       user: req.user ? req.user.username : null,
       role: req.user ? req.user.role : null,
       ...
   }
}
```

## 测试

运行基本的 Mocha 测试:

```
npm test
```

运行 Travis-CI 测试 (这将失败，因为 < 100% 覆盖率):

```
npm run test-travis
```

生成 `coverage.html` 覆盖率报告：

```
npm run test-coverage
```

## 问题和协作

如果遇到任何问题，请使用该项目 [Issues 部分](https://github.com/bithavoc/express-winston/issues) 来搜索或发布任何错误。

## 贡献者

* [Johan Hernandez](https://github.com/bithavoc) (https://github.com/bithavoc)
* [Lars Jacob](https://github.com/jaclar) (https://github.com/jaclar)
* [Jonathan Lomas](https://github.com/floatingLomas) (https://github.com/floatingLomas)
* [Ross Brandes](https://github.com/rosston) (https://github.com/rosston)

Also see AUTHORS file, add yourself if you are missing.

## MIT License

Copyright (c) 2012-2014 Bithavoc.io and Contributors - http://bithavoc.io

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NON-INFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
