---
title: Python操作Excel
date: 2021-05-29 16:03:09
# 文章出处名称 #
from: 原创
# 文章出处链接 #
url:
# 文章作者名称 #
author: p0ny
# 文章作者签名 #
about: 一穷二白
# 文章作者头像 #
avatar: 
# 是否开启评论 #
comments: true
# 文章标签 #
tags: Python
# 文章分类 #
categories: Python
# 文章摘要 #
description: Python操作Excel
# 文章置顶 #
sticky: 1
---
# Python 操作 Excel
### 准备工作
- 安装 `openpyxl` 库 `pip install openpyxl -i https://pypi.douban.com/simple --trusted pypi.douban.com`

### 调用案例【需要从上到下按顺序操作】

##### 1. 选中单元格并进行读写单元格内容【加载已有excel文档或者新建excel文档，操作sheet表，操作单元格】
  ```python
    # 读取json
    import json
    from openpyxl import load_workbook, workbook

    # 打开现有的 Excel 文件  =============  操作已经存在的 excel文件
    wb = load_workbook("1.xlsx")
    #  ===============================================================


    # ===================================== 新建一个文件然后再操作
    # 创建 Excel 且默认创建一个Sheet ==============
    wb = workbook.Workbook()
    # ===================


    print(wb.sheetnames)  # ['android', 'IOS', 'Steam', '敏感的第三方组件']

    #   =============================================
    # 要操作 哪个sheet就选择哪个sheet

    # 选择 名称为 android 的sheet  的方式一：
    sheet = wb['android']  # 然后可以使用 sheet 变量操作sheet里面的单元格

    # 基于索引位置来 选择某个sheet  的方式二：
    sheet = wb.worksheets[0]  # 选择 名称为 android 的sheet
    # 将第一个 Sheet对象赋给 变量 sheet
    #   =======================================


    #  ******************************************
    #  ******************************************
    #  ******************************************

    # 选择某个单元格方式一：
    cell = sheet.cell(6, 2)  # 这两个参数分别是 row, column 都是int 类型的数据，传进去的是单元格的行数和列数
    """
    def cell(self, row, column, value=None):

        Returns a cell object based on the given coordinates.

        Usage: cell(row=15, column=1, value=5)

        Calling `cell` creates cells in memory when they
        are first accessed.

        :param row: row index of the cell (e.g. 4)
        :type row: int

        :param column: column index of the cell (e.g. 3)
        :type column: int
        """

    # 选择某个单元格方式二：
    cell = sheet['A1']  # cell = <Cell 'android'.A1>

    # print(cell.value)  # 输出该单元格上的文本信息
    # print(cell.style)  # 输出该单元格上的样式
    # print(cell.font)  # 输出该单元格上的字体
    # print(cell.alignment)  # 输出该单元格上的排列情况：水平居中还是其他等等
    # 读取 名称为 android 的sheet，再读取该sheet中的 第6行第2列的单元格
    #  ******************************************
    #  ******************************************
    #  ******************************************



    # 获取部分单元格 比如：
    cell_list = sheet["b7":"c9"]
    print(cell_list) 
    # 截图在下面
    # ((<Cell 'android'.B7>, <Cell 'android'.C7>), (<Cell 'android'.B8>, <Cell 'android'.C8>), (<Cell 'android'.B9>, <Cell 'android'.C9>))





    # 获取第 N 行的所有单元格 A1,B1,C1,D1.....   =================================
    # for cell in sheet[5]:  # 获取第 5 行的所有单元格上的数据
    #     print(cell.value, end="\t")
    """
      序号	说明	权限字符	作用	备注	敏感权限	protectionLevel	
    """

    # 获取所有行的数据 【也就在遍历时候使用索引获取第 N 列的数据】=================================
    # for row in sheet.rows:
    #     """遍历sheet的每一行，加个索引就可以是 输出列的单元格上的数据"""
    #     # row = (<Cell 'android'.A1>, <Cell 'android'.B1>,...  <Cell 'android'.F1>, <Cell 'android'.G1>)
    #     # row = (<Cell 'android'.A2>, <Cell 'android'.B2>,.... <Cell 'android'.F2>, <Cell 'android'.G2>)
    #     print(row)
    # print(row[0].value) # 输出第一列的所有单元格上的数据


    # 获取所有列的数据【基于此加个索引也可以获取 某一行的单元格】=================================
    for col in sheet.columns:
        # col = (<Cell 'android'.A1>, <Cell 'android'.A2>, <Cell 'android'.A3>,... <Cell 'android'.A214>)
        # col = (<Cell 'android'.B1>, <Cell 'android'.B2>, <Cell 'android'.B3>,... <Cell 'android'.B214>)
        print(col[0])  # 获取第一行的单元格


    # 删除某个 Sheet
    del wb["IOS"]


    # 保存修改的数据
    wb.active = 0  # 指定默认打开的是哪个Sheet

    sheet.title = "android"  # Sheet 的名称
    wb.save("文件名.xlsx")

  ```


