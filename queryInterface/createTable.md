> 翻译自 [http://docs.sequelizejs.com/class/lib/query-interface.js~QueryInterface.html#instance-method-createTable](http://docs.sequelizejs.com/class/lib/query-interface.js~QueryInterface.html#instance-method-createTable)

> public createTable(tableName：字符串, attribtues：数组, options：对象, model：[模型]())：Promise

创建一张带有一系列给定的各属性的表

```js
queryInterface.createTable(
  '新表的表名',
  {
    id: {
      type: Sequelize.INTEGER,
      primaryKey: true,
      autoIncrement: true
    },
    createdAt: {
      type: Sequelize.DATE
    },
    updatedAt: {
      type: Sequelize.DATE
    },
    attr1: Sequelize.STRING,
    attr2: Sequelize.INTEGER,
    attr3: {
      type: Sequelize.BOOLEAN,
      defaultValue: false,
      allowNull: false
    },
    // 外键的用法
    attr4: {
      type: Sequelize.INTEGER,
      references: {
        model: 'another_table_name',
        key: 'id'
      },
      onUpdate: 'cascade',
      onDelete: 'cascade'
    }
  },
  {
    engine: 'MYISAM',    // 默认值：'InnoDB'
    charset: 'latin1',   // 默认值：null
    schema: 'public'     // 默认值：public，仅限PostgreSQL。
  }
)
```

### 参数：
名称 | 数据类型 | 属性 | 描述
-- | -- | -- | --
tableName | String | | 要创建的表名
attributes | Array | | 要创建的表的一列属性
options | Object | 可选配置
model | [Model]() | 可选配置

### 返回值：
Promise