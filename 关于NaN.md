#### NaN是什么？
NaN是一个全局对象的属性

<<<<<<< HEAD
=======

>>>>>>> 6300cbe75944aa1fef5ecd29807fb41cbae1bb00
#### typeof的结果是？
    typeof NaN； //number

#### 如何判断一个变量的值是否为NaN？
在最早的js版本中，有isNaN()函数。但是它传入的参数如果为非数值类型时，其结果很让人费解

    isNaN(undefined)  //true
    isNaN({})  //true
    isNaN('asfd')  //true
    isNaN(NaN)  //true
    isNaN(123)  //false
这结果有点让人 “匪夷所思” 究其因，原来是在判断参数类型时，isNaN()函数会先对参数进行Number()转换，对于非Number型的参数，通过转换后肯定都是NaN，所以输出的结果都是true。

那要怎么判断NaN呢？【来自《深入理解JavaScript》】

前面已经提到，isNaN()函数在判断前会进行Number()转换，所以我们先判断变量类型是否为Number类型

    function myIsNam(value){
    	return typeof value === 'number' && isNaN(value);
    }
或者

    function myIsNaN(value){
    	return value !== value;
    }
第二个办法是借助了NaN的特性，它是唯一一个值和自己本身不相等的
***
##### 值得一提的是
在ES6中，已经针对NaN的怪异行为做出了调整。专门为Number类型添加了isNaN()方法来判断是不是NaN

    Number.isNaN('word')  //false
    Number.isNaN(undefined)  //false
    Number.isNaN({})  //false
    Number.isNaN(NaN)  //true
一切恢复往常的平静与安宁。  END。
