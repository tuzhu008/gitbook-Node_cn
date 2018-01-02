# 快速入门

首先，要确定安装了 [MongoDB](http://www.mongodb.org.cn/) 和 [Node.js](http://nodejs.cn/) 。

接下来，使用 npm 命令安装 mongoose :

```bash
$ npm install mongoose
```

现在加入我们喜欢 fuzzy kittens，想要将我们遇到的每只喵咪记录下在 MongoDB 中。我们需要做的第一件事是在我们的项目中包含 mongoose，并在本地运行的 MongoDB 实例上打开与测试数据库的连接。

```js
// getting-started.js
var mongoose = require('mongoose');
mongoose.connect('mongodb://mongodb://127.0.0.1:27017');
```

我们有一个挂起的连接到本地主机上运行的测试数据库。如果我们连接成功或发生连接错误，我们现在需要得到通知：

```js
var db = mongoose.connection;
db.on('error', console.error.bind(console, 'connection error:'));
db.once('open', function() {
  // we're connected!
});
```

一旦我们的连接打开，我们的回调将被调用。为简洁起见，我们假设以下所有代码都位于此回调中。

Mongoose，一切都是从 Schema 派生的。 让我们来引用它，并定义我们的小猫。

```js
var kittySchema = mongoose.Schema({
    name: String
});
```

目前为止一切都很顺利。我们有一个属性——名称的 schema，这个属性将是一个字符串。 下一步是将我们的 schema 编译到模型中。

```js
var Kitten = mongoose.model('Kitten', kittySchema);
```

模型是我们构造文档的类。在这种情况下，每个文档将是一个小猫，其特性和行为在我们的模式中声明。让我们创建一个小猫文档，代表我们刚刚在外面的人行道上遇到的小家伙：

```js
var silence = new Kitten({ name: 'Silence' });
console.log(silence.name); // 'Silence'
```

小猫可以喵喵叫，那么让我们来看看如何在我们的文档中添加 “speak” 功能：

```js
// 注意: 在使用 mongoose.model() 编译之前，必须将 methods 添加到模式中
kittySchema.methods.speak = function () {
  var greeting = this.name
    ? "Meow name is " + this.name
    : "I don't have a name";
  console.log(greeting);
}

var Kitten = mongoose.model('Kitten', kittySchema);
```

添加到模式方法属性的函数被编译到模型原型中，并暴露在每个文档实例上：

```js
var fluffy = new Kitten({ name: 'fluffy' });
fluffy.speak(); // "Meow name is fluffy"
```

我们有会说话的小喵啦！但是我们还没有保存任何东西到 MongoDB。每个文档可以通过调用其保存方法保存到数据库中。回调的第一个参数将是一个错误，如果发生了任何错误的话。

```js
fluffy.save(function (err, fluffy) {
  if (err) return console.error(err);
  fluffy.speak();
});
```

时间流逝，我们想要展示我们看到的所有的小猫。我们可以通过我们的 Kitten 模型来访问所有的小猫文档。


```js
Kitten.find(function (err, kittens) {
  if (err) return console.error(err);
  console.log(kittens);
})
```

我们只把我们的数据库中的所有小猫记录到控制台。如果我们想按名称来过滤我们的小猫，Mongoose 支持 MongoDB 丰富的查询语法。


```js
Kitten.find({ name: /^fluff/ }, callback);
```

这将搜索名称属性以“fluff”开头的所有文档，并将结果作为小猫数组返回给回调。

祝贺!祝贺!
这是我们快速启动的结束。我们创建了一个模式，添加了一个自定义的文档方法，使用 Mongoose 在 MongoDB 中保存并查询了小猫。请转到[指南](/Library/mongoose/docs/guide.md)或[API文档](/Library/mongoose/docs/API.md)了解更多信息。

![](/assets/images/mongoose/mongoose.svg)

> **[info] 笔记**
>
> 如上图所示
>
> Schema 是所谓模式，类比可以是某个型号的汽车，这个型号的汽车有机动车车架号（唯一）、全景天窗，车长，扭矩，涡轮增压等等属性，并且有启动、刹车、加速等方法。
>
> Model  是所谓模型，类比是这个特定型号的汽车的生产线，所有的汽车都在这里下线。
>
> document 文档，类比则是某一辆具体的车，比如张三买了一辆，车牌号为：火A00000、李四买了一辆，车牌号为：火A88888。
>
> 如下图所示：

![](/assets/images/mongoose/car.svg)
