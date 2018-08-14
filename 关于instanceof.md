#### instanceof的用法
通常来讲，使用 instanceof 就是判断一个实例是否属于某种类型，例如：

	// 判断 foo 是否是 Foo 类的实例 , 并且是否是其父类型的实例
	function Aoo(){} 
	function Foo(){} 
	Foo.prototype = new Aoo();//JavaScript 原型继承
	 
	var foo = new Foo(); 
	console.log(foo instanceof Foo)//true 
	console.log(foo instanceof Aoo)//true


#### 不得不提的原型链
![](https://i.imgur.com/bglkhT1.jpg)


#### 易混点

	Object instanceof Object  // true
	Function instanceof Function  // true
	
	Object instanceof Function  // true
	Function instanceof Object  // true

我们都知道instanceof是会沿着原型链追溯上去的，那么对于这四个判断式，结合上图就不难理解了