
## 内容列表

- [IO](#io)
  - [io.protocol](#ioprotocol)
  - [io([url][, options])](#iourl-options)
    - [初始化的例子](#initialization-examples)
      - [With multiplexing](#with-multiplexing)
      - [With custom path](#with-custom-path)
      - [With query parameters](#with-query-parameters)
      - [With query option](#with-query-option)
      - [With extraHeaders](#with-extraheaders)
      - [With websocket transport only](#with-websocket-transport-only)
      - [With a custom parser](#with-a-custom-parser)
  - [类: io.Manager](#manager)
    - [new Manager(url[, options])](#new-managerurl-options)
    - [manager.reconnection([value])](#managerreconnectionvalue)
    - [manager.reconnectionAttempts([value])](#managerreconnectionattemptsvalue)
    - [manager.reconnectionDelay([value])](#managerreconnectiondelayvalue)
    - [manager.reconnectionDelayMax([value])](#managerreconnectiondelaymaxvalue)
    - [manager.timeout([value])](#managertimeoutvalue)
    - [manager.open([callback])](#manageropencallback)
    - [manager.connect([callback])](#managerconnectcallback)
    - [manager.socket(nsp, options)](#managersocketnsp-options)
    - [事件: 'connect_error'](#event-connect_error)
    - [事件: 'connect_timeout'](#event-connect_timeout)
    - [事件: 'reconnect'](#event-reconnect)
    - [事件: 'reconnect_attempt'](#event-reconnect_attempt)
    - [事件: 'reconnecting'](#event-reconnecting)
    - [事件: 'reconnect_error'](#event-reconnect_error)
    - [事件: 'reconnect_failed'](#event-reconnect_failed)
    - [事件: 'ping'](#event-ping)
    - [事件: 'pong'](#event-pong)
  - [类: io.Socket](#socket)
    - [socket.id](#socketid)
    - [socket.open()](#socketopen)
    - [socket.connect()](#socketconnect)
    - [socket.send([...args][, ack])](#socketsendargs-ack)
    - [socket.emit(eventName[, ...args][, ack])](#socketemiteventname-args-ack)
    - [socket.on(eventName, callback)](#socketoneventname-callback)
    - [socket.compress(value)](#socketcompressvalue)
    - [socket.close()](#socketclose)
    - [socket.disconnect()](#socketdisconnect)
    - [事件: 'connect'](#event-connect)
    - [事件: 'connect_error'](#event-connect_error-1)
    - [事件: 'connect_timeout'](#event-connect_timeout-1)
    - [事件: 'error'](#event-error)
    - [事件: 'disconnect'](#event-disconnect)
    - [事件: 'reconnect'](#event-reconnect-1)
    - [事件: 'reconnect_attempt'](#event-reconnect_attempt-1)
    - [事件: 'reconnecting'](#event-reconnecting-1)
    - [事件: 'reconnect_error'](#event-reconnect_error-1)
    - [事件: 'reconnect_failed'](#event-reconnect_failed-1)
    - [事件: 'ping'](#event-ping-1)
    - [事件: 'pong'](#event-pong-1)


### IO

作为 `io` 命名空间独立的构建被暴露，或调用 `require('socket.io-client')` 的结果。

```html
<script src="/socket.io/socket.io.js"></script>
<script>
  const socket = io('http://localhost');
</script>
```

```js
const io = require('socket.io-client');
// 或者使用 import 语法
import io from 'socket.io-client';
```

#### io.protocol

  * _(Number)_

协议的修订号。

#### io([url][, options])

  - `url` _(String)_ (默认为 `window.location`)
  - `options` _(Object)_
    - `forceNew` _(Boolean)_ 是否重用现有连接
  - **返回值** `Socket`

  为给定的 URL 创建一个新的 `Manager`，并尝试重用现有的 `Manager` 来进行后续调用，除非 `multiplex` 选项被使用 `false` 传递，通过这一选项相当于传递 `'force new connection': true` 或 `forceNew: true`.

  一个新的 `Socket` 实例返回到 URL 中路径名指定的命名空间，默认为 `/`。例如，如果 `url` 是 `http://localhost/users`，则将建立一个传输连接到 `http://localhost` 并且将建立一个到 `/users` 的 Socket.IO 连接。

  可以通过 `query` 选项或直接在 url (`http://localhost/users?token=abc`) 中提供查询参数。

  请参阅 [new Manager(url[, options])](#new-managerurl-options) 以获得可用的 `options`。

#### 初始化的例子 {#initialization-examples}

##### With multiplexing

默认情况下，在连接到不同的名称空间时使用一个单一的连接(以最小化资源):

```js
const socket = io();
const adminSocket = io('/admin');
// 一个单一的 connection 将被建立
```

使用 `forceNew` 选项可以禁用这个行为：

```js
const socket = io();
const adminSocket = io('/admin', { forceNew: true });
// 将创建两个不同的连接
```

注意: 重用相同的名称空间还将创建两个连接

```js
const socket = io();
const socket2 = io();
// will also create two distinct connections
```

##### With custom `path`

```js
const socket = io('http://localhost', {
  path: '/myownpath'
});

// server-side
const io = require('socket.io')({
  path: '/myownpath'
});
```

请求 URL 看起来像这样： `localhost/myownpath/?EIO=3&transport=polling&sid=<id>`

```js
const socket = io('http://localhost/admin', {
  path: '/mypath'
});
```

这里，socket 使用自定义的路径 `mypath` 连接到 `admin` 名称空间，。

请求 URL 看起来像： `localhost/mypath/?EIO=3&transport=polling&sid=<id>` (名称空间作为有效负载的一部分发送).

##### With query parameters

```js
const socket = io('http://localhost?token=abc');

// 服务器端
const io = require('socket.io')();

// 中间件
io.use((socket, next) => {
  let token = socket.handshake.query.token;
  if (isValid(token)) {
    return next();
  }
  return next(new Error('authentication error'));
});

// 然后
io.on('connection', (socket) => {
  let token = socket.handshake.query.token;
  // ...
});
```

##### With query option

```js
const socket = io({
  query: {
    token: 'cde'
  }
});
```

查询内容也可以在重新连接上进行更新:

```js
socket.on('reconnect_attempt', () => {
  socket.io.opts.query = {
    token: 'fgh'
  }
});
```

##### With `extraHeaders`


只有在启用 `polling` 传输时才会起作用(这是默认值)。当使用 `websocket` 作为传输时，不会附加自定义头部（headers）。这是因为 WebSocket 握手不遵循自定义的头信息。(关于背景，请查看[WebSocket protocol RFC](https://tools.ietf.org/html/rfc6455#section-4))

```js
const socket = io({
  transportOptions: {
    polling: {
      extraHeaders: {
        'x-clientid': 'abc'
      }
    }
  }
});

// 服务器端
const io = require('socket.io')();

// 中间件
io.use((socket, next) => {
  let clientId = socket.handshake.headers['x-clientid'];
  if (isValid(clientId)) {
    return next();
  }
  return next(new Error('authentication error'));
});
```

##### With `websocket` transport only

默认情况下，先建立一个长轮询连接，然后升级到“更好”的传输(如 WebSocket)。如果你喜欢处在危险之中，这部分可以跳过:

```js
const socket = io({
  transports: ['websocket']
});

// 在重新连接时，重置传输选项, 由于 Websocket 连接可能失败(由代理、防火墙、浏览器等引起)
socket.on('reconnect_attempt', () => {
  socket.io.opts.transports = ['polling', 'websocket'];
});
```

##### With a custom parser


默认的 [parser](https://github.com/socketio/socket.io-parser) 以牺牲性能为代价来促进兼容性(支持 `Blob`、`File`、二进制检查)。可以提供一个定制的解析器来匹配应用程序的需求。请看[这里]((https://github.com/socketio/socket.io/tree/master/examples/custom-parsers))的例子。

```js
const parser = require('socket.io-msgpack-parser'); // 或者 require('socket.io-json-parser')
const socket = io({
  parser: parser
});

// 服务器端必须要有相同的解析器，才能进行交流
const io = require('socket.io')({
  parser: parser
});
```

### Manager

#### new Manager(url[, options])

  - `url` _(String)_
  - `options` _(Object)_
    - `path` _(String)_ 服务器端捕获（captured）的路径名(`/socket.io`)
    - `reconnection` _(Boolean)_ 是否自定重连 (`true`)
    - `reconnectionAttempts` _(Number)_ 放弃之前尝试重连的次数 (`Infinity`)
    - `reconnectionDelay` _(Number)_ 在尝试新的重新连接之前要等待多长时间(`1000`)。 受 +/- `randomizationFactor` 的影响,例如，默认的初始延迟鉴于 500 到 1500 毫秒之间。
    - `reconnectionDelayMax` _(Number)_  重连之间等待的最大时间(`5000`)。每次尝试都增加了 2 倍的随机值的重新连接延迟。
    - `randomizationFactor` _(Number)_ (`0.5`), 0 <= randomizationFactor <= 1
    - `timeout` _(Number)_  `connect_error` 和 `connect_timeout`被发射之前的连接超时时间。 (`20000`)
    - `autoConnect` _(Boolean)_ 不管什么时候，只要你认为是合适的，你就可以设置它为 false 来调用 `manager.open`
    - `query` _(Object)_: 当连接到一个名称空间时被发送的额外的查询参数 (然后可以在服务器端的 `socket.handshake.query` 对象中找到)
    - `parser` _(Parser)_: 要使用的解析器。默认为 带有 socket.io 的 `Parser` 示例。 参见 [socket.io-parser](https://github.com/socketio/socket.io-parser).
  - **返回值** `Manager`

在底层的 `Socket` 初始化时，`options` 也会被传递给 `engine.io-client`。
查看[这里](https://github.com/socketio/engine.io-client#methods)的 `options` 可用选项。

#### manager.reconnection([value])

  - `value` _(Boolean)_
  - **返回值** `Manager|Boolean`

设置 `reconnection` 选项，或者如果没有传递参数，则返回它的当前值。

#### manager.reconnectionAttempts([value])

  - `value` _(Number)_
  - **返回值** `Manager|Number`

设置 `reconnectionAttempts` 选项，或者如果没有传递参数，则返回它的当前值。

#### manager.reconnectionDelay([value])

  - `value` _(Number)_
  - **返回值** `Manager|Number`

设置 `reconnectionDelay` 选项，或者如果没有传递参数，则返回它的当前值。

#### manager.reconnectionDelayMax([value])

  - `value` _(Number)_
  - **返回值** `Manager|Number`

设置 `reconnectionDelayMax` 选项，或者如果没有传递参数，则返回它的当前值。

#### manager.timeout([value])

  - `value` _(Number)_
  - **返回值** `Manager|Number`

设置 `timeout` 选项，或者如果没有传递参数，则返回它的当前值。

#### manager.open([callback])

  - `callback` _(Function)_
  - **返回值** `Manager`

如果使用 `autoConnect` 为 `false` 初始化 manager，打开一个新的连接进行尝试。

一旦尝试失败/成功，这个可选的 `callback` 参数将会被调用。

#### manager.connect([callback])

同义于 [manager.open([callback])](#manageropencallback).

#### manager.socket(nsp, options)

  - `nsp` _(String)_
  - `options` _(Object)_
  - **返回值** `Socket`

为给定的名称空间创建一个新的 `Socket` 。

#### Event: 'connect_error'

  - `error` _(Object)_ error object

连接错误时被触发。

#### Event: 'connect_timeout'

连接超时时被触发。

#### Event: 'reconnect'

  - `attempt` _(Number)_ 重连尝试次数

重连成功时触发。

#### Event: 'reconnect_attempt'

尝试重连时触发。

#### Event: 'reconnecting'

  - `attempt` _(Number)_ 重连尝试次数

重连成功时触发。

#### Event: 'reconnect_error'

  - `error` _(Object)_ error object

尝试重连发生错误时触发。

#### Event: 'reconnect_failed'

当无法在 `reconnectionAttempts` 中重连时被触发。

#### Event: 'ping'

当一个 ping 数据包被写到服务器时被触发。

#### Event: 'pong'

  - `ms` _(Number)_ 从 `ping` 数据包到收到 pong 数据包经历的毫秒数 (即: 延迟（latency）).

当接收到来自服务器的 pong 数据包时被触发。

### Socket

#### socket.id

  - _(String)_

套接字会话的唯一标识符。在 `connect` 事件被触发后设置，并在 `reconnect` 事件之后进行更新。

```js
const socket = io('http://localhost');

console.log(socket.id); // undefined

socket.on('connect', () => {
  console.log(socket.id); // 'G5p5...'
});
```

#### socket.open()

  - **返回值** `Socket`

手动打开套接字。

```js
const socket = io({
  autoConnect: false
});

// ...
socket.open();
```

它还可以用于手动重新连接:

```js
socket.on('disconnect', () => {
  socket.open();
});
```

#### socket.connect()

同义于 [socket.open()](#socketopen).

#### socket.send([...args][, ack])

  - `args`
  - `ack` _(Function)_
  - **返回值** `Socket`

发送一个 `message` 事件。参见 [socket.emit(eventName[, ...args][, ack])](#socketemiteventname-args-ack).

#### socket.emit(eventName[, ...args][, ack])

  - `eventName` _(String)_
  - `args`
  - `ack` _(Function)_
  - **返回值** `Socket`

将事件发射到由字符串名称标识的套接字。任何其他参数都可以包括在内。支持所有可序列化的数据结构，包括 `Buffer`。

```js
socket.emit('hello', 'world');
socket.emit('with-binary', 1, '2', { 3: '4', 5: new Buffer(6) });
```

`ack` 参数是可选的，它使用服务器的应答触发。

```js
socket.emit('ferret', 'tobi', (data) => {
  console.log(data); // data  将是  'woot'
});

// 服务器:
//  io.on('connection', (socket) => {
//    socket.on('ferret', (name, fn) => {
//      fn('woot');
//    });
//  });
```

#### socket.on(eventName, callback)

  - `eventName` _(String)_
  - `callback` _(Function)_
  - **返回值** `Socket`

为给定的事件出测一个新的处理程序。

```js
socket.on('news', (data) => {
  console.log(data);
});

// 使用多个参数
socket.on('news', (arg1, arg2, arg3, arg4) => {
  // ...
});
// 使用回调
socket.on('news', (cb) => {
  cb(0);
});
```

套接字实际上继承了 [Emitter](https://github.com/component/emitter) 类的每个方法，如 `hasListeners`, `once` 或 `off` (用来删除事件侦听器)。

#### socket.compress(value)

  - `value` _(Boolean)_
  - **返回值** `Socket`

为随后的事件发射设置一个修改器，只有当值为 `true` 时，事件数据才会被压缩。当您不调用方法时，默认为 `true`。

```js
socket.compress(false).emit('an event', { some: 'data' });
```

#### socket.close()

  - **返回值** `Socket`

手动断开连接套接字。

#### socket.disconnect()

同义于 [socket.close()](#socketclose).

#### Event: 'connect'

在连接上被触发，包括成功的重新连接。

```js
socket.on('connect', () => {
  // ...
});

// 注意: 您应该在 connect 之外注册事件处理程序
// 所以在重新连接上它们没有再次注册
socket.on('myevent', () => {
  // ...
});
```

#### Event: 'connect_error'

  - `error` _(Object)_ 错误对象

连接错误时被触发。

```js
socket.on('connect_error', (error) => {
  // ...
});
```

#### Event: 'connect_timeout'

连接超时时被触发。

```js
socket.on('connect_timeout', (timeout) => {
  // ...
});
```

#### Event: 'error'

  - `error` _(Object)_ 错误对象

发生错误时被触发。

```js
socket.on('error', (error) => {
  // ...
});
```

#### Event: 'disconnect'

  - `reason` _(String)_  'io server disconnect' 或者 'io client disconnect'

在断开连接时被触发。

```js
socket.on('disconnect', (reason) => {
  // ...
});
```

#### Event: 'reconnect'

  - `attempt` _(Number)_ 重连尝试次数

重连成功时被触发。

```js
socket.on('reconnect', (attemptNumber) => {
  // ...
});
```

#### Event: 'reconnect_attempt'

  - `attempt` _(Number)_ 重连尝试次数

尝试重新连接时被触发。

```js
socket.on('reconnect_attempt', (attemptNumber) => {
  // ...
});
```

#### Event: 'reconnecting'

  - `attempt` _(Number)_ 重连尝试次数

尝试重新连接时被触发。

```js
socket.on('reconnecting', (attemptNumber) => {
  // ...
});
```

#### Event: 'reconnect_error'

  - `error` _(Object)_ error object

重连尝试失败时被触发。

```js
socket.on('reconnect_error', (error) => {
  // ...
});
```

#### Event: 'reconnect_failed'

不能在 `reconnectionAttempts` 中重连时被触发。

```js
socket.on('reconnect_failed', () => {
  // ...
});
```

#### Event: 'ping'

当一个 ping 数据包被写到服务器时触发。

```js
socket.on('ping', () => {
  // ...
});
```

#### Event: 'pong'

  - `ms` _(Number)_ 从发送 `ping` 数据包到收到 pong 数据包的事件 (即: 延迟(latency)).

当收到来自服务器的 pong 数据包时被触发。

```js
socket.on('pong', (latency) => {
  // ...
});
```
