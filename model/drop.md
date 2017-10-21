> 翻译自 [http://docs.sequelizejs.com/class/lib/model.js~Model.html#static-method-drop](http://docs.sequelizejs.com/class/lib/model.js~Model.html#static-method-drop)

> public static drop(options：对象)：Promise

删除由这个模型所代表的表

### 参数：
名称 | 数据类型 | 属性 | 描述
-- | -- | -- | --
options | Object | 可选配置
options.cascade | Boolean | 可选配置，默认值：false | 同时删除所有基于这个表的所有对象，比如各视图。仅在postgre中生效
options.logging | Function | 可选配置，默认值：false | 一个在运行查询时被执行的方法用来打印sql。
options.benchmark | Boolean | 可选配置，默认值：false | 传出以毫秒计的查询执行耗时作为日志函数的第二个参数（options.logging）。

### 返回值：
Promise