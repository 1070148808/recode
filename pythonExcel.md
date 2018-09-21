#python:Excel #

#### 2018/9/15 10:27:10    ####
----------


1. ##注意 ##
	excel文件不能实现一个文件读写同时进行，需复制第二份文件实现一个读，一个写  
	使用三个包实现写，读，读写同步：xlwt，xlrd，xlutils  

1. ## 导包 ##
    	import xlwt
    	from xlrd import *
    	from xlutils.copy import copy
    	from datetime import datetime
    	import time




1. ## 写入单个数据 ##

    	def write():
	    	rb = xlwt.Workbook()
	    	sheet = rb.add_sheet(u'sheet1',cell_overwrite_ok=True)
	    	sheet.write(1,1,"foo")#向第0行第0列写入foo
	    	rb.save(path)




1. ## 写入一列数据 ##
		def wirte02():
		    f = xlwt.Workbook()               #创建工作簿
		    sheet1 = f.add_sheet(u'sheet1',cell_overwrite_ok=True) #创建sheet
		    l_=range(5)
		    x = [42,4,14,14,14]
		    for i in l_:
		        sheet1.write(0,i,x[i])    #write的第一个,第二个参数时坐标, 第三个是要写入的数据
		        sheet1.write(1,i,x[i])
		    #sheet1.write(0,0,start_date,set_style('Times New Roman',220,True))
		    f.save("2.xlsx")#保存文件



1. ## 修改数据 ##
		def write03():
		    rb =open_workbook(path)
		    wb = copy(rb)
		    s = wb.get_sheet(0)
		    s.write(0,1,"new data")
		    wb.save("new_data.xls")
		    print ("write finished")



1. ## 设置样式 ##
		def style1():
		    font = xlwt.Font()                            # Create the font
		    font.name = 'Times New Roman'
		    font.bold = True
		    font.underline = True
		    font.italic = True
		    font.colour_index = 2
		
		    style0 = xlwt.XFStyle()
		    style0.font = font                           # Add font to Style
		
		    wb = xlwt.Workbook()
		    ws = wb.add_sheet('A Test Sheet')
		
		    style1 = xlwt.XFStyle()
		    style1.num_format_str = 'D-M-Y'
		
		    ws.write(0, 0, 'Test', style0)
		    # ws.write(2, 2, xlwt.Formula("A3+B3"))
		    ws.write(2,2,time.strftime( "%Y-%m-%d %X", time.localtime()),style1)      #写入当前时间,精确到分钟
		    wb.save('example425.xls')

1. ## 单元格处理 ##
	

	* 一、打开文件  

	`xl = xlrd.open_workbook(file)` 
	
	* 	二、获取sheet  

			print (xl.sheet_names())#获取sheet名称
			print (xl.sheets())#获取sheet对象
			print(xl.nsheets) #获取sheet总数
			print(xl.sheet_by_name(u"目录"))
			print (xl.sheet_by_index(1))
	
	* 	三、获取sheet内的汇总数据  
	
			table1 = xl.sheet_by_name(u"目录")
			print(table1.name)
			print (table1.ncols)
			print(table1.nrows)
	
	* 	四、单元格批量读取  
 	
			print(table1.row_values(0))#获取第n行的值 若是合并单元格 首行显示值 其它为空
			print(table1.row(0))#获取值及类型
			print (table1.row_types(0))
			print(table1.col_values(0,1,4))#获取列，切片
			print(table1.row_slice(1,0,2))
	
	* 	五、特定单元格读取  

		    #取值
    		print(table1.cell(1,2).value)
    		print(table1.cell_value(1,2))
    		print(table1.row(1)[2]).value
    		print(table1.col(2)[1]).value
    		#取类型
    		print(table1.cell(1,2).ctype)
    		print(table1.cell_type(1,2))
    		print(table1.row(1)[2].ctype)
	



	* 六、常用技巧（0,0）转换成A1  

		    print(xlrd.cellname(0,0))
	    	print(xlrd.cellnameabs(0,0))
	    	print(xlrd.colname(0))