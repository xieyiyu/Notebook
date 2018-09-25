# python学习笔记

python 判断字符属于数字、字母还是空格：  
```
数字：c.isdigit()
字母：c.isalpha()
数字和字母：c.isalnum()
空格：c.isspace()
```

python 保留小数位    
float('%.2f' % a)  
  
Python join()方法  
```
str.join(sequence)用于将序列中的元素以指定的字符连接生成一个新的字符串。经常见到''.join()将列表字典等转化为字符串。

str = "-";
seq = ("a", "b", "c"); # 字符串序列
print str.join( seq ); # a-b-c
```

python str  
```
python 中的 str 类型不能修改，但可以通过切片操作来实现插入、删除和修改操作。
如 a = '12045'，需要把 '0' 修改为 '3'，
可以 a = a[:2] + '3' + a[3:]
```

### 列表
extend 和 append  
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

List index()
```python
list.index(obj) # 用于从列表中找出某个值第一个匹配项的索引位置，没有找到对象则抛出异常。
```

反转List: list.reverse()  
反转字符串: str[::-1]

### 正则表达式
<div align="center"><img src="../../pics/python/re.jpg"></div>
