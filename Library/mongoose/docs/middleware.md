# Midlleware（中间件）

中间件（也称为前后钩子）是在异步函数执行期间控制传递的函数。中间件是在模式级别指定的，这对编写[插件](/Library/mongoose/docs/plugins.md)很有用。 Mongoose 4.x 有四种类型的中间件：文档中间件，模型中间件，聚合（aggregate）中间件和查询中间件。文档中间件支持以下文档函数。 在文档中间件函数中，`this` 指向指文档。

  * [init](http://mongoosejs.com/docs/api.html#document_Document-init)
  * [validate](http://mongoosejs.com/docs/api.html#document_Document-validate)
  * [save](http://mongoosejs.com/docs/api.html#model_Model-save)
  * [remove](remove)

查询中间件支持以下 Model 和 Query 函数。在查询中间件函数中，`this` 指向的是查询。

  * [count](http://mongoosejs.com/docs/api.html#query_Query-count)
  * [find](http://mongoosejs.com/docs/api.html#query_Query-find)
  * [findOne](http://mongoosejs.com/docs/api.html#query_Query-findOne)
  * [findOneAndRemove](http://mongoosejs.com/docs/api.html#query_Query-findOneAndRemove)
  * [findOneAndUpdate](http://mongoosejs.com/docs/api.html#query_Query-findOneAndUpdate)
  * [update](http://mongoosejs.com/docs/api.html#query_Query-update)

聚合(Aggregate)中间件用于 `MyModel.aggregate()`。聚合中间件在集合对象上调用 `exec()` 时被执行。在聚合中间件中，`this` 指的是[聚合对象(aggregation object)](http://mongoosejs.com/docs/api.html#model_Model.aggregate)。

  * [aggregate](http://mongoosejs.com/docs/api.html#model_Model.aggregate)


模型中间件支持以下模型函数。在模型中间件函数中，`this` 指向模型。

  * [insertMany](http://mongoosejs.com/docs/api.html#model_Model.insertMany)

所有中间件类型都支持`pre`和 `post` 钩子。下面将更详细地描述前后钩子如何工作。

**注意：**`remove()` 没有查询钩子，查询钩子仅用于文档。如果您设置了 `remove` 钩子，则在调用 `myDoc.remove()` 时将会触发它，而不是在调用 `MyModel.remove()` 时触发。**注意：**`create()` 函数触发 `save()`钩子。

## Pre

有两种类型的 pre 钩子，串行(Serial)和并行(Parallel)。

### 串行

当每个中间件调用 `next`时，串行中间件函数被一个接一个地执行。

```js
var schema = new Schema(..);
schema.pre('save', function(next) {
  // do stuff
  next();
});
```

`next()` 调用**不会**阻止中间件函数中的其他代码执行。在调用 `next()`时，使用[提前 `return` 模式](https://www.bennadel.com/blog/2323-use-a-return-statement-when-invoking-callbacks-especially-in-a-guard-statement.htm)来防止其他中间件函数运行。

```js
var schema = new Schema(..);
schema.pre('save', function(next) {
  if (foo()) {
    console.log('calling next!');
    // `return next();` 确保该函数的其余部分不会，运行
    /*return*/ next();
  }
  // 除非取消上面的 `return` 进行注释，否则 'after next' 会打印出来
  console.log('after next');
});
```

## 并行

并行中间件提供更细粒度的流量控制。

```js
var schema = new Schema(..);

// `true` 表示这是一个并行的中间件。means this is a parallel middleware. You **must** specify `true`
// 如果你想使用并行中间件，你必须指定 `true` 作为第二个参数
schema.pre('save', true, function(next, done) {
  // 调用 next 并行开始下一个中间件
  next();
  setTimeout(done, 100);
});
```
这个钩子方法，在这种情况下 `save`，将不被执行，直到每个中间件 `done` 时被调用。

## 用例

中间件对于原子化模型逻辑和避免嵌套的异步代码块非常有用。这里有一些其他的想法：

* 复杂的验证
* 删除依赖文档
  - （删除用户删除他的所有博客帖子）
* 异步默认值
* 异步任务，某个动作触发
  - 触发自定义事件
  - 通知


### 错误处理

如果任何中间件使用一个 `Error` 类型的参数调用 `next` 或 `done`，则流程中断，并将错误传递给回调。

```js
schema.pre('save', function(next) {
  // You **must** do `new Error()`. `next('something went wrong')` will
  // **not** work
  var err = new Error('something went wrong');
  next(err);
});

// later...

myDoc.save(function(err) {
  console.log(err.message) // something went wrong
});
```

## Post 中间件

[post](http://mongoosejs.com/docs/api.html#schema_Schema-post) 中间件在钩子方法及其所有的 `pre` 中间件完成后执行。`post` 中间件不直接接收流控制，例如，没有 `next` 或 `done` 的回调传递给它。 `post` 钩子是为这些方法注册传统事件监听器的一种方法。

```js
schema.post('init', function(doc) {
  console.log('%s has been initialized from the db', doc._id);
});
schema.post('validate', function(doc) {
  console.log('%s has been validated (but not saved yet)', doc._id);
});
schema.post('save', function(doc) {
  console.log('%s has been saved', doc._id);
});
schema.post('remove', function(doc) {
  console.log('%s has been removed', doc._id);
});
```

## 异步 post 钩子

虽然 `post` 中间件没有收到流控制，但您仍然可以确保异步 `post` 钩子接按预定义的顺序执行。如果你的 `post` 钩子函数至少需要 2 个参数，mongoose 会假定第二个参数是 `next()` 函数，你将调用它来触发序列中的下一个中间件。

```js
// 需要2个参数：这是一个异步的 post 钩子
schema.post('save', function(doc, next) {
  setTimeout(function() {
    console.log('post1');
    // 启动第二个 post 钩子
    next();
  }, 10);
});

// 直到第一个中间件调用next()
schema.post('save', function(doc, next) {
  console.log('post2');
  next();
});
```

## Save/Validate 钩子


`save()` 函数会触发 `validate()` 钩子，因为 mongoose 有一个内置的 `pre('save')` 钩子来调用 `validate()`。这意味着所有 `pre('validate')` 和  `post('validate')` 钩子在任何 `pre('save')` 钩子**之前**被调用。

```js
schema.pre('validate', function() {
  console.log('this gets printed first');
});
schema.post('validate', function() {
  console.log('this gets printed second');
});
schema.pre('save', function() {
  console.log('this gets printed third');
});
schema.post('save', function() {
  console.log('this gets printed fourth');
});
```


## findAndUpdate()和查询中间件

`save()` 钩子**不会**在 `update()`，`findOneAndUpdate()`等上被执行。您可以在[此 GitHub 问题](http://github.com/Automattic/mongoose/issues/964)中看到更详细的讨论。 Mongoose 4.0 对这些函数有不同的钩子。

```js
schema.pre('find', function() {
  console.log(this instanceof mongoose.Query); // true
  this.start = Date.now();
});

schema.post('find', function(result) {
  console.log(this instanceof mongoose.Query); // true
  // prints returned documents
  console.log('find() returned ' + JSON.stringify(result));
  // prints number of milliseconds the query took
  console.log('find() took ' + (Date.now() - this.start) + ' millis');
});
```

查询中间件与文档中间件有着微妙而重要的区别：在文档中间件中，`this` 指向正在更新的文档。在查询中间件中，mongoose 不一定具有对被更新文档的引用，所以 `this` 指向查询对象而不是被更新的文档。

例如，如果你想为每个 `update()` 调用添加一个 `updatedAt` 时间戳，你可以使用下面的 pre 钩子。

```js
schema.pre('update', function() {
  this.update({},{ $set: { updatedAt: new Date() } });
});
```

## 错误处理中间件

4.5.0 新增特性

中间件执行通常会在第一次中间件使用错误调用 `next` 时停止。但是，有一种称为“错误处理中间件”的特殊 post 中间件，当发生错误时会执行该中间件。

错误处理中间件被定义为带有一个额外参数的中间件—— `error`，它作为函数的第一个参数出现。然后，错误处理中间件可以转换您想要的错误。

```js
var schema = new Schema({
  name: {
    type: String,
    // 当您保存一个副本时，将触发一个带有代码 11000 的 MongoError
    unique: true
  }
});

// 处理函数 **必须** 有 3 个参数: 发生的错误、出现问题的文档、和 `next()` 函数
schema.post('save', function(error, doc, next) {
  if (error.name === 'MongoError' && error.code === 11000) {
    next(new Error('There was a duplicate key error'));
  } else {
    next(error);
  }
});

// 将触发 `post('save')` 错误处理函数
Person.create([{ name: 'Axl Rose' }, { name: 'Axl Rose' }]);
```

错误处理中间件也可以与查询中间件一起工作。你也可以定义一个post `update()` 钩子来捕获 MongoDB 的重复键错误。

```js
//当你调用 update() 时，会发生同样的 E11000 错误
//这个函数 **必须** 取 3 个参数。
//如果你使用 `passRawResult` 函数，这个函数**必须**有 4 个参数
schema.post('update', function(error, res, next) {
  if (error.name === 'MongoError' && error.code === 11000) {
    next(new Error('There was a duplicate key error'));
  } else {
    next(error);
  }
});

var people = [{ name: 'Axl Rose' }, { name: 'Slash' }];
Person.create(people, function(error) {
  Person.update({ name: 'Slash' }, { $set: { name: 'Axl Rose' } }, function(error) {
    // `error.message` 将为 "There was a duplicate key error"
  });
});
```

## 接下来

现在我们已经介绍了 Midlleware，让我们来看看 Mongoose 使用 [population](/Library/mongoose/docs/populate.md) 助手来伪造 JOINs。
