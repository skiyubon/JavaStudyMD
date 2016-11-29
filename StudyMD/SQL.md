#1.数据库概念
- 数据库就是用来储存和管理数据的仓库

#2.数据库的优点
- 可储存大量的数据
- 方便检索
- 保持数据的一致性,完整性
- 安全,可共享
- 通过组合分析,可产生新的数据

#3.数据库的发展历程
- 没有数据库,使用磁盘文件储存数据
- 层次结构模型数据库
- 网状结构模型数据库
- 关系结构模型数据库:使用二维表格来储存数据
- 关系-对象※模型数据库
- MySQL就是关系型数据库

#4.常见的数据库
- Orcale:神谕,甲骨文公司(收费的大型数据库产品,市场占有率最高)
- DB2:IBM(收费,银行系统)
- SQLServer:微软,收费的中型数据库,c# , .net等语言使用.
- Sybase:赛尔斯(要被淘汰),提供了非常专业数据建模的工具PowerDesign.
- SQLite:嵌入式的小型数据库,应用在手机端.
- MySQL:开源免费的,甲骨文收购sun收购mysql 

#5.理解数据库
- RDBMS=管理员(manager)+仓库(database)
- database=N个table
- table:
	- 表结构:定义表的列名和列类型
	- 表记录:一行一行的记录的数据

- 我们现在所说的数据库泛指"关系型数据库管理系统"RDBMS-Relational database Manager System ,即数据库服务器,它是操作和管理数据库的大型软件.
- 当我们安装了数据库服务器后,就可以在数据库服务器中创建数据库,每个数据库中包含多张表格
- 数据库表就是一个多行多列的表格,在创建表示,需要指定表的列数,以及列名称.列类型等信息.而不用指定表格的行数,行数是没有上限的.
- 当把表格创建好后.可以向表格中添加数据.向表格添加数据时一行为单位的.

- java中的类,和数据表的对应关系
	- 类->表
	- 类字段,成员变量->列(column)
	- 对象->表中的每行记录(row)
	- 用户需要数据就创建对象,不需要就销毁对象,不然浪费资源.
	

#6.应用程序和数据库
- 应用程序使用数据库完成多数据的储存!

##2.MySQL目录结构
- MySQL的数据存储目录为data，data目录通常在C:\Documents and Settings\All Users\Application Data\MySQL\MySQL Server 5.1\data位置。在data下的每个目录都代表一个数据库。
- MySQL的安装目录下：
	- bin目录中都是可执行文件；
	- my.ini文件是MySQL的配置文件；

#7.基本命令
##1.启动和关闭MySQL服务器
- 启动:net start mysql;
- 关闭:net stop mysql;
- 就是启动了mysqld.exe服务器程序

##2.客户端登陆退出MySQL
> 在启动MySQL服务器后,我们需要使用管理员登陆MySQL服务器,然后对服务器进行操作.
> 
- 在登陆成功后,打开Windows任务管理器,会有一个mysqlde.exe的进程,所以mysql.exe是客户端程序

    登陆MySQL需要使用MySQL的客户端程序:mysql.exe
	登陆:mysql -u root -p 123 -h localhost;
		* -u:后面的root是用户名,这里使用是超级管理员root;
		* -p:后面的是密码,这是在安装MySQL是就以已经指定了的密码
		* -h:后面给出的localhost是服务器的主机名,它是可以省略的
		* 退出:quit或exit


#8.SQL语句
##1.SQL语句的概念
> SQL(Structure Query Language)是"结构化查询语言",它是对关系型数据库的操作语言,它可以应用到所有关系型数据库中,mysql,Orcale,SQL Server等.SQ标准(ANSI/ISO)有:
> 
- SQL-92:1992年发布的SQL语言标准
- SQL:1999:1999年发布的SQL语言标准
- SQL:2003:2003年发布的SQL语言标准
- 新的版本中总要有一些语法的变化.不同时期的数据库对不同标准做了实现
- 虽然在SQL可以用在所有关系型数据库中,但是许多数据库还都有标准之后的一些语法,我们可以称之为:方言.方言是独有,其他数据库都不支持.

