> 翻译自 [http://docs.sequelizejs.com/class/lib/model.js~Model.html#static-method-sync](http://docs.sequelizejs.com/class/lib/model.js~Model.html#static-method-sync)

> public static sync（配置：*）：Promise\<this>

同步模型到数据库，也就是创建表。当成功的时候，回调函数将会被模型实例（this）所调用

### 参数：
名称 | 数据类型 | 属性 | 描述
-- | -- | -- | --
options | *

### 返回值：
Promise\<this>

### 参见：
Sequelize#sync获取配置