# JerryFirst
自己的第一个仓库
## Mysql的学习

JavaEE：企业级Java开发  Web

前端（页面：展示，数据！）

后台 （连接点：连接数据库JDBC，链接前端（控制，控制视图跳转，和给前端传送数据	））

数据库（存数据，TXT，Excel，Word）

> 只会写代码，学好数据库，基本混饭吃
>
> 操作系统，数据结构与算法！当一个不错的程序员！
>
> 离散数学，数字电路，体系结构，编译原理。+实战经验，  高级程序员



## 1.1、为什么学习数据库

## 1.2、什么是数据库

数据库（DB，DataBa）

概念：数据仓库，软件，安装在操作系统（window，Linux，mac、...）之上

作用：存储数据



## 1.3、数据库分类

**关系型数据库**：Excel

* mysql，Oracle,Sql Server,DB2,SQLlIte
* 通过表和表之间，行和列之间的关系进行数据的储存，  学员信息表，考勤表 ....



**非关系型数据库**：

* Redis,MongDB
* 非关系型数据库，对象储存，通过对象的自身的属性来决定。

## 1.7、连接数据库

```java
mysql -uroot -p123456   --连接数据库

update mysql.user set authentication_string=password('123456') where user='rppt' and Host =
'localhost';           --修改用户密码
flush privileges;      --刷新权限
    
---------------------------------------------
--  所有的语句都使用 ; 结尾
show databases;  --查看所有的数据库
    
mysql> use school                            --切换数据库 use 数据库名
Database changed

show tables;                                 --查看数据库中所有的表
describle student;                           --显示数据库中所有的表的信息

create database westos;                      --创建一个数据库

exit;	                                     --退出连接

--单行注释（SQL的本来的注释）
/*   （SQL的多行注释）
hello！
asdf
dfas
*/     
```





**数据库 xxx 语言**               CRUD增删查改！  CV程序员   API程序员  	CRUD程序员！	

DDL       定义

DML      操作

DQL      查询

DCL      控制







## 2、操作数据库

操作数据库>操作数据库中的表>操作数据库中表的数据

==mysql关键字不区分大小写==

## 2.1、操作数据库(了解)

1、创建数据库

```
create database [if not exists] westos
```

2、删除数据库

```
drop detabase [if exist] westos
```

3、使用数据库

```4
-- tab 键的上面，如果你的表名或者字段名是一个特殊字符，就需要带  ` `
use `school`
```

4、查看数据库

```sql
show databases  
--查看所有的数据库
```

对比:SQLyog的可视化操作





学习思路：

* 对照SQLlog可视化历史记录查看SQL
* 固定的语法或关键字必须强行记住！

## 2.2、数据库的列类型

> 数值

* tinyint          十分小的数据             1个字节
* smallint       较小的数据                2个字节
* mediumint   中等大小的数据        3个字节
* **int                 标准的整数                 4个字节**  常用的
* bigint            较大的数据                 8个字节
* float               浮点数                         4个字节
* double          浮点数                           8个字节（精度问题！）
* decimal         字符串形式的浮点数    金融计算的时候，一般使用decimal

>字符串

* char             字符串固定大小的            0~255
* **varchar       可变字符串                 0~65535    常用的变量**   string
* tinytext       微型文本                 2^8 - 1
* **text                文本串                      2^16 - 1   **      保存大文本 

>时间日期

java.util.Date



* date              YYYY-MM-DD       日期格式
* time              HH：mm : ss      时间格式
* **datetime      YYYY-MM-DD  HH：mm : ss    最常用的时间格式**
* **timestamp    时间戳，     1970.1.1到现在的毫秒数！ ** 也较为常用！
* year        年份

> null

* 没有值，未知
* ==注意，不要使用NULL进行运算，结果为NULL==





## 2.3、数据库的字段属性（重点 ）

==Unsigned==：

* 无符号的整数
* 声明了该列不能声明为负数



==zerofill：==

* 0填充的
* 不足位数，使用0来填充， int（3）  ，  5   ---  005



==自增：==

* 通常在理解为自增，自动在上一条记录的基础上 +1（默认）
* 通常用来设置唯一的主键~index，必须是整数类型



==非空==        NULL    not   nul

* 假设设置为  not  null ，如果	不给它赋值，就会报错！
* NULL，如果不填写值，默认就是null！



==默认：==

* 设置默认的值！
* sex，默认值 为 男，如果不指定该列的值，则会有默认的值！



## 2.4、创建数据库表

```sql
-- 目标 ： 创建一个school数据库
-- 创建学生表（列，字段）  使用SQL 创建
-- 学号int  登录密码varchar(20) 姓名 ，性别varchar(2),出生日期(datatime),家庭住址，email


-- 注意点，使用英文  ()  ,表的名称 和 字段 尽量使用  `` 括起来
-- AUTO_INCREMENT  自增
-- 字符串使用 单括号括起来
-- 所有语句后边加 , (英文的) ，最后一个不用加
-- PRIMARY KEY 主键，一般是一个表只有一个唯一的主键！
CREATE TABLE if not exists `student`(
     `id` int(4) not null auto_increment comment '学号',
    `name` varchar(30) not null default '匿名' comment '姓名',
    `pwd` varchar(20) not null  default '123456' comment '密码',
    `sex` varchar(2) not null default '女' comment '性别',
    `birthday` datetime  default null comment '出生日期',
    `address` varchar(100) default null comment '家庭住址',
    `eamil` varchar(50) default null comment '邮箱',
    PRIMARY KEY(`id`)
   )ENGINE=InnoDB DEFAULT CHARSET=utf8
```



格式

``` sql
create table [if not exists]  `表名`(
      `字段名` 列类型  [属性] [索引] [注释] ,
      `字段名` 列类型  [属性] [索引] [注释] ,
              ...........
      `字段名` 列类型  [属性] [索引] [注释] 
)  
```



常用命令

```sql
show create database `exam`         --查看创建数据库的语句
show CREATE table `student111`      --查看student111数据表的定义语句
DESC `student111`                   --显示表的结构
```

```sql
-- 关于数据库引擎/*INNODB 默认使用MYISAM 早些年使用的*/
```

|              | MYISAM | NNNODB         |
| ------------ | ------ | -------------- |
| 事务支持     | 不支持 | 支持           |
| 数据行锁定   | 不支持 | 支持           |
| 外键约束     | 不支持 | 支持           |
| 全文索引     | 支持   | 不支持         |
| 表空间的大小 | 较小   | 较大，约为两倍 |

常规使用操作：

* MYISAM  节约空间，速度较快
* INNODB 安全性高，事务的处理，多表多用户操作

> 在物理空间存在的位置

所有的数据库文件都存在data目录下

本质还是文件的存储





