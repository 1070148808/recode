#Drallin的第3周 #
2018/9/17 15:52:05   

----------

## - 周日 ##
1. ### 参加hackathon比赛 ###
	* 连续三年参加，第一次没拿奖空手而回，发现技术工具越来越趋向大众所需求，精简快捷，市场专一化，不要普遍性
	* 同时了解到我们消费者bg拥有自己的小程序平台，简单快捷的实现功能
	* 和2012同事聊了聊自动化检测漏洞问题，觉得需要更多地了解公司已有的产品工具，通过外部调用，构建适应本部门的漏洞检测工具，减少部门的手工检测调试问题

----------

## - 周一 ##

1. ### 完成全部入职考试 ###

1. ### 阅读mango源码 ###

----------
## - 周二 ##

1. ### win10下ipython+jupyter配置 ###
	[python环境配置](python环境配置.html "python环境配置.html")


1. ### pychram ###
	了解到pychram中安装的所有模块均属于该项目，即每个项目有着自己的单独的工作环境，为了防止环境污染，py模块均在自己的项目包中，即安装的模块在别的项目中无法使用，若希望方便其他项目的环境部署，省去每次新项目都要配置环境，可以再setting中interpreter解释器中选择其他项目的解释器，或者选择本地安装包的解释器，然后在本地python安装包中安装所有的py模块


1. ### 参加南研AT DeepDive活动 ###
	了解到如何尽快提高自身的团队价值，不宜过急，把事情做好做精，趁这个时期多学习，多思考，给团队多一些新颖的建议

1. ### mobaxterm ###
	mobaxterm自带cygwin，可通过apt-cyg安装软件  
	设置中persistent root folder选项确定虚拟unix平台的2位置
### from 导师 ###
	
* 了解公司agent检测漏洞工具原理
* 通过hook出执行语句和agent拦截的语句对比差别，确定什么样的漏洞可以拦截
* 了解百度openrasp检测原理
* 对比两者，研发我们自己的产品工具

----------

## - 周三 ##

1. ### injectionKillerh和secRASP工具学习 ###
	injectionKiller系列，Instrumentation，jrs，探针打孔，责任链模式等  
	[漏洞检测工具.html](漏洞检测工具.html "漏洞检测工具.html")

1. ### 百度openrasp工具初步了解 ###

----------


## - 周四 ##
1. ### IAST-DAST-SAST-RASP区别 ###
	见下面IAST-DAST-SAST-RASP区别一章节
	[漏洞检测工具.html](漏洞检测工具.html "漏洞检测工具.html")  

1. ### IAST+RASP设计 ###
	[漏洞检测工具.html](漏洞检测工具.html "漏洞检测工具.html")


1. ### 公司工具injectionKiller和secRASP区别和整合准备 ###
	均为修改字节码操作，前者通过修改sql参数查看注入，后者通过sql语句判断是否继续请求；获得后者源码，前者就有jar包，初步认为可以把两者合为一个工具，前者检差完继续通过后者，对两者结果进行合并处理

----------

## - 周五 ##

1. ### 10.21.158.141 (root)服务器部署周报服务 ###
	jdk8.181+tomcat7+drallin_recode。（注8081端口）  
	公司GNU服务器root账户执行startup.sh出现wrong，需通过catalina.sh执行tomcat

1. ### 解析killer工具 ###
	
	
	* 部署killer插件需：1。tomcat+killer插件。2。待测web项目。  
		
	
	* 根据killer启动与catalina.bat文件，有必要解剖tomcat，以致跟踪killer运行  
		
	
	* [tomcat中catalina代码详解](https://www.cnblogs.com/fantiantian/p/3620022.html "https://www.cnblogs.com/fantiantian/p/3620022.html")  
	* JD-eclipse直接反编译killer源码  
	
	* 部署云巡航前台，后台 在本地，跑起来！  

**问题**  

	killer后台无法访问
**计划** 

	

* 本地通过跑起来killer插件检测测试云巡航

	

* secrasp的本地运行

	

* killer+secrasp整合
## - 周六 ##


## - 周日 ##
