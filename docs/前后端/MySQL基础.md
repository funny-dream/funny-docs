## MySQL基础

```shell
# =============================
# Author : mikigo
# Time   : 2020/3/1
# =============================
```

## 一、数据库基础

### 1、数据库概述

①概念：依照某种数据模型组织起来并存放在二级存储器（硬盘）中的数据集合。

②主流的数据库：关系型的有MySQL、SQLserver、oracle、DB2，非关系型：HBase、NoSQL（mongoDB、redis、memache）

### 2、概念模型

① 概念：是现实世界到机器世界的一个中间层侧，是数据库设计人员和用户之间交流的工具，通过它可以转换得到数据模型。

② 特点：简单清晰，易于理解，较强的语义表达能力。

③ 涉及到的基本概念：

(1) 实体（一本书，一个人）

(2) 属性（对实体的描述）

(3) 码：

a.超码：能够唯一确定的一个实体的一个或多个属性的集合。

b.候选码：能够确定一个实体的多个属性。

c.主码：能够唯一确定的一个实体的属性。

(4) 实体型和实体集：课程（课程号、课程名）就是一个实体型，所有课程组成一个实体集。

(5) 联系

a.一对一（1:1）

b.一对多（1：n）

c.多对多（m：n）

④ E-R模型和E-R图

(1) 用矩形表示实体，用椭圆表示属性，用菱形表示关系，用直线连接。

### 3、数据模型

① 数据模型的特点

(1) 能比较真实的模拟现实世界。

(2) 容易理解

(3) 便于在计算机上实现。

② 数据模型的组成要素

(1) 数据结构（静态特性的描述）

(2) 数据操作（主要是查询和更新）

(3) 完整性约束条件

③ 常见的数据模型

(1) 层次模型

a.定义：用树型结构表示实体之间的联系的模型

b.特点：在一个层次模型中的限制条件是：有且仅有一个节点，无父节点，此节点为树的根；其他节点有且仅有一个父节点。

(2) 网状模型

a.定义：用网络结构表示实体类型及其实体之间联系的模型

b.特点：

1) 允许一个以上的节点无父节点
2) 一个节点可以有多于一个父节点

(3) 关系模型

a.定义：用二维表的形式表示实体和实体之间联系的数据模型

b.特点：

1) 数据结构简单（二维表）
2) 扎实的理论基础：

a. 关系运算理论

b. 关系模式设计理论

c.关系数据模型的三种约束完整性

1）实体完整性：实体的主键不能取空值。

2）参照完整性：是指参照关系中每个元素的外码要么为空(NULL)，要么等于被参照关系中某个元素的主码。

3）用户定义完整性：指对关系中每个属性的取值作一个限制(或称为约束)的具体定义。比如 性别属性只能取”男“或”女“ ，再就是年龄的取值范围，可以取值0-130 ，但不能取负数，因为年龄不可能是负数。

## 二、MySQL基本知识

### 1.MySQL概述

（1）MySQL是一个小型关系型数据库管理系统。

（2）特点：

① 图形化用户界面，使得系统管理和数据库管理跟家直观、简单。

② 丰富的编程接口工具

③ 支持多用户、多线程

④ 跨平台使用

### 2.MySQL的安装

(1) MySQL为免费开源，可以在官网下载安装，使用wamp中的MySQL作为数据库。

(2) Navicat是MySQL的图形化管理软件，在Navicat官网下载安装后，使用破解工具破解

(3) 点击【连接】，选择MySQL

(4) 输入连接名（可以自己取名字），输入服务器IP地址（本次直接用localhost即可），输入服务器端口号、用户名（root）和密码（可以为空）

### 3.远程访问数据库

(1) 服务器端需要授权：MySQL查询编辑上输入：grant all privileges on*.*to’用户名’@’%’ identified by’密码’ with grant option;（%，是指对所有人，如果是针对某个人，可替换为对应的IP）

(2) 关闭防火墙

(3) Flush privileges（刷新权限）

### 4.MySQL系统数据简介

(1) 四个系统数据库

① Information schema 是信息数据库。保存MySQL服务器维护的其他数据库的信息。

② MySQL系统数据库，主要存储了一些存储MySQL服务的系统信息表。

③ Performance_schema 用于收集数据库服务器性能参数。

④ Sys系统数据库，可以了解系统的元数据信息。

(2) 常用的MySQL数据类型

① int 整型，可以存储-2的31次方到2的31次方之间的整数。占用4个字节。

② Float 浮点型，小数，在MySQL里是4个字节单精度。

③ Char 字符型，存储制定长度的定长非统一编码型的数据。（固定长度）

④ Varchar字符型，指定最大长度。（可以小于）

(3) 数据库的基本操作

①create database dbname;（创建数据库）

②Drop database dbname;（删除数据库）

③Create table name;（创建表）

④Varchar(5)长度为5个字符以内

⑤Primary key（主键）

⑥Not null（不能为空）