> 设置数据库表的字符集编码

```sql
charset=utf_8
```

不设置的话，会是mysql默认的字符集编码~（不支持中文）

mysql的默认编码是Latin1，不支持中文

在my.ini中配置默认编码

```sql
character-set-server=utf8
```





## 2.6、修改删除表

> 修改

```sql
-- 修改表名 ALTER TABLE 旧表名 RENAME AS 新表名ALTER TABLE `student1` RENAME AS `student`
-- 增加表的字段 ALTER TABLE 表名 ADD 字段名 列属性ALTER TABLE `student` ADD age int(11)
-- 修改表的字段 （重命名，修改约束！）
-- ALTER TABLE 表名 MODFIY 字段名 列属性[]ALTER TABLE `student1` MODIFY age VARCHAR(11)  
-- 修改约束-- ALTER TABLE 表名 CHANGE 旧名字 新名字 列属性[]ALTER TABLE `student` CHANGE age age1 int(1)  
-- 字段重命名-- 删除表的字段 : ALTER TABLE 表名 DROP 字段名ALTER TABLE `student` DROP age 
```

> 删除表

```sql
-- 删除表 (如果表存在再删除)DROP TABLE if EXISTS student
```

==所有的创建和删除操作尽量加上判断，以免报错~==





注意点:	

* ``  字段名，使用这个包裹！
* 注释    --      /**/ 
* SQL 关键字大小写不敏感，建议大家写小写
* 所有的符号全部用英文！



## 3.MySQL数据管理

### 3.1、外键（了解即可）

==最佳实践==

* 数据库就是单纯的表，只用来存数据，只有行（数据）和列（字段）
* 我们想使用多张表的数据，想使用外键 （程序去实现）



### 3.2、DML语言（全部记住）

数据库的意义 : 数据存储，数据管理

DML语言 :数据操作语言

* insert
* update
* delete

### 3.3、添加

> insert

```sql
-- 插入语句（添加）
-- INSERT INTO 表名([字段名1，字段2，字段3]VALUES ('值1')，('值1')，('值1')，...... )
INSERT into `student111` (`name`) VALUES ('	张三')-- 由于主键自增我们可以省略INSERT INTO `student111` (`NAME`) VALUES ('李四')
-- 一般写插入语句，我们一定要数据和字段一一对应！
-- 插入多个字段
INSERT INTO `student111` (`name`) 
VALUES ('王五'),('刘大'),('曹啦啦')

INSERT into `student111` (`NAME`,`pwd`,`sex`) 
VALUES ('大树','456987','男'),('小草','321654','女')
```

语法：`INSERT INTO 表名([字段名1，字段2，字段3]VALUES ('值1')，('值1')，('值1')，...... )`

注意事项：

1. 字段和字段之间使用 英文逗号 隔开
2. 字段是可以省略的，但是后面的值必须要一 一对应，不能少
3. 可以同时插入多条语句，values后面的值，需要使用，隔开即可  `values(),(),...`



### 3.4、修改

> updae 修改谁   （条件） set 原来的值 = 新值

```sql
-- 修改学员姓名,带了条件	
UPDATE `student111` SET `name` ='略略略' WHERE id =1
-- 不指定条件的情况下，会改动所有表	！！
UPDATE `student111` SET  `name` = '黑老大'
-- 修改多个属性，逗号隔开
UPDATE `student111` SET `name` = '黑老大',`email` ='45@163.com' WHERE id =1
-- 语法:-- update 表名 set colnum_name = values.[colnum_name = value, ....] where [条件]
```

条件 :   where 子句  运算符 ID等于某个值，大于某个值，在某个区间修改........

 操作符会返回 布尔值

| 操作符              | 含义         | 范围        | 结果  |
| ------------------- | ------------ | ----------- | ----- |
| =                   | 等于         | 5 =6        | false |
| <>或！=             | 不等于       | 5<>6        | true  |
| >                   |              |             |       |
| <                   |              |             |       |
| >=                  |              |             |       |
| <=                  |              |             |       |
| BETWEEN  ... and... | 在某个范围内 | [2,5]       |       |
| AND                 | 我和你&&     | 5>1 and 1>2 | false |
| OR                  | 我或你\|\|   | 5>1 or 1>2  | true  |

```sql
-- 通过多个条件定位数据，无上限！   
UPDATE `student111` SET `name` ='长江七号' WHERE `name` = '李四' AND sex= '女'
```

语法 : `update 表名 set colnum_name = values.[colnum_name = value, ....] where [条件]`

注意事项	：

* column_name 是数据库的列，尽量戴上   ``
* 条件，筛选的条件，如果没有指定，则会修改所有的列
* value，是一个具体的值，也可以是一个变量
* 多个设置的属性之间，使用英文逗号隔开

### 3.5、删除

> delete 命令

语法 ： `delete from 表名 [where 条件]`

```sql
-- 删除数据 (避免这样写，会全部删除) DELETE FROM `student111` 
-- 删除指定数据DELETE FROM `student111` WHERE id =1
```



> truncate 命令

作用 ： 完全清空一个数据库表，表的结构和索引约束不会变！

```sql
-- 清空student表 TRUNCATE `student`
```

> delete  和 truncate 区别

* 相同点 ：都能删除数据，都不会删除表结构
* 不同  ： 
  * truncate 重新设置 自增列 计数器会归零
  * truncate 不会影响事务





## 4、DQL查询依据（最重点）

### 4.1、DQL

(Data Query  Language : 数据查询语言)

* 所有的查询操作都用它 Select
* 简单的查询，复杂的查询他都能做
* ==数据库最核心的语言，最重要的语句==
* 使用频率最高的语句

> select 语法

```sql
SELECT    [ALL | DISTINCT | DISTINCTROW ]   
[HIGH_PRIORITY]    [STRAIGHT_JOIN]    
[SQL_SMALL_RESULT] [SQL_BIG_RESULT] [SQL_BUFFER_RESULT]    
[SQL_CACHE | SQL_NO_CACHE] [SQL_CALC_FOUND_ROWS]  
select_expr, ...  
[INTO OUTFILE 'file_name' export_options   |
INTO DUMPFILE 'file_name']   
FROM table_references    
[WHERE where_definition] 

-- 指定结果需满足的条件   
[GROUP BY {col_name | expr | position} 
-- 指定结果按照哪几个字段分组      [ASC | DESC], ... [WITH ROLLUP]]    [HAVING where_definition] 
-- 过滤分组记录必须满足的次要条件    [ORDER BY {col_name | expr | position}  
-- 指定查询记录按一个或多个条件排序      [ASC | DESC] , ...]    [LIMIT {[offset,] row_count | row_count OFFSET offset}]-
- 指定查询的记录从哪条至哪条    [PROCEDURE procedure_name(argument_list)]    [FOR UPDATE | LOCK IN SHARE MODE]]
```



