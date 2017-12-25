# Population

MongoDB 在 > = 3.2 版本中具有类似 join 的 [`$lookup`](https://docs.mongodb.com/manual/reference/operator/aggregation/lookup/) 聚合操作符。Mongoose 有一个更强大的替代方法叫做 `populate()`，它可以让你引用其他集合中的文档。

Population 是使用其他集合中的文档自动替换文档中的指定路径的过程。我们可以填充单个文档，多个文档，普通对象，多个普通对象或从查询返回的所有对象。我们来看一些例子。

```js
var mongoose = require('mongoose');
var Schema = mongoose.Schema;

var personSchema = Schema({
  _id: Schema.Types.ObjectId,
  name: String,
  age: Number,
  stories: [{ type: Schema.Types.ObjectId, ref: 'Story' }]
});

var storySchema = Schema({
  author: { type: Schema.Types.ObjectId, ref: 'Person' },
  title: String,
  fans: [{ type: Schema.Types.ObjectId, ref: 'Person' }]
});

var Story = mongoose.model('Story', storySchema);
var Person = mongoose.model('Person', personSchema);
```

到目前为止，我们创建了两个[模型](/Library/mongoose/docs/models.md)。我们的 Person 模型的 `stories` 被设置为一个 `ObjectIds` 数组。 `ref` 选项告诉 Mongoose 在 population 中使用哪个模型，在我们的案例中是 `Story` 模型。我们在这里存储的所有 `_id` 必须是来自 `Story` 模型的文档 `_id`。

> **[info] 注意**
>
> `ObjectId`，`Number`，`String` 和 `Buffer` 作为 `ref` 是有效的。但是，除非您是高级用户，否则应该使用 `ObjectId`，并且有足够的理由这么做。

## 保存 ref

保存引用(`ref`)的其他文档的方式与通常保存属性的方式相同，只需指定 `_id` 值即可：

```js
var author = new Person({
  _id: new mongoose.Types.ObjectId(),
  name: 'Ian Fleming',
  age: 50
});

author.save(function (err) {
  if (err) return handleError(err);

  var story1 = new Story({
    title: 'Casino Royale',
    author: author._id    // assign the _id from the person
  });

  story1.save(function (err) {
    if (err) return handleError(err);
    // thats it!
  });
});
```

## Population

到目前为止，我们没有做太多的改变。我们只是创造了一 `Person` 和一个 `Story`。现在我们来看看使用查询生成器来填充(populate)故事的作者：

```js
Story.
  findOne({ title: 'Casino Royale' }).
  populate('author').
  exec(function (err, story) {
    if (err) return handleError(err);
    console.log('The author is %s', story.author.name);
    // prints "The author is Ian Fleming"
  });
```

已填充（populated）的路径不再设置为它们的原始 `_id`，它们的值由被返回的 mongoose 文档替代，这个文档来自于在数据库中执行的一个独立地查询，然后返回查询结果。



ref 数组的工作方式相同。只要在查询上调用 [`populate`](http://mongoosejs.com/docs/api.html#query_Query-populate) 方法，将返回一个文档数组来代替原始的 `_id`。

> **注意：**mongoose >= 3.6 通过[`document#populated()``](http://mongoosejs.com/docs/api.html#document_Document-populated)方法暴露了在 population 中使用的原始 `_id`。

## 设置填充的字段

在 Mongoose >= 4.0 中，也可以手动填充一个字段。

```js
Story.findOne({ title: 'Casino Royale' }, function(error, story) {
  if (error) {
    return handleError(error);
  }
  // author 是一个文档
  story.author = author;
  console.log(story.author.name); // prints "Ian Fleming"
});
```

请注意，这只适用于单个引用。您目前**无法**手动填充引用数组。

## 字段选择

如果我们只想要为填充的文档返回一些特定的字段呢？这可以通过将通常的[字段名称语法](http://mongoosejs.com/docs/api.html#query_Query-select)作为第二个参数传递给 `populate` 方法来实现：

```js
Story.
  findOne({ title: /casino royale/i }).
  populate('author', 'name'). // 只返回 Persons name
  exec(function (err, story) {
    if (err) return handleError(err);

    console.log('The author is %s', story.author.name);
    // prints "The author is Ian Fleming"

    console.log('The authors age is %s', story.author.age);
    // prints "The authors age is null'
  })
```

## 填充多个路径

如果我们想同时填充多个路径呢？

```js
Story.
  find(...).
  populate('fans').
  populate('author').
  exec()
```

如果使用相同的路径多次调用 `populate()`，则只有最后一个会生效。

```js
//下面的第二个 `populate()` 调用覆盖第一个，因为它们
//都填充 “fans”。
Story.
  find().
  populate({ path: 'fans', select: 'name' }).
  populate({ path: 'fans', select: 'email' });
// 以上相当于：
Story.find().populate({ path: 'fans', select: 'email' });
```

## 查询条件和其他选项

如果我们想根据他们的年龄来填充我们的 fans 数组，只选择他们的名字，最多只能返回 5 个粉丝？

```js
Story.
  find(...).
  populate({
    path: 'fans',
    match: { age: { $gte: 21 }},
    // 明确地排除 `_id`, 参见 http://bit.ly/2aEfTdB
    select: 'name -_id',
    options: { limit: 5 }
  }).
  exec()
```

## 引用 children

但是，我们可能会发现，如果我们使用 `author` 对象，我们无法获得这些故事的列表。这是因为没有 `story` 对象被“推”到   `author.stories`。

这里有两个观点。首先，您可能希望 `author` 知道哪些故事是他们的。通常情况下，您的模式应该通过在 “many” 中有一个父指针来解决一对多(on-to-many)的关系。但是，如果您有充足的理由需要一个子指针数组，则可以将文档 `push()` 到数组中，如下所示。

```js
author.stories.push(story1);
author.save(callback);
```

这使我们能够执行 `find` 和 `populate` 组合：

```js
Person.
  findOne({ name: 'Ian Fleming' }).
  populate('stories'). // only works if we pushed refs to children
  exec(function (err, person) {
    if (err) return handleError(err);
    console.log(person);
  });
```

> **[info]**
>
> 我们真的想要两套指针是有争议的，因为它们可能不同步。相反，我们可以跳过填充和直接 `find` 我们感兴趣的故事。

```js
Story.
  find({ author: author._id }).
  exec(function (err, stories) {
    if (err) return handleError(err);
    console.log('The stories are an array: ', stories);
  });
```

> **[info]**
>
> 从 [query population](http://mongoosejs.com/docs/api.html#query_Query-populate) 返回的文档变得功能齐全，可以 `remove`，可以 `save` 文档，除非指定了 [`lean`](http://mongoosejs.com/docs/api.html#query_Query-lean) 选项。不要将它们与[子文档](/Library/mongoose/docs/subdocs.md)混淆。调用它的 `remove` 方法时要小心，因为您将从数据库中删除它，而不仅仅是数组。

## 填充现有的文档

如果我们有一个现有的 mongoose 文档，并且想要填充它的一些路径，mongoose >= 3.6 支持 [document#populate()](http://mongoosejs.com/docs/api.html#document_Document-populate) 方法。

## 填充多个现有的文件

如果我们有一个或多个 mongoose 文件，甚至是简单的对象（*比如 [mapReduce](http://mongoosejs.com/docs/api.html#model_Model.mapReduce) 输出*），我们可以使用 mongoose >= 3.6 中提供的 `Model.populate()` 方法来填充它们。这是什么 `document#populate()` 和 `query#populate() ` 用来填充文档的方法。

## 多级填充

假设你有一个保持用户对其朋友的追踪的模式。

```js
var userSchema = new Schema({
  name: String,
  friends: [{ type: ObjectId, ref: 'User' }]
});
```

`populate` 让你得到一个用户的朋友列表，但如果你还想要一个用户的朋友的朋友呢？指定 `populate` 选项来告诉 mongoose 填充所有用户的朋友的朋友数组：

```js
User.
  findOne({ name: 'Val' }).
  populate({
    path: 'friends',
    // Get friends of friends - populate the 'friends' array for every friend
    populate: { path: 'friends' }
  });
```
  
## 跨数据库填充

假设您有一个表示事件的模式和一个表示对话的模式。每个事件都有相应的对话线程。

```js
var eventSchema = new Schema({
  name: String,
  // 对应的对话的 id
  // 注意这里没有 ref！
  conversation: ObjectId
});
var conversationSchema = new Schema({
  numMessages: Number
});
```

另外，假设事件和对话存储在不同的 MongoDB 实例中。

```js
var db1 = mongoose.createConnection('localhost:27000/db1');
var db2 = mongoose.createConnection('localhost:27001/db2');

var Event = db1.model('Event', eventSchema);
var Conversation = db2.model('Conversation', conversationSchema);
```

在这种情况下，您将**无法**正常 `populate()`。对话 `conversation` 字段将始终为空，因为 `populate()` 不知道要使用哪个模型。但是，您可以[明确指定模型](http://mongoosejs.com/docs/api.html#model_Model.populate)。

```js
Event.
  find().
  populate({ path: 'conversation', model: Conversation }).
  exec(function(error, docs) { /* ... */ });
```

这被称为“跨数据库填充”，因为它使您能够跨 MongoDB 数据库甚至跨 MongoDB 实例填充。

## 动态引用

Mongoose 也可以同时从多个集合中填充。假设您有一个具有 “connections” 数据的用户模式 —— 用户可以连接到其他用户或组织。

```js
var userSchema = new Schema({
  name: String,
  connections: [{
    kind: String,
    item: { type: ObjectId, refPath: 'connections.kind' }
  }]
});

var organizationSchema = new Schema({ name: String, kind: String });

var User = mongoose.model('User', userSchema);
var Organization = mongoose.model('Organization', organizationSchema);
```

上面的 `refPath` 属性意味着 mongoose 会查看 `connections.kind` 路径来确定使用 `populate()` 的模型。换句话说，`refPath` 属性使您能够使 `ref` 属性动态化。

```js
// 假如我们有一个 organization:
// `{ _id: ObjectId('000000000000000000000001'), name: "Guns N' Roses", kind: 'Band' }`
// 和两个 users:
// {
//   _id: ObjectId('000000000000000000000002')
//   name: 'Axl Rose',
//   connections: [
//     { kind: 'User', item: ObjectId('000000000000000000000003') },
//     { kind: 'Organization', item: ObjectId('000000000000000000000001') }
//   ]
// },
// {
//   _id: ObjectId('000000000000000000000003')
//   name: 'Slash',
//   connections: []
// }
User.
  findOne({ name: 'Axl Rose' }).
  populate('connections.item').
  exec(function(error, doc) {
    // doc.connections[0].item is a User doc
    // doc.connections[1].item is an Organization doc
  });

```

## 填充属性

4.5.0 新增功能

到目前为止，您只基于 `_id` 字段进行填充。但是，这有时不是正确的选择。[特别是无限增长的数组是 MongoDB 的反面模式](https://docs.mongodb.com/manual/tutorial/model-referenced-one-to-many-relationships-between-documents/)。使用 mongoose 虚拟属性，你可以定义更复杂的文件之间的关系。

```js
var PersonSchema = new Schema({
  name: String,
  band: String
});

var BandSchema = new Schema({
  name: String
});
BandSchema.virtual('members', {
  ref: 'Person', // 要使用的 Model
  localField: 'name', // Find people where `localField`
  foreignField: 'band', // is equal to `foreignField`
  // 如果 `justOne` 为 true, 'members' 将是一个单独的文档，而不是一个数组。
  // `justOne` 默认为 false
  justOne: false
});

var Person = mongoose.model('Person', PersonSchema);
var Band = mongoose.model('Band', BandSchema);

/**
 * 假设你有 2 bands: "Guns N' Roses" 和 "Motley Crue"
 * 和 4 people: "Axl Rose" 、 "Slash" with "Guns N' Roses", and
 * "Vince Neil" 、 "Nikki Sixx" with "Motley Crue"
 */
Band.find({}).populate('members').exec(function(error, bands) {
  /* `bands.members` 现在时一个 `Person` 实例数组 */
});
```

请记住，默认情况下，虚拟属性不包含在 `toJSON()` 输出中。如果您希望在使用依赖于 `JSON.stringify()`，如 Express的 [`res.jons()`](http://expressjs.com/en/4x/api.html#res.json) 函数时填充虚拟属性来显示，请在模式的 `toJSON` 选项上设置 `virtuals: true` 选项。

```js

//设置 `virtuals: true`，所以 `res.json()`起作用
var BandSchema = new Schema({
  name: String
}, { toJSON: { virtuals: true } });

```

如果您使用填充预测，请确保预测中包含 `foreignField`。

```js
Band.
  find({}).
  populate({ path: 'members', select: 'name' }).
  exec(function(error, bands) {
    // Won't work, foreign field `band` is not selected in the projection
  });

Band.
  find({}).
  populate({ path: 'members', select: 'name band' }).
  exec(function(error, bands) {
    // Works, foreign field `band` is selected
  });
```

## 接下来

现在我们已经介绍了 Population，让我们来看看 [connections](/Library/mongoose/docs/connections.md)。
