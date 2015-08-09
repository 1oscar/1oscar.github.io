---
layout: post
title: "openpyxl对excel读写总结"
comments: true
share: true
tags: python excel
---

一: openpyxl读excel

```python

    from openpyxl import load_workbook
    wb = load_workbook(filename=r'***.xlsx')   #导入工作簿
    sheet_name_list = wb.get_sheet_names()    # 得到所有表格
		rows = wb.get_sheet_by_name(sheet_name_list[1]).rows  #第1个表格行列表
		col_num =1
		for col in rows[0]:       #遍历第一行的所有列
			col_num += 1
			ws_gather.cell(row=1,column=col_num).value = col.value    #将表第一行表头内容写入ws_gather，ws_gather是新建的表格
			

		i_row = 1
		for ele_sheet in sheet_name_list:  遍历所有表格
			rows = wb.get_sheet_by_name(ele_sheet).rows  # 表格所有行内容列表
			
			for row in rows[1:]:
				i_row += 1
				ws_gather.cell(row=i_row, column=1).value = str(ele_sheet)
				# ws_father是新建的excel
				i_col = 1
				for col in row:
					i_col += 1
					ws_gather.cell(row=i_row, column=i_col).value = col.value  # 写入excel单元格内容

		ew_gather.save(filename=dest_filename)  # ew_gather是新建的✉️excel
    
```

二:  openpyxl 对excel写

```python

    from openpyxl.writer.excel import ExcelWriter 
    from openpyxl.workbook import Workbook
    wb = Workbook()  #创建工作薄
	ew = ExcelWriter(workbook = wb) #写入工作薄对象
	ws1 = wb.worksheets[0]       #默认第一个表格
    ws1.title = sheet_list[0]     #默认第一个表格标题设置
    ws = wb.create_sheet()       #创建表格
    ws.title = '***'            #创建标题
    ws.cell(row=1, column=1).value = '**'    #写入单元格内容
    ew.save(filename = r'**.xlsx')      #保存excel
    
```

三: 其他excel读写
** xlrd、xlwt**

推荐文章: (openpyxl官网)[http://openpyxl.readthedocs.org/]
(未用到的特性)[https://automatetheboringstuff.com/chapter12/]