![获取部分单元格](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-5-28/1622170794929-image.png)


##### 2. 对齐方式
- horizontal：水平方式对齐：`general`,`left`,`center`,`right`,`fill`,`justify`,`centerContinuous`,`distributed`

- vertical: 垂直方式对齐：`top`, `center`, `bottom`, `justify`, `distributed`

- text_rotation: 旋转角度

- wrap_text：自动换行

```python
from openpyxl import load_workbook, workbook,styles


wb = load_workbook("1.xlsx")
sheet = wb.worksheets[0]  # 将第一个 Sheet对象赋给 变量 sheet

# 将 第6行第6列的单元格对象赋给 变量cell
cell = sheet.cell(6,6)
cell.alignment = styles.Alignment(horizontal='center',vertical='distributed', text_rotation=45, wrap_text=True)

wb.save('1.xlsx')

```



##### 3. 边框
- side的style有如下：
   `dashDot`,`dashDotDot`, `dashed`,`dotted`,
                            `double`,`hair`, `medium`, `mediumDashDot`, `mediumDashDotDot`,
                            `mediumDashed`, `slantDashDot`, `thick`, `thin`

```python
from openpyxl import load_workbook, workbook,styles
  
wb = load_workbook("1.xlsx")
sheet = wb.worksheets[0]  # 将第一个 Sheet对象赋给 变量 sheet

# 将 第6行第6列的单元格对象赋给 变量cell
cell = sheet.cell(6,6)
cell.border = cell.alignment = styles.Border(top=styles.Side(style='thin',color='ffb6c1'),
                               bottom=styles.Side(style='dashed',color='9932CC'),
                               left=styles.Side(style='dashed',color='9932CC'),
                               right=styles.Side(style='dashed',color='9932CC'),
                               diagonal=styles.Side(style='dashed',color='483d8b'), # 对角线
                               diagonalUp=True # 左下 - 右上
                               # diagonalDown=True # 左上 - 右下)

wb.save('1.xlsx')

```


##### 4. 字体

```python
from openpyxl import load_workbook, workbook,styles
  
wb = load_workbook("1.xlsx")
sheet = wb.worksheets[0] # 将第一个 Sheet对象赋给 变量 sheet

# 将 第6行第6列的单元格对象赋给 变量cell
cell = sheet.cell(6,6)
cell.font = styles.Font(name="微软雅黑",size=16,color='ff0000',underline='single')

wb.save('1.xlsx')

```

##### 5. 背景颜色

```python
from openpyxl import load_workbook, workbook,styles
  
wb = load_workbook("1.xlsx")
sheet = wb.worksheets[0] # 将第一个 Sheet对象赋给 变量 sheet

# 将 第6行第6列的单元格对象赋给 变量cell
cell = sheet.cell(6,6)
cell.fill = styles.PatternFill('solid',fgColor='99ccff')

wb.save('1.xlsx')
```

##### 6. 渐近背景颜色

```python
from openpyxl import load_workbook, workbook,styles
  
wb = load_workbook("1.xlsx")
sheet = wb.worksheets[0] # 将第一个 Sheet对象赋给 变量 sheet

# 将 第6行第6列的单元格对象赋给 变量cell
cell = sheet.cell(6,6)
cell.fill = styles.GradientFill('linear',stop=('FFFFFF','99ccff','000000')) # stop中的元素分别是 左中右的颜色

wb.save('1.xlsx')
```

##### 7. 设置行高列宽的值【索引从 1 开始】

```python
from openpyxl import load_workbook, workbook,styles
  
wb = load_workbook("1.xlsx")
sheet = wb.worksheets[0] # 将第一个 Sheet对象赋给 变量 sheet

sheet.row_dimensions[2].height = 50  # 设置 第 2 行的 高度
sheet.column_dimensions["E"].width = 100  # 设置 第 E 列的 宽度

wb.save('1.xlsx')
```

##### 8. 合并单元格

```python
from openpyxl import load_workbook, workbook,styles
  
wb = load_workbook("1.xlsx")
sheet = wb.worksheets[0] # 将第一个 Sheet对象赋给 变量 sheet

sheet.merge_cells("b2:d8")
sheet.merge_cell(start_row=15, start_column=3, end_row=18, end_cloumn=8)


# 解除合并
sheet.unmerge_cells("b2:d8")

wb.save('1.xlsx')
```


