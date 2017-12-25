# Sub Docs（子文档）

子文档是嵌入在其他文档中的文档。在 Mongoose 中，这意味着您可以在其他模式中嵌套模式。Mongoose 有两个不同的子文档概念：子文档数组和单个嵌套的子文档。

```js
var childSchema = new Schema({ name: 'string' });

var parentSchema = new Schema({
  //子文档数组
  children: [childSchema],
  //单个嵌套的子文档。警告：单个嵌套的subdocs只能工作
  //在 mongoose >= 4.2.0
  child: childSchema
});
```

子文档与普通文档类似。嵌套模式可以具有[中间件](/Library/mongoose/docs/middleware.md)，[自定义验证逻辑](/Library/mongoose/docs/validation)，虚拟属性以及任何其他可以使用的顶级模式的特性。
主要区别是子文档**不会单独保存**，只要保存其顶级父文档即可保存。

```js
var Parent = mongoose.model('Parent', parentSchema);
var parent = new Parent({ children: [{ name: 'Matt' }, { name: 'Sarah' }] })
parent.children[0].name = 'Matthew';

// `parent.children[0].save()` 是一个空操作, 它会触发中间件
// 但实际上**不会**保存子文档。
// 你需要保存父文档。
parent.save(callback);
```

子文档像顶级文档一样保存和验证[中间件](/Library/mongoose/docs/middleware.md)。在父文档上调用 `save()` 会为其所有子文档触发 `save()` 中间件，对于 `validate()` 中间件也一样。

```js
childSchema.pre('save', function (next) {
  if ('invalid' == this.name) {
    return next(new Error('#sadpanda'));
  }
  next();
});

var parent = new Parent({ children: [{ name: 'invalid' }] });
parent.save(function (err) {
  console.log(err.message) // #sadpanda
});
```

子文档的 `pre('save')`和 `pre('validate')` 中间件在顶层文档的 `pre('save')` 之前执行，而在顶层文档的 `pre('validate')` 中间件之后执行。这是因为在 `save()` 之前进行的验证实际上是一个内置的中间件。

```js
// 下面的代码将按顺序输出 1-4
var childSchema = new mongoose.Schema({ name: 'string' });

childSchema.pre('validate', function(next) {
  console.log('2');
  next();
});

childSchema.pre('save', function(next) {
  console.log('3');
  next();
});

var parentSchema = new mongoose.Schema({
  child: childSchema,
});

parentSchema.pre('validate', function(next) {
  console.log('1');
  next();
});

parentSchema.pre('save', function(next) {
  console.log('4');
  next();
});
```

## 查找子文档

默认情况下，每个子文档都有一个 `_id`。 Mongoose 文档数组有一个特殊的 [id](http://mongoosejs.com/docs/api.html#types_documentarray_MongooseDocumentArray-id) 方法，用于搜索文档数组以找到具有给定 `_id` 的文档。

```js
var doc = parent.children.id(_id);
```
## 将子文档添加到数组

MongooseArray 方法，诸如 [push](http://mongoosejs.com/docs/api.html#types_array_MongooseArray.push)
，[unshift](http://mongoosejs.com/docs/api.html#types_array_MongooseArray.unshift)，[addToSet](http://mongoosejs.com/docs/api.html#types_array_MongooseArray.addToSet)
和其他透明地将参数转换为正确的类型：

```js
var Parent = mongoose.model('Parent');
var parent = new Parent;

// create a comment
parent.children.push({ name: 'Liesl' });
var subdoc = parent.children[0];
console.log(subdoc) // { _id: '501d86090d371bab2c0341c5', name: 'Liesl' }
subdoc.isNew; // true

parent.save(function (err) {
  if (err) return handleError(err)
  console.log('Success!');
});
```

也可以使用 MongooseArrays 的 [`create`](http://mongoosejs.com/docs/api.html#types_documentarray_MongooseDocumentArray.create) 方法将子文档添加到数组中，创建子文档。

```js
var newdoc = parent.children.create({ name: 'Aaron' });
```

## 删除子目录

每个子文档都有自己的 [`remove`](http://mongoosejs.com/docs/api.html#types_embedded_EmbeddedDocument-remove) 方法。对于数组子文档，这相当于在子文档上调用 `.pull()`。对于单个嵌套的子文档，`remove()` 相当于将子文档设置为 `null`。

//相当于`parent.children.pull（_id）`
parent.children.id（_id）卸下摆臂（）;
//相当于`parent.child = null`
parent.child.remove（）;
parent.save（function（err）{
  如果（err）返回handleError（err）;
  console.log（'subdocs被删除'）;
}）;

```js
// 相当于 `parent.children.pull(_id)`
parent.children.id(_id).remove();
// 相当于  `parent.child = null`
parent.child.remove();
parent.save(function (err) {
  if (err) return handleError(err);
  console.log('the subdocs were removed');
});
```

## 数组的替代声明语法

如果使用对象数组创建模式，mongoose 会自动将对象转换为模式：

```js
var parentSchema = new Schema({
  children: [{ name: 'string' }]
});
// 等价
var parentSchema = new Schema({
  children: [new Schema({ name: 'string' })]
});
```

## 接下来

现在我们已经介绍了Sub-documents，让我们看看 [querying](/Library/mongoose/docs/queries.md)。
