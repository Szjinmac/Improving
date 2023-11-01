# Pandas入门



## Series是什么

Series是一种类似于一维数组的对象，它由一组数据（各种NumPy数据类型）以及一组与之相关的数据标签（即索引）组成。仅由一组数据即可产生最简单的Series：

```python
In [11]: obj = pd.Series([4, 7, -5, 3])

In [12]: obj
Out[12]: 
0    4
1    7
2   -5
3    3
dtype: int64
```

通常，我们希望所创建的Series带有一个可以对各个数据点进行标记的索引：

```python
In [15]: obj2 = pd.Series([4, 7, -5, 3], index=['d', 'b', 'a', 'c'])

In [16]: obj2
Out[16]: 
d    4
b    7
a   -5
c    3
dtype: int64

In [17]: obj2.index
Out[17]: Index(['d', 'b', 'a', 'c'], dtype='object')
```

对于许多应用而言，Series最重要的一个功能是，它会根据运算的索引标签自动对齐数据



## DataFrame是什么

DataFrame是一个表格型的数据结构，既有行索引也有列索引



### 丢弃

Obj.drop(['a','b'])



用一个值或序列对DataFrame进行索引其实就是获取一个或多个列



### loc和iloc

| df[val]                               | 从dataframe选取单列                     |
| ------------------------------------- | --------------------------------------- |
| df.loc[val]                           | 通过标签，选取dataframe的单个行或一组行 |
| df.loc[:,val]                         | 通过标签，选取单列或列子集              |
| `loc[row_label, column_label]`        | 通过标签，同时选取行和列                |
| `iloc[row_position, column_position]` | 通过整数位置，选取单个行或列子集        |
| df.iloc[:,where]                      | 通过整数位置，选取单个列或列子集        |
| df.iloc[i，j]                         | 通过整数位置，同时选取行和列            |
|                                       |                                         |
|                                       |                                         |
|                                       |                                         |





df1和df2把它们相加后将会返回一个新的DataFrame，其索引和列为原来那两个DataFrame的并集





### 排序

Obj.sort_index()



调用DataFrame的sum方法将会返回一个含有列的和的Series,传入axis='columns'或axis=1将会按行进行求和运算

### 

### 滤除缺失数据

pd.dropna返回一个仅含非空数据和索引值的series

对于dataframe，dropna默认丢弃含相关值的行

data.dropna(how='all')只会丢弃全为na的行



### 填充缺失数据

Pd.fillna();填充常数



### 移除重复数据

data.duplicated()各行是否是重复行

data.drop_duplicates()



### 利用函数或映射进行数据转换

Pd.map方法

data.replace(-999, np.nan)

pd.cut(ages,bins) ==bins==表示要划分的范围

pd.value_counts(cats)是pandas.cut结果的面元计数。

### 读取数据

pd.read_table('examples/ex1.csv', sep=',')

pd.read_csv('examples/ex6.csv', nrows=5)只读取5行

json.dumps(result)将Python对象转换成JSON格式

