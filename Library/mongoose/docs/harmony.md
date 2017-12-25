# Documents in ES6

异步的文档函数返回一个 [promises](https://www.npmjs.org/package/mpromise)，因此，与 [ES6 yield 关键字](http://github.com/Automattic/mongoose)和库类似 [co](https://www.npmjs.org/package/co) 的是兼容的。

#### `validate()` 与 co 和 yield 关键字集成

```js
co(function*() {
  var schema = null;
  var called = false;
  var shouldSucceed = true;
  var error;

  var validate = {
    validator: function() {
      called = true;
      return shouldSucceed;
    },
    message: 'BAM'
  };

  schema = new Schema({
    eggs: {type: String, required: true, validate: validate},
    bacon: {type: Boolean, required: true}
  });

  var M = db.model('validateSchema', schema, getCollectionName());
  var m = new M({eggs: 'Sunny side up', bacon: false});

  try {
    yield m.validate();
  } catch (e) {
    error = e;
  }

  assert.ok(!error);
  assert.equal(called, true);
  called = false;

  // The validator function above should now fail
  shouldSucceed = false;
  try {
    yield m.validate();
  } catch (e) {
    error = e;
  }

  assert.ok(error);
  assert.ok(error instanceof ValidationError);

  done();
})();
```

#### `save()` 预 co 和  yield 关键字集成

```js
co(function*() {
  var error;
  var schema = new Schema({
    description: {type: String, required: true}
  });

  var Breakfast = db.model('breakfast', schema, getCollectionName());

  var goodBreakfast = new Breakfast({description: 'eggs & bacon'});

  try {
    yield goodBreakfast.save();
  } catch (e) {
    error = e;
  }

  assert.ifError(error);
  var result;
  try {
    result = yield Breakfast.findOne().exec();
  } catch (e) {
    error = e;
  }
  assert.ifError(error);
  assert.equal(result.description, 'eggs & bacon');

  // Should cause a validation error because `description` is required
  var badBreakfast = new Breakfast({});
  try {
    yield badBreakfast.save();
  } catch (e) {
    error = e;
  }

  assert.ok(error);
  assert.ok(error instanceof ValidationError);

  done();
})();
```
#### `populate()` requires `execPopulate()` 与 yield 关键字

```js

/**
 *  Because the `populate()` function supports chaining, it's difficult
 *  to determine when the chain is 'done'. Therefore, you need to call
 *  `execPopulate()` to use `populate()` with `yield`.
 */
co(function*() {
  var error;
  var breakfastCollectionName = getCollectionName();
  var foodCollectionName = getCollectionName();
  var breakfastSchema = new Schema({
    foods: [{type: mongoose.Schema.ObjectId, ref: foodCollectionName}]
  });

  var foodSchema = new Schema({
    name: String
  });

  var Food = db.model(foodCollectionName, foodSchema, foodCollectionName);
  var Breakfast = db.model(breakfastCollectionName, breakfastSchema, breakfastCollectionName);

  var bacon = new Food({name: 'bacon'});
  var eggs = new Food({name: 'eggs'});
  var goodBreakfast = new Breakfast({foods: [bacon, eggs]});

  try {
    yield [bacon.save(), eggs.save(), goodBreakfast.save()];
  } catch (e) {
    error = e;
  }

  var result;
  try {
    result = yield Breakfast.findOne().exec();
  } catch (e) {
    error = e;
  }
  assert.ifError(error);
  assert.equal(result.foods.length, 2);

  try {
    result = yield result.populate('foods').execPopulate();
  } catch (e) {
    error = e;
  }
  assert.ifError(error);
  assert.equal(result.foods.length, 2);
  assert.equal(result.foods[0].name, 'bacon');
  assert.equal(result.foods[1].name, 'eggs');

  done();
})();
```

#### `update()`  与 co 和 yield 一起工作

```js
co(function*() {
  var schema = new Schema({
    steak: String,
    eggs: String
  });

  var Breakfast = db.model('breakfast', schema, getCollectionName());

  var breakfast = new Breakfast({});
  var error;

  try {
    yield breakfast.update({steak: 'Ribeye', eggs: 'Scrambled'}, {upsert: true}).exec();
  } catch (e) {
    error = e;
  }

  assert.ifError(error);
  var result;
  try {
    result = yield Breakfast.findOne().exec();
  } catch (e) {
    error = e;
  }
  assert.ifError(error);
  assert.equal(breakfast._id.toString(), result._id.toString());
  assert.equal(result.steak, 'Ribeye');
  assert.equal(result.eggs, 'Scrambled');
  done();
})();
```

# Queries in ES6

Mongoose 查询的 `.exec()` 函数返回一个promise， 因此，与 [ES6 yield 关键字](http://github.com/Automattic/mongoose)和库类似 [co](https://www.npmjs.org/package/co) 的是兼容的。

注意，`yield` 关键字目前仅在 NodeJS 0.11 中得到支持，带--harmony flag。

### exec() 与 co 和 yield 关键字集成

```js
co(function*() {
  var schema = new Schema({
    eggs: {type: Number, required: true},
    bacon: {type: Number, required: true}
  });

  var Breakfast = db.model('BreakfastHarmony', schema, getCollectionName());

  try {
    yield Breakfast.create(
      {eggs: 4, bacon: 2},
      {eggs: 3, bacon: 3},
      {eggs: 2, bacon: 4});
  } catch (e) {
    return done(e);
  }

  var result;
  try {
    result = yield Breakfast.findOne({eggs: 4}).exec();
  } catch (e) {
    return done(e);
  }

  assert.equal(result.bacon, 2);

  var results;
  try {
    results = yield Breakfast.find({eggs: {$gt: 2}}).sort({bacon: 1}).exec();
  } catch (e) {
    return done(e);
  }

  assert.equal(results.length, 2);
  assert.equal(results[0].bacon, 2);
  assert.equal(results[1].bacon, 3);

  var count;
  try {
    count = yield Breakfast.count({eggs: {$gt: 2}}).exec();
  } catch (e) {
    return done(e);
  }

  assert.equal(count, 2);

  done();
})();
```

#### 可以调用 `populate()` 与 `exec()`

```js
co(function*() {
  var bookSchema = new Schema({
    author: {type: mongoose.Schema.ObjectId, ref: 'AuthorHarmony'},
    title: String
  });

  var authorSchema = new Schema({
    name: String
  });

  var Book = db.model('BookHarmony', bookSchema, getCollectionName());
  var Author = db.model('AuthorHarmony', authorSchema, getCollectionName());

  try {
    var hugo = yield Author.create({name: 'Victor Hugo'});
    yield Book.create({author: hugo._id, title: 'Les Miserables'});
  } catch (e) {
    return done(e);
  }

  var result;
  try {
    result = yield Book.findOne({title: 'Les Miserables'}).populate('author').exec();
  } catch (e) {
    return done(e);
  }

  assert.equal(result.author.name, 'Victor Hugo');

  done();
})();
```
# Models in ES6

Model的异步函数返回一个promise， 因此，与 [ES6 yield 关键字](http://github.com/Automattic/mongoose)和库类似 [co](https://www.npmjs.org/package/co) 的是兼容的。

注意， 函数 `find()`、 `findOne()`、`findById()`、 `count()`、 `findOneAndUpdate()`、 `remove()`、 `distinct()`、`findByIdAndUpdate()`、 `findOneAndRemove()`、 `update()`、 和 `findByIdAndRemove()` 返回 Query 对象, 所以你需要使用 `.exec()` 来使用带有 `yield` 的上述函数 。

#### `create()` 与 co 和 yield 关键字集成

```js
co(function * () {
  var schema = new Schema({
    eggs: {type: String, required: true},
    bacon: {type: Boolean, required: true}
  });

  var M = db.model('harmonyCreate', schema, getCollectionName());

  var results;
  try {
    results = yield M.create([
      {eggs: 'sunny-side up', bacon: false},
      {eggs: 'scrambled', bacon: true}]);
  } catch (e) {
    return done(e);
  }

  assert.equal(results.length, 2);
  assert.equal(results[0].eggs, 'sunny-side up');
  assert.equal(results[1].eggs, 'scrambled');

  done();
})();
```

#### aggregate() 与 co 和 yield 关键字集成

```js
co(function*() {
var schema = new Schema({
  eggs: {type: String, required: true},
  bacon: {type: Boolean, required: true}
});

var M = db.model('harmonyAggregate', schema, getCollectionName());

try {
  yield M.create([
    {eggs: 'sunny-side up', bacon: false},
    {eggs: 'scrambled', bacon: true}]);
} catch (e) {
  return done(e);
}

var results;
try {
  results = yield M.aggregate([
    {$group: {_id: '$bacon', eggs: {$first: '$eggs'}}},
    {$sort: {_id: 1}}
  ]).exec();
} catch (e) {
  return done(e);
}

assert.equal(results.length, 2);
assert.equal(results[0]._id, false);
assert.equal(results[0].eggs, 'sunny-side up');
assert.equal(results[1]._id, true);
assert.equal(results[1].eggs, 'scrambled');

done();
})();
```

#### mapReduce() 也可以与 co 和 yield 一起使用

```js
co(function*() {
  var schema = new Schema({
    eggs: {type: String, required: true},
    bacon: {type: Boolean, required: true}
  });

  var M = db.model('harmonyMapreduce', schema, getCollectionName());

  try {
    yield M.create([
      {eggs: 'sunny-side up', bacon: false},
      {eggs: 'sunny-side up', bacon: true},
      {eggs: 'scrambled', bacon: true}]);
  } catch (e) {
    return done(e);
  }

  var results;
  try {
    results = yield M.mapReduce({
      map: function() { emit(this.eggs, 1); },
      reduce: function(k, vals) { return vals.length; }
    });
  } catch (e) {
    return done(e);
  }

  assert.equal(results.length, 2);
  assert.ok(results[0]._id === 'sunny-side up' || results[1]._id === 'sunny-side up');
  assert.ok(results[0]._id === 'scrambled' || results[1]._id === 'scrambled');

  done();
})();
```
