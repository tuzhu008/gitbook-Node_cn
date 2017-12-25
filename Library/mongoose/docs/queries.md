# Queries（查询）

文档可以通过[模型](/Library/mongoose/docs/models.md)的几个静态辅助方法来检索。

[涉及](http://mongoosejs.com/docs/api.html#model_Model.find)
[指定](http://mongoosejs.com/docs/api.html#model_Model.findById)
[查询](http://mongoosejs.com/docs/api.html#model_Model.count)
[条件](http://mongoosejs.com/docs/api.html#model_Model.count)
的任何
[模型方法](http://mongoosejs.com/docs/api.html#model_Model)

可以通过两种方式执行：

当一个回调函数：

  * 被传递时，操作将立即执行，并将结果传递给回调函数。
  * 不传递，则返回一个 [Query](http://mongoosejs.com/docs/api.html#query-js) 实例，它提供了一个特殊的查询生成器接口。

> **[info]**
>
> 在 mongoose 4中， [Query](http://mongoosejs.com/docs/api.html#query-js)  有一个 `.then()` 函数，因此可以作为一个 promise 来使用。

执行一个带有回调函数的查询时，可以将查询指定为 JSON 文档。 JSON 文档的语法与 [MongoDB shell](http://docs.mongodb.org/manual/tutorial/query-documents/) 相同。

```js
var Person = mongoose.model('Person', yourSchema);

// 查找每一个last name 为 'Ghost' 的人, 选择  `name` 和 `occupation` 字段
Person.findOne({ 'name.last': 'Ghost' }, 'name occupation', function (err, person) {
  if (err) return handleError(err);
  console.log('%s %s is a %s.', person.name.first, person.name.last, person.occupation) // Space Ghost is a talk show host.
})
```

在这里，我们看到查询被立即执行，结果传递给我们的回调。 Mongoose 中的所有回调都使用模式：`callback(error，result)`。如果执行查询时发生错误，`error` 参数将包含错误文档，`result` 将为空。如果查询成功，则 `error` 参数将为空，`result` 将填充查询结果。

> **[info]**
>
> 在 Mongoose 中，任何地方都会传递给查询的一个回调，这个回调都遵循模式回调 `callback(error, results)`。什么 `result` 取决于操作：
> 对于 `findOne()`，它是一个[可能为 null 的单个文档](http://mongoosejs.com/docs/api.html#model_Model.update)，
> `find()` [一个文档列表](http://mongoosejs.com/docs/api.html#model_Model.find)，
> `count()` [文档数量](http://mongoosejs.com/docs/api.html#model_Model.count)，
> `update()` 为[受影响的文档数量](http://mongoosejs.com/docs/api.html#model_Model.count)等。
> [API 文档为模型](http://mongoosejs.com/docs/api.html#model-js)提供了有关传递给回调函数的更多细节。

现在让我们来看看在没有回调被传递的的情况下会发生什么：

```js
// 找到每个 last name 匹配 'Ghost' 的人
var query = Person.findOne({ 'name.last': 'Ghost' });

// 选择 `name` 和 `occupation` 字段
query.select('name occupation');

// 稍后执行查询
query.exec(function (err, person) {
  if (err) return handleError(err);
  console.log('%s %s is a %s.', person.name.first, person.name.last, person.occupation) // Space Ghost is a talk show host.
})
```

在上面的代码中，查询变量是 [Query](http://mongoosejs.com/docs/api.html#query-js) 类型的。查询使您能够使用**链式**语法构建查询，而不是指定 JSON 对象。下面的两个例子是等价的。

```js
// With a JSON doc
Person.
  find({
    occupation: /host/,
    'name.last': 'Ghost',
    age: { $gt: 17, $lt: 66 },
    likes: { $in: ['vaporizing', 'talking'] }
  }).
  limit(10).
  sort({ occupation: -1 }).
  select({ name: 1, occupation: 1 }).
  exec(callback);

// Using query builder
Person.
  find({ occupation: /host/ }).
  where('name.last').equals('Ghost').
  where('age').gt(17).lt(66).
  where('likes').in(['vaporizing', 'talking']).
  limit(10).
  sort('-occupation').
  select('name occupation').
  exec(callback);
```
  
查询辅助器函数的完整列表可以在[API文档](http://mongoosejs.com/docs/api.html#query-js)中找到。

在 4.x 中，setter 默认不会被执行。例如，如果您在模式中使用小写的电子邮件：

```js
var personSchema = new Schema({
  email: {
    type: String,
    lowercase: true
  }
});
```
Mongoose 不会自动小写查询中的电子邮件，所以 `Person.find({ email: 'Val@karpov.io' })` 将不会返回任何结果。使用 `runSettersOnQuery` 选项来打开这个行为：

```js
var personSchema = new Schema({
  email: {
    type: String,
    lowercase: true
  }
}, { runSettersOnQuery: true });
```

## 引用其他文件

MongoDB 中没有 joins，但有时候我们仍然需要引用其他集合中的文档。这是 [population](/Library/mongoose/docs/populate.html) 进来的地方。在[这里](http://mongoosejs.com/docs/api.html#query_Query-populate)阅读更多关于如何在您的查询结果中包含来自其他集合的文档。

## 流

您可以从 MongoDB [流式](http://nodejs.org/api/stream.html)传输查询结果。
您需要调用 [`Query#cursor()`](http://mongoosejs.com/docs/api.html#query_Query-cursor) 函数
而不是 [`Query#exec()`](http://mongoosejs.com/docs/api.html#query_Query-exec) 来返回
[QueryCursor](http://mongoosejs.com/docs/api.html#querycursor-js) 的一个实例。

```js
var cursor = Person.find({ occupation: /host/ }).cursor();
cursor.on('data', function(doc) {
  // 为每个文档调用一次
});
cursor.on('close', function() {
  // 完成时被调用
});
```
## 接下来

现在我们已经介绍了 Queries，我们来看看 [validation](/Library/mongoose/docs/validation.md)。
