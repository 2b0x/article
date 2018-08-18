#### 先来看个例子

	var lowerCaseOnly = /^[a-z]+$/;
	[ lowerCaseOnly.test(null), lowerCaseOnly.test() ]

打印结果为：[ true, true ]


##### 解析：
test 方法的参数会被调用 toString 强制转换成字符串，此题转换的字符串是null、undefined。故匹配结果均为 true