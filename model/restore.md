> 翻译自 [http://docs.sequelizejs.com/class/lib/model.js~Model.html#static-method-restore](http://docs.sequelizejs.com/class/lib/model.js~Model.html#static-method-restore)

> public static restore(配置选项：Object)：Promise\<undefined>

当启用`paranoid`时恢复多个实例。

### 参数：

名称 | 数据类别 | 属性 | 描述
—- | -- | -- | --
options | Object
options.where | Object | 可选配置 | 筛选恢复（的条件）
options.hooks | Boolean | 可选配置，默认值：true | 是否运行`beforeBulkRestore`或`afterBulkRestore`钩子？
options.individualHooks | Boolean | 可选配置，默认值，false | 如果设为true，恢复将会基于where参数查找并将在每行执行`beforeBulkRestore`或`afterBulkRestore`钩子
options.limit | Number | 可选配置 | 反删除多少行（只针对mysql）
options.logging | Function | 可选配置，默认值：false | 一个在运行查询时被执行的方法用来打印sql。
options.benchmark | Boolean | 可选配置，默认值：false | 传出以毫秒计的查询执行耗时作为日志函数的第二个参数（options.logging）。
options.transaction | [Transaction]() | 可选配置 | 运行查询所基于的事务

### 返回值：

Promise\<undefined>