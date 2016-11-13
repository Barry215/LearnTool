## SQL学习

### 常用的数据库

#### 关系型数据库

MySQL，Oracle，SqlServer

#### 非关系型数据库

Redis，MongoDB

#### 两者关系

[为什么要使用NoSQL](http://www.infoq.com/cn/news/2011/01/nosql-why)

[关系型数据库和非关系型数据库](https://my.oschina.net/u/1773689/blog/364548)



### 数据库的数据类型 

#### 时间类型区别

| 数据类型      | 含义                        |
| --------- | ------------------------- |
| date      | 日期 '2008-12-2'            |
| time      | 时间 '12:25:36'             |
| datetime  | 日期时间 '2008-12-2 22:06:44' |
| timestamp | 自动存储记录修改时间 格式同上           |

> DATETIM和TIMESTAMP类型所占的存储空间不同，前者8个字节，后者4个字节。
>
> 这样造成的后果是两者能表示的时间范围不同。
>
> 前者范围为1000-01-01 00:00:00 ~ 9999-12-31 23:59:59，后者范围为1970-01-01 08:00:01到2038-01-19 11:14:07。
>
> 所以可以看到TIMESTAMP支持的范围比DATATIME要小,容易出现超出的情况。

#### 更多资料

[mysql中timestamp,datetime,int类型的区别与优劣](http://blog.csdn.net/souldak/article/details/11737799)

[MySQL数据类型详解](http://shanks.leanote.com/post/mysql%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B#title-1)



### MySQL关键字

| 关键字                | 含义            |
| ------------------ | ------------- |
| NULL               | 数据列可包含NULL值   |
| NOT NULL           | 数据列不允许包含NULL值 |
| DEFAULT            | 默认值           |
| PRIMARY KEY        | 主键            |
| AUTO_INCREMENT     | 自动递增，适用于整数类型  |
| UNSIGNED           | 无符号           |
| CHARACTER SET name | 指定一个字符集       |



### 须知

- SQL 对大小写不敏感
- `''`单引号包裹用来表示是字符，不过大多数数据库也支持`""`双引号
- `*`表示所有表内字段

### 

### 表示例

#### user

| USER_ID | USER_NAME | CLASS_ID |
| :-----: | :-------: | :------: |
|    1    |   frank   | 16052502 |
|    2    |   barry   | 16031023 |
|    3    |   peter   | 16021314 |

#### course

| COURSE_ID | COURSE_NAME | CREDIT |
| :-------: | :---------: | :----: |
|     1     |     数据库     |   3    |
|     2     |    操作系统     |   4    |
|     3     |    数据结构     |   2    |

#### class

| CLASS_ID | CLASS_NAME | CLASS_SIZE |
| :------: | :--------: | :--------: |
| 16052502 |    电子2班    |     35     |
| 16031023 |    软工3班    |     41     |
| 16021314 |    会计4班    |     37     |

#### grade

| USER_ID | COURSE_ID | SCORE |
| :-----: | :-------: | :---: |
|    1    |     2     |  73   |
|    2    |     1     |  86   |
|    3    |     1     |  54   |
|    3    |     3     |  88   |
|    2    |     2     |  90   |
|    1    |     3     |  69   |
|    2    |     3     |  93   |



### 基础语法

#### SELECT

从某个表里筛选

> SELECT 列名称 FROM 表名称

```sql
select * from user
```

| USER_ID | USER_NAME | CLASS_ID |
| :-----: | :-------: | :------: |
|    1    |   frank   | 16052502 |
|    2    |   barry   | 16031023 |
|    3    |   peter   | 16021314 |

```sql
select user_id,user_name from user
```

| USER_ID | USER_NAME |
| :-----: | :-------: |
|    1    |   frank   |
|    2    |   barry   |
|    3    |   peter   |

#### SELECT DISTINCT

把返回结果中重复的值去掉

> SELECT DISTINCT 列名称 FROM 表名称

```sql
select user_id from grade
```

| USER_ID |
| :-----: |
|    1    |
|    2    |
|    3    |
|    3    |
|    2    |
|    1    |
|    2    |

```sql
select distinct user_id from grade
```

| USER_ID |
| :-----: |
|    1    |
|    2    |
|    3    |

#### WHERE

增加筛选的条件

> SELECT 列名称 FROM 表名称 WHERE 列 运算符 值

| 运算符                     | 描述                   |
| ----------------------- | -------------------- |
| =                       | 等于                   |
| <>                      | 不等于                  |
| >                       | 大于                   |
| <                       | 小于                   |
| >=                      | 大于等于                 |
| <=                      | 小于等于                 |
| BETWEEN..AND..          | 在某个范围内  (字母顺序或数字顺序)  |
| NOT BETWEEN..AND..      | 不在某个范围内  (字母顺序或数字顺序) |
| LIKE '%..%'             | 以某种模式模糊匹配（字符串）       |
| NOT LIKE '%..%'         | 除了模糊匹配的以外的（字符串）      |
| IN ( .. , .. , .. )     | 在列表里                 |
| NOT IN ( .. , .. , .. ) | 不在列表里                |

```sql
select user_id from user where user_name = 'frank'
```

| USER_ID |
| :-----: |
|    1    |

```sql
select user_id,user_name from user where user_name like '%r%'
```

| USER_ID | USER_NAME |
| :-----: | :-------: |
|    1    |   frank   |
|    2    |   barry   |
|    3    |   peter   |

```sql
select user_id from user where user_name in ('frank','barry')
```

| USER_ID |
| :-----: |
|    1    |
|    2    |

#### AND&OR

AND 和 OR 可在 WHERE 子语句中把两个或多个条件结合起来

```sql
select score from grade where course_id = 2 and user_id = 2
```

| SCORE |
| :---: |
|  90   |

```sql
select score from grade where course_id = 2 and (user_id = 1 or user_id = 2)
```

| SCORE |
| :---: |
|  73   |
|  90   |

#### ORDER BY

用于根据指定的列对结果集进行排序，**默认是升序**，字母顺序或数字顺序

|  顺序  |  符号  |
| :--: | :--: |
|  升序  | ASC  |
|  降序  | DESC |

```sql
select score from grade order by score desc
```

| SCORE |
| :---: |
|  93   |
|  90   |
|  88   |
|  86   |
|  73   |
|  69   |
|  54   |

```sql
select user_name from user order by user_name
```

| USER_NAME |
| :-------: |
|   barry   |
|   frank   |
|   peter   |

```sql
select user_id,score from grade order by user_id desc , score asc
```

| USER_ID | SCORE |
| :-----: | :---: |
|    3    |  54   |
|    3    |  88   |
|    2    |  86   |
|    2    |  90   |
|    2    |  93   |
|    1    |  69   |
|    1    |  73   |

#### INSERT INTO

用于向表格中插入新的行

> INSERT INTO 表名称 VALUES (值1, 值2,....)
>
> INSERT INTO table_name (列1, 列2,...) VALUES (值1, 值2,....)

```sql
insert into user values (4,'tom',16063385);
select user_name from user
```

| USER_NAME |
| :-------: |
|   frank   |
|   barry   |
|   peter   |
|    tom    |

```sql
insert into user (user_id,user_name) values (5,'jerry');
select * from user
```

| USER_ID | USER_NAME | CLASS_ID |
| :-----: | :-------: | :------: |
|    1    |   frank   | 16052502 |
|    2    |   barry   | 16031023 |
|    3    |   peter   | 16021314 |
|    4    |    tom    | 16063385 |
|    5    |   jerry   |          |

#### UPDATE

用于修改表中的数据

> UPDATE 表名称 SET 列名称 = 新值 WHERE 列名称 = 某值

```sql
update grade set score = 100 where user_id = 1 and course_id = 3;
select user_id,course_id,score from grade where user_id = 1
```

| USER_ID | COURSE_ID | SCORE |
| :-----: | :-------: | :---: |
|    1    |     2     |  73   |
|    1    |     3     |  100  |

```sql
update grade set course_id = 1,score = 99 where user_id = 1 and course_id = 2;
select user_id,course_id,score from grade where user_id = 1
```

| USER_ID | COURSE_ID | SCORE |
| :-----: | :-------: | :---: |
|    1    |     1     |  99   |
|    1    |     3     |  100  |

#### DELETE

用于删除表中的行

> DELETE FROM 表名称 WHERE 列名称 = 值
>
> DELETE FROM table_name  删除表内所有的行
>
> DELETE * FROM table_name  删除表内所有的行

```sql
delete from user where user_name = 'peter';
select user_id,user_name from user
```

| USER_ID | USER_NAME |
| :-----: | :-------: |
|    1    |   frank   |
|    2    |   barry   |



### 进阶语法

#### LIMIT

用于规定要返回的记录的数目

> SELECT column_name(s)
> FROM table_name
> LIMIT number

```sql
select user_name from user limit 2
```

| USER_NAME |
| :-------: |
|   frank   |
|   barry   |

#### LIKE

用于在 WHERE 子句中搜索列中的指定模式

> SELECT column_name(s)
> FROM table_name
> WHERE column_name LIKE pattern

提示："%" 可用于定义通配符（模式中缺少的字母）。

```sql
select user_id,user_name from user like '%r'   --结尾是r
```

| USER_ID | USER_NAME |
| :-----: | :-------: |
|    3    |   peter   |

```sql
select user_id,user_name from user not like 'f%'  --开头不是f
```

| USER_ID | USER_NAME |
| :-----: | :-------: |
|    2    |   barry   |
|    3    |   peter   |

#### 通配符

在搜索数据库中的数据时，SQL 通配符可以替代一个或多个字符。

SQL 通配符必须与 LIKE 运算符一起使用。

| 通配符                      | 描述            |
| ------------------------ | ------------- |
| %                        | 替代一个或多个字符     |
| _                        | 仅替代一个字符       |
| [charlist]               | 字符列中的任何单一字符   |
| [^charlist]或者[!charlist] | 不在字符列中的任何单一字符 |

```sql
select user_name from user like '[fb]%'
```

| USER_NAME |
| :-------: |
|   frank   |
|   barry   |

#### AS别名

为列名称和表名称指定别名

表的别名

> SELECT column_name(s)
> FROM table_name
> AS alias_name

列的别名

> SELECT column_name AS alias_name
> FROM table_name

```sql
select user_id, user_name as name from user where name = 'frank'
```

| USER_ID | NAME  |
| :-----: | :---: |
|    1    | frank |

#### 连接查询

之前都是在一个表里进行查询，当查询涉及两个表以上时，就叫连接查询

```sql
select user.user_name,course.course_name from user,course
```

| USER_NAME | COURSE_NAME |
| :-------: | :---------: |
|   frank   |     数据库     |
|   frank   |    操作系统     |
|   frank   |    数据结构     |
|   barry   |     数据库     |
|   barry   |    操作系统     |
|   barry   |    数据结构     |
|   peter   |     数据库     |
|   peter   |    操作系统     |
|   peter   |    数据结构     |

```sql
select user.user_name,class.class_name from user,class where user.class_id = class.class_id
```

| USER_NAME | CLASS_NAME |
| :-------: | :--------: |
|   frank   |    电子2班    |
|   barry   |    软工3班    |
|   peter   |    会计4班    |

#### JOIN

专门用于查询两张及两张表以上的数据

##### INNER JOIN

两张表里都有匹配的话，就返回那一行

> SELECT column_name(s)
> FROM table_name1
> INNER JOIN table_name2 
> ON table_name1.column_name=table_name2.column_name

```sql
select user.user_name,grade.score from user inner join grade on user.user_id = grade.user_id
```

| USER_NAME | SCORE |
| :-------: | :---: |
|   frank   |  73   |
|   frank   |  69   |
|   barry   |  86   |
|   barry   |  90   |
|   barry   |  93   |
|   peter   |  54   |
|   peter   |  88   |

##### LEFT JOIN

LEFT JOIN 关键字会从左表那里返回所有的行，即使在右表中没有匹配的行

这里的左表就是指下面的table_name1，右表指的是下面的table_name2

> SELECT column_name(s)
> FROM table_name1
> LEFT JOIN table_name2 
> ON table_name1.column_name=table_name2.column_name

```sql
insert into user(user_id,user_name) values(4,'shell');
select user.user_name,class.class_name from user 
left join class on user.class_id = class.class_id
```

| USER_NAME | CLASS_NAME |
| :-------: | :--------: |
|   peter   |    会计4班    |
|   barry   |    软工3班    |
|   frank   |    电子2班    |
|   shell   |            |

##### RIGHT JOIN

RIGHT JOIN 关键字会右表那里返回所有的行，即使在左表中没有匹配的行。

这里的左表就是指下面的table_name1，右表指的是下面的table_name2

> SELECT column_name(s)
> FROM table_name1
> RIGHT JOIN table_name2 
> ON table_name1.column_name=table_name2.column_name

```sql
insert into class values (16090134,'新建班级',50);
select user.user_name,class.class_name from user 
right join class on user.class_id = class.class_id
```

| USER_NAME | CLASS_NAME |
| :-------: | :--------: |
|   frank   |    电子2班    |
|   barry   |    软工3班    |
|   peter   |    会计4班    |
|           |    新建班级    |

##### FULL JOIN

只要其中某个表存在匹配，就会返回行

> SELECT column_name(s)
> FROM table_name1
> FULL JOIN table_name2 
> ON table_name1.column_name=table_name2.column_name

```sql
select user.user_name,class.class_name from user
full join class on user.class_id = class.class_id
```

| USR_NAME | CLASS_NAME |
| :------: | :--------: |
|  frank   |    电子2班    |
|  barry   |    软工3班    |
|  peter   |    会计4班    |
|  shell   |            |
|          |    新建班级    |

#### 子查询

一个select语句中嵌套另一个select语句

[MySQL子查询](http://justcode.ikeepstudying.com/2016/08/mysql%E5%85%A5%E9%97%A8-%E4%B9%9D-%E5%AD%90%E6%9F%A5%E8%AF%A2-subquery/)

##### 子查询返回的是一个结果

> SELECT column_name(s)
>
> FROM table_name
>
> WHERE column_name 运算符 (SELECT子查询)

```sql
select user_name from user 
where class_id = (select class_id from class where class_name = '软工3班')
```

| USER_NAME |
| :-------: |
|   barry   |

##### IN / NOT IN

当子查询返回的结果有多个的时候，判断是不是在子查询的结果里

> SELECT column_name(s)
>
> FROM table_name
>
> WHERE column_name IN (SELECT子查询)

```sql
select user_name from user where user_id in (select user_id from grade where score > 80)
```

| USER_NAME |
| :-------: |
|   barry   |
|   peter   |

##### EXISTS / NOT EXISTS

判断子查询的结果存不存在

> SELECT column_name(s)
>
> FROM table_name
>
> WHER EXISTS (SELECT子查询)

```sql
select user_name from user 
where exists (select 1 from grade where user.user_id = grade.user_id and grade.score > 80)
```

| USER_NAME |
| :-------: |
|   barry   |
|   peter   |

##### ANY / SOME

当子查询返回的结果有多个的时候，表示任何的意思，ANY和SOME的结果一样，如where n > any (1,2) 等同 where n > 1 or n > 2, n>1或n>2都行

> SELECT column_name(s)
>
> FROM table_name
>
> WHERE column_name 运算符 ANY (SELECT子查询)

```sql
select user_name from user where class_id =  
any (select class_id from class where class_name = '软工3班' and class_name = '会计4班')
```

| USER_NAME |
| :-------: |
|   barry   |
|   peter   |

##### ALL

当子查询返回的结果有多个的时候，表示所有的意思，如where n > all (1,2) 等同 where n > 1 and n > 2, 必须满足n > 1 和 n > 2

> SELECT column_name(s)
>
> FROM table_name
>
> WHERE column_name 运算符 ALL (SELECT子查询)

```sql
select score from grade where score > all (select score from grade where user_id = 3)
```

| SCORE |
| :---: |
|  90   |
|  93   |

#### 函数

##### AVG()

求该列的平均值

> SELECT AVG(column_name) FROM table_name

```sql
select avg(score) as avg_score from grade
```

| AVG_SCORE |
| :-------: |
|    79     |

```sql
select user_name from user where user_id 
in (select user_id from grade where score > (select avg(score) from grade))
```

| USER_NAME |
| :-------: |
|   barry   |
|   peter   |

##### COUNT()

返回匹配指定条件的行数

> SELECT COUNT(column_name) FROM table_name

```sql
select count(user_id) as user_sum from grade
```

| USER_SUM |
| :------: |
|    7     |

```sql
select count(distinct user_id) as user_sum from grade
```

| USER_SUM |
| :------: |
|    3     |

##### MAX()

返回一列中的最大值

> SELECT MAX(column_name) FROM table_name

```sql
select max(score) from grade
```

| MAX(SCORE) |
| :--------: |
|     93     |

##### MIN()

返回一列中的最小值

> SELECT MIN(column_name) FROM table_name

```sql
select min(score) from grade
```

| MIN(SCORE) |
| :--------: |
|     54     |

##### SUM()

返回数值列的总数

> SELECT SUM(column_name) FROM table_name

```sql
select sum(score) from grade
```

| SUM(SCORE) |
| :--------: |
|    553     |

#### GROUP BY

根据一个或多个列对结果集进行分组

> SELECT column_name, aggregate_function(column_name)
> FROM table_name
> WHERE column_name operator value
> GROUP BY column_name

```sql
select user_id,avg(score) as avg from grade group by user_id
```

| USER_ID |  AVG   |
| :-----: | :----: |
|    1    | 71.000 |
|    2    | 89.667 |
|    3    | 71.000 |

```sql
select user_id,course_id,sum(score) from grade group by user_id,course_id
```

| USER_ID | COURSE_ID | SUM(SCORE) |
| :-----: | :-------: | :--------: |
|    1    |     2     |     73     |
|    1    |     3     |     69     |
|    2    |     1     |     86     |
|    2    |     2     |     90     |
|    2    |     3     |     93     |
|    3    |     1     |     54     |
|    3    |     3     |     88     |

#### HAVING

和where类似，不过筛选条件可以有函数

> SELECT column_name, aggregate_function(column_name)
> FROM table_name
> WHERE column_name operator value
> GROUP BY column_name
> HAVING aggregate_function(column_name) operator value

```sql
select user_id,avg(score) from grade where user_id > 1
group by user_id
having avg(score) > 70
```

| USER_ID | AVG(SCORE) |
| :-----: | :--------: |
|    2    |   89.667   |
|    3    |   71.000   |