# connect-mongo

适用于 [Connect](https://github.com/senchalabs/connect) 和 [Express](http://expressjs.com/) 的 MongoDB 会话存储

[![npm version](https://img.shields.io/npm/v/connect-mongo.svg)](https://www.npmjs.com/package/connect-mongo)
[![downloads](https://img.shields.io/npm/dm/connect-mongo.svg)](https://www.npmjs.com/package/connect-mongo)
[![Build Status](https://travis-ci.org/jdesboeufs/connect-mongo.svg?branch=master)](https://travis-ci.org/jdesboeufs/connect-mongo)
[![Coverage Status](https://coveralls.io/repos/jdesboeufs/connect-mongo/badge.svg?branch=master&service=github)](https://coveralls.io/github/jdesboeufs/connect-mongo?branch=master)
[![Dependency Status](https://david-dm.org/jdesboeufs/connect-mongo.svg?style=flat)](https://david-dm.org/jdesboeufs/connect-mongo)
[![Greenkeeper badge](https://badges.greenkeeper.io/jdesboeufs/connect-mongo.svg)](https://greenkeeper.io/)
[![XO code style](https://img.shields.io/badge/code_style-XO-5ed9c7.svg)](https://github.com/sindresorhus/xo)

## 兼容性

* 支持 快到来的 Express `5.0`
* 支持所有 Connect 版本
* 支持 [Mongoose](http://mongoosejs.com/index.html) `>= 4.1.2+`
* 支持 [原生 MongoDB 驱动器](http://mongodb.github.io/node-mongodb-native/) `>= 2.0.36`
* 支持 Node.js 4、6 和 8
* 支持 [MongoDB](https://www.mongodb.com/) `>= 3.0`

对于扩展兼容性，请参阅以前的版本。

## 用法

### 与 Express 或 Connect 集成

Express `4.x`, `5.0` 和 Connect `3.x`:

```js
const session = require('express-session');
const MongoStore = require('connect-mongo')(session);

app.use(session({
    secret: 'foo',
    store: new MongoStore(options)
}));
```

Express `2.x`, `3.x` 和 Connect `1.x`, `2.x`:

```js
const MongoStore = require('connect-mongo')(express);

app.use(express.session({
    secret: 'foo',
    store: new MongoStore(options)
}));
```

对于 Connect `1.x` and `2.x`, 只需要用 `connect` 替换掉 `express`。

### 连接到 MongoDB

在很多情况下，`connect-mongo` 不是应用程序中唯一需要连接到 MongoDB 数据库的部分。重用现有的连接可能会很有趣。

或者，您可以配置 `connect-mongo` 来建立一个新的连接。

#### 重用 Mongoose 连接

```js
const mongoose = require('mongoose');

// Basic usage
mongoose.connect(connectionOptions);

app.use(session({
    store: new MongoStore({ mongooseConnection: mongoose.connection })
}));

// 高级用法
const connection = mongoose.createConnection(connectionOptions);

app.use(session({
    store: new MongoStore({ mongooseConnection: connection })
}));
```

#### 重用原生 MongoDB 驱动器连接 (或一个 promise)

在这种情况下，您只需将您的 `Db` 实例给 `connect-mongo`。

如果连接没有打开，`connect-mongo` 将为您完成。

```js
/*
** There are many ways to create dbInstance.
** You should refer to the driver documentation.
*/

app.use(session({
    store: new MongoStore({ db: dbInstance })
}));
```

Or just give a promise...

```js
app.use(session({
    store: new MongoStore({ dbPromise: dbInstancePromise })
}));
```

#### 从 MongoDB 连接字符串创建一个新连接

[MongoDB 连接字符串](http://docs.mongodb.org/manual/reference/connection-string/) 是配置新连接的 __最好的方式__ 。 对于高级用法, 可以使用 `mongoOptions` 属性配置[更多选项](http://mongodb.github.io/node-mongodb-native/driver-articles/mongoclient.html#mongoclient-connect-options)。

```js
// 基本用法
app.use(session({
    store: new MongoStore({ url: 'mongodb://localhost/test-app' })
}));

// 高级用法
app.use(session({
    store: new MongoStore({
        url: 'mongodb://user12345:foobar@localhost/test-app?authSource=admins&w=1',
        mongoOptions: advancedOptions // See below for details
    })
}));
```

## 事件

`MongoStore` 实例将触发下面的事件：

| 事件名称 | 描述 | 有效载荷
| ----- | ----- | ----- |
| `create` | 会话已经被创建 | `sessionId` |
| `touch` | 会话被触碰（touch） (但未被修改) | `sessionId` |
| `update` | 会话已被更新 | `sessionId` |
| `set` | 会话已经被创建或更新 _(用于兼容的目的)_ | `sessionId` |
| `destroy` | 会话已经被销毁 | `sessionId` |

## 会话到期

当会话 cookie 有一个到期日期时，`connect-mongo` 将使用它。

否则，`connect-mongo` 将使用 `ttl` 选项创建一个新的到期日期，

```js
app.use(session({
    store: new MongoStore({
      url: 'mongodb://localhost/test-app',
      ttl: 14 * 24 * 60 * 60 // = 14 days. Default
    })
}));
```

__注意:__ 每当用户与服务器交互时，它的会话过期日期就会被刷新。

## 移除过期会话

默认情况下，`connect-mongo` 使用  MongoDB 的 TTL 连接特性 (2.2+) 来让 mangod 自动删除过去会话。但是你也可以改变这个行为。

### 设置 MongoDB 来清除过期会话 (默认模式)

`connect-mongo` 将在启动时为你创建一个 TTL 索引。你**必须** 拥有 MongoDB 2.2+ 和管理权限。

```js
app.use(session({
    store: new MongoStore({
      url: 'mongodb://localhost/test-app',
      autoRemove: 'native' // 默认
    })
}));
```

__注意:__ 如果在一个高并发的环境中使用 `connect-mongo`，应该避免这种模式，并且宁可自己设置索引，一次！

### 设置兼容模式

您有一个较旧的 MongoDB 版本(与 `connect-mongo` 兼容)，或者您不能或不想创建 TTL 索引。

`connect-mongo` 将负责移除过期的会话，使用定义的间隔。

```js
app.use(session({
    store: new MongoStore({
      url: 'mongodb://localhost/test-app',
      autoRemove: 'interval',
      autoRemoveInterval: 10 // In minutes. Default
    })
}));
```

### 禁用过期会话清理

在生产环境中，或者在其他地方管理 TTL 索引。

```js
app.use(session({
    store: new MongoStore({
      url: 'mongodb://localhost/test-app',
      autoRemove: 'disabled'
    })
}));
```

## 会话懒更新

如果你使用 [express-session](https://github.com/expressjs/session) >= [1.10.0](https://github.com/expressjs/session/releases/tag/v1.10.0)，而且，不要在每次用户刷新页面时都要重新保存数据库上的所有会话，您可以通过限制一段时间来更新会话。

```js
app.use(express.session({
    secret: 'keyboard cat',
    saveUninitialized: false, // 不创建会话，直到有东西被保存
	resave: false, //如果会话未被修改，不重新保存会话
	store: new MongoStore({
		url: 'mongodb://localhost/test-app',
		touchAfter: 24 * 3600 // 时间以秒为单位
	})
}));
```

通过这样做，设置 `touchAfter: 24 * 3600` ，你说的会话只在 24 小时内更新一次，不管有多少请求(除了那些在会话数据上改变了什么)的请求都不重要。

## 更多选项

  - `collection` 连接 (默认值: `sessions`)
  - `fallbackMemory` 回退到 `MemoryStore`。如果您想在某些情况下使用 MemoryStore，比如在开发环境中，那么这是很有用的。
  - `stringify` 如果是 `true`，connect-mongo 将在设置设置会话之前使用 `JSON.stringify` 序列化他们，
                并在获取他们时，用 `JSON.parse` 对它们进行反序列化(可选的,默认值: `true`)。
                如果你使用的是 MongoDB 不支持的类型，这是很有用的。
  - `serialize` 为 MongoDB 序列化会话的自定义钩子。如果您需要在写出会话之前修改它，这是很有帮助的。
  - `unserialize` 反序列化来自 MongoDB 的会话的自定义钩子。
                  可以被用在需要支持不同类型的序列化(例如，对象和 JSON 字符串)的场景中，
                  或者需要在应用程序中使用会话之前修改它。
  - `transformId` (可选) 将原始的 sessionId 转换为您想要用作存储键的任何内容。

## Tests

```js
npm test
```

测试使用一个名为 `connect-mongo-test` 的数据库。

## License

The MIT License
