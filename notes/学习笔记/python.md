# python学习笔记
<!-- GFM-TOC -->
* [字符串](#字符串)
* [列表](#列表)
* [python初始化问题](#python初始化问题)
* [python数据规范化问题](#python数据规范化问题)
* [正则表达式](#正则表达式)
* [位运算](#位运算)
<!-- GFM-TOC -->

## 字符串
#### python str  
python 中的 str 类型不能修改，但可以通过切片操作来实现插入、删除和修改操作。  
如 a = '12045'，需要把 '0' 修改为 '3'
```python
a = a[:2] + '3' + a[3:]
```

#### python join()
str.join(sequence)用于将序列中的元素以指定的字符连接生成一个新的字符串。经常见到''.join()将列表字典等转化为字符串。  
```python
str = "-";
seq = ("a", "b", "c"); # 字符串序列
print str.join( seq ); # a-b-c
```

#### python 判断字符属于数字、字母还是空格：  
```python
c.isdigit() # 数字
c.isalpha() # 字母
c.isalnum() # 数字和字母
c.isspace() # 空格
```

#### ord()和chr()
chr(i) 返回整数 i 对应的 ascii 字符。
ord(c) 返回字符 c 对应的 ascii 数值。
'A' 的 ascii 为 65， 'a' 的 ascii 为 97，小写字母比大写字母 **大 32**

## 列表
#### extend 和 append  
```python
list.append(object) # 向列表中添加一个对象 object, 整体打包添加进去
list.extend(sequence) # 把一个序列 seq 的内容添加到列表中
```
```python
a = [1, 2, 3]
b = [4, 5, 6]
a.append(b) # a = [1, 2, 3, [4, 5, 6]]
a.extend(b) # a = [1, 2, 3, 4, 5, 6]
```

#### List index()
```python
list.index(obj) # 用于从列表中找出某个值第一个匹配项的索引位置，没有找到对象则抛出异常。
```

#### 反转
反转List: list.reverse()  
反转字符串: str[::-1]

## python初始化问题

#### 一维数组初始化
```python
nums = [0 for i in range(n)]
```

#### 二维数组初始化
初始化 m 行 n 列的二维数组, 以嵌套循环的方式
```python
nums = [[0 for j in range(n)] for i in range(m)] # 列在前，行在后
```
以 numpy 方式, 调用 zeros 方法
```python
import numpy
nums = numpy.zeros([m, n])
```

#### 无穷大和无穷小
```python
float('inf') #无穷大
-float('inf') #无穷小
```

## python数据规范化问题
#### python 保留小数位    
float('%.2f' % a)  

## 位运算
python的位运算符是把数字看作二进制来进行计算的。
```
a = 0011 1100
b = 0000 1101
-----------------
a&b = 0000 1100
a|b = 0011 1101
a^b = 0011 0001
~a  = 1100 0011
```
<div align="center"><img src="../../pics/python/bit.jpg" weight='50%'></div>

## 正则表达式
<div align="center"><img src="../../pics/python/re.jpg"></div>
