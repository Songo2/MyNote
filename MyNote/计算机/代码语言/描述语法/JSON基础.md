JSON 是一种轻量级的数据交换格式，易于人阅读和编写，也易于机器解析和生成
它完全独立于语言，但使用了类似 C 家族语言的习惯(如 C、C++、Java、JavaScript 等),是当前网络传输中最主流的数据格式之一
全称是JavaScript Object Notation(JavaScript 对象表示法)

# 背景

在1999年,道格拉斯·克罗克福德(Douglas Crockford)就敏锐地发现JavaScript的对象字面量语法很适合表示数据
2000年,克罗克福德买下 json.org 域名
在2001年正式提出了“JSON”这个名字并发布了规范
他自谦为JSON的“发现者”而非“发明者”,因为这种格式本就存在于JavaScript语法.其实在1996年，Netscape公司就有人用类似方式传输数据了

# 格式

## 规则一

对象的数据(属性)要以键值对的形式保存
```json
"key":value
```
其中键必须有双引号,键值对之间以冒号分隔

## 规则二

键值对之间用逗号分隔
```json
"key1":value1,"key2":value2
```

## 规则三

对象用大括号包裹
```json
{
	"property1":value1,
	"property2":value2
}
```

## 规则四

数组用中括号也就是方括号包裹,数组中可以放JSON支持的数据
```json
["str",1,true,null]
```

## 规则五
JSON支持六种数据类型
### 数字
包括整数和浮点数

### 字符串
必须用双引号括起来

### 布尔值
都是小写,true,false

### 空值
null

### 对象
最后一个键值对后面不能有逗号

# Schema

JSON Schema是一种用 JSON 文档来描述和验证 JSON 数据结构的规范,它描述了一份合法的 JSON 数据应该长什么样,比如:必须包含哪些字段
每个字段是什么类型
字符串长度够不够、数字范围对不对
数组里应该有什么元素
哪些字段可以有、哪些必须有

一般将Schema写成一个JSON对象来使用,其中会使用到一些关键字,下面是2020-12版本的Schema关键字

## 标识、引用与核心关键字

这些关键字控制 Schema 自身的身份、复用和动态结构
### $schema
这个关键字是指明JSON所使用的版本,一般是个字符串的url
```json
"$schema":"https://json-schema.org/draft/2020-12/schema"
```

### $id
这个关键字是指明了Schema的标识符,是个字符串,一般是个url,这样方便被人根据这个url来引用这个Schema
```json
"$id": "https://example.com/address.schema.json"
```

### $anchor
这个关键字本身是锚点的意思,它可以在Schema内部起一个内部标识符,同一个Schema可以用这个标识符来引用它
```json
"$anchor": "address-def"
```

### $dynamicAnchor
动态锚点,它会让指向的Schema具有类似虚类的继承,当引用这个动态锚点时会沿着作用域层层寻找最近的同名Schema

### $ref
这个关键字搭配id和anchor使用,可以引用Schema

### $dynamicRef
这个关键字搭配dynamicAnchor使用

### $defs
定义可以复用的Schema,这是新版本的关键字,代替了旧版本的definitions,这个关键字冒号后面接的是定义的Schema对象

### $vocabulary
指明可以使用的关键字词汇表,后面接对象,但一般$schema已经包含
```json
"$vocabulary": {
  "https://json-schema.org/draft/2020-12/vocab/core": true,
  "https://json-schema.org/draft/2020-12/vocab/validation": true
}
```

### $comment
这是注释的关键字,JSON里不支持写常规注释
```json
"$comment": "这里需要严格校验，不能宽松"
```

## 通用值约束关键字

### type
这个关键字指明了可以用的数据类型
数据类型用字符串表示如"null", "boolean", "object", "array", "number", "string", "integer"
type后面可以接单个数据类型的字符串,也可以接一个数组
当接的是数组的时候,表示数据必须是其中的某一种
```json
"x": { "type": "number" }
```

### enum
作用等同于C++里的枚举,只能在选项中选一个,后面接的是一个数组,表示可以选的内容
```json
color: { "enum": ["red", "green", "blue"] }
```

### const
指定只能是后面接的值
```json
x: { "const": 42 }
```

## 数值约束关键字

这些关键字只能用于数值类型,即"number"和"integer"

### minimum
表示这个数值$\geq$给定值

### maximum
表示这个数值$\leq$给定值

### exclusiveMinimum
表示这个数值>给定值

### exclusiveMaximum
表示这个数值<给定值

### multipleOf
要求数值大于零,且可整除给定值,如果是小数的话有精度问题

## 字符串约束关键字
这些数值只能用于字符串

### minLength
表示字符串的最小长度,给定数值要求整数

### maxLength
表示字符串的最大长度,给定数值要求整数

### pattern
这个关键字的后面应该接正则表达式,要求字符串符合该正则表达式

### format
格式化的字符串标识,默认是"Format-Annotation"注释,校验器的话可以改为"Format-Assertion"断言,除此之外有
"date-time":ISO 8601
"email"RFC 5322
"hostname"
"url"
"uuid"

