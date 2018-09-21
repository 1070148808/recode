#python:机器学习 #

#### 2018/9/13 19:21:40    ####
----------


1. ##numpy ##


	* **基础概念**  
		NumPy
		数组的维数称为秩（rank）(维度)，可用`rank=a.ndim`获得  
		每一个线性的数组称为是一个轴（axes）（数组个数）  
		Numpy库中数组，即轴均为ndarray对象
	* **array和asarray**  
		仅仅对ndarray对象有区别，对list为参数，结果无区别
		当输入为ndarray时，array方法为新地址处理数据，asarray本地址处理，表现为：若asarray方法赋值给ndarray对象后，asarray参数对象变化了，被赋值的ndarray对象也会随之改变，如同指针引用。经测试为array创建了一个新的对象，asarray只是改变了原内存对象内容，因此，改变下述arr3的值，arr1也会变化。

    		import numpy as np
    		#example 2:
    		arr1=np.ones((3,3))
    		arr2=np.array(arr1)
    		arr3=np.asarray(arr1)
    		arr1[1]=2
    		print 'arr1:\n',arr1
    		print 'arr2:\n',arr2
			print 'arr3:\n',arr3
		输出  

    		arr1:
    		[[ 1.  1.  1.]
    		 [ 2.  2.  2.]
    		 [ 1.  1.  1.]]
    		arr2:
    		[[ 1.  1.  1.]
    		 [ 1.  1.  1.]
    		 [ 1.  1.  1.]]
    		arr3:
    		[[ 1.  1.  1.]
    		 [ 2.  2.  2.]
			 [ 1.  1.  1.]]

	* **random**  
		`numpy.random.rand(d0,d1,…,dn) `   
		rand函数根据给定维度生成[0,1)之间的数据，包含0，不包含1，dn表格每个维度，不接dn结果为一个数  
		下同  
		`numpy.random.random_sample(size=None)`  
		`numpy.random.random(size=None)`  
		`numpy.random.ranf(size=None)`  
		`numpy.random.sample(size=None)`  
		

		`numpy.random.randn(d0,d1,…,dn)`   
		同上，结果符合标准正态分布

		`numpy.random.normal(loc=0.0, scale=1.0, size=None)`  
		正态分布，loc：float，均值。scale：float，标准差（对应于分布的宽度，scale越大越矮胖，scale越小，越瘦高）

		`numpy.random.randint(low, high=None,size=None, dtype=’l’)`   
		随机整数，范围区间为[low,high），参数：low为最小值，high为最大值，size为数组维度大小，dtype为数据类型，默认的数据类型是np.int，high没有填写时，默认生成随机数的范围是[0，low)  
		eg：`np.random.randint(-5,5,size=(2,2))`
		
		`np.random.uniform(0, 100，size=None)`  
		指定范围0~100

		`numpy.random.choice(a, size=None, replace=True, p=None)`
		从给定的一维数组中生成随机数
		参数： a为**一维**数组类似数据或整数；size为数组维度；p为数组中的数据出现的概率
		a为整数时，输入的数组为np.arange(a)  
		注：np.arange(a) 数据类似range(a)
		eg：  

    		demo_list = ['lenovo', 'sansumg','moto','xiaomi', 'iphone']
    		np.random.choice(demo_list,size=(3,3), p=[0.1,0.6,0.1,0.1,0.1])

	* **切片，索引**  
		`arr1 = arr[1:3, 2:4] `   
		arr1为arr数组的【1~2】【2~3】区域数组切片，当arr数据改变时，arr1也会跟着改变，即索引

	* **变形**  
		`arr = np.ones([2,10])`  
		`arr.reshape([2,2,5]) `   
		后面接形状，但是arr数据个数必须和形状个数2*2*5一样  
		注：数据排列顺序为，从内层往外层依次排列

	* **升维**  
		`arr3_2[None,:]`  
		可在外面增加一个维度

	* **条件运算**  
		`arr1=np.where(arr < 4, 0, 10) `   
		遍历arr数组，小于4赋值为0，大于等于4赋值为10，即三目运算

		`arr > 4`  
		遍历arr数组，判断t/f，得出同arr的shape的boolean型数组

	* **轴运算**
		`np.amax(stus_score, axis=0)`  
		`np.amin(stus_score, axis=1)`  
		`np.mean(stus_score, axis=0)`  
		`np.std(stus_score, axis=0)`  
		指定轴最大值、最小值、平均值、方差    
		维度axis取值为从外往里的轴数，然后降解该维度，将重合的数据进行对应处理
		![](images\python_numpy_amin.PNG)

		`np.apply_along_axis(np.diff,0,b)`  
		在第0轴上进行差分运算，如下

    		>>> b = np.array([[1,2,3], [4,5,6], [7,8,9]])
    		>>> np.apply_along_axis(np.diff,0,b)
    		array([[3, 3, 3],
    		   [3, 3, 3]])
    		>>> np.apply_along_axis(np.diff,1,b)
    		array([[1, 1],
    		   [1, 1],
    		   [1, 1]])
    		
    		>>> b = np.array([[8,1,7], [4,3,9], [5,2,6]])
    		>>> np.apply_along_axis(sorted, 1, b)
    		array([[1, 7, 8],
    		   [3, 4, 9],
    		   [2, 5, 6]])
		轴运算使数组拥有线性方向的计算能力，方便处理行，列等等，少去遍历的时间消耗，eg：sorted排序
	* **ndarray数据运算**  
		`score[:, 0] = score[:, 0]+5 `   
		`score[2:, 0] = score[2:, 0]+5`  
		将score数据【0~n-1】【0】全部复制加5  
		将score数据【2~n-1】【0】全部复制加5  
		加减乘除均可，数组之间也可，许数组元素一一对应  

		矩阵：`result = np.dot(a, b)`  
		a，b需满足(M行, N列) * (N行, Z列) = (M行, Z列)，即a形状为（5，2），b为（2，3），可以实现矩阵运算

		矩阵拼接：`np.vstack((v1, v2))`或`np.hstack((v1, v2))`  
		垂直和水平拼接，即vstack坪街道外层，hstack拼接到内层。  
		注：对应拼接元素数量需要对应

	* **取值**  
		` np.genfromtxt("zhangshu.txt",delimiter=",")`   


1. ##学习点2 ##
	内容湿哒哒大多数


1. ##学习点3 ##
	内容湿哒哒大多数



