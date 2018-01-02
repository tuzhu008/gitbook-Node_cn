# Schemas（模式）

>**[warning]**
>
> 如果你还没有这样做，请花一分钟阅读一下[快速入门](/Library/mongoose/docs/quick-start.md)，了解一下 Mongoose 是如何工作的。如果你是从3.x 迁移到 4.x，请稍等一下，看一下[迁移指南](http://mongoosejs.com/docs/migration.html)。

## 定义模式

Mongoose 的一切都以 Schema 开始。每个模式映射到 MongoDB 集合(collection)，并定义该集合内的文档的形状。

```js
var mongoose = require('mongoose');
var Schema = mongoose.Schema;

var blogSchema = new Schema({
  title:  String,
  author: String,
  body:   String,
  comments: [{ body: String, date: Date }],
  date: { type: Date, default: Date.now },
  hidden: Boolean,
  meta: {
    votes: Number,
    favs:  Number
  }
});
```

如果你想在以后添加额外的键，请使用 [Schema#add](/Library/mongoose/docs/API.md#schema_Schema-add) 方法。

我们的 `blogSchema` 中的每个键都定义了我们的文档中的一个属性，该属性将被转换到它相关的 [SchemaType]()。例如，我们定义了一个 `title`，它将被转换为 String 模式类型和 `date`，它将被转换为 Date 模式类型。键还可以是一个对象，其中包含进一步的键/类型定义(如上面的 `meta` 属性)。

允许 SchemaTypes 是:

  * String
  * Number
  * Date
  * Buffer
  * Boolean
  * Mixed
  * ObjectId
  * Array

阅读[更多](/Library/mongoose/docs/SchemaTypes.md)关于它们的信息。

模式不仅定义了文档的结构和属性的转换，还定义了文档[实例方法](#实例方法)、静态[模型方法](#静态方法)、[复合索引](#索引)和称为[中间件](/Library/mongoose/docs/middleware.md)的文档生命周期钩子。

## 创建模型

为了使用我们的模式定义，我们需要将我们的 `blogSchema` 转换到一个可以使用的 [Model](/Library/mongoose/docs/models.md)中。为了做到这，我们把它传递到  `mongoose.model(modelName, schema)` 中:

```js
var Blog = mongoose.model('Blog', blogSchema);
// 开车啦!
```

## 实例方法

Model 的实例是[文档](/Library/mongoose/docs/documents.md)，文档有许多自己的[内置的实例方法]()。我们也可以定义自己的自定义文档实例方法。

```js
// 定义一个 schema
var animalSchema = new Schema({ name: String, type: String });

// 分配一个函数给 animalSchema 的 "methods" 对象
animalSchema.methods.findSimilarTypes = function(cb) {
  // this 指向
  return this.model('Animal').find({ type: this.type }, cb);
};
```

现在，我们所有的动物实例都有一个 `findSimilarTypes` 的方法。

```js
var Animal = mongoose.model('Animal', animalSchema);
var dog = new Animal({ type: 'dog' });

dog.findSimilarTypes(function(err, dogs) {
  console.log(dogs); // woof
});
```

> **[warning] 警告**
>
> 重写默认的 mongoose 文档方法可能会导致不可预测的结果。详情请见[此](http://mongoosejs.com/docs/api.html#schema_Schema.reserved)。

<br/>

> **[warning] 警告**
>
> 不要使用 ES6 箭头函数(`=>`)声明方法。箭头函数[显式地阻止绑定 `this`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow_functions)，因此您的方法将无法访问文档，上面的示例将无法工作。

## 静态方法 {#statics}

向 Model 中添加静态方法也很简单。继续使用我们的 `animalSchema`:

```js
// 分配一个函数给 animalSchema 的 "statics" 对象
animalSchema.statics.findByName = function(name, cb) {
  // this 指向的是由 animalSchema 编译成的模型
  return this.find({ name: new RegExp(name, 'i') }, cb);
};

var Animal = mongoose.model('Animal', animalSchema);
Animal.findByName('fido', function(err, animals) {
  console.log(animals);
});
```

> **[warning] 警告**
>
> 不要使用 ES6 箭头函数(`=>`)声明方法。箭头函数[显式地阻止绑定 `this`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow_functions)，因此您的方法将无法访问文档，上面的示例将无法工作。

## 查询助手

您还可以添加查询助手函数，这类似于实例方法，但只适用于 mongoose 查询。查询助手方法允许您扩展 mongoose 的[链式查询构建器 API](/Library/mongoose/docs/queries.md)。

```js
animalSchema.query.byName = function(name) {
  //this 指向的是由 animalSchema 编译成的模型
  return this.find({ name: new RegExp(name, 'i') });
};

var Animal = mongoose.model('Animal', animalSchema);
Animal.find().byName('fido').exec(function(err, animals) {
  console.log(animals);
});
```

## 索引

MongoDB 支持[二级索引](https://docs.mongodb.com/manual/indexes/)。对于 mongoose，我们在[路](http://mongoosejs.com/docs/api.html#schematype_SchemaType-index)[径](http://mongoosejs.com/docs/api.html#schematype_SchemaType-unique)[级](http://mongoosejs.com/docs/api.html#schematype_SchemaType-sparse)[别](http://mongoosejs.com/docs/api.html#schema_date_SchemaDate-expires)或模式级别定义这些索引。在创建[复合索引](https://docs.mongodb.com/manual/indexes/#Indexes-CompoundKeys)时，需要在模式级别定义索引。

```js
var animalSchema = new Schema({
  name: String,
  type: String,
  tags: { type: [String], index: true } // field level
});

animalSchema.index({ name: 1, type: -1 }); // schema level
```

> **[warning] 警告**
>
> 当你的应用程序启动时，Mongoose 会自动为你的模式中的每一个定义的索引调用 [`createIndex`](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#db.collection.createIndex)。Mongoose 将按顺序为每个索引调用 `createIndex`，并在所有的 `createIndex` 调用成功或出现错误时，在「模型」上发射一个 “index” 事件。虽然对开发很好，但是建议在生产中禁用该行为，因为索引创建可能会造成[显著的性能影响](http://docs.mongodb.org/manual/core/indexes/#index-creation-operations)。通过将您的模式的  `autoIndex` 选项设置为 `false`，或者在连接上全局性地设置 `config.autoIndex` 为 `false`， 从而禁用该行为。

```js
mongoose.connect('mongodb://user:pass@localhost:port/database', { config: { autoIndex: false } });
// or
mongoose.createConnection('mongodb://user:pass@localhost:port/database', { config: { autoIndex: false } });
// or
animalSchema.set('autoIndex', false);
// or
new Schema({..}, { autoIndex: false });
```

当索引被创建完成或者发生错误时，Mongoose 将会在模型上发射一个 `index` 事件。

```js
// 将会导致错误，因为 mongodb 在默认情况下有一个 id 索引，这不是稀疏的(sparse)
animalSchema.index({ _id: 1 }, { sparse: true });
var Animal = mongoose.model('Animal', animalSchema);

Animal.on('index', function(error) {
  // "_id 索引不能被 sparse（稀疏矩阵）"
  console.log(error.message);
});
```

也可以查看 `Model#ensureIndexes` 方法。

## 虚拟属性 {#virtuals}

[Virtuals](http://mongoosejs.com/docs/api.html#schema_Schema-virtual) 是可以获取和设置的文档属性，但这些属性不会被持久化到 MongoDB 中。getter 对于格式化或组合字段是很有用的，而 setter 对于将单个值组合成多个用于存储的值是很有用的。


```js
// 定义 schema
var personSchema = new Schema({
  name: {
    first: String,
    last: String
  }
});

// 编译 model
var Person = mongoose.model('Person', personSchema);

// 创建 document
var axl = new Person({
  name: { first: 'Axl', last: 'Rose' }
});
```

假设你想打印出这个人的全名。你可以自己做:

```js
console.log(axl.name.first + ' ' + axl.name.last); // Axl Rose
```

但是每次拼接名字和姓氏都会变得麻烦。而如果你想对名字做一些额外的处理，比如[删除变音符号?](https://www.npmjs.com/package/diacritics) [虚拟属性获取器]()可以让你定义一个不会被保存到 MongoDB 的 `fullName` 属性。

```js
personSchema.virtual('fullName').get(function () {
  return this.name.first + ' ' + this.name.last;
});
```

现在，每当你访问 `fullName` 属性时，mongoose 就会调用你的 getter 函数。

```js
console.log(axl.fullName); // Axl Rose
```


如果你使用 `toJSON()` 或者 `toObject()` (或者在一个 mongoose 文档上使用 `JSON.stringify()` ) mongoose 默认地将不会包含 virtuals。传递 `{ virtuals: true }` 给 `toObject()` 或 `toJSON()`。

你也可以添加一个自定义的 setter 给你的虚拟属性，让您通过 `fullName` 虚拟属性设置名称和姓氏。

```js
personSchema.virtual('fullName').
  get(function() { return this.name.first + ' ' + this.name.last; }).
  set(function(v) {
    this.name.first = v.substr(0, v.indexOf(' '));
    this.name.last = v.substr(v.indexOf(' ') + 1);
  });

axl.fullName = 'William Rose'; // Now `axl.name.first` is "William"
```

虚拟属性 setter 在其他校验之前应用。因此，上面的示例仍然可以工作，即使需要第一个和最后一个名称字段。

只有非虚拟属性才能作为查询和字段选择的一部分工作。由于虚拟属性没有存储在 MongoDB 中，所以不能对它们进行查询。

### 别名

别名是一种特定类型的虚拟属性，getter 和 setter 无缝地获取并设置另一个属性。这对于节省网络带宽是很方便的，因此您可以将存储在数据库中的一个简短的属性名转换为一个更长的名称，以提高代码的可读性。

```js
var personSchema = new Schema({
  n: {
    type: String,
    // 现在访问 `name` 将取得 `n` 的值, 并且设置 `n` 将设置 `name` 的值
    alias: 'name'
  }
});

// 设置 `name` 将传导给 `n`
var person = new Person({ name: 'Val' });
console.log(person); // { n: 'Val' }
console.log(person.toObject({ virtuals: true })); // { n: 'Val', name: 'Val' }
console.log(person.name); // "Val"

person.name = 'Not Val';
console.log(person); // { n: 'Not Val' }
```
> **[info] 笔记**
>
> `n` 是存储在数据库中的字段，`name` 只是这个字段在代码中一个语义化的别名。

## Options

Schemas have a few configurable options which can be passed to the constructor or set directly:
Schemas 有一些可配置选项，可以直接传递给构造函数或直接设置:

```js
new Schema({..}, options);

// 或者

var schema = new Schema({..});
schema.set(option, value);
```

有效的选项:

  * [autoIndex](#autoIndex)
  * [bufferCommands](#bufferCommands)
  * [capped](#capped)
  * [collection](#collection)
  * [emitIndexErrors](#emitIndexErrors)
  * [id](#id)
  * [minimize](#minimize)
  * [read](#read)
  * [safe](#safe)
  * [shardKey](#shardKey)
  * [strict](#strict)
  * [toJSON](#toJSON)
  * [toObject](#toObject)
  * [typeKey](#typeKey)
  * [validateBeforeSave](#validateBeforeSave)
  * [versionKey](#versionKey)
  * [collation](#collation)
  * [skipVersioning](#skipVersioning)
  * [timestamps](#timestamps)
  * [retainKeyOrder](#retainKeyOrder)

### 选项: autoIndex {#autoIndex}

在应用程序启动时，Mongoose 为您的 Schema 中声明的每个索引发送一个 [`createIndex` 命令](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#db.collection.createIndex)。在 Mongoose v3 中，在默认情况下，索引是在后台创建的。如果您希望禁用自动创建特性，并在创建索引时手动处理，将您的 Schemas `autoIndex` 选项设置为 `false`，并在您的模型上使用 [`ensureIndexes`](/Library/mongoose/docs/API.md#) 方法。

```js
var schema = new Schema({..}, { autoIndex: false });
var Clock = mongoose.model('Clock', schema);
Clock.ensureIndexes(callback);
```

### 选项: bufferCommands {#bufferCommands}

默认情况下，当连接下降时，mongoose 会缓冲命令，直到驱动程序重新连接。要禁用缓冲，将 `buffercommand` 设置为 `false`。

```js
var schema = new Schema({..}, { bufferCommands: false });
```

### option: capped {#capped}

Mongoose 支持 MongoDBs [capped](http://www.mongodb.org/display/DOCS/Capped+Collections) 集合。要指定底层的 MongoDB 集合被限制，可以设置 `capped` 选项作为集合的最大[字节](http://www.mongodb.org/display/DOCS/Capped+Collections#CappedCollections-size.)。

```js
new Schema({..}, { capped: 1024 });
```

如果您想要传递像 [max](http://www.mongodb.org/display/DOCS/Capped+Collections#CappedCollections-max) 或 [autoIndexId](http://www.mongodb.org/display/DOCS/Capped+Collections#CappedCollections-autoIndexId) 这样的附加选项，则设置 `capped` 选项也可以设置为对象。在这种情况下，您必须显式地传递所需的 `size` 选项。

```js
new Schema({..}, { capped: { size: 1024, max: 1000, autoIndexId: true } });
```

### 选项: collection {#collection}

默认情况下，Mongoose 通过将模型名称传递给 `utils.toCollectionName` 方法来产生一个集合名称。这个方法对名称进行了复数化。如果您的集合需要不同的名称，就设置这个选项。

```js
var dataSchema = new Schema({..}, { collection: 'data' });
```

### 选项: emitIndexErrors {#emitIndexErrors}

默认情况下，mongoose 会在模式中为你构建任何你指定的索引，当索引建立成功或错误时，它会在模型上发出一个 `index` 事件。

```js
MyModel.on('index', function(error) {
  /* If error is truthy, index build failed */
});
```

然而，这使得在索引构建失败时很难捕捉到。`emitIndexErrors` 选项使看到索引构建失败时的情况更简单。如果该选项已经打开，那么当索引构建失败时，mongoose 将会在模型上另外发出一个 `error` 事件。

```js
MyModel.schema.options.emitIndexErrors; // true
MyModel.on('error', function(error) {
  // gets an error whenever index build fails
});
```

[如果一个错误事件被发射，并且没有监听器，那么 Node.js 的内置事件发射器会抛出异常](https://nodejs.org/api/events.html#events_class_events_eventemitter)，因此很容易配置您的应用程序，以在索引构建失败时，快速失败。

### 选项: id {#id}

在默认情况下，Mongoose 将每个模式都分配给一个 id 虚拟属性 getter，这将把文档 `_id` 字段转换为字符串，或者在 ObjectIds 的情况下，它的 hexString。如果您不希望将 id getter 添加到您的模式，那么您可以在模式构建时禁用该选项。

```js
// 默认行为
var schema = new Schema({ name: String });
var Page = mongoose.model('Page', schema);
var p = new Page({ name: 'mongodb.org' });
console.log(p.id); // '50341373e894ad16347efe01'

// disabled id
var schema = new Schema({ name: String }, { id: false });
var Page = mongoose.model('Page', schema);
var p = new Page({ name: 'mongodb.org' });
console.log(p.id); // undefined
```

### 选项: _id

如果没有传递 `_id` 到 [Schema](http://mongoosejs.com/docs/api.html#schema-js) 构造函数中，Mongoose 就会默认为每个模式分配一个 `_id` 字段。指定的类型是一个与 MongoDB 的默认行为相一致的 [ObjectId](http://mongoosejs.com/docs/api.html#schema_Schema.Types)。如果您不希望将 `_id` 添加到您的模式中，您可以使用该选项禁用它。

您只能在子文档中使用此选项。如果不知道它的 id，Mongoose 就不能保存文档，所以如果你试图保存一个没有 `_id` 的文档，你就会有一个错误。


```js
// 默认行为
var schema = new Schema({ name: String });
var Page = mongoose.model('Page', schema);
var p = new Page({ name: 'mongodb.org' });
console.log(p); // { _id: '50341373e894ad16347efe01', name: 'mongodb.org' }

// disabled _id
var childSchema = new Schema({ name: String }, { _id: false });
var parentSchema = new Schema({ children: [childSchema] });

var Model = mongoose.model('Model', parentSchema);

Model.create({ children: [{ name: 'Luke' }] }, function(error, doc) {
  // doc.children[0]._id will be undefined
});
```

### 选项: minimize {#minimize}

默认情况下，Mongoose 会通过移除空对象来“最小化”模式。

```js
var schema = new Schema({ name: String, inventory: {} });
var Character = mongoose.model('Character', schema);

// 如果 `inventory` 是非空的，将存储它
var frodo = new Character({ name: 'Frodo', inventory: { ringOfPower: 1 }});
Character.findOne({ name: 'Frodo' }, function(err, character) {
  console.log(character); // { name: 'Frodo', inventory: { ringOfPower: 1 }}
});

// 如果 `inventory` 是空的，将不会存储它
var sam = new Character({ name: 'Sam', inventory: {}});
Character.findOne({ name: 'Sam' }, function(err, character) {
  console.log(character); // { name: 'Sam' }
});
```

可以通过将 `minimize` 选项设置为 `false` 来覆盖此行为。然后它将存储空对象。

```js
var schema = new Schema({ name: String, inventory: {} }, { minimize: false });
var Character = mongoose.model('Character', schema);

// 如果 `inventory` 为空，也将存储它
var sam = new Character({ name: 'Sam', inventory: {}});
Character.findOne({ name: 'Sam' }, function(err, character) {
  console.log(character); // { name: 'Sam', inventory: {}}
});
```
### 选项: read {#read}

允许在模式级别设置[query#read](http://mongoosejs.com/docs/api.html#query_Query-read)选项，为我们提供了一种方法，可以将默认的 ReadPreferences 应用于从模型派生的所有查询。

```js
var schema = new Schema({..}, { read: 'primary' });            // also aliased as 'p'
var schema = new Schema({..}, { read: 'primaryPreferred' });   // aliased as 'pp'
var schema = new Schema({..}, { read: 'secondary' });          // aliased as 's'
var schema = new Schema({..}, { read: 'secondaryPreferred' }); // aliased as 'sp'
var schema = new Schema({..}, { read: 'nearest' });            // aliased as 'n'
```

允许使用每个优先级的别名，因此不必输入 'secondaryPreferred'，很容易产生拼写错误，我们可以简单地传递 'sp'。

`read` 选项还允许我们指定标记集(tag sets)。这些告诉[驱动程序](https://github.com/mongodb/node-mongodb-native/)，它应该尝试读取的副本集的成员。在[这里](http://docs.mongodb.org/manual/applications/replication/#tag-sets)和[这里](http://mongodb.github.com/node-mongodb-native/driver-articles/anintroductionto1_1and2_2.html#read-preferences)阅读更多关于标记集的信息。

注意: 您还可以在连接时指定驱动程序读取优先级 `strategy` 选项：

```js
// 定期对副本集成员进行 ping ，以跟踪网络延迟
var options = { replset: { strategy: 'ping' }};
mongoose.connect(uri, options);

var schema = new Schema({..}, { read: ['nearest', { disk: 'ssd' }] });
mongoose.model('JellyBean', schema);
```

### 选项: safe {#safe}

该选项将通过所有操作传递给 MongoDB，并指定是否应该将错误返回给我们的回调，以及调优写入行为。

```js
var safe = true;
new Schema({ .. }, { safe: safe });
```

默认情况下，这对于所有的模式都是 `true` 的，这些模式保证任何发生的错误都会被传回回调。通过将 `safe` 设置为` { j: 1, w: 2, wtimeout: 10000 }`，我们可以保证写入操作被提交到 MongoDB 日志(j:1)，至少有 2 个副本(w:2)，如果需要超过 10 秒(wtimeout:10000)，写入将超时。错误仍然会传递给我们的回调。

注意: 在 3.6.x中， 您还需要关闭[版本](#versionKey)控制。在 3.7.x 和更高的版本中， 当 `safe` 被设置为 `false` 时，将自动禁用版本控制。

**注意**: 此设置会覆盖在[创建连接](http://mongoosejs.com/docs/api.html#index_Mongoose-createConnection)时通过传递 `db` 选项指定的任何设置。

还有其他写入的关注点，如 `{ w: "majority" }` 。参见 [MongoDB 文档](http://www.mongodb.org/display/DOCS/getLastError+Command)获取更多细节。

```js
var safe = { w: "majority", wtimeout: 10000 };
new Schema({ .. }, { safe: safe });
```

### 选项: shardKey {#shardKey}

The shardKey option is used when we have a sharded MongoDB architecture. Each sharded collection is given a shard key which must be present in all insert/update operations. We just need to set this schema option to the same shard key and we’ll be all set.
`shardKey` 选项是在我们拥有一个[共享的 MongoDB 架构](http://www.mongodb.org/display/DOCS/Sharding+Introduction)时使用的。每个共享的集合都有一个共享密钥(shard key)，必须在所有的插入/更新操作中都存在。我们只需要将这个模式选项设置为相同的共享密钥，我们就会全部设置。

```js
new Schema({ .. }, { shardKey: { tag: 1, name: 1 }})
```

请注意，Mongoose 没有为您发送 `shardcollection` 命令。您必须自己配置您的 shard。

### 选项: strict {#strict}

`strict` 选项(默认启用)，可以确保传递给模型构造函数的值（模式中未指定的）不会被保存到数据库中。

```js
// iAmNotInTheSchema 未在 Schema 选项中指定
var thingSchema = new Schema({..})
var Thing = mongoose.model('Thing', thingSchema);
var thing = new Thing({ iAmNotInTheSchema: true });
thing.save(); // iAmNotInTheSchema 不会被保存到数据库

// set to false..
var thingSchema = new Schema({..}, { strict: false });
var thing = new Thing({ iAmNotInTheSchema: true });
thing.save(); // iAmNotInTheSchema 现在会被保存到数据库。
```

这也会影响使用 `doc.set()` 来设置一个属性值。

```js
var thingSchema = new Schema({..})
var Thing = mongoose.model('Thing', thingSchema);
var thing = new Thing;
thing.set('iAmNotInTheSchema', true);
thing.save(); // iAmNotInTheSchema 不会被保存到数据库
```

通过在模型实例级传递第二个布尔参数，可以覆盖该选项的值。

```js
var Thing = mongoose.model('Thing');
var thing = new Thing(doc, true);  // 启用 strict 模式
var thing = new Thing(doc, false); // 禁用 strict 模式
```

`strict` 选项也可能被设置为 `'throw'`，这将导致产生错误，而不是删除糟糕的数据。

注意: 除非你有充分的理由，否则不要设为 `false`。

注意: 在 mongoose v2 中，默认值是假的。

注意: 无论模式选项是什么，模式中不存在的属性，在实例上设置的键/值始终都是被忽略的。

```js
var thingSchema = new Schema({..})
var Thing = mongoose.model('Thing', thingSchema);
var thing = new Thing;
thing.iAmNotInTheSchema = true;
thing.save(); // iAmNotInTheSchema 永远都不会被保存
```

### 选项: toJSON {#toJSON}

与 [`toObject` ](#toObject)选项完全相同，但仅在调用文档 `toJSON` 方法时适用。

```js
var schema = new Schema({ name: String });
schema.path('name').get(function (v) {
  return v + ' is my name';
});
schema.set('toJSON', { getters: true, virtuals: false });
var M = mongoose.model('Person', schema);
var m = new M({ name: 'Max Headroom' });
console.log(m.toObject()); // { _id: 504e0cd7dd992d9be2f20b6f, name: 'Max Headroom' }
console.log(m.toJSON()); // { _id: 504e0cd7dd992d9be2f20b6f, name: 'Max Headroom is my name' }
// 因为我们知道当 js 对象被字符串化时，toJSON 就会被调用:
console.log(JSON.stringify(m)); // { "_id": "504e0cd7dd992d9be2f20b6f", "name": "Max Headroom is my name" }
```

查看所有可用的 `toJSON`/`toObject` 选项，阅读[这里](http://mongoosejs.com/docs/api.html#document_Document-toObject)。

### 选项: toObject {#toObject}

文档有一个 [`toObject`](http://mongoosejs.com/docs/api.html#document_Document-toObject) 方法，它将 mongoose 文档转换到一个普通的 javascript 对象中。该方法接受一些选项。我们没有在每个文档基础上应用这些选项，我们可以在这里声明选项，并在默认情况下将其应用到所有模式文档中。

让所有的虚拟属性都出现在你的 `console.log` 输出中，将 `toObject` 选项设置为 `getter:true`:

```js
var schema = new Schema({ name: String });
schema.path('name').get(function (v) {
  return v + ' is my name';
});
schema.set('toObject', { getters: true });
var M = mongoose.model('Person', schema);
var m = new M({ name: 'Max Headroom' });
console.log(m); // { _id: 504e0cd7dd992d9be2f20b6f, name: 'Max Headroom is my name' }
```
查看所有可用的 `toObject` 选项，阅读[这里](http://mongoosejs.com/docs/api.html#document_Document-toObject)。

### 选项: typeKey {#typeKey}

默认情况下，如果您的模式中有一个具有键 'type' 的对象，则 mongoose 会将其解释为类型声明。

```js
// Mongoose 解释这个如同 'loc 是一个 String'
var schema = new Schema({ loc: { type: String, coordinates: [Number] } });
```

然而，对于像 [geoJSON](http://docs.mongodb.org/manual/reference/geojson/) 这样的应用程序，`type` 属性非常重要。如果您想要控制 mongoose 使用哪个 key 来查找类型声明，请设置  `typeKey` 模式选项。

```js
var schema = new Schema({
  // Mongoose 解释这个如同 'loc 是一个有 2 个键的对象，type 和 coordinates'
  loc: { type: String, coordinates: [Number] },
  // Mongoose 解释这个如同 'name 是一个 String'
  name: { $type: String }
}, { typeKey: '$type' }); // A '$type' key means this object is a type declaration
```
### 选项: validateBeforeSave {#validateBeforeSave}

默认情况下，文档在保存到数据库之前会被自动验证。这是为了防止保存无效的文档。如果您想手动处理验证，并且能够保存不经过验证的对象，您可以将 `validateBeforeSave` 设置为 `false`。

```js
var schema = new Schema({ name: String });
schema.set('validateBeforeSave', false);
schema.path('name').validate(function (value) {
    return v != null;
});
var M = mongoose.model('Person', schema);
var m = new M({ name: null });
m.validate(function(err) {
    console.log(err); // 会告诉你，不允许为 null
});
m.save(); // 虽然是无效的，但还是成功了
```

### 选项: versionKey {#versionKey}

每个文档第一次被 Mongoose 创建时，会为它们设置 `versionKey` 属性。这个键值包含文档的内部[修订](http://aaronheckmann.tumblr.com/post/48943525537/mongoose-v3-part-1-versioning)。`versionKey` 选项是表示用于版本控制的路径的字符串。默认值是 `__v`。如果这与您的应用程序发生冲突，您可以这样配置:

```js
var schema = new Schema({ name: 'string' });
var Thing = mongoose.model('Thing', schema);
var thing = new Thing({ name: 'mongoose v3' });
thing.save(); // { __v: 0, name: 'mongoose v3' }

// 自定义 versionKey
new Schema({..}, { versionKey: '_somethingElse' })
var Thing = mongoose.model('Thing', schema);
var thing = new Thing({ name: 'mongoose v3' });
thing.save(); // { _somethingElse: 0, name: 'mongoose v3' }
```

还可以通过将 `versionKey` 设置为 `false` 来禁用文档版本控制。除非您[知道您在做什么](http://aaronheckmann.tumblr.com/post/48943525537/mongoose-v3-part-1-versioning)，否则**不要**禁用版本控制。

```js
new Schema({..}, { versionKey: false });
var Thing = mongoose.model('Thing', schema);
var thing = new Thing({ name: 'no versioning please' });
thing.save(); // { name: 'no versioning please' }
```

### 选项: collation {#collation}

为每个查询和聚合(aggregation)设置一个默认的排序([collation](https://docs.mongodb.com/manual/reference/collation/))。[这里是关于 collation 的初学者友好的概述](http://thecodebarbarian.com/a-nodejs-perspective-on-mongodb-34-collations)。

```js
var schema = new Schema({
  name: String
}, { collation: { locale: 'en_US', strength: 1 } });

var MyModel = db.model('MyModel', schema);

MyModel.create([{ name: 'val' }, { name: 'Val' }]).
  then(function() {
    return MyModel.find({ name: 'val' });
  }).
  then(function(docs) {
    // `docs` will contain both docs, because `strength: 1` means
    // MongoDB will ignore case when matching.
  });
```

### 选项: skipVersioning {#skipVersioning}

`skipVersioning` 允许从版本控制中排除路径(即:即使更新了这些路径，内部修订也不会自增。）除非你知道你在做什么，否则**不要**这样做。对于子文档，使用完全限定的路径将其包含在父文档中。

```js
new Schema({..}, { skipVersioning: { dontVersionMe: true } });
thing.dontVersionMe.push('hey');
thing.save(); // version is not incremented
```

### 选项: timestamps {#timestamps}

如果设置了 `timestamps`，mongoose 将 `createdAt` 和 `updatedAt` 字段分配给您的模式，分配的类型是 [Date](http://mongoosejs.com/docs/api.html#schema-date-js)。

默认情况下，两个字段的名称是 `createdAt` 和 `updatedAt`，通过设置 `timestamps.createdAt` 和 `timestamps.updatedAt` 来自定义字段名称。

```js
var thingSchema = new Schema({..}, { timestamps: { createdAt: 'created_at' } });
var Thing = mongoose.model('Thing', thingSchema);
var thing = new Thing();
thing.save(); // `created_at` & `updatedAt` will be included
```

### 选项: useNestedStrict {#useNestedStrict}


在 mongoose 4 中， `update()` 和 `findOneAndUpdate()` 只检查顶级的模式的严格模式（`strict` 选项）设置。o

```js
var childSchema = new Schema({}, { strict: false });
var parentSchema = new Schema({ child: childSchema }, { strict: 'throw' });
var Parent = mongoose.model('Parent', parentSchema);
Parent.update({}, { 'child.name': 'Luke Skywalker' }, function(error) {
  // Error，因为 parentSchema 有 `strict: throw`，
  // 即使 `childSchema` 有 `strict: false`
});

var update = { 'child.name': 'Luke Skywalker' };
var opts = { strict: false };
Parent.update({}, update, opts, function(error) {
  // 正常工作，因为 `strict: false` 到 `update()` 重写了 parent schema
});
```

如果将 `useNestedStrict` 设置为 `true`，mongoose 将使用子模式的 `strict` 选项来转换更新。

```js
var childSchema = new Schema({}, { strict: false });
var parentSchema = new Schema({ child: childSchema },
  { strict: 'throw', useNestedStrict: true });
var Parent = mongoose.model('Parent', parentSchema);
Parent.update({}, { 'child.name': 'Luke Skywalker' }, function(error) {
  // Works!
});
```

### 选项: retainKeyOrder {#retainKeyOrder}

默认情况下，mongoose 将反转文档中的键顺序来进行性能优化。 例如， `new Model({ first: 1, second: 2 })`; 实际上将作为 `{second：2, first：1}`存储在 MongoDB 中。 这种行为[被认为是弃用的](https://github.com/Automattic/mongoose/wiki/5.0-Deprecation-Warnings)，因为它有许多意想不到的副作用，包括难以处理其 `_id` 字段是对象的文档。

Mongoose >= 4.6.4 有一个用于 schema 的 `retainKeyOrder` 选项，可以确保 mongoose 始终保持对象键的正确顺序。

```js
var testSchema = new Schema({ first: Number, second: Number }, { retainKeyOrder: true });
var Test = mongoose.model('Test', testSchema);
Test.create({ first: 1, second: 2 }); // Will be stored in mongodb as `{ first: 1, second: 2 }`
```

## 可插拔

Schema 也是[可插拔](/Library/mongoose/docs/plugins.md)的，它允许我们将可重用的特性打包到插件中，这些插件可以与社区共享，也可以在项目之间共享。

## 接下来

现在我们已经介绍了 Schemas，让我们看一下 [SchemaTypes](/Library/mongoose/docs/SchemaTypes.md)。
