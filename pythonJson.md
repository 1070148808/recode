#python:Json #

#### 2018/9/15 10:20:21      ####
----------


1. ##json r/w中文乱码： ##


	* **统一编译器utf8编码，或者脚本前置**  
		`#-*-coding:utf-8-*-`
	* **从文件读取json数据**  
		（str+replace+decode处理，可在最后输出时添加，方便前期数据处理，字符前的u标识不影响数据操作）  
		`import json f = file('j1.json')`读取文件  
		`jsondata = json.load(f)`加载  
		`dataforemployees=jsondata['employees']`取出对应键值，此处为employees  
		`stringdata=str(dataforemployees).replace('u\'','\'')`字符化，去除unicode的u字符标识  
		`strdecode=stringdata.decode("unicode-escape")`输出  
		即`.replace('u\'','\'').decode("unicode-escape")`  

		此处注意转换时的类型，如下显示  

		    print type(jsondata)  
    		print type(dataforemployees)  
    		print type(stringdata)  
    		print type(strdecode)  
		结果为  

		    <type 'dict'>
    		<type 'list'>
    		<type 'str'>
    		<type 'unicode'>
		测试json数据为  
		
		    {
    			"employees": [{
    					"firstName": "Bill",
    					"lastName": "Gates"
    				},
    				{
    					"firstName": "George",
    					"lastName": "Bush"
    				},
    				{
    					"firstName": "Thomas",
    					"lastName": "Carter"
    				}
    			]
    		}
		附录：4个格式的输出情况
		
		    print jsondata
    		print dataforemployees
    		print stringdata
    		print strdecode
		如下
		
		    {u'employees': [{u'lastName': u'Gates', u'firstName': u'Bill'}, {u'lastName': u'Bush', u'firstName': u'George'}, {u'lastName': u'Carter', u'firstName': u'Thomas'}]}
    		[{u'lastName': u'Gates', u'firstName': u'Bill'}, {u'lastName': u'Bush', u'firstName': u'George'}, {u'lastName': u'Carter', u'firstName': u'Thomas'}]
    		[{'lastName': 'Gates', 'firstName': 'Bill'}, {'lastName': 'Bush', 'firstName': 'George'}, {'lastName': 'Carter', 'firstName': 'Thomas'}]
    		[{'lastName': 'Gates', 'firstName': 'Bill'}, {'lastName': 'Bush', 'firstName': 'George'}, {'lastName': 'Carter', 'firstName': 'Thomas'}]


1. ##json 处理（接上，已经过中文读入，字符处理）： ##


	1：希望读取数组（list）中数据  
	
		for t in dataforemployees:
		print t['firstName']
	结果为
	
		Bill
		George
		Thomas




1. ## json网络请求数据 

		import requests
		r = requests.get('http://10.186.241.135:8080/statistics/cbsCheckerDefectInfo')
		print r.content


1. ## json解析 ##

	    json.dumps json-to-str
		json.loads str-to-dictionary
[详解dump和load](https://blog.csdn.net/dyx404514/article/details/50186413 "https://blog.csdn.net/dyx404514/article/details/50186413")




