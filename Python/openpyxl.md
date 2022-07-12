- [头文件](#头文件)
- [参考帖子](#参考帖子)
- [新建xlsx](#新建xlsx)
- [加载表](#加载表)
- [获取表](#获取表)
- [创建表](#创建表)
- [修改数据](#修改数据)
- [获取数据](#获取数据)
- 单元格样式
  - [字体样式](#字体样式)
  - [填充样式（背景颜色）](#填充样式（背景颜色）)
  - [边框样式](#边框样式)
  - [对齐样式](#对齐样式)
- [合并单元格](#合并单元格)
- [保存elsx](#保存elsx)
- [注意事项](#注意事项)

#### 头文件
```python
import openpyxl
from openpyxl.styles import Font, PatternFill, Border, Side, Alignment
```

#### 参考帖子
- 参考帖子：https://blog.csdn.net/liyuanjinglyj/article/details/87895700

#### 新建xlsx
```python
# 注意是大写的W !
wb=openpyxl.Workbook()
```

#### 加载表
- 注意：openpyxl只允许操作xlsx文件，不允许操作xls文件
```python
wb = openpyxl.load_workbook(r"C:\Users\84689\Desktop\毕设\Coursera.xlsx")
```

#### 获取表
```python
sheet = wb['Sheet1']
```

#### 创建表
```python
wb.create_sheet(title='test3')
sheet = wb['test3']
```

#### 修改数据
```python
sheet.cell(1, 1, '111111')
sheet.cell(1,1).value='1111111'
sheet['A1'].value='1111111'
```

#### 获取数据
```python
print(now[1][0].value)#打印第一行第一列的内容
print(now[1][1].value)#打印第一行第二列的内容
```

#### 字体样式
```python
# 设定单元格字体样式模板
font1 = Font(name='微软雅黑', size=10, bold=False, italic=False, vertAlign=None, underline='none', strike=False,
             color='FF000000')

# 修改单元格字体样式
sheet.cell(1,1).font=font1
sheet['A1'].font = font1
```

#### 填充样式（背景颜色）
```python
# 设定单元格样式（填充样式）模板
fill1 = PatternFill(fill_type='darkUp', start_color='FFFF00', end_color='FF0000')

# 修改单元格填充样式
sheet.cell(1, 1).fill = fill1
```

#### 边框样式
```python
# 设定边框样式模板
border = Border(left=Side(border_style='dashDotDot', color='9932CC'),
                right=Side(border_style='dashDotDot', color='121212'),
                top=Side(border_style='dashDotDot', color='8B0A50'),
                bottom=Side(border_style='dashDotDot', color='B3EE3A'), )

# 修改单元格边框样式
sheet.cell(5, 4).border = border
```

#### 对齐样式
```python
# 设定对齐样式模板
alignment = Alignment(horizontal='center', vertical='center', text_rotation=0, indent=0)

# 修改单元格对齐样式
sheet.cell(5, 3).alignment = alignment
```

#### 合并单元格
```python
sheet.merge_cells('A1:E1')
```

#### 保存elsx
```python
wb.save(r"C:\Users\84689\Desktop\毕设\Coursera.xlsx")
```

#### 注意事项
- 不能这样导入这个模块，会出大问题
```python
from openpyxl import *
```

