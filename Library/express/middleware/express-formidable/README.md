# express-formidable [![Build Status](https://travis-ci.org/noraesae/express-formidable.svg?branch=master)](https://travis-ci.org/noraesae/express-formidable)

一个 [Formidable](https://github.com/felixge/node-formidable) 的 [Express](http://expressjs.com) 中间件。

## 什么是 Express、Formidable 和 this?

[Express](http://expressjs.com) 是一个基于 Node.js 平台，快速、开放、极简的 web 开发框架。

[Formidable](https://github.com/felixge/node-formidable) 是一个 Node.js 模块，用于解析表单数据，包含了 `multipart/form-data` 文件上传。

因此， **`express-formidable`** 就像他们之间的一座桥，
具体地说，是 Formidable 的一个 Express 的中间件实现。

它的目的只是为了工作。

## 安装

```
npm install express-formidable
```

## 用法

```js
const express = require('express');
const formidable = require('express-formidable');

var app = express();

app.use(formidable());

app.post('/upload', (req, res) => {
  req.fields; // 包含非文件字段
  req.files; // 包含文件
});
```

就是这样。

express-formidable 基本上可以解析表单类型，Formidable 可以处理，包括 `application/x-www-form-urlencoded`、`application/json`、`multipart/form-data`。

## 选项

```js
app.use(formidable(opts));
```

`opts` 是可以被设置为 Formidable 中的  `form` 选项。例如:

```js
app.use(formidable({
  encoding: 'utf-8',
  uploadDir: '/my/dir',
  multiples: true, // req.files to be arrays of files
}));
```

要获取更多细节，请移步 [Formidable API](/Library/node-formidable/README.md#api)。

## 贡献

```
git clone https://github.com/noraesae/express-formidable.git
cd express-formidable
npm install
```

To lint and test:

```
npm test
```

## License

[MIT](LICENSE)
