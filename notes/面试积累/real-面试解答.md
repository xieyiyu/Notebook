### 20181215 字节跳动一面 50分钟 效率工程团队 后端
#### 1. 找出数组中第 k 大的数，Kth Largest 
其实相当于 求数组中最大的前 K 个数，topK 问题

应该提出疑问：是否可以改变输入的数组？

可以改变输入数组：  
思路： 以第一个数为基准，用一次快速排序找到他的正确位置，下标为 mid，则 mid 左边的数小于等于基数，mid 右边的数大于等于基数，可以知道 nums[mid] 是第 len(nums)-mid 大的数，有无重复数字都可以这样做  
平均的时间复杂度为 O(nlogn)， 最好的时候一次 O(n)，最差的时候 ？？？
```python
def topk(nums, k):
    n = len(nums)
    if k > n or k <= 0:
        return None
    left, right = 0, n-1
    while left <= right:
        mid = quick_sort(nums, left, right)
        if mid == n-k:
            return nums[mid]
        elif mid > n-k:
            right = mid - 1
        else:
            left = mid + 1

def quick_sort(nums, left, right):
    key = nums[left]
    while left < right:
        while left < right and nums[right] >= key:
            right -= 1
        nums[left] = nums[right]
        while left < right and nums[left] <= key:
            left += 1
        nums[right] = nums[left]
    nums[left] = key
    return left
```

如果需要返回最大的前 K 个数，需要按照从大到小的顺序排列，知道了最大的第 K 个数的下标后，返回其左边的数组即可。
  
若直接排序，则时间复杂度为 O(nlogn)
用最大堆可以将时间复杂度降到 O(nlogk), 适合处理海量数据
```python

```

#### 2. 上述问题用一次堆排序的时间复杂度，快排加二分实现的时间复杂度
一次堆排序时间复杂度 O(logn)，总的O(nlogn)

#### 3. python 实现多并发用的进程还是线程，进程和线程的区别

提问： 是使用 CPU 密集型还是 IO 密集型？

对于 python， 若为 CPU 密集型应用多进程模型，需要大量的计算；  
若为 IO 密集型应用多线程模型，需要数据的读取写入、网络 IO 数据传输。  

进程和线程的区别：  
1. 根本区别：进程是资源分配的基本单位，线程是程序执行的最小单位
2. 开销方面：每个进程有独立的代码和数据空间，每启动一个进程，系统会为他分配地址空间，进程间的切换有较大开销；同一类线程共享代码和数据空间，切换和创建的开销较小
3. 线程通信更加方便，同一进程下的线程共享全局变量、静态变量等数据；而进程需要以通信方式(IPC)进行
4. 由于进程有自己独立的地址空间，因此多进程程序更加健壮；而多线程程序有一个线程挂掉，全部线程都会挂掉

#### 4. tcp 和 udp 的区别，传输过程有什么不同，tcp的数据能够一次接收吗
tcp 和 udp 的区别：  
1. TCP 发送数据前需要建立连接； UDP 不需要
2. TCP 更可靠、稳定，但是效率较低，有延时，占用系统资源高； UDP 传输速度快，但不可靠、不稳定，可能丢包
3. 对网络通信质量有要求，数据准确时用 TCP，如浏览器、邮箱等； 不高、要求快用 UDP，如 QQ语音、视频
4. **本质区别： TCP 面向字节流，UDP 面向报文**  
TCP 通过字节流传输，有窗口大小限制，太长的话会被拆分进行发送
UDP 通过报文传输，无论交给 UDP 多长的报文都会一次性发送，会保留报文的边界，不合并不拆分

传输过程有什么不同，tcp的数据能够一次接收吗？？？不明白是什么？？？

