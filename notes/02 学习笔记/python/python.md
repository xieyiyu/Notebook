# python学习笔记
<!-- GFM-TOC -->
* [python 概念](#python-概念)
    * [python 优缺点](#python-优缺点)
    * [python java c 区别](#python-java-c-区别)
    * [python2 和 python3 区别](#python2-和-python3-区别)
    * [IDLE](#idle)
    * [python 参数传递机制](#python参数传递机制)
* [变量](#变量)
    * [星号和双星号](#星号和双星号)
    * [命名方式](#命名方式)
* [python 数据结构](#python-数据结构)
    * [number](#number)
    * [str](#str)
        *[字符串前缀](#字符串前缀)
    * [tuple](#tuple)
    * [list](#list)
    * [set](#set)
    * [dict](#dict)
* [python 运算（除法、取模）](#python-运算)
* [IO 编程](#io-编程)
    * [读取键盘输入](#读取键盘输入)
    * [文件读写](#文件读写)
    * [目录操作](#目录操作)
* [python内置函数](#python内置函数)
* [python初始化问题](#python初始化问题)
* [python数据规范化问题](#python数据规范化问题)
* [python浅拷贝和深拷贝](#python浅拷贝和深拷贝)
* [正则表达式](#正则表达式)
* [位运算](#位运算)
* [python三大神器](#python三大神器)
    * [装饰器](#装饰器)
    * [生成器](#生成器)
    * [迭代器](#迭代器)
* [函数式编程](#函数式编程)
    * [高阶函数](#高阶函数)
    * [lambda](#lambda)
    * [偏函数](#偏函数)
* [异常处理](#异常处理)
* [python 编码](#python-编码)
* [面向对象编程](#面向对象编程)
* [其他](#其他)
* [python 魔术方法](#python-魔术方法)
* [LEGB 规则](#legb-规则)
<!-- GFM-TOC -->

## python 基础
### python 优缺点
**优点**：
1. 优雅、明确、简单。易学，能够专注解决问题而不是搞明白语言本身。
2. 开发效率高，有强大的第三方库
3. 可移植性，在多种平台都可以使用
4. 可扩展性，能够将部分程序用 C 写，在 python 中使用
5. 可嵌入性，将 python 嵌入到 C 中，从而向程序用户提供脚本功能

**缺点**：
1. 相比于 C 和 JAVA，运行速度慢
2. 由于 python 开源，代码不能加密
3. python 的 GIL 锁限制并发，线程不能利用多 cpu

### python java c 区别
python 是动态语言，解释型语言，运行速度较慢；在运行期间才做数据类型检查；语法简单，代码量少，类库丰富
java、 c 是静态语言， 数据类型在编译前就需要明确

### python 为什么不需要编译
python 是解释性语言，程序不需要编译，在运行时才翻译成机器语言，每执行一次都要翻译一次，因此效率较低。
python 源码不需要编译成二进制代码，它可以直接从源代码运行程序。当我们运行 python 文件程序的时候，python 解释器将源代码转换为字节码，然后再由 python 解释器来执行这些字节码。

#### python 解释器
python 解释器由一个编译器和一个虚拟机构成，编译器负责将源代码转换成字节码文件，而虚拟机负责执行字节码。
所以，解释型语言其实也有编译过程，只不过这个编译过程并不是直接生成目标代码，而是中间代码（字节码），然后再通过虚拟机来逐行解释执行字节码。

### python2 和 python3 区别
1. print
2. 默认编码： python2 是 ASCII，python3 是 UTF-8
3. 最核心变化：python 2 中 unicode 是字符串（定义要 u''），str 是字节串码； python3 中 str 是字符串，byte 是字节串，py3 默认支持 unicode 字符集，因此不用定义 u
4. 解析用户输入：python2 用 raw_input(), python3 用 input() ，都输入 str
5. True 和 False：python2 中是两个全局变量，数值是 1 和 0，可以修改指向其他对象；python3 中是关键字，不可重新赋值
6. 在 python2 中很多返回 list 对象的的内置函数在 python3 中改为了返回类似迭代器的对象（惰性加载操作大数据更有效率），比如 dict.keys(), dict.values()
7. 加入 nonlocal 关键字，可以在闭包中给一个变量申明为非局部变量
8. 除法：python2 中 1/2==0， python3 中 1/2==0.5
9. sort 自定义排序函数，在 python2 中可以直接传入 cmp 函数； python3 中需要 from functools import cmp_to_key， 用的时候要 key = cmp_to_key(cmp)
10. long 类型： python2 的整型有 int 和长整型 long； python3 中整合了二者，只有 int 类型

将 python2 转为 python3 兼容的： `from __future__ imports xxx`

### IDLE
IDLE 是 python 整体化的开发和学习环境，装好 python，IDLE 就自动装好。其实在 cmd 中输出 python 进入 python 运行环境基本一致，但又高亮、自动缩进、方法提示等功能。

### python参数传递机制
python 中一切皆对象，任何变量都是对象的引用，python 中参数传递都是**“传对象引用”**的方式，相当于传值和传引用的结合。若收到是可变对象的引用，就能修改对象的原始值，相当于“传引用”； 若收到是不可变对象，就不能直接修改原始对象，相当于“传值”。

- 值传递：存放实参变量的值，被调函数对形参的任何操作都是作为局部变量进行，不影响主调函数的实参变量的值。
- 引用传递：存放实参变量的地址，被调函数对形参的任何操作都影响主调函数中的实参变量。

### pip 与 pypi
pip 是 Python 包管理工具，是easy_install的替代品，英文python  install packages ！

PyPI(Python Package Index， python包索引)是 python 官方的第三方库的仓库，所有人都可以下载第三方库或上传自己开发的库到 PyPI。PyPI 推荐使用 pip 包管理器来下载第三方库。

## 变量
### 星号和双星号
单个星号 * ：该位置接收任意多个非关键字参数，在函数中转化为**元组**(1,2,3,4)
双星号 ** ： 该位置接收任意多个关键字 (key-word) 参数，在函数中转化为**字典**{a=1,b=2}

### 命名方式
python中主要存在四种命名方式：
```
1、object #公用方法
2、_object #半保护
    #被看作是“protect”，意思是只有类对象和子类对象自己能访问到这些变量，在模块或类外不可以使用，不能用’from module import *’导入。
    #__object 是为了避免与子类的方法名称冲突， 对于该标识符描述的方法，父类的方法不能轻易地被子类的方法覆盖，他们的名字实际上是_classname__methodname。
3、__object  #全私有，全保护
    #私有成员“private”，意思是只有类对象自己能访问，连子类对象也不能访问到这个数据，不能用’from module import *’导入。
4、__object__     #内建方法，用户不要这样定义
```

### 系统变量
`__all__`
python 模块中的__all__，用于模块导入时限制，如：from module import *
此时被导入模块若定义了__all__属性，则只有__all__内指定的属性、方法、类可被导入；若没定义，则导入模块内的所有公有属性，方法和类。

## python数据结构
### 不可变数据类型
变量所指的内存地址的值不可以改变，对其重新赋值其实是重新创建了一个不可变类型的对象，并将原来的变量重新指向新创建的对象（若没有其他变量引用原来的对象，会被回收）。

不可变类型有： number(int、float、bool、complex)、 string、 tuple

#### number
python3 中对 int 和较短的 string 进行了缓存，无论声明多少个值相同的变量，实际上都是指向同一个内存地址

整数： 相同值的正整数和 0 的 id 都相同，相同值的负整数，-1 到 -5 相同，-6 之后不同
浮点数： 正浮点数都相同，负浮点数都不同，+0.0 和 -0.0 不同
虚数： 实部和虚部都存在的话，id 不同； 只有虚部的话 id 相同
字符串： 值相同的话 id 相同
元组： 空元组的 id 相同，非空的话 id 不同
列表，字典，集合： 无论什么情况，空或非空，id 标识都不同

**数据驻留小数据池**
在不同模块里，部分数据驻留小数据池中，python3 提前在内存中创建了 [-5,256] 范围的整数, 不同模块的两个变量,在此范围具有相同的值 id 相同。如果超出了这个范围，每次运行 id 都会变化。

小数据池针对： int、string、bool、空元祖()、None 关键字

目的： 节省内存空间，提升代码效率

如果在同一代码块下，则采用同一代码块下的换缓存机制。
如果是不同代码块，则采用小数据池的驻留机制。

#### str
##### 字符串与字节串
python3 中只有 str 这种数据类型可以保存文本信息，str 是字符串，是 unicode，没有前缀。  
python3 中新增 bytes 类型表示字节串（二进制数据），需要加前缀 b， by = b'china'，只能用字节作为序列值，用 [0, 256] 的整数表示。
```python
by = b'china'
print(list(by)) # [99, 104, 105, 110, 97]
```

文本用 str 表示，但将数据保存到文本或在网络编程中必须是二进制数据，因此字符串和字节串会进行一个转换。
- str.encode(encoding='xxx') 实现 str->bytes
- bytes.decode(encoding='xxx') 实现 bytes->str

##### 字符串前缀
###### 字符串前缀 f
格式化字符串常量（formatted string literals），是Python3.6新引入的一种字符串格式化方法，该方法源于PEP 498 – Literal String Interpolation，主要目的是使格式化字符串的操作更加简便。f-string在形式上是以 f 或 F 修饰符引领的字符串（f'xxx' 或 F'xxx'），以大括号 {} 标明被替换的字段；f-string在本质上并不是字符串常量，而是一个在运行时运算求值的表达式

```python
comedian = {'name': 'Eric Idle', 'age': 74}
f"The comedian is {comedian['name']}, aged {comedian['age']}."
```

###### 字符串前缀 r
python 中字符串的前导 r 代表**原始字符串标识符**，即字符串中的特殊符号不会被转义，适用于正则表达式中繁杂的特殊符号表示。 如 r'\n' 会直接输出 \n

#### tuple
Python 中的 tuple 结构为 “不可变序列”，用小括号表示。为了区别数学中表示优先级的小括号，当 tuple 中只含一个元素时，需要在元素后加上逗号。即 (1, )， 如果是 (1) 会被判定为 int 型

值相同的元组的地址可能不同，元组的本质是只读的列表

##### zip 函数
zip() ： 将可迭代的对象作为参数，将对象中对应的元素打包成一个个元组，python3 中返回 zip 对象，用 list() 将其转换成列表。

若各个迭代器的元素个数不一致，则返回列表长度与最短的对象相同，利用 * 号操作符，可以将元组解压为列表。

```python
a = [1, 2, 3]
b = [4, 5, 6]
c = [7, 8, 9, 10, 11]

print(zip(a, b)) # <zip object at 0x000002510A27AEC8>
print(list(zip(a, b))) # [(1, 4), (2, 5), (3, 6)]
print(list(zip(a, b, c))) # [(1, 4, 7), (2, 5, 8), (3, 6, 9)]

z = zip(a, b, c)
print(list(zip(*z))) # [(1, 2, 3), (4, 5, 6), (7, 8, 9)]
```

### 可变数据类型
变量所指的内存地址处的值是可以改变的，值的变化不会引起新建对象，地址不会改变。

有 list、 set 和 dict， 比如对 a = [1, 2, 3] 进行 append 或 pop， a 的地址不会改变，但若有一个 b = [1, 2, 3] ，a 和 b 的地址是不同的； 若 c = b，此时 b c 的地址相同

#### list
##### 4. sort()和sorted()
[sort()和sorted的区别](https://www.cnblogs.com/jonm/p/8281228.html)
- 内置函数 sort()
sort(fun，key，reverse=False)，可以对列表中的元素进行排序，会改变当前对象。
1. fun： 表明此 sort 函数是基于何种算法进行排序的，一般默认情况下 python 中用的是归并排序，并且一般情况下我们是不会重写此参数的，所以基本可以忽略；
2. key： 用来指定一个函数，此函数在每次元素比较时被调用，此函数代表排序的规则，也就是你按照什么规则对你的序列进行排序；
3. reverse： 用来表明是否逆序，默认的 False 情况下是按照升序的规则进行排序的，当 reverse=True 时，便会按照降序进行排序。

如果要自己写比较函数的话，python3 中需要 import functools.cmp_to_key() 方法。
```python
from functools import cmp_to_key

nums = [1, 3, 2, 4]
nums.sort(key=cmp_to_key(lambda a, b: a - b)) # nums = [1, 2, 3, 4]
```

- 全局函数 sorted()
与 sort 参数一致，对所有可迭代的序列都是适用的，只会返回一个排序后的当前对象的副本，而不会改变当前对象。要注意 sorted 返回的是一个列表，不管输入是 set 还是 dict

可以自定义比较函数，sorted()也是一个高阶函数，它可以接收一个比较函数来实现自定义排序，比较函数的定义是，传入两个待比较的元素 x, y，如果 x 应该排在 y 的前面，返回 -1，如果 x 应该排在 y 的后面，返回 1。如果 x 和 y 相等，返回 0。

```python
nums = sorted(nums, cmp) # 按从大到小的顺序排序

def cmp(x, y):
    if x > y:
        return -1
    if x < y:
        return 1
    return 0
```

##### 找出两个列表的相同元素和不同元素
```python
list1 = [1, 2, 3]; list2 = [3, 4, 5]
set1, set2 = set(list1), set(list2)
print(set1 & set2) # 交集，{3}
print(set1 | set2) # 并集，{1, 2, 3, 4, 5}
print(set1 ^ set2) # 异或，{{1, 2, 4, 5}}
```
注意： & | ^ 是用于集合操作，因此要把列表先转为 set

#### set
集合 set 中的元素互不相同，没有重复元素，set 中的元素是无序的，比如 {1, 2, 3} 和 {3, 2, 1} 是同一个集合，创建一个空集合可以用 `s = set()`，将一个 list 转为 set 元素的顺序会打乱。

set 和 dict 的底层实现方式类似，都是使用哈希，把 set 的实现方式叫做 Hash Set，dict 的实现叫 Hash Table。
set 与 dict 的不同是，set 只存储 key，对于 set 查找元素的时间复杂度为 O(1)

set 的去重是通过两个函数 `__hash__` 和 `__eq__` 结合实现的
1. 当两个变量的哈希值不同时，就认为这两个变量是不同的
2. 当两个变量哈希值相同时，调用 `__eq__` 方法，返回 True 则这两个变量是同一个，应该去除一个；返回 False 则不去重，因为哈希值相同的变量的值可能不同。

set 中的元素和 dict 的 key 必须是可以 hash 的，不可变类型类型都是可 hash 的，比如 number(int, float, complex)、布尔型、字符串(str, bytes)、tuple、None；而可变类型 list、set、dict 都是不可哈希的。

set 的 hash 寻址是二次散列和顺序寻址结合的,？？？

##### set 常用方法
1. s.add(elem)： 添加一个元素到 set 中，如果元素存在则什么都不做
2. s.remove(elem)： 删除 set 中的一个元素，元素不存则报错 KeyError
3. s.pop()： 删除并返回**任意**元素，空集报错 KeyError
4. s.clear()： 删除所有元素
set 不能修改元素，只能添加和删除元素，时间复杂度平均为 O(1), 最差的情况是 O(n)

#### dict
在 python2 中，字典是无序的，若要保持有序，需要用 OrderedDict
```python
from collections import OrderedDict
d = OrderedDict()
```

在 python3 中，字典是有序的

##### dict.items()
dict.items() 将 dict 转化为可迭代对象，dict 变成了一个列表，将字典中的每对 key 和 value 转换成了元组。

```python
dic = {'a':24, 'g':52, 'i':12, 'k':33}
print(dic.keys()) # dict_keys(['a', 'g', 'i', 'k'])
print(dic.values()) # dict_values([24, 52, 12, 33])
print(dic.items()) # dict_items([('a', 24), ('g', 52), ('i', 12), ('k', 33)])

for key, value in dic.items(): # 遍历每一对 key 和 value
    print(key, value)
```

dict.setdefault(key, default=None) 与 dict.get(key, default=None) 相似，都是返回指定键的值，如果键存在 dict 中，则返回其值，否则返回设置的默认值。
但不同的是，当键不存在于字典中，setdefault 会将其添加到 dict 中，并设置为默认值，而 get 不会。

##### 字典排序
用 sorted 可以对字典进行按 key 或按 value 排序，注意排序之后都会变成列表
```python
dic = {'a':24, 'k':33, 'g':52, 'i':12}
sorted(dic) # 默认按照 key 排序，结果为 ['a', 'g', 'i', 'k']
sorted(dic.keys()) # 按照 key 排序，结果为 ['a', 'g', 'i', 'k']
sorted(dic.values()) # 只会对 value 排序，结果为 [12, 24, 33, 52]
sorted(dic.items()) # 默认用 key 排序，结果为 [('a', 24), ('g', 52), ('i', 12), ('k', 33)]

# 按照 value 排序的正确做法
sorted(dic.items(), key=lambda x:x[1]) # 指定用 value 排序，结果为 [('i', 12), ('a', 24), ('k', 33), ('g', 52)]
```

##### 字典推导式
和列表生成式类似，字典也有推导式。推导式是从一个数据序列构建另一个新的数据序列的结构体。

将 dict 中的 key 和 value 互换
```python
dic = {'a': 10, 'b': 34}
dic = {v: k for k, v in dic.items()} # {10: 'a', 34: 'b'}
```

将字符串转化成字典
```python
str = "k:1|k1:2|k2:3|k3:4"
dic = {k:v for item in str.split('|') for k, v in (item.split(':') ,)} # {'k': '1', 'k1': '2', 'k2': '3', 'k3': '4'}
```

##### 两个列表组成一个字典
用 zip 函数将两个列表组合成一个 zip 对象，再用 dict 转成字典
```python
keys = ['a', 'b', 'c']
values = [1, 2, 3]
dic = dict(zip(keys, values)) # {'a': 1, 'b': 2, 'c': 3}
```

## python 运算
### 除法
#### 正数除法
python3 中的除法，`/` 总是返回浮点数，`//` 返回整除结果，且是向下取整。  
python2.6 之前的版本，除法只有 `/`，对于整数运算会舍弃小数部分，对于浮点数运算会保留小数。

需要注意的是：`//` 得到的是整除的结果，并不一定是整数，这取决于分子分母的数据类型。 `//` 叫做地板除，不保留浮点数的尾数
```python
a = 5 // 2 # 2
b = 5 / 3 # 1.6666666666666667
c = 5 % 2 # 1
d = 4.5 // 2 # 2.0
e = 4.5 / 2 # 2.25
f = 4.5 % 2 # 0.5
```

#### 负数除法
由于 python3 的除法是向下取整，比如 -4//3 = -2

但我们通常的计算中是**向零取整**，比如 -4//3 = -1，如果想要在 python3 中得到这个结果，需要 int(-4/3)

```python
a = int(-4/3) # 1
b = -4//3 # -2
c = -4/3 # -1.3333333333333333
```

### 取模
要注意的是对负数的取模运算，由于 python 是向下取整，对 -21%10 = 9，因为 -21//10 = -3

## IO 编程
在 IO 编程中，输入流 input stream 是数据从磁盘、网络等地方流入内存，输出流是从内存流到外面。  
同步 IO： CPU 等待程序完成，再执行后面的代码； 异步 IO： CPU 不等待磁盘操作

### 读取键盘输入
python2.x 中以下三个函数都支持
- raw_input([prompt]): 将所有输入作为字符串看待，返回字符串类型； prompt 提示的文字
- input([prompt])： 只能接收“数字”的输入，返回所输入的数字的类型（ int, float ）
- sys.stdin.readline() 将所有输入视为字符串，并在最后包含换行符'\n'，可以通过sys.stdin.readline().strip('\n')去掉换行符

python3.x 中：
- input(): 整合 raw_input()和input()，接收任意输入，将所有输入默认为字符串处理，并返回字符串类型。

### 文件读写
#### read
用 with open 方法能够自动调用 close() 方法
```python
with open('filename', 'r', encoding='utf-8') as f:
    f.read() # 一次性读取文件内容，适用于文件较小的情况，过大文件内存不足
    f.readline() # 每次读取一行内容
    f.readlines() # 一次性读取文件内容并按行返回 list，很适用配置文件
    for line in f: # 按行读取，使用大文件
```
- 读取二进制文件，如图片、视频等需要用 'rb' 模式
- 读取非 ASCII 码的文本文件，如 gbk 编码，需要先用二进制模式 'rb' 打开，再用 f.read().decode('gbk')  解码；用 codecs 可以自动转换编码直接读出 unicode
- 在 python3 下可以直接用 open()，是 io 模块提供； 而在 python2 中最好使用 codecs.open() 可以解决一些编码问题。

#### write
write()方法不会在字符串的结尾添加换行符('\n')
```python
fo = open('filename', 'r')
fo.write(string)
```

#### 文件读写模式
模式|可做操作|若文件不存在|是否覆盖
-|-|-|-
r  | 只读    |   报错     | - 
r+ | 可读可写 |   报错    | 是，要注意 r+ 从行首开始覆盖，有多长就覆盖多长，原来的后面还会存在
w  | 只写    |    创建    | 是
w+ | 可读可写 |   创建    | 是
a  | 只写    |    创建    | 否，行尾追加写
a+ | 可读可写 |   创建    | 否，行尾追加写

如果是 b(rb, r+b, wb, w+b, ab, a+b) 表示以二进制形式打开文件
在 python3 中，如果只是 r，则 read() 返回的是 str； 如果是 rb，read() 返回的是 bytes

如果是 rt，会自动识别 windows 平台的换行符，将 \r\n 转换成 \n。  
因为文本文件中的回车在不同操作系统中所用的字符表示不同。  
Windows: \r\n ； Linux/Unix: \n ； Mac OS: \r

如果要先写后读，w+ 和 a+ 需要用 seek(0,0) 将光标移到行首，否则读不出来
```python
with open('demo.txt', 'a+') as fw:
    fw.write('a')
    fw.seek(0,0)
    print(fw.read())
```

#### seek()
seek() 方法用于移动文件读取指针到指定位置。

`fileObject.seek(offset[, whence])`
offset： 开始的偏移量，也就是代表需要移动偏移的字节数
whence： 可选，默认值为 0。给 offset参 数一个定义，表示要从哪个位置开始偏移；0 代表从文件开头开始算起， 1 代表从当前位置开始算起，2 代表从文件末尾算起。
return： 成功返回新的文件位置， 失败返回 -1

#### 其他
os.rename(cur_file_name, new_file_name) 重命名 cur
os.remove(file_name) 删除文件

### 目录操作
- os.mkdir("newdir") 创建新目录
- os.chdir("dirname") 改变当前目录
- os.getcwd() 显示当前的工作目录
- os.rmdir('dirname') 删除目录，删除前所有内容应先被清除
- os.path.abspath(path) 返回绝对路径
- os.path.join(path1, path2) 合并路径

- os.walk() 实现文件、目录遍历器，返回三元组(root,dirs,files)
```python
for root, dirs, files in os.walk(dir):
    for file in files: # 遍历文件夹下的所有文件
```

- os.popen(cmd [, mode]) 用于从一个命令打开一个管道，运行 cmd 命令， mode 模式权限默认 'r'，也可以 'w'，可以用 read() 获取执行的输出
- os.system(cmd) 执行 cmd 命令，返回值是脚本运行的状态码，0 是成功


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
以 numpy 方式, 调用 zeros 方法
```python
import numpy
nums = numpy.zeros([m, n])
```

## python数据规范化问题
### python 保留小数位    
float('%.6f' % a) 可以控制保留六位小数，但是如果后面都是 0 的话，比如 0.00000，返回的是 0.0； 如果是 1.2200000 的话，返回的是 1.22

### Decimal
```python
from decimal import Decimal
num = 1
num = Decimal(num).quantize(Decimal('0.000000')) # 四舍五入，保留六位小数，不管 num 是什么形式
```

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
深拷贝是完全拷贝，包含对象里面的子对象的拷贝，所以原始对象的改变不会造成深拷贝里任何子元素的改变。
```python
import copy
a = [1,2,3,["a","b"]]
c = copy.deepcopy(a)
```
```python
b = a.copy() # dict 中的 copy() 方法，复制一份，不影响，独立的
b = copy.copy(a) # 浅拷贝
b = copy.deepcopy(a) # 深拷贝
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

左移 n 位： 最左边的 n 位被丢弃，在右边补上 n 个 0  
右移 n 位： 要考虑数值是否有符号。 若是无符号数值，则用 0 填补最左边 n 位； 若是有符号数值，正数用 0 填补，负数用 1 填补。

将整数右移一位与将整数除以 2 等价，但除法运算的效率比移位更低得多。 

## 正则表达式
<div align="center"><img src="../../pics/python/re.jpg"></div>

```\<``` 表示词首，如 ```\<abc``` 表示以 abc 为首的词
```\>``` 表示词尾，如 ```\>abc``` 表示以 abc 结尾的词

#### re.sub
替换字符串中的匹配项 re.sub(pattern, repl, string, count=0) 
repl 为替换的字符串，也可以是一个函数; count 为模式匹配替换的最大次数，默认 0 是替换所有。

#### re.compile
编译正则表达式，生成正则表达式对象，供 match() 和 search() 使用

#### re.match 和 re.search
- re.match(pattern, string, flag=0) flag 为标志位，用于控制正则表达式的匹配方式，如是否区分大小写, 匹配多行等  
从字符串的起始位置（也就是 index=0）开始匹配，若起始位置没有匹配成功就返回 None

- re.search(pattern, string, flag=0)
扫描整个字符串并返回第一个成功的匹配，没有符合的返回 None

#### findall
re.match 和 re.search 都是值匹配一次，而 findall 匹配所有，返回列表形式
```python
import re
pattern = re.compile(r'\d+') # 查找数字
res = pattern.findall(string)
```

#### finditer
与 findall 类似，但将匹配成功的结果作为一个迭代器返回

#### 匹配对象函数
- group(num=0) 匹配的整个表达式的字符串，group() 可以一次输入多个组号，从 1 开始，返回对象是 re.MatchObject
- groups() 返回一个包含所有小组字符串的元组，从 1 开始
- span() 返回匹配成功的位置，起始位置和终止位置

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

#### 闭包
闭包就是能够读取其他函数内部变量的函数，可以理解为定义在一个函数内部的函数，外部的叫外函数，内部的叫内函数。

在一个外函数中定义了一个内函数，内函数用到了外函数的临时变量，外函数的返回值是内函数的引用，这就构成了闭包。

```python
def outer(a):
    b = 10
    def inner(x):
        print(a * x +b) # a,b 是 outer 的临时变量
    return inner

demo = outer(1)
demo(2) # 输出 1*2+10 = 12
```

若要在内函数中修改闭包变量（外函数绑定给内函数的局部变量）：
1. 在 python3 中，用 nonlocal 关键字申明变量，表示这个变量不是局部变量空间的，需要向上一层变量空间中寻找该变量
2. 在 python2 中，没有 nonlocal 关键字，但可以把闭包变量改为可变类型数据进行修改，如 set、list、dict

```python
def outer(a):
    b = 10
    c = [a]
    def inner():
        nonlocal b
        b += 1 # 方法1
        c[0] += 1 # 方法2
        print(b, c[0])
    return inner

demo = outer(1)
demo() # 输出 11, 2
```

在使用闭包的过程中，一旦外函数被调用一次返回了内函数的引用，虽然每次调用内函数，是开启一个函数执行过后消亡，但是闭包变量实际上只有一份，每次开启内函数都在使用同一份闭包变量
```python
def outer(a):
    def inner(b):
        nonlocal a
        a += b
        return a
    return inner

demo = outer(1)
demo(2) # 输出 1+2=3
demo(3) # 输出 3+3=6
```

### 生成器
生成器 generator 可以实现一边循环一边计算，节省空间，与列表生成式的区别就在于最外层是 [] 还是 ()
```python
l = [x*x for x in range(10)]
g = (x*x for x in range(10))
```

通过函数可以实现复杂逻辑的生成器，当函数中包含 yield 关键字时

### 迭代器
可迭代对象 Iterable： 能够直接作用于 for 循环的对象，如 list、tuple、dict、set、str、generator
迭代器 Iterator： 可以被 next() 函数调用并不断返回下一个值的对象

生成器是 Iterator 对象，但 list、 dict、 str 虽然都是 Iterable，但不是 Iterator， 可以用 iter() 方法将其变成 Iterable 类型。

Python 的 Iterator 对象表示的是一个数据流，Iterator 对象可以被 next() 函数调用并不断返回下一个数据，直到没有数据时抛出 StopIteration 错误。可以把这个数据流看做是一个有序序列甚至是无限大的数据流，只能不断通过 next() 函数实现按需计算下一个数据，所以 Iterator 的计算是惰性的，只有在需要返回下一个数据时它才会计算。

for 循环的本质是不断调用 next()

## 函数式编程
特点： 允许把函数本身作为参数传入另一个函数，还允许返回一个函数
### 高阶函数
把函数作为参数传入，这样的函数称为高阶函数
#### 1. map/reduce
map(function, iterable, ...) 将传入的函数 function 依次作用到序列的每个元素上，并将结果作为新 list 返回。
```python
map(lambda x: x**2, [1,2,3]) # [1,4,9]
map(lambda x, y: x+y, [1,2,3], [4,5,6]) # [5,7,9]
```

reduce(function, iterable[, initializer]) 对参数序列中的元素进行累计，先用 function 计算序列中的 1,2 个元素，得到的结果在和第 3 个元素进行计算。
```python
# 实现将字符串转整数
def char2num(s):
    return {'0':0, '1':1, ...}
def str2int(s):
    return reduce(lambda x,y: x*10+y, map(char2num, s))
```

#### 2. filter
filter(function, iterable)，和 map 用法类似，但用于过滤序列，保留 function 中返回 true 的元素

#### 3. sorted
sorted(iterable[, cmp[, key[, reverse]]])

通常规定 x < y 返回 -1； x==y 返回 0； x > y 返回 1。

- sort() 应用在 list 上，直接对已有的 list 进行排序，无返回
- sorted() 可以对所有可迭代对象进行排序，返回的是新 list

```python
num = [[5,4], [1,6] ,...]
nums = sorted(nums, key=lambda x: (-x[0], x[1])) # 按照第一个元素降序、第二个元素升序规则排序。
```

### lambda
python 中用于创建匿名函数，允许在一行代码中创建一个函数并传递

lambda 一般可以用在 filter，map，reduce，sorted 等函数式编程服务中

- 优点： 代码简洁，适合完成某项简单的功能，且这项功能只在此处用到； 不增加额外变量，可以立刻传递，自动返回结果。
- 缺点： 难理解，降低了可读性和性能。

### 偏函数
functools.partial 帮助创建偏函数，可以创建一个新函数，这个新函数可以固定住原函数的部分参数，使函数能用更少的参数调用，从而调用时更加简单。

## 异常处理
### 常见异常
http://www.runoob.com/python/python-exceptions.html
- BaseException 所有异常的基类
- OverflowError 数值运算超过最大限制
- IOError 输入/输出操作失败
- ImportError 导入模块/对象失败
- RuntimeError 一般运行时错误
- SyntaxError 语法错误

捕捉异常 try/except

try/except语句用来检测try语句块中的错误，从而让except语句捕获异常信息并处理。

如果你不想在异常发生时结束你的程序，只需在try里捕获它。

try-finally 语句无论是否发生异常都将执行最后的代码。

自定义异常： 异常应该是典型的继承自Exception类，通过直接或间接的方式

Python的异常也是class，所有的异常类型都继承自BaseException，

Python中的 raise 关键字用于引发一个异常， raise 关键字后面是抛出是一个通用的异常类型(Exception)，一般来说抛出的异常越详细越， 主动抛出

```python
try:
    fh = open("testfile", "w")
    fh.write("这是一个测试文件，用于测试异常!!")
except IOError:
    print "Error: 没有找到文件或读取文件失败"
else:
    print "内容写入文件成功"
    fh.close()
```


### python 编码
python2 默认编码是 ASCII， python3 默认编码是 Unicode。

下面是在 python2 中的！！！！
Python 有两种不同的字符串数据类型： str 和 unicode，都是 basestring 的子类。

对于同一个汉字 "好"， 用 str 表示和 unicode 表示是不同的。 用 str 表示时，对应的 UTF-8 编码是 "\xe5\xa5\xbd", 而 Unicode 表示对应的符号是 u'\u597d'，等同于 u'好'。

str 可以通过 decode 解码成 unicode 字符串。unicode 可以通过 encode 编码得到 UTF-8 编码格式的 str 类型的字符串。

> str --> decode --> unicode  
unicode --> encode --> str

### 面向对象编程
面向对象的三个特征：封装、继承、多态
#### 封装
封装，即隐藏对象的属性和实现细节，仅对外公开接口，控制在程序中属性的读和修改的访问级别。
- 封装数据： 为了保护隐私，明确区分内外数据，对外提供操作该数据的接口
- 封装方法： 目的是隔离复杂度

#### 继承
在定义一个类的时候可以从当前有的类中进行继承。

python 允许多继承，并且在子类中拥有父类所有的成员变量和方法，为了缓解代码中的冗余，子类在父类的基础上增加的成员变量可以如下修改。
```python
class Person(object):
    def __init__(self):
        self.name = name

class Child(Person):
    def __init__(self):
        Person.__init__(self, name, sex)
        self.mother = mother
```

#### 多态
当子类继承父类之后，成员方法既可以重写也可以不重写。当调用的时候只要保证新方法编写正确，不用管原来的代码
- 对扩展开放（Open for extension）：允许子类重写方法函数
- 对修改封闭（Closed for modification）：不重写，直接继承父类方法函数

鸭子类型： 一些类含有相同的方法，则这些类就互称为鸭子

#### 多继承
MixIn的目的就是给一个类增加多个功能，这样，在设计类的时候，我们优先考虑通过多重继承来组合多个MixIn的功能，而不是设计多层次的复杂的继承关系。

#####  super()
super() 用于解决多重继承时父类的查找问题，用于调用父类(超类)的一个方法。
在单继承中，直接使用父类类名 `parentClass.__init__(self)` 与 `super().__init__(self)` 一样，但使用 super() 可以避免父类的显式调用，如果父类名称修改，在子类中可以不进行修改。

**养成好习惯：super 的第一个参数应该是当前类**

super() 其实和父类没有实质性的关联
比如有一个菱形继承关系
```html
  Base
  /  \
 /    \
A      B
 \    /
  \  /
   C
```
使用 super()
```python
class Base(object):
    def __init__(self):
        print("enter Base")
        print("leave Base")

class A(Base):
    def __init__(self):
        print("enter A")
        super(A, self).__init__()
        print("leave A")

class B(Base):
    def __init__(self):
        print("enter B")
        super(B, self).__init__()
        print("leave B")

class C(A, B):
    def __init__(self):
        print("enter C")
        super(C, self).__init__()
        print("leave C")

C()
```

测试结果:
```html
enter C
enter A
enter B
enter Base
leave Base
leave B
leave A
leave C
```


对定义的每个类，python 会计算出一个方法解析顺序（Method Resolution Order, MRO）列表，表示类继承的顺序。
一个类的 MRO 列表就是合并所有父类的 MRO 列表，并遵循以下三条原则：
1. 子类永远在父类前面
2. 如果有多个父类，会根据它们在列表中的顺序被检查
3. 如果对下一个类存在两个合法的选择，选择第一个父类

#### 访问限制
private：私有变量以 `__` 开头，只有内部能够访问，可以给类增加 get、set 方法
特殊变量： `__xxx__`, 可以直接访问

#### __init__ 和 __new__ 区别

```
__init__是当实例对象创建完成后被调用的，然后设置对象属性的一些初始值。
__new__是在实例创建之前被调用的，因为它的任务就是创建实例然后返回该实例，是个静态方法。

即，__new__在__init__之前被调用，__new__的返回值（实例）将传递给__init__方法的第一个参数，然后__init__给这个实例设置一些参数。
```

```
1. __init__ 方法为初始化方法, __new__方法才是真正的构造函数，创建实例。
2. __new__方法默认返回实例对象供__init__方法、实例方法使用。
3. __init__ 方法为初始化方法，为类的实例提供一些属性或完成一些动作。
4. __new__是一个静态方法，而__init__是一个实例方法。
```

#### @staticmethod 和 @classmethod
#### self 和 cls 区别
一般来说，要使用某个类的方法，需要先实例化一个对象再调用方法。python 中有三种定义类方法：
1. 实例方法，self 通常用作实例方法的第一参数，用来传递当前类对象的实例，调用含有 self 参数的方法必须要通过实例调用。

2. @classmethod 类方法，第一个参数是表明自身类的 cls 参数，cls传递当前类对象， 那么就可以调用类的属性、方法，实例化对象等。 

3. @staticmethod 申明了一个静态函数，参数不用绑定 self 或 cls

使用 @staticmethod 或 @classmethod，就可以不需要实例化，直接类名.方法名()来调用，当然也可以通过实例调用。

```python
class A(object):
    @staticmethod
    def foo1(name): # 静态函数，这种方法与类有某种关系但不需要使用到实例或者类来参与
        print(name) # 既可以作为类的方法使用，也可以作为类的实例的方法使用

    def foo2(self, name):
        print(name)

    @classmethod
    def foo3(cls, name):
        print(name)

a = A()
a.foo1('xyy')
A.foo1('xyy')

a.foo2('xyy')
A.foo2('xyy') # 报错，TypeError: foo2() missing 1 required positional argument: 'name'

a.foo3('xyy')
A.foo3('xyy')
```

区分方法类型后可读性更好，对方法所依赖的变量环境一目了然。

适用场景：
1. @staticmethod
适用于定义不需要访问任何实例方法和属性，纯粹地通过传入参数并返回数据的功能性方法，可以节省实例化对象的开销成本。 
其实这种方法放在类外面的模块层作为一个函数存在也可以，而放在类中，就仅为这个类服务。比如更改环境变量或者修改其他类的属性。

2. @classmethod
作为工厂方法创建实例对象，如内置模块 datetime.date 类中就有大量使用类方法作为工厂方法，以此来创建 date 对象。

### 其他
#### 复数
python 中复数表示为 real + image j，实部和虚部都是浮点数，虚部后缀可以是 j 或 J，方法 conjugate 返回复数的共轭复数。 python 不支持复数比较大小
```python
a = 1 + 2j
a.real # 1.0
a.imag # 2.0
print(a.conjugate()) # 1-2j
```

3. 系统变量 ```__name__``` 显示当前模块执行过程中的名字，单独执行这个模块时就是 ```__main__```； 当在另个一个模块导入这个模块时，那 ```__name__``` 是这个模块的名字。

#### 解释型语言的特性： 非独立、效率低

#### python is 和 == 的区别
python 对象包括三个基本要素，身份标识 id、 数据类型 type、 值 value  

is 和 == 都是用于用于对象的比较判断，但判断内容不相同。
- is 同一性运算符，比较两个对象的 id 是否相同。 当 a 和 b 的值相同时，只有数值型和字符型，**并且在通用对象池中的情况下**， a is b 为 True； 而 tuple，list，dict，set 时，a is b 为 False。 对于浮点数，只有正浮点数值相等时 a is b 为 True

- == 比较两个对象的值是否相同

- id(object) 查看 object 所在的内存地址

备注： 事实上 python 为了优化速度，使用了小整数对象池，避免为整数频繁申请和销毁内存空间。只有数值在 [-5,256] 之间时同一个数值的 id 才会相等，超过范围就是 Fasle。同理，字符串对象也有类似的缓冲池。

#### random 用法
```python
import random

random.random() # 生成 0 到 1 的随机浮点数
random.randint(1,100) # 生成 1 到 100 之间的随机整数
random.uniform(1.1, 2.2) # 生成 1.1 到 2.2 之间的随机浮点数
random.choice('hello world') # 从序列中随机选择一个元素
random.randrange(1, 101, 2) # 生成从 1 到 101 间隔为 2 的整数，也就是 1-101 的偶数 

a = [1,2,3,4,5,6]
random.shuffle(a) # 打乱 a 中元素的顺序
```

#### find() 和 index() 区别
index() 和 find() 都是检测字符串中是否包含子字符串 str ，如果指定 beg（开始） 和 end（结束） 范围，则检查是否包含在指定范围内。

不同的是： 
1. 如果找不到，find() 返回 -1 ； 而 index() 会报一个异常 substring not found。
2. 列表有 index() 方法，没有 find() 方法
 
```python
str.index(str, beg=0, end=len(string))
str.find(str, beg=0, end=len(string))
list.index(n)
```

## python 魔术方法
python 中以两个下划线开头的方法，如 `__init__`、 `__new__`、 `__doc__` 等称为魔术方法，这在类或对象的某些事件发生后会自动执行。

https://segmentfault.com/a/1190000007256392

1. 构造和初始化
`__new__` 用来创建类并返回这个类的实例，`__init__` 将传入的参数来初始化实例。

`__del__` 在对象生命周期结束时会调用，也就是进行垃圾回收时，可以理解为“析构函数”


2. 属性访问控制
`__getattr__(self, name)`, `__setattr__(self, name, value)`, `__delattr__(self, name)`

## LEGB 规则
python 中变量的作用域可能是局部或全局，通过 LEGB 规则可以对变量名进行作用域解析，变量的搜索顺序为： Local -> Enclosed -> Global -> Built-in

- Local 可能是在一个函数或者类方法内部。
- Enclosed 可能是嵌套函数内，比如说 一个函数包裹在另一个函数内部。
- Global 全局变量，代表的是执行脚本自身的最高层次。
- Built-in 内置变量，是 Python 为自身保留的特殊名称。

如果某个 name:object 映射在局部(local)命名空间中没有找到，接下来就会在闭包作用域(enclosed)进行搜索，如果闭包作用域也没有找到，Python 就会到全局(global)命名空间中进行查找，最后会在内建(built-in)命名空间搜索（注：如果一个名称在所有命名空间中都没有找到，就会产生一个 NameError）




## 学习
all：如果all(x)参数x对象的所有元素不为0、''、False或者x为空对象，则返回True，否则返回False
any：如果any(x)参数x对象中，有一个元素部位0、''、False，则返回True，如果全部元素都为0、''、False，则返回 False
```python
assert all((key, secret)) or not any((key, secret)), "key and secret must both exists or both not exists"
```