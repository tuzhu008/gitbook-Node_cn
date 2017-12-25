# Creating from ES6 Classes Using `oadClass()`

Mongoose 允许从 [ES6 类](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)创建模式（schema）。 `loadClass()` 函数使您可以从 ES6 类中提取 methods，statics 和 virtuals。类方法映射到模式方法，静态方法映射到[模式静态](/Library/mongoose/docs/guide.md#statics)，而 getters/setters 映射到[虚拟属性](/Library/mongoose/docs/guide.md#virtuals)。

```js

    const schema = new Schema({ firstName: String, lastName: String });

    class PersonClass {
      // getter setter
      // `fullName` becomes a virtual
      get fullName() {
        return `${this.firstName} ${this.lastName}`;
      }

      set fullName(v) {
        const firstSpace = v.indexOf(' ');
        this.firstName = v.split(' ')[0];
        this.lastName = firstSpace === -1 ? '' : v.substr(firstSpace + 1);
      }

      // 方法
      // `getFullName()` becomes a document method
      getFullName() {
        return `${this.firstName} ${this.lastName}`;
      }

      // 静态方法
      // `findByFullName()` becomes a static
      static findByFullName(name) {
        const firstSpace = name.indexOf(' ');
        const firstName = name.split(' ')[0];
        const lastName = firstSpace === -1 ? '' : name.substr(firstSpace + 1);
        return this.findOne({ firstName, lastName });
      }
    }

    schema.loadClass(PersonClass);
    var Person = db.model('Person', schema);

    Person.create({ firstName: 'Jon', lastName: 'Snow' }).
      then(doc => {
        assert.equal(doc.fullName, 'Jon Snow');
        doc.fullName = 'Jon Stark';
        assert.equal(doc.firstName, 'Jon');
        assert.equal(doc.lastName, 'Stark');
        return Person.findByFullName('Jon Snow');
      }).
      then(doc => {
        assert.equal(doc.fullName, 'Jon Snow');
      });
  ```
