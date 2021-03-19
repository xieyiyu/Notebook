## mybatis 简介
MyBatis是一个优秀的持久层框架，它对jdbc的操作数据库的过程进行封装，使开发者只需要关注 SQL 本身，而不需要花费精力去处理例如注册驱动、创建connection、创建statement、手动设置参数、结果集检索等jdbc繁杂的过程代码。

Mybatis通过xml或注解的方式将要执行的statement配置起来，并通过java对象和statement中的sql进行映射生成最终执行的sql语句，最后由mybatis框架执行sql并将结果映射成java对象并返回。

## 配置过程
1. 在pom.xml文件中引入需要jar的依赖

2. 创建model类，字段与数据库表中的一致，如 StudentModel 对应数据库中的 student 表

3. 创建Mapper文件
在 resources/mapper 目录下创建 student 表对应的 mapper 文件 studentMapper.xml。在该文件中写 sql 语句

4. 创建MyBatis的配置文件
在 resources/mapper 目录下创建 MyBatis 框架的配置文件 sqlMapConfig.xml。在该文件中配置数据库参数，配置 mapper 文件，声明 Model 类对应的别名

## mapper
mapper 文件是 MyBatis 的核心文件，操作数据库的 sql 语句都写在该文件中。一般情况下一个 Mapper 文件对应一个数据库表
