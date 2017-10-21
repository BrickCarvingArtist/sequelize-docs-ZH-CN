> 翻译自 [http://docs.sequelizejs.com/class/lib/model.js~Model.html#static-method-build](http://docs.sequelizejs.com/class/lib/model.js~Model.html#static-method-build)

> public static build(options：对象)：[Model]()或[Model]()[]

构建一个新的模型实例。

### 参数：
名称 | 数据类型 | 属性 | 描述
-- | -- | -- | --
values或values[] | Object | 可选配置，默认值：{} | 一个键值对组成的对象或一个包含这些对象的数组。如果是一个数组，这个函数将返回一个数组的实例。
options | Object | 可选配置
options.raw | Boolean | 可选配置，默认值：false | 如果设为true，值会忽略字段及各虚拟设置器。
options.isNewRecord | Boolean | 可选配置，默认值：true
options.include | Array | 可选配置 | 一个包含各配置项的数组 —— 用来构建预加载或内联模型实例。参见`set`

### 返回值：
[Model]()或[Model]()[]