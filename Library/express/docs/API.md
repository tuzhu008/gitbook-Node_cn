<p style="font-size=35px;font-weight=700"> Express 4.x API 中文手册 </p>

# express() {#express}

创建一个 Express 应用。`express()` 是一个由 **express** 模块导出的入口（top-level）函数。

```js
var express = require('express');
var app = express();
```

## 内置方法

### express.static(root, [options])

`express.static` 是 Express 内置的**唯一**一个中间件。是基于 [serve-static](https://github.com/expressjs/serve-static) 开发的，负责托管 Express 应用内的静态资源。

  * `root` 参数指的是静态资源文件所在的根目录。
  * `options` 对象是可选的，支持以下属性：

属性           | 描述             | 类型     | 默认值
---------------|--------------|----------|-------------
`dotfiles`     | 用于 serving dotfiles的选项。可选值有：“allow”、“deny” 和 “ignore”  | String   | "ignore"
`etag`         | 启用或禁用 etag 生成      | Boolean  | `true`
`extensions`   | 设置文件扩展名回退。  | Boolean  | `false`
`index`        | 发送目录索引文件。设置为 `false` 来禁用目录索引 | Mixed    | "index.html"
`lastModified` | 将 `Last-Modified` 头设置为在操作系统上的最后一个修改日期。| Boolean  | `true`
`maxAge`       | 设置 Cache-Control 头的 max-age 属性，以毫秒为单位或一个 [ms `format`][] 的字符串| Number   | 0
`redirect`     | 当路径名是一个目录时，重定向到 “/”。 | Boolean  | `true`
`setHeaders`   | 用于设置 HTTP 头文件的函数。 | Function | -

[ms `format`]: https://www.npmjs.org/package/ms


# Application {#application}

`app` 对象通常表示 Express 应用程序。通过调用由 Express 模块导出的顶级 `express()` 函数来创建它:

```js
var express = require('express');
var app = express();

app.get('/', function(req, res){
  res.send('hello world');
});

app.listen(3000);
```

`app` 对象有一些方法，用于：

  * 路由 HTTP 请求； 查看示例， [app.METHOD](#app.METHOD) 和 [app.param](#app.param).
  * 配置中间件；参见 [app.route](#app.route).
  * 渲染 HTML 视图；参见 [app.render](#app.render).
  * 注册模板引擎；参见 [app.engine](#app.engine).

它还具有影响应用程序行为的设置(属性)；要获得很多信息，参见 [app 设置表](#app_settings-table).

## 属性

### app.locals {#app_locals}

`app.locals` 是一个 JavaScript 对象，它的属性是应用程序内的局部变量。

```js
app.locals.title
// => 'My App'

app.locals.email
// => 'me@myapp.com'
```

一旦设置，`app.locals` 属性在应用程序的整个生命周期中都存在，而 [res.locals](#res.locals) 属性只对请求的生命周期有效。

您可以在应用程序中渲染的模板中访问 `local` 变量。这对于为模板提供辅助函数以及应用程序级的数据非常有用。但是请注意，您**不能**在中间件中访问本地变量。

```js
app.locals.title = 'My App';
app.locals.strftime = require('strftime');
app.locals.email = 'me@myapp.com';
```

### app.mountpath

`app.mountpath` 属性是挂载子应用的路径模式(s)。

> **[info]** 子应用是 `express` 的一个实例，它可以用于处理到路由的请求。

```js
var express = require('express');

var app = express(); // 主 app
var admin = express(); // 子 app

admin.get('/', function (req, res) {
  console.log(admin.mountpath); // /admin
  res.send('Admin Homepage');
})

app.use('/admin', admin); // 挂载子 app
```

它类似于 `req` 对象的 [baseUrl](#req.baseUrl) 属性，除了 `req.baseUrl` 返回匹配的 URL 路径，而不是匹配的模式(s)。

如果一个子应用被挂载在多个路径模式上，`app.mountpath` 返回所挂载的模式列表。如下面的例子所示：

```js
var admin = express();

admin.get('/', function (req, res) {
  console.log(admin.mountpath); // [ '/adm*n', '/manager' ]
  res.send('Admin Homepage');
})

var secret = express();
secret.get('/', function (req, res) {
  console.log(secret.mountpath); // /secr*t
  res.send('Admin Secret');
});

admin.use('/secr*t', secret); // load the 'secret' router on '/secr*t', on the 'admin' sub app
app.use(['/adm*n', '/manager'], admin); // load the 'admin' router on '/adm*n' and '/manager', on the parent app
```

## 事件

### app.on('mount', callback(parent)) {#app_mount-event}

当子应用被挂载到父应用的时候，`mount` 事件在子应用上被触发。父应用被传递给该事件的回调函数。

```js
var admin = express();

admin.on('mount', function (parent) {
  console.log('Admin Mounted');
  console.log(parent); // 指的是父应用（app）
});

admin.get('/', function (req, res) {
  res.send('Admin Homepage');
});

app.use('/admin', admin);
```

## 方法

### app.all(path, callback [, callback ...]) {#app_all}

这个方法相似于标准的 [app.METHOD()](#app.METHOD) 方法，除了它匹配的是所有的 HTTP 动词。

它对于映射特定路径前缀或任意匹配的 “全局” 逻辑非常有用。例如，如果您将下面的内容放在所有其他路由定义的顶部，那么它要求从该点开始的所有路由都需要身份验证，并自动加载用户。记住，这些回调不需要作为端点: `loadUser` 可以执行一个任务，然后调用 `next()` 继续匹配后续路由。

```js
app.all('*', requireAuthentication, loadUser);
```

或相当于:

```js
app.all('*', requireAuthentication)
app.all('*', loadUser);
```

另一个例子是白名单上的“全局”功能。这个例子和之前的很相似，但是它只限制了以 “/api” 开头的路径:

```js
app.all('/api/*', requireAuthentication);
```

### app.delete(path, callback [, callback ...]) {#app_delete}

使用指定的回调函数路由 HTTP DELETE 请求到指定的路径。要获取更多信息，请参见[路由指南](http://www.expressjs.com.cn/guide/routing.html)。

您可以提供与中间件类似的多个回调函数，但是这些回调可以调用 `next('route')` 来绕过余下的路由回调。您可以使用该机制在路由上设置前置条件，然后在没有理由继续当前路由的情况下将控制权传递给后续路由。

```js
app.delete('/', function (req, res) {
  res.send('DELETE request to homepage');
});
```


### app.disable(name) {#app_disable}

将布尔属性 `name` 设置为 `false`，其中 `name` 是 [app 设置表](#app_settings-table) 中的一个属性。对于一个布尔值属性来说，调用 `app.set('foo', false)` 和调用 `app.disable('foo')` 是一样的。

例如:

```js
app.disable('trust proxy');
app.get('trust proxy');
// => false
```

### app.disabled(name) {#app_disabled}

如果布尔值属性 `name` 现在是禁用的 (`false`)，则返回 `true`，其中 `name` 是 [app 设置表](#app_settings-table) 中的一个。

```js
app.disabled('trust proxy');
// => true

app.enable('trust proxy');
app.disabled('trust proxy');
// => false
```

### app.enable(name) {#app_enable}


将布尔属性 `name` 设置为 `true`，其中 `name` 是 [app 设置表](#app_settings-table) 中的一个属性。对于一个布尔值属性来说，调用 `app.set('foo', true)` 和调用 `app.enable('foo')` 是一样的。

```js
app.enable('trust proxy');
app.get('trust proxy');
// => true
```

### app.enabled(name) {#app_enabled}

如果布尔值属性 `name` 现在是启用的 (`true`)，则返回 `true`，其中 `name` 是 [app 设置表](#app_settings-table) 中的一个。

```js
app.enabled('trust proxy');
// => false

app.enable('trust proxy');
app.enabled('trust proxy');
// => true
```


### app.engine(ext, callback) {#app_engine}


将给定的模板引擎 `callback` 注册为 `ext`。

默认情况下，Express 将基于文件扩展名 `require()` 引擎。例如，如果您试图渲染一个 “foo.jade” 文件，Express 在内部调用以下内容，并在后续调用中缓存 `require()` 以提高性能。

```js
app.engine('jade', require('jade').__express);
```

对不提供的开箱即用的 `.__express` 的引擎使用这种方法，或者如果您想要“映射”一个不同的扩展到模板引擎。

例如，将 EJS 模板引擎映射到 “.html” 文件:

```js
app.engine('html', require('ejs').renderFile);
```

在这种情况下，EJS 提供了一个 `.renderFile()` 方法，它具有与 Express 所期望的相同的签名：`(path, options, callback)`，但是请注意，在内部，这个方法别名为 `ejs.__express`，所以如果使用 “.ejs” 扩展名，你不需要做任何事情。

一些模板引擎不遵循这个约定。[consolidate.js](https://github.com/tj/consolidate.js) 库将 Node 模板引擎映射为遵循这个约定，所以它们与 Express 一起工作得很好。

```js
var engines = require('consolidate');
app.engine('haml', engines.haml);
app.engine('html', engines.hogan);
```


### app.get(name) {#app_get}

返回应用设置 `name` 的值，其中 `name` 是 [app 设置表](#app_settings-table) 中的一个。

例如:

```js
app.get('title');
// => undefined

app.set('title', 'My Site');
app.get('title');
// => "My Site"
```

### app.get(path, callback [, callback ...]) {#app_get_req}

使用指定的回调函数路由 HTTP GET 请求到指定的路径。要获取更多信息，请参见[路由指南](http://www.expressjs.com.cn/guide/routing.html)。

您可以提供与中间件类似的多个回调函数，但是这些回调可以调用 `next('route')` 来绕过余下的路由回调。您可以使用该机制在路由上设置前置条件，然后在没有理由继续当前路由的情况下将控制权传递给后续路由。

```js
app.get('/', function (req, res) {
  res.send('GET request to homepage');
});
```

### app.listen(port, [hostname], [backlog], [callback]) {#app_listen}

在指定的主机和端口上绑定和监听连接。这个方法和 Node 的 [http.Server.listen()](http://nodejs.org/api/http.html#http_server_listen_port_hostname_backlog_callback) 是相同的。

```js
var express = require('express');
var app = express();
app.listen(3000);
```

`express()` 返回的 `app` 实际上是一个 JavaScript `Function`，被设计来作为回调传递给 Node 的 HTTP 服务器，用来处理请求。这使得提供使用相同的代码的 app 的 HTTP 和 HTTPS 版本变得简单，因为 app 不会从它们那继承（它只是一个回调）：

```js
var express = require('express');
var https = require('https');
var http = require('http');
var app = express();

http.createServer(app).listen(80);
https.createServer(options, app).listen(443);
```

`app.listen()` 方法是一个便捷方法，如下所示 (仅用于 HTTP):

```js
app.listen = function() {
  var server = http.createServer(this);
  return server.listen.apply(server, arguments);
};
```


### app.METHOD(path, callback [, callback ...]) {#app_METHOD}

路由 HTTP 请求，METHOD 是请求的 HTTP 方法，如 GET、PUT、POST 等等，以小写形式。因此，实际的方法是 `app.get()`、 `app.post()`、` app.put()` 等等。请参阅下面的完整列表。

要获取更多信息，请参见[路由指南](http://www.expressjs.com.cn/guide/routing.html)。

Express 支持下面的路由方法，对应 HTTP 相同名字的方法：

    * checkout
    * connect
    * copy
    * delete
    * get
    * head
    * lock
    * merge
    * mkactivity
    * mkcol
    * move
    * m-search
    * notify
    * options
    * patch
    * post
    * propfind
    * proppatch
    * purge
    * put
    * report
    * search
    * subscribe
    * trace
    * unlock
    * unsubscribe


> **[info]** 要路由那些转换为无效 JavaScript 变量名的方法，请使用括号表示法。 例如,  `app['m-search']('/', function ...`.


您可以提供与中间件类似的多个回调函数，但是这些回调可以调用 `next('route')` 来绕过余下的路由回调。您可以使用该机制在路由上设置前置条件，然后在没有理由继续当前路由的情况下将控制权传递给后续路由。

> **[info]**  API 文档只对流行的 HTTP 方法有显式的条目，如 `app.get()`、 `app.post()`、 `app.put()` 和 `app.delete()`。然而，上面列出的其他方法的工作方式完全相同。

有一种特殊的路由方法，`app.all()`，这并不派生自任何 HTTP 方法。它在所有请求方法的路径上装载中间件。

在下面的例子中，用于 “/secret” 请求的处理程序被执行，它使用 GET、POST、PUT、DELETE 或任何其他 HTTP 请求方法。

```js
app.all('/secret', function (req, res, next) {
  console.log('Accessing the secret section ...')
  next() // pass control to the next handler
})
```

### app.param([name], callback) {#app_param}

添加回调触发器到路由参数，其中 `name` 是参数的名称或参数名称数组，`callback` 是回调函数。 回调函数的参数依次是请求对象，响应对象，下一个中间件和参数的值也是这个顺序。`function(req, res, next)`。

如果 `name` 是一个数组，`callback` 触发器就会按照声明的顺序为数组中的每个参数进行注册。此外，除了最后一个声明的参数外，回调函数内调用 `next` 将调用下一个声明参数的回调函数。对于最后一个参数，调用 `next` 将调用正在处理的路由的下一个中间件，就像 `name` 只是一个字符串一样。

例如，当 `:user` 存在于路由路径中时，可以映射用户加载逻辑以自动向路由提供 `req.user`，或对参数输入执行验证。

```js
app.param('user', function(req, res, next, id) {

  // 尝试从 User 模块获取用户细节，并将其附加到请求对象
  User.find(id, function(err, user) {
    if (err) {
      next(err);
    } else if (user) {
      req.user = user;
      next();
    } else {
      next(new Error('failed to load user'));
    }
  });
});
```

参数回调函数在它们被定义的路由器上是本地的。它们不会被挂载的应用或路由器继承。因此，`app` 上定义的参数回调将仅由 `app` 路由上定义的路由参数触发。

所有参数回调将在参数发生的任何路由的任何处理程序之前被调用，并且在请求 - 响应周期中，每个参数回调都仅被调用**一次**，即使参数在多个路径中匹配，如以下示例所示。

```js
app.param('id', function (req, res, next, id) {
  console.log('CALLED ONLY ONCE');
  next();
})

app.get('/user/:id', function (req, res, next) {
  console.log('although this matches');
  next();
});

app.get('/user/:id', function (req, res) {
  console.log('and this matches too');
  res.end();
});
```

`GET /user/42` 时，打印如下：

```
CALLED ONLY ONCE
although this matches
and this matches too
```

```js
app.param(['id', 'page'], function (req, res, next, value) {
  console.log('CALLED ONLY ONCE with', value);
  next();
})

app.get('/user/:id/:page', function (req, res, next) {
  console.log('although this matches');
  next();
});

app.get('/user/:id/:page', function (req, res) {
  console.log('and this matches too');
  res.end();
});
```

`GET /user/42/3` 时，打印如下：

```
CALLED ONLY ONCE with 42
CALLED ONLY ONCE with 3
although this matches
and this matches too
```

> **[danger]** 以下部分描述的 app.param(callback)，从 v4.11.0 开始不推荐使用。

`app.param(name, callback)` 方法的行为完全可以通过只传递一个函数到 `app.param()` 来改变。 这个函数是 `app.param(name, callback)` 应该如何表现的自定义实现 - 它接受两个参数，并且必须返回一个中间件。

这个函数的第一个参数是应该被捕获的 URL 参数的名字，第二个参数可以是任何可用于返回中间件实现的 JavaScript 对象。

该函数返回的中间件决定了捕获 URL 参数时发生的情况。

在这个例子中，`app.param(name, callback)` 签名被修改为 `app.param(name, accessId)`。 `app.param()` 现在接受一个名字和一个数字，而不是接受一个名字和一个回调，

```js
var express = require('express');
var app = express();

// customizing the behavior of app.param()
app.param(function(param, option) {
  return function (req, res, next, val) {
    if (val == option) {
      next();
    }
    else {
      res.sendStatus(403);
    }
  }
});

// using the customized app.param()
app.param('id', 1337);

// route to trigger the capture
app.get('/user/:id', function (req, res) {
  res.send('OK');
})

app.listen(3000, function () {
  console.log('Ready');
})
```

在这个例子中，`app.param(name, callback)` 签名保持不变，定义了一个自定义的数据类型检查函数来验证用户 id 的数据类型，而不是中间件回调。

```js
app.param(function(param, validator) {
  return function (req, res, next, val) {
    if (validator(val)) {
      next();
    }
    else {
      res.sendStatus(403);
    }
  }
})

app.param('id', function (candidate) {
  return !isNaN(parseFloat(candidate)) && isFinite(candidate);
});
```

> **[success]**
>
> 在你的捕获正则种，‘.’ 字符不能被用来捕获一个字符。例如，你不能使用 '/user-.+/' 来捕获 'users-gami'，使用 [\\s\\S] 或 [\\w\\W] 代替 ('/user-[\\s\\S]+/'）.
>
> Examples:
>
> ```js
> //捕获 '1-a_6' 但不捕获 '543-azser-sder'
> router.get('/[0-9]+-[[\\w]]*', function);
>
> //捕获 '1-a_6' 和 '543-az(ser"-sder' but not '5-a s'
> router.get('/[0-9]+-[[\\S]]*', function);
>
> //捕获所有 (equivalent to '.*')
> router.get('[[\\s\\S]]*', function);
> ```


### app.path() {#app_path}

返回应用的规范路径，一个字符串。

```js
var app = express()
  , blog = express()
  , blogAdmin = express();

app.use('/blog', blog);
blog.use('/admin', blogAdmin);

console.log(app.path()); // ''
console.log(blog.path()); // '/blog'
console.log(blogAdmin.path()); // '/blog/admin'
```

在复杂的挂载应用中，这种方法的行为会变得非常复杂:使用 [req.baseUrl](#req.baseUrl) 来获得应用的规范路径通常会更好。


### app.post(path, callback [, callback ...]) {#app_post}

使用指定的回调函数来路由 HTTP POST 请求到指定路径。使用指定的回调函数路由 HTTP DELETE 请求到指定的路径。要获取更多信息，请参见[路由指南](http://www.expressjs.com.cn/guide/routing.html)。

您可以提供与中间件类似的多个回调函数，但是这些回调可以调用 `next('route')` 来绕过余下的路由回调。您可以使用该机制在路由上设置前置条件，然后在没有理由继续当前路由的情况下将控制权传递给后续路由。

```js
app.post('/', function (req, res) {
  res.send('POST request to homepage');
});
```

### app.put(path, callback [, callback ...]) {#app_put}

使用指定的回调函数来路由 HTTP PUT 请求到指定路径。使用指定的回调函数路由 HTTP DELETE 请求到指定的路径。要获取更多信息，请参见[路由指南](http://www.expressjs.com.cn/guide/routing.html)。

您可以提供与中间件类似的多个回调函数，但是这些回调可以调用 `next('route')` 来绕过余下的路由回调。您可以使用该机制在路由上设置前置条件，然后在没有理由继续当前路由的情况下将控制权传递给后续路由。

```js
app.put('/', function (req, res) {
  res.send('PUT request to homepage');
});
```


### app.render(view, [locals], callback) {#app_render}

通过 `callback` 函数返回一个视图的已渲染的HTML。它接受一个可选参数，该参数是一个包含该视图的局部变量的『对象』。它就像 [res.render()](#res.render)，除了它不能自己把渲染的视图发送给客户端。

> **[info]** 可以将 `app.render()` 看作是用来生成已渲染视图字符串的工具函数。`res.render()` 在内部使用 `app.render()` 来渲染视图。

-

> **[info]** 本地变量 `cache` 用于启用视图缓存。如果您希望在开发期间缓存视图，则将其设置为 `true`;默认情况下，在生产中启用了视图缓存。

```js
app.render('email', function(err, html){
  // ...
});

app.render('email', { name: 'Tobi' }, function(err, html){
  // ...
});
```

### app.route(path)

返回一个单一路由的实例，然后您可以使用它来处理带有可选中间件的 HTTP 动词。使用 `app.route()` 来避免重复的路由名称(以及拼写错误)。

```js
var app = express();

app.route('/events')
  .all(function(req, res, next) {
    // runs for all HTTP verbs first
    // think of it as route specific middleware!
  })
  .get(function(req, res, next) {
    res.json(...);
  })
  .post(function(req, res, next) {
    // maybe add a new event...
  })
```


### app.set(name, value) {#app_set}

将 `name` 设置为 `value`，其中 `name` 是来自 [app 设置表](#app_settings-table) 的属性中的一个。


Calling `app.set('foo', true)` for a Boolean property is the same as calling `app.enable('foo')`. Similarly, calling `app.set('foo', false)` for a Boolean property is the same as calling `app.disable('foo')`.

Retrieve the value of a setting with `app.get()`.

```js
app.set('title', 'My Site');
app.get('title'); // "My Site"
```

#### 应用设置 {#app_settings-table}

如果 `name` 是应用程序的设置之一，则会影响应用程序的行为。下表列出了应用程序的设置。

属性     |   类型    |     取值     | 默认值
-------------|-----------|---------------|-----------------
`case sensitive routing` | Boolean | 启用大小写区分   | `false`，表示禁用。"/Foo" 等同于 "/foo"。
`env`        | String  | 环境模式   | `process.env.NODE_ENV` (`NODE_ENV` 环境变黄) 或者 “development”.
`etag`      | Varied  | 设置 ETag 响应头。可能的值请参见 `etag` [options table](#etag-options).[更多关于 HTTP ETag 头的信息](http://en.wikipedia.org/wiki/HTTP_ETag). |
`jsonp callback name` | String	| 指定默认的 JSONP 回调名称。 | `?callback=`
`json replacer` | String	| JSON replacer callback. | `null`
`json spaces` | Number	| 当被设置时，发送使用指定数量的空格缩进美化的字符串| 禁用
`query parser` | String | 使用的查询解析器，“simple” or “extended”。简单的查询解析器基于 Node 原生的查询解析器，查询字符串。扩展的差序解析器基于 [qs][] | "extended"
`strict routing` | Boolean	| 启用严格的路由。	| `false`，禁用。"/foo" 和 "/foo/" 是等价的。
`subdomain offset` | Number	| 主机的点分隔的数字部分，用来删除访问子域。	| 2
`trust proxy` | Varied | 表示 app 位于前置代理(proxy)之后，并使用 `X-Forwarded-*` 头来确定客户端的连接和 IP 地址。 注意：`X-Forwarded-*` 头容易被欺骗，检测到的 IP 地址不可靠。默认情况下，`trust proxy` 被禁用。 启用后，Express 会尝试通过前置代理或一系列代理来确定连接的客户端的 IP 地址。 然后，`req.ips` 属性包含客户端连接的 IP 地址数组。要启用它，请使用 `trust proxy` [选项列表](#trust_proxy-options-table)中描述的值。`trust proxy `设置是通过 [proxy-addr][] 包来实现的。 有关更多信息，请参阅其文档。| Disabled.
`views` | String 或 Array	| 应用程序视图的目录或目录数组。如果为一个数组，视图会按照数组中出现的顺序查找。| `process.cwd() + '/views'`
`view cache` | Boolean	| 启用视图模板编译缓存 | 生产中为 `true`
`view engine` | String	| 当省略时使用的默认引擎扩展名。|-
`x-powered-by` | Boolean	| 启用 "X-Powered-By: Express" HTTP 头 | `true`

[proxy-addr]: https://www.npmjs.org/package/proxy-addr
[qs]: https://github.com/ljharb/qs

#### `trust proxy` 设置 {#trust_proxy-options-table}

  * Boolean
    - 如果为 `true`，客户端的 IP 地址被理解为 `X-Forwarded-*` 头中最左边的条目。
    - 如果为 `false`，该应用程序被理解为直接面向互联网，客户端的 IP 地址是从 `req.connection.remoteAddress` 派生的。这是默认设置。

  * IP 地址

    一个IP地址，子网或IP 地址数组以及要信任的子网。 以下是预配置的子网名称列表。

    - loopback - `127.0.0.1/8`, `::1/128`
    - linklocal - `169.254.0.0/16`, `fe80::/10`
    - uniquelocal - `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`, `fc00::/7`

    通过以下任何方式设置 IP 地址：

    ```js
    app.set('trust proxy', 'loopback') // 指定一个单一的子网
    app.set('trust proxy', 'loopback, 123.123.123.123') // 指定一个子网和一个地址
    app.set('trust proxy', 'loopback, linklocal, uniquelocal') // 指定多个子网为 CSV
    app.set('trust proxy', ['loopback', 'linklocal', 'uniquelocal']) // 指定多个子网作为数组
    ```

    当被指定时，将从地址确定过程中排除 IP 地址或子网，并将离应用程序服务器最近的不可信 IP 地址确定为客户端的 IP 地址。

  * Number

    信任来自前置代理服务器第 n 个跳转作为客户端。

  * Function

    自定义信任实现。只有当你知道你在做什么时才使用它。
    ```js
    app.set('trust proxy', function (ip) {
      if (ip === '127.0.0.1' || ip === '123.123.123.123') return true; // trusted IPs
      else return false;
    })
    ```

####  `etag` 设置的选项 {#etag-options}

* Boolean
  - `true` 启用弱 ETag。这是默认设置。
  - `false` 完全禁用 ETag。
* String

  如果为 "strong"，启用强 ETag。如果为 "weak"，则启用弱 ETag。
* Function

  自定义 ETag 函数实现。只有当你知道你在做什么时才使用它。
  ```js
  app.set('etag', function (body, encoding) {
    return generateHash(body, encoding); // consider the function is defined
    })
  ```


### app.use([path,] function [, function...]) {#app_use}

在 `path` 上挂载 [middleware](http://www.expressjs.com.cn/guide/using-middleware.html) `function(s)`
。如果 `path` 未被指定，默认为 “/”。

> **[info]** 路由将与任何路径匹配，这条路径将立即跟随一个 “/” 。例如: `app.use('/apple', ...)` 将匹配 “/apple”, “/apple/images”, “/apple/images/news”, 等等.

-

> **[info]**
>
> 中间件种的 `req.originalUrl` 是 `req.baseUrl` 和 `req.path` 的结合，如下面的例子所示。
>
> ```js
> app.use('/admin', function(req, res, next) {
>   // GET 'http://www.example.com/admin/new'
>   console.log(req.originalUrl); // '/admin/new'
>   console.log(req.baseUrl); // '/admin'
>   console.log(req.path); // '/new'
>   next();
> });
> ```

在 `path` 上挂载一个中间件将会导致在请求路径的基础与 `path` 匹配时执行中间件函数。

由于 `path` 默认为 “/”，没有路径的中间件将会在应用程序的每个请求中执行。

```js
// 该中间件将针对应用程序的每个请求执行。
app.use(function (req, res, next) {
  console.log('Time: %d', Date.now());
  next();
})
```

中间件函数是按顺序执行的，因此**中间件的顺序是很重要的**。

```js
// 这个中间件不允许请求超出它的要求
app.use(function(req, res, next) {
  res.send('Hello World');
})

// 请求永远不会到达这条路线
app.get('/', function (req, res) {
  res.send('Welcome');
})
```

`path` 可以是表示路径的字符串、路径模式、匹配路径的正则表达式或其组合的数组。


下面的中间件是简单的示例。


* 路径

  ```js
  // 将匹配以 /abcd 开始的路径
  app.use('/abcd', function (req, res, next) {
    next();
  })
  ```
* 路径模式

  ```js
  // 将匹配以 /abcd 和 /abd 开头的路径
  app.use('/abc?d', function (req, res, next) {
    next();
  })

  // 匹配以 /abcd，/abbcd，/abbbbbcd 等开始的路径
  app.use('/ab+cd', function (req, res, next) {
    next();
  })

  // 匹配以 /abcd, /abxcd, /abFOOcd, /abbArcd 等开始的路径
  app.use('/ab\*cd', function (req, res, next) {
    next();
  })

  // 匹配以 /ad 和 /abcd 开始的路径
  app.use('/a(bc)?d', function (req, res, next) {
    next();
  })
  ```

* 正则表达式

  ```js
  // 匹配以  /abc 和 /xyz 开始的路径
  app.use(/\/abc|\/xyz/, function (req, res, next) {
    next();
  })
  ```

* Array

  ```js
  // 匹配以 /abcd, /xyza, /lmn, 和 /pqr 开始的路径
  app.use(['/abcd', '/xyza', /\/lmn|\/pqr/], function (req, res, next) {
    next();
  })
  ```

`function` 可以是中间件函数、一系列中间件函数、一个中间件函数数组，或者是所有这些函数的组合。由于[route](#router) 和 [app](#app) 实现了中间件接口，所以您可以像使用任何其他中间件功能一样使用它们。

下面是一些用法和对应的示例：

* 单个中间件

  您可以在本地定义和挂载一个中间件函数。
  ```js
  app.use(function (req, res, next) {
    next();
  })
  ```
  路由器是有效的中间件。
  ```js
  var router = express.Router();
  router.get('/', function (req, res, next) {
    next();
  })
  app.use(router);
  ```
  Express app 是有效的中间件。
  ```js
  var subApp = express();
  subApp.get('/', function (req, res, next) {
    next();
  })
  app.use(subApp);
  ```
* 一系列的中间件

  您可以在相同的挂载路径中指定多个中间件函数。
  ```js
  var r1 = express.Router();
  r1.get('/', function (req, res, next) {
    next();
  })

  var r2 = express.Router();
  r2.get('/', function (req, res, next) {
    next();
  })

  app.use(r1, r2);
  ```
* 数组

  使用数组逻辑地对中间件进行分组。如果您将中间件作为第一个或唯一的中间件参数传递，那么您*必须*指定挂载路径。
  ```js
  var r1 = express.Router();
  r1.get('/', function (req, res, next) {
    next();
  })

  var r2 = express.Router();
  r2.get('/', function (req, res, next) {
    next();
  })

  app.use('/', [r1, r2]);
  ```
* 组合

  您可以将所有以上的挂载中间件的方法组合在一起。
  ```js
  function mw1(req, res, next) { next(); }
  function mw2(req, res, next) { next(); }

  var r1 = express.Router();
  r1.get('/', function (req, res, next) { next(); });

  var r2 = express.Router();
  r2.get('/', function (req, res, next) { next(); });

  var subApp = express();
  subApp.get('/', function (req, res, next) { next(); });

  app.use(mw1, [mw2, r1, r2], subApp);
  ```

下面是一些在 Express app 中使用  [express.static](http://www.expressjs.com.cn/guide/using-middleware.html#middleware.built-in) 中间件的例子。

从应用程序目录中的“public”目录中为应用程序提供静态内容:

```js
// GET /style.css etc
app.use(express.static(__dirname + '/public'));
```

只有当它们的请求路径带有 "/static" 前缀时，才会在 “/static” 中加载中间件来提供静态内容：

```js
// GET /static/style.css etc.
app.use('/static', express.static(__dirname + '/public'));
```

通过在静态中间件之后加载日志记录器中间件，为静态内容请求禁用日志记录:

```js
app.use(express.static(__dirname + '/public'));
app.use(logger());
```

从多个目录提供静态文件，但优先考虑 “./public”:

```js
app.use(express.static(__dirname + '/public'));
app.use(express.static(__dirname + '/files'));
app.use(express.static(__dirname + '/uploads'));
```

# Request {#request}

`req` 对象表示 HTTP 请求，并具有请求查询字符串、参数、主体、HTTP 头等的属性。在这个文档和约定中，对象总是被称为 `req` (HTTP 响应是 `res`)，但是它的实际名称是由您工作的回调函数的参数决定的。

例如:

```js
app.get('/user/:id', function(req, res){
  res.send('user ' + req.params.id);
});
```

但你也可以这样做:

```js
app.get('/user/:id', function(request, response){
  response.send('user ' + request.params.id);
});
```

## 属性

> **[warning]** 在 Express 4 中，默认情况下，`req` 对象上的 req.files 不再可用。要在 req.files 对象上访问上传的文件，请使用「多文件处理」中间件，例如 busboy、multer、[formidable]()、multipart、connect-multiparty、或者 pez.

[formidable]: https://tuzhu008.github.io/gitbook-Node_cn/Library/node-formidable/


### req.app {#req_app}

该属性对使用该中间件的 express 应用程序的实例进行了引用。

如果您遵循创建模块的模式，只需导出一个中间件，以便在您的主文件中 require 它，那么中间件就可以通过 `req.app` 访问 express 实例。

示例:

```js
//index.js
app.get("/viewdirectory", require("./mymiddleware.js"))
```

```js
//mymiddleware.js
module.exports = function (req, res) {
  res.send("The views directory is " + req.app.get("views"));
});
```

### req.baseUrl {#req_baseUrl}

路由器实例被挂载的 URL 路径。例如：

```js
var greet = express.Router();

greet.get('/jp', function (req, res) {
  console.log(req.baseUrl); // /greet
  res.send('Konichiwa!');
});

app.use('/greet', greet); // 在 '/greet' 上加载路由器
```

即使您使用路径模式或一个路径模式集合来加载路由器，`baseUrl` 属性将返回匹配的字符串，而不是模式(s)。在下面的示例中，`greet` 路由器被加载到两个路径模式中。

```js
app.use(['/gre+t', '/hel{2}o'], greet); // 在 '/gre+t' 和 '/hel{2}o' 上加载路由器
```

当请求为 `/greet/jp`, `req.baseUrl` 是 “/greet”。当请求为 `/hello/jp`, `req.baseUrl` 是 “/hello”.

`req.baseUrl` 类似于 `app` 对象上的 [`mountpath`](#app_mountpath) 属性，除了 `app.mountpath` 返回的是匹配的路径模式。


### req.body {#req_body}

包含在请求主体中提交的数据的键值对。默认情况下，它是 `undefined`，并且在使用 [body-parsing](https://www.npmjs.org/package/body-parser) 和 [multer](https://www.npmjs.org/package/multer) 这样的请求体解析中间件时被填充。

这个例子展示了如何使用 body-parsin 中间件来填充 `req.body`。

```js
var app = require('express')();
var bodyParser = require('body-parser');
var multer = require('multer');

app.use(bodyParser.json()); // for parsing application/json
app.use(bodyParser.urlencoded({ extended: true })); // for parsing application/x-www-form-urlencoded
app.use(multer()); // for parsing multipart/form-data

app.post('/', function (req, res) {
  console.log(req.body);
  res.json(req.body);
})
```


### req.cookies {#req_cookies}


当使用 [cookie-parser](https://www.npmjs.com/package/cookie-parser) 中间件时，设个属性将是一个对象，它包含了由请求发送的 cookie。如果这个请求没包含 cookie，那它默认为 {}。

```
// Cookie: name=tj
req.cookies.name
// => "tj"
```

要了解更多信息、问题或关注，请参阅 [cookie-parser](https://www.npmjs.com/package/cookie-parser).


### req.fresh {#req_fresh}


表示当前请求是否“新鲜”。这与 `req.stale` 相反。

如果 `cache-control` 请求头没有一个 `no-cache` 指令，下面的任何一条都是 true 的:

  *  if-modified-since 的请求头被指定，而 last-modified 请求头等于或早于 modified 响应头。
  *  if-none-match 请求头为 *.
  *  if-none-match 请求头，在被解析到它的指令之后，不匹配 etag 响应头。


```js
req.fresh
// => true
```
要了解更多信息、问题或关注，请参阅 [fresh](https://github.com/jshttp/fresh).


### req.hostname {#req_hostname}

包含来自 “Host” HTTP 头的主机名。

```
// Host: "example.com:3000"
req.hostname
// => "example.com"
```


### req.ip {#req_ip}

请求的远程 IP 地址。

如果 `trust proxy` 被设置为启用，它将是上游地址；参见 [Express behind proxies](http://www.expressjs.com.cn/guide/behind-proxies.html) 获得更多信息。

```
req.ip
// => "127.0.0.1"
```


### req.ips {#req_ips}

当 `trust proxy` 设置为 `true` 时，这个属性包含了一个在 “X-Forwarded-For” 请求头种指定的 IP 地址数组。否则，它包含一个空数组。

例如，如果 “X-Forwarded-For” 是 “client, proxy1, proxy2”，`req.ips` 将会是 `["client", "proxy1", "proxy2"]`，其中 “proxy2” 是最遥远的下游。

要获得更多关于 `trust proxy` 设置的信息，请参见 [app.set](#app_set).

### req.originalUrl {#req_originalUrl}

> **[warning]** `req.url` 不是原生的 Express 属性，它继承自 Node 的 [http 模块](https://nodejs.org/api/http.html#http_message_url).

这个属性很像 `req.url`；但是，它保留了原始的请求 URL，允许您自由地重写 `req.url` 用于内部路由目的。例如，[app.use()](#app_use)的 “mounting” 特性将会重写 `req.url` 来去掉挂载点的。

```
// GET /search?q=something
req.originalUrl
// => "/search?q=something"
```


### req.params {#req_params}

一个对象，包含了被映射到命名路由“参数”的属性。例如，如果您有路由 `/user/:name`，那么 “name” 属性就可以作为  `req.params.name` 提供。这个对象默认为 `{}`。

```
// GET /user/tj
req.params.name
// => "tj"
```

当您在路由定义中使用正则表达式时，将使用 `req.params[n]` 在数组中提供捕捉组。其中 `n` 是第 n 个捕捉组。此规则适用于未命名的通配符匹配字符串路由，如  `/file/*`：

```
// GET /file/javascripts/jquery.js
req.params[0]
// => "javascripts/jquery.js"
```


### req.path {#req_path}

包含请求 URL 的路径部分。

```
// example.com/users?sort=desc
req.path
// => "/users"
```

> 当从中间件调用时，挂载点被包含在 `req.path` 中。查找 [app.use()](#app_use) 获得更多细节。。


### req.protocol {#req_protocol}

请求的协议字符串，"http" 或 当请求使用 TLS 时为 “https。当 “trust proxy” [设置](#trust_proxy-options-table) 信任 socket 地址时，“X-Forwarded-Proto” 头（“http” 或 “https”）字段的值将会被信任并被使用，如果存在的话。

```
req.protocol
// => "http"
```

### req.query {#req_query}

一个对象，包含路由中的每个查询字符串参数。如果没有查询字符串，将会是一个空对象，`{}`。

```
// GET /search?q=tobi+ferret
req.query.q
// => "tobi ferret"

// GET /shoes?order=desc&shoe[color]=blue&shoe[type]=converse
req.query.order
// => "desc"

req.query.shoe.color
// => "blue"

req.query.shoe.type
// => "converse"
```


### req.route {#req_route}

一个字符串，表示当前匹配的路由。例如：

```js
app.get('/user/:id?', function userIdHandler(req, res) {
  console.log(req.route);
  res.send('GET');
})
```

上面代码片段的示例输出：

```js
{ path: '/user/:id?',
  stack:
   [ { handle: [Function: userIdHandler],
       name: 'userIdHandler',
       params: undefined,
       path: undefined,
       keys: [],
       regexp: /^\/?$/i,
       method: 'get' } ],
  methods: { get: true } }
```


### req.secure {#req_secure}

一个布尔值，如果一个 TLS 连接建立起来，它将为 `true`。等价于：

```js
'https' == req.protocol;
```


### req.signedCookies {#req_signedCookies}

当使用 [cookie-parser](https://www.npmjs.com/package/cookie-parser) 中间件时,这个属性包含请求发送的签名 cookie，unsigned and ready for use。签名 cookie 驻留在不同的对象中，以显示开发人员的意图；否则，可能会在 `req.cookie` (很容易被欺骗)值上放置恶意攻击。请注意，签名一个 cookie 并不能使其“隐藏”或加密；只是简单地防止篡改(因为用于签名的秘密是私有的)。如果没有发送签名的 cookie，则该属性将是默认值 {}。

```
// Cookie: user=tobi.CP7AWaXDfAKIRfH49dQzKJx7sKzzSoPq7/AcBBRVwlI3
req.signedCookies.user
// => "tobi"
```

要了解更多信息、问题或关注，请参阅 [cookie-parser](https://www.npmjs.com/package/cookie-parser).


### req.stale {#req_stale}

表示该请求是否 “stale”(过时)，并 `req.fresh` 相反。有关更多信息,请参见 [req.fresh](#req_fresh).

```
req.stale
// => true
```


### req.subdomains {#req_subdomains}

请求的域名的一组子域名。

```
// Host: "tobi.ferrets.example.com"
req.subdomains
// => ["ferrets", "tobi"]
```


### req.xhr {#req_xhr}

如果请求的 “X-Requested-With” 头字段是 “XMLHttpRequest”，那么这个布尔值是 `true`，表示请求是由诸如 jQuery 这样的客户端库发出的。

```
req.xhr
// => true
```


## 方法


### req.accepts(types) {#req_accepts}

根据请求的 `Accept` HTTP 头字段检查指定的内容类型是否可接受。该方法返回最佳匹配，如果没有指定的内容类型可以接受，则返回 `undefined`(在这种情况下，应用程序应该响应 406 "Not Acceptable")。

`type` 值可能是一个 MIME 类型字符串(例如 “application/json”)，一个扩展名，例如“json”，一个逗号分隔的列表，或者一个数组。对于一个列表或数组，该方法返回最佳匹配(如果有的话)。

```js
// Accept: text/html
req.accepts('html');
// => "html"

// Accept: text/*, application/json
req.accepts('html');
// => "html"
req.accepts('text/html');
// => "text/html"
req.accepts(['json', 'text']);
// => "json"
req.accepts('application/json');
// => "application/json"

// Accept: text/*, application/json
req.accepts('image/png');
req.accepts('png');
// => undefined

// Accept: text/*;q=.5, application/json
req.accepts(['html', 'json']);
// => "json"
```

更多信息，如果你有问题或担忧，参见 [accepts](https://github.com/expressjs/accepts)。


### req.acceptsCharsets(charset [, ...]) {#req_acceptsCharsets}


根据请求的 `Accept-Charset`  HTTP 头字段，返回指定字符集的第一个被接受的字符集。如果没有一个指定的字符集被接受，则返回 `false`。

更多信息，如果你有问题或担忧，参见 [accepts](https://github.com/expressjs/accepts)。


### req.acceptsEncodings(encoding [, ...]) {#req_acceptsEncodings}


根据请求的 `Accept-Encoding` HTTP 头字段，返回第一个指定编码的被接受的编码。如果不接受指定的编码，则返回 `false`。

更多信息，如果你有问题或担忧，参见 [accepts](https://github.com/expressjs/accepts)。



### req.acceptsLanguages(lang [, ...]) {#req_acceptsLanguages}


根据请求的 `Accept-Language` HTTP 头字段，返回指定语言的第一个被接受的语言。如果没有指定的语言被接受，则返回 `false`。

更多信息，如果你有问题或担忧，参见 [accepts](https://github.com/expressjs/accepts)。


### req.get(field) {#req_get}

返回指定的 HTTP 请求头字段(不区分大小写匹配)。`Referrer` 和 `Referer` 字段是可互换的。

```js
req.get('Content-Type');
// => "text/plain"

req.get('content-type');
// => "text/plain"

req.get('Something');
// => undefined
```

别名为 `req.header(field)`。


### req.is(type) {#req_is}

如果传入请求的 “Content-Type” HTTP 头字段与类型参数指定的MIME `type` 匹配，那么返回 `true`。否则返回 `false`。

```js
// With Content-Type: text/html; charset=utf-8
req.is('html');
req.is('text/html');
req.is('text/*');
// => true

// When Content-Type is application/json
req.is('json');
req.is('application/json');
req.is('application/*');
// => true

req.is('html');
// => false
```

更多信息，如果你有问题或担忧，[type-is](https://github.com/expressjs/type-is).



### req.param(name [, defaultValue]) {#req_param}

> **[danger] 已弃用**。 请使用 `req.params`, `req.body` 或 `req.query`。


当存在时，返回参数 `name` 的值。

```js

// ?name=tobi
req.param('name')
// => "tobi"

// POST name=tobi
req.param('name')
// => "tobi"

// /user/tobi for /user/:name
req.param('name')
// => "tobi"
```

Lookup is performed in the following order:

  * req.params
  * req.body
  * req.query


Optionally, you can specify `defaultValue` to set a default value if the parameter is not found in any of the request objects.

> **[danger]**
>
> 直接访问 `req.body`, `req.params`, 和 `req.query` 应该得到明确的支持 - 除非你 > 真正接受来自每个对象的输入。
>
> 可以预见的是，必须要为 `req.param()` 加载 Body-parsing 中间件来工作。 参考 [req.body](#req_body) 获得更多细节。


# Response  {#response}

`res` 对象表示一个 Express 应用程序收到 HTTP 请求时发送的 HTTP 响应。

在这个文档和约定中，响应对象总是被称为 `res` (HTTP 请求是 `req`)，但是它的实际名称是由您工作的回调函数的参数决定的。

例如:

```js
app.get('/user/:id', function(req, res){
  res.send('user ' + req.params.id);
});
```

但你也可以这样做:

```js
app.get('/user/:id', function(request, response){
  response.send('user ' + request.params.id);
});
```

## 属性


### res.app {#req_app}

该属性对使用中间件的 express 应用程序的实例进行了引用。

`res.app` 等同于请求对象中的 [req.app](#req_app) 属性。


### res.headersSent {#res_headersSent}

布尔值属性，表示应用程序是否为响应发送了 HTTP 头。

```js
app.get('/', function (req, res) {
  console.log(res.headersSent); // false
  res.send('OK');
  console.log(res.headersSent); // true
})
```


### res.locals {#res_locals}

一个包含响应局部变量的对象，它作用于请求的范围，因此只有在请求/响应周期(如果有)时渲染的视图(s)才可用。否则，该属性与 [app.locals](#app_locals) 完全相同。

此属性对于暴露请求级别信息，如请求路径名、经过身份验证的用户、用户设置等，非常有用。


```js
app.use(function(req, res, next){
  res.locals.user = req.user;
  res.locals.authenticated = ! req.user.anonymous;
  next();
});
```


## 方法


### res.append(field [, value]) {#res_append}

> **[success]** `res.append()` 被 Express v4.11.0+ 支持。

将指定的 `value` 附加到 HTTP 响应头 `field`。如果头还没有设置，它将创建带有指定 `value` 的头。`value` 参数可以是字符串或数组。

注意: 在 `res.append()` 之后调用 `res.set()` 将重置先前设置的头的值。

```js
res.append('Link', ['<http://localhost/>', '<http://localhost:3000/>']);
res.append('Set-Cookie', 'foo=bar; Path=/; HttpOnly');
res.append('Warning', '199 Miscellaneous warning');
```


### res.attachment([filename]) {#res_attachment}

将 HTTP 响应 `Content-Disposition` 头字段设置为 “attachment”。如果给定一个 `filename`，那么它将通过 `res.type()` 来基于扩展名设置 Content-Type。并设置 `Content-Disposition` “filename=” 参数。

```js
res.attachment();
// Content-Disposition: attachment

res.attachment('path/to/logo.png');
// Content-Disposition: attachment; filename="logo.png"
// Content-Type: image/png
```


### res.cookie(name, value [, options]) {#res_cookie}


设置 cookie `name` 为 `value`。 `value` 参数可以是一个字符串或者转换为 JSON 的对象。

`options` 参数是一个对象，它可以包含下面的属性。

属性	| 类型	| 描述
----------|-------|--------------
`domain`	| String	| cookie 的域名。默认为 app 的域名。
`expires`	| Date	| GMT 的过期时间。如果没有指定或设置为 0，则创建一个会话 cookie。
`httpOnly`	| Boolean	| 将 cookie 标记为只能通过 web 服务器访问。
`maxAge`	| String	| 在以毫秒为单位的时间内设置过期时间的方便选项。
`path`	| String	| cookie 的路径。默认为 “/”。
`secure`	| Boolean	| 标记 cookie 为只用 HTTPS 使用 。
`signed`	| Boolean	| 表示 cookie 是否应该被签名。

> **[warning]** 所有的 `res.cookie()` 都会使用提供的选项设置 HTTP `Set-Cookie` 头。 任何未指定的选项都默认为 RFC 6265 中所述的值。

示例:

```js
res.cookie('name', 'tobi', { domain: '.example.com', path: '/admin', secure: true });
res.cookie('rememberme', '1', { expires: new Date(Date.now() + 900000), httpOnly: true });
```

`maxAge` 选项是相对于当前时间以毫秒为单位设置 “expires” 的一个方便选项。下面是上面的第二个例子。

```js
res.cookie('rememberme', '1', { maxAge: 900000, httpOnly: true })
```

您可以传递一个对象作为 `value` 参数；然后将它序列化为 JSON，并由 `bodyParser()` 中间件解析。

```js
res.cookie('cart', { items: [1,2,3] });
res.cookie('cart', { items: [1,2,3] }, { maxAge: 900000 });
```

当使用 [cookie-parser](https://www.npmjs.com/package/cookie-parser) 中间件时，这个方法还支持签名 cookies。简单地将 `signed` 选项设置为 `true`。然后 `res.cookie()` 将使用被传递给 `cookieParser(secret)` 的秘密签署这个值。

```js
res.cookie('name', 'tobi', { signed: true });
```

稍后您可以通过 `req.signedCookie`对象 访问该值。


### res.clearCookie(name [, options]) {#res_clearCookie}


清空依靠 `name` 指定的 cookie。要获取关于 `options` 对象的细节，请参见 [res.cookie()](l#res_cookie).

```js
res.cookie('name', 'tobi', { path: '/admin' });
res.clearCookie('name', { path: '/admin' });
```


### res.download(path [, filename] [, fn]) {#res_download}

将文件传输到 `path` 作为 “attachment”。通常，浏览器会提示用户下载。默认情况下， `Content-Disposition` 头 “filename=” 参数是 `path`(这通常出现在浏览器对话框中)。用 `filename` 参数覆盖这个默认值。

当一个错误发生或传输完成时，该方法调用可选的回调函数 `fn`。这个方法使用 [res.sendFile()](#res_sendFile) 来传输文件。

```js
res.download('/report-12345.pdf');

res.download('/report-12345.pdf', 'report.pdf');

res.download('/report-12345.pdf', 'report.pdf', function(err){
  if (err) {
    // 处理错误，但请记住，响应可以被部分发送，因此请检查  res.headersSent
  } else {
    // decrement a download credit, etc.
  }
});
```

### res.end([data] [, encoding]) {#res_end}


结束响应过程。这种方法实际上来自 Node 核心,特别是[http.ServerResponse 的 response.end()方法](https://nodejs.org/api/http.html#http_response_end_data_encoding_callback)。

用来快速结束响应，而不需要任何数据。如果需要对数据进行响应，则使用诸如 [res.send()](#res_send)和 [res.json()](#res_json) 这样的方法替代。


```js
res.end();
res.status(404).end();
```


### res.format(object) {#res_format}

在请求对象的 `Accept` HTTP 头上执行 content-negotiation，当存在时。它使用 `req.accepts()` 来为请求选择一个处理函数，根据其 quality 值排序的可接受的类型。如果没有指定头，那么将调用第一个回调。当没有找到匹配时，服务器响应为 406 “Not Acceptable”，或者调用 `default` 回调。

`Content-Type` 响应头是在选择回调时设置的。但是，您可以使用诸如 `res.set()` 或 `res.type()` 之类的方法在回调中修改它。

下面的示例，当 `Accept` 头字段被设置为 “application/json” 或 “*/json” 时，将使用 `{ "message": "hey" }` 进行响应，(然而如果它是 “*/*”，响应将是 “hey”）。

```js
res.format({
  'text/plain': function(){
    res.send('hey');
  },

  'text/html': function(){
    res.send('<p>hey</p>');
  },

  'application/json': function(){
    res.send({ message: 'hey' });
  },

  'default': function() {
    // log the request and respond with 406
    res.status(406).send('Not Acceptable');
  }
});
```

除了规范化的 MIME 类型之外，您还可以使用映射到这些类型的扩展名来实现稍微不那么详细的实现:

```js
res.format({
  text: function(){
    res.send('hey');
  },

  html: function(){
    res.send('<p>hey</p>');
  },

  json: function(){
    res.send({ message: 'hey' });
  }
});
```

### res.get(field) {#res_get}

返回靠 `field` 指定的 HTTP 响应头。匹配不区分大小写。

```js
res.get('Content-Type');
// => "text/plain"
```


### res.json([body]) {#res_json}

发送一个 JSON 响应。这个方法与使用对象或数组作为参数的 `res.send()` 相同。但是，您可以使用它将其他值转换为 JSON，例如 `null` 和 `undefined`。(尽管从技术上来说，这些都不是有效的JSON)。

```js
res.json(null)
res.json({ user: 'tobi' })
res.status(500).json({ error: 'message' })
```


### res.jsonp([body]) {#res_jsonp}


使用 JSONP 支持发送一个 JSON 响应。这个方法与 `res.json()` 相同，除了它支持 JSONP 回调。

```js
res.jsonp(null)
// => null

res.jsonp({ user: 'tobi' })
// => { "user": "tobi" }

res.status(500).jsonp({ error: 'message' })
// => { "error": "message" }
```

默认情况下，JSONP 回调名是简单的 `callback`。使用 [jsonp callback](#app_settings-table) 名设置来覆盖。

下面是使用相同代码的 JSONP 响应的一些示例:

```js
// ?callback=foo
res.jsonp({ user: 'tobi' })
// => foo({ "user": "tobi" })

app.set('jsonp callback name', 'cb');

// ?cb=foo
res.status(500).jsonp({ error: 'message' })
// => foo({ "error": "message" })
```


### res.links(links) {#res_links}

连接提供的 `links` 作为参数的属性，以填充响应的 `Link` HTTP 头字段。

```js
res.links({
  next: 'http://api.example.com/users?page=2',
  last: 'http://api.example.com/users?page=5'
});
```

yields:

```
Link: <http://api.example.com/users?page=2>; rel="next",
      <http://api.example.com/users?page=5>; rel="last"
```


### res.location(path) {#res_location}

将响应的 `Location` HTTP 头设置为指定的 `path` 参数。

```js
res.location('/foo/bar');
res.location('http://example.com');
res.location('back');
```

“back” 的 `path` 值有一个特殊的含义，它指的是在请求的 `Referer` 头部中指定的 URL。如果没有指定 `Referer` 头，它是指 “/”。

> **[danger]**
>
> Express 将指定的 URL 字符串按原样传递给 `Location` 头中的浏览器，而不进行任何验证或操作，除了 `back` 的情况。
>
> 浏览器负责从当前 URL 或引用 URL 中派生出预期的 URL，以及在 `Location` 头中指定的 URL；然后相应地重定向用户。


### res.redirect([status,] path) {#res_redirect}

使用指定的 [HTTP 状态码](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) `status`，重定向到派生自指定的 `path` 的 URL。 如果您不指定 `status`，则状态代码默认为 “302 “Found”。

```js
res.redirect('/foo/bar');
res.redirect('http://example.com');
res.redirect(301, 'http://example.com');
res.redirect('../login');
```

重定向可以是重定向到其他网站的完全限定的 URL：

```js
res.redirect('http://google.com');
```

重定向可以是相对于主机名的根。例如，如果应用程序位于 `http://example.com/admin/post/new`，则以下将重定向到 URL `http://example.com/admin`：

```js
res.redirect('/admin');
```

重定向可以相对于当前 URL 。例如,从 `http://example.com/blog/admin/`(注意尾部的斜杠),以下将重定向到该 URL `http://example.com/blog/admin/post/new`。

```js
res.redirect('post/new');
```

从 `http://example.com/blog/admin` 重定向到 `post/new`（没有使用斜杠），将重定向到 `http://example.com/blog/post/new`。

如果您发现上面的行为令人困惑，请将路径段看作目录(带有斜杠)和文件，它将开始有意义。

相对路径重定向也是可以的。如果你在 `http://example.com/admin/post/new` 上，下面将重定向到 `http://example.com/admin/post`:

```js
res.redirect('..');
```

`back` 重定向将重定向请求回退到 [referer](http://en.wikipedia.org/wiki/HTTP_referer)， 当 referer 缺失时，默认为 `/`。

```js
res.redirect('back');
```


### res.render(view [, locals] [, callback]) {#res_render}

渲染一个 `view` 并发送选然后的 HTML 字符串到客户端。可选的参数有：

  * `locals`， 一个对象，它的属性为视图定义局部变量。
  * `callback`，一个回调函数。如果提供了，该方法将返回可能的错误和渲染的字符串，但不会执行自动响应。当出现错误时，该方法将在内部调用 next(err)。

>**[warning]** 本地变量 `cache` 将启用视图缓存。设置为 `true`，以在开发中缓存视图；在生产中，视图缓存是默认开启的。

```js
// 发送渲染好的视图给客户端
res.render('index');

// 如果指定了回调函数，渲染的 HTML 字符串被显示地发送
res.render('index', function(err, html) {
  res.send(html);
});

// 将一个局部变量传递给视图
res.render('user', { name: 'Tobi' }, function(err, html) {
  // ...
});
```


### res.send([body]) {#res_send}

发送 HTTP 响应。

`body` 参数可以是一个 `Buffer` 对象，`String`，Object，或者一个 `Array`。例如：

```js
res.send(new Buffer('whoop'));
res.send({ some: 'json' });
res.send('<p>some html</p>');
res.status(404).send('Sorry, we cannot find that!');
res.status(500).send({ error: 'something blew up' });
```

此方法为简单的非流响应执行许多有用的任务: 例如，它自动分配 `Content-Length` HTTP 响应头字段(除非预先定义)，并提供自动的 HEAD 和 HTTP 缓存的新鲜（freshness）支持。

当参数是一个 `Buffer` 对象时，该方法将 `Content-Type` 的响应头字段设置为 “application/octet-stream”，除非前面已经定义如下:

```js
res.set('Content-Type', 'text/html');
res.send(new Buffer('<p>some html</p>'));
```

当参数是一个 `String`，该方法将设置 `Content-Type` 为 “text/html”:

```js
res.send('<p>some html</p>');
```

When the parameter is an `Array` or `Object`, Express responds with the JSON representation:

```js
res.send({ user: 'tobi' });
res.send([1,2,3]);
```

### res.sendFile(path [, options] [, fn])

> **[success]** `res.sendFile()` 从 Express v4.8.0 开始被支持。

在给定的 `path` 上传输文件。根据文件名的扩展设置 `Content-Type` 响应 HTTP 头字段。除非在options对象中设置 `root` 选项，否则  `path` 必须是文件的绝对路径。

`options` 对象的详细信息列在下面的表中。

属性	| 描述	| 默认值	| 可用性
----------|-------------|---------|--------------
`maxAge`	| 以[毫秒](https://www.npmjs.org/package/ms)或字符串格式设置 `Cache-Control` 头的 max-age 属性| 0 | -
`root`	| 相对文件名的根目录 | - |-
`lastModified`	| 将 `Last-Modified` 头设置为 OS 上文件的最后修改日期。 设置 `false` 来禁用它。| `true`，启用	| 4.9.0+
`headers`	| Object | 包含 HTTP 头文件以服务于文件。containing HTTP headers to serve with the file.| -
`dotfiles`	| 用于serving dotfiles 的选项。可能的值有 “allow”, “deny”, “ignore”.	| “ignore”| -

当传输完成或发生错误时，该方法调用回调函数 `fn(err)`。如果指定回调函数并发生错误，回调函数必须通过结束请求-响应循环，或者通过将控制权传递给下一个路由，来显式地处理响应过程。

这里有一个使用带所有参数的 `res.sendFile` 例子：

```js
app.get('/file/:name', function (req, res, next) {

  var options = {
    root: __dirname + '/public/',
    dotfiles: 'deny',
    headers: {
        'x-timestamp': Date.now(),
        'x-sent': true
    }
  };

  var fileName = req.params.name;
  res.sendFile(fileName, options, function (err) {
    if (err) {
      console.log(err);
      res.status(err.status).end();
    }
    else {
      console.log('Sent:', fileName);
    }
  });

})
```

`res.sendFile` 提供了对文件服务的细粒度支持，如下面的示例所示

```js
app.get('/user/:uid/photos/:file', function(req, res){
  var uid = req.params.uid
    , file = req.params.file;

  req.user.mayViewFilesFrom(uid, function(yes){
    if (yes) {
      res.sendFile('/uploads/' + uid + '/' + file);
    } else {
      res.status(403).send('Sorry! you cant see that.');
    }
  });
});
```

更多的信息，如果你有问题或担心，请参阅 send。


### res.sendStatus(statusCode) {#res_sendStatus}

设置响应 HTTP 状态码为 `statusCode` 并发送它的字符串表示作为响应主体。

```js
res.sendStatus(200); // 等价于 res.status(200).send('OK')
res.sendStatus(403); // 等价于 res.status(403).send('Forbidden')
res.sendStatus(404); // 等价于 res.status(404).send('Not Found')
res.sendStatus(500); // 等价于 res.status(500).send('Internal Server Error')
```

如果指定了不受支持的状态代码，那么 HTTP 状态仍然会被设置为 `statusCode`，而代码的字符串版本会作为响应体发送。

```js
res.sendStatus(2000); // 等价于 res.status(2000).send('2000')
```

[更多关于 HTTP 状态码](http://en.wikipedia.org/wiki/List_of_HTTP_status_codes)


### res.set(field [, value]) {#res_set}

设置想用的 HTTP 头 `field` 为 `value。为了一次设置多个字段，可以传递一个对象作为参数。

```js
res.set('Content-Type', 'text/plain');

res.set({
  'Content-Type': 'text/plain',
  'Content-Length': '123',
  'ETag': '12345'
})
```

等价于 `res.header(field [, value])`.


### res.status(code) {#res_status}

使用这个方法来为响应设置 HTTP 状态。它是 Node 的 [response.statusCode](http://nodejs.org/api/http.html#http_response_statuscode) 的一个可链接的别名。

```js
res.status(403).end();
res.status(400).send('Bad Request');
res.status(404).sendFile('/absolute/path/to/404.png');
```


### res.type(type) {#res_type}

根据 [ mime.lookup()](https://github.com/broofa/node-mime#mimelookuppath) 为指定的 `type` 确定 MIME 类型，该 MIME 类型被用来设置 `Content-Type` HTTP 头。如果 `type` 包含 “/” 字符，那么它将设置 `Content-Type` 为 `type`。
    
```js
res.type('.html');              // => 'text/html'
res.type('html');               // => 'text/html'
res.type('json');               // => 'application/json'
res.type('application/json');   // => 'application/json'
res.type('png');                // => image/png:
```


### res.vary(field) {#res_vary}

添加这个 `field` 到 `Vary` 响应头,如果它不在那里。

```js
res.vary('User-Agent').render('docs');
```

# Router {#router}

`router` 对象是中间件和路由的一个单独的实例。您可以把它看作是一个“迷你应用程序”，它只能够执行中间件和路由函数。每一个 Express 应用都有一个内置的应用程序路由器。

路由器的行为类似于中间件本身，因此您可以将其作为 [app.use()](#app_use) 的参数使用或作为另一个路由器的 [use()](#router_use) 方法的参数。

顶级 `express` 对象有一个 `Router()` 函数，它可以创建一个新的 `router` 对象。

## Router([options])

创建一个新的路由器，如下所示：

```js
var router = express.Router([options]);
```

可选的 `options` 参数指定了路由器的行为：

属性  | 描述  |  默认值 |  有效性
-----------|------------|-----------|-----------
`caseSensitive`  |  启用区分大小写  |  默认是禁用的，同等对待 “/Foo” 和 “/foo”。 |
`mergeParams`  |  保留来自父路由器的 `req.params` 值。如果父路由器和子路由器的 params 名字有冲突，子路由的就会优先考虑。 |  `false` | 4.5.0+
`strict`  | 使用严格路由  | 默认是禁用的，路由器同等对待 “/foo” 和 “/foo/”。 | -

您可以将中间件和 HTTP 方法路由(例如 `get`、`put`、`post`等等)添加到 `router`，就像应用程序一样。

```js
// 为任何请求被传递到这个路由器调用
router.use(function(req, res, next) {
  // .. some logic here .. like any other middleware
  next();
});

// 将处理任何以 /events 结束的请求
// 取决于路由器在哪里被 “use()”
router.get('/events', function(req, res, next) {
  // ..
});

```

然后，你可以为特定的根 URL 使用路由器，这样就可以将你的路由分成文件，甚至是迷你应用程序。

```js
// 只有 /calendar/* 的请求将发送这个“router”
app.use('/calendar', router);
```

## 方法

### router.all(path, [callback, ...] callback) {#router_all}

这个方法函数就像 `router.METHOD()` 方法，除了它匹配所有的 HTTP 动词。

这个方法对于映射特定路径前缀或任意匹配的“全局”逻辑非常有用。例如，如果您将以下路由放置在所有其他路由定义的顶部，那么它将要求从该点开始的所有路由都需要身份验证，并自动加载用户。请记住，这些回调不需要作为端点; `loadUser` 可以执行一个任务，然后调用 `next()` 继续匹配后续路线。

```js
router.all('*', requireAuthentication, loadUser);
```

或相当于:

```js
router.all('*', requireAuthentication)
router.all('*', loadUser);
```

另一个例子是白色列出的“全局”功能。这里的例子与之前的很相似，但它只限制了前缀为“/api”的路径:

```js
router.all('/api/*', requireAuthentication);
```

### router.METHOD(path, [callback, ...] callback) {#router_METHOD}

在 Express 种，`router.METHOD()` 方法提供路由功能，其中 METHOD 是 HTTP 方法之一，如 GET、PUT、POST等，以小写形式。因此，实际的方法是`router.get()`、`router.post()`、`router.put()` 等等。

您可以提供多个回调，并且所有的回调都是一样的，并且行为就像中间件一样，只不过这些回调可以调用 `next('route')` 绕过余下的路由回调(s)。您可以使用此机制在路由上执行前置条件，然后在没有理由继续匹配路由时将控制权传递给后续路由。

下面的代码片段说明了可能的最简单的路由定义。Express 将路径字符串转换为正则表达式，用于内部匹配传入的请求。在执行这些匹配时，不考虑查询字符串，例如 “GET/” 会匹配以下路线，“GET/?name=tobi”。

```js
router.get('/', function(req, res){
  res.send('hello world');
});
```

如果你有非常具体的约束，您还可以使用常规有用的表达，例如下面的将匹配 “GET /commits/71dbb9c” 以及 “GET /commits/71dbb9c..4c084f9”。

```js
router.get(/^\/commits\/(\w+)(?:\.\.(\w+))?$/, function(req, res){
  var from = req.params[0];
  var to = req.params[1] || 'HEAD';
  res.send('commit range ' + from + '..' + to);
});
```


### router.param([name,] callback) {#router_param}

为路由参数添加回调触发器，其中 `name` 是参数的名称或它们的数组，而 `callback` 是回调函数。回调函数的参数是请求对象、响应对象、下一个中间件，以及参数的值都是这个顺序。『译者注：』`callback(req, res, next)`。

如果名称是一个数组，那么这个回调触发器将在声明的每个参数中注册，以声明它们的顺序。此外，对于每个声明的参数，除了最后一个参数之外，回调中的 `next` 调用将调用下一个声明参数的回调。对于最后一个参数，对 `next` 的调用将调用当前正在处理的路由的下一个中间件，就像如果名称只是一个字符串一样。

> **[info] 路由参数（route parameters）是什么？**
>
> app.get('/user/:id') 中，匹配到的 `id` 就是路由参数。一个路径中有多个路由参数，如 app.get('/user/:id/:user')。这个函数就是为这些在 `name` 或者 `[name]` 数组中匹配到的路由参数添加回调触发器，一旦匹配到路由参数，则为这些匹配到的每个路由参数调用。

例如，当用户出现在路由路径时，您可能会映射用户加载逻辑，以自动提供 `req.user` 到路由，或者在参数输入上执行验证。

```js
router.param('user', function(req, res, next, id) {

  // 尝试从 User 模块获取 user 细节，并将其附加到请求对象
  User.find(id, function(err, user) {
    if (err) {
      next(err);
    } else if (user) {
      req.user = user;
      next();
    } else {
      next(new Error('failed to load user'));
    }
  });
});
```

参数回调函数在定义它们的路由器上是本地的。它们不是由安装的应用程序或路由器继承的。因此，在路由器上定义的参数回调只能由路由器路由上定义的路由参数触发。

在请求-响应循环中，参数回调只会被调用一次，即使参数在多个路径中匹配，如下面的例子所示。


```js
router.param('id', function (req, res, next, id) {
  console.log('CALLED ONLY ONCE');
  next();
})

app.get('/user/:id', function (req, res, next) {
  console.log('although this matches');
  next();
});

app.get('/user/:id', function (req, res) {
  console.log('and this matches too');
  res.end();
});
```

当 `GET /user/42`，上面的代码输出如下：

```
CALLED ONLY ONCE
although this matches
and this matches too
```

```js
router.param(['id', 'page'], function (req, res, next, value) {
  console.log('CALLED ONLY ONCE with', value);
  next();
})

app.get('/user/:id/:page', function (req, res, next) {
  console.log('although this matches');
  next();
});

app.get('/user/:id/:page', function (req, res) {
  console.log('and this matches too');
  res.end();
});
```

在 `GET /user/42/3`，上面的代码输出如下：

```
CALLED ONLY ONCE with 42
CALLED ONLY ONCE with 3
although this matches
and this matches too
```

> **[danger]** The following section describes `router.param(callback)`, which is deprecated as of v4.11.0.

The behavior of the `router.param(name, callback)` method can be altered entirely by passing only a function to `router.param()`. This function is a custom implementation of how `router.param(name, callback)` should behave - it accepts two parameters and must return a middleware.

The first parameter of this function is the name of the URL parameter that should be captured, the second parameter can be any JavaScript object which might be used for returning the middleware implementation.

The middleware returned by the function decides the behavior of what happens when a URL parameter is captured.

In this example, the `router.param(name, callback)` signature is modified to `router.param(name, accessId)`. Instead of accepting a name and a callback, `router.param()` will now accept a name and a number.

```js
var express = require('express');
var app = express();
var router = express.Router();

// customizing the behavior of router.param()
router.param(function(param, option) {
  return function (req, res, next, val) {
    if (val == option) {
      next();
    }
    else {
      res.sendStatus(403);
    }
  }
});

// using the customized router.param()
router.param('id', 1337);

// route to trigger the capture
router.get('/user/:id', function (req, res) {
  res.send('OK');
})

app.use(router);

app.listen(3000, function () {
  console.log('Ready');
})
```

In this example, the `router.param(name, callback)` signature remains the same, but instead of a middleware callback, a custom data type checking function has been defined to validate the data type of the user id.

```js
router.param(function(param, validator) {
  return function (req, res, next, val) {
    if (validator(val)) {
      next();
    }
    else {
      res.sendStatus(403);
    }
  }
})

router.param('id', function (candidate) {
  return !isNaN(parseFloat(candidate)) && isFinite(candidate);
});
```


### router.route(path) {#router_route}

返回一个单一路由的实例，然后您可以使用它来处理带有可选中间件的 HTTP 动词。使用 `router.route()` 来避免重复的路由名称(以及拼写错误)。

在上面的 `router.param()` 示例中绑定，下面的代码显示如何使用 `router.route()` 来指定各种各样的 HTTP 方法处理函数。

```js
var router = express.Router();

router.param('user_id', function(req, res, next, id) {
  // 样本用户，实际从 DB 取回，等等。
  req.user = {
    id: id,
    name: 'TJ'
  };
  next();
});

router.route('/users/:user_id')
.all(function(req, res, next) {
  // 首先运行 all HTT P动词
  // 可以将其视为路由特定的中间件！
  next();
})
.get(function(req, res, next) {
  res.json(req.user);
})
.put(function(req, res, next) {
  // 这是一个可能更新用户的例子
  req.user.name = req.params.name;
  // 保存 user ... etc
  res.json(req.user);
})
.post(function(req, res, next) {
  next(new Error('not implemented'));
})
.delete(function(req, res, next) {
  next(new Error('not implemented'));
})
```

这种方法重用单一的 ‘/users/:user_id’ 路径，并为各种 HTTP 方法添加处理程序。


### router.use([path], [function, ...] function) {#router_use}

使用指定的中间件 `function`，带有可选的挂载路径 `path`，默认为 “/”。

这个方法类似于 [app.use()](#app_use)。下面将介绍一个简单的示例和用例。参见 [app.use()](#app_use) 获取更多信息。

中间件就像一个水管管道，请求从您定义的第一个中间件开始，按照它们匹配的每条路径“向下”中间件堆栈处理。

```js
var express = require('express');
var app = express();
var router = express.Router();

// 简单的记录这个路由器的请求
// 所有的请求到这个路由器将首先触发这个中间件
router.use(function(req, res, next) {
  console.log('%s %s %s', req.method, req.url, req.path);
  next();
});

// 这只会在路径从挂载点的以 '/bar' 开始时被调用
router.use('/bar', function(req, res, next) {
  // ... maybe some additional /bar logging ...
  next();
});

// 始终调用
router.use(function(req, res, next) {
  res.send('Hello World');
});

app.use('/foo', router);

app.listen(3000);
```

The “mount” path is stripped and is not visible to the middleware `function`. The main effect of this feature is that mounted middleware may operate without code changes regardless of its “prefix” pathname.
“挂载” 路径被剥离，对中间件 `function` 是不可见。这个特性的主要作用是挂载的中间件不管代码的“前缀”路径名都可以在不改变代码的情况下运行。

用 `router.use()` 定义中间件的顺序非常重要。它们是按顺序调用的，因此顺序定义了中间件的优先级。例如，通常记录器是您要使用的第一个中间件，因此每个请求都被记录下来。

```js
var logger = require('morgan');

router.use(logger());
router.use(express.static(__dirname + '/public'));
router.use(function(req, res){
  res.send('Hello');
});
```

现在假设你想忽略对静态文件的记录请求，但是要继续记录在 logger() 之后定义的路由和中间件。 你只需要移动上面的static()：

```js
router.use(express.static(__dirname + '/public'));
router.use(logger());
router.use(function(req, res){
  res.send('Hello');
});
```

另一个具体例子是从多个目录提供文件，优先“./public”而不是其他目录：

```js
app.use(express.static(__dirname + '/public'));
app.use(express.static(__dirname + '/files'));
app.use(express.static(__dirname + '/uploads'));
```

`router.use()` 方法还支持命名参数，以便其他路由器的挂载点可以从使用命名参数的预加载中获益。
