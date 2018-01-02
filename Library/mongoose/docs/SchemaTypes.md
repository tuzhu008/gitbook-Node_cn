# SchemaTypes

 SchemaTypes 处理路径
 [defaults](/Library/mongoose/docs/API.md#SchemaType_default)、
 [validation](/Library/mongoose/docs/API.md#SchemaType_validate)、
 [getter](/Library/mongoose/docs/API.md#SchemaType_get)、
 [setter](/Library/mongoose/docs/API.md#SchemaType_set)、
 [queries](/Library/mongoose/docs/API.md#query-js) 的
 [field selection defaults](/Library/mongoose/docs/API.md#select)以及
 [Strings](/Library/mongoose/docs/API.md#schema_string) 和
 [Numbers](/Library/mongoose/docs/API.md#schema_number)
 的其他常规特征的定义。请参阅它们各自的API文档，了解更多细节。

下面是一些可用的 [Schema Types](/Library/mongoose/docs/API.md#Schema_Types).

  * [String](/Library/mongoose/docs/API.md#schema_string)
  * [Number](/Library/mongoose/docs/API.md#schema_number)
  * [Date](/Library/mongoose/docs/API.md#schema_date)
  * [Buffer](/Library/mongoose/docs/API.md#schema_buffer)
  * [Boolean](/Library/mongoose/docs/API.md#schema_boolean)
  * [Mixed](/Library/mongoose/docs/API.md#schema_mixed)
  * [Objectid](/Library/mongoose/docs/API.md#schema_objectid)
  * [Array](/Library/mongoose/docs/API.md#schema_array)

## 示例

```js
var schema = new Schema({
  name:    String,
  binary:  Buffer,
  living:  Boolean,
  updated: { type: Date, default: Date.now },
  age:     { type: Number, min: 18, max: 65 },
  mixed:   Schema.Types.Mixed,
  _someId: Schema.Types.ObjectId,
  array:      [],
  ofString:   [String],
  ofNumber:   [Number],
  ofDates:    [Date],
  ofBuffer:   [Buffer],
  ofBoolean:  [Boolean],
  ofMixed:    [Schema.Types.Mixed],
  ofObjectId: [Schema.Types.ObjectId],
  ofArrays:   [[]],
  ofArrayOfNumbers: [[Number]],
  nested: {
    stuff: { type: String, lowercase: true, trim: true }
  }
})

// example use

var Thing = mongoose.model('Thing', schema);

var m = new Thing;
m.name = 'Statue of Liberty';
m.age = 125;
m.updated = new Date;
m.binary = new Buffer(0);
m.living = false;
m.mixed = { any: { thing: 'i want' } };
m.markModified('mixed');
m._someId = new mongoose.Types.ObjectId;
m.array.push(1);
m.ofString.push("strings!");
m.ofNumber.unshift(1,2,3,4);
m.ofDates.addToSet(new Date);
m.ofBuffer.pop();
m.ofMixed = [1, [], 'three', { four: 5 }];
m.nested.stuff = 'good';
m.save(callback);
```

## SchemaType 选项

您可以使用类型直接声明一个模式类型，或者一个具有 `type` 属性的对象。

```js
var schema1 = new Schema({
  test: String // `test` is a path of type String
});

var schema2 = new Schema({
  test: { type: String } // `test` is a path of type string
});
```

除了 `type` 属性之外，您还可以为路径指定额外的属性。例如，如果在「保存之前」想要小写的字符串:

```js
var schema2 = new Schema({
  test: {
    type: String,
    lowercase: true // 总是转换 `test` 为小写
  }
});
```

`lowercase` 属性只适用于字符串。有一些特定的选项适用于所有的模式类型，还有一些适用于特定的模式类型。

### 通用的 SchemaType 选项

选项  |  类型 |  描述
-------------|-----------------|----------
required  |  Boolean or Function  | 如果 `true`，需要为该属性添加[必要的验证器](/Library/mongoose/docs/validation.html#built-in-validators)
default  |  Any or Function | 设置该路径的默认值。如果值是一个函数，那么函数的返回值就会被用作默认值。
select  | Boolean  | 指定查询的默认[预测(projections)](https://docs.mongodb.com/manual/tutorial/project-fields-from-query-results/)
validate  |  Function or Array or Object | 为该属性添加[验证器函数](/Library/mongoose/docs/API.md#SchemaType_validate)
get  |  Function |  使用 [`Object.defineProperty()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty) 为该属性定义一个自定义 getter。
set  |  Function |  使用 [`Object.defineProperty()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty) 为该属性定义一个自定义 setter。
alias  |  String |  mongoose >= 4.10.0 可用。定义一个具有给定名称的虚拟属性，可以用来获取或者设置此路径。

```js
var numberSchema = new Schema({
  integerOnly: {
    type: Number,
    get: v => Math.round(v),
    set: v => Math.round(v),
    alias: 'i'
  }
});

var Number = mongoose.model('Number', numberSchema);

var doc = new Number();
doc.integerOnly = 2.001;
doc.integerOnly; // 2
doc.i; // 2
doc.i = 3.001;
doc.integerOnly; // 3
doc.i; // 3
```
### Indexes

您还可以使用模式类型选项定义 [MongoDB 索引](https://docs.mongodb.com/manual/indexes/)。

选项  |  类型 |  描述
-------------|-----------------|----------
index   |  Boolean  | 是否在这个属性上定义一个[索引](https://docs.mongodb.com/manual/indexes/)。
unique  |  Boolean  | 是否要在这个属性上定义一个『[惟一的』索引](https://docs.mongodb.com/manual/core/index-unique/)。
sparse  |  Boolean  | 是否在这个属性上定义一个[『稀疏的』索引](https://docs.mongodb.com/manual/core/index-sparse/)。

```js
var schema2 = new Schema({
  test: {
    type: String,
    index: true,
    unique: true // 唯一的索引. 如果指定 `unique: true`
    // 如果设置了 `unique: true`，`index: true`就是可选的
  }
});
```

### String

选项  |  类型 |  描述
-------------|-----------------|----------
lowercase   |  Boolean  | 是否始终在这个值上调用 `.toLowerCase()`
uppercase  | Boolean  | 是否始终在这个值上调用 `.toUpperCase()`
trim  |  Boolean | 是否始终在这个值上调用 `.trim()`
match  |  RegExp | 创建一个[验证器](/Library/mongoose/docs/validation.md)，检查该值是否与给定的正则表达式相匹配
enum  |  Array | 创建一个[验证器](/Library/mongoose/docs/validation.md)，检查该值是否在给定数组中。

### Number

选项  |  类型 |  描述
-------------|-----------------|----------
min   |  Number  | 创建一个[验证器](/Library/mongoose/docs/validation.md)，检查该值是否大于或等于给定值
max  | Number  |  创建一个[验证器](/Library/mongoose/docs/validation.md)，检查该值是否小于或等于给定的最大值。

### Date

选项  |  类型 |  描述
-------------|-----------------|----------
min   |  Date  | 创建一个[验证器](/Library/mongoose/docs/validation.md)，检查该日期是否大于或等于给定值
max  | Date  |  创建一个[验证器](/Library/mongoose/docs/validation.md)，检查该日期是否小于或等于给定的最大值。


## 使用笔记:

### Dates

内置的 [Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) 方法[不会勾挂在](https://github.com/Automattic/mongoose/issues/1598) mongoose 更改跟踪逻辑中，英文表示如果您在文档中使用 Date 并使用 `setMonth()` 方法对其进行修改，则 mongoose 将不会意识到此更改，而 `doc.save()` 不会保存这个修改。如果您必须使用内置方法修改 Date 类型，请在保存之前使用 `doc.markModified('pathToYourDate')` 告诉 mongoose 有关更改。

```js
var Assignment = mongoose.model('Assignment', { dueDate: Date });
Assignment.findOne(function (err, doc) {
  doc.dueDate.setMonth(3);
  doc.save(callback); // 这里不会保存修改

  doc.markModified('dueDate');
  doc.save(callback); // 保存啦
})
```
### Mixed

任何 SchemaType，它的灵活性来自于难以维护的折衷。 Mixed 可以通过 `Schema.Types.Mixed` 或通过传递一个空的对象文字来获得。 以下是等同的：

```js
var Any = new Schema({ any: {} });
var Any = new Schema({ any: Object });
var Any = new Schema({ any: Schema.Types.Mixed });
```

由于它是一个「无模式（schema-less）」类型，您可以将其值更改为其他任何您喜欢的值，但 Mongoose 失去了自动检测和保存这些更改的功能。 为了 “告诉” Mongoose Mixed 类型的值已经改变，调用文档的 `.markModified(path)` 方法，将路径传递给刚刚更改的 Mixed 类型。

```js
person.anything = { x: [3, 4, { y: "changed" }] };
person.markModified('anything');
person.save(); // 任何东西都会被保存下来
```

### ObjectIds

要指定一个 ObjectId 的类型，在你的声明中使用 `Schema.Types.ObjectId`

```js
var mongoose = require('mongoose');
var ObjectId = mongoose.Schema.Types.ObjectId;
var Car = new Schema({ driver: ObjectId });
// or just Schema.ObjectId for backwards compatibility with v2
```

### Arrays

提供 of[SchemaTypes](/Library/mongoose/docs/API.md_Schema_Types) 或 [子文档](/Library/mongoose/docs/subdocs.md) 数组。

```js
var ToySchema = new Schema({ name: String });
var ToyBox = new Schema({
  toys: [ToySchema],
  buffers: [Buffer],
  string:  [String],
  numbers: [Number]
  // ... etc
});
```
注意: 指定一个空数组等价等价于 toMixed。下面这些都创建了 Mixed 的数组:

```js
var Empty1 = new Schema({ any: [] });
var Empty2 = new Schema({ any: Array });
var Empty3 = new Schema({ any: [Schema.Types.Mixed] });
var Empty4 = new Schema({ any: [{}] });
```
Array 隐式地有一个 `[]` 默认值(空数组)。

```js
var Toy = mongoose.model('Test', ToySchema);
console.log((new Toy()).toys); // []
```

为了重写默认值，你需要设置默认值为  `undefined`

```js
var ToySchema = new Schema({
  toys: {
    type: [ToySchema],
    default: undefined
  }
});
```

如果一个数组被标记为 `required`，那么它必须至少有一个元素。

```js
var ToySchema = new Schema({
  toys: {
    type: [ToySchema],
    required: true
  }
});
var Toy = mongoose.model('Toy', ToySchema);
Toy.create({ toys: [] }, function(error) {
  console.log(error.errors['toys'].message); // Path "toys" is required.
});
```
## 创建自定义类型

Mongoose 也可以使用自定义的 SchemaTypes 进行扩展。搜索[插件网站](http://plugins.mongoosejs.com/)上的兼容类型如 [mongoose-long](https://github.com/aheckmann/mongoose-long)，[mongoose-int32](https://github.com/vkarpov15/mongoose-int32) 和[其他](https://github.com/aheckmann/mongoose-function)[类型](https://github.com/OpenifyIt/mongoose-types)。要创建自己的自定义 schema，请查看[创建基本的自定义 Schema 类型](/Library/mongoose/docs/customschematypes.md)。

## `schema.path()` 函数

[`schema.path()` 函数](/Library/mongoose/docs/API.md#Schema_path) 为给定路径返回实例化的模式类型。

```js
var sampleSchema = new Schema({ name: { type: String, required: true } });
console.log(sampleSchema.path('name'));

// 输出看起来像:
/**
 * SchemaString {
 *   enumValues: [],
 *   regExp: null,
 *   path: 'name',
 *   instance: 'String',
 *   validators: ...
 */
```

您可以使用该函数检查给定路径的模式类型，包括它拥有的验证器和类型是什么。

## 接下来

现在我们已经介绍了 SchemaTypes，让我们来看看[Model](/Library/mongoose/docs/models.md)。
