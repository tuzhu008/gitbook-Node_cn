# Documents（文档）

Mongoose [文档](http://mongoosejs.com/docs/api.html#document-js) 代表了存储在 MongoDB 中的文档的一对一映射。每个文档都是其 [Model](/Library/mongoose/docs/models.md) 的一个实例。

## 检索

有很多方法可以从 MongoDB 中检索文档。我们不会在这一节中介绍。查看关于[查询](/Library/mongoose/docs/queries.md)细节的章节。

## 更新

有许多方法可以更新文件。我们首先看一下使用 [`findById`](http://mongoosejs.com/docs/api.html#model_Model.findById) 的传统方法：

```js
Tank.findById(id, function (err, tank) {
  if (err) return handleError(err);

  tank.size = 'large';
  tank.save(function (err, updatedTank) {
    if (err) return handleError(err);
    res.send(updatedTank);
  });
});
```

您也可以使用 [`.set()`](http://mongoosejs.com/docs/api.html#document_Document-set) 来修改文档。在后台，`tank.size ='large';` 变成 `tank.set({size: 'large'})`。

```js
Tank.findById(id, function (err, tank) {
  if (err) return handleError(err);

  tank.set({ size: 'large' });
  tank.save(function (err, updatedTank) {
    if (err) return handleError(err);
    res.send(updatedTank);
  });
});
```

这种方法首先从 Mongo 检索文档，然后发出更新命令（通过调用 `save` 触发）。但是，如果我们不需要在我们的应用程序中返回的文档，而只是想直接更新数据库中的属性，[`Model#update`](http://mongoosejs.com/docs/api.html#model_Model.update) 更新适合我们：

```js
Tank.update({ _id: id }, { $set: { size: 'large' }}, callback);
```

如果我们确实需要在我们的应用程序中返回的文档，还有另外一个更好的选择：

```js
Tank.findByIdAndUpdate(id, { $set: { size: 'large' }}, { new: true }, function (err, tank) {
  if (err) return handleError(err);
  res.send(tank);
});
```
`findAndUpdate` / `Remove` 静态方法最多只对一个文档进行更改，只需对数据库进行一次调用即可将其返回。 [findAndModify](http://www.mongodb.org/display/DOCS/findAndModify+Command) 主题[有](http://mongoosejs.com/docs/api.html#model_Model.findByIdAndRemove)[几个](http://mongoosejs.com/docs/api.html#model_Model.findOneAndUpdate)[变体](http://mongoosejs.com/docs/api.html#model_Model.findOneAndRemove)。阅读 [API](http://mongoosejs.com/docs/api.html) 文档以获取更多细节。

_注意: `findAndUpdate` / `Remove` 在数据库中进行更改之前不执行任何钩子或验证。您可以使用 [`runValidators` 选项](http://mongoosejs.com/docs/validation.html#update-validators)访问文档验证的有限子集。但是，如果您需要钩子和完整文档验证，请首先查询文档，然后 `save()`。

## 验证

文件在被保存之前被验证。阅读 [API](http://mongoosejs.com/docs/api.html#document_Document-validate) 文档或[验证](http://mongoosejs.com/docs/validation.html)章节获取更多细节。

## 覆盖

您可以使用 `.set()` 重写整个文档。如果要更改在[中间件](/Library/mongoose/docs/middleware.md)中保存的文档，这很方便。

```js
Tank.findById(id, function (err, tank) {
  if (err) return handleError(err);
  // Now `otherTank` is a copy of `tank`
  otherTank.set(tank);
});
```

## 接下来

现在我们已经介绍了 Documents，让我们来看看 [Sub-documents](/Library/mongoose/docs/subdocs.md)。
