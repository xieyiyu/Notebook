### 函数式编程
#### 1. Lambda 实现一个a+b
```python
f = lambda a, b: a+b
f(1, 2)
```
lambda 优点：

### 文件操作
1. python 读写文件，写一个读文件并按行打印的代码，考虑关掉文件，考虑异常，如何捕捉异常并写代码

2. 写随机生成一个 1-100 之间的数字，并写入文件 

### python 的 is 和 == 的区别
python 对象包括三个基本要素，身份标识 id、 数据类型 type、 值 value  
is 和 == 都是用于用于对象的比较判断，但判断内容不相同。
- is 同一性运算符，比较两个对象的 id 是否相同。 当 a 和 b 的值相同时，只有数值型和字符型，**并且在通用对象池中的情况下**， a is b 为 True； 而 tuple，list，dict，set 时，a is b 为 False。 对于浮点数，只有正浮点数值相等时 a is b 为 True
- == 比较两个对象的值是否相同
- id(object) 查看 object 所在的内存地址

备注： 事实上 python 为了优化速度，使用了小整数对象池，避免为整数频繁申请和销毁内存空间。只有数值在 [-5,256] 之间时同一个数值的 id 才会相等，超过范围就是 Fasle。同理，字符串对象也有类似的缓冲池。

### 正则表达式
#### 1.python 中正则的 search 和 match 区别
match() 在 string 的开始位置匹配，如果不匹配，返回 None，只有在 0 位置匹配成功才有返回  
search() 扫描整个 string 查找匹配，全部没有返回 None

### python2 和 python3 区别