##### 9. 插入公式

```python
from openpyxl import load_workbook, workbook,styles
  
wb = load_workbook("1.xlsx")
sheet = wb.worksheets[0] # 将第一个 Sheet对象赋给 变量 sheet

# 插入公式的写法相当于是写入值到单元格中
from openpyxl import workbook, load_workbook

wb = load_workbook('2.xlsx')
sheet = wb.worksheets[0]

# 使用方式一选中单元格对象，然后使用该对象的 value 属性进行将公式写进去【必须带上value属性】
cell = sheet.cell(1, 3)
cell.value = "=a1+b1"

wb.save("2.xlsx")
wb.close()

```

##### 10. 选取部分区域
```python
from openpyxl import load_workbook

wb = load_workbook('2.xlsx')
sheet = wb.worksheet[0]  # 操作 第一个 sheet


# for i in sheet.iter_rows(min_col=1, min_row=5,max_col=7, max_row=10):
    """
    参数说明：
      1. min_col: 最小列数
      2. min_row: 最小行数
      
      3. max_col: 最大列数
      4. max_row: 最大行数
    """
 
```

###### 10.1 截取部分，使用案例一：
```python
from openpyxl import load_workbook

wb = load_workbook('2.xlsx')
sheet = wb.worksheets[0]

# 截取部分区域
for cell in sheet.iter_cols(min_row=1, max_row=3, min_col=1, max_col=2):  # 从 第一行 到 第三行，从第一列 到 第二列
    """
    迭代行数，cell = (<Cell 'Sheet1'.A1>, <Cell 'Sheet1'.A2>, <Cell 'Sheet1'.A3>)
    """
    print(cell)



for cell in sheet['b2':'c6']:
    print(cell)
    

```

![ 截取部分，使用案例一](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-5-28/1622191208356-image.png)


![截取部分，使用案例一](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-5-28/1622192257969-image.png)



##### 11. 删除 `sheet.delete_rows(idx,amount)`、`sheet.delete_cols(idx,amount)`
- 参数说明：
   1. idx：要删除的索引位置
   2. amount：从索引位置开始要删除的个数【 默认为1 】
```python
from openpyxl import load_workbook

wb = load_workbook('2.xlsx')
sheet = wb.worksheets[0]  # 将工作表对象 赋 给 变量 sheet

sheet.delete_cols(idx=1,amount=1)
sheet.delete_rows(idx=1,amount=1)
wb.save('2.xlsx')
```




##### 12. 插入 `sheet.insert_rows(idx,amount)`、`sheet.insert_cols(idx,amount)`
- 参数说明：
   1. idx：要插入的索引位置
   2. amount：从索引位置开始要插入的个数【 默认为1 】
```python
from openpyxl import load_workbook

wb = load_workbook('2.xlsx')
sheet = wb.worksheets[0]  # 将工作表对象 赋 给 变量 sheet

sheet.insert_rows(idx=5,amount=10)
sheet.insert_cols(idx=3,amount=2)
wb.save('2.xlsx')
```

##### 13. 移动 `sheet.move_range("H2:J10", rows=-1, cols=15)`
- 参数说明：
   1. 第一个字符串类型的参数：选中的Excel表格的区域 `"H2:J10"`
   2. rows = -1 : 向上移动1个位置、rows = 1 ：向下移动 1 行
   3. cols = 15 : 向右移动15个位置
```python
from openpyxl import load_workbook
wb = load_workbook('2.xlsx')
sheet = wb.worksheets[0]  # 将工作表对象 赋 给 变量 sheet

sheet.move_range("H2:J10", rows=-1, cols=15)
wb.save('2.xlsx')
```
###### 13.1 移动的区域中的单元格显示的数据是 写入公式的出来的结果
 - 假如 ：c1 单元格的数据是 由 a1 * b1 相乘的来的也就是公式：`=a1*b1`

   现在要将 a1 到 c1 的数据向右移动 n 列，那么若想公式随着位置的移动而改变，需要在 `move_range` 方法中添加个参数并且改为 `True` 
```python
from openpyxl import load_workbook
wb = load_workbook('2.xlsx')
sheet = wb.worksheets[0]  # 将工作表对象 赋 给 变量 sheet

sheet.move_range("a1:c3", cols=15, translate=True)
# True 相当于随着源数据单元格的变动而改变

wb.save('2.xlsx')
```








