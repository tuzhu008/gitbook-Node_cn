# connect-flash

Flash 是用于存储消息的会话的特殊区域。 消息被写入闪存并在显示给用户后清除。
Flash 通常与重定向结合使用，确保消息可用于要渲染的下一页。

这个中间件是从 [Express](http://expressjs.com/) 2.x 中提取的，Express 3.x 删除了直接支持的 flash。 `connect-flash` 将此功能带回到 Express 3.x 以及任何其他中间件兼容的框架或应用程序。+1 for [radical reusability](http://substack.net/posts/b96642/the-node-js-aesthetic).

## 安装

```bash
$ npm install connect-flash
```

## 用法

#### Express 3.x

Flash 消息被存储在会话中。首先，通过启用 `cookieParser` 和 `session` 中间件来设置会话。然后，使用由 connect-flash 提供的 `flash` 中间件。

```javascript
var flash = require('connect-flash');
var app = express();

app.configure(function() {
  app.use(express.cookieParser('keyboard cat'));
  app.use(express.session({ cookie: { maxAge: 60000 }}));
  app.use(flash());
});
```

有了 `flash` 中间件，所有请求都会有一个可以用于 flash 消息 `req.flash()` 的函数。

```javascript
app.get('/flash', function(req, res){
  // 设置一个 flash 消息，通过传递键值，和值到 req.flash()。req.flash(key, value)
  req.flash('info', 'Flash is back!')
  res.redirect('/');
});

app.get('/', function(req, res){
  // 通过传递键到 req.flash() 来获取一个 flash 消息数组
  res.render('index', { messages: req.flash('info') });
});
```

#### Express 4.x

Express 4.x 中，除 `express.static` 中间见外，其余中间件已移除，因此需要独立安装和加载。

```js
var session = requrie('express-session');
var cookieParser = require('cookie-parser');
var flash = require('connect-flash');
var app = express();

app.use(cookieParser('keyboard cat'));
app.use(session({ cookie: { maxAge: 60000 }}));
app.use(flash());
```

## 示例

在  Express 3.x 应用中使用 connect-flash 的例子，请参见 [express3](https://github.com/jaredhanson/connect-flash/tree/master/examples/express3)
示例。

## Tests

```bash
$ npm install --dev
$ make test
```

[![Build Status](https://secure.travis-ci.org/jaredhanson/connect-flash.png)](http://travis-ci.org/jaredhanson/connect-flash)

## 关于作者

  - [Jared Hanson](http://github.com/jaredhanson)
  - [TJ Holowaychuk](https://github.com/visionmedia)

## License

[The MIT License](http://opensource.org/licenses/MIT)

Copyright (c) 2012-2013 Jared Hanson <[http://jaredhanson.net/](http://jaredhanson.net/)>