### 4.2、指定查询字段

```sql
-- 查询全部学生 SELECT 字段 FROM 表SELECT * FROM student-- 查询指定字段		
SELECT  `StudentNo` ,`StudentName`  FROM `student`
-- 别名，给结果起一个名字  AS  可以给字段起别名，也可以给表起别名SELECT  `StudentNo` AS 学号 ,`StudentName` AS 学生姓名  FROM `student` AS s
-- 函数 CONCAT(a,b)SELECT CONCAT('姓名 :  ',StudentName) AS 新名字 FROM student
```

语法 : `select 字段 ...from 表`

> 有的时候，列名字不是那么见名知意。我们起别名   AS 字段名 AS   别名        表名   AS   别名







> 去重  distinct

作用  ： 去除select查询出来的结果中重复的数据，只显示一条

```sql
-- 查询一下有哪些同学参加了考试，成绩SELECT * FROM result             
-- 查询全部的成绩考试SELECT `StudentNo` FROM result   
-- 查询有哪些同学参加了考试SELECT DISTINCT `StudentNo` AS 参加考试同学编号 FROM result  
-- 发现重复数据，去重
```

> 数据库的列   （表达式）

```sql
SELECT VERSION()  
-- 查看系统版本 （函数）SELECT 100*2-1 As 计算结果  
-- 用来计算 （表达式）SELECT @@auto_increment_increment  
-- 查询自增的步长 （变量）
-- 学员考试成绩 +1 分查看SELECT `StudentNo` ,`StudentResult` +1  AS 提分后 FROM result
```

==数据库中的表达式	： 文本值， 列，NULL ，函数，计算表达式，系统变量....==

select   `表达式`    from    表



### 4.3、where条件子句

作用 ： 检索数据中`符合条件`的值

搜索的条件由一个或者多个表达式组成！  结果  布尔值

> 逻辑运算符

| 运算符     | 语法               | 描述                             |
| ---------- | ------------------ | -------------------------------- |
| AND    &&  | a and b     a&&b   | 逻辑与，两个都为真，结构为真     |
| OR    \|\| | a or b     a\|\|b  | 逻辑或，其中一个为真，则结果为真 |
| NOT  !     | not a         !  a | 逻辑非，真为假，假为真           |

==尽量使用英文字母==



```sql
-- ==========================where=============================
SELECT `studentno`AS 编号 ,`studentresult`AS 成绩 FROM result
-- 查询考试成绩在 95~100分之间SELECT `studentno`AS 编号 ,`studentresult`AS 成绩 FROM resultWHERE studentresult >=95 and studentresult <=100
-- and  && SELECT `studentno`AS 编号 ,`studentresult`AS 成绩 FROM resultWHERE studentresult >=95 && studentresult <=100
-- 模糊查询（区间）SELECT `studentno`AS 编号,`studentresult` AS 成绩 FROM resultWHERE `studentresult` BETWEEN 95 AND 100
-- 除了1000号学生之外的同学的成绩SELECT `studentno`AS 编号,`studentresult` AS 成绩 FROM resultWHERE `studentno` !=1000
-- !=  NOTSELECT `studentno`AS 编号,`studentresult` AS 成绩 FROM resultWHERE  NOT `studentno` = 1000
```

> 模糊查询	： 比较运算符

| 运算符      | 语法                 | 描述                                             |
| ----------- | -------------------- | ------------------------------------------------ |
| IS NULL     | a is null            | 如果操作符为NULL，结果为真                       |
| IS NOT NULL | a is not null        | 如果操作符为not null,结果为真                    |
| BETWEET     | a beweent and c      | 若a在b和c之间，则结果为真                        |
| **LIKE**    | a like b             | sql匹配，如果a匹配b，则结果为真                  |
| **in**      | a in(a1,a2,a3......) | 假设 a在a1，或者a2....其中的某一个值中，结果为真 |

```sql
-- ======================  模糊查询  =================================
-- 查询姓刘的同学
-- like 结合 %(代表0到任意个字符)   _（一个字符）
SELECT `studentno` ,`studentname` FROM studentWHERE studentname like '刘%'
-- 查询姓刘的同学,名字后面只有一个字的SELECT `studentno` AS 编号 ,`studentname` as 姓名 FROM studentWHERE studentname like '刘_'
-- 查询姓刘的同学,名字后面只有2个字的SELECT `studentno` AS 编号 ,`studentname` as 姓名 FROM studentWHERE studentname like '刘__'
-- 查询名字中间有嘉字的同学 %可%SELECT `studentno` AS 编号 ,`studentname` as 姓名 FROM studentWHERE studentname like '%可%'
-- ====================   in （具体的一个或多个值）    =============================
-- 查询1001,1002,1003号学员信息SELECT `studentno` AS 编号 ,`studentname` as 姓名 FROM studentWHERE `studentno`in (1001,1002,1003)
-- 查询在北京的学生SELECT `studentno` AS 编号 ,`studentname` as 姓名 FROM studentWHERE `address` in ('安徽')

-- ================    null       not null     =====================================

-- 查询地址为空的学生	 null  '' 
SELECT `studentno` AS 编号 ,`studentname` as 姓名 FROM studentWHERE `address` = '' or address IS null 
-- 查询有出生日期的学生   不为空SELECT `studentno` AS 编号 ,`studentname` as 姓名 FROM studentwhere  borndate is not NULL
```

### 4.4、连表查询

> JOIN 对比

```sql
-- =============  连表查询  join ===========================
-- 查询参加了考试的同学（学号，姓名，科目编号，分数）SELECT * FROM student
/*思路	
1.分析需求，分析查询字段来自哪些表，（连接查询）2.确定使用哪种连接查询？  
7种确定交叉点（这两个表中哪个数据是相同的）
判断的条件  ： 学生表中的   studentno  = 成绩表  
studentno*/SELECT s.studentno AS 编号 ,`studentname` AS 姓名,`subjectno` as 课程编号,`studentresult` AS 成绩FROM student AS s
INNER JOIN result AS rWHERE s.studentno =r.StudentNo
-- Right JoinSELECT r.studentno AS 编号 ,`studentname` AS 姓名,`subjectno` as 课程编号,`studentresult` AS 成绩FROM student AS s
RIGHT JOIN  result AS rON s.studentno =r.StudentNo
-- Left JoinSELECT r.studentno AS 编号 ,`studentname` AS 姓名,`subjectno` as 课程编号,`studentresult` AS 成绩FROM student AS s
left  JOIN  result AS rON s.studentno =r.StudentNo
```

