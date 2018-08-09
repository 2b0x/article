#### 关于数组的push方法
push 方法具有通用性。该方法和call()、apply()一起使用时，可应用在类似数组的对象上。通常来讲，push会在数组最尾端加入数据，即入队和进栈。

#### 一点小疑问
但push真的只能在数组尾端添加数据嘛？来看一个案例先

	var obj = {
	  "2": "a",
	  "3": "b",
	  "length": 2,
	  "push": Array.prototype.push
	}
	obj.push("c");
	obj.push("d");

两次push之后，obj 会的值会是什么呢？先思考一下，答案马上揭晓

	var obj = {
	  "2": "c",
	  "3": "d",
	  "length": 4,
	  "push": Array.prototype.push
	}

Anything was so amazing ！！！

#### push的实现原理
push方法根据length属性来决定从哪里开始插入给定的值。如果length不能被转换成一个数值，则插入的元素索引为0。但当length不存在的时，将会创建它。

唯一的原生类数组（array-like）对象是 Strings，尽管如此，它们并不适用该方法，因为字符串是不可改变的。

所以说，push会根据对象length属性的值去确定插入的位置，转化成代码就是：

	Array.prototype.push = function (target) {
	    obj[obj.length] = target;
	    obj["length"]++;
	}



[MDN关于Array.push的解释](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/push)

