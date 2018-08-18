#### 先看个例子

	var min = Math.min(), max = Math.max()
	console.log(min < max);  // false

##### 关于 min 和 max
Math.min()：	返回参数中最小的值。如果没有参数，则返回 Infinity。如果有某个参数为 NaN，或是不能转换成数字的非数字值，则返回 NaN。

Math.max()：	返回参数中最大的值。如果没有参数，则返回 -Infinity。如果有某个参数为 NaN，或是不能转换成数字的非数字值，则返回 NaN。