| 操作         | 描述                                     |
| ------------ | ---------------------------------------- |
| Inner Join   | 如果表中至少有一个匹配，就返回行         |
| Left   Join  | 会从左表返回所有的值，即使右表中没有匹配 |
| Right   Join | 会从右表返回所有的值，即使左表中没有匹配 |

```sql
-- =============  连表查询  join ===========================
- 查询参加了考试的同学（学号，姓名，科目编号，分数）SELECT * FROM student
/*思路	
1.分析需求，分析查询字段来自哪些表，（连接查询）2.确定使用哪种连接查询？  
7种确定交叉点（这两个表中哪个数据是相同的）
判断的条件  ： 学生表中的   studentno  = 成绩表  studentno
*/
-- JOIN（连接的表） ON（判断的条件） 连接查询
-- where  等值查询
SELECT s.studentno AS 编号 ,`studentname` AS 姓名,`subjectno` as 课程编号,`studentresult` AS 成绩FROM student AS sINNER JOIN result AS r
WHERE s.studentno =r.StudentNo
-- Right JoinSELECT r.studentno AS 编号 ,`studentname` AS 姓名,`subjectno` as 课程编号,`studentresult` AS 成绩FROM student AS sRIGHT JOIN  result AS r
ON s.studentno =r.StudentNo
-- Left JoinSELECT r.studentno AS 编号 ,`studentname` AS 姓名,`subjectno` as 课程编号,`studentresult` AS 成绩FROM student AS sleft  JOIN  result AS r
ON s.studentno =r.StudentNo
-- 查询缺考的同学SELECT r.studentno AS 编号 ,`studentname` AS 姓名,`subjectno` as 课程编号,`studentresult` AS 成绩FROM student AS sleft  JOIN  result AS r
ON s.studentno =r.StudentNoWHERE studentresult is NULL
-- 思考题（查询了参加考试的同学的信息 ： 学号， 学生姓名， 科目名 ，分数）
/*思路	
1.分析需求，分析查询字段来自哪些表，（连接查询）
2.确定使用哪种连接查询？  
7种确定交叉点（这两个表中哪个数据是相同的）
判断的条件  ： 
学生表中的   studentno  = 成绩表  studentno
*/
SELECT  s.StudentNo AS 学号 ,StudentName AS 姓名 ,subjectname as 科目名,StudentResult as 成绩FROM student AS s
LEFT JOIN result AS ron s.studentno = r.StudentNo
INNER JOIN `subject` as subON s.gradeid =sub.gradeid
-- 我要查询哪些数据....-- 从哪几个表中查询  from 表 xxx Join	连接的表  on 交叉条件
-- 假设存在一种多张表查询 ，慢慢来，先查询两张表然后再慢慢增加
-- from  a left join   b-- from  a right join  b
```

> 自连接

==自己的表和自己的表连接==，核心 ： **一张表拆成两张一样的表即可**

### 4.5、分页和排序

> 排序

```sql
-- 排序 ： 升序 ASC  , 降序DESC
-- ORDER BY 通过哪个字段排序 ， 怎么排
-- 查询的结果根据 成绩升序 降序
SELECT s.studentno AS 编号 ,`studentname` AS 姓名,`subjectno` as 课程编号,`studentresult` AS 成绩FROM student AS s
INNER JOIN result AS rWHERE s.studentno =r.StudentNoORDER BY StudentResult ASC
```

> 分页

```sql
-- 为什么要分页-- 缓解数据库压力，给人的体验更好     瀑布流
-- 分页 ， 每页只显示五条数据
-- 语法 ：  limit 起始值  ，页面的大小-- 网页应用 ： 当前页， 总的页数 ， 页面的大小
-- LIMIT  0,5	      1~5	-- LIMIT  1,5        2~6-- 第一页  limit 0,5    （1-1）*5
-- 第二页  limit 5,5     （2-1）*5-- 第三页  limit 10,5      （3-1）*5-- 第N页  limit 0,5            （N-1）* pagesize，pagesize
-- 【 pagesize  :  页面大小 	】
-- 【（n-1）*pagesize起始值】
-- 【 n  当前页】
-- 【数据总数/页面大小  = 总页数】
SELECT s.studentno AS 编号 ,`studentname` AS 姓名,`subjectno` as 课程编号,`studentresult` AS 成绩FROM student AS s
INNER JOIN result AS rWHERE s.studentno =r.StudentNo
ORDER BY StudentResult ASCLIMIT  1,5
```

语法 ： `limit (查询起始下标，pagesize)`

```sql
-- 思考 ： 查询 JAVA第一学年 课程成绩排名前十的学生，并且分数要大于80的学生信息（学号，姓名，课程名称，分数）
SELECT s.studentno AS 学号 , studentname AS 姓名, subjectname AS 课程名称 , studentresult AS 分数FROM student  AS s
INNER JOIN result AS ron s.studentno = r.studentno
INNER JOIN  `subject` as subON s.gradeid = sub.gradeid
WHERE subjectname = 'JAVA第一学年' AND studentresult >=80
ORDER BY studentresult DESCLIMIT 0,10  
```

### 4.6、子查询

where（值是固定的，这个值是计算出来的）

本质 ： `在where语句中嵌套一个子查询语句`

where（select   *   from）

### 4.7、分组和过滤

```sql
-- 查询不同课程的平均分，最高分，最低分，平均分大于80分
-- 核心  ： （根据不同的课程分组）
SELECT subjectname as 课程名,AVG( studentresult) as 平均分,MAX(studentresult) as 最高分,MIN(studentresult) as 最低分
FROM student as s
INNER JOIN result as r ON  r.studentno =s.studentnoINNER JOIN `subject` as sub  on s.gradeid =sub.GradeID
GROUP BY sub.subjectname 
-- 通过什么字段来分组	HAVING 平均分 >=80
```

### 4.8、select小结

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20210906210446294.png" alt="image-20210906210446294" style="zoom:150%;" />

## 5、MySQL函数

```sql
-- =========     常用函数    ================== 
-- 数学运算SELECT ABS(-8) 
-- 绝对值SELECT CEILING(9.4) 
-- 向上取整SELECT FLOOR(9.4)   
-- 向下取整SELECT RAND()   
-- 返回一个 0~1的随机数SELECT SIGN(10)  
-- 判断一个数的符号  0-0 负数返回 -1  正数返回 1
-- 字符串函数SELECT CHAR_LENGTH('心有多大舞台就有多大')  
-- 字符串长度SELECT CONCAT('我','爱','Java') 
- 拼接字符串SELECT INSERT ('我爱 HELLO  WORD !',1,2,'超级热爱') 
-- 查询，从某个位置开始替换某个长度SELECT LOWER('ADAFSF') 
-- 转小写字母SELECT UPPER('asfds')  -- 转大写字母SELECT REPLACE('好好学习，能取得好成绩','能','一定能')  
-- 替换出现的指定字符串-- 时间和日期函数（记住）SELECT CURRENT_DATE() 
-- 获取当前日期SELECT CURDATE() 
-- 获取当前日期SELECT NOW()  
-- 获取当前时间SELECT   LOCALTIME() 
-- 本地实际SELECT SYSDATE()   
-- 系统时间SELECT 	year(NOW())  SELECT MONTH(now())  SELECT day(now())  SELECT hour(now())  SELECT minute(now())  SELECT second(now())
-- 系统SELECT SYSTEM_USER()SELECT USER()SELECT VERSION()
```