#### 5. 数据库怎么判断一个字段是否需要建索引，索引用的什么数据结构
- 较频繁的作为查询条件的字段应该创建索引
- 唯一性太差的字段不适合单独创建索引，即使频繁作为查询条件
- 更新非常频繁的字段不适合创建索引
索引的数据结构：B+树、B-树、通信R-树、散列  
大部分数据库系统及文件系统都采用 B-树 或 B+树 作为索引结构，B-树索引实现是一个专门为范围查询设计的，散列实现对直接查询方式能提供最优性能，但对一定范围的查找却效率低下。

#### 6. 什么是事务，事务出错的如何回滚，保证正确
事务: 数据库运行的逻辑工作单位，是用户定义的一组操作序列，要么完全执行，要么完全不执行。  
ACID：原子性、一致性、隔离性、持续性

#### 7. 栈和堆在程序上的区别
**堆栈空间分配：** 
- 栈区 stack： 由编译器自动分配释放，存放函数的参数值、局部变量的值等，操作方式类似数据结构中的栈 
- 堆区 heap： 一般由程序员分配释放，若程序员不释放，程序结束时可能由 OS 回收。不是数据结构中的堆，分配方式类似于链表

**堆栈缓存方式：**
- 栈使用一级缓存，通常是被调用时处于存储空间中，调用完立即释放
- 堆使用二级缓存，生命周期由虚拟机的垃圾回收算法来决定，因此调用速度更低一些

void f() { int* p=new int[5]; }   
new：分配了一块堆内存
指针p：分配一块栈内存  
因此，上述为在栈内存中存放一个指向一块堆内存的指针 p。 程序先确定在堆中分配内存的大小，然后调用 operator new 分配内存，然后返回这块内存的首地址，放入栈中。

#### 8. python 的 is 和 == 的区别
python 对象包括三个基本要素，身份标识 id、 数据类型 type、 值 value  
is 和 == 都是用于用于对象的比较判断，但判断内容不相同。
- is 同一性运算符，比较两个对象的 id 是否相同。 当 a 和 b 的值相同时，只有数值型和字符型，**并且在通用对象池中的情况下**， a is b 为 True； 而 tuple，list，dict，set 时，a is b 为 False。 对于浮点数，只有正浮点数值相等时 a is b 为 True
- == 比较两个对象的值是否相同
- id(object) 查看 object 所在的内存地址

备注： 事实上 python 为了优化速度，使用了小整数对象池，避免为整数频繁申请和销毁内存空间。只有数值在 [-5,256] 之间时同一个数值的 id 才会相等，超过范围就是 Fasle。同理，字符串对象也有类似的缓冲池。

#### 9. python 中正则的 search 和 match 区别，正则怎么实现过程如何
match() 在 string 的开始位置匹配，如果不匹配，返回 None，只有在 0 位置匹配成功才有返回  
search() 扫描整个 string 查找匹配，全部没有返回 None

#### 10. 一个很大的文本，比如log数据，以行存储，如何快速计算一个字段的平均值


### 20181220 金山云 测试开发 20分钟
#### 1. 简历上的 appium+python 自动化测试，具体讲一下做了什么？ 比如“滑动”功能怎么实现
#### 2. 有没有什么难点？遇到了什么问题？怎么解决的？ 
#### 3. 性能测试做了什么? 你说的那些不算是性能测试吧？

#### 4. python 多进程怎么实现的？
multiprocessing 中的 Process 类，代表进程对象
用进程池 Pool 的方式批量创建子进程，Pool 的默认大小是 CPU 的核数
对 Pool 对象调用 join() 方法会等待所有子进程执行完毕，调用 join() 之前必须先调用 close()，调用 close() 之后就不能继续添加新的 Process 了。
```python
pool_size = multiprocessing.cpu_count()*2
pool = multiprocessing.Pool(processes = 2)
    pool.apply_async(sparse_matrix, (filename, allword, matrix_file, )) # apply_async 是异步非阻塞的
pool.close()
pool.join()
```

#### 5. linux 平时用过一些什么命令？ 查看 mysql 进程
ps aux | grep mysql

