#### 看个栗子
	var a = [0];
	if ([0]) {
	  console.log(a == true);
	} else {
	  console.log("wut");
	}
先猜下会打印什么出来，“wut”？结果是false

因为在if语句中，会先把括号内的内容强制转换为Boolean

转为false的数据|转为true的数据
:--:|:--:
false|true
''|'string'
null|[]
undefined|{}
NaN|123

也就是说会进入语句 console.log(a == true)，且最后将输出false

注意：在进行‘==’比较时，不同类型的数据进行比较时也会有隐形转化。如如果其他类型和数字比较时，会尝试把这个类型转成数字再进行宽松比较，而对象（数组也是对象）会先调用它的toString()方法，此时[0]会变成‘0’，然后将字符串‘0’转成数字0，而0 == true的结果显然是false