### 5.2、聚合函数（常用）

| 函数名称  | 描述   |
| --------- | ------ |
| count（） | 计数   |
| SUM（）   | 求和   |
| AVG（）   | 平均值 |
| MAX（）   | 最大值 |
| MIN（）   | 最小值 |
| ...       | .....  |

```sql
 -- ===============  聚合函数  ======================
 -- 都能够统计 表中的数据（想查询一个表中有多少记录，就使用这个count（））
 SELECT COUNT(studentname) FROM student  
 -- Count(指定列) ，会忽略所有的null值SELECT COUNT(*) FROM student            
 -- Count （*）  ，不会忽略所有的null值  ，本质 计数行数
 SELECT COUNT(1) FROM student            
 -- Count （1）  ，会忽略所有的null值  ，本质 计数行数
 SELECT SUM(`studentresult`) as 总和 FROM resultSELECT AVG( `studentresult`) as 平均分 FROM resultSELECT MAX(`studentresult`) AS 最高分 
 FROM resultSELECT MIN(`studentresult`) as  最低分 FROM result
```

### 5.3、数据库级别的MD5加密（扩展）

什么是MD5 ？

主要增强算法复杂的和不可逆性

MD5不可逆，具体的值 的 md5 是一样的

MD5 破解网站的原理，背后有一个词典，MD5加密后的值  加密前的值

```sql
-- =============  测试MD5加密  ==========================
-- 明文密码INSERT into testmd5 VALUES(4,'liuda','852357159')
-- 加密update testmd5 set pwd=MD5(pwd) where id =4update testmd5 set pwd=MD5(pwd)  
-- 加密全部的密码-- 插入的时候加密insert into testmd5 VALUES (5,'HeiLaoHu',MD5('852951'))
-- 如何校验，将用户传递进来的密码，进行MD5加密，然后比对加密后的值
select * from testmd5 where `name` ='HeiLaoHu' and MD5('852951')
```

## 6、事务

### 6.1、什么是事务

==要么都成功，要么都失败==

一一一一一一

1.SQL执行  A 给 B 转账         A 1000   --->200              B 200

2.SQL执行 B 收到 A 的钱      A 800        --->      B 400

一一一一一一

将一组SQL放在一个批次中去执行

> 事务原则 ： ACID 原则   原子性，一致性，持久性 ，隔离性   （脏读，幻读）	                                                         

**原子性 **

要么都成功，要么都失败

**一致性**

事务前后的数据完整性要保证一致

**持久性**

不可逆，被持久化到数据库中	！

**隔离性**

多用户并发访问数据库，每个的事务，不能被其他事务的操作干扰



> 隔离

**脏读**：

指一个事务读取了另一个事务未提交的数据

**不可重复读：**

在一个事务读取某一行数据，多次读取结果不同。（不一定是错误，只是场合不对）

**虚读（幻读）：**

指一个事务内读取到别的事务插进的数据，导致前后读取不一致

> 执行事务

```sql
 -- ============   事  务  ================
 -- mysql 是默认开启事务自动提交的
 set autocommit = 0 /*关闭*/
 set autocommit = 1 /*开启 （默认的）*/
 -- 手动处理事务set autocommit = 0  
 -- 关闭自动提交
 -- 事务开启	
 start TRANSACTION 
 -- 标记一个事务的开启，从这之后的SQL 都在同一事务内
 -- 提交COMMIT-- 回滚ROLLBACK
 -- 事务结束set autocommit = 1  
 -- 开启自动提交SAVEPOINT 保存点名  
 -- 设置一个事务的保存点ROLLBACK to SAVEPOINT 保存点名   
 -- 回滚到保存点RELEASE  SAVEPOINT 保存点名   
 -- 撤销保存点
```

## 7、索引

> MySQL对索引的定义 ： **索引（index）是帮助MySQL高速获取数据的数据结构。**
>
> 提取句子主干，就可以得到索引的本质：索引是数据结构

### 7.1、索引的分类

> 在一个表中，主键索引只能有一个，唯一索引可以有多个

* 主键索引（primary  key）
  * 唯一的标识，不可重复，只能有一个列作为索引
* 唯一索引（unique  key）
  * 避免重复的列出现，唯一索引可以重复，多个列都可以标识唯一索引
* 常规索引  （key / index）
  * 默认的，index，key 关键字来设置
* 全文索引   （FullText）
  * 在特定的数据库引擎下才有 MyISAM
  * 快速定位数据



基础语法

```sql
-- 索引的使用
-- 1.在创建表的时候给字段增加索引
-- 2.创建完毕后，增加索引
-- 显示所有的索引信息SHOW INDEX FROM student 
-- 增加一个全文索引  (索引名) 列名	
ALTER TABLE school.`student` ADD FULLTEXT INDEX `studentanme`(`studentname`)
-- EXPLAIN 分析SQL执行的状况EXPLAIN select * from student ;  
-- 非全文索引EXPLAIN select * from student WHERE MATCH(studentname) AGAINST ('刘') 
```

### 7.2、 测试索引

==索引在小数据量的时候用处不大，但在大数据的时候，区别十分明显==

### 7.3、索引原则

* 索引不是越多越好
* 不要对进程变动数据加索引
* 小数据量的表不需要加索引
* 索引一般加在常用来查询的字段上



> 索引的数据结构

Hash 类型的索引	

Btree ： InnoDB的默认数据结构



## 数据库规范设计

==当数据库比较复杂的时候，需要设计==





## 三大范式

**为什么要数据规范化？**

* 信息重复
* 更新异常
* 插入异常
  * 无法正常显示信息
* 删除异常
  * 丢失有效信息

> 三大范式

**第一范式（1NF）**

原子性：保证每一列不可再分

**第二范式（2NF）**

前提：满足第一范式  

每张表只描述一件事情

**第三范式（23NF）**

前提：满足第二范式

确保数据表中的每一列数据都与主键直接相关，而不能间接相关



（规范数据库设计）



**规范性 和 性能的问题**

关联查询的表不得超过三张表

