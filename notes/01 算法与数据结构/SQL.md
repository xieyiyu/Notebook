# SQL

## 查询表
### 连接查询
>left join(左联接) 返回包括左表中的所有记录和右表中联结字段相等的记录  
right join(右联接) 返回包括右表中的所有记录和左表中联结字段相等的记录  
inner join(等值连接) 只返回两个表中联结字段相等的行

[Leetcode : 175. Combine Two Tables (Easy)](https://leetcode.com/problems/combine-two-tables/description/)
```sql
select FirstName, LastName, City, State 
from Person 
left join Address on Person.PersonId = Address.PersonId
```

### DATEDIFF日期差
[Leetcode : 197. Rising Temperature (Easy)](https://leetcode.com/problems/rising-temperature/description/)
>Given a Weather table, write a SQL query to find all dates' Ids with higher temperature compared to its previous (yesterday's) dates.

```sql
select w1.Id from Weather w1, Weather w2 
where w1.Temperature > w2.Temperature and datediff(w1.RecordDate, w2.RecordDate) = 1 
```

## 更新表
### 删除重复记录
[Leetcode : 196. Delete Duplicate Emails (Easy)](https://leetcode.com/problems/delete-duplicate-emails/description/)

需要删除重复的记录，保留其中一条，并且保留的是 Id 最小的记录。  
>注意：  
mysql 中不能在同一表中查询的数据作为同一表的更新数据,  
需要在 select 外边套一层，让数据库认为你不是查同一表的数据作为同一表的更新数据。

```sql
delete from Person where Id not in 
(select a.Id from 
 (select min(Id) as Id from Person group by Email) a)
```

### SQL-IF用法
当数据表中的某个字段只有两种情况时：  
IF(expr1,expr2,expr3)  
expr1是判断条件，expr2和expr3是符合expr1的自定义的返回结果。  
  
当数据表中的某个字段只有两种情况时：  
case when then用法  
```sql
case sex
    when 'm' then '男'
    when 'f' then '女’
    else '其他' end
```

[Leetcode : 627. Swap Salary (Easy)](https://leetcode.com/problems/swap-salary/description/)
>Given a table salary, such as the one below, that has m=male and f=female values. Swap all f and m values (i.e., change all f values to m and vice versa) with a single update query and no intermediate temp table.

```sql
update salary set sex = if(sex = 'm', 'f', 'm')
```

