> 翻译自 [http://docs.sequelizejs.com/class/lib/transaction.js~Transaction.html#instance-constructor-constructor](http://docs.sequelizejs.com/class/lib/transaction.js~Transaction.html#instance-constructor-constructor)

> public constructor(sequelize：Sequelize, options：对象)

### 参数：
名称 | 数据类型 | 属性 | 描述
-- | -- | -- | --
sequelize | Sequelize | | 一个配置好的sequelize实例
options | Object | | 一个含各配置的对象
options.autocommit | Boolean | 设置事务的自动提交属性。
options.type | String | 默认值：true | 设置事务的类型。
options.isolationLevel | String | 默认值：true | 设置事务的隔离层级。
options.deferrable | String | 设置各约束是要延迟或是立即检验。