#### 6. 文件很大的话如何处理？有没有遇到什么瓶颈？
1. 在 linux 下用 awk 命令
2. 读取大文件： 用 with open, 在打开文件的过程中，不会一次性读取全部文件，而是每次读取一行的方式，类似 buffer 机制
```python
with open(filename) as f:
    for line in f
```
3. 处理大文件：如果可以去重的话，尽量用 set 和 dic，不用 list（查询速度慢）
4. 用一些工具进行文件切割

#### 7. 数据库，学生(学号、课程号、成绩)，查询全部学科成绩在80分以上的学生信息
select sno from student where sno not in (select sno from student where grad <= 80)


### 20181220 好未来 python 开发 45min
实际上应该是和测试相关的，测试工具的开发
1. 描述一下实习经历，测试，重点讲一下自动化测试，用到了 python 的哪些功能？

#### 2. python 用过哪些数据结构？ 哪些是可变的，哪些不可变
python 有六种标准数据类型  
- 可变：list、set、dict
- 不可变，变量所指向的内存地址处的值不可改变： number（int、float、bool、complex）、 string、 tuple

#### 3. 直接参数传递和引用传递有什么区别？ 类里面的变量是用的什么传递？
值传递： 传的是实参变量的值，形参是作为一个局部变量，形参改变不会影响主调函数中的实参
引用传递： 传的是实参变量的地址，被调函数中的形参修改会改变主调函数中的实参

python 中的“传对象引用”的方式，对于不可变对象相当于是值传递，可变对象相当于是引用传递。

#### 4. python有什么比较大的优势，python 用过哪些开源包？
优雅、简洁、易懂，开发效率高、开源库丰富，可移植性、可扩展性、可嵌入性。  
自然语言处理jieba、 爬虫beautifulsoup、深度学习tensorflow、numpy

#### 5. 多进程与多线程的区别？ 多线程里面：IO密集型任务，与资源的共享有啥关系吗？ 什么是僵尸进程？
僵尸进程： 子进程退出后，父进程没有调用 wait/waitpid 来获取子进程的状态信息，那子进程的进程描述符就仍让在系统中，这就是僵尸进程。

#### 6. 除了 python 之外，还擅长什么？

#### 7. linux 熟悉程度？ 写命令：查看端口号，查看进程，统计一个字符串出现的次数， 复制文件
netstat -anp | grep 80
ps aux | grep xxx
grep -c xxx filedir
cp sourcedir destdir

#### 8. 编程： 给一个字符串，找出次数最多的字符和次数

#### 9. 微信的输入框和发送界面，如何设计测试用例？
需要考虑通信问题，网络问题，对方是否能够接收

### 20181224 百度 测开-AI产品 27min
主要是智能客服类产品，银行的机器人客服、在线客服
1. 自我介绍
2. 命名实体识别项目，做过哪些测试？指标如何设计的？有没有误召回率？

#### 3. 讲一下快速排序的思路
以第一个数为基准 key，通过一次快速排序找到 key 的位置，左边的元素 <= key，右边的元素 >= key
一次快排的过程： 用两个指针 left 和 right 记录下左右的位置，key 与 right 指向的元素比较，如果 key <= nums[right]，那么 right-1，否则将 right 指向的元素放在 left 指向的位置；然后再拿 key 和 left 指向的元素比较。
左右两边重复快排过程，所有的子序列长度都为 1 后，则排好序。

#### 4. lambda 函数有什么好处？
代码简洁，适合完成某项简单的工作；不增加额外变量。

#### 5. 深拷贝和浅拷贝的区别？
浅拷贝创建一个具有相同类型，相同值但 id 不同的新对象。
注意：对 copy 后的新对象的元素进行修改不会影响原对象，但是若对新对象或原对象中的子对象（即["a", "b"]）进行修改，那么新对象和原对象会同步改变，即对子对象只是引用。
 
深拷贝是完全拷贝，包含对象里面的子对象的拷贝，所以原始对象的改变不会造成深拷贝里任何子元素的改变。

