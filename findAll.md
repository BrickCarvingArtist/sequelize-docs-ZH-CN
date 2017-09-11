> 翻译自 [http://docs.sequelizejs.com/class/lib/model.js~Model.html#static-method-findAll](http://docs.sequelizejs.com/class/lib/model.js~Model.html#static-method-findAll)

> public static findAll(配置选项: 对象): Promise<Array\<Model>>
用来查询多个实例。

### 用AND和=来简单查询

```js
Model.findAll({
	where: {
		attr1: 42,
		attr2: 'cake'
	}
})
```

```sql
WHERE attr1 = 42 AND attr2 = 'cake'
```

### 用比...大，比...小等（来查询）

```js
Model.findAll({
	where: {
		attr1: {
			gt: 50
		},
		attr2: {
			lte: 45
		},
		attr3: {
			in: [1,2,3]
		},
		attr4: {
			ne: 5
		}
	}
})
```

```sql
WHERE attr1 > 50 AND attr2 <= 45 AND attr3 IN (1,2,3) AND attr4 != 5
```

可能的配置选项有： `$ne, $in, $not, $notIn, $gte, $gt, $lte, $lt, $like, $ilike/$iLike, $notLike, $notILike, $regexp, $notRegexp, '..'/$between, '!..'/$notBetween, '&&'/$overlap, '@>'/$contains, '<@'/$contained`

### 使用OR的查询条件

```js
Model.findAll({
  where: {
	name: 'a project',
	$or: [
	  {id: [1, 2, 3]},
	  {
		$and: [
		  {id: {gt: 10}},
		  {id: {lt: 100}}
		]
	  }
	]
  }
});
```

```sql
WHERE `Model`.`name` = 'a project' AND (`Model`.`id` IN (1, 2, 3) OR (`Model`.`id` > 10 AND `Model`.`id` < 100));
```

当查询语句执行成功时，这个promise返回一个装着模型的数组。

### 别名：all

### 参数：

**名称** | **数据类型** | **属性** | **描述**
-- | -- | -- | --
options	| Object | 可选配置 | 一系列配置选项来描述搜索的范围
options.where	| Object | 可选配置 | 一系列属性来描述你的搜索。在上面看示例。
options.attributes | Array\<String> | 可选配置 | 一系列你想要选取的属性，或者一个包含和排除某些键的对象。你可以传一个有两个元素 —— 第一个是数据库里属性的名称（或一些如`sequelize.literal`，`sequelize.fn`等的表达式），第二个是你想要这个属性在被返回的实例的名字的数组来重命名属性。
options.attributes.include | Array\<String> | 可选配置 | 选择模型里的所有属性，再加上一些额外的。对聚合很有用，例如`{ attributes: { include: [[sequelize.fn('COUNT', sequelize.col('id')), 'total']] }`
options.attributes.exclude | Array\<String> | 可选配置 | 选取模型中除了少许的一些以外的全部属性。有助于安全考虑，例如`{ attributes: { exclude: ['password'] } }`
options.paranoid | Boolean | 可选配置，默认值：true | 如果true，只会返回未被删除的纪录。如果false，删除过的和未被删除的纪录都会被返回。只会在模型的`option.paranoid`是true时启用。
options.include | Array\<Object|Model|String> | 可选配置 | 使用一个左联接预加载的关系列表。`{ include: [ Model1, Model2, ...]}`、` include: [{ model: Model1, as: 'Alias' }]}`或`{ or { include: ['Alias']}` 都是被支持的。如果你的关系是以（如`X.hasMany(Y, { as: 'Z }`）架设，你需要当预加载Y时在属性上`as`指定`Z`。
options.include[].model | Model	| 可选配置 | 你打算预加载的模型
options.include[].as | String | 可选配置 | 联系的别名，在你打算加载的模型已进行过别名的场景里。对于`hasOne`与`belongsTo`（的关系里），这个（配置）应该是单个名称，而对于`hasMany`（关系），它应该是复数形式的（即数组）
options.include[].association | Association	| 可配置的 | 你想要预加载的关系。（这能以提供model及as对子来替代）
options.include[].where | Object | 可选配置 | 在子模型上启用的where条件。注意这会把预加载转变为一个内联接，除非你明确地设置了`required:false`
options.include[].or | Boolean | 可选配置，默认值：false | 任意绑定ON和WHERE的条件会以OR组合而不是AND。
options.include[].on | Object | 可选配置 | 提供你自己的对于联接的ON条件。
options.include[].attributes | Array<String> | 可选配置 | 从子模型选取的属性列表
options.include[].required | Boolean | 可选配置 | 如果true，转换成一个内联接，这意味着父模型只会在它有匹配到任意子模型时被加载。设置了`include.where`时是true，其他情况都是false。
options.include[].separate | Boolean | 可选配置 | 如果true，单独运行一个查询来拉取被关联的实例，只支持hasMany的关系
options.include[].limit | Number | 可选配置 | 限制被联接的行数，只在include.separate等于true时才被支持
options.include[].through.where | Object | 可选配置 | belongsToMany关系在联接模型上的筛选功能
options.include[].through.attributes | Array | 可选配置 | 一个为belongsToMany关系所用的从联接模型选取属性的列表
options.include[].include | Array\<Object|Model|String> | 可选配置 | 加载更深嵌套的有关联模型
options.order | Array或fn或col或literal | 可选配置 | 指定一个排序。使用一个数组时，你能提供一些列或函数来进行排序。每个元素更能被以一个两个元素的数组包裹。第一个元素是用来排序的列或函数，第二个是顺序。举个例子：`order: [['name', 'DESC']]`。在这种情况下列名将会被拆解出来，而顺序不会。
options.limit | Number | 可选配置 |
options.offset | Number | 可选配置 |
options.transaction | Transaction	| 可选配置 | 运行查询所基于的事务
options.lock | String或Object | 可选配置 | 锁住被选中的行。可能的配置有transaction.LOCK.UPDATE和transaction.LOCK.SHARE。Postgre还支持transaction.LOCK.KEY\_SHARE，transaction.LOCK.NO\_KEY\_UPDATE和特定的与联接有关的模型锁。示例参见ransaction.LOCK
options.raw | Boolean | 可选配置 | 返回未被处理的结果。更多信息参见sequelize.query。
options.logging | Function | 可选配置，默认值：false | 一个在运行查询时被执行的方法用来打印sql。
options.benchmark | Boolean | 可选配置，默认值：false | 传出以毫秒计的查询执行耗时作为日志函数的第二个参数（options.logging）。
options.having | Object	| 可选配置 |
options.searchPath | String | 可选配置，默认值：DEFAULT | 一个用来指定模式的search_path的可选配置（仅限Postgre）
options.rejectOnEmpty | Boolean或Error | 可选配置，默认值：false | 在没有记录时抛出一个错误

### 返回值：
Promise<Array\<Model>>
