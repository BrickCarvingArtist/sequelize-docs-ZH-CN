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

### 参数：
名称 | 数据类型 | 属性 | 描述
-- | -- | -- | --
attributes | Object | | 一个对象，它的每一个属性都是表格的一列。每列既可以是一个数据类型，字符串或一个以如下特性来描述类型的对象：
attributes.column | String或[DataTypes]()或Object | | 对数据库列的描述
attributes.column.type | String或[DataTypes]() | | 一个字符串或一个数据的类型
attributes.column.allowNull | Boolean | 可选配置，默认值：true | 如果是false，这一列将会有一个非空约束，并且会在是被存储之前运行一个非空校验。
attributes.column.defaultValue | any | 可选配置，默认值：null | 一个字面上的默认值，一个JavaScript函数，或一个SQL函数（参见`sequelize.fn`）
attributes.column.unique | String或Boolean | 可选配置，默认值：false | 如果是true，这一列将获得一个唯一约束。如果被提供的是一个字符串，这一列将会成为混合唯一索引的一部分。如果多个列拥有同样的字符串，它们都会成为同一唯一索引的一部分
attributes.column.primaryKey | Boolean | 可选配置，默认值：false
attributes.column.field | String | 可选配置，默认值：null | 如果设置了，sequelize会在数据库中以不同的名称匹配这个属性名
attributes.column.autoIncrement | Boolean | 可选配置，默认值：false
attributes.column.comment | String | 可选配置，默认值：null
attributes.column.references | String或[Model]() | 可选配置，默认值：null | 一个包含引用配置的对象
attributes.column.references.model | String或Model | 可选配置 | 如果这一列饮用了其他表，用一个Model或者string提供它到这里
attributes.column.references.key | String | 可选配置，默认值：'id' | 这个表所引用的外部表的列
attributes.column.onUpdate | String | 可选配置 | 当被引用的键更新时该作何反应。CASCADE，RESTRICT，SET DEFAULT，SET NULL或NO ACTION中的任一。
attributes.column.onDelete | String | 可选配置 | 当被引用的键更新时该作何反应。CASCADE，RESTRICT，SET DEFAULT，SET NULL或NO ACTION中的任一。
attributes.column.get | Function | 可选配置 | 为这一列设置一个个性化的获取器。使用`this.getDataValue(String)`来操作底层的值。
attributes.column.set | Function | 可选配置 | 为这一列提供一个个性化的设置器。使用`this.getDataValue(String)`来操作底层的值。
attributes.validate | Object | 可选配置 | 模型在任意时间被存储试为这列执行校验的一个对象。既可以是一个由`validator.js`提供的校验的名字，又可以是一个由进击的`validator.js`（更多细节参见`DAOValidator`的特性）所提供的校验函数，或者一个个性化的校验函数。各个性化校验函数被域的值所调用，并极有可能带着第二个回调函数参数，以示意它们是异步的。如果校验器是同步的，就失败的校验来说它需要抛错，如果它是同步的，回调函数需要带着错误文本被调用。
options | Object | 可选配置 | 这些配置与提供给Sequelize构造函数中的默认的定义选项进行合并。
options.defaultScope | Object | 可选配置，默认值：{} | 定义用于此模型的默认搜索范围。各范围与被传给`find`或`fillAll`的选项是同样的规制。
options.scopes | Object | 可选配置 | 更多的范围，与上面的默认范围是同样的定义方式。更多关于各范围是如何被定义的，及你能与它们做些什么的信息参见`Model.scope`
options.omitNull | Boolean | 可选配置 | 不存留null值。这意味着所有包含null值的列都不会被存储
options.timestamps | Boolean | 可选配置，默认值：true | 添加创建于和更新于时间戳到模型上。
options.paranoid | Boolean | 可选配置，默认值：false | 调用`destory`将不删除模型，当这个值为true时取而代之的是设置一个`deleteAt`的时间戳。需要`timestamps=true`得以运作。