* 考虑商业化的需求和目标，（成本，用户体验！）数据库的性能更加重要
* 在规范性能问题的时候，需要适当的考虑规范性！
* 故意给某些表增加一些冗余的字段。（从表查询中变为单表查询）
* 故意增加一些计算列（从大数据量降低为小数据量的查询 ： 索引）

## 10、JDBC（重点）

### 10.1、数据库驱动

驱动 ： 声卡，显卡，数据库

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20210907073842444.png" alt="image-20210907073842444" style="zoom:80%;" />

我们的程序会通过 数据库 驱动 ，和数据库打交道！



### 10.3、JDBC

SUN公司为了简便开发人员 （对数据库的统一）操作，提供了一个（Java操作数据库的）规范 JDBC

这些规范的实现由具体的厂商去做	~

对于开发人员，我们只需要掌握jdbc接口的操作即可

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20210907074345161.png" alt="image-20210907074345161" style="zoom:80%;" />

java.sql	

javax.sql

还需要导入一个数据库驱动包



### 10.3、第一个JDBC程序

> 创建测试数据库

1. 创建一个普通项目

2. 导入数据库驱动
3. 编写测试代码

```java
package com.zhang.lesson01;import java.sql.*;
public class JdbcFirstDemo {    
public static void main(String[] args) throws ClassNotFoundException, SQLException {     
//1.加载驱动       
Class.forName("com.mysql.jdbc.Driver");   
//固定写法，加载驱动      
//2.用户信息和URL     
//useUnicode=true&characterEconding=utf8&useSSL=false     
String url ="jdbc:mysql://localhost:3306/jdbcstudy?useUnicode=true&characterEnconding=utf8&useSSL=false";  
String username ="root";      
String password ="123456";      
//3.连接成功，数据库对象 Connection 代表数据库    
Connection connection = DriverManager.getConnection(url, username, password);     
//4.执行SQL对象 Statement 执行SQL对象     
Statement statement = connection.createStatement(); 
//5.执行SQL的对象 去 执行SQL,可能存在结果，查看返回结果    
String sql="select * from users";      
ResultSet resultSet = statement.executeQuery(sql);//返回的结果集,结果集中封装了我们全部查询出来的结果   
while (resultSet.next()){        
System.out.println("id=" +resultSet.getObject("id"));       
System.out.println("name=" +resultSet.getObject("NAME"));    
System.out.println("pwd=" +resultSet.getObject("PASSWORD"));        
System.out.println("email=" +resultSet.getObject("email"));      
System.out.println("birth=" +resultSet.getObject("birthday"));     
}   
//6.释放连接     
resultSet.close();  
statement.close();     
connection.close();  
}}
```

步骤总结 ： 

1. 加载驱动
2. 连接数据库DriverManger
3. 获得执行SQL的对象 Statement
4. 获得返回的结果集
5. 释放连接



> DriverManger

```java
//1.加载驱动      
Class.forName("com.mysql.jdbc.Driver");  
//固定写法，加载驱动Connection connection = DriverManager.getConnection(url, username, password);
//connection 代表数据库
//数据库设置自动提交
//事务提交
//事务回滚      
connection.rollback();    
connection.commit();      
connection.setAutoCommit();
```



> URL

```java
 String url ="jdbc:mysql://localhost:3306/jdbcstudy?useUnicode=true&characterEnconding=utf8&useSSL=false";
 //mysql 
 -- 3306//jdbc:mysql://locallhost:3306
 （主机地址：端口号）/数据库名?参数1&参数2&参数3
 // oracle 
 -- 1521//jdbc:oracle:thin:@locallhost:1521:sid
```

> Statement 执行SQL的对象                  
>  PrepareStatement执行SQL的对象

```java
    String sql="select * from users"; 
    //编写SQL          
    statement.executeQuery();  
    //查询操作，返回ResultSet  
    statement.execute();//执行任何SQL   
    statement.executeUpdate();//更新，插入，删除。都是用这个，返回一个受影响的行数
```

> ResulltSet 查询的结果集 ： 封装了所有的查询结果

获得指定的数据类型

```java
resultSet.getObject(); 
//在不知道列类型的情况下使用
//如果知道列的类型就使用指定的类型
resultSet.getString();
resultSet.getInt();
resultSet.getFloat();
resultSet.getDate();
.....
```

遍历，指针

```
resultSet.beforeFirst(); 
//移动到最前面resultSet.afterLast();
//移动到最后面resultSet.next(); 
//移动到下一个数据resultSet.previous(); 
//移动到下一行resultSet.absolute(row); 
//移动到指定行
```

> 释放资源

```
//6.释放连接resultSet.close();
statement.close();connection.close(); 
//耗资源，用完关掉！
```

### 10.4、statement对象

==JDBC中的statement对象用于向数据库发送SQL语句，想完成对数据库的增删改查，只需要通过这个对象向数据库发送增删改查语句即可。==

 Statement对象的executeUpdate方法，用于向数据库发送增、删、改的SQL语句，executeUpdate执行完毕后，将会返回一个整数（即增删改语句导致数据库的几行数据发生变化）。

Statement.executeQuery方法用于向数据库发送查询语句，executeQuery方法返回代表查询结果的ResultSet对象。

> CRUD操作 
> -- create

使用executeUpdate(String sql)方法完成数据添加操作	，示例操作 :

```java
statement st =conn.createstatement():
String sql = "insert into user(...)values(...)";
int num =st.executeUpdate(sql);
if(num>0){ 
system.out.println("插入成功！！")
}
```

> CRUD操作 
>-- delete

使用executeUpdate(String sql)方法完成数据删除操作，示例操作 ： 

```java
statement st =conn.createstatement():
String sql = "delete from user where id =1";
int num =st.executeUpdate(sql);
if(num>0){ 
system.out.println("删除成功！！")
}
```

> CRUD操作  -- update

使用executeUpdate(String sql)方法完成数据修改操作，示例操作 ： 

```java
statement st =conn.createstatement():
String sql = "update user set name='' where name=''";
int num =st.executeUpdate(sql);
if(num>0){  
system.out.println("修改成功！！")
}
```

> CRUD操作  -- read

使用executeUpdate(String sql)方法完成数据查询操作，示例操作 ： 

```java
·statement st =conn.createstatement():
String sql = "select * from user where id =1";
ResultSet rs =st.executeQuery(sql);
while(rs.next()){ 
//根据获取列的数据类型，分别调用rs的相应方法映射到java对象中
}
```

> 代码实现

1. 提取工具类

