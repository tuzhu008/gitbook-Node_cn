# method-override

[![NPM Version][npm-image]][npm-url]
[![NPM Downloads][downloads-image]][downloads-url]
[![Build Status][travis-image]][travis-url]
[![Test Coverage][coveralls-image]][coveralls-url]
[![Gratipay][gratipay-image]][gratipay-url]

让你在客户端不支持的地方使用 HTTP 动词，例如 PUT 或 DELETE 。

## 安装

这是一个通过 [npm 注册表](https://www.npmjs.com/) 可用的 [Node.js](https://nodejs.org/en/)  模块。使用 [`npm install` 命令](https://docs.npmjs.com/getting-started/installing-npm-packages-locally) 安装：

```sh
$ npm install method-override
```

## API

**注意** 在任何需要知道请求方法的模块**之前**使用这个模块是非常重要的 (例如，它 _必须_ 在 `csurf` 模块之前被使用)。

### methodOverride(getter, options)

创建一个新的中间件函数使用新值来覆盖 `req.method` 属性。这个值将从提供的 `getter` 中被提取出来。

- `getter` - 这个 getter 用来为请求查找覆盖请求方法。 (默认值: `X-HTTP-Method-Override`)
- `options.methods` - 进行值覆盖时允许原始请求的请求方法的。(默认值: `['POST']`)

如果找到的方法是 node.js 核心支持的，`req.method` 将被设置为这个值，好像它本来就是那个值。`req.method` 之前的值将被存储在 `req.originalMethod` 中。

#### getter

这是从请求中获取覆盖值的方法。如果提供的是一个函数，则将 `req` 作为第一个参数传递，将 `res` 作为第二个参数，并且该方法将被返回。如果提供的是一个字符串，则使用字符串来查找该方法，并使用以下规则:

- 如果字符串以 `X-` 开头，那么，它被当作 header 的名称，而该 header 被用于方法覆盖。如果请求包含多个相同的 header，那么第一个出现的就会被使用。
- 所有其他字符串都在 URL 查询字符串中被当作键。

#### options.methods

这允许指定原始请求*必须*在指定的 methods 中，以检查方法覆盖值。默认值仅为 `POST` 方法，这表示需要被覆盖的方法只能以 `POST` 到到。这里可能会指定更多的方法，但是当请求通过缓存时，可能会引入安全问题并导致奇怪的行为。这个值是一个大写的方法数组。指定为 `null` 表示允许所有方法。

> **[info] 「译者注」：**
>
> 类型：Array
> 描述：每一项为大写的方法字符串，如 "POST"、"GET"...当到达的请求的请求方法为数组中的某一项时才进行覆盖。


## 示例

### 使用 header 覆盖

要使用 header 来覆盖该方法，请将 header 名作为字符串参数指定给方法 `methodOverride` 函数。然后进行调用，将 `POST` 请求发送到带有覆盖的方法的 URL 作为该 header 的值。这种使用 header 的方法通常会在『不支持「你尝试使用的方法」的实现』中与 `XMLHttpRequest` 一起使用。

```js
var express = require('express')
var methodOverride = require('method-override')
var app = express()

// override with the X-HTTP-Method-Override header in the request
app.use(methodOverride('X-HTTP-Method-Override'))
```

使用 `XMLHttpRequest` 设置 header 来进行覆盖：

<!-- eslint-env browser -->

```js
var xhr = new XMLHttpRequest()
xhr.onload = onload
xhr.open('post', '/resource', true)
xhr.setRequestHeader('X-HTTP-Method-Override', 'DELETE')
xhr.send()

function onload () {
  alert('got response: ' + this.responseText)
}
```

### 使用查询字符串覆盖

要使用查询字符串值来覆盖该方法，请将查询字符串键作为字符串参数指定给 `methodOverride` 函数。然后进行调用，将 `POST` 请求发送到带有覆盖的方法的 URL 作为该查询字符串键的值。当尝试支持遗留浏览器，但仍然使用较新的方法时，使用查询值的方法通常会与普通的 HTML `<form>` 元素一起使用。

```js
var express = require('express')
var methodOverride = require('method-override')
var app = express()

// override with POST having ?_method=DELETE
app.use(methodOverride('_method'))
```

使用 HTML `<form>` 与查询字符串来进行覆盖：

```html
<form method="POST" action="/resource?_method=DELETE">
  <button type="submit">Delete resource</button>
</form>
```

### multiple format support

```js
var express = require('express')
var methodOverride = require('method-override')
var app = express()

//使用不同的 headers 进行覆盖; 最近的优先。
app.use(methodOverride('X-HTTP-Method'))          // Microsoft
app.use(methodOverride('X-HTTP-Method-Override')) // Google/GData
app.use(methodOverride('X-Method-Override'))      // IBM
```

### custom logic


您可以使用一个函数为 `getter` 实现任何类型的自定义逻辑。下面实现了查找 `req.body` 逻辑，这是在`method-override@1`:

```js
var bodyParser = require('body-parser')
var express = require('express')
var methodOverride = require('method-override')
var app = express()

// 注意: 当使用 req.body 时，你必须完全解析请求主体
// 在中间件堆栈调用 methodOverride() 之前
// 否则 req.body 不会被填充 
app.use(bodyParser.urlencoded())
app.use(methodOverride(function (req, res) {
  if (req.body && typeof req.body === 'object' && '_method' in req.body) {
    // 查找解码的 POST 主体 并 删除它
    var method = req.body._method
    delete req.body._method
    return method
  }
}))
```

使用 HTML `<form>` 和查询字符串进行覆盖：

```html
<!-- enctype 必须在调用 methodOverride() 之前被设置为你讲要解析的类型 -->
<form method="POST" action="/resource" enctype="application/x-www-form-urlencoded">
  <input type="hidden" name="_method" value="DELETE">
  <button type="submit">Delete resource</button>
</form>
```

## License

[MIT](LICENSE)

[npm-image]: https://img.shields.io/npm/v/method-override.svg
[npm-url]: https://npmjs.org/package/method-override
[travis-image]: https://img.shields.io/travis/expressjs/method-override/master.svg
[travis-url]: https://travis-ci.org/expressjs/method-override
[coveralls-image]: https://img.shields.io/coveralls/expressjs/method-override/master.svg
[coveralls-url]: https://coveralls.io/r/expressjs/method-override?branch=master
[downloads-image]: https://img.shields.io/npm/dm/method-override.svg
[downloads-url]: https://npmjs.org/package/method-override
[gratipay-image]: https://img.shields.io/gratipay/dougwilson.svg
[gratipay-url]: https://www.gratipay.com/dougwilson/
