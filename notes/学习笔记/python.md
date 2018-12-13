# python学习笔记
<!-- GFM-TOC -->
* [字符串](#字符串)
* [列表](#列表)
* [python内置函数](#python内置函数)
* [python初始化问题](#python初始化问题)
* [python数据规范化问题](#python数据规范化问题)
* [python浅拷贝和深拷贝](#python浅拷贝和深拷贝)
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
seq = ("a", "b", "c") # 字符串序列
print(str.join(seq)) # a-b-c
```

#### python 判断字符属于数字、字母还是空格：  
```python
c.isdigit() # 数字
c.isalpha() # 字母
c.isalnum() # 数字和字母
c.isspace() # 空格
```

#### python strip()
str.strip(c) 用于移除字符串首尾指定的字符，不指定 c 则默认为空格或换行符，只要首尾包含有 c 的序列就删除，不管具体的顺序。  
str.lstrip(c) 移除左端指定字符。  
str.rstrip(c) 移除末端指定字符。

## 列表
#### list 和 set
判断值是否在 set 中的速度比 list 快的多，因此 set 用到 hash 时间复杂度为 O(1)， 而 list 时间复杂度 O(n)  
因此可以将 list 转为 set 来提高查询效率

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

#### sort()和sorted()
[sort()和sorted的区别](https://www.cnblogs.com/jonm/p/8281228.html)
- 内置函数 sort()
sort(fun，key，reverse=False)，可以对列表中的元素进行排序，会改变当前对象。
1. fun： 表明此 sort 函数是基于何种算法进行排序的，一般默认情况下 python 中用的是归并排序，并且一般情况下我们是不会重写此参数的，所以基本可以忽略；
2. key： 用来指定一个函数，此函数在每次元素比较时被调用，此函数代表排序的规则，也就是你按照什么规则对你的序列进行排序；
3. reverse： 用来表明是否逆序，默认的 False 情况下是按照升序的规则进行排序的，当 reverse=True 时，便会按照降序进行排序。

- 全局函数 sorted()
与 sorted 参数一致，对所有可迭代的序列都是适用的，只会返回一个排序后的当前对象的副本，而不会改变当前对象。

如果要自己写比较函数的话，python3 中需要 import functools.cmp_to_key() 方法。
```python
from functools import cmp_to_key

nums = [1, 3, 2, 4]
nums.sort(key=cmp_to_key(lambda a, b: a - b)) # nums = [1, 2, 3, 4]
```
#### 反转
反转List: list.reverse()  
反转字符串: str[::-1]


## python内置函数
#### int()和bin()
int() 函数用于将一个字符串或数字转换为整型。 
用法：int(x, base=10)，x 为字符串或数字，base为x进制数，默认十进制。

bin() 返回一个整数 int 或者长整数 long int 的二进制表示。

#### ord()和chr()
chr(i) 返回整数 i 对应的 ascii 字符。
ord(c) 返回字符 c 对应的 ascii 数值。
'A' 的 ascii 为 65， 'a' 的 ascii 为 97，小写字母比大写字母 **大 32**

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

## python浅拷贝和深拷贝
1. 直接赋值  
在 python 中，对象赋值实际上是对象的引用。当创建一个对象，然后把它赋给另一个变量的时候，python 并没有拷贝这个对象，而只是拷贝了这个对象的引用。  
若原始列表改变，被赋值的 b 也会做相同的改变； 若 b 改变，原始列表也会做相同的改变；即 a 和 b 是同步变化。
```python
a = [1,2,3,["a","b"]]
b = a # b = [1,2,3,["a","b"]]
a.append(4) # b = [1, 2, 3, ['a', 'b'], 4]
```

2. 浅拷贝  
在 copy 模块中，用 copy 函数完成浅拷贝。  
浅拷贝创建一个具有相同类型，相同值但 id 不同的新对象。

注意：对 copy 后的新对象的元素进行修改不会影响原对象，但是若对新对象或原对象中的子对象（即["a", "b"]）进行修改，那么新对象和原对象会同步改变，即对子对象只是引用。

```python
import copy
a = [1,2,3,["a","b"]]
c = copy.copy(a)
a.append(4) # a = [1, 2, 3, ['a', 'b'], 4] b = [1, 2, 3, ['a', 'b']]
c. append(1) # a = [1, 2, 3, ['a', 'b'], 4] b = [1, 2, 3, ['a', 'b'], 1]
a[3].append('c') # a = [1, 2, 3, ['a', 'b', 'c'], 4] b = [1, 2, 3, ['a', 'b', 'c'], 1]
```

3. 深拷贝
在 copy 模块中，用 deepcopy 函数完成深拷贝。  
深拷贝是完全拷贝，包含对象里面的自对象的拷贝，所以原始对象的改变不会造成深拷贝里任何子元素的改变。
```python
import copy
a = [1,2,3,["a","b"]]
c = copy.deepcopy(a)
```


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
<div align="center"><img src="../../pics/python/bit.jpg"></div>

## 正则表达式
<div align="center"><img src="../../pics/python/re.jpg"></div>

## 变量
#### 星号和双星号
单个星号 * ：该位置接收任意多个非关键字参数，在函数中转化为**元组**(1,2,3,4)
双星号 ** ： 该位置接收任意多个关键字 (key-word) 参数，在函数中转化为**字典**{a=1,b=2}

## python三大神器
### 装饰器
- 装饰器 Decorator 本质上是一个 python 函数，可以让其他函数在不需要任何代码变动的前提下增加额外功能。  
- 装饰器的返回值是一个函数对象，常用场景有：插入日志、性能测试、事务处理、缓存、权限校验等。  
- 装饰器可以抽离出大量与函数本身功能无关的雷同代码并继续重用

```python
import functools

def log(text):
	def wrapper(func):
		@functools.wraps(func)
		def inner_wrapper(*args, **kw): 
			print('%s %s()' %(text, func.__name__))
			return func(*args, **kw) # 可以让其用于任何函数，无论参数形式如何
		return inner_wrapper
	return wrapper
```

### 生成器
生成器 generator 可以实现一边循环一边计算，节省空间，与列表生成式的区别就在于最外层是 [] 还是 ()
```python
l = [x*x for x in range(10)]
g = (x*x for x in range(10))
```

通过函数可以实现复杂逻辑的生成式，当函数中包含 yield 关键字时