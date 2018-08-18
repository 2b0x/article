#### 语法

	parseInt(string, radix)
- string为字符串，若不是字符串则转换为字符串
- radix是一个介于2-36之间的整数，表示字符串的基数，当未指定基数或基数为0，不同的实现会产生不同的结果，通常将值默认为10
- 如果被解析参数的第一个字符无法被转化成数字类型，则返回NaN


看几个栗子：

	parseInt("1",0)  // 以10进制转换，返回1
	parseInt("2",1)  // 基数非法，返回NaN
	parseInt("3",2)  // 以二进制转换，第一个参数非法，返回NaN
	parseInt("11",2)  // 以二进制转换，第一个参数为合法的二进制，返回3

****

#### 当parseIn遇到map
	["1", "2", "3"].map(parseInt)
猜猜会打印什么？

	[1, NaN, NaN]

该结果是由于map的回调函数而导致的

#### 来看一下map的用法
map对数组的每个元素调用定义的回调函数并返回包含结果的数组

	array.map(callback(currentValue, index, arr), thisValue)

callback：必选函数。数组中的每个元素都会执行这个函数

 - currentValue必选。当前元素的值。
 - index：可选。当前元素的索引值
 - arr：可选。当前元素属于所在的数组对象


thisValue：可选。对象作为该执行回调时使用，传递给函数，用作“this”的值。如果省略了thisValue，“this”的值为“undefined”


*回到上面的问题*

	["1", "2", "3"].map(parseInt)  
	//展开相当于：
		parseInt(1, 0, [1,2,3]);
		parseInt(2, 1, [1,2,3]);
		parseInt(3, 2, [1,2,3]);

结合上面parseInt的用法，就很容易得出为什么打印[1，NaN，NaN]了











