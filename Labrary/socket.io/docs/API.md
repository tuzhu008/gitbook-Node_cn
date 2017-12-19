
## 内容列表

  - [类: Server](#server)
    - [new Server(httpServer[, options])](#new-serverhttpserver-options)
    - [new Server(port[, options])](#new-serverport-options)
    - [new Server(options)](#new-serveroptions)
    - [server.sockets](#serversockets)
    - [server.engine.generateId](#serverenginegenerateid)
    - [server.serveClient([value])](#serverserveclientvalue)
    - [server.path([value])](#serverpathvalue)
    - [server.adapter([value])](#serveradaptervalue)
    - [server.origins([value])](#serveroriginsvalue)
    - [server.origins(fn)](#serveroriginsfn)
    - [server.attach(httpServer[, options])](#serverattachhttpserver-options)
    - [server.attach(port[, options])](#serverattachport-options)
    - [server.listen(httpServer[, options])](#serverlistenhttpserver-options)
    - [server.listen(port[, options])](#serverlistenport-options)
    - [server.bind(engine)](#serverbindengine)
    - [server.onconnection(socket)](#serveronconnectionsocket)
    - [server.of(nsp)](#serverofnsp)
    - [server.close([callback])](#serverclosecallback)
  - [类: Namespace](#namespace)
    - [namespace.name](#namespacename)
    - [namespace.connected](#namespaceconnected)
    - [namespace.adapter](#namespaceadapter)
    - [namespace.to(room)](#namespacetoroom)
    - [namespace.in(room)](#namespaceinroom)
    - [namespace.emit(事件Name[, ...args])](#namespaceemiteventname-args)
    - [namespace.clients(callback)](#namespaceclientscallback)
    - [namespace.use(fn)](#namespaceusefn)
    - [事件: 'connect'](#event-connect)
    - [事件: 'connection'](#event-connect)
    - [标记: 'volatile'](#flag-volatile)
    - [标记: 'local'](#flag-local)
  - [类: Socket](#socket)
    - [socket.id](#socketid)
    - [socket.rooms](#socketrooms)
    - [socket.client](#socketclient)
    - [socket.conn](#socketconn)
    - [socket.request](#socketrequest)
    - [socket.handshake](#sockethandshake)
    - [socket.use(fn)](#socketusefn)
    - [socket.send([...args][, ack])](#socketsendargs-ack)
    - [socket.emit(eventName[, ...args][, ack])](#socketemiteventname-args-ack)
    - [socket.on(eventName, callback)](#socketoneventname-callback)
    - [socket.once(eventName, listener)](#socketonceeventname-listener)
    - [socket.removeListener(eventName, listener)](#socketremovelistenereventname-listener)
    - [socket.removeAllListeners([eventName])](#socketremovealllistenerseventname)
    - [socket.eventNames()](#socketeventnames)
    - [socket.join(room[, callback])](#socketjoinroom-callback)
    - [socket.join(rooms[, callback])](#socketjoinrooms-callback)
    - [socket.leave(room[, callback])](#socketleaveroom-callback)
    - [socket.to(room)](#sockettoroom)
    - [socket.in(room)](#socketinroom)
    - [socket.compress(value)](#socketcompressvalue)
    - [socket.disconnect(close)](#socketdisconnectclose)
    - [标记: 'broadcast'](#flag-broadcast)
    - [标记: 'volatile'](#flag-volatile-1)
    - [事件: 'disconnect'](#event-disconnect)
    - [事件: 'error'](#event-error)
    - [事件: 'disconnecting'](#event-disconnecting)
  - [类: Client](#client)
    - [client.conn](#clientconn)
    - [client.request](#clientrequest)


### Server

使用 `require('socket.io')` 暴露。、

> **[success] 『译者注』**
>
> 本文档 API 属性后面的括号中的值表示该属性的默认值。

#### new Server(httpServer[, options])

  - `httpServer` _(http.Server)_ 要绑定到的服务器。
  - `options` _(Object)_
    - `path` _(String)_: 获取的路径名 (`/socket.io`)
    - `serveClient` _(Boolean)_: 是否为客户端文件服务 (`true`)
    - `adapter` _(Adapter)_: 要使用的适配器。默认为附带基于内存的 socket.io 的 `Adapter` 实例。 参见 [socket.io-adapter](https://github.com/socketio/socket.io-adapter)
    - `origins` _(String)_: 允许的源(`*`)
    - `parser` _(Parser)_: 要使用的解析器。 默认为与 socket.io 一起使用的 `Parser`  的实例。参见 [socket.io-parser](https://github.com/socketio/socket.io-parser).

不需要关键字 `new`:

```js
const io = require('socket.io')();
// 或者
const Server = require('socket.io');
const io = new Server();
```

传递给 socket.io 的选项同样总是会被传递给 `engine.io` 被创建的`Server`。参见 engine.io [options](https://github.com/socketio/engine.io#methods-1) 作为参考.

其中:

  - `pingTimeout` _(Number)_: 有多少毫秒没有一个 pong 数据包，就考虑关闭连接。 (`60000`)
  - `pingInterval` _(Number)_: 在发送一个 ping 数据包前间隔多少毫秒。 (`25000`).

这两个参数将在客户端知道服务器不再可用之前对延迟产生影响。例如，如果底层的 TCP 连接由于网络问题而不能正确地关闭，那么客户端可能不得不等待到 `pingTimeout + pingInterval`  毫秒，才能获得一个 `disconnect` 事件。

  - `transports` _(Array<String>)_: 允许连接的传输 (`['polling', 'websocket']`).

**注意:** 顺序是很重要的。默认情况下，首先建立一个长轮询连接，然后，如果可能的话，升级到 WebSocket。使用 `['websocket']` 意思是如果 WebSocket 连接不能打开，就没有备选方案了。

```js
const server = require('http').createServer();

const io = require('socket.io')(server, {
  path: '/test',
  serveClient: false,
  // 下面是 engine.IO 选项
  pingInterval: 10000,
  pingTimeout: 5000,
  cookie: false
});

server.listen(3000);
```

#### new Server(port[, options])

  - `port` _(Number)_ 要剪听的端口 (创建一个新的 `http.Server`)
  - `options` _(Object)_

可用的选项，请参见 [前面](#new-serverhttpserver-options)。

```js
const server = require('http').createServer();

const io = require('socket.io')(3000, {
  path: '/test',
  serveClient: false,
  // below are engine.IO options
  pingInterval: 10000,
  pingTimeout: 5000,
  cookie: false
});
```

#### new Server(options)

  - `options` _(Object)_

可用的选项，请参见 [前面](#new-serverhttpserver-options)。

```js
const io = require('socket.io')({
  path: '/test',
  serveClient: false,
});

// 要么
const server = require('http').createServer();

io.attach(server, {
  pingInterval: 10000,
  pingTimeout: 5000,
  cookie: false
});

server.listen(3000);

// 或者
io.attach(3000, {
  pingInterval: 10000,
  pingTimeout: 5000,
  cookie: false
});
```

#### server.sockets

  * _(Namespace)_

默认名称空间为 `/`。

#### server.serveClient([value])

  - `value` _(Boolean)_
  - **『返回值』** `Server|Boolean`

如果值为 `true`，附加服务器( 参见 `Server#attach`)将服务于客户端文件。默认为 `true`。这种方法在 `attach` 被调用后没有效果。如果没有提供参数，该方法将返回当前值。

```js
// 传递一个服务器和`serveClient`选项
const io = require('socket.io')(http, { serveClient: false });

// 或者没有服务器，然后你就可以调用这个方法了
const io = require('socket.io')();
io.serveClient(false);
io.attach(http);
```

#### server.path([value])

  - `value` _(String)_
  - **『返回值』** `Server|String`

设置 `engine.io` 和将被服务的静态文件的路径为 `value`。默认为 `/socket.io`。 如果没有提供参数，该方法将返回当前值。

```js
const io = require('socket.io')();
io.path('/myownpath');

// 客户端
const socket = io({
  path: '/myownpath'
});
```

#### server.adapter([value])

  - `value` _(Adapter)_
  - **『返回值』** `Server|Adapter`

设置 adapter 为 `value`。
Sets the adapter `value`. 默认为附带基于内存的 socket.io 的 `Adapter` 实例。 参见 [socket.io-adapter](https://github.com/socketio/socket.io-adapter)。 如果没有提供参数，该方法将返回当前值。

```js
const io = require('socket.io')(3000);
const redis = require('socket.io-redis');
io.adapter(redis({ host: 'localhost', port: 6379 }));
```

#### server.origins([value])

  - `value` _(String)_
  - **『返回值』** `Server|String`

设置允许的源为`value`。 默认是允许任何源。如果没有提供参数，该方法将返回当前值。

```js
io.origins(['foo.example.com:443']);
```

#### server.origins(fn)

  - `fn` _(Function)_
  - **『返回值』** `Server`

提供一个函数，该函数带有两个参数，`origin:String` 和 `callback(error, success)`，其中 `success` 是一个布尔值，表示是否允许。

__潜在缺陷__:
* 在某些情况下, 当不可能确定 `origin` 时它可能有 `*` 的值
* 由于每个请求都将执行该函数，因此建议使此函数尽可能快地工作
* 如果 `socket.io` 被用于 `Express`，CORS 头只会受到 `socket.io` 请求的影响。 对于 Express 你可以使用 [cors](https://github.com/expressjs/cors).

```js
io.origins((origin, callback) => {
  if (origin !== 'https://foo.example.com') {
    return callback('origin not allowed', false);
  }
  callback(null, true);
});
```

#### server.attach(httpServer[, options])

  - `httpServer` _(http.Server)_ 要连接到的服务器
  - `options` _(Object)_

使用提供的 `options`(可选) 将 `Server` 连接到 `httpServer`上的 engine.io 实例，并附带提供的`options`(可选)。

#### server.attach(port[, options])

  - `port` _(Number)_ 要监听的端口
  - `options` _(Object)_

使用提供的 `options`(可选) 将 `Server` 连接到 `httpServer`上的 engine.io 实例，并附带提供的`options`(可选)。


#### server.listen(httpServer[, options])

同义于 [server.attach(httpServer[, options])](#serverattachhttpserver-options).

#### server.listen(port[, options])

同义于  server.attach(port[, options])](#serverattachport-options).

#### server.bind(engine)

  - `engine` _(engine.Server)_
  - **『返回值』** `Server`

仅限高级使用。绑定服务器到一个指定的 engine.io `Server` 实例(或兼容的 API)。

#### server.onconnection(socket)

  - `socket` _(engine.Socket)_
  - **『返回值』** `Server`

仅限高级使用。创建一个新的套接字。从传入的 engine.io(或兼容的API) `Socket`创建一个新的 `socket.io` 客户端“套接字”。

#### server.of(nsp)

  - `nsp` _(String)_
  - **『返回值』** `Namespace`

通过它的路径名标识符 `nsp` 初始化并检索给定的 `Namespace`。如果名称空间已经被初始化，它将立即返回。

```js
const adminNamespace = io.of('/admin');
```

#### server.close([callback])

  - `callback` _(Function)_

关闭 socket.io 服务器。 `callback` 是可选的，当所有连接都已关闭时将被调用。

```js
const Server = require('socket.io');
const PORT   = 3030;
const server = require('http').Server();

const io = Server(PORT);

io.close(); // 关闭当前服务器

server.listen(PORT); // 要使用的 PORT 是空闲的

io = Server(server);
```

#### server.engine.generateId

重写默认方法来生成自定义的套接字 id。

该函数以一个 node 请求对象(`http.IncomingMessage`)作为第一个参数调用。

```js
io.engine.generateId = (req) => {
  return "custom:id:" + custom_id++; // 自定义 id 必须是惟一的
}
```

### Namespace

表示一个由路径名标识的给定作用域下的已连接的套接字池（例如：`/chat`）。

一个客户端始终连接到 `/`(主名称空间)，然后可能连接到其他名称空间(使用相同的底层连接)。

#### namespace.name

  * _(String)_

名称空间标识符。

#### namespace.connected

  * _(Object<Socket>)_

连接到这个名称空间的 `Socket` 对象的哈希，以 `id` 作为索引。

#### namespace.adapter

  * _(Adapter)_


用于命名空间的 `Adapter`。在使用基于 [Redis](https://github.com/socketio/socket.io-redis) 的 `Adapter` 时很有用，因为它暴露了跨集群（cluster）管理套接字和房间的方法。

**注意:** 主名称空间的适配器(adapter)可以通过 `io.of('/').adapter` 访问。

#### namespace.to(room)

  - `room` _(String)_
  - **『返回值』** `Namespace` ，可用于链式调用

为随后的事件发射设置一个修改器，该事件只会对已进入给定 `room` 的客户端进行广播。

要发射到多个房间，你可以调用 `to` 多次。

```js
const io = require('socket.io')();
const adminNamespace = io.of('/admin');

adminNamespace.to('level1').emit('an event', { some: 'data' });
```

#### namespace.in(room)

同义于 [namespace.to(room)](#namespacetoroom).

#### namespace.emit(eventName[, ...args])

  - `eventName` _(String)_
  - `args`

向所有已连接的客户端发送事件。以下两个是等价的:


```js
const io = require('socket.io')();
io.emit('an event sent to all connected clients'); // 主 namespaces

const chat = io.of('/chat');
chat.emit('an event sent to all connected clients in chat namespace');
```

**注意:** 当从名称空间发射(emitting)时，不支持确认(acknowledgements)。

#### namespace.clients(callback)

  - `callback` _(Function)_

获取连接到该名称空间的客户端 ID 列表(如果适用的话，在所有节点之间)。

```js
const io = require('socket.io')();
io.of('/chat').clients((error, clients) => {
  if (error) throw error;
  console.log(clients); // => [PZDoMHjiu8PYfRiKAAAF, Anw2LatarvGVVXEIAAAD]
});
```
一个名称空间的房间中的所有客户端的示例：

```js
io.of('/chat').in('general').clients((error, clients) => {
  if (error) throw error;
  console.log(clients); // => [Anw2LatarvGVVXEIAAAD]
});
```

与广播（broadcasting）一样，默认所有客户端都来自默认的名称空间('/'):


```js
io.clients((error, clients) => {
  if (error) throw error;
  console.log(clients); // => [6em3d4TJP8Et9EMNAAAA, G5p55dHhGgUnLUctAAAB]
});
```

#### namespace.use(fn)

  - `fn` _(Function)_

注册一个中间件，该中间件是一个函数，每个进来的 `Socket` 都会执行这个函数，它接收一个 socket 和 一个函数（该函数可以将执行延迟到下一个注册的中间件上。）作为参数。

传递给中间件回调的错误被作为特殊的 `error` 数据包发送给客户端。

```js
io.use((socket, next) => {
  if (socket.request.headers.cookie) return next();
  next(new Error('Authentication error'));
});
```

#### Event: 'connect'

  - `socket` _(Socket)_ 与客户端连接的 socket

根据来自客户端的连接被触发。

```js
io.on('connect', (socket) => {
  // ...
});

io.of('/admin').on('connect', (socket) => {
  // ...
});
```

#### Event: 'connection'

同义于 [Event: 'connect'](#event-connect).

#### Flag: 'volatile'

为随后的事件发射设置一个修改器，如果客户端还没有准备好接收消息，则事件数据可能会丢失(因为网络慢或其他问题，或者因为它们通过长轮询连接，并且处于请求-响应周期的中间)。

```js
io.volatile.emit('an event', { some: 'data' }); // 客户端可能会或者可能不会接收到它
```

#### Flag: 'local'

为随后的事件发射设置一个修改器，事件数据只会被 _广播_ 到当前节点(当使用 [Redis adapter](https://github.com/socketio/socket.io-redis) 时使用)。

```js
io.local.emit('an event', { some: 'data' });
```

### Socket

`Socket` 是与浏览器客户端交互的基础类。`Socket` 属于某些 `Namespace`(默认为 `/`)，并使用一个底层 `Client` 进行通信。

应该注意的是，`Socket` 与实际的底层 TCP/IP `socket` 套接字**没有**直接联系，它只是类的名称。

在每个 `Namespace` 中，您还可以定义 `Socket` 可以进入和离开的任意通道(称为 `room`)。这提供了一种方便的方式向一组 `Socket` 广播(见下面的 `Socket#to`)。

`Socket` 类继承自 [EventEmitter](https://nodejs.org/api/events.html#events_class_eventemitter)。`Socket` 类覆盖了 `emit` 方法，并且不修改任何其他 `EventEmitter` 方法。这里所记录的所有方法，都是 `EventEmitter` 方法(除了 `emit`)，都是由 `EventEmitter` 实现的，[`EventEmitter` 的文档](http://nodejs.cn/api/events.html#events_class_eventemitter) 在这里也适用。


#### socket.id

  * _(String)_

会话的唯一标识符，它来自于底层 `Client`。

#### socket.rooms

  * _(Object)_

一个字符串的哈希，用于标识客户端所处的房间，并按房间名称进行索引。


```js
io.on('connection', (socket) => {
  socket.join('room 237', () => {
    let rooms = Object.keys(socket.rooms);
    console.log(rooms); // [ <socket.id>, 'room 237' ]
  });
});
```

#### socket.client

  * _(Client)_

对底层 `Client` 对象的引用。

#### socket.conn

  * _(engine.Socket)_

对底层 `Client` 传输连接的引用(engine.io `Socket` 对象)。这允许访问 IO 传输层，该层仍然(大部分)抽象真实的 TCP/IP 套接字。

#### socket.request

  * _(Request)_

一个 getter 代理(proxy)，它返回「 源于底层 engine.io `Client`的 `request` 」的引用。用于访问请求头信息，如 `Cookie` 或 `User-Agent`。

#### socket.handshake

  * _(Object)_

握手的细节:

```js
{
  headers: /* 作为握手的一部分被发送的 头 */,
  time: /* 创建日期 (字符串) */,
  address: /* 客户端的 ip */,
  xdomain: /*连接是否是跨域(cross-domain)的 */,
  secure: /* 连接是否安全 */,
  issued: /* 创建日期 (unix 时间戳) */,
  url: /* 请求 URL 字符串 */,
  query: /* 查询对象 */
}
```

用法:

```js
io.use((socket, next) => {
  let handshake = socket.handshake;
  // ...
});

io.on('connection', (socket) => {
  let handshake = socket.handshake;
  // ...
});
```

#### socket.use(fn)

  - `fn` _(Function)_

  注册一个中间件，它是一个为每个传入的 `Packet`(数据包) 执行的函数，它接收一个 packet 和一个函数作为参数，可选择性地将执行延迟到下一个注册的中间件。

  传递给中间件回调的错误被作为特殊的 `error` 数据包发送给客户端。

```js
io.on('connection', (socket) => {
  socket.use((packet, next) => {
    if (packet.doge === true) return next();
    next(new Error('Not a doge error'));
  });
});
```

#### socket.send([...args][, ack])

  - `args`
  - `ack` _(Function)_
  - **『返回值』** `Socket`

发送一个 `message` 事件。查看[socket.emit(eventName[, ...args][, ack])](#socketemiteventname-args-ack)。

#### socket.emit(eventName[, ...args][, ack])

*(覆盖 `EventEmitter.emit`)*
  - `eventName` _(String)_
  - `args`
  - `ack` _(Function)_
  - **『返回值』** `Socket`

将事件发送到由字符串名称标识的套接字。任何其他参数都可以包括在内。支持所有可序列化的数据结构，包括 `Buffer`。

```js
socket.emit('hello', 'world');
socket.emit('with-binary', 1, '2', { 3: '4', 5: new Buffer(6) });
```
`ack` 参数是可选的，将使用客户端的应答进行调用。

```js
io.on('connection', (socket) => {
  socket.emit('an event', { some: 'data' });

  socket.emit('ferret', 'tobi', (data) => {
    console.log(data); // data 将是 'woot'
  });

  // 客户端代码
  // client.on('ferret', (name, fn) => {
  //   fn('woot');
  // });

});
```

#### socket.on(eventName, callback)

*(inherited from `EventEmitter`)*
  - `eventName` _(String)_
  - `callback` _(Function)_
  - **『返回值』** `Socket`

为给定的事件注册一个新的处理函数。

```js
socket.on('news', (data) => {
  console.log(data);
});
// 使用多个参数
socket.on('news', (arg1, arg2, arg3) => {
  // ...
});
// 或者使用确认（acknowledgement）
socket.on('news', (data, callback) => {
  callback(0);
});
```

#### socket.once(eventName, listener)
#### socket.removeListener(eventName, listener)
#### socket.removeAllListeners([eventName])
#### socket.eventNames()

继承自 `EventEmitter`。查看 Node.js 文档的 [`events` 模块](http://nodejs.cn/api/events.html#events_class_eventemitter)。

#### socket.join(room[, callback])

  - `room` _(String)_
  - `callback` _(Function)_
  - **『返回值』** `Socket` for chaining

添加客户端到 `room`，并且可以选择带有 `err` 签名的回调(如果有的话)。

```js
io.on('connection', (socket) => {
  socket.join('room 237', () => {
    let rooms = Object.keys(socket.rooms);
    console.log(rooms); // [ <socket.id>, 'room 237' ]
    io.to('room 237').emit('a new user has joined the room'); // 向房间里的每个人广播
  });
});
```

加入房间的机制由已配置的 `Adapter` 处理(见上面的 `Server#adapter`)，默认为 [socket.io-adapter](https://github.com/socketio/socket.io-adapter)。

为方便起见，每个套接字将自动连接一个由其 id 标识的房间(请参阅 `Socket#id`)。这使得向其他套接字发送消息很容易:

```js
io.on('connection', (socket) => {
  socket.on('say to someone', (id, msg) => {
    // 发送一个私信到给定 id 的socket
    socket.to(id).emit('my message', msg);
  });
});
```

#### socket.join(rooms[, callback])

  - `rooms` _(Array)_
  - `callback` _(Function)_
  - **『返回值』** `Socket` for chaining

添加客户端到房间列表，并且可以选择带有 `err` 签名的回调(如果有的话)。


#### socket.leave(room[, callback])

  - `room` _(String)_
  - `callback` _(Function)_
  - **『返回值』** `Socket` ，可用于链式调用

从 `room` 移除客户端，并且触发一个带有 `err` 签名的回调（如果有的话）。

**在断开时会自动离开房间**.

#### socket.to(room)

  - `room` _(String)_
  - **『返回值』** `Socket` 可用于链式调用

为随后的事件发射设置一个修改器，该事件只会被 _广播_ 到已加入给定 `room` 的客户端(套接字本身被排除在外)。

为了发射到多个房间，可以调用 `to` 多次。

```js
io.on('connection', (socket) => {
  // to one room
  socket.to('others').emit('an event', { some: 'data' });
  // to multiple rooms
  socket.to('room1').to('room2').emit('hello');
  // 发送私信给其他 socket
  socket.to(/* 其他 socket id */).emit('hey');
});
```

**注意:** 广播时，不支持确认(acknowledgements)。

#### socket.in(room)

同义于 [socket.to(room)](#sockettoroom).

#### socket.compress(value)

  - `value` _(Boolean)_ 是否对后面的数据包进行压缩
  - **『返回值』** `Socket` 可用于链式调用

为随后的事件发射设置一个修改器，只有当值为 `true` 时，事件数据才会被 _压缩_。当您不调用方法时，默认为 `true`。

```js
io.on('connection', (socket) => {
  socket.compress(false).emit('uncompressed', "that's rough");
});
```

#### socket.disconnect(close)

  - `close` _(Boolean)_ 是否关闭底层连接
  - **『返回值』** `Socket`

断开这个客户端。如果关闭的值为 `true`，则关闭底层连接。否则，它只会断开名称空间的连接。

```js
io.on('connection', (socket) => {
  setTimeout(() => socket.disconnect(true), 5000);
});
```

#### Flag: 'broadcast'

为随后的事件发射设置一个修改器，事件数据只会被 _广播_ 到每个套接字，除开发送者。

```js
io.on('connection', (socket) => {
  socket.broadcast.emit('an event', { some: 'data' }); // 每个socket 都能获得它，除了发送者
});
```

#### Flag: 'volatile'

为随后的事件发射设置一个修改器，如果客户端还没有准备好接收消息(由于网络慢或其他问题，或者因为它们通过长轮询连接，并且处于请求-响应周期的中间)，事件数据可能会丢失。

```js
io.on('connection', (socket) => {
  socket.volatile.emit('an event', { some: 'data' }); // 客户端可能会，也可能不会接收到它
});
```

#### Event: 'disconnect'

  - `reason` _(String)_ 断开连接的原因(客户端或服务器端)

在断开连接时被触发。

```js
io.on('connection', (socket) => {
  socket.on('disconnect', (reason) => {
    // ...
  });
});
```

#### Event: 'error'

  - `error` _(Object)_ 错误对象

当有发生错误时被触发。

```js
io.on('connection', (socket) => {
  socket.on('error', (error) => {
    // ...
  });
});
```

#### Event: 'disconnecting'

  - `reason` _(String)_ 断开连接的原因(客户端或服务器端)

当客户端断开连接时被触发(但还没有离家 `rooms`)。

```js
io.on('connection', (socket) => {
  socket.on('disconnecting', (reason) => {
    let rooms = Object.keys(socket.rooms);
    // ...
  });
});
```

这些保留事件 (与 `connect`, `newListener` 和 `removeListener`一起) 不能用作事件名。

### Client

`Client` 类表示一个进来的传输(engine.io)连接。`Client` 可以与属于不同名称空间的多路复用(multiplexed) `Socket` 相关联。

#### client.conn

  * _(engine.Socket)_

底层 `engine.io` `Socket` 连接的引用。

#### client.request

  * _(Request)_


一个 getter 代理(proxy)，它返回「源于 engine.io 连接的 `request` 的引用」发起引擎的请求的引用。用于访问请求头信息，如 `Cookie` 或 `User-Agent`。
