
# socket.io

[![Backers on Open Collective](https://opencollective.com/socketio/backers/badge.svg)](#backers) [![Sponsors on Open Collective](https://opencollective.com/socketio/sponsors/badge.svg)](#sponsors)
[![Build Status](https://secure.travis-ci.org/socketio/socket.io.svg?branch=master)](https://travis-ci.org/socketio/socket.io)
[![Dependency Status](https://david-dm.org/socketio/socket.io.svg)](https://david-dm.org/socketio/socket.io)
[![devDependency Status](https://david-dm.org/socketio/socket.io/dev-status.svg)](https://david-dm.org/socketio/socket.io#info=devDependencies)
[![NPM version](https://badge.fury.io/js/socket.io.svg)](https://www.npmjs.com/package/socket.io)
![Downloads](https://img.shields.io/npm/dm/socket.io.svg?style=flat)
[![](https://slackin-socketio.now.sh/badge.svg)](https://slackin-socketio.now.sh)

## 特性

Socket.IO  使基于事件的实时双向通信成为可能。它包括:

- 一个 Node.js 服务器 (这个仓库)
- 一个 适用于浏览器的 [Javascript 客户端库](https://github.com/socketio/socket.io-client) (或者一个 Node.js 客户端)

其他语言的一些可用实现：

- [Java](https://github.com/socketio/socket.io-client-java)
- [C++](https://github.com/socketio/socket.io-client-cpp)
- [Swift](https://github.com/socketio/socket.io-client-swift)

主要的特性有:

#### 可靠性

即使在存在的情况下，联系也会建立起来：
  - 代理和负载平衡器。
  - 个人防火墙和防病毒软件。

出于这个目的，它依赖于 [Engine.IO](https://github.com/socketio/engine.io)，它首先建立了一个长轮询连接，然后尝试升级到更好的传输（这是在一旁“被测试的”），比如 WebSocket。请参阅 [Goals](https://github.com/socketio/engine.io#goals) 部分获得更多信息。

#### 支持自动重连

除非另有指示，否则断开连接的客户端将尝试重新连接，直到服务器再次可用。请在[这里](https://github.com/socketio/socket.io-client/blob/master/docs/API.md#new-managerurl-options)查看可用的重新连接选项。

#### 断开检测

在 Engine.IO 级别实现了心跳机制，允许服务器和客户端知道对方何时不再响应。

该功能是通过在服务器和客户端设置的计时器实现的，在连接[握手](https://baike.baidu.com/item/%E6%8F%A1%E6%89%8B/5800282?fr=aladdin)期间共享超时值(`pingInterval` 和 `pingTimeout` 参数)。这些计时器要求任何后续的客户端调用被定向到同一个服务器，因此在使用多个节点时需要 `sticky-session` 必要条件。

#### 支持二进制

任何可序列化的数据结构都可以被发射，包括:

- 浏览器中的 [ArrayBuffer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer) 和 [Blob](https://developer.mozilla.org/en-US/docs/Web/API/Blob)

- Node.js 中的 [ArrayBuffer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer) 和 [Buffer](https://nodejs.org/api/buffer.html)

#### 简单和方便的 API

示例代码:

```js
io.on('connection', function(socket){
  socket.emit('request', /* */); // 发射一个事件到 socket
  io.emit('broadcast', /* */); // 发射一个事件到所有已连接的 sockets
  socket.on('reply', function(){ /* */ }); // 监听事件
});
```

#### 跨浏览器

在 Saucelabs 中测试浏览器:

[![Sauce Test Status](https://saucelabs.com/browser-matrix/socket.svg)](https://saucelabs.com/u/socket)

#### 支持多路复用（Multiplexing）

为了在应用程序中创建关注点隔离(例如每个模块，或者基于权限)，Socket.IO 允许创建多个 `Namespaces`，这些名称空间将充当单独的通信通道，但将共享相同的底层连接。

#### 支持房间（Room）


在每个 `Namespace` 中，您可以定义任意的通道，称为 `Rooms`，套接字可以加入和离开。然后你可以把它广播到任何一个给定的房间，到达加入这个房间的每一个套接字。

这是向一组用户发送通知的有用功能，或者是向在多个设备上连接的给定用户发送通知。


**注意:** Socket.IO 不是 WebSocket 的实现。尽管 Socket.IO 确实在可能的情况下使用 WebSocket 作为传输，它为每个数据包(packet)添加了一些元数据：当需要消息确认时，包类型、名称空间和 确认(ack) id。这就是为什么 WebSocket 客户端无法成功连接到 Socket.IO 服务器，并且一个 Socket.IO 客户端无法连接到 WebSocket 服务器的原因。(如:`ws://echo.websocket.org`)。请参阅[这里](https://github.com/socketio/socket.io-protocol)的协议规范。


## 安装

```bash
npm install socket.io --save
```

## 怎么用

下面示例将 socket.io 连接到一个普通的 Node.js HTTP 服务器（运行在 `3000` 端口 ）。

```js
var server = require('http').createServer();
var io = require('socket.io')(server);
io.on('connection', function(client){
  client.on('event', function(data){});
  client.on('disconnect', function(){});
});
server.listen(3000);
```

### 独立的

```js
var io = require('socket.io')();
io.on('connection', function(client){});
io.listen(3000);
```

### 与 Eexpress 集成

从 **3.0** 开始，express 应用程序已经成为您传递给 http 或 http 服务器实例的请求处理函数。您需要将 `Server` 传递给 `socket.io`，而不是 express 应用程序函数。也一定要在 `server` 调用 `.listen` ，而不是`app`。

```js
var app = require('express')();
var server = require('http').createServer(app);
var io = require('socket.io')(server);
io.on('connection', function(){ /* … */ });
server.listen(3000);
```

### 与 Koa 集成

如同 Express.JS，Koa 的工作是暴露一个应用程序作为请求处理函数，但仅靠调用 `callback` 方法。

```js
var app = require('koa')();
var server = require('http').createServer(app.callback());
var io = require('socket.io')(server);
io.on('connection', function(){ /* … */ });
server.listen(3000);
```

## 文档

请参见 [中文文档](/Library/socketIO/docs/README.md). 欢迎贡献！

## 调试 / 记录

Socket.IO 是由 [debug](https://github.com/visionmedia/debug) 驱动的。为了查看所有的调试输出，可以在需要的作用域下使用环境变量 `DEBUG` 来运行您的应用程序。

要查看所有 Socket.IO 的调试作用域的输出，可以使用:

```
DEBUG=socket.io* node myapp
```

## 测试

```
npm test
```
这将运行 `gulp` 任务 `test`。默认情况下，将使用 `lib` 目录中的源代码运行测试。

设置 `TEST_VERSION` 为 `compat` 来测试该代码的经过转换的 es5 兼容版本。

The `gulp` task `test` will always transpile the source code into es5 and export to `dist` first before running the test.



在运行测试之前，首先，`gulp` 任务 `test` 将始终将源代码转换为 es5，并将其导出到 `dist`。

## 支持者

每月的捐款支持我们，并帮助我们继续我们的活动。[[称为支持者](https://opencollective.com/socketio#backer)]

<a href="https://opencollective.com/socketio/backer/0/website" target="_blank"><img src="https://opencollective.com/socketio/backer/0/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/1/website" target="_blank"><img src="https://opencollective.com/socketio/backer/1/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/2/website" target="_blank"><img src="https://opencollective.com/socketio/backer/2/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/3/website" target="_blank"><img src="https://opencollective.com/socketio/backer/3/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/4/website" target="_blank"><img src="https://opencollective.com/socketio/backer/4/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/5/website" target="_blank"><img src="https://opencollective.com/socketio/backer/5/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/6/website" target="_blank"><img src="https://opencollective.com/socketio/backer/6/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/7/website" target="_blank"><img src="https://opencollective.com/socketio/backer/7/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/8/website" target="_blank"><img src="https://opencollective.com/socketio/backer/8/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/9/website" target="_blank"><img src="https://opencollective.com/socketio/backer/9/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/10/website" target="_blank"><img src="https://opencollective.com/socketio/backer/10/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/11/website" target="_blank"><img src="https://opencollective.com/socketio/backer/11/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/12/website" target="_blank"><img src="https://opencollective.com/socketio/backer/12/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/13/website" target="_blank"><img src="https://opencollective.com/socketio/backer/13/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/14/website" target="_blank"><img src="https://opencollective.com/socketio/backer/14/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/15/website" target="_blank"><img src="https://opencollective.com/socketio/backer/15/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/16/website" target="_blank"><img src="https://opencollective.com/socketio/backer/16/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/17/website" target="_blank"><img src="https://opencollective.com/socketio/backer/17/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/18/website" target="_blank"><img src="https://opencollective.com/socketio/backer/18/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/19/website" target="_blank"><img src="https://opencollective.com/socketio/backer/19/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/20/website" target="_blank"><img src="https://opencollective.com/socketio/backer/20/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/21/website" target="_blank"><img src="https://opencollective.com/socketio/backer/21/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/22/website" target="_blank"><img src="https://opencollective.com/socketio/backer/22/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/23/website" target="_blank"><img src="https://opencollective.com/socketio/backer/23/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/24/website" target="_blank"><img src="https://opencollective.com/socketio/backer/24/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/25/website" target="_blank"><img src="https://opencollective.com/socketio/backer/25/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/26/website" target="_blank"><img src="https://opencollective.com/socketio/backer/26/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/27/website" target="_blank"><img src="https://opencollective.com/socketio/backer/27/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/28/website" target="_blank"><img src="https://opencollective.com/socketio/backer/28/avatar.svg"></a>
<a href="https://opencollective.com/socketio/backer/29/website" target="_blank"><img src="https://opencollective.com/socketio/backer/29/avatar.svg"></a>


## 赞助商

成为一个赞助商，您的网站标志将出现在 Github 的 READM 中，它将链接到你的网站上。 [[成为赞助商](https://opencollective.com/socketio#sponsor)]

<a href="https://opencollective.com/socketio/sponsor/0/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/0/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/1/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/1/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/2/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/2/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/3/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/3/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/4/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/4/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/5/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/5/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/6/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/6/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/7/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/7/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/8/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/8/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/9/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/9/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/10/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/10/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/11/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/11/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/12/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/12/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/13/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/13/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/14/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/14/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/15/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/15/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/16/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/16/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/17/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/17/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/18/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/18/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/19/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/19/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/20/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/20/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/21/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/21/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/22/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/22/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/23/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/23/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/24/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/24/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/25/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/25/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/26/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/26/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/27/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/27/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/28/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/28/avatar.svg"></a>
<a href="https://opencollective.com/socketio/sponsor/29/website" target="_blank"><img src="https://opencollective.com/socketio/sponsor/29/avatar.svg"></a>


## License

[MIT](LICENSE)
