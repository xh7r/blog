# 登录/退出

登录：mysql -uroot -p
退出：quit/exit

# 查看

show databses；查看有哪些数据库（这个不是SQL语句，属于MySQL的命令。）
show tables; 查看数据库中的表
select * from table; 查看表中的数据
desc table; 查看表结构（describe）
show database(); 查看当前数据库
show version(); 查看版本号

# SQL语句*

## DQL

数据查询语言

### select

select a from S;
select a,b from S; 查询多个字段
select a,b,c,d,e,f,g from S; 查询全部字段
select * from S; 查询全部字段(在实际开发中并不建议使用，*会把全部字段找出来然后再去查找，开发效率低，可读性差。想快速查看全表数据可以这么干)

注意：MySQL中查询的方式为两种：
1：全局扫描
2：通过索引检索

#### 完整语句

​		select            5

​              ..

​       from                     1     

​              ..

​       where                   2

​              ..

​       group by       3

​              ..

​       having           4

​              ..

​       order by        6

​		limit 			7

​              ..

#### 条件查询

语法格式：

​              select 字段,字段...  from 表名

​              where 条件; // 条件中若有字符串需使用单引号括起来。

​      		 执行顺序：先from，然后where，最后select

比较：大于小于不等于
SQL中表示不等于用<>和!=均可

范围查找：between and
between and在使用的时候必须左小右大。

查找中存在空值NULL：
空不是一个值，不能用等号衡量。
 必须使用 is null或者is not null

and 和 or：
select ename,sal,deptno from emp where sal > 1000 and (deptno = 20 or deptno = 30); // 正确的。
注意：当运算符的优先级不确定的时候加小括号。

in/not in：
select ename,job from emp
where sal in(800, 5000); // in后面的值不是区间，是具体的值。

模糊查询like：
%代表任意多个字符，_代表任意1个字符。
需查询%或\_时需用\转义

#### 分组查询

group by ... having ...
group by 分组 having 过滤(类似与where)

select 后面只能跟分组函数和group by 后面有的字段
having只能在有group by时使用，且能用where的优先用where
group by 后面可以跟多个字段进行分组

分组函数一般都会和group by联合使用，这也是为什么它被称为分组函数的原因。
并且任何一个分组函数（count sum avg max min）都是在group by语句执行结束之后才会执行的。
当一条sql语句没有group by的话，整张表的数据会自成一组。(没写group by其实还是进行分组了的)

#### 连接查询(多表)

内连接
SELECT B.A,C.D FROM B JOIN C ON [连接条件]
WHERE ...

外连接
	右连接RIGHT JOIN
	SELECT B.A,C.D FROM B RIGHT JOIN C ON [连接条件]
	// B表是主表，查询结果会把B.A都显示出来，若C中没有匹配的，则查询结果的C.D会为NULL

​	左连接LEFT JOIN
​	// 同理
加了JOIN后连接次数还是不变，只是有筛选的呈现数据。

union
union是对要连接的两组数据相加，有时union比join效率更高，join是相乘。
//查出来的要是相同列的数据

大于2张表连接
select  x from a
join b on a和b连接的条件
join c on a和c连接的条件
join d on a和d连接的条件
...

#### 子查询

select/from/where 后面出现select
select后面跟的select查询出来的记录不能超过一个，不然会报错。
子查询出来的表可以通过起别名的方法将其处理为临时表以供使用。



## DML

数据操作语言

### insert 增

insert into t_wsdsb(字段1，字段2...) values(...); //字段名和后面的values要一 一对应。
insert into t_wsdsb(a) values(1); //除了a字段以外的其它字段都为默认值(为设置默认值的字段默认为NULL)
inser into t_wsdsb values(..) //没写字段名相当于全都写上了，这里values()中要一一对应全写

插入多条：
insert into t_wsdsb values(),(),()....;

### delete 删

delete from 表名 where
// 不加where：整张表删除
delete删除不会删除数据在磁盘上的空间(可恢复：rollback；)

### update 改

update 表名 set 字段1=值1，字段2=值2.. where..
不加where：整张表更新



## DDL

数据定义语言(操作的是表的结构，不是数据)

### create
create table t_wsdsb(
a int,
b varchar(10),
c int //最后一个后面没逗号
);
表名建议以t_或tbl\_开头

#### 补充操作

##### 指定默认值

default [默认值] //不指定的话为NULL



### drop

drop table a;
drop table if exist a;

### alter

### truncate

删除
truncate table a;
效率高(速度快)，但是删完不可回复。

## TCL

事务控制语言
commit 事务提交
rollback 事务回滚

## DCL

数据控制语言
grant 授权
revoke 撤销授权

# 导入数据

source 路径名
路径中不要有中文，文件为.sql文件

# 列起别名

select a,b as B from S;
select a,b B from S; 可以省略as
select a,b as '傻逼' from S；别名中有中文要用‘’括起来

