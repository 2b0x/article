#### 解析并提取url参数
这个函数实现比较简单，所以直接上代码：

	function getUrlData(url){
		var obj = {};
		var urls = url;
		var str = urls.slice(1).split('&');
		
		for(var i=0; i<str.length;++i){
			var item = str[i].split('=');
			obj[item[0]] = item[1];
		}
	
		return obj
	}