```java
package com.zhang.lesson2.utils;
import java.io.IOException;
import java.io.InputStream;
import java.sql.*;
import java.util.Calendar;
import java.util.Properties;
public class JdbcUtils {   
private static String driver;    
private static String url;   
private static String username;    
private static String password;    
static{       
try{         
InputStream in = JdbcUtils.class.getClassLoader().getResourceAsStream("db.properties");     
Properties properties = new Properties();       
properties.load(in);        
driver =properties.getProperty("driver");     
url =properties.getProperty("url");         
username =properties.getProperty("username");     
password =properties.getProperty("password");        
//1.驱动只加载一次          
Class.forName(driver);    
} catch (Exception e) { 
e.printStackTrace();      
}    }   
//获取连接  
public static  Connection getConnection() throws SQLException {    
return DriverManager.getConnection(url, username, password);  
}    
//释放连接资源  
public static  void release(Connection conn, Statement st, ResultSet rs){  
if (rs !=null){      
try {          
rs.close();       
} catch (SQLException throwables) {      
throwables.printStackTrace();     
}        }      
if (st != null){      
try {            
st.close();        
} catch (SQLException throwables) {     
throwables.printStackTrace();        
}       
if (rs  != null){    
try {             
rs.close();         
} catch (SQLException throwables) {      
throwables.printStackTrace();             
}            }        }    }}
```

2. 编写增删改的方法，`executeUpdate`

   ```java
   package com.zhang.lesson2.utils;
   import java.sql.Connection;import java.sql.ResultSet;
   import java.sql.SQLException;
   import java.sql.Statement;
   public class TestInsert {   
   public static void main(String[] args) {   
   Connection conn =null;      
   Statement st =null;     
   ResultSet rs =null;     
   try {           
   conn =JdbcUtils.getConnection();//获取数据库连接    
   st =conn.createStatement();      
   String sql ="INSERT INTO users(id,`NAME`,`PASSWORD`,`email`,`birthday`)" +     
   "VALUES (4,'HeiDa','123456','15714034373@qq.com','1999-02-14')";       
   int i = st.executeUpdate(sql);        
   if (i >0){          
   System.out.println("插入成功！");      
   }        } catch (SQLException throwables) { 
   throwables.printStackTrace();    
   }finally {         
   JdbcUtils.release(conn,st,rs);    
   }    }}
   ```

```java
package com.zhang.lesson2.utils;
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;import java.sql.Statement;public class TestDelete {  
public static void main(String[] args) {   
Connection conn=null;   
Statement st = null;     
ResultSet rs =null;    
try {       
conn = JdbcUtils.getConnection();    
st =conn.createStatement();        
String sql =" delete from users  where id =4";     
int i  = st.executeUpdate(sql);        
if (i>0){             
System.out.println( "删除成功");      
}        } catch (SQLException throwables) {    
throwables.printStackTrace();     
}        finally {      
JdbcUtils.release(conn,st,rs);    
}    }}
```

```java
package com.zhang.lesson2.utils;
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;import java.sql.Statement;public class TestUpdate { 
public static void main(String[] args) {     
Connection conn=null;      
Statement st =null;       
ResultSet rs =null;    
try {         
conn = JdbcUtils.getConnection();  
st =conn.createStatement();      
String sql ="Update users set `NAME`= 'zcz',`email`='1571403473@qq.com' WHERE id = 1 ";       
int i = st.executeUpdate(sql);    
if (i>0){            
System.out.println("修改成功");      
}        } catch (SQLException throwables) {   
throwables.printStackTrace();    
}finally {        
JdbcUtils.release(conn,st,rs);      
}    }}
```

3.查询`executeQuery`

```java
package com.zhang.lesson2.utils;
import java.sql.Connection;
mport java.sql.ResultSet;
import java.sql.SQLException;import java.sql.Statement;
public class TestSelect {   
public static void main(String[] args) { 
Connection conn =null;     
Statement st =null;   
ResultSet rs =null;    
try {           
conn = JdbcUtils.getConnection();       
st =conn.createStatement();         
String sql ="select * from users";        
rs = st.executeQuery(sql); 
//查询完毕会返回一个结果集      
while (rs.next()){             
System.out.printf(rs.getString("NAME"));      
}        } catch (SQLException throwables) { 
throwables.printStackTrace();    
}finally {      
JdbcUtils.release(conn,st,rs);   
}    }}
```

> SQL注入问题

SQL存在漏洞，会被攻击，导致数据泄露 ==SQL会被拼接 or==

```java
package com.zhang.lesson2.utils;
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
public class SQL注入 {   
public static void main(String[] args) {    
//  login("zcz","123456");   
// login(" ' or '1=1"," 'or '1=1"); 
login("1 and version() >0"," 'or '1=1");    }   
//登录业务    public  static  void  login(String username,String password){ 
Connection conn =null;      
Statement st =null;    
ResultSet rs =null;       
try {        
conn = JdbcUtils.getConnection();     
st =conn.createStatement();       
String sql ="select * from users where NAME ='"+username+"' AND password = '"+password+"'";     
rs = st.executeQuery(sql); 
//查询完毕会返回一个结果集     
while (rs.next()){            
System.out.printf(rs.getString("NAME"));      
System.out.printf(rs.getString("password"));   
System.out.println("=============================");    
}     } catch (SQLException throwables) {    
throwables.printStackTrace();    
}finally {        
JdbcUtils.release(conn,st,rs);        }    }    }
```

### 10.5、PrepareStatement对象

PrepareStatement  可以防止SQL注入	，效率更高！



1. 新增

   ```java
   package com.zhang.lesson3;
   import com.zhang.lesson2.utils.JdbcUtils;import java.sql.*;
   import  java.util.Date;public class TestInsert {  
   public static void main(String[] args) {       
   Connection conn = null;    
   PreparedStatement st = null;  
   ResultSet rs = null;      
   try {         
   conn =JdbcUtils.getConnection();   
   //区别          
   //使用问号？占位符代替参数     
   String sql ="INSERT INTO users(id,`NAME`,`PASSWORD`,`email`,`birthday`) values(?,?,?,?,?)";   
   st   = conn.prepareStatement(sql);//预编译SQL，先写SQL，然后不执行    
   //手动给参数赋值         
   st.setInt(1,4);      
   st.setString(2,"聂士煌");   
   st.setString(3,"456789");   
   st.setString(4,"789654@163.com");    
   //注意点 ： sql.Date   数据库   java.sql.Date   
   //        util.Date  java   new Date().getTime()获得时间戳     
   st.setDate(5, new  java.sql.Date(new Date().getTime()));     
   //执行       
   int i = st.executeUpdate();      
   if (i>0){             
   System.out.println("插入成功！");        
   }        } catch (SQLException throwables) {    
   
   throwables.printStackTrace();    
   }finally {        
   JdbcUtils.release(conn,st,rs);        }    }}
   ```

   

