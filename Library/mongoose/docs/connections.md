# connections（连接）

您可以使用 `mongoose.connect()` 方法连接到 MongoDB。

```js
mongoose.connect('mongodb://localhost/myapp');
```

这是连接在默认端口（27017）上本地运行的 `myapp` 数据库所需的最小化的代码。如果本地连接失败，请尝试使用 127.0.0.1 而不是 localhost 主机。当本地主机名已被更改时，有时可能会出现问题。

您也可以在 `uri` 中指定更多的参数：

```js
mongoose.connect('mongodb://username:password@host:port/database?options...');
```

有关更多详细信息，请[参阅 mongodb 连接字符串规范](http://docs.mongodb.org/manual/reference/connection-string/)。

## 操作缓冲

Mongoose 可以让你立即开始使用你的模型，而无需等待 mongoose 建立到 MongoDB 的连接。

```js
mongoose.connect('mongodb://localhost/myapp');
var MyModel = mongoose.model('Test', new Schema({ name: String }));
// Works
MyModel.findOne(function(error, result) { /* ... */ });
```

这是因为 mongoose 缓冲模型的函数是在内部调用的。这种缓冲是方便的，但也是一个混乱的来源。如果您使用未连接的模型，Mongoose 默认 *不会抛出任何错误*。

```js
var MyModel = mongoose.model('Test', new Schema({ name: String }));
// 这将会挂起，直到 mongoose 成功连接
MyModel.findOne(function(error, result) { /* ... */ });

setTimeout(function() {
  mongoose.connect('mongodb://localhost/myapp');
}, 60000);
```

要禁用缓冲，请关闭[模式上的 `bufferCommands` 选项](/Library/mongoose/docs/guide.md#bufferCommands)。如果您有缓冲命令，并且连接被挂起，请尝试关闭 `bufferCommands` 以查看是否没有正确打开连接。


## 选项

`connect` 方法还接受一个选项对象，它将被传递给底层的 MongoDB 驱动程序。

```js
mongoose.connect(uri, options);
```

在 [connect() 的 MongoDB Node.js 驱动程序文档](http://mongodb.github.io/node-mongodb-native/2.2/api/MongoClient.html#connect)中可以找到完整的选项列表。Mongoose 将选项传递给驱动程序而无需修改，下面将解释三个例外。

  * `useMongoClient` - 这是一个特定于 mongoose 的选项（不会传递给 MongoDB 驱动程序），它选择了 mongoose 4.11 的新连接逻辑。如果您正在编写新的应用程序，则**应**将其设置为 `true`。
  * `user/pass` —— 用于验证的用户名和密码。这些选项是特定于 mongoose 的，它们相当于 MongoDB 驱动程序的 `auth.user` 和 `auth.password` 选项。
  * `autoIndex` —— 默认情况下，mongoose 将在连接时自动生成在模式中定义的索引。这对于开发很有用，但对于大型生产部署来说并不理想，因为索引构建可能会导致性能下降。如果将 `autoIndex` 设置为 false`，mongoose 将不会自动为与此连接关联的任何模型创建索引。

下面是一些对调整 mongoose 很重要的选项。


* `autoReconnect` —— 底层的 MongoDB 驱动程序会在失去与 MongoDB 的连接时自动尝试重新连接。除非您是非常高级的用户，想要管理自己的连接池。否则**不要**将此选项设置为 `false`。
* `reconnectTries` —— 如果您连接到单个服务器或 mongos代理（而不是副本集），那么 MongoDB 驱动程序将尝试重新连接 `reconnectTries` 次，每隔 `reconnectInterval` 毫秒，然后放弃。当驱动程序放弃时，mongoose 连接发出 `reconnectFailed` 事件。该选项对副本集连接没有任何作用。
* `reconnectInterval` —— 查看 `reconnectTries`。
* `promiseLibrary` —— 设置[底层驱动程序的 promise](http://mongodb.github.io/node-mongodb-native/2.1/api/MongoClient.html)
* `poolSize` —— MongoDB 驱动程序将为此连接保持打开的最大套接字数量。默认情况下，`poolSize` 是 `5` 。请记住，从 MongoDB 3.4 开始，MongoDB 一次只允许每个套接字进行一个操作，因此，如果您发现有一些缓慢的查询阻止了更快的查询，那么您可能想要增加这个值。
* `bufferMaxEntries` —— MongoDB 驱动程序也有自己的缓冲机制，当驱动程序断开连接时会启动。如果希望数据库操作在驱动程序未连接时立即失败，请将此选项设置为 `0`，并在模式中将 `bufferCommands` 设置为 `false`，而不是等待重新连接。

示例：

```js
var options = {
  useMongoClient: true,
  autoIndex: false, // Don't build indexes
  reconnectTries: Number.MAX_VALUE, // Never stop trying to reconnect
  reconnectInterval: 500, // Reconnect every 500ms
  poolSize: 10, // Maintain up to 10 socket connections
  // If not connected, return errors immediately rather than waiting for reconnect
  bufferMaxEntries: 0
};
mongoose.connect(uri, options);
```

### Callbak


`connect()` 函数也接受一个回调参数并返回一个 [promise](/Library/mongoose/docs/promises.md)。

```js
mongoose.connect(uri, options, function(error) {
  // 在初始连接中检查错误。回调没有第二个参数。
});

// 或者使用 promises
mongoose.connect(uri, options).then(
  () => { /** ready to use. The `mongoose.connect()` promise resolves to undefined. */ },
  err => { /** handle initial connection error */ }
);
```
### 连接字符串选项

您也可以在连接字符串中指定选项作为 URI 的[查询字符串部分的参数](https://en.wikipedia.org/wiki/Query_string)。

```js
mongoose.connect('mongodb://localhost:27017/test?connectTimeoutMS=1000', { useMongoClient: true });
// 上面的等效于
mongoose.connect('mongodb://localhost:27017/test', {
  useMongoClient: true,
  connectTimeoutMS: 1000
});
```

在查询字符串中添加选项的缺点是查询字符串选项难以阅读。优点是你只需要一个配置选项，即 URI，而不是单独的 `socketTimeoutMS`，`connectTimeoutMS` 等选项。最佳实践是区分开发和生产，分开放置。如 `replicaSet` 或 `ssl`，以及应该保持不变的选项，应该放在连接字符串中；如 `connectTimeoutMS` 或 `poolSize` 应该放在选项对象中。

[MongoDB 文档](https://docs.mongodb.com/manual/reference/connection-string/)具有支持的连接字符串选项的完整列表。

### 关于 keepAlive 的说明

> **[info]**
>
> 对于长时间运行的应用程序，通常谨慎的做法是使用一个毫秒数启用 `keepAlive`。没有它，一段时间后，你可能会开始看到 `"connection closed"` 的错误，似乎没有理由。如果是这样，[读完这个](http://tldp.org/HOWTO/TCP-Keepalive-HOWTO/overview.html)之后，你可以决定启用 `keepAlive`：

```js
options.server.socketOptions = options.replset.socketOptions = { keepAlive: 120 };
mongoose.connect(uri, options);
```

## 副本集连接

要连接到副本集(replica set)，请传递要连接到的主机列表，以逗号分隔，而不是单个主机。

```js
mongoose.connect('mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][?options]]' [, options]);
```

要连接到单个节点副本集，请指定 `replicaSet` 选项。

```js
mongoose.connect('mongodb://host1:port1/?replicaSet=rsName');
```

## Multi-mongos 支持

多个 `mongos` 实例的高可用性也被支持。传递 `mongos` 实例的连接字符串并将 `mongos` 选项设置为 `true` ：

```js
mongoose.connect('mongodb://mongosA:27501,mongosB:27501', { mongos: true }, cb);
```

## 多个连接

到目前为止，我们已经看到了如何使用 Mongoose 的默认连接来连接到 MongoDB。有时候我们可能需要 Mongo 的多个连接，每个连接都有不同的读/写设置，或者可能只是针对不同的数据库。在这些情况下，我们可以使用 `mongoose.createConnection()` 来接受之前已经讨论过的所有参数，并返回一个新的连接。

```js
var conn = mongoose.createConnection('mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][?options]]', options);
```

这个[连接](http://mongoosejs.com/docs/api.html#connection_Connection)对象然后用来创建和检索[模型](/Library/mongoose/docs/models.md)。模型**始终**限定为一个连接。

## 连接池
每个 `connection`（无论是使用 `mongoose.connect` 还是 `mongoose.createConnection` 创建的）都由内部可配置连接池支持，默认最大大小为 5。使用连接选项调整池大小：

```js
// 单个服务器
var uri = 'mongodb://localhost/test';
mongoose.createConnection(uri, { server: { poolSize: 4 }});

// 一个副本集
mongoose.createConnection(uri, { replset: { poolSize: 4 }});

// 在 URI 中传递选项与单个或副本集一起工作
var uri = 'mongodb://localhost/test?poolSize=4';
mongoose.createConnection(uri);
```

## `useMongoClient` 选项

Mongoose 的默认连接逻辑从 4.11.0 开始已弃用。请使用 `useMongoClient` 选项选择新的连接逻辑，但是如果您要升级现有的代码库，请确保先测试连接。

```js
// 使用 `mongoose.connect`...
var promise = mongoose.connect('mongodb://localhost/myapp', {
  useMongoClient: true,
  /* other options */
});
// 或者 `createConnection`
var promise = mongoose.createConnection('mongodb://localhost/myapp', {
  useMongoClient: true,
  /* other options */
});
promise.then(function(db) {
  /* 使用 `db`, 对于实例 `db.model()`
});
// 或者, 如果你已经有了一个连接
connection.openUri('mongodb://localhost/myapp', { /* options */ });
```

`openUri()` 的参数被透明传递给底层的 MongoDB 驱动程序的 [`MongoClient.connect()`](http://mongodb.github.io/node-mongodb-native/2.2/api/MongoClient.html#connect) 函数。有关选项，请参阅[此函数的驱动程序文档](http://mongodb.github.io/node-mongodb-native/2.2/api/MongoClient.html#connect)。如果 `useMongoClient` 为 `true`，` connect()` 和 `createConnection()`也是 `true`。

您可能会在 `useMongoClient` 中看到以下弃用警告：

```
the server/replset/mongos options are deprecated, all their options are supported at the top level of the options object
```

在旧版本的 MongoDB 驱动程序中，您必须为服务器连接，副本集连接和 mongos 连接指定不同的选项：

```js
mongoose.connect(myUri, {
  server: {
    socketOptions: {
      socketTimeoutMS: 0,
      keepAlive: true
    },
    reconnectTries: 30
  },
  replset: {
    socketOptions: {
      socketTimeoutMS: 0,
      keepAlive: true
    },
    reconnectTries: 30
  },
  mongos: {
    socketOptions: {
      socketTimeoutMS: 0,
      keepAlive: true
    },
    reconnectTries: 30
  }
});
```

使用 `useMongoClient`，你可以在顶层声明这些选项，而不需要额外的嵌套。 以下是所有支持选项的列表。

```js
//等同于上面的代码
mongoose.connect(myUri, {
  socketTimeoutMS: 0,
  keepAlive: true,
  reconnectTries: 30
});
```

这个弃用是因为 [MongoDB 驱动](https://www.npmjs.com/package/mongodb)已经弃用了一个对 mongoose 的连接逻辑至关重要的 API 来支持 MongoDB 3.6，请参阅[这个 github 问题](https://github.com/Automattic/mongoose/issues/5304)和[这个博客帖子](http://thecodebarbarian.com/mongoose-4.11-use-mongo-client.html)了解更多细节。

## 接下来

现在我们已经介绍了 `connections`，让我们来看看如何将我们的功能分解成可重用和可共享的[插件](/Library/mongoose/docs/plugins.md)。
无线
