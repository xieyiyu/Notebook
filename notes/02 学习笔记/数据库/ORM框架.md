## ORM框架
ORM(Object Relational Mapping) 对象关系映射：一种为了解决面向对象与关系数据库存在的互不匹配的现象的技术。ORM 通过使用描述对象和数据库之间映射的元数据（映射文件信息），将程序中的对象自动持久化到关系数据库中。

优点：
1、操作简单，挺高开发效率。
2、数据访问更抽象，更轻便
3、支持面向对象封装
4、 ORM框架还有一个功能，它可以根据我们设计的类自动帮我们生成数据库中的表格，省去了我们自己建表的过程。
5、避免sql注入，比字符串拼接更安全

缺点：
1、执行性能低，自动化进行关系数据库的映射需要消耗系统性能
2、在处理多表联查、where条件复杂之类的查询时，ORM的语法会变得复杂
3、开发思维容易固定化
Java ORM框架：Hibernate，mybatits


## python sqlalchemy
1. 导入 sqlalchemy，并初始化 DBSession
```python
# 导入:
from sqlalchemy import Column, DateTime, Float, String, text, create_engine
from sqlalchemy.dialects.mysql import INTEGER
from sqlalchemy.orm import sessionmaker
from sqlalchemy.ext.declarative import declarative_base

# 创建对象的基类:
Base = declarative_base()
metadata = Base.metadata

# 定义User对象:
class User(Base):
    # 数据库中表的名字:
    __tablename__ = 'user'

    # 表的结构:
    id = Column(String(20), primary_key=True)
    name = Column(String(20))

# 初始化数据库连接:
engine = create_engine('mysql+mysqlconnector://root:password@localhost:3306/test')
# 创建DBSession类型:
DBSession = sessionmaker(bind=engine)
```

sqlalchemy 使用 `数据库类型+数据库驱动名称://用户名:口令@机器地址:端口号/数据库名` 字符串来表示连接信息

2. 获取session，添加一个 user 对象到数据库中，即 insert
```python
# 创建session对象:
session = DBSession()
# 创建新User对象:
new_user1 = User(id='1', name='Bob')
new_user2 = User(id='2', name='Tom')
# 添加到session:
session.add(new_user1) # 添加一行记录
session.add_all([new_user1, new_user2]) # 添加多个记录
# 提交即保存到数据库，对应insert操作
session.commit()
# 关闭session:
session.close()
```

3. 查询数据库
```python
# 创建Session:
session = DBSession()
# 创建Query查询，filter是where条件，最后调用one()返回唯一行，如果调用all()则返回所有行:
user = session.query(User).filter(User.id=='5').one()
# 打印类型和对象的name属性:
print('type:', type(user))
print('name:', user.name)
# 关闭Session:
session.close()
```

### Sqlalchemy model 文件自动生成
作用：根据数据库定义，自动生成每张表对应的 class 

1. 使用 pip 安装 sqlacodege
2. 安装后运行命令生成 models.py 文件
若数据库连接字符串是： mysql://root:root@127.0.0.1:3306/mydb
则使用命令：sqlacodegen mysql://root:root@127.0.0.1:3306/mydb > models.py 即可在当前目录生成models.py文件
查看了下生成的models.py文件，可以符合PEP8规范，可生成视图类，会根据有没有主键决定是不是meta table，可以生成外键，就目前的使用没有出现过问题。

3.如果是 python3 会报错 No module named 'MySQLdb'
需要安装 pymysql， 然后在 sqlacodegen 的__init__.py文件里加上以下代码，再次运行可以成功
```python
import pymysql
pymysql.install_as_MySQLdb()
```