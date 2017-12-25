
# socket.io-client

[![Build Status](https://secure.travis-ci.org/socketio/socket.io-client.svg?branch=master)](http://travis-ci.org/socketio/socket.io-client)
[![Dependency Status](https://david-dm.org/socketio/socket.io-client.svg)](https://david-dm.org/socketio/socket.io-client)
[![devDependency Status](https://david-dm.org/socketio/socket.io-client/dev-status.svg)](https://david-dm.org/socketio/socket.io-client#info=devDependencies)
![NPM version](https://badge.fury.io/js/socket.io-client.svg)
![Downloads](http://img.shields.io/npm/dm/socket.io-client.svg?style=flat)
[![](http://slack.socket.io/badge.svg?)](http://slack.socket.io)

[![Sauce Test Status](https://saucelabs.com/browser-matrix/socket.svg)](https://saucelabs.com/u/socket)

## 如何使用

一个独立的 `socket.io-client` 构建，被 socket.io 作为 `/socket.io/socket.io.js` 自动暴露。或者，您也为 `dist` 文件夹下的 `socket.io.js` 文件提供服务。

```html
<script src="/socket.io/socket.io.js"></script>
<script>
  var socket = io('http://localhost');
  socket.on('connect', function(){});
  socket.on('event', function(data){});
  socket.on('disconnect', function(){});
</script>
```

```js
// 使用 ES6 导入
import io from 'socket.io-client';

const socket = io('http://localhost');
```

也可以使用轻巧版（不含 `JSON3`，一个 适用于 IE6/IE7 和 `debug` 的 JSON polyfill ）的构建：`socket.io.slim.js`。

Socket.IO 与 [browserify](http://browserify.org/) 和 [webpack](https://webpack.js.org/) 是兼容的([参见示例](https://github.com/socketio/socket.io/tree/2.0.3/examples/webpack-build))。

### Node.JS (服务器端用法)

  添加 `socket.io-client` 到你的 `package.json`，然后：

  ```js
  var socket = require('socket.io-client')('http://localhost');
  socket.on('connect', function(){});
  socket.on('event', function(data){});
  socket.on('disconnect', function(){});
  ```

## API

参见 [API](/docs/API.md)

## License

[MIT](/LICENSE)
