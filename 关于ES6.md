#### 函数默认值
	// Before
	function decimal(num, fix) {
	    fix = fix === void(0) ? 2 : fix;
	
	    return +num.toFixed(fix);
	}

	// After
	function decimal(num, fix = 2) {
	    return +num.toFixed(fix);
	}

- 注意点：设定了默认值的入参，应该放在没有设置默认值的参数之后，也就是我们不应该这样写：function decimal(fix = 2, num){}，虽然通过变通手段也可以正常运行，但不符合规范。


#### 模版字符串
	// Before
	var type = 'simple';
	'This is a ' + type + ' string join.'

	// After
	var type = 'singleline';
	`This is a ${type} string.`


#### let & const
>**let**

- 无变量提升
- 有块级作用域
- 禁止重复声明

>**const**

- 禁止重复赋值

		const DEV = true;
		DEV = false; // => TypeError
		基于静态常量的定义我们可以很明显知道，const 声明的常量一经声明便不能再更改其值。
- 必须赋初始值

		const DEV; // => SyntaxError
		也是基于定义，const 声明的常量既然一经声明便不能再更改其值，那声明的时候没有附初始值显然是不合理的，一个没有任何值的常量是没有意义的，浪费内存。

#### 新增库函数
>**Number**

	Number.isInteger(Infinity); //用来判断一个数是否为整数，返回布尔值
	Number.isNaN('NaN'); //用来判断入参是否为 NaN

>**String**

	'abcde'.includes('cd'); // => true
	'abc'.repeat(3);        // => 'abcabcabc'
	'abc'.startsWith('a');  // => true
	'abc'.endsWith('c');    // => true
- inclueds() 方法用来判断一个字符串中是否存在指定字符串
- repeat() 方法用来重复一个字符串生成一个新的字符串
- startsWith() 方法用来判断一个字符串是否以指定字符串开头，可以传入一个整数作为第二个参数，用来设置查找的起点，默认为 0，即从字符串第一位开始查找
- endsWith() 与 startsWith() 方法相反

>**Math**

	Math.trunc(4.1) // => 4
	Math.trunc(-4.1) // => -4
	解决floor()向下取整时的不足 Math.floor(-4.1); // => -5


#### 箭头函数（重要新特性）
>**共享父级this对象**

	// Before
	var obj = {
	    arr: [1, 2, 3, 4, 5, 6],
	    getMaxPow2: function() {
	        var that = this,
	            getMax = function() {
	                return Math.max.apply({}, that.arr);
	            };
	        
	        return Math.pow(getMax(), 2);
	    }
	}
	// After
	var obj = {
	    arr: [1, 2, 3, 4, 5, 6],
	    getMaxPow2: function() {
	        var getMax = () => {
	            return Math.max.apply({}, this.arr);
	        }
	
	        return Math.pow(getMax(), 2);
	    }
	}
在箭头函数中，函数体内部没有自己的 this，默认在其内部调用 this 的时候，会自动查找其父级上下文的 this 对象（如果父级同样是箭头函数，则会按照作用域链继续向上查找），这无疑方便了许多，我们无需在多余地声明一个临时变量来做这件事了。

**注意：**

1. 某些情况下我们可能需要函数有自己的 this，例如 DOM 事件绑定时事件回调函数中，我们往往需要使用 this 来操作当前的 DOM，这时候就需要使用传统匿名函数而非箭头函数。
2. 在严格模式下，如果箭头函数的上层函数均为箭头函数，那么 this 对象将不可用。
3. 由于箭头函数没有自己的 this 对象，所以箭头函数不能当做构造函数。

>**共享父级arguments**

	function getSum() {
	    var example = () => {
	        return Array
	            .prototype
	            .reduce
	            .call(arguments, (pre, cur) => pre + cur);
	    }
	
	    return example();
	}
	getSum(1, 2, 3); // => 6
由于箭头函数本身没有 arguments 对象，所以如果他的上层函数都是箭头函数的话，那么 arguments 对象将不可用。


>**不能当做构造函数**

由于箭头函数没有自己的 this 对象，所以箭头函数不能当做构造函数


#### 类和继承


#### 模块化
内联导出：

	export const DEV = true;
	export function example() {
	    //...
	}
	export class expClass {
	    //...
	}
	export let obj = {
	    DEV,
	    example,
	    expClass,
	    //...
	}
	使用 export 关键字，后面紧跟声明关键字（let、function 等）声明一个导出对象，这种声明并同时导出的导出方式称作内联导出。
	未被导出的内容（变量、函数、类等）由于独立代码块的原因，将仅供模块内部使用（可类比成一种闭包）。

对象导出：

	const DEV = true;
	function example() {
	    //...
	}
	class expClass {
	    //...
	}
	let obj = {
	    DEV,
	    example,
	    expClass,
	    //...
	}
	// module example.js
	export {DEV, example, expClass, obj};
	export {DEV, example as exp, expClass, obj};
	我们可以像写普通 JS 文件一样写主要的功能逻辑，最后通过 export 集中导出。
	在导出时我们可以使用 as 关键字改变导出对象的名称。
默认导出：

	export default {DEV, example as exp, expClass, obj};
	// OR
	export default obj;
	// OR
	export default const DEV = true;
	我们可以在 export 关键字后接 default 来设置模块的默认导出对象，需要注意的是：一个模块只能有一个默认导出。

导入模块：

	import example from './example.js';
	// OR 
	import default as example from './example.js';
	import {DEV, example} from './example.js';
	import * as exp from './example.js';
	import {default as expMod, * as expAll, DEV, example as exp} from './example.js';
	使用 import 关键字导入一个模块，上边这两种写法是等效的。默认导入对象既是模块默认导出对象，即对应模块定义中的 export default 所导出的内容。