#### 6. 数据库左连接和右连接区别？ 将一个表的姓名里包含xx的人的某一个字段修改为xx
update table set 字段='xxx' where name like '%xx%'

#### 7. mysql引擎是否有了解？
## InnoDB
是 MySQL 默认的事务型存储引擎，只有在需要它不支持的特性时，才考虑使用其它存储引擎。
实现了四个标准的隔离级别，默认级别是可重复读（REPEATABLE READ）。在可重复读隔离级别下，通过多版本并发控制（MVCC）+ 间隙锁（Next-Key Locking）防止幻影读。
主索引是聚簇索引，在索引中保存了数据，从而避免直接读取磁盘，因此对查询性能有很大的提升。
内部做了很多优化，包括从磁盘读取数据时采用的可预测性读、能够加快读操作并且自动创建的自适应哈希索引、能够加速插入操作的插入缓冲区等。
支持真正的在线热备份。其它存储引擎不支持在线热备份，要获取一致性视图需要停止对所有表的写入，而在读写混合场景中，停止写入可能也意味着停止读取。

## MyISAM
设计简单，数据以紧密格式存储。对于只读数据，或者表比较小、可以容忍修复操作，则依然可以使用它。
提供了大量的特性，包括压缩表、空间数据索引等。
不支持事务。
不支持行级锁，只能对整张表加锁，读取时会对需要读到的所有表加共享锁，写入时则对表加排它锁。但在表有读取操作的同时，也可以往表中插入新的记录，这被称为并发插入（CONCURRENT INSERT）。
可以手工或者自动执行检查和修复操作，但是和事务恢复以及崩溃恢复不同，可能导致一些数据丢失，而且修复操作是非常慢的。
如果指定了 DELAY_KEY_WRITE 选项，在每次修改执行完成时，不会立即将修改的索引数据写入磁盘，而是会写到内存中的键缓冲区，只有在清理键缓冲区或者关闭表的时候才会将对应的索引块写入磁盘。这种方式可以极大的提升写入性能，但是在数据库或者主机崩溃时会造成索引损坏，需要执行修复操作。

## 比较
- 事务：InnoDB 是事务型的，可以使用 Commit 和 Rollback 语句。
- 并发：MyISAM 只支持表级锁，而 InnoDB 还支持行级锁。
- 外键：InnoDB 支持外键。
- 备份：InnoDB 支持在线热备份。
- 崩溃恢复：MyISAM 崩溃后发生损坏的概率比 InnoDB 高很多，而且恢复的速度也更慢。
- 其它特性：MyISAM 支持压缩表和空间数据索引。

#### 8. linux 的 sed，awk，远程拷贝（从一个服务器到另一个服务器），是否知道与查看 cpu、io等的命令
远程拷贝 scp
top 可以查看 cpu 相关

#### 9. 实习主要做什么？介绍一下你做的自动化测试
#### 10. 做一个自动售货机的测试用例
先分为几大块再去细化你的测试用例

### 20181224 新浪微博 python，golang实习生 k8s 开发实习生 一面 25min
#### 1. 介绍最近的一个项目，平时字典是怎么维护的？
#### 2. python 异常处理，怎么定义一个异常，有哪些常见的异常
try except 模块
自定义异常类需要继承父类 Exception，需要重写父类的 __init__ 方法， 可以通过添加一个 err 属性来存放错误信息，方便在后续的异常处理中可以根据错误信息的不同来进行不同的处理。
```python
class myException(Exception):
    def __init__(self, err):
        Exception.__init__(self)
        self.err = err

try:
    raise myException('myerr') # 引发自己定义的异常，可以生成该异常类的一个实例，并抛出
except myException as e:
    print(e.err)
```

#### 3. python 断言
assert 断言语句用来声明某个条件是真的，其作用是测试一个条件(condition)是否成立，如果不成立，则抛出异常。
当assert语句失败的时候，会引发一AssertionError
assert 1 == 1 # True
assert 1 == 2 # 会抛出异常 AssertionError

