---
title: javascript梳理.md
date: 2019-05-07 11:37:28
tags: js
---

## javascript要点梳理
### 数据类型
javascript语言规定了7种数据类型，分别是
1. Undefined
2. Null
3. Boolean
4. String
5. Number
6. Symbol
7. Object

这些数据类型分为两种类型，`基本类型`和`引用类型`，其中除了**Object**是引用类型， 其他都是基本类型。

**String**并不是严格意义上的字符串，是字符串的UTF16编码，对字符串的所有操纵都是战队UTF16编码的，有这些特性
  * 字符串的最大长度受字符串的编码长度控制
  * BMP(基本基辅区域)的范围0-65536（U+0000 - U+FFFF）
  * 字符串一旦创建就无法被改变，所有的修改都是创建新的字符串
  * JS把字符串中每个UTF16单元当做一个字符来处理，所以当处理非BMP时，可能会产生和预期不一致的后果 

**Number**在JS中都用双精度浮点数规则表示，JS为了不让除以0出错引入了Infinity的概念，number具有这些特点
  * 根据浮点数的定义，非整数的Number运算可能存在精度问题，可能会差一个微小的值，不能用`==`和`===`直接比较，比如经典的`0.1 + 0.2 !== 0.3`问题，这里引入了一个**最小精度**的概念`Number.EPSILON`, 正确的比较方法应该使用JS提供的这个最小精度值
  `Math.abs(0.1 + 0.2 - 0.3) <= Number.EPSILON`
  * 在除法运算中要区分`0`的特殊性，大于的整数除以0的值是Infinity, 0除以0是NaN
  `A/0 -> Infinity`
  `A/-0 -> -Infinity`
  `0/0 -> NaN`

**Symbol**是ES6中新引入的类型，表示非字符串的`key`, 具有这些特性
  * 值具有唯一性, 即使描述相同`Symbol('str') !== Symbol('str')`

**Object**是JS中最复杂的类型，同时也是所有对象的原型
  * 每个对象均有自己的Class属性， 可以用`Object.protoType.toString`获取, 并用来判断对象类型
  `Object.prototype.toString.call([]) -> [object Array]`

> 基本类型`.`操作符会产生封箱和拆箱操纵 `'abc'.length -> 3`
### 类型转换
#### StringToNumber
  * 可以使用`Number`函数，不加`new`表示转换为数字，支持`二进制`, `八进制`, `十进制`, `十六进制`的值，比如`Number(0b111)`, `Number(0xFF)`, `Number(30)`, `Number(0o13)`等， 还包括科学计数法`Number(1e3)`, `Number(-1e-2)`等
  * 也可以使用`parseInt(str, ?radix)`， 在不传第二参数的时候，只支持16进制前缀`0x`, 会忽略非数字以及之后的字符，
  `parseInt('13ab12121') -> 13; parseInt('0xff') -> 255`
  * `parseFloat`直接将字符串当做十进制来解析，不支持其他进制

#### NumberToString
  * 数字较小范围时，知己转换为字符串， 当数值绝对值过大时， 会转换为`科学计数法`的字符串
  `String(65464546546487887980000) -> "6.5464546546487885e+22"`
#### Object转基本类型
  * 类型转换内部实现是通过toPrimitive(input, PreferredType)实现
#### 判断数据类型
* **typeof**可以用于判断除了null之外的基础类型，和function
* Object.prototype.toString 可以用来判断引用数据的类型， 基本类型也可以使用，只不过在使用的过程中会被转化为相应的包装对象
`Object.prototype.toString.call(false)  -> "[object Boolean]"`
`Object.prototype.toString.call(1)  -> "[object Number]"`
`Object.prototype.toString.call('a')  -> "[object String]"`
`Object.prototype.toString.call(Symbol('a'))  -> "[object Symbol]"`
`Object.prototype.toString.call([])  -> "[object Array]"`
