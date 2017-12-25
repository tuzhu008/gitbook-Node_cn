redis - 一个 node.js redis 客户端
===========================

[![Build Status](https://travis-ci.org/NodeRedis/node_redis.svg?branch=master)](https://travis-ci.org/NodeRedis/node_redis)
[![Coverage Status](https://coveralls.io/repos/NodeRedis/node_redis/badge.svg?branch=)](https://coveralls.io/r/NodeRedis/node_redis?branch=)
[![Windows Tests](https://img.shields.io/appveyor/ci/BridgeAR/node-redis/master.svg?label=Windows%20Tests)](https://ci.appveyor.com/project/BridgeAR/node-redis/branch/master)
[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/NodeRedis/node_redis?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)


这是 node.js 的一个完整且功能丰富的 Redis 客户端。**它支持所有的 Redis 命令**，并专注于高性能。

安装:

    npm install redis

## 用法示例

```js
var redis = require("redis"),
    client = redis.createClient();

// 如果你想选择 database 3，而不是 0（默认），请调用
// client.select(3, function() { /* ... */ });

client.on("error", function (err) {
    console.log("Error " + err);
});

client.set("string key", "string val", redis.print);
client.hset("hash key", "hashtest 1", "some value", redis.print);
client.hset(["hash key", "hashtest 2", "some other value"], redis.print);
client.hkeys("hash key", function (err, replies) {
    console.log(replies.length + " replies:");
    replies.forEach(function (reply, i) {
        console.log("    " + i + ": " + reply);
    });
    client.quit();
});
```

这将显示:

    mjr:~/work/node_redis (master)$ node example.js
    Reply: OK
    Reply: 0
    Reply: 0
    2 replies:
        0: hashtest 1
        1: hashtest 2
    mjr:~/work/node_redis (master)$

请注意，该 API 完全是异步的。要从服务器获取数据，您需要使用一个回调。从 v.2.6 的 API 支持驼峰写法和 snake_case写法，并且所有的选项/变量/事件等都支持。
建议使用驼峰写法，因为这是 node.js 的默认风格。

### Promises

您还可以在 node_redis 中使用 promises，通过 [bluebird](https://github.com/petkaantonov/bluebird) promise化 node_redis:

```js
var redis = require('redis');
bluebird.promisifyAll(redis.RedisClient.prototype);
bluebird.promisifyAll(redis.Multi.prototype);
```

它将为所有的 node_redis 函数添加一个 *Async* (例如 `return client.getAsync().then()`)

```js
// 我们期待一个值 'foo': 'bar' 出现
// 因此不这样写 client.get('foo', cb); 你应该这样写:
return client.getAsync('foo').then(function(res) {
    console.log(res); // => 'bar'
});

// 通过 multi 使用 promise，像这样：

return client.multi().get('foo').execAsync().then(function(res) {
    console.log(res); // => 'bar'
});
```

### 发送命令

每一个 Redis 命令都暴露为 `client` 对象上的一个函数。所有的函数都有一个 `args`数组 和一个可选的 `callback` 函数未做参数，或者是一群可变数量的单个参数，后面跟了一个可选的回调函数。例如：

```js
client.hmset(["key", "test keys 1", "test val 1", "test keys 2", "test val 2"], function (err, res) {});
// 和下面一样：
client.hmset("key", ["test keys 1", "test val 1", "test keys 2", "test val 2"], function (err, res) {});
// 或者
client.hmset("key", "test keys 1", "test val 1", "test keys 2", "test val 2", function (err, res) {});
```

如果数组是可能的(通过 body-parser，查询字符串或其他方法)，就应该使用用户输入，因为单个参数可能会被无意地解释为多个 args。

注意：无论哪种形式，`callback` 都是可选的。

```js
client.set("some key", "some val");
client.set(["some other key", "some val"]);
```

如果丢失了 key，则应答将为空（null）。只有当 [Redis命令引用](http://redis.io/commands)声明其他内容时，它才不会为空。

```js
client.get("missingkey", function(err, reply) {
    // 当密钥丢失时，应答是空的
    console.log(reply);
});
```

对于 Redis 命令列表，请参见 [Redis 命令](http://www.redis.cn/commands.html)。

对响应进行最小的解析。命令返回 一个整数返回 JavaScript  Numbers，数组则返回 JavaScript Array。`HGETALL` 返回一个由哈希键键控的对象。所有的字符串都将作为字符串或缓冲区返回，这取决于您的设置。请注意，发送 null、undefined 和布尔值 将导致被强制转为一个字符串值！

# Redis 命令

这个库是对 [Redis 命令](https://redis.io/commands) 的 1 对 1 的映射。它不是一个缓存库，所以请参考 Redis 命令页，以获得完整的使用细节。

使用 SET 命令设置 key 自动过期的例子
[SET 命令](http://www.redis.cn/commands.html#set)

```js
// 这个 key 将在 10 秒后过期
client.set('key', 'value!', 'EX', 10);
```

# API

## 连接和其他事件

`client` 将会发射一些关于连接到 Redis 服务器的状态的事件。

### "ready"

一旦建立连接，`client` 就会发射 `ready`。在 `ready` 事件之前下达的命令被排队，然后在此事件被发出之前重新播放。_「译者注」：也就是在连接建立之前下达的命令会等待。_

### "connect"

`client` 将在连接到服务器后立即发射 `connect`。

### "reconnecting"

在失去连接后尝试重新连接到 Redis 服务器时，`client` 将会发射 `reconnecting`。监听器被传入一个包含 `delay`（毫秒） 和 `attempt`（尝试次数） 属性的对象。

### "error"

当遇到连接到 Redis 服务器的错误或 node_redis 中出现任何其他错误时，`client` 将会发射 `error`。如果您使用一个没有回调的命令，并且遇到一个 ReplyError，它将被发送给错误监听器。_「译者注」：也就是说，发生的错误未能在回调函数中得到妥善处理的时候就会被抛出，然后被错误监听器捕获。_

因此，请将错误监听器附加到 node_redis。

### "end"

当一个已建立的 Redis服务器 连接已经关闭时，`client` 将会发射 `end`。

### "drain" (deprecated)

当与 Redis 服务器的 TCP 连接被缓冲时，`client` 将会发射 `drain`，但是现在是可写的。该事件可用于将命令「流」到 Redis，并适应反压力。

如果流被缓冲，`client.should_buffer` 是被设置为 `true`的。否则，该变量总是被设为 `false`。这样你就可以决定什么时候减少你的发送率，并且当你获得 `drain`时重新发送命令。

您还可以检查每个命令的返回值，因为它还会返回反压力指示符(**已弃用**)。如果返回 `false`，则流必须缓冲。

### "warning"

当设置密码但是不需要，并且如果使用了一个已弃用的 选项/函数/类似的方法时，`client` 会发射 `warning`。

### "idle" (deprecated)

当没有未完成的命令等待响应时，`client` 将会发出 `idle`。

## redis.createClient()

如果您在同一台机器上运行了 `redis-server` 服务器 和 node，那么默认的端口和主机可能很好，您不需要提供任何参数。`createClient()` 返回一个 `RedisClient` 对象。否则，`createClient()` 接受这些参数:

* `redis.createClient([options])`
* `redis.createClient(unix_socket[, options])`
* `redis.createClient(redis_url[, options])`
* `redis.createClient(port[, host][, options])`

__提示：__ 如果 Redis 服务器在与客户端相同的机器上运行
如果可能的话，可以使用 unix 套接字来增加吞吐量。

#### `options` 对象属性
| 属性  | 默认值   | 描述 |
|-----------|-----------|-------------|
| host      | 127.0.0.1 | Redis 服务器的 IP 地址 |
| port      | 6379      | Redis 服务器的端口 |
| path      | null      | Redis 服务器的 UNIX 套接字字符串 |
| url       | null      | Redis 服务器的 URL。 格式: `[redis:]//[[user][:password@]][host][:port][/db-number][?db=db-number[&password=bar[&option=value]]]` (更多的可用信息在 [IANA](http://www.iana.org/assignments/uri-schemes/prov/redis))。 |
| parser    | javascript | __弃用的__ Use either the built-in JS parser [`javascript`]() or the native [`hiredis`]() parser. __Note__ `node_redis` < 2.6 uses hiredis as default if installed. This changed in v.2.6.0. |
| string_numbers | null | 设置为 `true`, `node_redis` 将返回作为 String 的 Redis 数字值，，而不是 JavaScript Numbers。如果你需要处理一个大量的数字，这是很有用户的 (超过 `Number.MAX_SAFE_INTEGER === 2^53`)。 Hiredis 无法执行此行为，因此将此选项设置为 `true` 将导致内置的 javascript 解析器被使用，无论 `parser` 选项的值如何。|
| return_buffers | false | 如果设置为 `true`，然后，所有的应答都将作为缓冲区（Buffers）而不是字符串（Strings）发送给回调。 |
| detect_buffers | false | 如果设置为 `true`，然后，应答将作为缓冲区被发送给回调。这个选项允许您在每个命令的基础上切换缓冲区和字符串，而 `return_buffers` 适用于客户端上的每个命令。__注意__：这在 pubsub 模式下不能正常工作。订阅者必须总是返回字符串或缓冲区。|
| socket_keepalive | true | 如果设置为 `true`，将启用底层套接字上的 keep-alive 功能|
| no_ready_check | false |  当一个到 Redis 服务器的连接被建立时，服务器可能仍然在从磁盘加载数据库。在加载时，服务器不会响应任何命令。为了解决这个问题，`node_redis` 有一个“就绪检查（ready check）”，它将 `INFO` 命令发送到服务器。`INFO` 命令的响应表明服务器是否已经准备好了更多的命令。当准备就绪时，`node_redis` 会发出一个 `ready` 事件。设置 `no_ready_check` 为 `true` 将检查设置为true将会禁止此检查。 |
| enable_offline_queue |  true | 默认情况下，如果没有与 Redis 服务器的活动连接，则将命令添加到队列中，并在连接建立后执行。将 `enable_offline_queue` 设置为 `false` 将禁用该特性，回调将使用一个错误立即执行，如果没有指定回调，则会发射一个错误。|
| retry_max_delay | null | __弃用的__ _Please use `retry_strategy` instead._ By default, every time the client tries to connect and fails, the reconnection delay almost doubles. This delay normally grows infinitely, but setting `retry_max_delay` limits it to the maximum value provided in milliseconds. |
| connect_timeout | 3600000 | __弃用的__ _Please use `retry_strategy` instead._ Setting `connect_timeout` limits the total time for the client to connect and reconnect. The value is provided in milliseconds and is counted from the moment a new client is created or from the time the connection is lost. The last retry is going to happen exactly at the timeout time. Default is to try connecting until the default system socket timeout has been exceeded and to try reconnecting until 1h has elapsed. |
| max_attempts | 0 | __弃用的__ _Please use `retry_strategy` instead._ By default, a client will try reconnecting until connected. Setting `max_attempts` limits total amount of connection attempts. Setting this to 1 will prevent any reconnect attempt. |
| retry_unfulfilled_commands | false | 如果设置为 `true`，连接丢失时未实现的所有命令将在连接重新建立后重试。如果您使用状态更改命令(例如 `incr`)，请谨慎使用此命令。如果您使用阻塞命令，这尤其有用。|
| password | null | 如果设置，客户端将在连接上研究呢行 Redist 身份认证命令。 别名叫 `auth_pass` __注意__ `node_redis` < 2.5 必须使用 `auth_pass` |
| db | null | 如果设置，客户端将在 连接上运行 Redis `select` 命令。 |
| family | IPv4 | 如果将 `family` 设置为 `'IPv6'` ，将强制使用 IPv6。 关于如何使用 family 类型，请参见 Node.js [net](http://nodejs.cn/api/net.html) 或者 [dns](http://nodejs.cn/api/dns.html) 模块。 |
| disable_resubscribing | false | 如果设置为 `true`，客户在断开连接后不会重新订阅。 |
| rename_commands | null | 传递带有重命名命令的对象来使用，而不是原始的函数。例如，如果您将命令 KEYS 重命名为 "DO-NOT-USE"，那么 rename_commands 对象将是:`{ KEYS : "DO-NOT-USE" }`。有关更多信息，请参阅 [Redis 安全主题](http://redis.io/topics/security)。|
| tls | null | 一个对象，包含传递到 [tls.connect](http://nodejs.org/api/tls.html#tls_tls_connect_port_host_options_callback) 的选项。用来设置到 Redis 的 TLS 连接(例如，如果它被设置为可通过隧道（tunnel）访问)。|
| prefix | null | 一个字符串，被用于所有使用的键的前缀(例如: `namespace:test`)。请注意，`keys` 命令不会被添加前缀。`keys` 命令有一个 "pattern" 作为参数，没有键，如果被添加了前缀，那么就不可能确定 Redis 中现有的键。|
| retry_strategy | function |一个函数，它接收一个选项对象作为参数，这个对象包括重试 `attempt`、`total_retry_time`，说明自上次连接后经过了多少时间、连接丢失的 `error` 和 `times_connected` 数的总和。如果您从该函数返回一个数字，那么重试将精确地发生在这个以毫秒为间隔的时间后。如果您返回一个非数字，则不会发生进一步的重试，所有的脱机命令都会被错误刷新。返回一个错误，将这个特定的错误返回到所有的脱机命令。下面的例子。|

```js
var redis = require("redis");
var client = redis.createClient({detect_buffers: true});

client.set("foo_rand000000000000", "OK");

// This will return a JavaScript String
client.get("foo_rand000000000000", function (err, reply) {
    console.log(reply.toString()); // Will print `OK`
});

// 这将返回一个 Buffer，因为原始的 key 被指定为一个 Buffer
client.get(new Buffer("foo_rand000000000000"), function (err, reply) {
    console.log(reply.toString()); // 将打印 `<Buffer 4f 4b>`
});
client.quit();
```

retry_strategy 示例：

```js
var client = redis.createClient({
    retry_strategy: function (options) {
        if (options.error && options.error.code === 'ECONNREFUSED') {
            // 在一个指定的错误时结束重连，并且使用一个个别的错误冲掉所有命令
            return new Error('The server refused the connection');
        }
        if (options.total_retry_time > 1000 * 60 * 60) {
            // End reconnecting after a specific timeout and flush all commands
            // with a individual error
            // 在一个指定的超时之后结束重连，并且使用一个个别的错误冲掉所有命令
            return new Error('Retry time exhausted');
        }
        if (options.attempt > 10) {
            // 使用内置的错误结束重连
            return undefined;
        }
        // 在经过下面的时间后，进行重连
        return Math.min(options.attempt * 100, 3000);
    }
});
```

## client.auth(password[, callback])


当连接到需要身份验证的 Redis 服务器时，必须将 `AUTH` 命令作为连接后的第一个命令发送。这可能需要与重新连接、就绪检查等进行协调。为了使这个更容易，`client.auth()` 设置 `password` 并在每次连接后发送它，包括重新连接。`callback` 只在对第一个 `AUTH` 命令发出的响应之后才调用一次。注意: 您对 `client.auth()` 的调用不应该在就绪的处理程序中。如果您做错了，客户端会发射一个错误，看起来类似这个:`Error: Ready check failed: ERR operation not permitted`。

## backpressure

### stream

客户端将使用的 [stream](http://nodejs.cn/api/stream.html) 暴露在 `client.stream`中，如果流或客户端必须 [buffer](http://nodejs.cn/api/stream.html#stream_writable_write_chunk_encoding_callback_1) 客户端的命令到 `client.should_buffer` 中。结合这一点，可以在发送命令之前检查缓冲区状态，并侦听流的 `drain` 事件，从而实现反压力(backpressure)。

## client.quit()

这会将退出命令发送到 redis 服务器，并在被正确处理的所有运行的命令之后以干净的方式结束。如果这是在重新连接时调用的(因此不存在与 redis 服务器的连接)，它将立即终止连接，而不是导致进一步的重新连接！在这种情况下，所有的离线命令都将被一个错误所刷新。

## client.end(flush)

强行关闭与 Redis 服务器的连接。注意，这不会等到所有的应答都被解析后才执行。如果您想要干净地退出，请调用`client.quit()`，如上所述。

如果您不完全确定您不关心其他命令，那么您应该将 `flush` 设置为 `true`。如果您将 `flush` 设置为 `false`，所有仍然运行的命令将会无声地失败。

这个例子在读取应答之前关闭了与 Redis 服务器的连接。你可能不想这样做:

```js
var redis = require("redis"),
    client = redis.createClient();

client.set("foo_rand000000000000", "some fantastic value", function (err, reply) {
    // 这将导致一个错误 (flush 参数设置为 true)
    // 或则将会无声地失败并且这个回调不会被调用(flush 设置为 false)
    console.log(err);
});
client.end(true); // 没有进一步的命令被执行
client.get("foo_rand000000000000", function (err, reply) {
    console.log(err); // => 'The connection has already been closed.'
});
```

`client.end()` 不将 `flush`参数设置为 `true`，就**不应该**在生产中使用！

## Error handling (>= v.2.6)

当前存在下列错误子类：

* `RedisError`: 被客户端返回的 _所有错误_
* `ReplyError` 是 `RedisError` 的子类: 由 __Redis__ 自身返回的所有错误
* `AbortError` 是 `RedisError` 的子类: 因为有什么原因，所有的命令都无法完成
* `ParserError` 是 `RedisError` 的子类: 在解析器错误时被返回(这种情况本不应该发生)
* `AggregateError` 是 `AbortError` 的子类: 在调试模式下，多个没有回调函数的未解决的命令会被拒绝，`AggregateError`错误被发射，以防大量的 `AbortError`。

所有的错误类都是由模块导出的。

示例:
```js
var redis = require('./');
var assert = require('assert');
var client = redis.createClient();

client.on('error', function (err) {
    assert(err instanceof Error);
    assert(err instanceof redis.AbortError);
    assert(err instanceof redis.AggregateError);
    // The set and get get aggregated in here
    assert.strictEqual(err.errors.length, 2);
    assert.strictEqual(err.code, 'NR_CLOSED');
});
client.set('foo', 123, 'bar', function (err, res) { // Too many arguments
    assert(err instanceof redis.ReplyError); // => true
    assert.strictEqual(err.command, 'SET');
    assert.deepStrictEqual(err.args, ['foo', 123, 'bar']);

    redis.debug_mode = true;
    client.set('foo', 'bar');
    client.get('foo');
    process.nextTick(function () {
        // Force closing the connection while the command did not yet return
        client.end(true);
        redis.debug_mode = false;
    });
});

```

每个 `ReplyError` 中的 `command` 名都是大写的，并将其包含在参数(`args`)中。

如果 node_redis 因为另一个错误而发射一个库错误，那么「触发错误」是作为 `origin` 属性被添加到返回的错误中。

___错误代码___

如果客户端连接失败，node_redis 返回一个 `NR_CLOSED` 的错误代码。如果一个命令未解决的命令被拒绝，则返回一个 `UNCERTAIN_STATE` 的代码。如果 node_redis 放弃了重新连接，则使用一个 `CONNECTION_BROKEN` 的错误代码。

## client.unref()

在 Redis 服务器的底层套接字连接上调用 `unref()`，允许程序在没有更多命令被挂起的情况下退出。

这是一个**实验性的**特性，并且只支持 Redis 协议的一个子集。任何在 Redis 服务器上保存客户端状态的命令，例如 `*SUBSCRIBE` 或阻塞的 `BL*` 命令都*不能*与 `.unref()` 一起工作。

```js
var redis = require("redis")
var client = redis.createClient()

/*
    调用 unref() 将允许该程序在 get 命令完成后立即退出。
    否则，只要客户端-服务器连接还活着，客户端就会挂起。
*/
client.unref()
client.get("foo", function (err, value){
    if (err) throw(err)
    console.log(value)
})
```

## 友好的哈希命令

大多数 Redis 命令都使用单个字符串或字符串数组作为参数，应答被作为单个字符串或字符串数组被发回。在处理哈希值时，有几个有用的例外。

### client.hgetall(hash, callback)

来自 `HGETALL` 命令的应答将会被 `node_redis` 转换为一个 JavaScript 对象。通过这种方式，您可以使用 JavaScript 语法与响应进行交互。

示例:

```js
client.hmset("hosts", "mjr", "1", "another", "23", "home", "1234");
client.hgetall("hosts", function (err, obj) {
    console.dir(obj);
});
```

输出:

```js
{ mjr: '1', another: '23', home: '1234' }
```

### client.hmset(hash, obj[, callback])

一个哈希中的多个值可以通过提供一个对象来设置:

```js
client.HMSET(key2, {
    "0123456789": "abcdefghij", // 注意: key and value 将被强制转为字符串
    "some manner of key": "a type of value"
});
```

这个对象的属性和值将在 Redis 散列中被设置为键和值。

### client.hmset(hash, key1, val1, ... keyn, valn, [callback])

还可以通过提供一个列表来设置多个值:

```js
client.HMSET(key1, "0123456789", "abcdefghij", "some manner of key", "a type of value");
```

## 发布 / 订阅

发布/订阅(publish / subscribe) API 的例子。该程序打开两个客户端连接，订阅其中一个通道，并发布到另一个通道上:

```js
var redis = require("redis");
var sub = redis.createClient(), pub = redis.createClient();
var msg_count = 0;

sub.on("subscribe", function (channel, count) {
    pub.publish("a nice channel", "I am sending a message.");
    pub.publish("a nice channel", "I am sending a second message.");
    pub.publish("a nice channel", "I am sending my last message.");
});

sub.on("message", function (channel, message) {
    console.log("sub channel " + channel + ": " + message);
    msg_count += 1;
    if (msg_count === 3) {
        sub.unsubscribe();
        sub.quit();
        pub.quit();
    }
});

sub.subscribe("a nice channel");
```

当客户机发出 `SUBSCRIBE` 或 `PSUBSCRIBE` 时，该连接将被放入“订阅者（subscriber）”模式。在这一点上，只有修改订阅集的命令是有效的并退出(并且依赖于 redis 版本 ping)。当订阅集为空时，连接将被放回常规模式。

如果您需要在订阅模式下向 Redis 发送常规命令，只需打开另一个与新客户机的连接(提示:使用 `client.duplicate()`)。

## 订阅者事件

如果客户端有订阅活动，它可能会发出这些事件:

### "message" (channel, message)

客户端将为收到的每一条与活动订阅相匹配的消息发射 `message`事件。通道名称作为 `channel`，消息作为 `message`  被传递到监听器。

### "pmessage" (pattern, channel, message)

客户端将为收到的每一条与活动订阅模式相匹配的消息发射  `pmessage` 事件。与`PSUBSCRIBE`一起使用的原始模式将作为 `pattern`，发送信息的通道名称作为 `channel`，信息作为 `message` 被传递给监听器。

### "message_buffer" (channel, message)

这与带有异常的 `message` 事件相同，它总是会发射一个缓冲区。如果您在监听 `message_buffer` 的同时监听 `message`，它总是会发射一个字符串。

### "pmessage_buffer" (pattern, channel, message)

这与带有异常的 `pmessage` 事件相同，它总是会发射一个缓冲区。如果您在监听 `pmessage_buffer` 的同时监听 `message`，它总是会发射一个字符串。

### "subscribe" (channel, count)

客户端将会响应 `SUBSCRIBE` 命令时发射 `subscribe` 事件。通道名称作为 `channel`，并将此客户端的新订阅计数作为 `count` 传递给监听器。

### "psubscribe" (pattern, count)

客户端将会在响应 `PSUBSCRIBE` 命令时发射 `psubscribe`事件。原始的模式作为 `pattern`，并将此客户端的新订阅计数作为 `count` 传递给监听器。

### "unsubscribe" (channel, count)

客户端将在响应 `UNSUBSCRIBE` 命令时发射 `unsubscribe` 事件。通道名称作为 `channel`，并将此客户端的新订阅计数作为 `count` 被传递给监听器。当 `count` 为 0 时，该客户端已经离开了订阅者模式，并且不再会发射订阅者事件。

### "punsubscribe" (pattern, count)

客户端将在响应 `PUNSUBSCRIBE`  命令时发射 `punsubscribe` 事件。原始的模式作为 `pattern`，并将此客户端的新订阅计数作为 `count` 传递给监听器。当 `count` 为 0 时，该客户端已经离开了订阅者模式，并且不再会发射订阅者事件。


## client.multi([commands])

`MULTI` 命令排队等待，直到 `EXEC` 被下达，然后所有的命令由 Redis 在 原子地（atomically）运行。`node_redis` 中的这个接口是通过调用 `client.multi()` 返回的一个单独的 `Multi` 对象。如果任何命令都不能执行队列，那么所有命令都会被回滚，并且不会执行任何操作(关于特性的信息请参见[事务（transactions）](http://www.redis.cn/topics/transactions))。

```js
var redis  = require("./index"),
    client = redis.createClient(), set_size = 20;

client.sadd("bigset", "a member");
client.sadd("bigset", "another member");

while (set_size > 0) {
    client.sadd("bigset", "member " + set_size);
    set_size -= 1;
}

// 带一个个别回调的 multi 链
client.multi()
    .scard("bigset")
    .smembers("bigset")
    .keys("*", function (err, replies) {
        // 注意: 这个回调中的代码不是原子的（atomic）
        // 这只发生在 .exec 执行调用完成之后。
        client.mget(replies, redis.print);
    })
    .dbsize()
    .exec(function (err, replies) {
        console.log("MULTI got " + replies.length + " replies");
        replies.forEach(function (reply, index) {
            console.log("Reply " + index + ": " + reply.toString());
        });
    });
```

### Multi.exec([callback])

`client.multi()` 是一个返回一个 `Multi` 对象的构造函数。`Multi` 对象与 `client` 对象共享所有相同的命令方法。在 `Multi`对象中，命令被排队等候直到 `Multi.exec()` 被调用。

如果您的代码包含一个语法错误，那么将会抛出一个 `EXECABORT` 错误，所有的命令都将被中止。那个错误包含一个 `.errors` 属性，该属性包含具体的错误。如果所有命令都成功地排队，并且在「正在处理结果数组中的命令」中返回了错误，redis 会抛出一个错误！除了 `onces` 失败之外，没有其他命令会被中止。

您可以将 `MULTI` 命令链式组合在一起，像上面的示例中，或者您可以在仍然发送常规客户端命令的时对单个命令进行排队，如下所示：

```js
var redis  = require("redis"),
    client = redis.createClient(), multi;

// 启动一个单独的 multi 命令队列
multi = client.multi();
multi.incr("incr thing", redis.print);
multi.incr("incr other thing", redis.print);

// 立即运行
client.mset("incr thing", 100, "incr other thing", 1, redis.print);

// 洩流（drain） multi 队列，并以原子的方式（atomically）运行
multi.exec(function (err, replies) {
    console.log(replies); // 101, 2
});
```

除了单独地向 `MULTI` 队列添加命令之外，还可以向构造函数传递一个命令和参数数组:

```js
var redis  = require("redis"),
    client = redis.createClient();

client.multi([
    ["mget", "multifoo", "multibar", redis.print],
    ["incr", "multifoo"],
    ["incr", "multibar"]
]).exec(function (err, replies) {
    console.log(replies);
});
```

### Multi.exec_atomic([callback])

与 Multi.exec 相同，但是执行单个命令的区别将不会使用事务([transactions](http://www.redis.cn/topics/transactions))。

## client.batch([commands])

与 `.multi` 相同，但不使用事务。如果您希望同时执行多个命令，但不需要依赖事务，那么建议您这样做。

`BATCH` 命令被排队，直到 `EXEC` 被下达，然后所有的命令都由 Redis 原子地（atomically）运行。`node_redis` 中的这个接口是通过调用 `client.batch()` 来返回一个单独的 `Batch` 对象。`.batch` 与 `.multi` 唯一的区别是没有事务将被使用。请注意，错误是——就像在 multi 语句中一样——在结果中。否则，错误和结果都可以同时返回。

如果您同时触发多个命令，与在循环中使用相同的命令相比，这将大大提高执行速度，这不需要等待结果！查看特性比较的[基准](http://www.redis.cn/topics/benchmarks.html)。请记住，所有的命令都保存在内存中，直到它们被触发。

## 监控模式

Redis支持 `MONITOR` 命令，这让您可以在所有客户端连接中看到 Redis 服务器接收到的所有命令，包括来自其他客户端库和其他计算机。

连接到服务器的任何客户端（包括监控客户端本身）发出的每个命令，都会发射一个 `monitor` 事件。`monitor` 事件的回调从 Redis 服务器获取时间戳，一个命令数组参数和原始监控字符串。

示例:

```js
var client  = require("redis").createClient();
client.monitor(function (err, res) {
    console.log("Entering monitoring mode.");
});
client.set('foo', 'bar');

client.on("monitor", function (time, args, raw_reply) {
    console.log(time + ": " + args); // 1458910076.446514:['set', 'foo', 'bar']
});
```

# 额外的

还有一些你可能想知道的事情。

## client.server_info

在就绪探测（ready probe）完成之后，·`INFO` 命令的结果将保存在 `client.server_info` 对象中。

`versions` 键包含版本字符串的元素数组，以便进行比较。

```
> client.server_info.redis_version
'2.3.0'
> client.server_info.versions
[ 2, 3, 0 ]
```

## redis.print()

一个方便的回调函数，用于在测试时显示返回值。例子:

```js
var redis = require("redis"),
    client = redis.createClient();

client.on("connect", function () {
    client.set("foo_rand000000000000", "some fantastic value", redis.print);
    client.get("foo_rand000000000000", redis.print);
});
```

这将输出:

```
Reply: OK
Reply: some fantastic value
```

注意，这个程序不会干净地退出，因为客户端仍然是连接的。


## Multi-word commands

要执行 redis 多字(multi-word)命令，如 `SCRIPT LOAD` 或 `CLIENT LIST`，将第二个单词作为第一个参数传递:

```js
client.script('load', 'return 1');
client.multi().script('load', 'return 1').exec(...);
client.multi([['script', 'load', 'return 1']]).exec(...);
```

## client.duplicate([options][, callback])

复制所有当前选项并返回一个新的 redisClient 实例。传递给 `duplicate` 函数的所有选项都将替换原来的选项。如果您传递了一个回调，`duplicate` 将等待客户端准备好并在回调中返回它。如果同时发生错误，则会直接返回一个错误，而不是在回调中。

使用 `duplicate()` 的一个例子是适应连接阻塞的redis命令BRPOP、BLPOP和BRPOPLPUSH。如果这些命令在与非阻塞命令相同的redisClient实例上使用，则非阻塞的命令可能会排队直到阻塞的命令结束。

一个例子是，当使用 `duplicate()` 时，可以使用连接阻塞的 redis 命令 `BRPOP`、`BLPOP` 和 `BRPOPLPUSH`。如果这些命令作为非阻塞命令被用于相同的 redisClient 实例，则非阻塞的命令可能会排队直到阻塞的命令结束。

```js
var Redis=require('redis');
var client = Redis.createClient();
var clientBlocking = client.duplicate();

var get = function() {
    console.log("get called");
    client.get("any_key",function() { console.log("get returned"); });
    setTimeout( get, 1000 );
};
var brpop = function() {
    console.log("brpop called");
    clientBlocking.brpop("nonexistent", 5, function() {
        console.log("brpop return");
        setTimeout( brpop, 1000 );
    });
};
get();
brpop();
```

使用 `duplicate()` 的另一个原因是，当通过 redis `SELECT` 命令访问同一个服务器上的多个 DBs 时。每个 DB 都可以使用它自己的连接。

## client.send_command(command_name[, [args][, callback]])

所有的 Redis 命令都被添加到 `client` 对象中。但是，如果在这个库更新之前引入了新的命令，或者如果您想要添加单独的命令，那么可以使用 `send_command()` 向 Redis 发送任意命令。

所有命令都是作为多批量(multi-bulk)命令发送的。`args` 可以是一组参数，也可以是 undefine（省略或者被设置为）。

## client.add_command(command_name)

调用 add_command 将向原型添加一个新的命令。在使用这个新命令调用时，将使用精确的命令名。可以像其他任何命令一样，可以使用任意参数。

## client.connected

布尔值，跟踪连接到 Redis 服务器的连接状态。

## client.command_queue_length

已经发送到 Redis 服务器，但还未应答的命令的数量。您可以使用此命令在已连接时对命令执行某种最大队列深度。

## client.offline_queue_length

为一个未来的连接而排队的命令的数量。您可以使用它来为预连接命令强制执行某种最大队列深度。

### 带有可选和关键字参数的命令


这适用于任何 [redis.io/commands](http://redis.io/commands) 文档中使用可选的 `[WITHSCORES]` 或`[LIMIT offset count]` 的东西。

示例:

```js
var args = [ 'myzset', 1, 'one', 2, 'two', 3, 'three', 99, 'ninety-nine' ];
client.zadd(args, function (err, response) {
    if (err) throw err;
    console.log('added '+response+' items.');

    // 负无穷 和 正无穷也能工作
    var args1 = [ 'myzset', '+inf', '-inf' ];
    client.zrevrangebyscore(args1, function (err, response) {
        if (err) throw err;
        console.log('example1', response);
        // write your code here
    });

    var max = 3, min = 1, offset = 1, count = 2;
    var args2 = [ 'myzset', max, min, 'WITHSCORES', 'LIMIT', offset, count ];
    client.zrevrangebyscore(args2, function (err, response) {
        if (err) throw err;
        console.log('example2', response);
        // write your code here
    });
});
```

## 性能

花费了大量的精力使 `node_redis` 尽可能快地进行普通操作。

```
Lenovo T450s, i7-5600U and 12gb memory
clients: 1, NodeJS: 6.2.0, Redis: 3.2.0, parser: javascript, connected by: tcp
         PING,         1/1 avg/max:   0.02/  5.26 2501ms total,   46916 ops/sec
         PING,  batch 50/1 avg/max:   0.06/  4.35 2501ms total,  755178 ops/sec
   SET 4B str,         1/1 avg/max:   0.02/  4.75 2501ms total,   40856 ops/sec
   SET 4B str,  batch 50/1 avg/max:   0.11/  1.51 2501ms total,  432727 ops/sec
   SET 4B buf,         1/1 avg/max:   0.05/  2.76 2501ms total,   20659 ops/sec
   SET 4B buf,  batch 50/1 avg/max:   0.25/  1.76 2501ms total,  194962 ops/sec
   GET 4B str,         1/1 avg/max:   0.02/  1.55 2501ms total,   45156 ops/sec
   GET 4B str,  batch 50/1 avg/max:   0.09/  3.15 2501ms total,  524110 ops/sec
   GET 4B buf,         1/1 avg/max:   0.02/  3.07 2501ms total,   44563 ops/sec
   GET 4B buf,  batch 50/1 avg/max:   0.10/  3.18 2501ms total,  473171 ops/sec
 SET 4KiB str,         1/1 avg/max:   0.03/  1.54 2501ms total,   32627 ops/sec
 SET 4KiB str,  batch 50/1 avg/max:   0.34/  1.89 2501ms total,  146861 ops/sec
 SET 4KiB buf,         1/1 avg/max:   0.05/  2.85 2501ms total,   20688 ops/sec
 SET 4KiB buf,  batch 50/1 avg/max:   0.36/  1.83 2501ms total,  138165 ops/sec
 GET 4KiB str,         1/1 avg/max:   0.02/  1.37 2501ms total,   39389 ops/sec
 GET 4KiB str,  batch 50/1 avg/max:   0.24/  1.81 2501ms total,  208157 ops/sec
 GET 4KiB buf,         1/1 avg/max:   0.02/  2.63 2501ms total,   39918 ops/sec
 GET 4KiB buf,  batch 50/1 avg/max:   0.31/  8.56 2501ms total,  161575 ops/sec
         INCR,         1/1 avg/max:   0.02/  4.69 2501ms total,   45685 ops/sec
         INCR,  batch 50/1 avg/max:   0.09/  3.06 2501ms total,  539964 ops/sec
        LPUSH,         1/1 avg/max:   0.02/  3.04 2501ms total,   41253 ops/sec
        LPUSH,  batch 50/1 avg/max:   0.12/  1.94 2501ms total,  425090 ops/sec
    LRANGE 10,         1/1 avg/max:   0.02/  2.28 2501ms total,   39850 ops/sec
    LRANGE 10,  batch 50/1 avg/max:   0.25/  1.85 2501ms total,  194302 ops/sec
   LRANGE 100,         1/1 avg/max:   0.05/  2.93 2501ms total,   21026 ops/sec
   LRANGE 100,  batch 50/1 avg/max:   1.52/  2.89 2501ms total,   32767 ops/sec
 SET 4MiB str,         1/1 avg/max:   5.16/ 15.55 2502ms total,     193 ops/sec
 SET 4MiB str,  batch 20/1 avg/max:  89.73/ 99.96 2513ms total,     223 ops/sec
 SET 4MiB buf,         1/1 avg/max:   2.23/  8.35 2501ms total,     446 ops/sec
 SET 4MiB buf,  batch 20/1 avg/max:  41.47/ 50.91 2530ms total,     482 ops/sec
 GET 4MiB str,         1/1 avg/max:   2.79/ 10.91 2502ms total,     358 ops/sec
 GET 4MiB str,  batch 20/1 avg/max: 101.61/118.11 2541ms total,     197 ops/sec
 GET 4MiB buf,         1/1 avg/max:   2.32/ 14.93 2502ms total,     430 ops/sec
 GET 4MiB buf,  batch 20/1 avg/max:  65.01/ 84.72 2536ms total,     308 ops/sec
 ```

## 调试

为了获得调试输出，您可以使用 `NODE_DEBUG=redis` 运行你的 `node_redis` 应用程序。

这也会导致好的堆栈跟踪，而不是无用的堆栈追踪，否则对于任何异步操作都是如此。如果您只想拥有好的堆栈追踪，而不是在开发模式下调试输出运行您的应用程序(`NODE_ENV=development`)。

好的堆栈跟踪只在开发和调试模式中被激活，因为这将导致严重的性能损失。

___比较___:
无用的堆栈追踪:
```
ReplyError: ERR wrong number of arguments for 'set' command
    at parseError (/home/ruben/repos/redis/node_modules/redis-parser/lib/parser.js:158:12)
    at parseType (/home/ruben/repos/redis/node_modules/redis-parser/lib/parser.js:219:14)
```
好的堆栈追踪:
```
ReplyError: ERR wrong number of arguments for 'set' command
    at new Command (/home/ruben/repos/redis/lib/command.js:9:902)
    at RedisClient.set (/home/ruben/repos/redis/lib/commands.js:9:3238)
    at Context.<anonymous> (/home/ruben/repos/redis/test/good_stacks.spec.js:20:20)
    at callFnAsync (/home/ruben/repos/redis/node_modules/mocha/lib/runnable.js:349:8)
    at Test.Runnable.run (/home/ruben/repos/redis/node_modules/mocha/lib/runnable.js:301:7)
    at Runner.runTest (/home/ruben/repos/redis/node_modules/mocha/lib/runner.js:422:10)
    at /home/ruben/repos/redis/node_modules/mocha/lib/runner.js:528:12
    at next (/home/ruben/repos/redis/node_modules/mocha/lib/runner.js:342:14)
    at /home/ruben/repos/redis/node_modules/mocha/lib/runner.js:352:7
    at next (/home/ruben/repos/redis/node_modules/mocha/lib/runner.js:284:14)
    at Immediate._onImmediate (/home/ruben/repos/redis/node_modules/mocha/lib/runner.js:320:5)
    at processImmediate [as _immediateCallback] (timers.js:383:17)
```

## 如何贡献
- 打开一个 pull请求或一个关于您想要实现/变更的问题。我们很高兴得到任何帮助！
 - 请注意，我们只接受经过充分测试的代码。
## 贡献

node_redis 的原始作者是 [Matthew Ranney](https://github.com/mranney)

当前的主要维护人员是 [Ruben Bridgewater](https://github.com/BridgeAR)

Many [others](https://github.com/NodeRedis/node_redis/graphs/contributors)
contributed to `node_redis` too. Thanks to all of them!

## License

[MIT](LICENSE)

### Consolidation: It's time for celebration

Right now there are two great redis clients around and both have some advantages
above each other. We speak about ioredis and node_redis. So after talking to
each other about how we could improve in working together we (that is @luin and
@BridgeAR) decided to work towards a single library on the long run. But step by
step.

First of all, we want to split small parts of our libraries into others so that
we're both able to use the same code. Those libraries are going to be maintained
under the NodeRedis organization. This is going to reduce the maintenance
overhead, allows others to use the very same code, if they need it and it's way
easyer for others to contribute to both libraries.

We're very happy about this step towards working together as we both want to
give you the best redis experience possible.

If you want to join our cause by help maintaining something, please don't
hesitate to contact either one of us.