assert 断言语句添加异常参数，来解释断言并更好的知道是哪里出了问题
assert expression [, arguments]

- 断言：是用来检查非法情况而不是错误情况的，用来帮开发者快速定位问题的位置。断言用于检查函数输入的合法性，要求输入满足一定的条件才能继续执行;
- 异常处理： 用于对程序发生异常情况的处理，增强程序的健壮性和容错性。

#### 4. python 追加列表， 替换字符， 分割字符串
替换字符： 
str.replace(old, new [,max]) max 为替换不超过 max 次；
正则：re.sub(pattern, repl, string) repl 为替换的字符串，也可以是一个函数

#### 5. python io 操作，文件输入输出
读取键盘输入： raw_input(), input()
文件操作： with open(filename, 'r') as fr: f.read()/readline()/readlines(), for i in fr
f.write
os 操作: os.rename(), os.remove(), os.mkdir, os.walk 等

#### 6. python 的数据结构
#### 7. python2 和 python3 的区别
- python3 不向下兼容
- print 语法不同，但 print() 也可以在 python2 中兼容
- python2 中有两种字符串类型 unicode字符串 和 非unicode字符串； python3 中只有一种 unicode 字符串
- python3 中的除法有两种，/ 整数相除是浮点数， // 得到整数； 而在 python2 的 / 得到整数
- python3 的异常处理用 as 作为关键词，且只有继承自 BaseException 的对象才能抛出； 2 是所有异常都可抛出
- 数据类型： python3 中去掉 long 类型，只有 int 一种整型； 新增 bytes 类型 by = b'china'; .encode() str->bytes; .decode() bytes->str

#### 8. python 函数式编程有了解吗
特点： 允许把函数本身作为参数传入另一个函数，还允许返回一个函数
高阶函数(map, reduce, filter, sorted), lambda, 装饰器, 偏函数

#### 9. python 获取类型 isinstance 和 type 区别
- type 一般用于检测基本(值)数据类型，number、 string、 boolean、 null、 undefined， 返回值类型是 string, 不认为子类是一种父类类型
- isinstance 检测引用(对象)类型，判断一个对象是否是一个已知的类型 object、 function、 array， 返回值类型是 bool，认为子类是一种父类类型
```python
type(a)
isinstance(a, int)
```

#### 10. 类和直接定义方法，平时用什么


#### 11. 给一个字符串 abcd，用递归方式实现反转
```python
def fun(s):
    if not s:
        return s
    return fun(s[1:]) + s[0]
```

#### 12. 大数据框架是否有了解？hadoop？
#### 13. linux grep、awk、sed 是否有了解

#### 14. sql 的内连接和外链接区别，排序的 sortby 和 orderby 的区别
sortby 和 orderby 是 Hive 中的
hive 是基于 hadoop 的数据仓库工具，可以将 sql 语句转化为 MapReduce 任务运行，适合数据仓库的统计分析。

- order by 会引发全局排序
- 使用 distribute 和 sort 进行分组排序, 是按组有序, 全局无序的, select * from table distribute by col1 sort by col2 desc;

#### 15. java 怎么进行内存管理
#### 16. shell 写脚本用过吗？
#### 17. 快速排序和堆排序的时间复杂度和实现区别？
#### 18. 机器学习的 lr、adaboost 等有了解吗

### 20181225 滴滴 测试开发 一面 65min
1. 挑一个项目介绍，遇到什么难点，如何解决， 用到了什么技术来完成，项目的来源是？项目意义，有什么应用
2. 讲一下实习经历，自动化测试框架怎么搭的
3. python 用过什么库？第三方的和内置的？说一下 os 里面你记得的几个方法
4. python 分割字符串， 字典遍历 key 和 value， 数组遍历后五个元素， 交换两个元素
5. python 的装饰器和生成器，怎么理解装饰器，怎么创建生成器，生成器与列表生成式的区别，得到生成器下一个元素，
6. python 多进程和多线程用过吗？ 多进程怎么用的？

