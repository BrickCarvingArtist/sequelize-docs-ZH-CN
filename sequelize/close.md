> 翻译自 [http://docs.sequelizejs.com/class/lib/model.js~Model.html#instance-method-close](http://docs.sequelizejs.com/class/lib/model.js~Model.html#instance-method-close)

> public close()：Promise

关闭所有由这个sequelize实例使用的连接，释放所有引用，这样实例就能被垃圾回收了。

通常这会在进程退出时完成，所以你只有在当你正在创建多个实例的时候去调用这个函数，并且想要垃圾回收它们中的部分实例。

### 返回值：
Promise