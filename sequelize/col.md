> 翻译自 [http://docs.sequelizejs.com/class/lib/sequelize.js~Sequelize.html#instance-method-col](http://docs.sequelizejs.com/class/lib/sequelize.js~Sequelize.html#instance-method-col)

> public static col(col：字符串)：[col](https://github.com/BrickCarvingArtist/sequelize-docs-ZH-CN/blob/master/sequelize/col.md)自v2.0.0-dev3起

创建一个在数据库中代表一列的对象，这允许在你的查询语句中引用另一列。这在与`sequelize.fn`同时使用时常常很有用，因此各未经处理的字符串参数都将被转义。

### 参数：
名称 | 数据类型 | 属性 | 描述
-- | -- | -- | --
col | String | | 列名

### 返回值：
[col](https://github.com/BrickCarvingArtist/sequelize-docs-ZH-CN/blob/master/sequelize/col.md)

### 参见：
Sequelize#fn