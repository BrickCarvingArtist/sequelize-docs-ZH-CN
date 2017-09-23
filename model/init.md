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
options.underscored | Boolean | 可选配置，默认值：false | 如果为true则把所有驼峰命名列转换为下划线命名列。将不影响各由模型选项具名的时间戳的域以及具体设置的`field`选项
options.underscoredAll | Boolean | 可选配置，默认值：false | 如果为true则把所有驼峰命名模型名称转换为下划线命名的表名。当freezeTableName被设为true时将不会更改模型的名称
options.freezeTableName | Boolean | 可选配置，默认值：false | 如果freeTableName为true，sequelize将不尝试通过去更改模型名称来获取表明。反之，模型名称将会是复数形式的
options.name | Object | 可选配置 | 一个拥有两个属性的对象，`singular`和`plural`，它们在模型被与其他（模型）关联时使用。
options.name.singular | String | 可选配置，默认值：Utils.singularize(模型名称)
options.name.plural | String | 可选配置，默认值：Utils.pluralize(模型名称)
options.indexes | Array\<Object> | 可选配置
options.indexes[].name | String | 可选配置 | 索引的名称。默认为模型名 + _ + 被联系起来的域
options.indexes[].type | String | 可选配置 | 索引类型。仅限mysql使用。UNIQUE，FULLTEXT和SPATIAL中的任一。
options.indexes[].method | String | 可选配置 | 用（SQL中的`USING`语句）以创建索引的方法。BTREE和HASH是被mysql和postgre支持的，而且postgre还额外支持GIST和GIN。
options.indexes[].unique | Boolean | 可选配置，默认值：false | 索引需要唯一吗？也能通过设置类型为UNIQUE被触发
options.indexes[].concurrently | Boolean | 可选配置，默认值：false | PostgreSQL将不带上任何写入锁来构建索引。仅限Postgre
options.indexes[].fields | Array\<String或Object> | 可选配置 | 一个各索引的域数组。每一个域既能是一个包含域名的字符串，又能是一个sequelize对象（如`sequelize.fn`），或一个携带以下属性的对象：attribute（域的名称），length（创建一个长度char的前缀索引），order（列需要被排序的顺序），collate（列的（排序顺序）集合）
options.createdAt | String或Boolean | 可选配置 | 当被提供的是一个字符串时覆盖createAt列的名字，当为false时不启用（这一列）。时间戳必须为true。不受下划线设置的影响。
options.updatedAt | String或Boolean | 可选配置 | 当被提供的是一个字符串时覆盖updatedAt列的名字，当为false时不启用（这一列）。时间戳必须为true。不受下划线设置的影响。
options.deletedAt | String或Boolean | 可选配置 | 当被提供的是一个字符串时覆盖deletedAt列的名字，当为false时不启用（这一列）。时间戳必须为true。不受下划线设置的影响。
options.tableName | String | 可选配置 | 默认为复数形式的模型名称，除非freezeTableName是true，才会一字不差地使用模型名称
options.schema | String | 可选配置，默认值：'public'
options.engine | String | 可选配置
options.charset | String | 可选配置
options.comment | String | 可选配置
options.collate | String | 可选配置
options.initialAutoIncrement | String | 可选配置 | 在MySQL中设置初始化AUTO_INCREMENT值。
options.hooks | Object | optional | 一个在特定生命周期事件中被调用的钩子函数对象。可能的钩子有：beforeValidate，afterValidate，validationFailed，beforeBulkCreate，beforeBulkDestroy，beforeBulkUpdate，beforeCreate，beforeDestroy，beforeUpdate，afterCreate，afterDestroy，afterUpdate， afterBulkCreate，afterBulkDestory和afterBulkUpdate。更多关于钩子函数和它们的用法说明参见钩子。
options.validate | Object | 可选配置 | 一个模型的广义校验对象。校验通过这个对象触及所有模型的值。如果校验器方法带着一个参数，它被冒充成异步的，并且被一个接受一个带有可选的错误的回调函数所调用。

### 返回值：

[Model]()

### 参见：

[DataTypes]()

Hooks