### 函数式编程
#### 1. Lambda 实现一个a+b
```python
f = lambda a, b: a+b
f(1, 2)
```
lambda 优点：
代码简洁，适合完成某项简单的功能，且这项功能只在此处用到； 
不增加额外变量，可以立刻传递，自动返回结果。

### 文件操作
1. python 读写文件，写一个读文件并按行打印的代码，考虑关掉文件，考虑异常，如何捕捉异常并写代码
```python
try:
    with open('1.txt', 'r', encoding='utf-8') as fr:
        for line in fr:
            print(line)
        fr.close()
except Exception as e: # 可以指定抛出的异常类型 except IOError
    print(e)
```

2. 随机生成一个 1-100 之间的数字，并写入文件 
```python
import random

x = random.randint(1, 100)
print(x)
fw = open('1.txt', 'a+', encoding='utf-8') # 追加，文件不存在自动创建
fw.write(str(x)) # 写入的必须是 str 类型
fw.close()
```

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

### 数据结构相关
1. 将｛'a':1,'b':2｝转为[('a','b'),(1,2)]
```python
dict = {'a':1, 'b':2}
keys = tuple([key for key in dict])
vals = tuple([dict[k] for k in keys])
print([keys, vals])
```

### python定时任务
1. 循环 + time.sleep()
只能执行固定间隔时间的任务，如果是定时任务无法完成。 且 sleep 是阻塞函数，执行 sleep 的期间什么也不能做

2. threading.Timer()
Timer() 是非阻塞函数，定时器只能执行一次，如果需要重复执行，需要重新添加任务。

3. 调度模块 schedule
schedule 是一个第三方轻量级的任务调度模块，可以按照秒，分，小时，日期或者自定义事件执行时间。

4. APScheduler 框架：  是 Python 的一个定时任务框架，用于执行周期或者定时任务，
可以基于日期、时间间隔，及类似于 Linux 上的定时任务 crontab 类型的定时任务；
该该框架不仅可以添加、删除定时任务，还可以将任务存储到数据库中，实现任务的持久化，使用起来非常方便。

### 如何优化 python 代码
优化通常包含两方面的内容：减小代码的体积，提高代码的运行效率。
1. 改进算法，选择合适的数据结构： 比如频繁访问应该用 dict，求 list 的交并集等可以转为 set
2. 对循环的优化： 尽量减少循环过程中的计算量，有多重循环的尽量将内层的计算提到上一层
3. 对字符串优化：字符串连接的使用尽量使用 join() 而不是 +， 格式化 print 比连接更快
4. 用生成器表达式

#### 定位程序性能
使用 profile 进行性能分析，能够描述程序运行时候的性能，并提供各种统计帮助用户定位程序的性能瓶颈。
```python
import profile
def fun():
	xxx
profile.run("fun()")
```

#### python 性能优化工具
可以将关键 python 代码部分重写成 C 扩展模块，或者选用在性能上更为优化的解释器等，优化工具有 psyco，Pypy，Cython，Pyrex等

Cython 代码与 python 不同，必须先编译，编译一般需要经过两个阶段，将 pyx 文件编译为 .c 文件，再将 .c 文件编译为 .so 文件。

### 为什么 Python 不支持函数重载
在 JAVA 中：
重写 Override： 子类对父类的允许访问的方法的实现过程进行重新编写, 返回值和形参都不能改变。
重载 Overload： 在一个类里面，方法名字相同，而参数不同的函数。

函数重载主要是为了解决两个问题：可变参数类型、可变参数个数。
对于可变参数类型： python 可以接受任何类型的参数，如果函数的功能相同，那么不同的参数类型在 python 中很可能是相同的代码，不需要重载成两个函数。
对于可变参数个数： python 可以对缺少的参数设定为缺省参数

### python 与设计模式
#### 单例模式
单例模式： 确保某个类只有一个实例存在，保证了在程序的不同位置都可以且仅可以取到同一个对象实例：如果实例不存在，会创建一个实例；如果已存在就会返回这个实例。

特点： 只有一个实例、单例类的构造函数是私有的，自行创建类的实例、向整个系统公开这个实例接口

使用场景：
1. Python 的 logger 就是一个单例模式，用以日志记录
2. Windows 的资源管理器是一个单例模式
3. 线程池，数据库连接池等资源池一般也用单例模式
4. 网站计数器

为什么不用全局变量？
全局变量不能保证应用程序只有一个实例，且可能会有名称空间的干扰，如果有重名的可能会被覆盖，不能继承

用 `__new__` 方法实现单例模式：

```python
class Singleton(object):
    _instance = None
    def __new__(cls, *args, **kwargs):
        if cls._instance is None:
            cls._instance = object.__new__(cls)
        return cls._instance
    def __init__(self):
        pass

s1 = Singleton()
s2 = Singleton()
print(id(s1) == id(s2)) # True,说明是同一个实例
```

但是当有多个线程同时去初始化对象时，就很可能同时判断 `_instance is None`，无法实现单例。这种情况下，需要用同步锁来解决问题。
```python
from synchronize import make_synchronized
class Singleton(object):
    instance = None
    @make_synchronized # 用装饰器
    def __new__(cls, *args, **kwargs):
    	pass
```