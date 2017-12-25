# Models（模型）

[Model]() 是从我们的模式定义编译后的奇特的构造函数。这些模型的实例代表文档，文档可以被保存，可以被从数据库查找。从数据库中创建和检索所有文档都由这些模型处理。

## 编译你的第一个模型：

```js
var schema = new mongoose.Schema({ name: 'string', size: 'string' });
var Tank = mongoose.model('Tank', schema);
```

第一个参数是你的模型的集合的单数名称。 **mongoose 自动寻找您的模型名称的复数版本。** 因此，对于上面的例子，模型 Tank 是用于数据库中 tanks 的收集。 `.model()` 函数生成『模式』的副本。在调用 `.model()` 之前，确保你已经添加了你想要的模式。

## 构造文档

[文档](/Library/mongoose/docs/documents.md) 是模型的实例。创建它们并保存到数据库非常简单：

```js
var Tank = mongoose.model('Tank', yourSchema);

var small = new Tank({ size: 'small' });
small.save(function (err) {
  if (err) return handleError(err);
  // saved!
})

// or

Tank.create({ size: 'small' }, function (err, small) {
  if (err) return handleError(err);
  // saved!
})
```

请注意，除非您的模型使用的连接打开，否则不会有 tank 被创建/移除。每个模型都有一个关联的连接。当你使用 `mongoose.model()` 时，你的模型将使用默认的 mongoose 连接。

```js
mongoose.connect('localhost', 'gettingstarted');
```

如果您创建自定义连接，请改用该连接的 `model()` 函数。「译者注」：一个是 `mongoose.model`、一个是 `connection.modele`。

```js
var connection = mongoose.createConnection('mongodb://localhost:27017/test');
var Tank = connection.model('Tank', yourSchema);
```

## 查询

使用 Mongoose 查找文档很容易，它支持 MongoDB [丰富的](http://www.mongodb.org/display/DOCS/Advanced+Queries)查询语法。可以使用每个模型 [find](http://mongoosejs.com/docs/api.html#model_Model.find)，[findById](http://mongoosejs.com/docs/api.html#model_Model.findById)，[findOne](http://mongoosejs.com/docs/api.html#model_Model.findOne) 或 [where](http://mongoosejs.com/docs/api.html#model_Model.where) 静态方法来检索文档。

```js
Tank.find({ size: 'small' }).where('createdDate').gt(oneYearAgo).exec(callback);
```
有关如何使用 [Query](/http://mongoosejs.com/docs/api.html#query-js) API的更多详细信息，请参阅[查询](/Library/mongoose/docs/queries.html)一章。

## 删除

模型有一个静态的 `remove` 方法可用于删除所有文件匹配条件。

```js
Tank.remove({ size: 'large' }, function (err) {
  if (err) return handleError(err);
  // removed!
});
```


## 更新

每个模型都有其自己的更新方法，用于修改数据库中的文档而不将它们返回到应用程序。有关更多详细信息，请参阅 [API](http://mongoosejs.com/docs/api.html#model_Model.update) 文档。

如果要更新数据库中的单个文档并将其返回给您的应用程序，请改为使用 [findOneAndUpdate](http://mongoosejs.com/docs/api.html#model_Model.findOneAndUpdate)。

## 还有更多

[API](http://mongoosejs.com/docs/api.html#model_Model.update) 文档涵盖了许多其他可用的方法，如 [count](http://mongoosejs.com/docs/api.html#model_Model.count)，[mapReduce](http://mongoosejs.com/docs/api.html#model_Model.mapReduce)，[aggregate](http://mongoosejs.com/docs/api.html#model_Model.aggregate) [等](http://mongoosejs.com/docs/api.html#model_Model.findOneAndRemove)。

## 接下来

现在我们已经介绍了 Models，让我们来看看 [Documents](/Library/mongoose/docs/documents.md)。
