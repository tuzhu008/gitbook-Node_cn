# 在模式中声明默认值

您的模式可以为某些路径定义默认值。如果您创建文档时未设置新路径，这个默认值会启动。

```js
var schema = new Schema({
  name: String,
  role: { type: String, default: 'guitarist' }
});

var Person = db.model('Person', schema);

var axl = new Person({ name: 'Axl Rose', role: 'singer' });
assert.equal(axl.role, 'singer');

var slash = new Person({ name: 'Slash' });
assert.equal(slash.role, 'guitarist');

var izzy = new Person({ name: 'Izzy', role: undefined });
assert.equal(izzy.role, 'guitarist');

Person.create(axl, slash, function(error) {
  assert.ifError(error);
  Person.find({ role: 'guitarist' }, function(error, docs) {
    assert.ifError(error);
    assert.equal(docs.length, 1);
    assert.equal(docs[0].name, 'Slash');
  });
});
```

## Default 函数

您还可以将 `default` 模式选项设置为一个函数。Mongoose 将执行该函数并使用返回值作为默认值。

```js
var schema = new Schema({
 title: String,
 date: {
   type: Date,
   // `Date.now()` returns the current unix timestamp as a number
   default: Date.now
 }
});

var BlogPost = db.model('BlogPost', schema);

var post = new BlogPost({title: '5 Best Arnold Schwarzenegger Movies'});

// The post has a default Date set to now
assert.ok(post.date.getTime() >= Date.now() - 1000);
assert.ok(post.date.getTime() <= Date.now());
```

###  `setDefaultsOnInsert` 选项

默认情况下，mongoose 仅在创建新文档时应用默认值。如果使用 `update()`和 `findOneAndUpdate()`，它将**不会**设置默认值。 但是，mongoose 4.x 允许您使用 `setDefaultsOnInsert` 选项来选择此行为。

### 重要的

`setDefaultsOnInsert` 选项依赖于 [MongoDB `$setOnInsert ` 运算符](https://docs.mongodb.org/manual/reference/operator/update/setOnInsert/)。 `$setOnInsert ` 运算符是在 MongoDB 2.4 中引入的。 如果您正在使用 MongoDB 服务器 < 2.4.0，请不要使用 `setDefaultsOnInsert`。

```js
var schema = new Schema({
 title: String,
 genre: {type: String, default: 'Action'}
});

var Movie = db.model('Movie', schema);

var query = {};
var update = {title: 'The Terminator'};
var options = {
 // Return the document after updates are applied
 new: true,
 // Create a document if one isn't found. Required
 // for `setDefaultsOnInsert`
 upsert: true,
 setDefaultsOnInsert: true
};

Movie.
 findOneAndUpdate(query, update, options, function (error, doc) {
   assert.ifError(error);
   assert.equal(doc.title, 'The Terminator');
   assert.equal(doc.genre, 'Action');
 });
 ```
