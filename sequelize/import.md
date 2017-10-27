> 翻译自 [http://docs.sequelizejs.com/class/lib/sequelize.js~Sequelize.html#instance-method-import](http://docs.sequelizejs.com/class/lib/sequelize.js~Sequelize.html#instance-method-import)

> public import(path：字符串)：[Model]()

导入一个由另一文件定义的模型  

已导入的模型被缓存起来，所以多次调用对统一路径的调用不会多次加载文件  

参见[https://github.com/sequelize/express-example](https://github.com/sequelize/express-example)获取一个简短的关于如何去定义你的拆分开的各文件中的模型例子，这样它们能被以sequelize.import导入

### 参数：
名称 | 数据类型 | 属性 | 描述
-- | -- | -- | --
path | String | | 你想要导入的携带模型的文件的路径。如果这部分是相对的，它将被相对地分解以调用文件。

### 返回值：
[Model]()