# 约束

在创建表的时候，我们可以给表中的一些字段加上约束。
分类：
列级约束：写在列后面
表级约束：写在最后

## not null

只有列级约束

## unique

不能重复，但是可以为null(null可以重复)

两个字段联合唯一：
create table t_a (
b int,
c int,
unique(b,c) //写在最后（表级约束）

);

## not null unique



## primary key*

主键：记录的唯一标识(相当于身份证)
自然主键：自然数
业务主键：与业务相关
开发中一般使用自然主键，因为主键起到标识作用即可，若与业务挂钩，业务会因客户需求更改，所以不好。

可以两个字段联合主键
但一般不用，没啥意义，一个够了。

primary key auto_increment 自增主键
自动创建主键，主键值自增。



## foreign key*

外键：相当于引用另外一张表的一个字段。外键值只能在引用表中该字段的值中。

foreign key(cno) references t_a(cno)   //表级约束，写在最后.

# 存储引擎

存储引擎：一个表存储/组织数据的方式。
查看当前MySQL支持哪些存储引擎：show engines \G
指定表的存储引擎：在创建表时，括号后面加
	create table t_a(
......

)engines=InnoDB default charset=utf-8;  //前面那个是存储引擎，后面那个是字符格式。MySQL中表的存储引擎默认为innoDB
可以用show create table t_a;查看这张表创建时的信息

# 事务*

## 概述

一个事务是一个完整的业务逻辑单元，不可再分。

mysql事务默认情况下是自动提交的。
取消自动提交:start transaction；

和事务相关的语句只有：DML语句。（insert delete update）
		为什么？因为它们这三个语句都是和数据库表当中的“数据”相关的。
		事务的存在是为了保证数据的完整性，安全性。

## 特性

事务包括四大特性：ACID
		A: 原子性：事务是最小的工作单元，不可再分。
		C: 一致性：事务必须保证多条DML语句同时成功或者同时失败。
		I：隔离性：事务A与事务B之间具有隔离。
		D：持久性：持久性说的是最终数据必须持久化到硬盘文件中，事务才算成功的结束。

## 事务的隔离性

事务隔离性存在隔离级别，理论上隔离级别包括4个：
			第一级别：读未提交（read uncommitted）——**可以读取另一个事务中未提交的数据**
				对方事务还没有提交，我们当前事务可以读取到对方未提交的数据。
				读未提交存在脏读（Dirty Read）现象：表示读到了脏的数据。
			第二级别：读已提交（read committed）——**可以读取另一个事务中提交了的数据，未提交的读不了**
				对方事务提交之后的数据我方可以读取到。
				这种隔离级别解决了: 脏读现象没有了。
				读已提交存在的问题是：不可重复读。
			第三级别：可重复读（repeatable read）——**只能读取当前事务开始时，数据库中的数据，相当于在事务开始时搞了个“快照”，另一个事务提交后仍然不可读取提交后事务的数据。**
				这种隔离级别解决了：不可重复读问题。
				这种隔离级别存在的问题是：读取到的数据是幻象。
			第四级别：序列化读/串行化读（serializable） —使用数据要排队：若事务A和事务B都在运行，事务A先运行，要事务A结束了以后，事务B才能正常运行，不然B会不动的。
				解决了所有问题。
				效率低。需要事务排队。

MySQL中默认隔离性为第三级

## 设置隔离性级别

set global transaction isolation level [等级名]；

## 查看当前隔离级别

select @@tx_isolation;
MySQL中默认为repeatable read

# 排序

order by：
asc 升序(默认)，desc 降序
select ename,sal from emp order by sal desc , ename asc;
注意：越靠前的字段越能起到主导作用。只有当前面的字段无法完成排序的时候，才会启用后面的字段。(先排前面的)

# 分组函数

count 计数
sum 求和
avg 平均值
max 最大值
min 最小值

记住：所有的分组函数都是对“某一组”数据进行操作的。
分组函数不可直接使用在where子句当中
分组函数还有另一个名字：多行处理函数。
多行处理函数的特点：输入多行，最终输出的结果是1行。
分组函数自动忽略NULL。

# 单行处理函数

ifnull() 空处理函数
fnull(可能为NULL的数据,被当做什么处理) ： 属于单行处理函数。重点：所有数据库都是这样规定的，只要有NULL参与的运算结果一定是NULL。
 使用ifnull函数：
select ename,(sal+ifnull(comm,0))*12 as yearsal from emp;

# distinct去重

select distinct A from B;
select C,distinct A from B;  //不能这样用！！！
select distict A,B from C; //这样表示两个字段联合起来去重

# 用查询结果创建表

create table b as select * from a;
create table b  as select a1 from a;

# 将查询结果插入表中

insert into a select * from b;

# Limit*

## 语法

