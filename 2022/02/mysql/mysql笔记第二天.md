# 连表查询

笛卡尔积现象。

两个集合x 和 y ,进行乘积，最后总和等于xy 

加条件进行过滤

SQL92 ：（太老了，不用了）

select 

   e.name,d.name

from 

	emp e ,dept d

where 

	e.deptno = d.deptno;

SQL99：（最新的）

select 

	e.ename,d.dname

from 

	emp e

join 

	dept d

on

	e.deptno =d.deptno;

<br/>

<br/>

### 自连表

##### 内连接

 内连接：不分主表和附表，如果有数值不匹配舍弃，

select 

	a.ename as '员工表'，b.ename as '领导表'

from 

	emp a

inner join 

	emp b

on 

	a.mgr =b.empno;

##### 外连接

外连接：分主副表，主表没有匹配数据的话就用NULL进行匹配

select 

	a.ename as '员工表',b.ename as '领导表'

from

	emp a

left join 

	emp b

on ---->条件，区别于where

 	a.mgr = b.empno; 

<br/>

right 就是右面是主表，left 就是左面为主表

内连接inner

外连接outer

区分用left | right

##### 全连接

既有左连接又有右链接，两个都是主表，两个都不舍弃，a表未匹配则匹配null ,b表未匹配则匹配null

<br/>

##### 子查询

select 后面能加sql（嵌套子查询）

from 后面能加sql

where 后面能加sql

---

union 能把两个表相加

select ename,job from emp where job = "MANAGER"

union

select ename ,job from emp where job="SALESMAN";

<br/>

#### limit

mysql 特有

limit starIndex ,Length

	startIndex 表示起始位置 ，从0开始，到Length-1个

select ename,sal from emp order bty sal desc limit 0,5;

分页用处大，

limit (page-1)*Length,Length;

## 创建表

create table 表名（

	字段名1 数据类型，

	字段名2 数据类型 default 数据（初始化），

	字段名3 数据类型，

	......

）；

<br/>

int   				整数型

char             定点字符串

float				浮点型

varchar		可变长度字符串

bigint			长整形

date				日期类型

BLOB			二进制大对象（存储图片，视频等流媒体信息）

CLOB			字符大对象（存储较大文本，比如，可以存储4G的字符串）

### 插入数据

insert into 表名(字段1,字段2......)values (值1,值2......)

drop table if exists t_student;//当这个表存在的时候删除

### 复制表

create table emp2 as select * from emp;

### 插入表

insert into dep1 select * from dep;

### 更新表

update 表名 set 字段名1=值1，字段名2=值2 where 条件；

如果没有条件的话就全部更新

### 删除数据

delete from 表名 where 条件；

delete from 表名 ；真整个表；--->可以回滚，效率低。

truncate table 表名；删除大表；---不能返回，永久丢失。

---

DQL(select) 

DML(insert delete update) ----->对于数据

DDL(create drop alter)-----> 对于表结构的

增删改查 术语：CRUD 操作

insert delete update select

----

### 约束

非空约束（not null）//不能为null

唯一约束（unique）//不能重复

主键约束（primary key）//既不能重复，也不能为null

外键约束（foreigh key）//