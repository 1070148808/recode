#Drallin的第2周 #
2018/9/11 10:43:38   

----------

From 导师

本周：
9月10---9月14日

* 1、	Numpy、Pandas、Matplotlib学习
* 2、	Numpy培训分享
* 3、	SQL注入测试点总结


----------

## - 周一 ##

1. ### SQL注入 ###
 理解’ 和1的测试类型，and测试注入点，or查所有数据，order by查字段数，union查版本，数据库名，用户名，所有表

1. ### win10更新系统后，docker后台运行会出现termial无法连接的问题 ###
 netcfg –d命令重置网络，任务管理器重启docker服务即可，无需重装docker

1. ### sql全函数 ###
 为sql注入学习，学习了w3school上的sql全函数教程，补充自己在sql语法上的知识空缺。

1. ### dumpfile  ###
 outfile后面不能接0x开头或者char转换以后的路径，只能是单引号路径。这个问题在php注入中更加麻烦，因为会自动将单引号转义成\',那么基本就GG了，但是load_file，后面的路径可以是单引号、0x、char转换的字符，但是路径中的斜杠是/而不是\

	语法为`select 'a\naa\raaaa' into dumpfile '/tmp/test.txt'`


----------
## - 周二 ##
1. ### 配置markdown模板 ###
	文档分类：周报，学习心得资料

1. ### 整理sql注入学习心得 ###
 	总结sql注入顺序步骤，部分sql注入绕过技巧，后门木马尝试  
	[SQL注入](SQL注入.html "详见")

1. ### 整理sql命令学习心得 ###
	github资料整合本地之
	[SQL命令（后续补充）](SQL命令学习.html "详见")


----------

## - 周三 ##
1. ### SQL注入网站 ###
	入侵到暴库，然后被封了ip，后面继续更新  
	[实战：SQL注入（后续补充）](实战：SQL注入.html "实战：SQL注入.html")

1. ### 发现sql注入到木马上传与webshell绝对路径问题 ###
	木马上传到webshell目录才可以通过web项目http访问，可新版本mysql特性增加安全文件字段，无法上传到webshell位置，解决方案未解决，拟定两个方案1：输入错误url，根据web项目浏览器报错显示绝对路径，2：查找同web项目下有没有其他测试页面有记载绝对路径；之后通过提权获得上传权限  
	[SQL注入](SQL注入.html "详见")


----------

## - 周四 ##
1. ### 尝试sqlmap使用 ###
	sqlmap入侵dvam平台，缺少cookie，学习cookie添加

1. ### 尝试burpsuite使用 ###
	对cookie等网络数据查看，找到有burpsuite，开始学习，挂代理拦截，字符处理，学习翻译后的部分文档说明  
	[burpsuite使用](burpsuite使用.html "burpsuite使用.html")

1. ### 简单记录numpy处理方法：random系列 ###
	[python机器学习](python机器学习.html "python机器学习.html")

----------

## - 周五 ##
1. ### 记录numpy处理方法：轴运算 ###
	[python机器学习](python机器学习.html "python机器学习.html")

1. ### 简单学习pandas ###

1. ### 分享会了解近期目标 ###

## - 周六 ##
1. ### 整理github上记录到本地
	安全漏洞，安全平台搭建，pythonjson，pythonexecl等文件整理
1. ### 新员工入职考试3门课程

1. ### 安全代码样本初步精简特征（周一讨论分享方案）
## - 周日 ##
