#### 各类型typeof的值

类型|结果
---|:--:
Undefined|"undefined"
Null|"null"
Boolean|"boolean"
Number|"number"
String|"string"
Symbol|"symbol"
函数对象|"function"
任何其他对象|"object"


#### 值得注意的是
	typeof null === 'object'
在 JavaScript 最初的实现中，JavaScript 中的值是由一个表示类型的标签和实际数据值表示的。对象的类型标签是0。因为 null 代表的是空指针(大多数平台下值为0x00)，因而，null的类型标签也成为了0，typeof null就错误的返回了"object".