# mysql

[![NPM Version][npm-image]][npm-url]
[![NPM Downloads][downloads-image]][downloads-url]
[![Node.js Version][node-version-image]][node-version-url]
[![Linux Build][travis-image]][travis-url]
[![Windows Build][appveyor-image]][appveyor-url]
[![Test Coverage][coveralls-image]][coveralls-url]

## 内容列表

- [安装](#安装)
- [介绍](#介绍)
- [贡献者](#贡献者)
- [赞助商](#赞助商)
- [建立连接](#建立连接)
- [连接选项](#连接选项)
- [终止连接](#终止连接)
- [连接池](#连接池)
- [池选项](#池选项)
- [池事件](#池事件)
- [关闭一个池中的所有连接](#关闭一个池中的所有连接)
- [池集群](#池集群)
- [切换用户和更改连接状态](#切换用户和更改连接状态)
- [服务器断开连接](#服务器断开连接)
- [执行查询](#执行查询)
- [转义查询值](#转义查询值)
- [转义查询标识符](#转义查询标识符)
- [获取插入行的 id](#获取插入行的-id)
- [获取受影响的行数](#获取受影响的行数)
- [获取被修改的行数](#获取被修改的行数)
- [获取连接 ID](#获取连接-id)
- [并行执行查询](#并行执行查询)
- [流式查询行](#流式查询行)
- [多语句查询](#多语句查询)
- [存储过程](#存储过程)
- [带有重叠列名的 Joins](#带有重叠列名的-joins)
- [事务](#事务)
- [Ping](#ping)
- [超时](#超时)
- [错误处理](#错误处理)
- [异常安全](#异常安全)
- [类型转换](#类型转换)
- [连接标志](#连接标志)
- [调试和报告问题](#调试和报告问题)
- [安全问题](#安全问题)
- [贡献](#贡献)
- [运行测试](#运行测试)
- [Todo](#todo)


## 安装

```sh
$ npm install mysql
```

关于之前的 0.9.x 版本的信息，请访问 [v0.9 branch][].

有时，我可能还会请求你安装 Github 上的最新版本，以检查 bug 修复是否有效。在这种情况下，请:

```sh
$ npm install mysqljs/mysql
```

[v0.9 branch]: https://github.com/mysqljs/mysql/tree/v0.9

## 介绍

这是一个 mysql 的 node.js 驱动程序。它是用 JavaScript 编写的，不需要编译，并且 100% 的 MIT 许可。

这里有一个关于如何使用它的例子:

```js
var mysql      = require('mysql');
var connection = mysql.createConnection({
  host     : 'localhost',
  user     : 'me',
  password : 'secret',
  database : 'my_db'
});

connection.connect();

connection.query('SELECT 1 + 1 AS solution', function (error, results, fields) {
  if (error) throw error;
  console.log('The solution is: ', results[0].solution);
});

connection.end();
```

从这个示例中，您可以了解以下内容:

* 您在连接上调用的每个方法都是排队并按顺序执行的。
* 关闭连接是使用 `end()` 完成的，在发送一个退出数据包到 mysql 服务器之前，确保所有剩余的查询都被执行。

## 贡献者

感谢那些为这个模块贡献代码的人, 查看
[GitHub 贡献页面][].

[GitHub 贡献页面]: https://github.com/mysqljs/mysql/graphs/contributors

另外，我还要感谢以下的人:

* [Andrey Hristov][] (Oracle) - 帮助我解决了协议的诸多问题。
* [Ulf Wendel][] (Oracle) - 帮助我解决了协议的诸多问题。

[Ulf Wendel]: http://blog.ulf-wendel.de/
[Andrey Hristov]: http://andrey.hristov.com/

## 赞助商

以下公司在财务上支持这个项目，允许我在它上花更多的时间(按贡献时间排序):

* [Transloadit](http://transloadit.com) (my startup, we do file uploading &
  video encoding as a service, check it out)
* [Joyent](http://www.joyent.com/)
* [pinkbike.com](http://pinkbike.com/)
* [Holiday Extras](http://www.holidayextras.co.uk/) (they are [hiring](http://join.holidayextras.co.uk/))
* [Newscope](http://newscope.com/) (they are [hiring](https://newscope.com/unternehmen/jobs/))

## 社区

如果你想讨论这个模块，或者问一些关于这个模块的问题，请使用以下的一个:

* **Mailing list**: https://groups.google.com/forum/#!forum/node-mysql
* **IRC Channel**: #node.js (在 freenode.net 上，我会注意到任何包含术语 `mysql` 的消息。)

## 建立连接

建立连接的推荐方法是这样的:

```js
var mysql      = require('mysql');
var connection = mysql.createConnection({
  host     : 'example.org',
  user     : 'bob',
  password : 'secret'
});

connection.connect(function(err) {
  if (err) {
    console.error('error connecting: ' + err.stack);
    return;
  }

  console.log('connected as id ' + connection.threadId);
});
```

但是，也可以通过调用查询来隐式地建立连接:

```js
var mysql      = require('mysql');
var connection = mysql.createConnection(...);

connection.query('SELECT 1', function (error, results, fields) {
  if (error) throw error;
  // connected!
});
```

根据您喜欢处理错误的方式，任何一种方法都可能是合适的。
任何类型的连接错误(握手或网络)都被认为是一个致命错误，请参阅 [错误处理](#错误处理) 部分以获得更多信息。

## 连接选项

在建立连接时，您可以设置以下选项:

* `host`: 要连接的数据库的主机名。 (默认值: `localhost`)
* `port`: 要连接到的端口号。 (默认值: `3306`)
* `localAddress`: 用于 TCP 连接的源 IP 地址。(可选)
* `socketPath`: 连接到 unix 域套接字的路径。当使用 `host` 和 `port` 时被忽略。
* `user`: 进行身份验证 MySQL 用户名。
* `password`: MySQL 用户的密码。
* `database`: 用于此连接的数据库的名称(可选)。
* `charset`: 连接的字符集。这在 MySQL 的 SQL 级(如 `utf8_general_ci`) 中被称为“collation”。如果指定了一个sql级字符集(如 `utf8mb4`)，则使用该字符集的默认排序(collation)。(默认值: `'UTF8_GENERAL_CI'`)
* `timezone`: 在 MySQL 服务器上配置的时区。这用于将 「服务器日期/时间」 值类型转换为 JavaScript `Date` 对象，反之亦然。这可以是 `'local'`，`'Z'`，或者是形式 `+HH:MM` 或 `-HH:MM`。(默认: `'local'`)
* `connectTimeout`: 在连接到 MySQL 服务器的初始连接期间发生超时的毫秒。(默认值: `10000`)
* `stringifyObjects`: 字符串化对象而不是转换为值。 参见
issue [#501](https://github.com/mysqljs/mysql/issues/501). (默认值: `false`)
* `insecureAuth`: 允许连接到要求旧(不安全)身份验证方法的 MySQL 实例。 (默认值: `false`)
* `typeCast`: 确定是否应该将列值转换为原生的 JavaScript 类型。 (默认值: `true`)
* `queryFormat`: 自定义的查询格式化函数。参见 [自定义格式](#自定义格式)。
* `supportBigNumbers`: 当在数据库中处理大数字(BIGINT 和 DECIMAL 列)时，应该启用这个选项。(默认值: `false`).
* `bigNumberStrings`: 启用 `supportBigNumbers` 和 `bigNumberStrings` 会迫使大量的数字(BIGINT 和 DECIMAL列)总是作为 JavaScript 字符串对象被返回(默认值: `false`)。启用 `supportBigNumbers` ，但是保持 `bigNumberStrings` 的禁用，当他们不能被准确地使用 [JavaScript Number 对象](http://ecma262-5.com/ELS5_HTML.htm#Section_8.5)表示(当他们超过了 [-2^53, +2^53] 这个范围)时，大数字将作为字符串对象被返回，否则它们将作为 Number 对象被返回。如果 `supportBigNumbers` 被禁用，将忽略此选项。
* `dateStrings`: 强制日期类型(TIMESTAMP, DATETIME, DATE)作为字符串返回，而不是让其膨胀为 JavaScript Date 对象。可以是 `true`/`false` 或一个类型名字符串的数组。(默认值: `false`)
* `debug`: 将协议细节打印到标准输出。 可以是 `true`/`false` 或者一个「应该被打印的数据包类型名称数组」。(默认值: `false`)
* `trace`: 在 `Error` 上生成堆栈跟踪信息，包括调用库入口站点(“长堆栈跟踪”)。对大多数调用来说，会有轻微的性能损失。(默认值: `true`)
* `multipleStatements`: 允许每个查询使用多个 mysql 语句。注意这一点，它可能会增加 SQL 注入攻击的范围。(默认值: `false`)
* `flags`: 指定连接标志的列表，来使用的不是默认的标志。也有可能将默认的标志列入黑名单。更多信息，请查看 [连接标志](#连接标志)。
* `ssl`: 一个带有 ssl 参数的对象或包含 ssl 配置文件名称的字符串。查看 [SSL 选项](#ssl-选项).

> **[info] 选项列表**
>
> 选项  |  类型   | 描述  |  默认值
> ------------|------------|----------------|----------------
>  `host` |   String    | 要连接的数据库的主机名 |  `localhost`
>  `port`  |    Number    | 要连接到的端口号  |  `3306`
>  `localAddress` |   String     | 用于 TCP 连接的源 IP 地址  |  可选
>  `socketPath` |    String      | 连接到 unix 域套接字的路径。当使用 `host` 和 `port` 时被忽略。 |
>  `user` |     String    | 进行身份验证 MySQL 用户名 |
>  `password` |    String    | MySQL 用户的密码  |
>  `database` |    String    | 用于此连接的数据库的名称  | 可选
>  `charset` |    [String](https://dev.mysql.com/doc/refman/5.7/en/charset-charsets.html)     | 连接的字符集 | `'UTF8_GENERAL_CI'`
>  `timezone` |    String    | 在 MySQL 服务器上配置的时区  | `'local'`
>  `connectTimeout` |    Number     | 在连接到 MySQL 服务器的初始连接期间发生超时的毫秒 | `10000`
>  `stringifyObjects` |    Boolean    | 字符串化对象而不是转换为值  | `false`
>  `insecureAuth` |    Boolean    | 允许连接到要求旧(不安全)身份验证方法的 MySQL 实例  | `false`
>  `typeCast` |    Boolean    | 确定是否应该将列值转换为原生的 JavaScript 类型  | `true`
>  `queryFormat` |    Function or Boolean     | 自定义的查询格式化函数 | `false`
>  `supportBigNumbers` |   Boolean      | 当在数据库中处理大数字(BIGINT 和 DECIMAL 列)时，应该启用这个选项 | `false`
>  `bigNumberStrings` |    Boolean     | 大数字是否始终作为字符串对象被返回 | `false`
>  `dateStrings` |    Boolean or Array     | 强制日期类型(TIMESTAMP, DATETIME, DATE)作为字符串返回 | `false`
>  `debug` |    Boolean     | 将协议细节打印到标准输出  | `false`
>  `trace` |      Boolean or Array   | 在 `Error` 上生成堆栈跟踪信息，包括调用库入口站点(“长堆栈跟踪”) | `true`
>  `multipleStatements` |   Boolean      | 允许每个查询使用多个 mysql 语句 | `false`
>  `flags` |   List     | 指定连接标志的列表，来使用的不是默认的标志  |
>  `ssl` |    Object or String    | 一个带有 ssl 参数的对象或包含 ssl 配置文件名称的字符串  |


除了将这些选项作为对象传递之外，还可以使用 url 字符串。例如:

```js
var connection = mysql.createConnection('mysql://user:pass@host/db?debug=true&charset=BIG5_CHINESE_CI&timezone=-0700');
```

注意:首先尝试将查询值作为 JSON 解析，如果失败则假定为明文字符串。

### SSL 选项

连接选项中的 `ssl` 选项需要一个字符串或一个对象。当给定一个字符串时，它使用一个预定义的 SSL 配置文件。以下配置文件包括:

* `"Amazon RDS"`: 该配置文件用于连接到 Amazon RDS 服务器，并包含来自 https://rds.amazonaws.com/doc/rds-ssl-ca-cert.pem 和 https://s3.amazonaws.com/rds-downloads/rds-combined-ca-bundle.pem 的证书。


当连接到其他服务器时，您需要提供一个选项的对象，与 [tls.createSecureContext](https://nodejs.org/api/tls.html#tls_tls_createsecurecontext_options) 格式相同。请注意，这个参数期望的是证书的字符串，而不是证书的文件名。这里有一个简单的例子:

```js
var connection = mysql.createConnection({
  host : 'localhost',
  ssl  : {
    ca : fs.readFileSync(__dirname + '/mysql-ca.crt')
  }
});
```

您也可以连接到一个 MySQL 服务器，而不需要正确地提供适当的 CA 来信任。 _你不应该这样做_.

```js
var connection = mysql.createConnection({
  host : 'localhost',
  ssl  : {
    // 不要这样做
    // 正确地设置你的 ca 来信任这个连接
    rejectUnauthorized: false
  }
});
```

## 终止连接

有两种方法可以结束连接。通过调用 `end()` 方法来优雅地终止连接：

```js
connection.end(function(err) {
  // 连接现在终止了
});
```
这将确保在向 MySQL 服务器发送 `COM_QUIT` 数据包之前，所有之前的排队的查询都是静态的。
如果在发送 `COM_QUIT` 数据包之前发生了致命错误，那么将会向回调提供 `err` 的参数，但是无论如何，连接将被终止。

结束连接的另一种方法是调用 `destroy()` 方法。这将导致底层套接字的立即终止。
另外，`destroy()` 保证连接不会触发任何事件或回调。

```js
connection.destroy();
```

不同于 `end()` ， `destroy()` 方法不接受回调函数。

## 连接池

Pooling connection。这个模块不是逐个创建和管理连接，而是使用 `mysql.createPool(config)` 提供内置的连接池。
[阅读更多关于连接池](https://en.wikipedia.org/wiki/Connection_pool)。

直接使用池。
```js
var mysql = require('mysql');
var pool  = mysql.createPool({
  connectionLimit : 10,
  host            : 'example.org',
  user            : 'bob',
  password        : 'secret',
  database        : 'my_db'
});

pool.query('SELECT 1 + 1 AS solution', function (error, results, fields) {
  if (error) throw error;
  console.log('The solution is: ', results[0].solution);
});
```

连接可以被集中起来，以方便共享单个连接，或者管理多个连接。


```js
var mysql = require('mysql');
var pool  = mysql.createPool({
  host     : 'example.org',
  user     : 'bob',
  password : 'secret',
  database : 'my_db'
});

pool.getConnection(function(err, connection) {
  // connected! (unless `err` is set)
});
```

当您完成一个连接时，只需调用 `connection.release()` 连接就会返回到池中，准备再次被其他人使用。


```js
var mysql = require('mysql');
var pool  = mysql.createPool(...);

pool.getConnection(function(err, connection) {
  // 使用连接
  connection.query('SELECT something FROM sometable', function (error, results, fields) {
    // 完成了连接。
    connection.release();

    //在 release 后处理错误
    if (error) throw error;

    // 不要在这里使用连接，它已经返回到池中。
  });
});
```

如果您想关闭连接并将其从池中删除，则使用 `connection.destroy()` 代替。这个池将在下一次需要时创建一个新的连接。

连接是由池怠惰地(lazily)创建的。如果您将池配置为允许最多 100 个连接，但是只同时使用5个连接，那么只有5个连接会被创建。连接也是循环的（cycled）轮询（round-robin）样式，连接从池的顶部被取走并返回底部。

当从池中检索到以前的连接时，将发送一个 ping 数据包到服务器，以检查连接是否仍然良好。

## 池选项

池接受所有与连接相同的[选项](#连接选项)。在创建新连接时，选项只是简单地传递给连接构造函数。除了这些选项之外，池还可以接受一些额外的选项:

* `acquireTimeout`: 在连接获取期间发生超时之前的毫秒。这与 `connectTimeout` 略有不同，因为获得一个池连接并不总是涉及创建连接。(默认值: `10000`)
* `waitForConnections`: 当没有可用连接并且已经达到了限制，确定池的动作。如果是 `true`，池将排队等待连接请求，并在可用时调用它。如果为 `false`，池将立即返回错误。(默认值: `true`)
* `connectionLimit`: 同时被创建的连接的最大数量。(默认值: `10`)
* `queueLimit`: 从 `getConnection` 返回错误之前，池将排队的最大连接请求数。如果设置为 `0`，排队的连接请求的数量是没有限制的。 (默认值: `0`)

## 池事件

### acquire

当从池中获取连接时，池将发射一个 `acquire` 事件。这是在连接被提交到获取代码的回调之前，连接上所有的获取活动都被执行完成之后调用的。_「译者注：」 已经拿到到连接但是还未将连接发到回调函数_

```js
pool.on('acquire', function (connection) {
  console.log('Connection %d acquired', connection.threadId);
});
```

### connection

当在池中建立新的连接时，池将发出一个 `connection` 事件。如果您需要在连接使用之前设置会话变量，那么您可以监听 `connection` 事件。

>**[info] 注意**
>
> 在池中新建一个连接时才会触发这个事件，如果是复用池中的连接不会触发此事件。


```js
pool.on('connection', function (connection) {
  connection.query('SET SESSION auto_increment_increment=1')
});
```

### enqueue

当一个回调已经排队等待可用连接时，池将发出一个 `enqueue` 事件。

```js
pool.on('enqueue', function () {
  console.log('Waiting for available connection slot');
});
```

### release

当连接被释放回池时，池将发射一个 `release` 事件。这是在连接上的所有释放动作被执行完成之后调用的，所以在事件发生时，连接将被列出。「译者注」：也就是说，在 `release` 事件的回调中，这个被释放的连接是可用的。

```js
pool.on('release', function (connection) {
  console.log('Connection %d released', connection.threadId);
});
```

## 关闭一个池中的所有连接

当您使用完这个池时，您必须结束所有的连接。或者 Node.js 事件循环将保持活动状态，直到 MySQL 服务器关闭连接。如果在脚本中使用池或试图优雅地关闭服务器时，通常会这样做。要结束池中的所有连接，请在池上使用 `end` 方法:

```js
pool.end(function (err) {
  // 池中的所有连接都已结束
});
```

`end` 方法的回调是 _可选的_，你可以使用它来告知一次：所有的连接都已结束了。

**一旦 `pool.end()` 被调用， `pool.getConnection` 和其他操作都不能被执行了。**

这是通过在池中的每个活动连接上调用 `connection.end()` 完成的，池会在连接上排队一个 `QUIT` 数据包。并设置一个标志来防止 `pool.getConnection` 继续创建任何新连接。

由于在每个连接上都有一个 `QUIT`  数据包，所以已经在进行中的所有命令/查询都将完成，就像调用 `connection.end()` 一样。如果 `pool.end` 被调用，还有一些尚未被释放的连接，这些连接将无法在 `pool.end` 执行任何新的命令。因为他们在队列中有一个行将发生的的 `QUIT` 数据包；在调用 `pool.end()` 之前，等待，直到所有连接释放回池中。

由于 `pool.query` 方法是 `pool.getConnection` -> `connection.query` `connection.release()` 流程的一个速记形式，在所有的查询通过 `pool.query` 已经完成添加之前调用 `pool.end()`，会因为底层的 `pool.getConnection` 而失败，因为所有连接正在结束中并且不允许创建新的连接而失败。

>**[info] 笔记**
>
> 总结以上的叙述，有一下几点：
> * `pool.end()` 结束所有连接是靠在每个连接上调用 `connection.end()` 来完成的。
> * 由于是正常的结束，因此已经获取到的连接上进行的查询操作会继续知道完成，然后释放连接。
> * 已释放的连接不允许再用来进行任何操作
> * 正在等待获取连接的操作 `pool.query`、`pool.getConnection` 都不会再继续执行了。



## 池集群

池集群提供多个主机连接。 (group & retry & selector)

```js
// 创建
var poolCluster = mysql.createPoolCluster();

// 添加配置 (config 是一个池配置对象)
poolCluster.add(config); // 添加带有自动名称的配置
poolCluster.add('MASTER', masterConfig); // 添加一个命名配置
poolCluster.add('SLAVE1', slave1Config);
poolCluster.add('SLAVE2', slave2Config);

// 移除配置
poolCluster.remove('SLAVE2'); // By nodeId
poolCluster.remove('SLAVE*'); // By target group : SLAVE1-2

// Target Group : ALL(anonymous, MASTER, SLAVE1-2), Selector : round-robin(默认)
poolCluster.getConnection(function (err, connection) {});

// Target Group : MASTER, Selector : round-robin
poolCluster.getConnection('MASTER', function (err, connection) {});

// Target Group : SLAVE1-2, Selector : order
// 如果不能连接到 SLAVE1, 返回 SLAVE2. (从集群中移除 SLAVE1)
poolCluster.on('remove', function (nodeId) {
  console.log('REMOVED NODE : ' + nodeId); // nodeId = SLAVE1
});

// 被传递的模式可以使用 * 作为通配符
poolCluster.getConnection('SLAVE*', 'ORDER', function (err, connection) {});

// 模式也可以是正则表达式
poolCluster.getConnection(/^SLAVE[12]$/, function (err, connection) {});

// of namespace : of(pattern, selector)
poolCluster.of('*').getConnection(function (err, connection) {});

var pool = poolCluster.of('SLAVE*', 'RANDOM');
pool.getConnection(function (err, connection) {});
pool.getConnection(function (err, connection) {});
pool.query(function (error, results, fields) {});

// 关闭所有连接
poolCluster.end(function (err) {
  //池集群中的所有连接都已结束
});
```

### 池集群选项

* `canRetry`: 如果为 `true`, 当连接失败时，`PoolCluster` 将尝试重连。 (默认值: `true`)
* `removeNodeErrorCount`: 如果连接失败, 节点的 `errorCount` 增加。
  当 `errorCount` 大于 `removeNodeErrorCount` 时，删除 `PoolCluster` 中的一个节点。 (Default: `5`)
* `restoreNodeTimeout`: 如果连接失败，指定在另一个连接尝试之前的毫秒数。如果为 `0`， 那么节点将被删除，而不会重新使用。(默认值: `0`)
* `defaultSelector`: 默认的选择器。 (默认值: `RR`)
  * `RR`: 选择一个交替 (alternately)。 (Round-Robin)
  * `RANDOM`: 使用 random 函数选择节点。
  * `ORDER`: 无条件地选择第一个可用的节点。

```js
var clusterConfig = {
  removeNodeErrorCount: 1, // Remove the node immediately when connection fails.
  defaultSelector: 'ORDER'
};

var poolCluster = mysql.createPoolCluster(clusterConfig);
```

## 切换用户和更改连接状态

MySQL 提供了 `changeUser` 命令，允许您更改连接的当前用户和其他方面，而不需要关闭底层套接字。

```js
connection.changeUser({user : 'john'}, function(err) {
  if (err) throw err;
});
```

该特性的可用选项是:

* `user`: 新用户的名称 (默认为前一个)。
* `password`: 新用户的密码 (默认为前一个)。
* `charset`: 新的字符集 (默认为前一个)。
* `database`: 新的数据库 (默认为前一个)。

该功能副作用有时候是有用的，副作用是该函数还会重置任何连接状态(变量、事务等)。

在这个操作过程中遇到的错误将被这个模块视为致命的连接错误。

## 服务器断开连接

由于网络问题、服务器定时启动、服务器重启或崩溃，您可能会丢失与 MySQL 服务器的连接。
所有这些事件都被认为是致命的错误，并且会有 `err.code ='PROTOCOL_CONNECTION_LOST'`。
参见 [错误处理](#错误处理) 部分获得更多信息。

重连一个连接是通过建立一个新的连接来完成的。一旦终止，一个现有的连接对象就不能重新连接，这是被设计成这样的。

在池中，断连的连接将被从池中删除，从而为在下一次 `getConnection` 调用中创建的新连接释放出空间。


## 执行查询

执行查询的最基本的方法是在一个对象上（像 `Connection`, `Pool`, 或者 `PoolNamespace` 实例）调用 `.query()` 方法。

`.query()` 最简单的形式是 `.query(sqlString, callback)`，其中 SQL 字符串是第一个参数，第二个参数是回调:

```js
connection.query('SELECT * FROM `books` WHERE `author` = "David"', function (error, results, fields) {
  // 如果在查询期间发生了一个错误，error 将会是一个 Error 对象
  // results 将包含查询结果
  // fields 将包含返回的结果字段的信息(如果有的话)
});
```
当使用占位符值时，第二种形式 `.query(sqlString, values, callback)` 来了。(参见 [转义查询值](#转义查询值)):

```js
connection.query('SELECT * FROM `books` WHERE `author` = ?', ['David'], function (error, results, fields) {
  // 如果在查询期间发生了一个错误，error 将会是一个 Error 对象
  // results 将包含查询结果
  // fields 将包含返回的结果字段的信息(如果有的话)
});
```

当在查询中使用各种高级选项时，如[转义查询值](#转义查询值),
[带有重叠列名的 Joins](#带有重叠列名的-joins),
[超时](#超时), 和 [类型转换](#类型转换)，可以使用第三种形式 `.query(options, callback)`。

```js
connection.query({
  sql: 'SELECT * FROM `books` WHERE `author` = ?',
  timeout: 40000, // 40s
  values: ['David']
}, function (error, results, fields) {
  // 如果在查询期间发生了一个错误，error 将会是一个 Error 对象
  // results 将包含查询结果
  // fields 将包含返回的结果字段的信息(如果有的话)
});
```

注意，可以使用第二和第三种形式的组合，将占位符值作为参数传递，而不是在选项对象中。`values` 参数将覆盖选项对象中的 `values`。

```js
connection.query({
    sql: 'SELECT * FROM `books` WHERE `author` = ?',
    timeout: 40000, // 40s
  },
  ['David'],
  function (error, results, fields) {
    // 如果在查询期间发生了一个错误，error 将会是一个 Error 对象
    // results 将包含查询结果
    // fields 将包含返回的结果字段的信息(如果有的话)
  }
);
```

## 转义查询值

**谨慎** 这些转义值的方法只有在 [NO_BACKSLASH_ESCAPES](https://dev.mysql.com/doc/refman/5.7/en/sql-mode.html#sqlmode_no_backslash_escapes) 才可用。
SQL 模式是禁用的（这是MySQL服务器的默认状态）。

为了避免 SQL 注入攻击，在 SQL 查询中使用它之前，您应该总是转义任何用户提供的数据。可以使用 `mysql.escape()`, `connection.escape()` 或者 `pool.escape()` 方法：

```js
var userId = 'some user provided value';
var sql    = 'SELECT * FROM users WHERE id = ' + connection.escape(userId);
connection.query(sql, function (error, results, fields) {
  if (error) throw error;
  // ...
});
```

或者，您可以使用 `?` 字符作为你想要转义的值的占位符:

```js
connection.query('SELECT * FROM users WHERE id = ?', [userId], function (error, results, fields) {
  if (error) throw error;
  // ...
});
```

多个占位符被映射到与通过的相同顺序传入的值数组中。例如，在以下的查询中，`foo` = `a`，`bar` = `b`，`baz` = `c`，而 `id` 将是 `userId`:

```js
connection.query('UPDATE users SET foo = ?, bar = ?, baz = ? WHERE id = ?', ['a', 'b', 'c', userId], function (error, results, fields) {
  if (error) throw error;
  // ...
});
```

这看起来类似于 MySQL 中的 prepared statements，但是它实际上只是在内部使用了同一个 `connection.escape()`内部的方法。

**谨慎** 这也与 prepared statements 不同，即所有的 `？`都被替换，即使是包含在注释和字符串中的。

不同的值类型被不同地转义，下面是如何:

* Numbers 保持不变
* Booleans 被转换为 `true` / `false`
* Date 对象被转换为 `'YYYY-mm-dd HH:ii:ss'` 字符串
* Buffers 被转换为十六进制字符串，例如 `X'0fa5'`
* Strings 被安全地转义
* Arrays 被变成 list，例如 `['a', 'b']` 变为 `'a', 'b'`
* 嵌套 arrays 被变为分组的 lists (对于批量插入), 例如 `[['a','b'], ['c', 'd']]` 变为 `('a', 'b'), ('c', 'd')`
* Object，具有 `toSqlString` 方法的对象将被调用`.toSqlString()` 并且返回的值被用作原始 SQL。
* Objects 上的每个可枚举属性被转换成 `key = 'val'` 对。如果属性值是一个函数，则跳过;如果属性的值是一个对象，则调用 `toString()`，并使用返回的值。
* `undefined` / `null` 被转为 `NULL`
* `NaN` / `Infinity` 按原样。 MySQL 不支持这些，尝试将它们作为值插入，将会触发 MySQL 错误，直到它们实现支持。

这种转义可以让你做这样的事情:

```js
var post  = {id: 1, title: 'Hello MySQL'};
var query = connection.query('INSERT INTO posts SET ?', post, function (error, results, fields) {
  if (error) throw error;
  // Neat!
});
console.log(query.sql); // INSERT INTO posts SET `id` = 1, `title` = 'Hello MySQL'
```

`toSqlString` 方法允许您使用函数来组成复杂的查询:

```js
var CURRENT_TIMESTAMP = { toSqlString: function() { return 'CURRENT_TIMESTAMP()'; } };
var sql = mysql.format('UPDATE posts SET modified = ? WHERE id = ?', [CURRENT_TIMESTAMP, 42]);
console.log(sql); // UPDATE posts SET modified = CURRENT_TIMESTAMP() WHERE id = 42
```

要使用 `toSqlString` 方法生成对象，`mysql.raw()` 方法可以被使用。
这就创建了一个对象，当在一个 `?` 占位符中使用时，保持不变，占位符，对于使用函数作为动态值很有用:

**谨慎** 提供给 `mysql.raw()` 的字符串在使用时将跳过所有转义函数，因此在传入未经验证的输入时要小心。

```js
var CURRENT_TIMESTAMP = mysql.raw('CURRENT_TIMESTAMP()');
var sql = mysql.format('UPDATE posts SET modified = ? WHERE id = ?', [CURRENT_TIMESTAMP, 42]);
console.log(sql); // UPDATE posts SET modified = CURRENT_TIMESTAMP() WHERE id = 42
```

如果您觉得需要靠自己来转义查询，那么您也可以直接使用转义函数:

```js
var query = "SELECT * FROM posts WHERE title=" + mysql.escape("Hello MySQL");

console.log(query); // SELECT * FROM posts WHERE title='Hello MySQL'
```

## 转义查询标识符

如果您不能信任 SQL 标识符(数据库/表/列名)，因为它是由用户提供的，那么您应该使用 `mysql.escapeId(identifier)`、
`connection.escapeId(identifier)` 或者 `pool.escapeId(identifier)` 来对它进行转义，像这样：

```js
var sorter = 'date';
var sql    = 'SELECT * FROM posts ORDER BY ' + connection.escapeId(sorter);
connection.query(sql, function (error, results, fields) {
  if (error) throw error;
  // ...
});
```

它还支持添加合格的标识符。它将会转义这两个部分。

```js
var sorter = 'date';
var sql    = 'SELECT * FROM posts ORDER BY ' + connection.escapeId('posts.' + sorter);
// -> SELECT * FROM posts ORDER BY `posts`.`date`
```

如果你不想把 `.` 作为合格的标识符，您可以将第二个参数设置为 `true`，以保持字符串作为文字标识符:

```js
var sorter = 'date.2';
var sql    = 'SELECT * FROM posts ORDER BY ' + connection.escapeId(sorter, true);
// -> SELECT * FROM posts ORDER BY `date.2`
```

或者，你可以使用 `??` 字符作为标识符的占位符，您希望这样转义:

```js
var userId = 1;
var columns = ['username', 'email'];
var query = connection.query('SELECT ?? FROM ?? WHERE id = ?', [columns, 'users', userId], function (error, results, fields) {
  if (error) throw error;
  // ...
});

console.log(query.sql); // SELECT `username`, `email` FROM `users` WHERE id = 1
```
**请注意，最后一个字符序列是实验性的，语法可能会改变**

当您将一个对象传递给 `.escape()` 或者 `.query()`, `.escapeId()` 时，这被用来避免对象键中的 SQL 注入。

### 准备查询

您可以使用 `mysql.format` 来准备一个带有多个插入点的查询，利用适当的转义 id 和 值。下面是一个简单的例子:

```js
var sql = "SELECT * FROM ?? WHERE ?? = ?";
var inserts = ['users', 'id', userId];
sql = mysql.format(sql, inserts);
```

这样做之后，您就有了一个有效的、转义的查询，然后您可以安全地将其发送到数据库。
如果您希望在实际将其发送到数据库之前准备好查询，那么这将非常有用。
`mysql.format` 是从 `SqlString.format` 暴露的，你也可以选择（但不是必须的）传入 stringifyObject 和 timezone，允许您提供一种自定义的方法来将对象转换为字符串，以及一个特定位置/时区感知(location-specific/timezone-aware) 的 Date。

### 自定义格式


如果您更喜欢使用其他类型的查询转义格式，则可以使用连接配置选项来定义一个自定义格式函数。如果你想使用内建的 `.escape()` 或任何其他的连接函数，你可以访问连接对象。

这是一个如何实现另一种格式的例子：

```js
connection.config.queryFormat = function (query, values) {
  if (!values) return query;
  return query.replace(/\:(\w+)/g, function (txt, key) {
    if (values.hasOwnProperty(key)) {
      return this.escape(values[key]);
    }
    return txt;
  }.bind(this));
};

connection.query("UPDATE posts SET title = :title", { title: "Hello MySQL" });
```

## 获取插入行的 id

如果您将一行插入到一个带有自动递增主键的表中，您可以像这样检索插入 id:

```js
connection.query('INSERT INTO posts SET ?', {title: 'test'}, function (error, results, fields) {
  if (error) throw error;
  console.log(results.insertId);
});
```

当处理大数字（在 JavaScript 数字精度限制之上）时，您应该考虑启用 `supportBigNumbers` 选项，
该选项能够将插入 ID 读取为一个字符串，否则会引发错误。

从数据库中获取大数字时，也需要此选项，否则由于精度限制，您将得到四舍五入到数百或数千的值。

## 获取受影响的行数

您可以从insert、update 或 delete 语句中获得受影响的行数。

```js
connection.query('DELETE FROM posts WHERE title = "wrong"', function (error, results, fields) {
  if (error) throw error;
  console.log('deleted ' + results.affectedRows + ' rows');
})
```

## 获取被修改的行数

您可以从 update 语句中获取被更改的行数。

`changedRows` 与 `affectedRows` 的不同之处在于，它不计算其值未更改的更新行。

```js
connection.query('UPDATE posts SET ...', function (error, results, fields) {
  if (error) throw error;
  console.log('changed ' + results.changedRows + ' rows');
})
```

## 获取连接 ID

您可以使用 `threadId` 属性获取给定连接的 MySQL 连接ID（"thread ID"）。

```js
connection.connect(function(err) {
  if (err) throw err;
  console.log('connected as id ' + connection.threadId);
});
```

## 并行执行查询

MySQL协议是顺序的，这意味着你需要多个连接来并行执行查询。
您可以使用 Pool 来管理连接，一个简单的方法是为每个传入的 http 请求创建一个连接。

## 流式查询行

有时，您可能希望选择大量的行，并在接收到它们时处理它们。可以这样做:

```js
var query = connection.query('SELECT * FROM posts');
query
  .on('error', function(err) {
    // 处理错误，在这之后会发射一个 `end` 事件
  })
  .on('fields', function(fields) {
    // 为行提供的字段数据包
  })
  .on('result', function(row) {
    // 如果您的处理涉及到 I/O，那么暂停连接是很有用的
    connection.pause();

    processRow(row, function() {
      connection.resume();
    });
  })
  .on('end', function() {
    // 所有的行都被接收了
  });
```

请注意关于上面的例子的一些事情：

* 通常情况下，在开始使用 `pause()` 调节连接之前，您会希望收到一定数量的行。 这个数字将取决于您的行数量和大小。

* `pause()` / `resume()` 操作底层套接字和解析器。 你可以保证在调用 `pause()` 后不会再有 `'result'`  事件被触发。

* 在进行流式查询行时，你**不能**为 `query()` 方法提供回调。

* `'result'` 事件将触发行以及确认 INSERT/UPDATE 查询成功的 OK 数据包。

* 这点为非常重要：不要暂停 result 太长事件，否则可能会遇到错误：`Error: Connection lost: The server closed the connection.`。这个时间限制是由 MySQL 服务器上的 [net_write_timeout setting](https://dev.mysql.com/doc/refman/5.5/en/server-system-variables.html#sysvar_net_write_timeout) 设置决定的。

此外，您可能有兴趣知道目前无法对单个行列进行流式处理，它们将始终被完全缓冲。如果你有一个很好的用例来向 MySQL 流式发送大字段，我很乐意为你提供你的想法和贡献。

### Piping results with Streams

查询对象提供了一个方便的方法 `.stream([options])` 将「查询事件」封装到一个 [可读流](http://nodejs.org/api/stream.html#stream_class_stream_readable) 对象中。
这个数据流可以很容易地被传送（pipe）到下游，并根据下游拥塞和可选的 `highWaterMark` 提供自动 暂停/恢复。
流的 `objectMode` 参数被设置为 `true` 并且不能被更改（如果需要字节流，则需要使用变换流，例如 [objstream](https://www.npmjs.com/package/objstream) ）。

例如，用管道输送查询结果到另一个流（最大缓冲区为5个对象）是简单的：

```js
connection.query('SELECT * FROM posts')
  .stream({highWaterMark: 5})
  .pipe(...);
```

## 多语句查询

出于安全原因，对多个语句的支持是禁用的(如果值没有正确地转义，它允许 SQL 注入攻击)。
要使用这个特性，你必须为你的连接启用它:

```js
var connection = mysql.createConnection({multipleStatements: true});
```

一旦启用，您就可以像其他查询一样执行多个语句查询:

```js
connection.query('SELECT 1; SELECT 2', function (error, results, fields) {
  if (error) throw error;
  // `results` 是一个数组，其中的每一个元素对应查询中的一条语句。
  // 每一个元素又是一个数组
  console.log(results[0]); // [{1: 1}]
  console.log(results[1]); // [{2: 2}]
});
```

>**[info]**
>
> 查询语句:
>
> ```js
> var sql = 'SELECT id, content FROM test WHERE id =3;' +
>           'SELECT id, content FROM test WHERE id =6;'
> connection.query(sql, function (err, results, fields) {
>   console.log(results)
> });
> ```
> 运行结果：
>
> ```
> [ [ RowDataPacket { id: 3, content: 'content for row3' } ],
>   [ RowDataPacket { id: 6, content: 'content for row6' } ] ]
> ```

此外，您还可以对多个语句查询的结果进行流:

```js
var query = connection.query('SELECT 1; SELECT 2');

query
  .on('fields', function(fields, index) {
    // 后面的结果行的字段
  })
  .on('result', function(row, index) {
    // result 是针对每个查询语句的查询的每一行
    // index 指的是这个结果属于(从0开始)的语句。
  });
```

> **[info]**
>
> 查询语句：
>
> ```js
> // 总共 10000 条数据
> var sql = 'SELECT id, content FROM test WHERE id >= 9996;' +
>           'SELECT id, content FROM test WHERE id >= 9996;'
>
> var query = connection.query(sql);
>
> query
>   .on('fields', function(fields, index) {
>     // 后面的结果行的字段
>   })
>   .on('result', function(row, index) {
>     console.log('第 ' + index + ' 查询语句：');
>     console.log(row);
>   });
> ```
> 执行结果：

> ```
> 第 0 查询语句：
> RowDataPacket { id: 9996, content: 'content for row9996' }
> 第 0 查询语句：
> RowDataPacket { id: 9997, content: 'content for row9997' }
> 第 0 查询语句：
> RowDataPacket { id: 9998, content: 'content for row9998' }
> 第 0 查询语句：
> RowDataPacket { id: 9999, content: 'content for row9999' }
> 第 0 查询语句：
> RowDataPacket { id: 10000, content: 'content for row10000' }
> 第 1 查询语句：
> RowDataPacket { id: 9996, content: 'content for row9996' }
> 第 1 查询语句：
> RowDataPacket { id: 9997, content: 'content for row9997' }
> 第 1 查询语句：
> RowDataPacket { id: 9998, content: 'content for row9998' }
> 第 1 查询语句：
> RowDataPacket { id: 9999, content: 'content for row9999' }
> 第 1 查询语句：
> RowDataPacket { id: 10000, content: 'content for row10000' }
> ```

如果查询中的某个语句导致错误，则生成的 Error 对象将包含一个 `err.index` 属性，该属性将告诉您哪个语句导致了该错误。 发生错误时，MySQL 也将停止执行任何剩余的语句。

请注意，用于流式传输多个语句查询的接口是实验性的，我期待着对其进行反馈。

## 存储过程

您可以像任何其他 mysql 驱动程序一样从查询中调用存储过程（stored procedure）。如果存储过程产生多个结果集，那么它们将以与多个语句查询的结果相同的方式显示给您。

## 带有重叠列名的 Joins

在执行 `JOIN` 时，您可能会得到重叠列名称的结果集。

默认情况下，node-mysql 将按照从 MySQL 接收列的顺序重写冲突的列名，导致一些收到的值不可用。

但是，您也可以指定您希望将列嵌套在表名下方，如下所示：

```js
var options = {sql: '...', nestTables: true};
connection.query(options, function (error, results, fields) {
  if (error) throw error;
  /* results will be an array like this now:
  [{
    table1: {
      fieldA: '...',
      fieldB: '...',
    },
    table2: {
      fieldA: '...',
      fieldB: '...',
    },
  }, ...]
  */
});
```

或者使用一个字符串分隔符来将结果合并。

```js
var options = {sql: '...', nestTables: '_'};
connection.query(options, function (error, results, fields) {
  if (error) throw error;
  /* results will be an array like this now:
  [{
    table1_fieldA: '...',
    table1_fieldB: '...',
    table2_fieldA: '...',
    table2_fieldB: '...',
  }, ...]
  */
});
```

## 事务

在连接级别上可以使用简单的事务支持（transaction support）:

```js
connection.beginTransaction(function(err) {
  if (err) { throw err; }
  connection.query('INSERT INTO posts SET title=?', title, function (error, results, fields) {
    if (error) {
      return connection.rollback(function() {
        throw error;
      });
    }

    var log = 'Post ' + results.insertId + ' added';

    connection.query('INSERT INTO log SET data=?', log, function (error, results, fields) {
      if (error) {
        return connection.rollback(function() {
          throw error;
        });
      }
      connection.commit(function(err) {
        if (err) {
          return connection.rollback(function() {
            throw err;
          });
        }
        console.log('success!');
      });
    });
  });
});
```

请注意，`beginTransaction()`，`commit()` 和 `rollback()` 是简单的便利函数，分别执行 `START TRANSACTION`，`COMMIT` 和 `ROLLBACK` 命令。 需要了解的是，MySQL 中的许多命令可以导致隐式提交(commit)，如 [MySQL 文档](http://dev.mysql.com/doc/refman/5.5/en/implicit-commit.html) 中所述。

## Ping

ping 数据包可以使用 `connection.ping` 方法通过连接发送。这个方法会向服务器发送一个 ping 数据包，当服务器响应时，这个回调会被触发。 如果发生错误，回调会触发一个错误参数。

```js
connection.ping(function (err) {
  if (err) throw err;
  console.log('Server responded to ping');
})
```

## 超时

每个操作都有一个可选的不活动超时选项。 这使您可以为操作指定适当的超时。需要注意的是，这些超时不是 MySQL 协议的一部分，而是通过客户端的超时操作。这意味着当超时达到时，发生的连接将被破坏，不能进行进一步的操作。

```js
// 60秒后 kill 查询
connection.query({sql: 'SELECT COUNT(*) AS count FROM big_table', timeout: 60000}, function (error, results, fields) {
  if (error && error.code === 'PROTOCOL_SEQUENCE_TIMEOUT') {
    throw new Error('too long to count table rows!');
  }

  if (error) {
    throw error;
  }

  console.log(results[0].count + ' rows');
});
```

## 错误处理

这个模块带有一个一致的错误处理方法，您应该仔细阅读以编写可靠的应用程序。

这个模块创建的大多数错误都是 JavaScript [Error][] 对象的实例。另外他们通常还有两个额外的属性：

* `err.code`：[MySQL 服务器错误][]（例如 `'ER_ACCESS_DENIED_ERROR'`），Node.js错误（例如 `'ECONNREFUSED'`）或内部错误（例如 `'PROTOCOL_CONNECTION_LOST'`）。
* `err.fatal`：Boolean，指示此错误是否为连接对象的终点。如果错误不是来自 MySQL 协议操作，那么这个不会被定义。
* `err.sql`：String，包含失败查询的完整 SQL。当使用像生成查询的 ORM 这样的更高级别的接口时，这会很有用。
* `err.sqlMessage`：String，包含提供错误文本描述的消息字符串。只从 [MySQL 服务器错误][] 进行填充。


[Error]: https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Error
[MySQL 服务器错误]: http://dev.mysql.com/doc/refman/5.5/en/error-messages-server.html

致命错误传播到*所有*待处理的回调。在下面的示例中，尝试连接到无效的端口会触发致命错误。因此，错误对象被传播到两个悬而未决的回调：

```js
var connection = require('mysql').createConnection({
  port: 84943, // 错误端口
});

connection.connect(function(err) {
  console.log(err.code); // 'ECONNREFUSED'
  console.log(err.fatal); // true
});

connection.query('SELECT 1', function (error, results, fields) {
  console.log(error.code); // 'ECONNREFUSED'
  console.log(error.fatal); // true
});
```

然而，正常的错误只能委托给它们所属的回调。所以在下面的例子中，只有第一个回调收到错误，第二个查询按预期工作：

```js
connection.query('USE name_of_db_that_does_not_exist', function (error, results, fields) {
  console.log(error.code); // 'ER_BAD_DB_ERROR'
});

connection.query('SELECT 1', function (error, results, fields) {
  console.log(error); // null
  console.log(results.length); // 1
});
```

最后但并非最不重要的：如果发生致命错误，并且没有待处理的回调，或者发生没有回调属于它的正常错误，则错误作为连接对象上的 `'error'` 事件被发射。 这在下面的例子中被证明：

```js
connection.on('error', function(err) {
  console.log(err.code); // 'ER_BAD_DB_ERROR'
});

connection.query('USE name_of_db_that_does_not_exist');
```

注意：`'error'` 事件在 node 中是特殊的。 如果它们没有附加的监听器，则会打印一个堆栈跟踪，并且您的进程将被终止。

**tl;dr:** 本模块不希望您处理无声的失败。您应该始终为您的方法调用提供回调。
如果你想忽略这个建议并抑制未处理的错误，你可以这样做：

```js
// I am Chuck Norris:
connection.on('error', function() {});
```

## 异常安全

这个模块是异常安全的。这意味着你可以继续使用它，即使你的回调函数之一会抛出一个你使用 'uncaughtException' 或者一个域来捕获的错误。

## 类型转换

为了方便起见，默认情况下，此驱动程序将把 mysql 类型转换为原生 JavaScript 类型。 存在以下映射：

### Number

* TINYINT
* SMALLINT
* INT
* MEDIUMINT
* YEAR
* FLOAT
* DOUBLE

### Date

* TIMESTAMP
* DATE
* DATETIME

### Buffer

* TINYBLOB
* MEDIUMBLOB
* LONGBLOB
* BLOB
* BINARY
* VARBINARY
* BIT (最后一个字节将使用 0 bits 填充 是有必要的)

### String

**注意** 二进制字符集中的文本作为 `Buffer` 而不是字符串形式返回。

* CHAR
* VARCHAR
* TINYTEXT
* MEDIUMTEXT
* LONGTEXT
* TEXT
* ENUM
* SET
* DECIMAL (可能超过 float 精度)
* BIGINT (可能超过 float 精度)
* TIME (可以映射到 Date，但会设置什么日期？)
* GEOMETRY (从来没有使用过，如果你这样做，请联系)

不建议（可能会在将来消失/更改）禁用类型转换，但是目前您可以在连接上执行此操作：

```js
var connection = require('mysql').createConnection({typeCast: false});
```

或者在查询层面：

```js
var options = {sql: '...', typeCast: false};
var query = connection.query(options, function (error, results, fields) {
  if (error) throw error;
  // ...
});
```

你也可以传递一个函数并处理自己的类型转换。给你一些列信息，如数据库，表和名称，还有类型和长度。
如果您只想将自定义类型转换应用于特定类型，则可以执行此操作，然后回退到默认值。
以下是将 `TINYINT(1)` 转换为布尔值的示例：

```js
connection.query({
  sql: '...',
  typeCast: function (field, next) {
    if (field.type == 'TINY' && field.length == 1) {
      return (field.string() == '1'); // 1 = true, 0 = false
    }
    return next();
  }
});
```

> **[warning] 警告**
>
> 您必须在自定义的 `typeCast` 回调中使用这三个字段函数之一来调用解析器。他们只能被调用一次。（见 [#539](https://github.com/mysqljs/mysql/issues/539) 讨论）

```
field.string()
field.buffer()
field.geometry()
```

他们是下面这些函数的别名：

```
parser.parseLengthCodedString()
parser.parseLengthCodedBuffer()
parser.parseGeometryValue()
```
__您可以找到需要使用的字段函数，查看: [RowDataPacket.prototype._typeCast](https://github.com/mysqljs/mysql/blob/master/lib/protocol/packets/RowDataPacket.js#L41)__


## 连接标志

如果出于任何原因想要更改默认连接标志，则可以使用连接选项 `flags`。
使用逗号分隔的项目列表来传递字符串以添加到默认标志。
如果您不希望使用默认标志，则将该标志加上负号。
要添加一个不在默认列表中的标志，只需写上标志名称，或者用加号（不区分大小写）加前缀。

**请注意，一些不支持的可用标志（例如：Compression）仍然不允许指定。**

### 示例

下一个例子来自默认的连接标志黑名单 FOUND_ROWS 标志。

```js
var connection = mysql.createConnection("mysql://localhost/test?flags=-FOUND_ROWS");
```

### 默认标志

在新连接上默认发送以下标志:

- `CONNECT_WITH_DB` - 能够在连接上指定数据库。
- `FOUND_ROWS` - 发送找到的行，而不是作为 `affectedRows` 的受影响的行。
- `IGNORE_SIGPIPE` - 旧的; 没有作用。
- `IGNORE_SPACE` - 让解析器忽略查询中 `(` 之前的空格。
- `LOCAL_FILES` - 可以使用 `LOAD DATA LOCAL`.
- `LONG_FLAG`
- `LONG_PASSWORD` - 使用旧密码认证的改进版。
- `MULTI_RESULTS` - 可以处理 COM_QUERY 的多个结果集。
- `ODBC` 旧的; 没有作用。
- `PROTOCOL_41` - 使用 4.1 协议。
- `PS_MULTI_RESULTS` - 可以处理 COM_STMT_EXECUTE 的多个结果集。
- `RESERVED` - 4.1 协议的旧标志。
- `SECURE_CONNECTION` - 支持原生的 4.1 身份认证。
- `TRANSACTIONS` - 询问事务状态的标志。

此外，如果选项 `multipleStatements` 被设置为 `true`，则将发送以下标记:

- `MULTI_STATEMENTS` - 客户端可以在每个查询或语句准备时发送多条语句。

### 其他可用标志

还有其他可用的标志。它们可能或可能不具有功能，但仍然可以指定。

- COMPRESS
- INTERACTIVE
- NO_SCHEMA
- PLUGIN_AUTH
- REMEMBER_OPTIONS
- SSL
- SSL_VERIFY_SERVER_CERT

## 调试和报告问题

如果您遇到了问题，有一件事情可能会帮助您，那就是启用连接的 `debug` 模式:

```js
var connection = mysql.createConnection({debug: true});
```

这将在标准输出上打印所有传入和传出的数据包。您还可以通过将一个类型数组传递给调试来限制对数据包类型的调试。

```js
var connection = mysql.createConnection({debug: ['ComQueryPacket', 'RowDataPacket']});
```

限制对查询和数据包的调试。

如果这没有什么帮助，可以自由地打开 GitHub 的 issue。一个好的 GitHub 问题将会有:

* 重现问题所需的最少数量的代码(如果可能的话)
* 尽可能多的调试输出和关于您的环境的信息(mysql 版本、node 版本、操作系统等等)。

## 安全问题

安全问题不应该首先通过 GitHub 或其他公共论坛报告，但保持私密，以便合作者评估报告，并（a）制定修补程序并计划发布日期或（b）声明不是安全 问题（在这种情况下，它可以张贴在公共论坛，如 GitHub 问题）。

主要的私人会谈是电子邮件，无论是给模块的作者发电子邮件或打开一个 GitHub 的问题，只是询问安全问题应该谁来解决，而不透露问题或问题的类型。

一个理想的报告将包括清楚地表明安全问题是什么以及如何利用安全问题，理想的是带有一个概念证明（“PoC”），让合作者再次工作，并验证潜在的修补程序。

## 贡献

This project welcomes contributions from the community. Contributions are
accepted using GitHub pull requests. If you're not familiar with making
GitHub pull requests, please refer to the
[GitHub documentation "Creating a pull request"](https://help.github.com/articles/creating-a-pull-request/).

For a good pull request, we ask you provide the following:

1. Try to include a clear description of your pull request in the description.
   It should include the basic "what" and "why"s for the request.
2. The tests should pass as best as you can. See the [Running tests](#running-tests)
   section on how to run the different tests. GitHub will automatically run
   the tests as well, to act as a safety net.
3. The pull request should include tests for the change. A new feature should
   have tests for the new feature and bug fixes should include a test that fails
   without the corresponding code change and passes after they are applied.
   The command `npm run test-cov` will generate a `coverage/` folder that
   contains HTML pages of the code coverage, to better understand if everything
   you're adding is being tested.
4. If the pull request is a new feature, please be sure to include all
   appropriate documentation additions in the `Readme.md` file as well.
5. To help ensure that your code is similar in style to the existing code,
   run the command `npm run lint` and fix any displayed issues.

## 运行测试

测试套件分为两部分：单元测试和集成测试。单元测试在任何机器上运行，而集成测试需要设置 MySQL 服务器实例。

### Running unit tests

```sh
$ FILTER=unit npm test
```

### 运行集成测试

设置环境变量 `MYSQL_DATABASE`, `MYSQL_HOST`, `MYSQL_PORT`,
`MYSQL_USER` 和 `MYSQL_PASSWORD`。 `MYSQL_SOCKET` 也可以用来代替 `MYSQL_HOST` 和 `MYSQL_PORT` 来通过 UNIX 套接字进行连接。然后运行`npm test`。

例如，如果您在 localhost:3306 上安装了 mysql ，并且没有为 `root` 用户设置密码，请运行：

```sh
$ mysql -u root -e "CREATE DATABASE IF NOT EXISTS node_mysql_test"
$ MYSQL_HOST=localhost MYSQL_PORT=3306 MYSQL_DATABASE=node_mysql_test MYSQL_USER=root MYSQL_PASSWORD= FILTER=integration npm test
```

## Todo

* prepared statements
* 支持 UTF-8 / ASCII 以外的编码

[npm-image]: https://img.shields.io/npm/v/mysql.svg
[npm-url]: https://npmjs.org/package/mysql
[node-version-image]: https://img.shields.io/node/v/mysql.svg
[node-version-url]: https://nodejs.org/en/download/
[travis-image]: https://img.shields.io/travis/mysqljs/mysql/master.svg?label=linux
[travis-url]: https://travis-ci.org/mysqljs/mysql
[appveyor-image]: https://img.shields.io/appveyor/ci/dougwilson/node-mysql/master.svg?label=windows
[appveyor-url]: https://ci.appveyor.com/project/dougwilson/node-mysql
[coveralls-image]: https://img.shields.io/coveralls/mysqljs/mysql/master.svg
[coveralls-url]: https://coveralls.io/r/mysqljs/mysql?branch=master
[downloads-image]: https://img.shields.io/npm/dm/mysql.svg
[downloads-url]: https://npmjs.org/package/mysql
