### 关于Ajax
##### 工作原理
- ajax的技术核心：XMLHttpRequest对象
- ajax请求过程：创建XMLHttpRequest对象、连接服务器、发送请求、服务器做出响应、接收响应数据

##### 实现一个原生Ajax的五个步骤
1. 创建 XMLHttpRequest 对象
2. 使用open方法设置和服务器的交互信息
3. 设置发送的数据，开始和服务器端交互
4. 注册事件
5. 更新界面


##### get方法实现
	function ajax(url,fnSuccess,fnFaild){
	  　　//1.创建Ajax对象
	  　　//js中,使用一个没有定义的变量会报错,使用一个没有定义的属性,是undefined
	  　　//IE6下使用没有定义的XMLHttpRequest会报错,所以当做window的一个属性使用
	  　　if (window.XMLHttpRequest) {
	    　　//非IE6
	    　　var oAjax=new XMLHttpRequest();
	  　　}else{
	    　　//IE6
	    　　var oAjax=new ActiveXObject("Microsoft.XMLHTTP");
	  　　}
	
	  　　//2.连接到服务器
	  　　oAjax.open('GET',url,true);
	
	  　　//3.发送请求
	  　　oAjax.send();
		
	  　　//4.接收返回值
	  　　oAjax.onreadystatechange=function(){
	    　　//oAjax.readyState--浏览器和服务器之间进行到哪一步了
	    　 if(oAjax.readyState==4){  //读取完成
	      　　if(oAjax.status==200){  //读取的结果是成功
	        　　　　fnSuccess(oAjax.responseText); //成功时执行的函数
	      　　  }else{
	        　　   if(fnFaild){   //判断是否传入失败是的函数,即用户是否关心失败时的结果
	          　　　　 fnFaild(oAjax.responseText);  //对失败的原因做出处理
	        　　   }
	      　　  }
	    　　 }
	  　　}
	　 }

##### post方法实现
	function ajaxPost(url,id,fnSuccess,fnFaild){
	  　　//1.创建Ajax对象
	 　　 if (window.XMLHttpRequest) {
	    　　//非IE6
	    　　var xhr=new XMLHttpRequest();
	  　　}else{
	    　　//IE6
	   　　 var xhr=new ActiveXObject("Microsoft.XMLHTTP");
	 　　 }

	  　　//2.连接到服务器
	  　　xhr.open("POST",url,true);
	  　　//设置头信息
	  　　xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
	  　　var form=document.getElementById(id);

	  　　//3.发送请求，传递数据
	  　　xhr.send(serialize(form));

	  　　//4.接收返回值
	  　　xhr.onreadystatechange=function(){
	    　　if(xhr.readyState==4){
	      　　if ((xhr.status>=200 && xhr.status<300) || xhr.status==304) {
	        　　fnSuccess(xhr.responseText);
	     　　 }else{
	        　　fnFaild(xhr.responseText);
	      　　}
	    　　}
	  　　};
	　　}


#### 各个步骤解读
1.open(method, url, async)

- method：发送请求所使用的方法（一般为post和get）
- url：发送请求的目标地址(该文件可以是任何类型的文件，比如 .txt 和 .xml，或者服务器脚本文件，比如 .asp 和 .php （在传回响应之前，能够在服务器上执行任务）)
- async：规定对请求进行异步(true)还是同步(false)处理；true是在等待服务器响应时执行其他脚本，当响应就绪后对响应进行处理；false是等待服务器响应再继续执行。

2.send()方法可以将请求送往服务器

3.onreadystatechange：存有处理服务器响应的函数，每当readyState改变时，onreadystaychange函数就会被执行。

4.readyState：存有服务器响应的状态信息

- 0：请求未初始化（代理被创建，但尚未调用open()方法）
- 1：服务器连接已建立（open()方法已经被调用）
- 2：请求已接收（send()方法已经被调用，并且头部和状态已经可获取）
- 3：请求处理中（下载中，responseText属性已经包含部分数据）
- 4：请求已完成，且响应已就绪（下载操作已完成）

5.responseText：获取字符串形式的响应数据

6.setRequestHeader()：POST传递数据时，用来添加HTTP头，然后send(data)，注意data格式；GET发送信息时直接加参数到url就可以了


#### Ajax优缺点
###### 优点：
- 无刷新即可更新数据
- 异步服务器通信
- 前端和后端负载平均
- 界面与应用分离

###### 缺点：
- ajax使得back和history丧失，即破坏了浏览器机制
- ajax存在安全问题，无意间将后端目标地址暴露了
- 对搜索引擎支持比较弱
- 破坏程序的异常处理机制
- 违背了URL和资源定位的初衷
- ajax对移动设备的支持不是很好

