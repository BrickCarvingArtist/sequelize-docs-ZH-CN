> 翻译自 [http://docs.sequelizejs.com/class/lib/model.js~Model.html#instance-method-truncate](http://docs.sequelizejs.com/class/lib/model.js~Model.html#instance-method-truncate)

> public truncate(options：对象)：Promise

删除所有通过sequelize各模型定义的表中的数据。通过调用每个模型的Model.truncate()以达成。

### 参数
名称 | 数据类型 | 属性 | 描述
-- | -- | -- | --
options | object | 可选配置 | 除了传递给truncate以外的要传给Model.destroy的参数
options.transaction | Boolean或function | 可选配置
options.logging | Boolean或function | | 一个打印各sql语句的方法，或者false表示不打印

### 返回值：
Promise

## 参见：
[Model.truncate](https://github.com/BrickCarvingArtist/sequelize-docs-ZH-CN/blob/master/model/truncate.md)以获取更多信息