2. 删除

   ```java
   package com.zhang.lesson3;
   import com.zhang.lesson2.utils.JdbcUtils;
   import java.sql.Connection;
   import java.sql.PreparedStatement;
   import java.sql.SQLException;public class TestDelete {   
   public static void main(String[] args) {   
   Connection conn =null;    
   PreparedStatement st =null;   
   try {           
   conn= JdbcUtils.getConnection();     
   String sql="delete from  users where id=?";    
   st = conn.prepareStatement(sql);        
   st.setInt(1,4);        
   int i = st.executeUpdate();    
   if (i>0){             
   System.out.println("删除成功！");     
   }        } catch (SQLException throwables) {     
   throwables.printStackTrace();    
   }finally {      
   JdbcUtils.release(conn,st,null);     
   }    }}
   ```

   

3. 更新

   ```java
   package com.zhang.lesson3;
   import com.zhang.lesson2.utils.JdbcUtils;import java.sql.Connection;
   import java.sql.PreparedStatement;
   import java.sql.SQLException;public class TestUpdate {  
   public static void main(String[] args) {     
   Connection conn =null;    
   PreparedStatement st =null;     
   try {        
   conn = JdbcUtils.getConnection();      
   String sql="update users set    `NAME`  =?  where id=? ;";   
   st=conn.prepareStatement(sql);         
   st.setString(1,"任凯龙");        
   st.setInt(2,2);        
   int i = st.executeUpdate();   
   if (i>0){               
   System.out.println("修改成功");    
   }        } catch (SQLException throwables) {    
   throwables.printStackTrace();     
   }finally {      
   JdbcUtils.release(conn,st,null);        }    }}
   ```

   

4. 查询

   ```java
   package com.zhang.lesson3;
   import com.zhang.lesson2.utils.JdbcUtils;
   import java.sql.Connection;import java.sql.PreparedStatement;
   import java.sql.ResultSet;import java.sql.SQLException;public class TestSelect {   
   public static void main(String[] args) {     
   Connection conn=null;     
   PreparedStatement st =null;   
   ResultSet rs =null;    
   try {         
   conn= JdbcUtils.getConnection();    
   String sql="select * from users  where id =?;";     
   st=conn.prepareStatement(sql);       
   st.setInt(1,2);        
   rs=st.executeQuery();      
   if (rs.next()){           
   System.out.println(rs.getString("NAME"));    
   }        } catch (SQLException throwables) {  
   throwables.printStackTrace();      
   }finally {          
   JdbcUtils.release(conn,st,rs);   
   }    }} 
   ```

   

5. 防止SQL注入

   ```java
   package com.zhang.lesson2.utils;
   import java.sql.*;
   public class SQL注入 {  
   public static void main(String[] args) {
   //    login("zcz","123456");   
   // login(" ' or '1=1"," 'or '1=1");      
   login("1 and version() >0"," 'or '1=1");  
   }   
   //登录业务 
   public  static  void  login(String username,String password){   
   Connection conn =null;   
   PreparedStatement st =null;     
   ResultSet rs =null;       
   try {          
   conn = JdbcUtils.getConnection();     
   //PrepareStatement 防止注入的本质，把传递进来的参数当做字符     
   //假设其中存在转义字符，就直接忽略  比如， ‘ 会被直接转义    
   String sql ="select * from users where NAME =? AND password = ?";   
   st=conn.prepareStatement(sql);           
   st.setString(1,username);        
   st.setString(2,password);         
   rs = st.executeQuery(); 
   //查询完毕会返回一个结果集       
   while (rs.next()){          
   System.out.printf(rs.getString("NAME"));        
   System.out.printf(rs.getString("password"));    
   System.out.println("=============================");   
   }        } catch (SQLException throwables) {     
   throwables.printStackTrace();   
   }finally {        
   JdbcUtils.release(conn,st,rs);    
   }    }    }
   ```

   

### 10.7、使用IDEA连接数据库

![image-20210907221036220](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20210907221036220.png)

连接成功后，可以选择数据库

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20210908073732131.png" alt="image-20210908073732131" style="zoom:67%;" />

双击数据库

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20210908074014393.png" alt="image-20210908074014393" style="zoom:67%;" />



更新数据

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20210908075412015.png" alt="image-20210908075412015" style="zoom:67%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20210908075255381.png" alt="image-20210908075255381" style="zoom:67%;" />

### 10.8、事务

==要么都成功，要么都失败==

> ACID原则

原子性 ：要么全部完成，要么都不完成

一致性 ：总数不变

**隔离性 ：多个进程互不干扰**

持久性 ： 一单提交不可逆



隔离性的问题 ：

脏读 ：一个事务读取了另一个没有提交的事务

不可重复读 ： 在同一个事务内，重新读取表中的数据，表数据发生改变

虚读（幻读） ： 在一个事务内，读取到了别人插入的数据，导致前后读取的结果不一致

> 代码实现

1. 开启事务`conn.setAutoCommit(false);`
2. 一组业务执行完毕，提交事务
3. 可以在catch语句中显示的定义 回滚语句，但默认失败就回滚

```java
package com.zhang.lesson4;import com.zhang.lesson2.utils.JdbcUtils;
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;public class TestTransaction {    
public static void main(String[] args) {     
Connection conn =null;   
PreparedStatement st =null;    
ResultSet rs =null;     
try {      
conn = JdbcUtils.getConnection();   
//关闭数据库的自动提交功能,自动开始事务     
conn.setAutoCommit(false);//开启事务        
String sql1 ="update account set money = money -100 where name = 'A'";    
st=conn.prepareStatement(sql1);        
st.executeUpdate();        
String sql2 ="update account set money = money +100 where name = 'B'";       
st =conn.prepareStatement(sql2);       
st.executeUpdate();      
//业务完毕，提交事务        
conn.commit();        
System.out.println("操作成功！");     
} catch (SQLException throwables) {    
try {           
//失败默认回滚    
conn.rollback();//如果失败就回滚    
} catch (SQLException e) {       
e.printStackTrace();       
}          
throwables.printStackTrace();    
}finally {JdbcUtils.release(conn,st,rs);    
}    }}
```

### 10.9、数据库连接池

数据库连接---执行完毕----释放        

 连接----释放  十分浪费系统资源

**池化技术 ： 准备一些预先的资源，过来就连接预先准备好的**

最小连接数 ： 10

最大连接数 ： 15业务最高承载上限

等待超时 ： 100ms



==编写连接池 ，实现一个接口 DateSourse==



> 开源数据源实现（拿来即用）

DBCP

C3P0

Druid : 阿里巴巴



使用了这些数据库连接池后，我们在项目中就不需要编写数据库的代码了！

> DBCP

需要用的jar包

commons-dbcp-1.4.jar，commons-pool-1.6.jar

> C3P0

需要用的jar包

c3p0-0.9.5.2，mchange-commons-java-0.2.12

> Druid

需要用的jar包

druid-1.0.9
