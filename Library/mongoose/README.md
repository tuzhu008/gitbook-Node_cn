# Mongoose

Mongoose 是一种用于在异步环境中工作的 [MongoDB](https://www.蒙古族) 对象建模工具。

[![Slack Status](http://slack.mongoosejs.io/badge.svg)](http://slack.mongoosejs.io)
[![Build Status](https://api.travis-ci.org/Automattic/mongoose.svg?branch=master)](https://travis-ci.org/Automattic/mongoose)
[![NPM version](https://badge.fury.io/js/mongoose.svg)](http://badge.fury.io/js/mongoose)
[![Dependency Status](https://gemnasium.com/Automattic/mongoose.svg)](https://gemnasium.com/Automattic/mongoose)
[![Get help on Codementor](https://cdn.codementor.io/badges/get_help_github.svg)](https://www.codementor.io/vkarpov?utm_source=github&utm_medium=button&utm_term=vkarpov&utm_campaign=github)

## 文档

[mongoosejs.com](http://mongoosejs.com/)

## 支持

  - [Stack Overflow](http://stackoverflow.com/questions/tagged/mongoose)
  - [Bug Reports](https://github.com/Automattic/mongoose/issues/)
  - [Mongoose Slack Channel](http://slack.mongoosejs.io/)
  - [Help Forum](http://groups.google.com/group/mongoose-orm)
  - [MongoDB Support](https://docs.mongodb.org/manual/support/)

## 插件

访问 [插件搜索网站](http://plugins.mongoosejs.io/) 来查看社区的数百个相关模块。 接下来，从这个 [文档](http://mongoosejs.com/docs/plugins.html) 或者 [这篇博客](http://thecodebarbarian.com/2015/03/06/guide-to-mongoose-plugins) 学习如何编写自己的插件。

## 贡献

查看所有 300+ [贡献者](https://github.com/Automattic/mongoose/graphs/contributors)。也欢迎你称为一个[贡献者](https://github.com/Automattic/mongoose/blob/master/CONTRIBUTING.md)！

## 安装

先安装 [node.js](http://nodejs.cn/) 和 [mongodb](https://www.mongodb.org/downloads)。 然后:

```sh
$ npm install mongoose
```

## 稳定性

当前的稳定分支是 [master](https://github.com/Automattic/mongoose/tree/master)。[3.8.x](https://github.com/Automattic/mongoose/tree/3.8.x)  分支包含对遗留的 3.x 版本系列支持，在2015年9月之前不再处于积极的开发阶段。[3.8.x  文档](http://mongoosejs.com/docs/3.8.x/)仍然可用。

## 概述

### 连接 MongoDB

首先，我们需要定义一个连接。如果你的应用只使用一个数据库，你应该使用 `mongoose.connect`。 如果您需要创建其他连接，请使用 `mongoose.createConnection`。

`connect` 和 `createConnection` 都带有一个 `mongodb://` URI，或者参数 `host，database，port，options`。

```js
var mongoose = require('mongoose');

mongoose.connect('mongodb://localhost/my_database');
```

一旦连接后，`open` 事件在 `Connection` 实例上被触发。 如果你使用 `mongoose.connect`，`Connection`是 `mongoose.connection`。 否则，`mongoose.createConnection` 的返回值是 `Connection`。

**注意:** _如果本地连接失败，请尝试使用 127.0.0.1 而不是 localhost。当本地主机名已被更改时，有时可能会出现问题。_

**重要的!** Mongoose 缓存所有的命令，直到连接到数据库。这意味着您不必等到连接到 MongoDB 才能定义模型，运行查询等。

### 定义模型

模型是通过 `Schema` 接口定义的。

```js
var Schema = mongoose.Schema,
    ObjectId = Schema.ObjectId;

var BlogPost = new Schema({
    author    : ObjectId,
    title     : String,
    body      : String,
    date      : Date
});
```

除了定义文档的结构和存储的数据类型之外，Schema 还处理以下定义：

* [Validators](http://mongoosejs.com/docs/validation.html) (async and sync)
* [Defaults](http://mongoosejs.com/docs/api.html#schematype_SchemaType-default)
* [Getters](http://mongoosejs.com/docs/api.html#schematype_SchemaType-get)
* [Setters](http://mongoosejs.com/docs/api.html#schematype_SchemaType-set)
* [Indexes](http://mongoosejs.com/docs/guide.html#indexes)
* [Middleware](http://mongoosejs.com/docs/middleware.html)
* [Methods](http://mongoosejs.com/docs/guide.html#methods) definition
* [Statics](http://mongoosejs.com/docs/guide.html#statics) definition
* [Plugins](http://mongoosejs.com/docs/plugins.html)
* [pseudo-JOINs](http://mongoosejs.com/docs/populate.html)

下面的例子展示了这些特性:

```js
var Comment = new Schema({
  name: { type: String, default: 'hahaha' },
  age: { type: Number, min: 18, index: true },
  bio: { type: String, match: /[a-z]/ },
  date: { type: Date, default: Date.now },
  buff: Buffer
});

// a setter
Comment.path('name').set(function (v) {
  return capitalize(v);
});

// middleware
Comment.pre('save', function (next) {
  notify(this.get('email'));
  next();
});
```

看一下 `examples/schema.js` 中的例子，一个典型设置的端到端示例。

### 访问模型

一旦我们通过 `mongoose.model('ModelName', mySchema)` 定义了一个模型，我们可以通过相同的函数来访问它：

```js
var myModel = mongoose.model('ModelName');
```

或者只是一次性完成

```js
var MyModel = mongoose.model('ModelName', mySchema);
```

第一个参数是您的模型所使用的集合的*唯一*名称。**Mongoose 会自动寻找你的模型名称的*复数*版本**。例如，如果你使用

```js
var MyModel = mongoose.model('Ticket', mySchema);
```

然后，Mongoose 将为你的 __tickets__ 集合创建模型，而不是你的 __ticket__ 集合。

一旦我们有了模型，我们就可以实例化它，并保存它:

```js
var instance = new MyModel();
instance.my.key = 'hello';
instance.save(function (err) {
  //
});
```
或者我们可以从相同的集合中查找文档：

```js
MyModel.find({}, function (err, docs) {
  // docs.forEach
});
```

你也可以`findOne`、`findById`、`update`, 等等。 查看 [这个文档](http://mongoosejs.com/docs/queries.html) 获取更多细节。

**重要的!** 如果你使用 `mongoose.createConnection()` 打开一个单独的连接，但是尝试通过 `mongoose.model('ModelName')` 来访问模型，它不会像预期的那样工作，因为它没有连接到一个活动的数据库连接。在这种情况下，通过您创建的连接访问您的模型:

```js
var conn = mongoose.createConnection('your connection string'),
    MyModel = conn.model('ModelName', schema),
    m = new MyModel;
m.save(); // works
```

vs

```js
var conn = mongoose.createConnection('your connection string'),
    MyModel = mongoose.model('ModelName', schema),
    m = new MyModel;
m.save(); // 不会工作，因为默认的连接对象从未被使用
```

### 嵌入式文档

在第一个示例代码片段中，我们在 Schema 中定义了一个键，如下所示：

```
comments: [Comment]
```

其中 `Comment` 是我们创建的 `Schema`。 这意味着创建嵌入式文档就像下面这样简单：

```js
// 检索我的模型
var BlogPost = mongoose.model('BlogPost');

// 创建一篇博客文章
var post = new BlogPost();

// 创建一个评论
post.comments.push({ title: 'My comment' });

post.save(function (err) {
  if (!err) console.log('Success!');
});
```

删除它们也是一样的：

```js
BlogPost.findById(myId, function (err, post) {
  if (!err) {
    post.comments[0].remove();
    post.save(function (err) {
      // do something
    });
  }
});
```

嵌入式文档享有与您的模型相同的功能。 默认值、验证器、中间件。每当发生错误时，就会向 `save()` 错误回调冒泡，所以错误处理很简单！


### 中间件

查看 [文档](http://mongoosejs.com/docs/middleware.html) 页面。

#### 截取和修改方法参数

可以通过中间件截取方法的参数。

例如，每当有人在您的文档中 `set` 路径为新值时，这将允许您广播关于您的文档的更改：

```js
schema.pre('set', function (next, path, val, typel) {
  // `this` 指向当前文档
  this.emit('set', path, val);

  // 把控制权交给下一个 pre
  next();
});
```

此外，你可以改变传入的 `method` 参数，以便后续的中间件看到这些参数的不同值。 为此，只需将新值传递给 `next` 即可：

```js
.pre(method, function firstPre (next, methodArg1, methodArg2) {
  // Mutate methodArg1
  next("altered-" + methodArg1.toString(), methodArg2);
});

// pre declaration is chainable
.pre(method, function secondPre (next, methodArg1, methodArg2) {
  console.log(methodArg1);
  // => 'altered-originalValOfMethodArg1'

  console.log(methodArg2);
  // => 'originalValOfMethodArg2'

  // Passing no arguments to `next` automatically passes along the current argument values
  // i.e., the following `next()` is equivalent to `next(methodArg1, methodArg2)`
  // and also equivalent to, with the example method arg
  // values, `next('altered-originalValOfMethodArg1', 'originalValOfMethodArg2')`
  next();
});
```

#### Schema 疑难杂症

`type`在 Mongoose 中的 schema 被使用时有特殊的含义。 如果您的 schema 需要使用 `type` 作为嵌套属性，则必须使用对象表示法：

```js
new Schema({
  broken: { type: Boolean },
  asset: {
    name: String,
    type: String // uh oh, it broke. asset will be interpreted as String
  }
});

new Schema({
  works: { type: Boolean },
  asset: {
    name: String,
    type: { type: String } // works. asset is an object with a type property
  }
});
```

### 驱动程序访问

Mongoose 建立在[官方的 MongoDB Node.js 驱动程序](https://github.com/mongodb/node-mongodb-native) 之上。 每个 mongoose 模型都保留对 [原生 MongoDB 驱动程序集合](http://mongodb.github.io/node-mongodb-native/2.1/api/Collection.html) 的引用。 可以使用 `YourModel.collection` 访问集合对象。 然而，使用集合对象会直接绕过所有的 mongoose 特性，包括钩子，验证等。一个明显的例外是：`YourModel.collection` 仍然缓冲命令。因此，`YourModel.collection.find()` **不会**返回光标。

## API 文档

请参阅 [API 文档](http://mongoosejs.com/docs/api.html)，该文档由 [dox](https://github.com/tj/dox) 和 [acquit](https://github.com/vkarpov15/acquit) 生成。

## License

Copyright (c) 2010 LearnBoost &lt;dev@learnboost.com&gt;

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
