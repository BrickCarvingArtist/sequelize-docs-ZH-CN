> 翻译自 [http://docs.sequelizejs.com/class/lib/model.js~Model.html#static-method-getTableName](http://docs.sequelizejs.com/class/lib/model.js~Model.html#static-method-getTableName)

> public static getTableName()：String或Object

获取模型的表名，将schema带入账户。当模型没有schema时，这个方法将以字符串形式返回它的名称，反之返回一个含有表名，schema及各分隔符属性的对象。

### 返回值：
String或Object