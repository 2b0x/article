#### 先看个例子

	var min = Math.min(), max = Math.max()
	console.log(min < max);  // false

##### 关于 min 和 max的返回值
Math.min()：	返回参数中最小的值。如果没有参数，则返回 Infinity。如果有某个参数为 NaN，或是不能转换成数字的非数字值，则返回 NaN。

Math.max()：	返回参数中最大的值。如果没有参数，则返回 -Infinity。如果有某个参数为 NaN，或是不能转换成数字的非数字值，则返回 NaN。


##### 关于min和max的参数问题
参与min和max方法统计的参数需要一一传入函数中，即为：

	Math.min(1,3,5,7,9)  //1
	Math.max(2,4,6,8,10)  //10

可能会有同学会说，如果我想比较一个数组内的数，还要把数组遍历一遍岂不是多此一举了？如果是直接遍历数组确实有点多此一举了，不过我们有其他办法~

就是利用apply函数

	function getMinByArry(arry){
		Math.min.apply(null, arry)
	}
	
	function getMaxByArry(arry){
		Math.max.apply(null, arry)
	}
	
如果你已经用上了ES6，那么就更好啦，直接用ES6的解构赋值即可

	Math.min(...arry)
	Math.max(...arry)
