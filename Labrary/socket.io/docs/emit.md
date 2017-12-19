
## Emit 参考手册

```js

io.on('connect', onConnect);

function onConnect(socket){

  // 发送到客户端
  socket.emit('hello', 'can you hear me?', 1, 2, 'abc');

  // 发送到除开发送者的所有客户端
  socket.broadcast.emit('broadcast', 'hello friends!');

  // 发送到 'game' 房间下的除了发送者之外的所有客户端
  socket.to('game').emit('nice game', "let's play a game");

  // 发送到 'game1' 和/或 'game2' 房间下的除了发送者之外的所有客户端
  socket.to('game1').to('game2').emit('nice game', "let's play a game (too)");

  // 发送到 'game' 房间下的所有客户端，包括发送者
  io.in('game').emit('big-announcement', 'the game will start soon');

  // 发送到 'myNamespace' 名称空间中的所有客户端
  io.of('myNamespace').emit('bigger-announcement', 'the tournament will start soon');

  // 发送到指定名称空间中的指定房间的所有客户端，，包括发送者
  io.of('myNamespace').to('room').emit('event', 'message');

  // 发送到单个的 socketid (私有消息)
  socket.to(<socketid>).emit('hey', 'I just met you');

  // 带确认（acknowledgement）的发送
  socket.emit('question', 'do you think so?', function (answer) {});

  // 发送不经压缩的信息
  socket.compress(false).emit('uncompressed', "that's rough");

  // 发送消息，如果客户端不准备接收消息，可能会被删除
  socket.volatile.emit('maybe', 'do you really need it?');

  // 发送到该 node 上的所有客户端（当使用多个 node 时）
  io.local.emit('hi', 'my lovely babies');

  // 发送到所有已连接到的客户端
  io.emit('an event sent to all connected clients');

};

```

**注意:** 以下事件是保留的，不应该被应用程序用作事件名称:
- `error`
- `connect`
- `disconnect`
- `disconnecting`
- `newListener`
- `removeListener`
- `ping`
- `pong`
