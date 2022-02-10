### 1.约束

非空约束（not null）//不能为null

唯一约束（unique）//不能重复

主键约束（primary key）//既不能重复，也不能为null

外键约束（foreigh key）//

唯一约束 不能重复但是可以为null

create table t_user (

	id int ,

	usercode varchar(255),

	username varchar(255),

	unique (username ,usercode)

//只要usernam，usercode不同时一样就行

主键约束（PK）

drop table if exists t_user;

create table t_user(

	id int primary key,

	username varchar(255),

	email varchar(255)

);

insert into t_user (id,username,email) values (1,'wu','2173015865@qq.com');

insert into t_user (id,username,email)values(1,'jin','8008120458@emil.egn.cn');

select * from t_user;

主键划分

主键约束 

主键字段

主键值

主键自增primary key aut_

外键

drop table if exists t_student;

drop table if exists t_class;

<br/>

create table t_class(

	con int,

	cname varchar(255),

	primary key (cno)

);

create table t_students(

	sno int,

	sname varchar(255),

	classno int,

	primary key (sno),

	foreigh key (classno) references t_class(cno)

);

insert into t_class values(101,'wujinjke');

<br/>

### 2.存储引擎

show engines \G

create table `t_x`(

	`id` int (11) DEFAULT NULL

) ENGING=储存引擎 DEFAULT CHARSET = utf8;

InnoDB 安全

MyISAM 

MEMORY

### 3.事务

事务的特征？

事务包括四大特征：ACID

A:原子性：事务是最小的工作单元，不可再分。

C:一致性：事务必须保证多条DML语句同时成功或者同时失败。

I:隔离性：事务A与事务B之间具有隔离。

D:持久性：持久性说的是最终数据必须持久化到硬盘文件中，事务才算成功的结束。

<br/>

start transaction ; 关闭自动提交机制。

   rollback;//回滚

set global transaction isolation level read uncommitted;//设置隔离级别

查看隔离级别 select @@global.tx isolation;

commit； //提交

### 4.索引

创建索引对象：

	create index 索引名称 on 表名（字段名）;

删除索引对象：

	drop index 索引名称 on 表名；

什么时候考虑给字段添加索引？	

	数据量庞大。（根据客户的需求，根据线上环境）

	该字段很少的DML 操作。（因为字段进行修改操作，索引也需要维护）

	该字段经常出现在where 子句中。（经常根据那个字段查询）

查询是否有索引

	创建索引：create index emp_sal_index on emp(sal);

	explain select ename,sal from emp where sal = 5000;

索引底层采用的数据结构是：B+tree

索引原理：通过B+Tree 缩小范围，底层进行排序，分区，索引会携带数据在表中的“物理地址”，最终通过索引检索数据后，得到相对应的物理地址，通过物理地址，定向找到，数据。

索引的分类

	单一索引：给单个字段添加索引

	复合索引：多个字段联合起来添加1个索引

	主键索引：主键上会自动添加索引

	唯一索引：有unique 的约束字段上会自动添加索引

索引什么时候失效？

	select ename from emp where ename like '%A%';

索引主要根据B+Tree 进行首字母搜索，如果没有首字母就不能进行检索。

### 5.视图（view）

	创建视图

		create view myview as select empno ,ename from emp;

		drop view myview;

	视图的作用

		视图可以隐藏表的细节

### 6.DBA命令

	新建用户

	create user username identified by 'password';

	导出数据

		在window dos 窗口中执行；（不能登录）

			mysqldump 库名  //选择要导出的数据表

			\>  //指向所存放的位置的指向符号

			d:\库名.sql  //导出的sql 语句存放的路径

			-uroot -pqazxc125890 //密码

		mysqldump 库名 表名>

<br/>

	导入数据

			drop database 库名;

			create database 库名;

			use 库名;

			source sql文件路径;

### 7.数据库设计三范式（重点内容）

	1.不会出现数据冗余

	2.三范式具体内容

		第一范式：任何一张表都是应该有主键，并且每一个字段原子性不可再分。

		第二范式：建立在第一范式之上，所有非主键字段完全依赖主键，不能产生部分依赖。

			多对多，三张表，关系表中加两个外键链接。(fk)外键（PK）主键

			(任何一个数据都要和本行中的所有主键都有关系)	

			学生t_student

			cno(PK) 		cname

			\----------------------

			1					student1

			2					student2

			3					student3

			4  				student4	

			教师t_teacher

			sno(PK)		sname

			\------------------------

			101				teacher1

			102    			teacher2

			关系t_relationship

			dno(PK) 		cno(fk)			sno(fk)

			\------------------------------------

			1					1					102

			2					2					101

			3					3					101

			4					4					102

		第三范式：建立在第二范式的基础之上，所有非主键字段直接依赖主键，不能产生传递依赖。

			一对多，两张表，多的表加外键。

			班级表t_class

			cno(PK)            	cname

		\------------------------------------

			1							班级1

			2							班级2

			学生表t_student

			sno(PK) 				sname				classno(fk)

		\---------------------------------------------------

			101						张1					1

			102						张2					1

			103 						武1					1

			104 						武2					2

	提醒：拿冗余换速度 

	一对一设计

	主键共享

t_user_login 用户登录表

id(PK)			username			password

\---------------------------------------------

1					wy						123456

2                  wz                        112312

t_user_detail 用户详细信息表

id(PK+fk)         realname      tel

\------------------------------------------

1						wyk				123456789

2						wzi				123124214

//共用主键，一个主键对应的值分别在两个表里面