> 翻译自 [http://docs.sequelizejs.com/class/lib/query-interface.js~QueryInterface.html#instance-method-addColumn](http://docs.sequelizejs.com/class/lib/query-interface.js~QueryInterface.html#instance-method-addColumn)

> public addColumn(tableName：字符串, key：字符串, attribute：对象, options：对象)：Promise

往表里添加新一列

### 参数：
名称 | 数据类型 | 属性 | 描述
-- | -- | -- | --
table | String | | 将要添加列的表
key | String | | 列名
attribute | Object | | 各属性定义
options | Object | 可选配置 | 语句选项

### 返回值：
Promise