#### 7. 数据库sql 查看表的结构，表与表之间的连接，数据库用过哪些， 非关系型和关系型数据库的区别，非关系型存储格式有哪些， 更新某表某字段， 分组查询
describe table_name 查看表结构； show tables 当前数据库的所有表名; show create table_name 查看创建表的语句

#### 8. python 怎么调用数据库？
Python 标准数据库接口为 Python DB-API，Python DB-API为开发人员提供了数据库应用编程接
python 的 mysql 驱动有两种：
mysql-connector-python：是MySQL官方的纯Python驱动；
MySQL-python：是封装了MySQL C驱动的Python驱动。

python3 连接 mysql 用到 pymysql 模块
```python
import pymysql
db = pymysql.connect("localhost","testuser","test123","TESTDB" ) # 打开数据库连接
cursor = db.cursor() # # 使用 cursor() 方法创建一个游标对象 cursor
cursor.execute("SELECT VERSION()") # 使用 execute()  方法执行 SQL 查询 
data = cursor.fetchone() # 使用 fetchone() 方法获取单条数据
db.close() # 关闭数据库连接
```

#### 9. linux 熟悉的命令有哪些，ls 显示详细信息， 查看磁盘的命令是？
查看磁盘： df -h 统计磁盘整体情况

10. 用过 shell 和 vim 吗？ 服务器要修改文件怎么做？
11. 从输入 URL 到浏览器显示页面发生了什么？
12. get 和 post 区别
13. 数据结构掌握的如何？ 讲一下快排的原理和时间复杂度，树的遍历有哪些，构造二叉树的话必须要知道那种遍历
#### 14. git 的流程，分支如何创建？ 产生冲突如何解决？ 还用过什么别的版本控制工具吗？
15. 测试 黑盒和白盒的区别
16. 操作系统的死锁是怎么产生的
17. 编程思路： 给定一个时间如 11.47，计算时针与分针的夹角,<=180 的
18. 学过哪些与计算机相关的课程？研究生主要是什么课程？为什么想做技术相关的
19. 平时都看什么技术博客或者论坛吗？
20. 让你去学习一门新的技术或框架，会怎么学？

### 20181225 滴滴 测试开发 一面 25min
滴滴语音，主要是云计算，做服务端测试和自动化测试
1. 外部字典是怎么获取？有没有进行维护和更新？怎么爬的 用的什么包，用的 request 里的什么方法，get 和 post 的区别
2. list 和 tuple 的区别， 字典怎么遍历所有的 key 和 value

#### 3. 迭代器和生成器


#### 4. python 面向对象，类怎么定义一个私有变量
在 Python 中可以通过在属性变量名前加上双下划线定义属性为私有属性。Python没有真正的私有变量。内部实现上，是将私有变量进行了转化，变成了 \_ClassName__variableName。
python默认的成员函数和成员变量都是公开的,没有像其他类似语言的public,private等关键字修饰.但是可以在变量前面加上两个下划线"\_",这样的话函数或变量就变成私有的.

通过在类中定义接口,实现私有变量的读取和修改

1、 \_xx 以单下划线开头的表示的是protected类型的变量。即保护类型只能允许其本身与子类进行访问。若内部变量标示，如： 当使用“from M import”时，不会将以一个下划线开头的对象引入 。

2、 \_\_xx 双下划线的表示的是私有类型的变量。只能允许这个类本身进行访问了，连子类也不可以用于命名一个类属性（类变量），调用时名字被改变（在类FooBar内部，\_\_boo变成\_FooBar\_\_boo,如self.\_FooBar\_\_boo）

3、 __xx__ 定义的是特列方法。用户控制的命名空间内的变量或是属性，如init , __import__ 或是file 。只有当文档有说明时使用，不要自己定义这类变量。 （就是说这些是python内部定义的变量名）

#### 5. sql 向表中添加一个字段
#### 6. linux 查看某个进程
#### 7. 有一个产品是水杯，销售之前如何测试？ 内部液体的温度、种类等