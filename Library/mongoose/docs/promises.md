# 内置的 Promises

Mongoose 异步操作，如 `.save()` 和查询，返回符合  [Promises/A+ 的 promises](https://promisesaplus.com/)。这意味着您可以执行像 `MyModel.findOne({}).then()`和 `yield MyModel.findOne({}).exec()`（如果使用的是 [co](https://www.npmjs.com/package/co)）。

为了向后兼容，Mongoose 4 默认返回 [mpromise](https://www.npmjs.com/package/mpromise) promise。

```js
var gnr = new Band({
  name: "Guns N' Roses",
  members: ['Axl', 'Slash']
});

var promise = gnr.save();
assert.ok(promise instanceof require('mpromise'));

promise.then(function (doc) {
  assert.equal(doc.name, "Guns N' Roses");
});
```

## 查询不是 promises

mongoose 的查询**不是**promises。但是，它们对 `yield` 和 `async /await` 有 `.then()` 函数。如果您需要完整的 promise，请使用 `.exec() ` 函数。

```js
var query = Band.findOne({name: "Guns N' Roses"});
assert.ok(!(query instanceof require('mpromise')));

// A query is not a fully-fledged promise, but it does have a `.then()`.
query.then(function (doc) {
 // use doc
});

// `.exec()` gives you a fully-fledged promise
var promise = query.exec();
assert.ok(promise instanceof require('mpromise'));

promise.then(function (doc) {
 // use doc
});
```
  
## 插入自己的承诺库

Mongoose 4.1.0 中的新功能

虽然 mpromise 已经足够用于基本用例，但是高级用户可能希望插入像 [bluebird](https://www.npmjs.com/package/bluebird) 这样的最受欢迎的的 [ES6 风格的 promise 库](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)，或者使用原生 ES6 promise。只要设置 `mongoose.Promise` 为到你最喜欢的ES6风格的 pomise 构造，mongoose 将使用它。

Mongoose 测试使用的是 ES6 原生 promise，[bluebird](https://www.npmjs.com/package/bluebird) 和 [q](https://www.npmjs.com/package/q)。任何导出 ES6 风格的 promise 构造函数的 promise 库都理论上都能正常工作，但理论往往与实践有所不同。如果您发现错误，请在 [GitHub上打开一个问题](https://github.com/Automattic/mongoose/issues)。

```js
var query = Band.findOne({name: "Guns N' Roses"});

// Use native promises
mongoose.Promise = global.Promise;
assert.equal(query.exec().constructor, global.Promise);

// Use bluebird
mongoose.Promise = require('bluebird');
assert.equal(query.exec().constructor, require('bluebird'));

// Use q. Note that you **must** use `require('q').Promise`.
mongoose.Promise = require('q').Promise;
assert.ok(query.exec() instanceof require('q').makePromise);

```
  
## 适用于 MongoDB 驱动程序的 Promises

`mongoose.Promise` 属性设置 mongoose 使用的 promises。但是，这不会影响底层的 MongoDB 驱动程序。如果使用底层驱动程序（例如 `Model.collection.db.insert()`），则需要做一些额外的工作来更改底层的 promise 库。请注意，下面的代码假定 mongoose >= 4.4.4。

```js
var uri = 'mongodb://localhost:27017/mongoose_test';
// Use bluebird
var options = { promiseLibrary: require('bluebird') };
var db = mongoose.createConnection(uri, options);

Band = db.model('band-promises', { name: String });

db.on('open', function() {
 assert.equal(Band.collection.findOne().constructor, require('bluebird'));
});
```
