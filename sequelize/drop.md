> 翻译自 [http://docs.sequelizejs.com/class/lib/model.js~Model.html#instance-method-drop](http://docs.sequelizejs.com/class/lib/model.js~Model.html#instance-method-drop)

> public drop(options：对象)：Promise

删除所有通过这个sequelize实例定义的表。通过调用每个模型的Model.drop以达成。

### 参数：
名称 | 数据类型 | 属性 | 描述
-- | -- | -- | --
options | object | | 传给每次调用Model.drop中的各配置选项
options.logging | Boolean或function | 一个打印各sql语句的方法，或者false表示不打印

### 返回值：
Promise

### 参见：
[Model.drop](https://github.com/BrickCarvingArtist/sequelize-docs-ZH-CN/blob/master/model/drop.md)获取各配置选项