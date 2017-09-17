> 翻译自 [http://docs.sequelizejs.com/class/lib/model.js~Model.html#static-method-hasMany](http://docs.sequelizejs.com/class/lib/model.js~Model.html#static-method-hasMany)

> public static hasMany（目标：模型，配置选项：对象）：HasMany

在这个（源）和提供的目标（模型）中创建一个一对多关系。外键被加在目标（模型）上。

### 参数：
名称 | 数据类型 | 属性 | 描述
-- | -- | -- | --
target | Model
options | object | 可选配置
options.hooks | boolean | 可选配置，默认值：false | 设为true来当一个关系模型被因由串联而删除时运行beforeDestory或afterDestroy钩子。举个例子如果`User.hasOne(Profile, {onDelete: 'cascade', hooks:true})`，profile的beforeDestory或afterDestroy钩子会在当一个user被删除时调用。反之profile将会在没有触发任何钩子（的情况下）被删除
options.as | string或object | 可选配置 | 这个模型的别名。如果你提供了一个字符串，它应该是复数的，然后将会被用node.inflection单数化。如果你想要自己控制单数版本，提供一个拥有`plural`和`singular`键的对象。同样可见传递给`sequelize.define`的`name`配置。如果你为同一个表格创建了多个关系，你应该提供一个别名才能区别它们。如果你在创建关联时提供一个别名，你需要在预加载和当你获取关联模型时提供同样的别名。默认设置成目标（模型名称的）复数形式的名称。
options.foreignKey | string或object | 可选配置 | 目标表的外键名称或一个对象代表了外键列的类型定义（语法参见`Sequelize.define`）。当使用一个对象时，你可以添加一个`name`属性来设置列名。默认为源（模型）名+源（模型）的主键名
options.sourceKey | string | 可选配置 | 域的名字用作来源表里的组合关联的键。默认设为来源表的主键
options.scope | object | 可选配置 | 一个设来用作关系创建和查找目标（模型）默认值的键值对。（sqlite不支持多对多）
options.onDelete | string | 可选配置，默认值：'SET NULL'或'CASCADE' | 如果foreignKey允许null设为SET NULL，其他情况设为CASCADE
options.onUpdate | string | 可选配置，默认值：'CASCADE'
options.constraints | boolean | 可选配置，默认值：true | 是否应该在外键上启用更新和删除约束。

### 返回值：
HasMany

### 例子：
```js
User.hasMany(Profile) // 这将添加userId到profile表
```
