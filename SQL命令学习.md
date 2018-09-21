#SQL注入 #

#### 2018/9/11 17:13:58    ####
----------


1. ## SQL 通配符 ##
	
	与like联合使用  
	% | 替代一个或多个字符  
	_ | 仅替代一个字符  
	[charlist] | 字符列中的任何单一字符  
	[^charlist]或者[!charlist] | 不在字符列中的任何单一字符   

	如：
	希望 "Persons" 表中选取居住的城市以 "A" 或 "L" 或 "N" 开头的人：  
	以使用下面的 SELECT 语句：  

    	SELECT * FROM Persons  
    	WHERE City LIKE '[ALN]%'  



1. ## WHERE IN ##
	匹配多个  

    	SELECT * FROM Persons  
    	WHERE LastName IN ('Adams','Carter')  
	查找LastName =Adams和LastName =Carter的人


1. ## WHERE BETWEEN ##
	匹配范围  

    	SELECT * FROM Persons  
    	WHERE LastName  
    	NOT BETWEEN 'Adams' AND 'Carter'  
	若不在范围内，使用not


1. ## SELECT INTO ##
	IN 子句可用于向另一个数据库中拷贝表：

    	SELECT *
    	INTO Persons IN 'Backup.mdb'
    	FROM Persons
	其他同select语句
	即在后面加into


1. ## 约束，修改表 ##
	`ALTER TABLE Persons`

	增加约束
	`ADD UNIQUE (Id_P)`

	增加多个约束，并命名
	`ADD CONSTRAINT uc_PersonID UNIQUE (Id_P,LastName)`

	撤销约束
	`DROP uc_PersonID Id_P`

	命名外键，关联persons表主键
	`CONSTRAINT fk_PerOrders FOREIGN KEY (Id_P) REFERENCES Persons(Id_P)`
	
	check约定范围
	`CHECK (Id_P>0 AND City='Sandnes')`
	
	主键自增
	`P_Id int NOT NULL AUTO_INCREMENT,`


1. ## 日期 ##
	DATE - 格式 YYYY-MM-DD  
	DATETIME - 格式: YYYY-MM-DD HH:MM:SS  
	TIMESTAMP - 格式: YYYY-MM-DD HH:MM:SS  
	YEAR - 格式 YYYY 或 YY


1. ## GROUP BY,HAVING ##
    	SELECT Customer,SUM(OrderPrice) FROM Orders
    	WHERE Customer='Bush' OR Customer='Adams'
    	GROUP BY Customer
    	HAVING SUM(OrderPrice)>1500
	sum（）函数只能用having条件处理
	group by按照后面字段分组
	
	上述代码实现  
	按照Customer查询OrderPrice总数，且总数大于1500的，Customer为bush和adams的  
	Customer SUM(OrderPrice)  
	数据集


1. ## MID（） ##
	SELECT MID(City,1,3) as SmallCity FROM Persons  
	查找city字段全部数据，输出city字段数据的前三个字符  
	city-->字段  
	1---->起始位置  
	3---->截取字符个数


1. ## ROUND() ##
	SELECT ProductName, ROUND(UnitPrice,0) as UnitPrice FROM Products  
	UnitPrice字段输出0位小数（即只显示整数部分）
