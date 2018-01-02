# Validation（验证）

在介绍验证语法的具体细节之前，请牢记以下规则：

  * 验证在 [SchemaType](/Library/mongoose/docs/SchemaType.md) 中定义
  * 验证是[中间件](/Library/mongoose/docs/middleware.md)。 Mongoose 默认将验证注册为每个模式的 `pre('save')` 钩子。
  * 您可以使用 `doc.validate(callback)` 或 ` doc.validateSync()` 手动运行验证
  * 验证器不在未定义的值上运行。 唯一的例外是 [required的验证器](http://mongoosejs.com/docs/api.html#schematype_SchemaType-required)。
  * 验证是异步递归的; 当您调用 [Model#save](http://mongoosejs.com/docs/api.html#model_Model-save) 时，也会执行子文档验证。如果发生错误，您的 [Model#save] 回调会收到它
  * 验证是可定制的

```js
var schema = new Schema({
 name: {
   type: String,
   required: true
 }
});
var Cat = db.model('Cat', schema);

// This cat has no name :(
var cat = new Cat();
cat.save(function(error) {
 assert.equal(error.errors['name'].message,
   'Path `name` is required.');

 error = cat.validateSync();
 assert.equal(error.errors['name'].message,
   'Path `name` is required.');
});
```

## 内置验证器

Mongoose 有几个内置的验证器。

  * 所有 [SchemaTypes](/Library/mongoose/docs/SchemaType.md) 都有内置的 [required](http://mongoosejs.com/docs/api.html#schematype_SchemaType-required) 验证器。 required 的验证器使用 SchemaType 的 [`checkRequired()`](http://mongoosejs.com/docs/api.html#schematype_SchemaType-checkRequired) 函数来确定该值是否满足 required 验证器。
  * 数字有 [min](http://mongoosejs.com/docs/api.html#schema_number_SchemaNumber-min) 和 [max](http://mongoosejs.com/docs/api.html#schema_number_SchemaNumber-max) 验证器。
  * 字符串有 [enum](http://mongoosejs.com/docs/api.html#schema_string_SchemaString-enum)、[match](http://mongoosejs.com/docs/api.html#schema_string_SchemaString-match)、[maxlength](http://mongoosejs.com/docs/api.html#schema_string_SchemaString-maxlength) 和 [minlength](http://mongoosejs.com/docs/api.html#schema_string_SchemaString-minlength) 验证器。

```js
var breakfastSchema = new Schema({
  eggs: {
    type: Number,
    min: [6, 'Too few eggs'],
    max: 12
  },
  bacon: {
    type: Number,
    required: [true, 'Why no bacon?']
  },
  drink: {
    type: String,
    enum: ['Coffee', 'Tea'],
    required: function() {
      return this.bacon > 3;
    }
  }
});
var Breakfast = db.model('Breakfast', breakfastSchema);

var badBreakfast = new Breakfast({
  eggs: 2,
  bacon: 0,
  drink: 'Milk'
});
var error = badBreakfast.validateSync();
assert.equal(error.errors['eggs'].message,
  'Too few eggs');
assert.ok(!error.errors['bacon']);
assert.equal(error.errors['drink'].message,
  '`Milk` is not a valid enum value for path `drink`.');

badBreakfast.bacon = 5;
badBreakfast.drink = null;

error = badBreakfast.validateSync();
assert.equal(error.errors['drink'].message, 'Path `drink` is required.');

badBreakfast.bacon = null;
error = badBreakfast.validateSync();
assert.equal(error.errors['bacon'].message, 'Why no bacon?');
```

## `unique` 选项不是验证器

初学者常见的一个问题是，模式的 `unique` 选项不是验证器。这是构建 MongoDB 唯一索引的便利帮手。查看[常见问题](/Library/mongoose/docs/faq.md)了解更多信息。

```js
var uniqueUsernameSchema = new Schema({
  username: {
    type: String,
    unique: true
  }
});
var U1 = db.model('U1', uniqueUsernameSchema);
var U2 = db.model('U2', uniqueUsernameSchema);

var dup = [{ username: 'Val' }, { username: 'Val' }];
U1.create(dup, function(error) {
  // 将成功保存
});

// 保存前需要等待索引完成建设，
    // 否则 unique 的约束可能会被违反。
U2.on('index', function(error) {
  assert.ifError(error);
  U2.create(dup, function(error) {
    // 将可能发生错误，但**不是** 一个 mongoose 验证器错误
    // 将是一个重复的键错误
    assert.ok(error);
    assert.ok(!error.errors);
    assert.ok(error.message.indexOf('duplicate key error') !== -1);
  });
});

// 还有一个基于 promise 的等价事件发射器 API。
    // `init()` 函数是幂等的，并返回一个 promise
    //一旦建立索引完成就会 resolve;
U2.init().then(function() {
  U2.create(dup, function(error) {
    // 将发生错误，但**不是** 一个 mongoose 验证器错误
    // 将是一个重复的键错误
    assert.ok(error);
    assert.ok(!error.errors);
    assert.ok(error.message.indexOf('duplicate key error') !== -1);
  });
});

```

## 异步的自定义验证器

定制验证器也可以是异步的。如果验证器函数接受2个参数，那么 mongoose 会认为第二个参数是一个回调函数。

即使你不想使用异步验证器，也要小心，因为 mongoose 4 会假设所有带有 2 个参数的函数都是异步的，比如[validator.isEmail](https://www.npmjs.com/package/validator) 函数。 从 4.9.0 开始，此行为被视为弃用，您可以通过在自定义验证器上指定 `isAsync: false` 来关闭它。

```js
var userSchema = new Schema({
  phone: {
    type: String,
    validate: {
      // 在 mongoose 4.x 中，`isAsync` 不是必须的
      // 但是依赖于 2 个参数验证器是异步的这种行为被弃用。
      // 将 `isAsync` 选项设置为 `true` ，以使弃用警告消失。
      // v 为需要被验证的值，cb 为回调函数，但都不需要自己传入
      isAsync: true,
      validator: function(v, cb) {
        setTimeout(function() {
          var phoneRegex = /\d{3}-\d{3}-\d{4}/;
          var msg = v + ' is not a valid phone number!';
          // 第一个参数是一个布尔值，验证器是否成功
          // 第二个参数是一个可选的错误消息覆盖
          cb(phoneRegex.test(v), msg);
        }, 5);
      },
      // 默认的错误消息，被 `cb()` 的第二个参数覆盖
      message: 'Default error message'
    },
    required: [true, 'User phone number required']
  },
  name: {
    type: String,
    // 你也可以创建一个返回 promise 的异步验证器。
    // 如果你返回了一个 promise，不要指定 `isAsync` 选项
    validate: function(v) {
      return new Promise(function(resolve, reject) {
        setTimeout(function() {
          resolve(false);
        }, 5);
      });
    }
  }
});

var User = db.model('User', userSchema);
var user = new User();
var error;

user.phone = '555.0123';
user.name = 'test';
user.validate(function(error) {
  assert.ok(error);
  assert.equal(error.errors['phone'].message,
    '555.0123 is not a valid phone number!');
  assert.equal(error.errors['name'].message,
    'Validator failed for path `name` with value `test`');
});
```

## 验证错误

验证失败后返回的错误包含一个错误对象，其值为ValidatorError对象。 每个 [ValidatorError](http://mongoosejs.com/docs/api.html#error-validation-js) 都有 kind、 path、value 和 message 属性。 ValidatorError 也可能有一个 reason 属性。 如果错误在验证器中被抛出，这个属性将包含抛出的错误。

```js
var toySchema = new Schema({
    color: String,
    name: String
  });

  var validator = function(value) {
    return /red|white|gold/i.test(value);
  };
  toySchema.path('color').validate(validator,
    'Color `{VALUE}` not valid', 'Invalid color');
  toySchema.path('name').validate(function(v) {
    if (v !== 'Turbo Man') {
      throw new Error('Need to get a Turbo Man for Christmas');
    }
    return true;
  }, 'Name `{VALUE}` is not valid');

  var Toy = db.model('Toy', toySchema);

  var toy = new Toy({ color: 'Green', name: 'Power Ranger' });

  toy.save(function (err) {
    // `err` is a ValidationError object
    // `err.errors.color` is a ValidatorError object
    assert.equal(err.errors.color.message, 'Color `Green` not valid');
    assert.equal(err.errors.color.kind, 'Invalid color');
    assert.equal(err.errors.color.path, 'color');
    assert.equal(err.errors.color.value, 'Green');

    assert.equal(err.errors.name.message, 'Name `Power Ranger` is not valid');
    assert.equal(err.errors.name.value, 'Power Ranger');
    assert.equal(err.errors.name.reason.message,
      'Need to get a Turbo Man for Christmas');

    assert.equal(err.name, 'ValidationError');
  });
  ```

## 嵌套对象上的Required 验证器

在 mongoose 中的嵌套对象上定义验证器是非常棘手的，因为嵌套对象不是完全成熟的路径。

```js
var personSchema = new Schema({
 name: {
   first: String,
   last: String
 }
});

assert.throws(function() {
 // 这将抛出一个 error, 因为 'name' 不是一个完全成熟的路径
 personSchema.path('name').required(true);
}, /Cannot.*'required'/);

// 要使一个嵌套对象 required，请使用一个嵌套的 schema
var nameSchema = new Schema({
 first: String,
 last: String
});

personSchema = new Schema({
 name: {
   type: nameSchema,
   required: true
 }
});

var Person = db.model('Person', personSchema);

var person = new Person();
var error = person.validateSync();
assert.ok(error.errors['name']);
```

## 更新验证器 {#built-in-validators}

在上面的例子中，您了解了文档验证。 Mongoose 还支持 `update()` 和 `findOneAndUpdate()` 操作的验证。 在Mongoose 4.x 中，更新验证器默认是关闭的 —— 您需要指定 `runValidators` 选项。

要打开更新验证器，请为 `update()` 或 `findOneAndUpdate()` 设置 `runValidators` 选项。 小心：更新验证器默认关闭，因为他们有几个警告。

```js
var toySchema = new Schema({
    color: String,
    name: String
  });

  var Toy = db.model('Toys', toySchema);

  Toy.schema.path('color').validate(function (value) {
    return /blue|green|white|red|orange|periwinkle/i.test(value);
  }, 'Invalid color');

  var opts = { runValidators: true };
  Toy.update({}, { color: 'bacon' }, opts, function (err) {
    assert.equal(err.errors.color.message,
      'Invalid color');
  });
  ```

## 更新验证器和 `this`

更新验证器和文档验证器之间有几个关键的区别。 在上面的颜色验证函数中，`this` 指向在使用文档验证时正在被验证的文档。但是，在运行更新验证器时，正在更新的文档可能不在服务器的内存中，所以默认情况下 `this` 值没有被定义。

```js
var toySchema = new Schema({
    color: String,
    name: String
  });

  toySchema.path('color').validate(function(value) {
    // 当在 `validate()` 或 `validateSync()` 中运行时，
    // 验证器可以使用 `this` 访问文档
    // 但是**不能**在更新验证器中这样使用
    if (this.name.toLowerCase().indexOf('red') !== -1) {
      return value !== 'red';
    }
    return true;
  });

  var Toy = db.model('ActionFigure', toySchema);

  var toy = new Toy({ color: 'red', name: 'Red Power Ranger' });
  var error = toy.validateSync();
  assert.ok(error.errors['color']);

  var update = { color: 'red', name: 'Red Power Ranger' };
  var opts = { runValidators: true };

  Toy.update({}, update, opts, function(error) {
    // update validator 抛出一个错误 :
    // "TypeError: Cannot read property 'toLowerCase' of undefined",
    // because `this` is **not** the document being updated when using
    // update validators
    assert.ok(error);
  });

```

## `context` 选项

`context` 选项允许您将更新验证器中 `this` 的值设置为基础查询对象。

```js
toySchema.path('color').validate(function(value) {
   // 当运行 `context` 选项设置为 'query' 的更新验证器时
   // `this` 指向 query 对象
   if (this.getUpdate().$set.name.toLowerCase().indexOf('red') !== -1) {
     return value === 'red';
   }
   return true;
 });

 var Toy = db.model('Figure', toySchema);

 var update = { color: 'blue', name: 'Red Power Ranger' };
 // 注意 context 选项
 var opts = { runValidators: true, context: 'query' };

 Toy.update({}, update, opts, function(error) {
   assert.ok(error.errors['color']);
 });
```

## 更新验证器路径

另一个关键区别是，更新验证器仅在更新中指定的路径上运行。例如，在下面的例子中，因为更新操作中没有指定 `'name'`，所以更新验证将成功。

当使用更新验证器时，required 验证器**仅在**您试图显式 `$unset` 键（「译者注」：也就是删除 schema 某项属性）时才会失败。

```js
var kittenSchema = new Schema({
    name: { type: String, required: true },
    age: Number
  });

  var Kitten = db.model('Kitten', kittenSchema);

  var update = { color: 'blue' };
  var opts = { runValidators: true };
  Kitten.update({}, update, opts, function(err) {
    // 操作成功，尽管事实上没有指定 'name'
  });

  var unset = { $unset: { name: 1 } };
  Kitten.update({}, unset, opts, function(err) {
    // Operation fails because 'name' is required
    assert.ok(err);
    assert.ok(err.errors['name']);
  });

```

## 更新验证器仅运行在指定的路径上

最后一个细节值得注意：更新验证器只能在以下更新操作符上运行：

*`$set` * `$unset` * `$push` (>= 4.8.0) * `$addToSet` (>= 4.8.0) * `$pull` (>= 4.12.0) * `$pullAll` (>= 4.12.0)

例如，下面的更新会成功，不管数字的值是多少，因为更新验证器忽略 `$inc`。 另外，`$push`，`$addToSet`，`$pull` 和 `$pullAll` 验证不会在数组本身上运行任何验证，只会对数组中的单个元素进行验证。

```js

  var testSchema = new Schema({
    number: { type: Number, max: 0 },
    arr: [{ message: { type: String, maxLength: 10 } }]
  });

  // 更新验证器不会检查这个，所以你仍然可以在数组上加上 `$push` 2 个元素，只要它们没有太长的 `message'。
  testSchema.path('arr').validate(function(v) {
    return v.length < 2;
  });

  var Test = db.model('Test', testSchema);

  var update = { $inc: { number: 1 } };
  var opts = { runValidators: true };
  Test.update({}, update, opts, function(error) {
    // 这里永远不会有验证错误
    update = { $push: [{ message: 'hello' }, { message: 'world' }] };
    Test.update({}, update, opts, function(error) {
      // 即使数组至少有 2 个元素，这也不会出错。
    });
  });

```

## 关于 `$push` 和 `$addToSet`


4.8.0 中的新增功能：更新验证器也在 `$push `和 `$addToSet` 上运行

```js
var testSchema = new Schema({
   numbers: [{ type: Number, max: 0 }],
   docs: [{
     name: { type: String, required: true }
   }]
 });

 var Test = db.model('TestPush', testSchema);

 var update = {
   $push: {
     numbers: 1,
     docs: { name: null }
   }
 };
 var opts = { runValidators: true };
 Test.update({}, update, opts, function(error) {
   assert.ok(error.errors['numbers']);
   assert.ok(error.errors['docs']);
 });

```

## 其他示例

[单验证器数组](/Library/mongoose/docs/API.md#SchemaType_validate):

```js
var custom = [validator, 'Uh oh, {PATH} does not equal "something".']
new Schema({ name: { type: String, validate: custom }});
```

[多验证器数组](/Library/mongoose/docs/API.md#SchemaType_validate)：

```js
var many = [
    { validator: validator, msg: 'uh oh' }
  , { validator: anotherValidator, msg: 'failed' }
]
new Schema({ name: { type: String, validate: many }});
```
