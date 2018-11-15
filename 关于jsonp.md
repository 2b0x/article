#### 什么是jsonp
一种用来解决非同源限制（即跨域问题）的方法

#### 实现原理
我们都知道script、img、iframe这几个标签都是不受非同源限制的。其中script标签可以执行js文件，那么我们就可以借以通过js文件返回我们想要的数据，进而来达到跨域的目的。实现jsonp的一个药店就是允许用户传递一个callback参数给服务端，然后服务端返回数据时将这个callback参数作为函数名来包裹住json数据

#### 实现过程
	<script>
	    var callback = function(data){};
	
	    // 提供jsonp服务的url地址（不管是什么类型的地址，最终生成的返回值都是一段javascript代码）
	    var url = "url + callback=callback";
	
	    // 创建script标签，设置其属性
	    var script = document.createElement('script');
	    script.setAttribute('src', url);
	
	    // 把script标签加入head，此时调用开始
	    document.getElementsByTagName('head')[0].appendChild(script); 

    </script>