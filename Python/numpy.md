### numpy笔记
- [numpy.array:生成数组](#生成数组)
- [numpy.tile:将数据复制多次并生成新的数组](#将数据复制多次并生成新的数组)
- [笔记](#笔记)


#### 生成数组
```python
# 二维，数据默认是numpy.float64类型
X = numpy.array([
	[0, 2, 0, 3],
	[0, 1, 4, 3],
	[0.1, 1, 1, 3],
])

# 一维
Y = numpy.array([0, 0, 1, 1])
```

#### 将数据复制多次并生成新的数组
```python
# 将X数组复制两次并生成new_array
new_array = numpy.tile(X, 2)

# 将X数组内部元素复制3次，再将新生成的数组整体复制5个组成更高维的数组
new_array = numpy.tile(X, (5, 3))
```

#### 笔记
```python
# 矩阵想减，直接用-，如果维数不同的话，会将维数少的复制多份，但是前提是两个数组最里面的那维数组的长度是一样的
new_array = X - Y

# 矩阵每一项都变成自身的5次方
new_array = X**5
# 矩阵每项开方
new_array = X**0.5


# 求和：行向量相加、列向量相加
X = numpy.array([
	[0, 2, 0, 3],
	[0, 1, 4, 3],
	[0.1, 1, 1, 3],
])
# 行向量相加
new_array = X.sum(axis = 1)
new_array = X.sum(1)

# 列向量相加
new_array = X.sum(axis = 0)
new_array = X.sum(0)

# 从小到大排序并返回索引值
# 从大到小排序并返回索引值

```
