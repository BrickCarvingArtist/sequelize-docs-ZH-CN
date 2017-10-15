> 翻译自 [http://docs.sequelizejs.com/class/lib/sequelize.js~Sequelize.html#instance-method-fn](http://docs.sequelizejs.com/class/lib/sequelize.js~Sequelize.html#instance-method-fn)

> public static fn(fn：字符串, args：任意)：[fn](https://github.com/BrickCarvingArtist/sequelize-docs-ZH-CN/blob/master/sequelize/fn.md)自v2.0.0-dev3起

创建一个代表数据库函数的对象。它能用在各查询语句，where和排序，以及在各列定义中作为默认值。如果你想要在你的函数中引用列，你需要使用`sequelize.col`，这样各列被合适得理解成列而不是字符串。  

转换一个用户的用户名到大写形式

```js
instance.updateAttributes({
  username: self.sequelize.fn('upper', self.sequelize.col('username'))
})
```

### 参数：
名称 | 数据类型 | 属性 | 描述
-- | -- | -- | --
fn | String | 你想要调用的函数
args | any | 更多的参数将会以arguments的形式传给函数

### 返回值：
[fn](https://github.com/BrickCarvingArtist/sequelize-docs-ZH-CN/blob/master/sequelize/fn.md)

### 例如：
转换一个用户的用户名到大写形式

```js
instance.updateAttributes({
  username: self.sequelize.fn('upper', self.sequelize.col('username'))
})
```

### 参见：
[Model.findAll](https://github.com/BrickCarvingArtist/sequelize-docs-ZH-CN/blob/master/model/fillAll.md)

[Sequelize.define](https://github.com/BrickCarvingArtist/sequelize-docs-ZH-CN/blob/master/sequelize/define.md)

[Sequelize.col](https://github.com/BrickCarvingArtist/sequelize-docs-ZH-CN/blob/master/sequelize/col.md)