##2.语法要求
- SQL语句可以单行或者多行书写,以分号结尾
- 可以用空格和缩进来增强语句的可读性
- 关键字不区别大小写,建议使用大写
- /**/注释



##3.SQL分类
- DDL,定义语言,用来定义数据库对象:数据库,表,列等.create,alter,drop
- DML,操作语言,表中的记录更新,inset,delete,update
- DCL,控制语言,定义数据库的访问权限和安全级别及创建用户.
- DQL,查询数据语言,select

##4.数据类型
- int:整型
- double:浮点型
- varchar:var(可变),可变字符型
- data:日期类型,只有年月日,没有时分秒
- char:

##5.创建数据库
    create database 数据库名
	create database 数据库名 character set 字符集 (字符集默认已设置好)
	show databases	查看所有数据库
	drop database 数据库名	//删除数据库

##6.创建修改数据表

    create table 表名(
		列名1 数据类型 约束(可选),
		列名2 数据类型 约束,
		....
	);
	
	create table users (
		uid INT,
		uname VARCHAR(20),
		uaddress VARCHAR(200)
	);

> 约束:限制列能写什么样的数据(主键约束,非空约束,唯一约束,...)

    show tables; 查看数据库中的所有表
	desc 表名;	查看表结构
	drop 表名;	删除表
	******************************************
	alter table 表名 add 列名 数据类型 约束; //添加列,添加字段
	alter table 表名 modify 列名 数据类型 约束; //修改列,修改字段
	alter table 表名 change 旧列名 新列名 数据类型 约束;//修改列名
	alter table 表名 drop 列名
	rename table 表名 to 新名
	alter table 表名 character set 字符集;//修改字符集

##7.添加数据

	insert into 表名(列名1,列名2,列名3) values (值1,值2,值3);
	insert into 表名(列名2,类名3) values (值2,值3);	省略主键列
	insert into 表名 values (全列值);	不能省略主键值

	insert into 表名 (列名1,列名2,列名3) values (值1,值2,值3),(值1,值2,值3);		//批量写入

##8.更行数据

    update 表名 set 列1=值1,列2=值2	不加条件则修改表中全部的数据

    update 表名 set 列1=值1,列2=值2 while 条件

	/*
	修改条件的写法:
	id = 6;
	id <> 6	;		不等于6
	id <=6;
	and			//java:&&
	or			//java:||
	not			//java:!
	id in (1,3,4,5,6);	包含,not in 不包含

##9.删除数据

    delete from 表名 where 条件
	truncate table 表名

##10.查询

    查询指定列的数据
	select 列名1,列名2 from 表名	
	select * from 表名
	select distinct 列名 from 表名		//查询并去除重复记录
	select 列名 as '新名' from 表名   	//查询重新命名列
	select 列名+1000 as 'sum' from 表名	//查询中计算

	
	***********************************************
	条件查询:
	between and 	//包头包尾
	in(set)			//集合
	like 通配符	:  % 多个字符,  _一个字符		模糊查询
	is (not) null :判断是够为空
	and
	or
	not
	
	***********************************************
	查询,对结果集进行排序

	order by 列名 [asc][desc] 	[升序][降序]

	纵向查询,用集合函数
	sum
	max
	count
	min
	AVG
	
	*******************************************
	分组查询
	group by 被分组的列名,必须跟随聚合函数,要出现在select 选择列的后面
	select sum(zmoney),zname from zhangwu group by zname

	select sum(zmoney)as'getsum',zname from zhangwu where zname like '%支出%' group by zname order by getsum desc having getsum>5000
				//having ,是分组后再过滤
				//where,是分组前过滤
	
	