#burpsuite使用 #

#### 2018/9/13 11:17:25    ####
----------


1. ##新手入门 ##
	关闭iaccess公司内网（关闭代理）  
	设置代理地址为127.0.0.1,端口8080即可
	
	*   Raw 这是视图主要显示web请求的raw格式，包含请求地址、http协议版本、主机头、浏览器信息、Accept可接受的内容类型、字符集、编码方式、cookie等。你可以通过手工修改这些信息，对服务器端进行渗透测试。  
	

	* 	params 这个视图主要显示客户端请求的参数信息、包括GET或者POST请求的参数、Cookie参数。渗透人员可以通过修改这些请求参数来完成对服务器端的渗透测试。  
	
	* 	headers 这个视图显示的信息和Raw的信息类似，只不过在这个视图中，展示得更直观、友好。
	
	* 	Hex 这个视图显示Raw的二进制内容，你可以通过hex编辑器对请求的内容进行修改。


1. ##各模块细解 ##
	[Burp Suite详细基本用法](https://blog.csdn.net/lynnlinlin/article/details/76736972 "https://blog.csdn.net/lynnlinlin/article/details/76736972")  
	内容湿哒哒大多数

1. ##Proxy SwitchySharp ##
	使用该插件实现浏览器快速代理切换