⑦Create database dbname default character set utf8 collate utf8_general_ci;(创建一个字符集为utf8的数据库，否则输入汉字时，会变成问号）

Create database `test` ：代表的是创建数据库 test。

default character set utf8 ：代表的是将默认编码格式设置为utf8格式。

collate utf8_general_ci ：代表的是数据库校对规则

## 三、数据库基本操作

### 数据库对象

（1）表：有行和列表示

①每列为一个字段。

②每行为一条记录。

③有一个唯一的主键，主键不能为空。

（2）外键：两个实体中的主键，在关系表中成为外键。

（3）索引（index）：根据指定的数据库表列建立起来的顺序。它提供了快速访问数据的途径。索引所指向的列中的数据不重复。

（4）视图（view）：是查询数据库产生的，从数据库去相应的数据进行呈现，视图内数据无法修改，在基表中修改后，视图表会自动修改。

（5）触发器（trigger.扳机、开枪）：设置一个触发的动作，对表自动进行增删改查。

（6）存储过程（store procedure）:存储在数据库的SQL程序。 

### 表约束

**1.主键约束（primary key）**

①一个表通过一个列或多个列组合的数据来唯一标识表总的每一行，这一列或多个列的组合成为主键。

a 主键列具有唯一性

b 一个表只有一个主键

c MySQL通过主键建议唯一索引，加快对主键的查询速度。

②主键约束两种写法

a.列级约束：直接在字段后定义primary key

1) Create table mikigo (

m_name primary key

);

b.表级约束：先写完表，再定义表里的primary key

1) Create table mikigo (

m_name varchar(6),

m_id varchar(11),

Constraint pk_id primary key(m_id)

);

**2.外键约束（foreign）**

① 定义：建立和强调两个表之间的关系，即关系表的一个列与另一个表中的具有唯一性的列相关，这个列就是关系表中的外键。

**3.唯一性约束（unique）**

①保证在非主键的指定唯一性的列上不会出现重复的数据，（在学生表中指定了学好为主键，身份证列作为非主键建立唯一性约束，则身份证号不能重复。）

② 唯一性约束可以建立在多个非主键的列上，而且允许为空值。（和主键约束的区别）

（4）检查约束（check）：在MySQL上没有用

（5）默认值约束（default）：如果用户没有明确出某一列的值，将显示为默认值。

（6）空值约束（null）：不为空时约束为not null， 为空为null，为空可以不写。

### SQL结构化查询语句

SQL（structrued query language）查询语句包含四类：

(1) 数据定义语言（DDL，data definition language）

(2) 数据操纵语言（DML,data manipulation language）

(3) 数据控制语言（DCL,data control language）

(4) 系统存储语言（System Stored procedure）

#### 1.数据定义语言

(1) Create table（建表）

```sql
Create table 表名(
sname varchar(3) not null,
Sid varchar(5) primary key
);
```

(2) Create index（建索引）

(3) Alter table（修改表）

(4) Drop table（删表）

① Drop table 表名;（删除某个表）

(5) Drop index（删索引）

(6) Insert into....select... ：表示将一个表中的数据插入到另一个表中

```sql
Insert into student(sno,ssex,sname) Select sno,ssex,sname from student_1
```

