# Plugins（插件）

模式是可插拔的，也就是说，它们允许应用预先打包的功能来扩展其功能。这是一个非常强大的特性。

假设我们的数据库中有多个集合，并且想要为每个集合添加「最后修改」的功能。用插件这很容易。只需创建一个插件并将其应用于每个模式：

```js
// lastMod.js
module.exports = exports = function lastModifiedPlugin (schema, options) {
  schema.add({ lastMod: Date })

  schema.pre('save', function (next) {
    this.lastMod = new Date
    next()
  })

  if (options && options.index) {
    schema.path('lastMod').index(options.index)
  }
}

// game-schema.js
var lastMod = require('./lastMod');
var Game = new Schema({ ... });
Game.plugin(lastMod, { index: true });

// player-schema.js
var lastMod = require('./lastMod');
var Player = new Schema({ ... });
Player.plugin(lastMod);
```

我们刚刚添加了「最后修改」的行为到我们的 `Game` 和 `Player` 模式，并在我们的 Game 的 `lastMod` 路径上声明一个索引。对于几行代码来说，这是不错的。

## 全局插件

想要为所有模式注册一个插件？ mongoose 单例有一个 `.plugin()` 函数，为每个模式注册一个插件。例如：

```js
var mongoose = require('mongoose');
mongoose.plugin(require('./lastMod'));

var gameSchema = new Schema({ ... });
var playerSchema = new Schema({ ... });
// `lastModifiedPlugin` gets attached to both schemas
var Game = mongoose.model('Game', gameSchema);
var Player = mongoose.model('Player', playerSchema);

```

## 社区！

您不仅可以在自己的项目中重新使用模式功能，还可以从 Mongoose 社区获得好处。任何发布到 [npm](https://npmjs.org/) 并带有 `mongoose` [标签](https://npmjs.org/doc/tag.html)的插件都会显示在我们的[搜索结果](http://plugins.mongoosejs.com/)页面上。

## 接下来

现在我们已经介绍了插件，以及如何参与围绕它们的伟大社区，让我们来看看如何为 Mongoose 本身的持续发展做出[贡献](https://github.com/Automattic/mongoose/blob/master/CONTRIBUTING.md)。
