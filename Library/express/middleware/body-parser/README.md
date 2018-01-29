# body-parser

[![NPM Version][npm-image]][npm-url]
[![NPM Downloads][downloads-image]][downloads-url]
[![Build Status][travis-image]][travis-url]
[![Test Coverage][coveralls-image]][coveralls-url]

Node.js body 解析中间件。

在请求被处理程序处理之前解析传入的请求主体，
Parse incoming request bodies in a middleware before your handlers, available
under the `req.body` property.

**注意：** `req.body` 对象的形式是基于用户输入的，对象中所有的属性和其值都是不可信的，因此在信任之前进行验证。
例如，`req.body.foo.toString()` 可能会在多种情况下失败，例如，`foo` 属性可能不存在，也可能不是字符串，或者 `toString` 不是一个函数而是一个字符串或其他用户输入。

[了解 Node.js 中 HTTP 事务的剖析](https://nodejs.org/en/docs/guides/anatomy-of-an-http-transaction/).

_此中间件不能处理多部分主体的情况_，由于它们的很杂复杂性和通常又很大。对于多部分的主体，您可能对以下模块感兴趣:

  * [busboy](https://www.npmjs.org/package/busboy#readme) 和
    [connect-busboy](https://www.npmjs.org/package/connect-busboy#readme)
  * [multiparty](https://www.npmjs.org/package/multiparty#readme) 和
    [connect-multiparty](https://www.npmjs.org/package/connect-multiparty#readme)
  * [formidable](https://www.npmjs.org/package/formidable#readme)
  * [multer](https://www.npmjs.org/package/multer#readme)

这个模块提供以下解析器:

  * [JSON body parser](#bodyparserjsonoptions)
  * [Raw body parser](#bodyparserrawoptions)
  * [Text body parser](#bodyparsertextoptions)
  * [URL-encoded form body parser](#bodyparserurlencodedoptions)

您可能感兴趣的其他请求体解析器:

- [body](https://www.npmjs.org/package/body#readme)
- [co-body](https://www.npmjs.org/package/co-body#readme)

## 安装

```sh
$ npm install body-parser
```

## API

<!-- eslint-disable no-unused-vars -->

```js
var bodyParser = require('body-parser')
```

`bodyParser` 对象暴露各种工厂函数来创建中间件。当 `Content-Type` 请求头与 `type` 选项匹配时，
所有的中间件都会使用解析后的主体来填充 `req.body` 属性，如果没有主体可以解析、`Content-Type` 不匹配或发生错误，那么所有的中间件都会使用空对象（`{}`）。

[错误部分](#errors)描述了这个模块返回的各种错误。

### bodyParser.json([options])

返回一个只解析 `json` 的中间件，并且只会查找只查找 `Content-Type` 头部与 `type` 选项相匹配的请求。
这个解析器接受主体的任何 Unicode 编码，并支持自动解压 `gzip` 和 `deflate` 编码。

包含解析后的数据的新 `body` 对象被填充到中间件之后的 `request` 对象（即 `req.body`）上。

#### 选项

`json` 函数接受一个可选的 `options` 对象，这个对象可以包含下面的内容：

##### inflate

当 `inflate` 设置为 `true` 时，被压缩过的主体将被解压；
当为 `false`，被压缩过的主体将被拒绝。默认为 `true`。

##### limit

控制请求主体的最大尺寸。如果 `limit` 是一个数字，那么该值指定了字节数，这个值将被传入 [bytes](https://www.npmjs.com/package/bytes) 库进行解析。默认为 `'100kb'`。

##### reviver

`reviver` 选项被直接传入 `JSON.parse` 作为它的第二个参数。你可以在 [JSON.parse 的 MDN 文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse#Example.3A_Using_the_reviver_parameter) 找到关于这个参数的更多信息。

##### strict

当设置为 `true` 时，将只会接受数组或对象；当为 `false` 时，可以接收任何 `JSON.parse` 接受的东西。默认为 `true`。

##### type

`type` 选项用于确定中间件将解析的媒体类型。该选项可以是一个字符串，字符串数组或函数。
如果不是函数，`type` 选项直接传递给 [type-is](https://www.npmjs.org/package/type-is#readme) 库，这可以是扩展名（如 `json`），MIME 类型（如 `application/json`）或带有通配符的 MIME 类型（如 `*/*` 或 `*/json`）。
如果是一个函数， `type` 选项被以 `fn(req)` 的形式调用，并且如果返回一个真值，则该请求被解析。
默认为 `application/json`。

##### verify

如果提供了 `verify` 选项，则以 `verify(req, res, buf, encoding)` 形式被调用，其中 `buf` 为原始请求体的 `Buffer`， `encoding` 为请求的编码。抛出错误可以中止解析。

### bodyParser.raw([options])

返回将所有主体解析为 `Buffer` 的中间件，并仅查看 `Content-Type` 头与 `type` 选项匹配的请求。
这个解析器支持支持自动解压 `gzip` 和 `deflate` 编码。

包含解析的数据的新的 `body` 对象被填充在中间件之后的 `request` 对象（即，`req.body`）上。
这将是请求主体的一个 `Buffer` 对象。

#### Options

`raw` 函数接受一个可选的 `options` 对象，这个对象可以包含下面的内容：

##### inflate

当 `inflate` 设置为 `true` 时，被压缩过的主体将被解压；
当为 `false`，被压缩过的主体将被拒绝。默认为 `true`。

##### limit

控制请求主体的最大尺寸。如果 `limit` 是一个数字，那么该值指定了字节数，这个值将被传入 [bytes](https://www.npmjs.com/package/bytes) 库进行解析。默认为 `'100kb'`。

##### type

`type` 选项用于确定中间件将解析的媒体类型。该选项可以是一个字符串，字符串数组或函数。
如果不是函数，`type` 选项直接传递给 [type-is](https://www.npmjs.org/package/type-is#readme) 库，这可以是扩展名（如 `bin`），MIME 类型（如 `application/octet-stream`）或带有通配符的 MIME 类型（如 `*/*` 或 `application/*`）。
如果是一个函数， `type` 选项被以 `fn(req)` 的形式调用，并且如果返回一个真值，则该请求被解析。
默认为 `application/octet-stream`。

##### verify

如果提供了 `verify` 选项，则以 `verify(req, res, buf, encoding)` 形式被调用，其中 `buf` 为原始请求体的 `Buffer`， `encoding` 为请求的编码。抛出错误可以中止解析。

### bodyParser.text([options])

返回将所有主体解析为字符串的中间件，并仅查看 `Content-Type` 头与 `type` 选项匹配的请求。这个解析器支持自动解压 `gzip` 和 `deflate` 编码。

包含解析的数据的新的 `body` 对象被填充在中间件之后的 `request` 对象（即，`req.body`）上。
这将是请求主体的一个字符串。

#### Options

`text` 函数接受一个可选的 `options` 对象，这个对象可以包含下面的内容：


##### defaultCharset

如果未在请求的 `Content-Type` 头中指定字符集，请指定文本内容的默认字符集。 默认为 `utf-8`。

##### inflate

当 `inflate` 设置为 `true` 时，被压缩过的主体将被解压；
当为 `false`，被压缩过的主体将被拒绝。默认为 `true`。

##### limit

控制请求主体的最大尺寸。如果 `limit` 是一个数字，那么该值指定了字节数，这个值将被传入 [bytes](https://www.npmjs.com/package/bytes) 库进行解析。默认为 `'100kb'`。

##### type

`type` 选项用于确定中间件将解析的媒体类型。该选项可以是一个字符串，字符串数组或函数。
如果不是函数，`type` 选项直接传递给 [type-is](https://www.npmjs.org/package/type-is#readme) 库，这可以是扩展名（如 `txt`），MIME 类型（如 `text/plain`）或带有通配符的 MIME 类型（如 `*/*` 或 `text/*`）。
如果是一个函数， `type` 选项被以 `fn(req)` 的形式调用，并且如果返回一个真值，则该请求被解析。
默认为 `text/plain`。


##### verify

如果提供了 `verify` 选项，则以 `verify(req, res, buf, encoding)` 形式被调用，其中 `buf` 为原始请求体的 `Buffer`， `encoding` 为请求的编码。抛出错误可以中止解析。

### bodyParser.urlencoded([options])

返回仅解析 `urlencoded` 主体的中间件，并仅查看 `Content-Type` 头与 `type` 选项匹配的请求。
此解析器只接受主体的 UTF-8 编码，并支持自动解压 `gzip` 和 `deflate` 编码。

包含解析的数据的新的 `body` 对象被填充在中间件之后的 `request` 对象（即，`req.body`）上。
这个对象将包含一组键值对，其中值可以是一个字符串或数组（当 `extended` 为 `false` 时），或任何类型（当 `extended` 为 `true` 时）。

#### Options

`urlencoded` 函数接受一个可选的 `options` 对象，这个对象可以包含下面的内容：


##### extended

`extended` 选项允许选择使用 `querystring` 库（如果为 `false`）或 `qs` 库（如果为 `true`）来解析 URL 编码的数据。 "extended" 语法允许将丰富的对象和数组编码为 URL 编码的格式，从而允许使用类似 JSON 体验的 URL 编码的数据。有关更多信息，[请参阅 qs 库](https://www.npmjs.org/package/qs#readme)。

默认为 `true`，但使用默认值已被弃用。请研究 `qs` 和 `querystring` 之间的差异，并选择适当的设置。

##### inflate

当 `inflate` 设置为 `true` 时，被压缩过的主体将被解压；
当为 `false`，被压缩过的主体将被拒绝。默认为 `true`。

##### limit

控制请求主体的最大尺寸。如果 `limit` 是一个数字，那么该值指定了字节数，这个值将被传入 [bytes](https://www.npmjs.com/package/bytes) 库进行解析。默认为 `'100kb'`。

##### parameterLimit

`parameterLimit` 选项控制了 URL 编码数据中允许的最大参数数目。
如果一个请求包含比这个值更多的参数，一个 413 将被返回给客户端。 默认为 `1000`。

##### type

`type` 选项用于确定中间件将解析的媒体类型。该选项可以是一个字符串，字符串数组或函数。
如果不是函数，`type` 选项直接传递给 [type-is](https://www.npmjs.org/package/type-is#readme) 库，这可以是扩展名（如 `urlencoded`），MIME 类型（如 `application/x-www-form-urlencoded`）或带有通配符的 MIME 类型（如 `*/x-www-form-urlencoded`）。
如果是一个函数， `type` 选项被以 `fn(req)` 的形式调用，并且如果返回一个真值，则该请求被解析。
默认为 `application/x-www-form-urlencoded`。

##### verify

如果提供了 `verify` 选项，则以 `verify(req, res, buf, encoding)` 形式被调用，其中 `buf` 为原始请求体的 `Buffer`， `encoding` 为请求的编码。抛出错误可以中止解析。

## Errors

此模块提供的中间件根据解析过程中的错误情况创建错误。 这些错误通常具有 `status`/`statusCode` 属性，其中包含建议的 HTTP 响应代码，用于确定 `message` 属性是否应显示给客户端的 `expose` 属性，用于确定错误类型而不与 `message` 匹配的 `type` 属性，以及包含当前读取的主体的 `body` 属性（如果可用）。

以下是发布的常见错误，但出于各种原因可能会出现任何错误。

### content encoding unsupported

This error will occur when the request had a `Content-Encoding` header that
contained an encoding but the "inflation" option was set to `false`. The
`status` property is set to `415`, the `type` property is set to
`'encoding.unsupported'`, and the `charset` property will be set to the
encoding that is unsupported.

### request aborted

This error will occur when the request is aborted by the client before reading
the body has finished. The `received` property will be set to the number of
bytes received before the request was aborted and the `expected` property is
set to the number of expected bytes. The `status` property is set to `400`
and `type` property is set to `'request.aborted'`.

### request entity too large

This error will occur when the request body's size is larger than the "limit"
option. The `limit` property will be set to the byte limit and the `length`
property will be set to the request body's length. The `status` property is
set to `413` and the `type` property is set to `'entity.too.large'`.

### request size did not match content length

This error will occur when the request's length did not match the length from
the `Content-Length` header. This typically occurs when the request is malformed,
typically when the `Content-Length` header was calculated based on characters
instead of bytes. The `status` property is set to `400` and the `type` property
is set to `'request.size.invalid'`.

### stream encoding should not be set

This error will occur when something called the `req.setEncoding` method prior
to this middleware. This module operates directly on bytes only and you cannot
call `req.setEncoding` when using this module. The `status` property is set to
`500` and the `type` property is set to `'stream.encoding.set'`.

### too many parameters

This error will occur when the content of the request exceeds the configured
`parameterLimit` for the `urlencoded` parser. The `status` property is set to
`413` and the `type` property is set to `'parameters.too.many'`.

### unsupported charset "BOGUS"

This error will occur when the request had a charset parameter in the
`Content-Type` header, but the `iconv-lite` module does not support it OR the
parser does not support it. The charset is contained in the message as well
as in the `charset` property. The `status` property is set to `415`, the
`type` property is set to `'charset.unsupported'`, and the `charset` property
is set to the charset that is unsupported.

### unsupported content encoding "bogus"

This error will occur when the request had a `Content-Encoding` header that
contained an unsupported encoding. The encoding is contained in the message
as well as in the `encoding` property. The `status` property is set to `415`,
the `type` property is set to `'encoding.unsupported'`, and the `encoding`
property is set to the encoding that is unsupported.

## 示例

### Express/Connect top-level generic

此示例演示了将通用的 JSON 和 URL 编码解析器添加为顶级中间件，该解析器将解析所有传入请求的主体。这是最简单的设置。

```js
var express = require('express')
var bodyParser = require('body-parser')

var app = express()

// parse application/x-www-form-urlencoded
app.use(bodyParser.urlencoded({ extended: false }))

// parse application/json
app.use(bodyParser.json())

app.use(function (req, res) {
  res.setHeader('Content-Type', 'text/plain')
  res.write('you posted:\n')
  res.end(JSON.stringify(req.body, null, 2))
})
```

### Express route-specific

这个例子演示了如何将body 解析器专门添加到需要它们的路由中。
一般来说，这是 Express 使用 body-parser 最值得推荐的方法。

```js
var express = require('express')
var bodyParser = require('body-parser')

var app = express()

// create application/json parser
var jsonParser = bodyParser.json()

// create application/x-www-form-urlencoded parser
var urlencodedParser = bodyParser.urlencoded({ extended: false })

// POST /login gets urlencoded bodies
app.post('/login', urlencodedParser, function (req, res) {
  if (!req.body) return res.sendStatus(400)
  res.send('welcome, ' + req.body.username)
})

// POST /api/users gets JSON bodies
app.post('/api/users', jsonParser, function (req, res) {
  if (!req.body) return res.sendStatus(400)
  // create user in req.body
})
```

### 更改解析器接受的类型

所有的解析器都接受一个 `type` 选项，允许你改变中间件解析的 `Content-Type`。


```js
var express = require('express')
var bodyParser = require('body-parser')

var app = express()

// 将各种不同的自定义 JSON 类型解析为JSON
app.use(bodyParser.json({ type: 'application/*+json' }))

// 解析一些自定义的东西到一个 Buffer
app.use(bodyParser.raw({ type: 'application/vnd.custom-type' }))

// 将HTML body 解析为一个字符串
app.use(bodyParser.text({ type: 'text/html' }))
```

## License

[MIT](LICENSE)

[npm-image]: https://img.shields.io/npm/v/body-parser.svg
[npm-url]: https://npmjs.org/package/body-parser
[travis-image]: https://img.shields.io/travis/expressjs/body-parser/master.svg
[travis-url]: https://travis-ci.org/expressjs/body-parser
[coveralls-image]: https://img.shields.io/coveralls/expressjs/body-parser/master.svg
[coveralls-url]: https://coveralls.io/r/expressjs/body-parser?branch=master
[downloads-image]: https://img.shields.io/npm/dm/body-parser.svg
[downloads-url]: https://npmjs.org/package/body-parser
