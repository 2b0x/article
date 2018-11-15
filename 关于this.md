##### this的指向
this的指向在函数定义的时候是确定不了的，只有函数执行的时候才能确定this到底指向谁，实际上this的最终指向的是那个调用它的对象


    var myObject = {
     	foo: "bar",
    	func: function() {
        	var self = this;
        	console.log("outer func:  this.foo = " + this.foo);
        	console.log("outer func:  self.foo = " + self.foo);
        	(function() {
            	console.log("inner func:  this.foo = " + this.foo);
            	console.log("inner func:  self.foo = " + self.foo);
        	}());
    	}
    };
    myObject.func();