## 数组约束关键字
这些关键字只能用于数组

### prefixItems
这个关键字后面接的是数组
按顺序验证数组的前几个元素的类型,这个关键字代替了旧版本的items后接数组的写法
```json
{
  "prefixItems": [
    { "type": "string" },
    { "type": "number" }
  ]
}
```

### items
这个数组后面接的是单个的type对象
除去prefixItems指定的元素后所有元素,要求所有元素符合该类型,若没有prefixItems,则需要整个数组的所有元素为该类型
新版本移除了additionalItems,它的功能被加进了items,如果items:false则不允许出现prefixItems之外的剩余元素
```json
{
  "type": "array",
  "prefixItems": [{ "type": "string" }],
  "items": { "type": "integer" }
}
```

### contains
要求数组中存在这种类型的元素
```json
{ "contains": { "type": "number" } }
```

### minContains
与contains配合使用,可要求该类型元素的最少个数
```json
{ "contains": { "type": "number" }, "minContains": 2 }
```

### maxContains
与contains配合使用,可要求该类型元素的最大个数
```json
{ "contains": { "type": "number" }, "maxContains": 10 }
```

### unevaluatedItems
这个关键字是additionItems的智能升级,它会判断除Contains,prefxItems,还有items这些约束之外的元素,但是一般不和items一起,因为没有发挥的机会
当unevaluatedItems:false时不允许出现约束之外的元素

### minItems
这个关键字后面接的是正整数,规定了数组的最小长度

### maxItems
这个关键字后面接的是正整数,规定了数组的最大长度

### uniqueItems
如果为true,则数组元素不允许相同
```json
{ "uniqueItems": true }
```

## 对象约束关键字
这些关键字只能用于对象

### properties
这个关键字后面接的是对象,要求指定的对象必须含有内部的所有数据(属性),类似基类
```json
{
  "properties": {
    "name": { "type": "string" },
    "age": { "type": "integer" }
  }
}
```

### patternProperties
这个关键字和properties的差别是内部的具体属性名变成了正则表达式,满足正则表达式的属性的值必须满足规定的数据类型
```json
{
  "patternProperties": {
    "^S_": { "type": "string" },
    "^I_": { "type": "integer" }
  }
}
```

### additionalProperties
用来判断除了properties和patternProperties规定的属性,如果"additonalProperties":false,则不允许出现额外属性,但是这个是旧版本的关键字

### unevaluatedProperties
这是新版本代替additionalProperties的关键字
用来判断除了properties和patternProperties还有additionalProperties和allOf规定的属性

### required
这个关键字和properties的区别是这个关键字后接的只是属性名组成的数组,对象只需要有这些属性的声明就行

### dependentRequired
这个关键字要求如果对象存在某个属性时,需要同时存在相应的依赖属性
```json
{
  "dependentRequired": {
    "A": ["B"]
  }
}
```

### ependentSchemas
这个关键字要求如果对象存在某个属性,这个属性还要满足的schema

### minProperties
规定了最少属性个数

### maxProperties
规定了最多属性个数

### propertyNames
规定了对象所有属性的名字,一般配合"pattern"使用
```json
{ "propertyNames": { "pattern": "^[a-z_]+$" } }
```

## 组合与条件关键字
这些关键字用于组织、扩展 Schema，可应用于任何类型，但通常用于对象

### allOf
这个关键字后面接的是数组,表示需要满足的所有Schema
```json
{ "allOf": [ {"type":"string"}, {"maxLength":5} ] }
```

### anyOf
这个关键字后面接的是数组,表示需要满足其中的任一Schema
```json
{ "anyOf": [ {"type":"string"}, {"type":"number"} ] }
```

### not
这个关键字后面接的是单个Schema,表示不得满足该Schema
```json
{ "not": { "type": "string" } }
```

### if-then-else
如果满足if后面接的Schema,则还需满足then后面的Schema,否则需满足else后面的Schema

## 内容编码与媒体类型

### contentEncoding
如果JSON内容需要嵌入二进制内容如图片,文件等时,通常会编码为base64字符串,这个关键字指明了对字符串的解码方式,一般为base64

### contentMediaType
这个关键字指明了字符串内容的媒体类型和编码方式,一般配合contentEncoding使用
```json
{
  "type": "string",
  "contentEncoding": "base64",
  "contentMediaType": "image/png"
}
```

## 元数据与注释关键字
这些关键字不影响验证，仅用于提供文档、UI提示、代码生成等

|关键字|类型|说明|
|---|---|---|
|`title`|string|简短标题|
|`description`|string|详细描述|
|`default`|any|默认值，仅供文档参考|
|`deprecated`|boolean|标记该属性已弃用|
|`readOnly`|boolean|标记该字段为只读（如服务端生成）|
|`writeOnly`|boolean|标记该字段为只写（如密码）|
|`examples`|array|提供一组示例值|