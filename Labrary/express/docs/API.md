# Express 4.x API 中文手册

## express()

## Aplication

## Request

## Response

## Router

A router object is an isolated instance of middleware and routes. You can think of it as a “mini-application,” capable only of performing middleware and routing functions. Every Express application has a built-in app router.

A router behaves like middleware itself, so you can use it as an argument to app.use() or as the argument to another router’s use() method.

The top-level express object has a Router() function that creates a new router object.

路由器对象是中间件和路由的一个孤立实例。您可以把它看作是一个“迷你应用程序”，它只能够执行中间件和路由函数。每一个 Express 应用都有一个内置的应用程序路由器。

路由器的行为类似于中间件本身，因此您可以将其作为 `app.use()` 的参数使用或作为另一个路由器的 `use()` 方法的参数。

顶级 express 对象有一个 `Router()` 函数，它可以创建一个新的路由器对象。

### Router([options])

创建一个新的路由器，如下所示：

```js
var router = express.Router([options]);
```

可选的选项参数指定了路由器的行为：

属性  | 描述  |  默认值 |  有效性
-----------|------------|-----------|-----------
caseSensitive  |  启用区分大小写  |  默认是禁用的，同等对待 “/Foo” 和 “/foo”。 |
mergeParams  |  保留来自父路由器的 `req.params` 值。如果父路由器和子路由器的 params 名字有冲突，子路由的就会优先考虑。 |  `false` | 4.5.0+
strict  | 使用严格路由  | 默认是禁用的，路由器同等对待 “/foo” 和 “/foo/”。 | -

您可以将中间件和 HTTP 方法路由(例如 get、put、post等等)添加到路由器，就像应用程序一样。

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


> **[info] 路由器的方法**
>
> 方法                | 描述
> :-------------------|:----
> [router.router()](#routerparamname-callback) | -
> [router.all()](#routerallpath-callback--callback)    | -
> [router.METHOD()](#routermethodpath-callback--callback) | -
> [router.param()](#routerparamname-callback)  | -
> [router.route()](#routerroutepath)  | -
> [router.use()](#routerusepath-function--function)    | -

### router.all(path, [callback, ...] callback)

### router.METHOD(path, [callback, ...] callback)

### router.param([name,] callback)

为路由参数添加回调触发器，其中名称是参数的名称或它们的数组，而函数是回调函数。回调函数的参数是请求对象、响应对象、下一个中间件，以及参数的值都是这个顺序。『译者注：』`callback(req, res, next)`。

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

Param 回调函数在定义它们的路由器上是本地的。它们不是由安装的应用程序或路由器继承的。因此，在路由器上定义的 param 回调只能由路由器路由上定义的路由参数触发。

在请求-响应循环中，param 回调只会被调用一次，即使参数在多个路径中匹配，如下面的例子所示。


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

当 GET /user/42，上面的代码输出如下：

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

在 GET /user/42/3，上面的代码输出如下：

```
CALLED ONLY ONCE with 42
CALLED ONLY ONCE with 3
although this matches
and this matches too
```

### router.route(path)

### router.use([path], [function, ...] function)
