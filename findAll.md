> 翻译自 [http://docs.sequelizejs.com/class/lib/model.js~Model.html#static-method-findAll](http://docs.sequelizejs.com/class/lib/model.js~Model.html#static-method-findAll)

> public static findAll(配置选项: 对象): Promise<Array<Model>>
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
options	| Object | 可选配置 | 一系列配置选项来表述搜索的范围
options.rejectOnEmpty | Boolean或Error | 可选配置，默认值：false | 在没有记录时抛出一个错误

### 返回值：
Promise<Array<Model>>