limit startindex,length
limit length //从0开始显示length条记录
// startindex 开始的下标(默认为0)
//length 显示记录的长度

## 分页

每页显示n条记录：
第x页：limit (x-1)*n,n

# 索引

## 概念

索引底层采用的数据结构是：B + Tree

### 索引的实现原理
​		通过B Tree缩小扫描范围，底层索引进行了排序，分区，索引会携带数据在表中的“物理地址”，
​		最终通过索引检索到数据之后，获取到关联的物理地址，通过物理地址定位表中的数据，效率
​		是最高的。
​			select ename from emp where ename = 'SMITH';
​		通过索引转换为：
​			select ename from emp where 物理地址 = 0x3;

### 索引的分类
​		单一索引：给单个字段添加索引
​		复合索引: 给多个字段联合起来添加1个索引
​		主键索引：主键上会自动添加索引
​		唯一索引：有unique约束的字段上会自动添加索引

### 注意

PK和unique的字段自动添加索引。

select ename,sal from emp where ename = 'SMITH';
当ename字段上没有添加索引的时候，以上sql语句会进行全表扫描，扫描ename字段中所有的值。
当ename字段上添加索引的时候，以上sql语句会根据索引扫描，快速定位。

索引虽然可以提高检索效率，但是不能随意的添加索引，因为索引也是数据库当中
的对象，也需要数据库不断的维护。是有维护成本的。比如，表中的数据经常被修改
这样就不适合添加索引，因为数据一旦修改，索引需要重新排序，进行维护。

## 创建/删除

创建索引：
create index 索引名 on 表名(字段名)；

删除索引：
drop index 索引名 on 表名；

## 查看SQL语句执行计划

explain select ename,sal from emp where sal = 5000;
+----+-------------+-------+------+---------------+---------------+---------+-------+------+-------------+
		| id | select_type | table | type | possible_keys | key           | key_len | ref   | rows | Extra       |
		+----+-------------+-------+------+---------------+---------------+---------+-------+------+-------------+
		|  1 | SIMPLE      | emp   | ref  | emp_sal_index | emp_sal_index | 9       | const |    1 | Using where |
		+----+-------------+-------+------+---------------+---------------+---------+-------+------+-------------+

type字段为red代表该sal字段有索引，并在该语句执行中生效。(若是PK或unique的字段则为const)

## 索引失效的情况

1：模糊查询时一个通配符使用的是%
select ename from emp where ename like '%A';

2：使用or
使用or时，两边字段必须都有索引。如果有一个没有，另外一个字段的索引也会失效。

3：使用复合索引查找时没有用最左字段

4：where中索引列参加了运算

5：where中索引列使用了函数

# 视图

## 概述

站在不同的角度去看到数据。（同一张表的数据，通过不同的角度去看待）。
对视图进行增删改查，会影响到原表数据。（通过视图影响原表数据的，不是直接操作的原表）
可以对视图进行CRUD操作。
注意：只有DQL语句才能以视图对象的方式创建出来。

## 创建/删除

create view myview as select empno,ename from emp;
drop view myview;

## 视图的作用

方便，简化开发，利于维护。(view相当于对创建表的SQL语句进行了封装)
视图可以隐藏表的实现细节。保密级别较高的系统，数据库只对外提供相关的视图，java程序员
只对视图对象进行CRUD。

# DBA命令

## 导入/导出

导入：登录MYSQL数据库管理系统之后执行：source [文件绝对路径]

导出：在windows的dos命令窗口(Linux终端)中执行：mysqldump 数据库名 [表名]> 导出的文件的绝对路径 -uroot –p[密码]    //或者-p后面不输密码，系统会让你输的。

## 其它命令

其它命令要用的时候搜一下就好了。

# 数据库设计三范式*

## 概述

什么是设计范式？
		设计表的依据。按照这个三范式设计的表不会出现数据冗余。

第一范式：任何一张表都应该有主键，并且每一个字段原子性不可再分。(有主键，且一个字段不可分为两个字段)

第二范式：建立在第一范式的基础之上，所有非主键字段完全依赖主键，不能产生部分依赖。
			多对多？三张表，关系表两个外键。(每个字段都得依赖主键)

第三范式：建立在第二范式的基础之上，所有非主键字段直接依赖主键，不能产生传递依赖。
			一对多？两张表，多的表加外键。(一个字段只能依赖主键，不能依赖表中的其它字段)

## 注意

三规范不是绝对的，理论和实际是有偏差的。
在实际的开发中，以满足客户的需求为主，有的时候会拿冗余换执行速度。

# 注意

## sql语句以“；”结尾

mysql语句不见‘“；”不结束
若输入错误可以用\c中止
也可以直接输入；但是可能会报错

## SQL语句不区分大小写

## 字符串用‘’括起来

标准sql语句中要求字符串使用单引号括起来。虽然mysql支持双引号，尽量别用。

## 日期也可以降序，升序

