# express-session

[![](https://img.shields.io/npm/v/express-session.svg)](https://npmjs.org/package/express-session)  
[![](https://img.shields.io/npm/dm/express-session.svg)](https://npmjs.org/package/express-session)  
[![](https://img.shields.io/travis/expressjs/session/master.svg)](https://travis-ci.org/expressjs/session)  
[![](https://img.shields.io/coveralls/expressjs/session/master.svg)](https://coveralls.io/r/expressjs/session?branch=master)  
[![](https://img.shields.io/gratipay/dougwilson.svg)](https://gratipay.com/dougwilson/)

## 安装

这是一个通过 [npm 注册表](https://www.npmjs.com/) 可用的 [Node.js](https://nodejs.org/en/)  模块。使用 [`npm install` 命令](https://docs.npmjs.com/getting-started/installing-npm-packages-locally) 安装：

```sh
$ npm install express-session
```

## API

```js
var session = require('express-session')
```

> **\[info\] 「译者注」**
>
> API 列表：
>
> | 选项 | 类型 | 描述 |
> | :--- | :--- | :--- |
> | [session\(options\)](#sessionoptions) | Function | 使用给定的 `options` 创建一个会话中间件。 |
> | [req.session](#reqsession) | Object | 存储或访问会话数据 |
> | [req.session.id](#req-session-id) |  | 每个会话都有一个与之关联的惟一ID。[`req.sessionID`](#reqsessionid-1) 的别名 |
> | [req.session.cookie](#reqsessioncookie) | Object | 每个会话都有一个惟一的 cookie 对象。 |
> | [req.sessionID](#reqsessionid) |  | 加载会话的 ID |

### session\(options\)

使用给定的 `options` 创建一个会话中间件。

**注意** 会话数据**不会**被保存在 cookie 中，保存的知识会话 ID。会话数据是被保存在服务器端的。

**注意** 自版本 1.5.0 以来，这个模块不再需要使用 [`cookie-parser` middleware](https://www.npmjs.com/package/cookie-parser) 中间件来工作。这个模块现在直接在 `req`/`res` 上读取和写入 cookie。如果这个模块和 `cookie-parser` 之间的 `secret` 不同，那么使用cookie解析器可能会导致问题。

**警告** 默认的服务器端会话存储, `MemoryStore`，是 _有意_ **不**为生产环境而设计的。它在大多数情况下泄漏内存，不会扩展到单个进程，用于调试和开发。

更多存储列表，请参见 [兼容的会话存储](#兼容的会话存储).

#### Options

`express-session` 接受一个选项对象，该对象可以有下列属性。

> **\[info\] 「译者注」**
>
> 选项列表：
>
> | 选项 | 类型 | 描述 | 默认值 |
> | :--- | :--- | :--- | :--- |
> | [cookie](#cookie) | Obeject | 为会话 ID cookie 而设置的对象。 | `{ path: '/', httpOnly: true, secure: false, maxAge: null }` |
> | cookie.domain | String | cookie 适用的域名 | 不设置，默认为只适用于当前域名 |
> | cookie.expires |  | cookie 到期时间 | - |
> | cookie.httpOnly | Boolean | 是否只使用 http cookie | `true` |
> | cookie.maxAge | Number | 用于计算 `Expires` `Set-Cookie` 属性。 |  |
> | cookie.path | String | cookie 的目录 | `/` |
> | cookie.sameSite | Boolean or String | 同源策略 | 未标准化 |
> | cookie.secure | Boolean or `'auto'` | 是否启用安全的 cookie | `false` |
> | genid | Fucntion | 一个函数，来生成一个新的会话 ID。 | 一个 `uid-safe` 库的函数 |
> | name |  | 一个用来在响应中设置\(从请求中读取\)会话 ID cookie 的名称。 | `'connect.sid'` |
> | proxy | Boolean or `undefined` | 在设置安全 cookie 时，信任反向代理\(通过 "X-Forwarded-Proto" 头\)。 | `undefined` |
> | resave | Boolean | 强制将会话保存回会话存储，即使会话在请求期间从未被修改过。 | 现为`true` |
> | rolling | Boolean | 强制在每个响应中设置一个会话标识符 cookie | `false` |
> | saveUninitialized | Boolean | 强制将一个“未初始化”的会话保存到存储中。 | 现为`true` |
> | secret |  | 这是用于签署会话ID cookie 的秘密 |  |
> | store | Object | 会话存储的实例 | `MemoryStore` 实例 |
> | unset | String | 控制取消设置 `req.session` 的结果 | `'keep'` |

##### cookie

为会话 ID cookie 而设置的对象。默认值为  
`{ path: '/', httpOnly: true, secure: false, maxAge: null }`。

下面是可以在这个对象中设置的选项。

##### cookie.domain

为 `Domain` `Set-Cookie` 属性指定值。默认情况下，不设置域名，大多数客户会认为 cookie 只适用于当前的域。

##### cookie.expires

为 `Expires` `Set-Cookie` 属性指定一个 `Date` 对象值。默认情况下，不设置到期时间，大多数认为这是一个“非持久 cookie” ，在类似退出浏览器应用程序的情况下会删除这个 cookie。

**注意** 如果在选项对象（options）中同时设置了 `expires` 和 `maxAge` ，那么最后一个定义的将会被使用。

**注意** `expire` 选项不应该被直接设置，只使用 `maxAge` 选项。

##### cookie.httpOnly

为 `HttpOnly` `Set-Cookie` 属性指定一个 `boolean` 值。当为真时，`HttpOnly` 被设置，否则不设置。默认情况下，`HttpOnly` 属性是设置的。

**注意** 将其设置为 `true` 的时候要小心，因为兼容的客户端不允许客户端 JavaScript 查看 `document.cookie` 中的 cookie。

##### cookie.maxAge

指定一个 `number` 用于计算 `Expires` `Set-Cookie` 属性。这是通过使用当前的服务器时间，并在值中加上 `maxAge` 毫秒来计算一个 `Expires` 日期时间。默认情况下，不设置最大年龄。

**注意** 如果在选项对象（options）中同时设置了 `expires` 和 `maxAge` ，那么最后一个定义的将会被使用。

##### cookie.path

为 `Path` `Set-Cookie` 指定值。默认情况下，它被设置为 `/`，用以表示域名的根路径。

##### cookie.sameSite

为 `SameSite` `Set-Cookie` 属性指定一个 `boolean` 或 `string` 类型的值。

* `true` 将设置 `SameSite` 为 `Strict`，适用于严格地相同站点执行。
* `false` 将不设置 `SameSite` 属性。
* `'lax'` 将设置 `SameSite` 属性为 `Lax`，适用于宽松的相同站点执行。
* `'strict'` 将设置 `SameSite` 为 `Strict`，适用于严格地相同站点执行。

关于不同的执行级别的更多信息可以在[规范](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1.1)中找到。

**注意** 这是一个尚未完全标准化的属性，将来可能会发生变化。这也意味着许多客户端可能会忽略这个属性，直到他们理解了这个属性。

##### cookie.secure

为 `Secure` `Set-Cookie` 属性指定一个 `boolean` 值。当为真时，`Secure` 被设置，否则不设置。默认情况下，`Secure` 是不设置的。

**注意** 在将此设置为 `true` 时要小心，因为如果浏览器没有 HTTPS 连接，那么兼容的客户端将来不会将 cookie 发送回服务器。

请注意 `secure: true` 是**被推荐的**选项。然而，它需要一个启用了 https 的网站。HTTPS 对于安全的 cookie 是必需的。如果 `secure` 被设置，并且通过 HTTP 访问您的站点，则 cookie 不会被设置，如果您的 node.js 位于代理\(proxy\)后，并且正在使用 `secure: true`，您需要在 express 中设置 "trust proxy":

```js
var app = express()
app.set('trust proxy', 1) // trust first proxy
app.use(session({
  secret: 'keyboard cat',
  resave: false,
  saveUninitialized: true,
  cookie: { secure: true }
}))
```

为了在产品中使用安全的 cookie，但是允许在开发中进行测试，下面是一个在 express 中基于 `NODE_ENV` 启用这个设置的示例:

```js
var app = express()
var sess = {
  secret: 'keyboard cat',
  cookie: {}
}

if (app.get('env') === 'production') {
  app.set('trust proxy', 1) // trust first proxy
  sess.cookie.secure = true // serve secure cookies
}

app.use(session(sess))
```

`cookie.secure` 选项也可以设置为特殊值 `'auto'`，让这个设置自动匹配连接的确定的安全性。在使用此设置时要小心，如果该站点同时可用 HTTP 和 HTTPS ，那么一旦 cookie 被设置为HTTPS，它将不再在 HTTP 上可见。当 Express  `"trust proxy"`被适当地设置以简化开发和生产配置时，这是很有用的。

##### genid

一个函数，来生成一个新的会话 ID。提供一个返回一个字符串作为会话ID的函数。如果你想在生成 ID 时使用一些 `req` 的附加值，那么给定 `req` 作为这个函数第一个参数。

默认值为使用 `uid-safe` 库的函数，用以生成 ID。

**注意** 要小心生成惟一的 ID，这样会话就不会冲突。

```js
app.use(session({
  genid: function(req) {
    return genuuid() // use UUIDs for session IDs
  },
  secret: 'keyboard cat'
}))
```

##### name

一个用来在响应中设置\(从请求中读取\)会话 ID cookie 的名称。

默认值是 `'connect.sid'`.

**注意** 如果有多个应用程序运行在相同的主机名上\(这只是名称，即 `localhost` 或 `127.0.0.1`；不同的方案和端口不会命名不同的主机名\)，然后您需要将会话 cookie 彼此分开。最简单的方法是在每个应用程序中设置不同的 `name`。

##### proxy

在设置安全 cookie 时，请信任反向代理\(通过 "X-Forwarded-Proto" 头\)。

默认值是 `undefined`.

* `true` "X-Forwarded-Proto" 头将被设置。
* `false` 所有的头都被忽略，只有在有直接的 TLS/SSL 连接时，连接才被认为是安全的。
* `undefined` 使用来自 express 的  "trust proxy" 设置。

##### resave

强制将会话保存回会话存储，即使会话在请求期间从未被修改过。这取决于你的存储，对存储来说这可能是必要的,但它也可以创建竞态条件，客户端对服务器进行了两个并行请求，当一个请求结束时，在另一个请求中对会话进行更改可能会被覆盖，即使它没有改变\(这种行为也取决于你使用的存储\)。

默认值是 `true`，但是使用默认值已经被弃用，因为默认值将在将来发生变化。请研究这个设置，并选择适合您的用例。通常情况下,你会想使用 `false`。

我怎么知道这对我的存储来说是必要的?最好的方法是检查你的存储是否实现了 `touch` 方法。如果是这样，那么您可以安全地设置 `resave: false`。如果它没有实现 `touch` 方法，并且您的存储在保存的会话中设置了一个过期日期，那么您可能需要 `resave: true`。

##### rolling

强制在每个响应中设置一个会话标识符 cookie。过期时间被重置为原始的 [`maxAge`](#cookiemaxage)，重新设置过期倒计时。

默认值是 `false`。

**注意** 当选项被设置为 `true`，但 `saveUninitialized` 被设置为 `false`，在会话上将使用未被初始化的会话设置 cookie。

##### saveUninitialized

强制将一个“未初始化”的会话保存到存储中。一个会话在它是新的但未被修改时是未初始化的。选择 `false` 对于实现登录会话、减少服务器存储（storage）使用、或遵守在设置 cookie 之前加载许可的规则是非常有用的。选择 `false` 还可以帮助客户端在没有会话下进行多个并行请求的竞态条件。

默认值是 `true`，但是使用默认值已经被弃用，因为默认值将在将来发生变化。请研究这个设置，并选择适合您的用例。

**注意** 如果您正在结合使用 Session 与 PassportJS，那么Passport 将向会话中添加一个空的 Passport 对象，以便在用户经过身份验证后使用该会话，这将作为对会话的修改，从而使其被保存。_这在 PassportJS 0.3.0 中得到了修正。_

##### secret

**必需的选项**

这是用于签署会话ID cookie 的秘密。这可以是单个秘密的字符串，也可以是多个秘密的数组。如果提供了秘密数组，那么只有第一个元素将被用于签署会话ID cookie，而在验证请求中的签名时，所有的元素都将被考虑。

##### store

会话存储的实例，默认为一个新的 `MemoryStore` 实例。

##### unset

控制取消设置 `req.session` 的结果（通过 `delete`、设置为 `null` 等等）。

默认值是 `'keep'`。

* `'destroy'` 当响应结束时，会话将被销毁\(删除\)。
* `'keep'` 存储中的会话将被保留，但是在请求期间所做的修改将被忽略，而不会被保存。

### req.session

要存储或访问会话数据，只需使用请求属性 `req.session` ，这\(通常\)是由存储序列化为 JSON 的，所以嵌套对象通常都很好。下面是一个特定于用户的视图计数器:

```js
// 使用 session 中间件
app.use(session({ secret: 'keyboard cat', cookie: { maxAge: 60000 }}))

// 使用 req.sessio 访问会话
app.get('/', function(req, res, next) {
  if (req.session.views) {
    req.session.views++
    res.setHeader('Content-Type', 'text/html')
    res.write('<p>views: ' + req.session.views + '</p>')
    res.write('<p>expires in: ' + (req.session.cookie.maxAge / 1000) + 's</p>')
    res.end()
  } else {
    req.session.views = 1
    res.end('welcome to the session demo. refresh!')
  }
})
```

> **\[info\] 「译者注」**
>
> 方法列表：
>
> | 方法 | 描述 |
> | :--- | :--- |
> | Session.regenerate\(callback\) | 重新生成会话 |
> | Session.destroy\(callback\) | 销毁会话，并取消设置 `req.session` 属性。 |
> | Session.reload\(callback\) | 从存储中重新加载会话数据，并重新填充 `req.session` 对象 |
> | Session.save\(callback\) | 将会话保存回存储，将存储中的内容替换为内存中的内容 |
> | Session.touch\(\) | 更新 `.maxAge` 属性。 |

#### Session.regenerate\(callback\)

要重新生成会话，只需调用该方法。一旦完成，将在 `req.session` 中初始化一个新的 SID 和 `Session` 实例，并且 `callback` 将被调用。

```js
req.session.regenerate(function(err) {
  // will have a new session here
})
```

#### Session.destroy\(callback\)

销毁会话，并取消设置 `req.session` 属性。一旦完成，`callback` 将被调用。

```js
req.session.destroy(function(err) {
  // cannot access session here
})
```

#### Session.reload\(callback\)

从存储中重新加载会话数据，并重新填充 `req.session` 对象。一旦完成，`callback` 将被调用。

```js
req.session.reload(function(err) {
  // session updated
})
```

#### Session.save\(callback\)

将会话保存回存储，将存储中的内容替换为内存中的内容\(尽管存储可能会做其他事情——请参考存储的文档以获得准确的行为\)。

如果会话数据已被更改，则该方法在 HTTP 响应的末尾被自动调用\(尽管该行为可以在中间件构造函数中使用不同的选项进行修改\)。因此，通常这种方法不需要被调用。

在某些情况下，调用这种方法是很有用的，例如，重定向、长时间的请求或 WebSockets。

```js
req.session.save(function(err) {
  // session saved
})
```

#### Session.touch\(\)

更新 `.maxAge` 属性。通常，这并不需要调用，因为会话中间件为您做了这个。

### req.session.id {#req-session-id}

每个会话都有一个与之关联的惟一ID。这个属性是 [`req.sessionID`](#reqsessionid-1) 的别名，不能被修改。添加了这个会话 ID，就可以从 `session` 对象访问会话 ID。

### req.session.cookie

每个会话都有一个惟一的 cookie 对象。这允许您更改每个访问者的会话 cookie。例如，我们可以设置 `req.session.cookie.expires`  为 `false`，使 cookie仅在用户代理\(user-agent\)的持续时间内保留。

#### Cookie.maxAge

或者 `req.session.cookie.maxAge` 将返回以毫秒为间隔的时间，我们也可以重新分配一个新的值来适当地调整 `.expires` 属性。下面是等效的:

```js
var hour = 3600000
req.session.cookie.expires = new Date(Date.now() + hour)
req.session.cookie.maxAge = hour
```

例如，当 `maxAge` 被设置为 `60000` \(一分钟\)，30 秒过去了它将返回 `30000` 直到当前请求完成，在这段时间的`req.session.touch()` 被调用来重置`req.session.maxAge` 为原始值。

> **\[info\] 「译者注」**
>
> 也就是说 `maxAge` 属性是一个实时变化的值，是一个倒计时。

```js
req.session.cookie.maxAge // => 30000
```

### req.sessionID

要获取已加载会话的 ID，请访问请求属性 `req.sessionID`。当一个会话被载入/创建时，这只是一个只读值。

## 会话存储实现

每个会话存储 _必须_ 是一个 `EventEmitter` 并实现一些指定的方法。下面有一些**必需的**、**推荐的**、**可选的**方法。

* 必需的方法是这个模块总是要在存储上调用的方法。
* 推荐的方法是如果有的话，这个模块可以在存储上调用它。
* 可选的方法是这个模块根本不调用的，但是可以帮助向用户提供统一的存储。

对于一个示例实现，请查看 [connect-redis](http://github.com/visionmedia/connect-redis) 仓库。

> **\[info\] 「译者注」**
>
> 方法列表：
>
> | 方法 | 描述 | 类型 |
> | :--- | :--- | :---: |
> | store.destroy\(sid, callback\) | 从存储中 销毁/删除 一个给定的会话 ID 的会话。 | 必需 |
> | store.get\(sid, callback\) | 从存储使用给定的会话 ID（`sid`）获取一个会话。 | 必需 |
> | store.set\(sid, session, callback\) | 将一个会话更新插入（upsert）到存储\(store\)中，使用给定会话 ID\(`sid`\)和会话\(`session`\)对象。 | 必需 |
> | store.touch\(sid, session, callback\) | 被用来“触碰”（touch）给定的一个给定会话ID\(`sid`\)和会话\(`session`\)对象的会话。 | 推荐 |
> | store.all\(callback\) | 将存储中所有的会话提取到一个数组。 | 可选 |
> | store.clear\(callback\) | 删除存储中所有的会话 | 可选 |
> | store.length\(callback\) | 用于获取存储中所有会话的个数 | 可选 |

### store.all\(callback\)

**可选的**

这个可选的方法被用来将存储中所有的会话提取到一个数组。  
`callback` 应该像 `callback(error, sessions)` 这样被调用。

### store.destroy\(sid, callback\)

**必需的**

这个可选的方法被用于从存储中 销毁/删除 一个给定的会话 ID 的会话。一旦这个会话被销毁，`callback` 应该像 `callback(error)` 这样被调用。

### store.clear\(callback\)

**可选的**

这个可选的方法被用于删除存储中所有的会话。一旦存储被清空，`callback` 应该像 `callback(error)`被调用。

### store.length\(callback\)

**可选的**

这个可选的方法被用于获取存储中所有会话的个数。  
 `callback` 像 `callback(error, len)` 这样被调用。

### store.get\(sid, callback\)

**必需的**

这个必须的方法被用于从存储使用给定的会话 ID（`sid`）获取一个会话。`callback` 应该如同 `callback(error, session)` 这样被调用。

`session` 参数应该是一个被找到的会话，否则如果会话未被找到，它将是 `null` 或 `undefined`（不是一个错误）。一个特殊的例子是，当 `error.code === 'ENOENT'` 时表现得像 `callback(null, null)`。

### store.set\(sid, session, callback\)

**必需的**

这个必需的方法被用于将一个会话更新插入（upsert）到存储\(store\)中，使用给定会话 ID\(`sid`\)和会话\(`session`\)对象。一旦会话被设置到了存储中，回调应该如同 `callback(error)` 一样被调用。

### store.touch\(sid, session, callback\)

**推荐**

这个推荐的方法被用来“触碰”（touch）给定的一个给定会话ID\(`sid`\)和会话\(`session`\)对象。一旦会话被触碰`callback` 应该如同 `callback(error)` 被调用。

这主要用于当存储自动删除空闲会话时，该方法用于向存储发出信号，即给定会话是活动的，可能会重置空闲计时器。

## 兼容的会话存储

下面的模块实现了一个与这个模块兼容的会话存储。请制作一个 PR 来添加额外的模块:\)

[![](https://img.shields.io/github/stars/aerospike/aerospike-session-store-expressjs.svg?label=★) aerospike-session-store](https://www.npmjs.com/package/aerospike-session-store) A session store using [Aerospike](http://www.aerospike.com/).

[![](https://img.shields.io/github/stars/webcc/cassandra-store.svg?label=★) cassandra-store](https://www.npmjs.com/package/cassandra-store) An Apache Cassandra-based session store.

[![](https://img.shields.io/github/stars/coolaj86/cluster-store.svg?label=★) cluster-store](https://www.npmjs.com/package/cluster-store) A wrapper for using in-process / embedded  
stores - such as SQLite \(via knex\), leveldb, files, or memory - with node cluster \(desirable for Raspberry Pi 2  
and other multi-core embedded devices\).

[![](https://img.shields.io/github/stars/mike-goodwin/connect-azuretables.svg?label=★) connect-azuretables](https://www.npmjs.com/package/connect-azuretables) An [Azure Table Storage](https://azure.microsoft.com/en-gb/services/storage/tables/)-based session store.

[![](https://img.shields.io/github/stars/adriantanasa/connect-cloudant-store.svg?label=★) connect-cloudant-store](https://www.npmjs.com/package/connect-cloudant-store) An [IBM Cloudant](https://cloudant.com/)-based session store.

[![](https://img.shields.io/github/stars/christophermina/connect-couchbase.svg?label=★) connect-couchbase](https://www.npmjs.com/package/connect-couchbase) A [couchbase](http://www.couchbase.com/)-based session store.

[![](https://img.shields.io/github/stars/adriantanasa/connect-datacache.svg?label=★) connect-datacache](https://www.npmjs.com/package/connect-datacache) An [IBM Bluemix Data Cache](http://www.ibm.com/cloud-computing/bluemix/)-based session store.

[![](https://img.shields.io/github/stars/wallali/connect-db2.svg?label=★) connect-db2](https://www.npmjs.com/package/connect-db2) An IBM DB2-based session store built using [ibm\_db](https://www.npmjs.com/package/ibm_db) module.

[![](https://img.shields.io/github/stars/ca98am79/connect-dynamodb.svg?label=★) connect-dynamodb](https://github.com/ca98am79/connect-dynamodb) A DynamoDB-based session store.

[![](https://img.shields.io/github/stars/Requarks/connect-loki.svg?label=★) connect-loki](https://www.npmjs.com/package/connect-loki) A Loki.js-based session store.

[![](https://img.shields.io/github/stars/bluetorch/connect-ml.svg?label=★) connect-ml](https://www.npmjs.com/package/connect-ml) A MarkLogic Server-based session store.

[![](https://img.shields.io/github/stars/patriksimek/connect-mssql.svg?label=★) connect-mssql](https://www.npmjs.com/package/connect-mssql) A SQL Server-based session store.

[![](https://img.shields.io/github/stars/MonetDB/npm-connect-monetdb.svg?label=★) connect-monetdb](https://www.npmjs.com/package/connect-monetdb) A MonetDB-based session store.

[![](https://img.shields.io/github/stars/kcbanner/connect-mongo.svg?label=★) connect-mongo](https://www.npmjs.com/package/connect-mongo) A MongoDB-based session store.

[![](https://img.shields.io/github/stars/mongodb-js/connect-mongodb-session.svg?label=★) connect-mongodb-session](https://www.npmjs.com/package/connect-mongodb-session) Lightweight MongoDB-based session store built and maintained by MongoDB.

[![](https://img.shields.io/github/stars/voxpelli/node-connect-pg-simple.svg?label=★) connect-pg-simple](https://www.npmjs.com/package/connect-pg-simple) A PostgreSQL-based session store.

[![](https://img.shields.io/github/stars/tj/connect-redis.svg?label=★) connect-redis](https://www.npmjs.com/package/connect-redis) A Redis-based session store.

[![](https://img.shields.io/github/stars/balor/connect-memcached.svg?label=★) connect-memcached](https://www.npmjs.com/package/connect-memcached) A memcached-based session store.

[![](https://img.shields.io/github/stars/liamdon/connect-memjs.svg?label=★) connect-memjs](https://www.npmjs.com/package/connect-memjs) A memcached-based session store using  
[memjs](https://www.npmjs.com/package/memjs) as the memcached client.

[![](https://img.shields.io/github/stars/llambda/connect-session-knex.svg?label=★) connect-session-knex](https://www.npmjs.com/package/connect-session-knex) A session store using  
[Knex.js](http://knexjs.org/), which is a SQL query builder for PostgreSQL, MySQL, MariaDB, SQLite3, and Oracle.

[![](https://img.shields.io/github/stars/mweibel/connect-session-sequelize.svg?label=★) connect-session-sequelize](https://www.npmjs.com/package/connect-session-sequelize) A session store using  
[Sequelize.js](http://sequelizejs.com/), which is a Node.js / io.js ORM for PostgreSQL, MySQL, SQLite and MSSQL.

[![](https://img.shields.io/github/stars/rafaelrpinto/dynamodb-store.svg?label=★) dynamodb-store](https://www.npmjs.com/package/dynamodb-store) A DynamoDB-based session store.

[![](https://img.shields.io/github/stars/chill117/express-mysql-session.svg?label=★) express-mysql-session](https://www.npmjs.com/package/express-mysql-session) A session store using native  
[MySQL](https://www.mysql.com/) via the [node-mysql](https://github.com/felixge/node-mysql) module.

[![](https://img.shields.io/github/stars/slumber86/express-oracle-session.svg?label=★) express-oracle-session](https://www.npmjs.com/package/express-oracle-session) A session store using native  
[oracle](https://www.oracle.com/) via the [node-oracledb](https://www.npmjs.com/package/oracledb) module.

[![](https://img.shields.io/github/stars/konteck/express-sessions.svg?label=★) express-sessions](https://www.npmjs.com/package/express-sessions): A session store supporting both MongoDB and Redis.

[![](https://img.shields.io/github/stars/rawberg/connect-sqlite3.svg?label=★) connect-sqlite3](https://www.npmjs.com/package/connect-sqlite3) A [SQLite3](https://github.com/mapbox/node-sqlite3) session store modeled after the TJ's `connect-redis` store.

[![](https://img.shields.io/github/stars/dwhieb/documentdb-session.svg?label=★) documentdb-session](https://www.npmjs.com/package/documentdb-session) A session store for Microsoft Azure's [DocumentDB](https://azure.microsoft.com/en-us/services/documentdb/) NoSQL database service.

[![](https://img.shields.io/github/stars/louischatriot/express-nedb-session.svg?label=★) express-nedb-session](https://www.npmjs.com/package/express-nedb-session) A NeDB-based session store.

[![](https://img.shields.io/github/stars/theogravity/express-session-cache-manager.svg?label=★) express-session-cache-manager](https://www.npmjs.com/package/express-session-cache-manager)  
A store that implements [cache-manager](https://www.npmjs.com/package/cache-manager), which supports  
a [variety of storage types](https://www.npmjs.com/package/cache-manager#store-engines).

[![](https://img.shields.io/github/stars/tgohn/express-session-level.svg?label=★) express-session-level](https://www.npmjs.com/package/express-session-level) A [LevelDB](https://github.com/Level/levelup) based session store.

[![](https://img.shields.io/github/stars/gildean/express-etcd.svg?label=★) express-etcd](https://www.npmjs.com/package/express-etcd) An [etcd](https://github.com/stianeikeland/node-etcd) based session store.

[![](https://img.shields.io/github/stars/aliceklipper/fortune-session.svg?label=★) fortune-session](https://www.npmjs.com/package/fortune-session) A [Fortune.js](https://github.com/fortunejs/fortune)  
based session store. Supports all backends supported by Fortune \(MongoDB, Redis, Postgres, NeDB\).

[![](https://img.shields.io/github/stars/jackspaniel/hazelcast-store.svg?label=★) hazelcast-store](https://www.npmjs.com/package/hazelcast-store) A Hazelcast-based session store built on the [Hazelcast Node Client](https://www.npmjs.com/package/hazelcast-client).

[![](https://img.shields.io/github/stars/scriptollc/level-session-store.svg?label=★) level-session-store](https://www.npmjs.com/package/level-session-store) A LevelDB-based session store.

[![](https://img.shields.io/github/stars/BenjaminVadant/medea-session-store.svg?label=★) medea-session-store](https://www.npmjs.com/package/medea-session-store) A Medea-based session store.

[![](https://img.shields.io/github/stars/roccomuso/memorystore.svg?label=★) memorystore](https://www.npmjs.com/package/memorystore) A memory session store made for production.

[![](https://img.shields.io/github/stars/jwathen/mssql-session-store.svg?label=★) mssql-session-store](https://www.npmjs.com/package/mssql-session-store) A SQL Server-based session store.

[![](https://img.shields.io/github/stars/JamesMGreene/nedb-session-store.svg?label=★) nedb-session-store](https://www.npmjs.com/package/nedb-session-store) An alternate NeDB-based \(either in-memory or file-persisted\) session store.

[![](https://img.shields.io/github/stars/MattMcFarland/sequelstore-connect.svg?label=★) sequelstore-connect](https://www.npmjs.com/package/sequelstore-connect) A session store using [Sequelize.js](http://sequelizejs.com/).

[![](https://img.shields.io/github/stars/valery-barysok/session-file-store.svg?label=★) session-file-store](https://www.npmjs.com/package/session-file-store) A file system-based session store.

[![](https://img.shields.io/github/stars/llambda/session-rethinkdb.svg?label=★) session-rethinkdb](https://www.npmjs.com/package/session-rethinkdb) A [RethinkDB](http://rethinkdb.com/)-based session store.

## 示例

一个使用 `express-session` 来为一个用户存储页面视图的简单示例。

```js
var express = require('express')
var parseurl = require('parseurl')
var session = require('express-session')

var app = express()

app.use(session({
  secret: 'keyboard cat',
  resave: false,
  saveUninitialized: true
}))

app.use(function (req, res, next) {
  if (!req.session.views) {
    req.session.views = {}
  }

  // 获取 url pathname
  var pathname = parseurl(req).pathname

  // count the views
  req.session.views[pathname] = (req.session.views[pathname] || 0) + 1

  next()
})

app.get('/foo', function (req, res, next) {
  res.send('you viewed this page ' + req.session.views['/foo'] + ' times')
})

app.get('/bar', function (req, res, next) {
  res.send('you viewed this page ' + req.session.views['/bar'] + ' times')
})
```

## License

[MIT](LICENSE)

