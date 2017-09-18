> 翻译自 [http://docs.sequelizejs.com/class/lib/model.js~Model.html#static-method-init](http://docs.sequelizejs.com/class/lib/model.js~Model.html#static-method-init)

> public static init（属性：对象，配置：对象）：[Model]()

初始化一个模型，代表数据库里的一个表，以及属性和配置。

表的列以一个被给在第二个参数的哈希定义。哈希中的每一个属性代表一列。一个短的表定义大概像这样：

```js
Project.init({
  columnA: {
    type: Sequelize.BOOLEAN,
    validate: {
      is: ['[a-z]','i'],        // 将只允许字母
      max: 23,                  // 只允许值小于23
      isIn: {
        args: [['en', 'zh']],
        msg: "Must be English or Chinese"
      }
    },
    field: 'column_a'
    // 其他的属性（继续往后）写在这里
  },
  columnB: Sequelize.STRING,
  columnC: '我的非常个人的表类型'
}, {sequelize})

sequelize.models.modelName // 这个模型现在将是基于传给define的name在models中启用。（译者注：说白了就是sequelize的models这个属性里的，你传给sequelize.define的模型的名称属性就是这个模型）
```

如上所示，列定义既可以是字符串，一个对任一被预定义在Sequelize构造函数上的数据类型的引用，又可以是一个允许你同时定义列的类型和其他诸如默认值，外键约束和个性化setter和getter的属性的对象。

获取一个可用数据类型列表，参见[DataTypes]()

获取更多关于校验（的内容），参见[https://github.com/BrickCarvingArtist/sequelize-docs-ZH-CN/blob/master/validation.md](https://github.com/BrickCarvingArtist/sequelize-docs-ZH-CN/blob/master/validation.md)