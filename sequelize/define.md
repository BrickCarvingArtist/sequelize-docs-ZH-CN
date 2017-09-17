> 翻译自 [http://docs.sequelizejs.com/class/lib/sequelize.js~Sequelize.html#instance-method-define](http://docs.sequelizejs.com/class/lib/sequelize.js~Sequelize.html#instance-method-define)

> public define（模型名称：字符串，属性：对象，配置：对象）：[Model]()

定义一个新的模型，代表数据库里的一个表。

表的列被一个提供在第二个参数的对象所定义。对象的每一个键代表着一列

### 参数：
名称 | 数据类型 | 属性 | 描述
-- | -- | -- | --
modelName | String | | 模型的名称。模型会以这个名字被保存到`sequelize.models`中
attributes | Object | |  一个对象，它的每一个属性都是表格的一列。参见[Model.init]()
options | Object | 可选配置 | 这些配置被与默认的定义配置合并被提供给Sequelize的构造函数以及被传递给Model.init()

### 返回值：
[Model]()

### 举个例子：

```js
sequelize.define('modelName', {
    columnA: {
        type: Sequelize.BOOLEAN,
        validate: {
          is: ["[a-z]",'i'],        // 将只允许字母
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
})

sequelize.models.modelName // 这个模型现在将是基于传给define的name在models中启用。（译者注：说白了就是sequelize的models这个属性里的，你传给sequelize.define的模型的名称属性就是这个模型）
```

### 参见：
[Model.init]()查看一个更综合的对`options`及`attributes`对象的定义。

[关于定义模型的手册章节]()

[数据类型]()查看一列的可用数据类型的列表