(7)update 表名 set 列名=’更新值’ Where 。。。。  (表示更新某个字段数据）

```sql
update student
Set sname=’mikigo’
Where sno=401
```

(8)delete from 表名 Where.. （表示删除某行数据）(drop 是直接删表，delete是对表中的数据进行删除)

```sql
Delete from student
Where sno=101
```

（9）alter table修改表

- 修改表名：Alter table 原表名 rename to 目标表名 

  ```sql
  Alter table student rename to student_1
  ```

- 新增字段：Alter table 表名 add 字段名 varchar(50) null

  ```sql
  Alter table student add pass_or_not varchar（50）
  ```

- 修改字段属性：Alter table 表名 change 原字段名 新字段名 varchar(4)

  ```sql
   Alter table student change sno sno varchar(4) primary key
  ```

- 删除字段：alter table 表名 drop column 字段名

  ```sql
   Alter table student drop column pass_or_not
  ```

#### 2.数据操纵语言

##### (1) insert插入语句

```sql
Insert into student(sno, sname)（表名）
Values（001，mikigo）
```

表示向student表中插入一行数据。

```sql
Insert into student2（sno,sname）
Select student1 (s_no,s_name)
```

表示将student1中的内容插入到student2中。

##### (2) select查询

① Select * From student

(查询student表中所有列)

② Distinct 过滤重复行

```sql
Select distinct sno from score
```

（从成绩表中查询剔重后的学号）

##### (3) Where 子句，指定条件查询

① 范围运算符 between...and..，not between....and...（（不）在什么之间）

```sql
Select title , price
From titles
Where price between 10 and 30
```

② 列表运算符in ，not in（表示在指定项中）

```sql
Select sname
From student
Where sno in (‘001’,’002’)
```

③ 空值判断符 is null , is not null  （是否为空）

```sql
Select title , price
From titles
Where price is null
```

④ 逻辑运算符 and , or

And 表示同时满足

Or 表示满足一个条件即可

##### (4) 模糊匹配like ， not like

① 匹配任意类型长度的字符用%，固定长度字符用下划线__

```sql
Select sname ,sage
From student
Where sname like ‘%王%’ (‘王_’)
```

表示查询命中中带有“王”的姓名

② 指定一个字符、字符串或范围用[  ]、`[^  ]`

```sql
Select sname
From student
Where sname like ‘[b-k]%’
```

表示名字开头是b-k的姓名

##### (5) 集合函数（聚合函数）

① 平均值 avg

② 总和 sum

③ 最小值 min

④ 最大值 max

⑤ 计数 count

集合函数使用在select 后面

```sql
Select min(price) from titles
```

表示在表中，取价格的最小值，min(price) as 价格

##### (6) Group by 子句，分组

① Group by 子句中，不能使用集合函数

```sql
Select sname,ssex
From student
Group by ssex
```

表示已性别作为分组，统计显示姓名和性别

②select 中多个非集合项出现时，group by 里面也要有同样的非集合项

##### (7) Order by 排序：

对查询结果按照升序（asc）或降序（desc）排列。

```sql
Select sname,sage
From student
Where ssex=’男’
Order by sage desc
```

表示将student表中的男生，按照年龄降序排列，显示姓名和年龄

##### (8)having ...条件

Having 子句与group by 使用表示增加某个条件。

```sql
select count(*)
From student
Group by ssex
Having age<15
```

##### (9)嵌套查询

①Where 表达式 （not）in  (子查询)

```sql
select *
from score
where cno in(select cno
from course
where tno in(select tno from teacherwhere depart ='电子工程系'));
```

②比较运算符

a.Any: `where degree >any(81.85) `表示degree 大于81或85中的任意一个。

b.All : `where degree >all(81.85) `表示degree 大于81或85中的每一个。

c.Some：同 any

③联接查询

a.内连接

```sql
from student inner join score on student.sno=score.sno
```

或

```sql
Where student.sno=score.sno
```

b.外连接

1）左联接：（以左边表为基准，左边所有数据要出现，右边表无数据的，为空值）

```sql
from course left join score on course.cno=score.cno 
```

2）右联接： (以右边表为基准，右边所有数据要出现，左边表无数据的，为空值）

```sql
from course right join score on course.cno=score.cno
```

#### 3.数据控制语言（DCL）

（1）grant 语句

Grant 权限1，权限2 on 表名 to uername

为某个用户授予某个权限

```sql
grant update on student to mikigo
```

（2）Revoke 语句

Revoke 权限1，权限2 on 表名 from uername

收回某个用户的某个权限

```sql
Revoke update on student from mikigo 
```

#### 4.View 视图

（1）视图是某个查询结果的虚表。试图对应的数据并不实际存在。

（2）语法：create view 视图名称 As Select 列名称 from 表名称 where 条件

 ```sql
 Create view mikigo
 As
 Select *
 From Student
 Where ssex=’男’
 ```

（3）修改视图：drop view 视图名称。

#### 5.procedure 存储过程

（1）存储过程的三个组成部分。

1) 所有的输入参数以及传给调用者的输出参数
2) 被执行的正对数据库的操作语句，包括调用其它存储过程的语句。
3) 返回给调用者的状态值，以指明调用是否成功。

（2）使用navicat 创建存储过程

1) 点击函数右键，选择新建函数，输入定义模式、参数名、数据类型。
2) 点击完成，在begin和end之间存储过程语句，点击保存，设置过程名。

```sql
Begin
While i<30 do
Insert into score values (floor(110+rand()+20),’5-245’,’99’);
Set i=i+1;
End while;
End
```

调用的使用：call 过程名（赋值）

#### 6.trigger 触发器

（1）触发器是一种特殊类型的存储过程，主要通过事件进行触发而被执行。触发器用于MySQL约束、默认值和规则的完整新的检查。

（2）触发器类型

1) Update 在更新时触发
2) Insert 在插入时触发
3) Delete 在删除操作时触发
4) After 在一个触发动作之后激活

（3）语法：

```sql
Create trigger huang
After update on student for each row
Insert into student_1
Values (404,’明天’,’男’)
```

表示当对student表进行更新之后，将一组数据插入到student_1表中。

#### 7.常见函数

（1）Left/right 函数

Select left (‘kdhoa’,3) 表示从左向右，截取3个字节

（2）Length函数

Select length(‘ijgoado’)表示括号内字符的长度

（3）Replace 函数

Select replace (‘ydk’,’k’,’a’) 表示将字符中的k 替换成a

（4）Substring 函数

Select substring (‘eohgdhd’,2,3) 表示从第2位开始取，往后取3位(ohg)

（5）日期函数

1) Now( )：表示当前日期，精确到时分秒 2019-10-29 19:31:20
2) curdate( )：表示当前时间，精确到日 2019-10-29
3) Year( )：表示日期年份2019
4) Month( )：表示日期月份10
5) Day( )：表示日期的日29

（6）Datediff函数

1) 表示函数返回两个日期之间的天数
2) Select datediff (‘time1’,’time2’)  计算逻辑是time1-time2