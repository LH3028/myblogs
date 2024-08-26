# mysql常用命令

### 1、连接Mysql





**1、连接到本机上的MYSQL。** 

首先打开DOS窗口，然后进入目录mysql\bin，再键入命令mysql -u root -p，回车后提示你输密码.注意用户名前可以有空格也可以没有空格，但是密码前必须没有空格，否则让你重新输入密码。
如果刚安装好MYSQL，超级用户root是没有密码的，故直接回车即可进入到MYSQL中了，MYSQL的提示符是： mysql>
**2、连接到远程主机上的MYSQL。**

假设远程主机的IP为：110.110.110.110，用户名为root,密码为abcd123。则键入以下命令：   mysql -h110.110.110.110 -u root -p 123;（注:u与root之间可以不用加空格，其它也一样）
**3、退出MYSQL命令**： exit （回车）

 

### 2、修改密码

格式：mysqladmin -u用户名 -p旧密码 password 新密码
**1、给root加个密码ab12。** 首先在DOS下进入目录mysql\bin，然后键入以下命令   mysqladmin -u root -password ab12 注：因为开始时root没有密码，所以-p旧密码一项就可以省略了。
**2、再将root的密码改为djg345。**   mysqladmin -u root -p ab12 password djg345



### 3、增加新用户

注意：和上面不同，下面的因为是MYSQL环境中的命令，所以后面都带一个分号作为命令结束符
格式：grant select on 数据库.* to 用户名@登录主机 identified by “密码”
**1、增加一个用户test1密码为abc，让他可以在任何主机上登录，并对所有数据库有查询、插入、修改、删除的权限。首先用root用户连入MYSQL，然后键入以下命令：**   grant select,insert,update,delete on *.* to [email=test1@”%]test1@”%[/email]” Identified by “abc”;
但增加的用户是十分危险的，你想如某个人知道test1的密码，那么他就可以在internet上的任何一台电脑上登录你的mysql数据库并对你的数据可以为所欲为了，解决办法见2。
**2、增加一个用户test2密码为abc,让他只可以在localhost上登录，并可以对数据库mydb进行查询、插入、修改、删除的操作（localhost指本地主机，即MYSQL数据库所在的那台主机）**，这样用户即使用知道test2的密码，他也无法从internet上直接访问数据库，只能通过MYSQL主机上的web页来访问了。   grant select,insert,update,delete on mydb.* to [email=test2@localhost]test2@localhost[/email] identified by “abc”;
如果你不想test2有密码，可以再打一个命令将密码消掉。   grant select,insert,update,delete on mydb.* to [email=test2@localhost]test2@localhost[/email] identified by “”;



### 4、 创建数据库

注意：创建数据库之前要先连接Mysql服务器
命令：create database <数据库名>
**例1：建立一个名为xhkdb的数据库**   mysql> create database xhkdb;
**例2：创建数据库并分配用户**
①CREATE DATABASE 数据库名;
②GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER ON 数据库名.* TO 数据库名@localhost IDENTIFIED BY '密码';
③SET PASSWORD FOR '数据库名'@'localhost' = OLD_PASSWORD('密码');
依次执行3个命令完成数据库创建。注意：中文 “密码”和“数据库”是户自己需要设置的。



### 4.2 显示数据库

命令：show databases （注意：最后有个s） mysql> show databases;
注意：为了不再显示的时候乱码，要修改数据库默认编码。以下以GBK编码页面为例进行说明：
**1、修改MYSQL的配置文件：**my.ini里面修改default-character-set=gbk **2、代码运行时修改：**   ①Java代码：jdbc:mysql://localhost:3306/test?useUnicode=true&characterEncoding=gbk   ②PHP代码：header("Content-Type:text/html;charset=gb2312");   ③C语言代码：int mysql_set_character_set( MYSQL * mysql, char * csname)； 该函数用于为当前连接设置默认的字符集。字符串csname指定了1个有效的字符集名称。连接校对成为字符集的默认校对。该函数的工作方式与SET NAMES语句类似，但它还能设置mysql- > charset的值，从而影响了由mysql_real_escape_string() 设置的字符集。

### 4.3 删除数据库

命令：drop database <数据库名> 例如：删除名为 xhkdb的数据库 mysql> drop database xhkdb;
例子1：删除一个已经确定存在的数据库   mysql> drop database drop_database;   Query OK, 0 rows affected (0.00 sec)
例子2：删除一个不确定存在的数据库   mysql> drop database drop_database;   ERROR 1008 (HY000): Can't drop database 'drop_database'; database doesn't exist    //发生错误，不能删除'drop_database'数据库，该数据库不存在。   mysql> drop database if exists drop_database;   Query OK, 0 rows affected, 1 warning (0.00 sec)//产生一个警告说明此数据库不存在   mysql> create database drop_database;   Query OK, 1 row affected (0.00 sec)   mysql> drop database if exists drop_database;//if exists 判断数据库是否存在，不存在也不产生错误   Query OK, 0 rows affected (0.00 sec)

### 4.4 连接数据库

命令： use <数据库名>
例如：如果xhkdb数据库存在，尝试存取它：   mysql> use xhkdb; 屏幕提示：Database changed
**use 语句可以通告MySQL把db_name数据库作为默认（当前）数据库使用，用于后续语句。**该数据库保持为默认数据库，直到语段的结尾，或者直到发布一个不同的USE语句：   mysql> USE db1;   mysql> SELECT COUNT(*) FROM mytable;  # selects from db1.mytable   mysql> USE db2;   mysql> SELECT COUNT(*) FROM mytable;  # selects from db2.mytable
**使用USE语句为一个特定的当前的数据库做标记，不会阻碍您访问其它数据库中的表。**下面的例子可以从db1数据库访问作者表，并从db2数据库访问编辑表：   mysql> USE db1;   mysql> SELECT author_name,editor_name FROM author,db2.editor     ->    WHERE author.editor_id = db2.editor.editor_id;
USE语句被设立出来，用于与Sybase相兼容。
有些网友问到，连接以后怎么退出。其实，不用退出来，use 数据库后，使用show databases就能查询所有数据库，如果想跳到其他数据库，用   use 其他数据库名字 就可以了。

### 4.5 当前选择的数据库

命令：mysql> select database();
MySQL中SELECT命令类似于其他编程语言里的print或者write，你可以用它来显示一个字符串、数字、数学表达式的结果等等。如何使用MySQL中SELECT命令的特殊功能？
**1.显示MYSQL的版本** mysql> select version(); +-----------------------+ | version()       | +-----------------------+ | 6.0.4-alpha-community | +-----------------------+ 1 row in set (0.02 sec) 
**2. 显示当前时间** mysql> select now(); +---------------------+ | now()        | +---------------------+ | 2009-09-15 22:35:32 | +---------------------+ 1 row in set (0.04 sec) 
**3. 显示年月日** SELECT DAYOFMONTH(CURRENT_DATE); +--------------------------+ | DAYOFMONTH(CURRENT_DATE) | +--------------------------+ |            15 | +--------------------------+ 1 row in set (0.01 sec)   SELECT MONTH(CURRENT_DATE); +---------------------+ | MONTH(CURRENT_DATE) | +---------------------+ |          9 | +---------------------+ 1 row in set (0.00 sec)   SELECT YEAR(CURRENT_DATE); +--------------------+ | YEAR(CURRENT_DATE) | +--------------------+ |        2009 | +--------------------+ 1 row in set (0.00 sec) 
**4. 显示字符串** mysql> SELECT "welecome to my blog!"; +----------------------+ | welecome to my blog! | +----------------------+ | welecome to my blog! | +----------------------+ 1 row in set (0.00 sec) 
**5. 当计算器用** select ((4 * 4) / 10 ) + 25; +----------------------+ | ((4 * 4) / 10 ) + 25 | +----------------------+ |        26.60 | +----------------------+ 1 row in set (0.00 sec) 
**6. 串接字符串** select CONCAT(f_name, " ", l_name) AS Name from employee_data where title = 'Marketing Executive'; +---------------+ | Name     | +---------------+ | Monica Sehgal | | Hal Simlai  | | Joseph Irvine | +---------------+ 3 rows in set (0.00 sec) 注意：这里用到CONCAT()函数，用来把字符串串接起来。另外，我们还用到以前学到的AS给结果列'CONCAT(f_name, " ", l_name)'起了个假名。





### 5.1 创建数据表

命令：create table <表名> ( <字段名1> <类型1> [,..<字段名n> <类型n>]);
例如，建立一个名为MyClass的表，

| 字段名 | 数字类型 | 数据宽度 | 是否为空 | 是否主键    | 自动增加       | 默认值 |
| ------ | -------- | -------- | -------- | ----------- | -------------- | ------ |
| id     | int      | 4        | 否       | primary key | auto_increment |        |
| name   | char     | 20       | 否       |             |                |        |
| sex    | int      | 4        | 否       |             |                | 0      |
| degree | double   | 16       | 是       |             |                |        |

mysql> **create****table** MyClass( > id int(4) not null **primary key auto_increment**, > name char(20) not null, > sex int(4) not null **default** '0', > degree double(16,2));

### 5.3 删除数据表

命令：drop table <表名>
例如：删除表名为 MyClass 的表   mysql> drop table MyClass;
DROP TABLE用于取消一个或多个表。您必须有每个表的DROP权限。所有的表数据和表定义会被取消，所以使用本语句要小心！
注意：对于一个带分区的表，DROP TABLE会永久性地取消表定义，取消各分区，并取消储存在这些分区中的所有数据。DROP TABLE还会取消与被取消的表有关联的分区定义（.par）文件。
对与不存在的表，使用IF EXISTS用于防止错误发生。当使用IF EXISTS时，对于每个不存在的表，会生成一个NOTE。
RESTRICT和CASCADE可以使分区更容易。目前，RESTRICT和CASCADE不起作用。

### 5.4 表插入数据

命令：insert into <表名> [( <字段名1>[,..<字段名n > ])] values ( 值1 )[, ( 值n )]
例如：往表 MyClass中插入二条记录, 这二条记录表示：编号为1的名为Tom的成绩为96.45, 编号为2 的名为Joan 的成绩为82.99， 编号为3 的名为Wang 的成绩为96.5。   mysql> insert into MyClass values(1,'Tom',96.45),(2,'Joan',82.99), (2,'Wang', 96.59);
注意：insert into每次只能向表中插入一条记录。

### 5.5 查询表中的数据

**1)、查询所有行** 命令： select <字段1，字段2，...> from < 表名 > where < 表达式 > 例如：查看表 MyClass 中所有数据   mysql> select * from MyClass;
**2）、查询前几行数据** 例如：查看表 MyClass 中前2行数据 mysql> select * from MyClass order by id limit 0,2;
select一般配合where使用，以查询更精确更复杂的数据。

### 5.6 删除表中数据

 

 

 

命令：delete from 表名 where 表达式
例如：删除表 MyClass中编号为1 的记录 mysql> delete from MyClass where id=1;
下面是一个删除数据前后表的对比。

| FirstName | LastName | Age  |
| --------- | -------- | ---- |
| Peter     | Griffin  | 35   |
| Glenn     | Quagmire | 33   |

下面以PHP代码为例删除 "Persons" 表中所有 LastName='Griffin' 的记录：

```
<?php 
   $con = mysql_connect("localhost","peter","abc123"); 
   if (!$con) 
   {
      die('Could not connect: ' . mysql_error()); 
   } 
   mysql_select_db("my_db", $con); 
   mysql_query("DELETE FROM Persons WHERE LastName='Griffin'"); mysql_close($con); 
?>
```

在这次删除之后，表是这样的：

| FirstName | LastName | Age  |
| --------- | -------- | ---- |
| Glenn     | Quagmire | 33   |

### 5.7 修改表中数据

语法：update 表名 set 字段=新值,… where 条件   mysql> update MyClass set name='Mary' where id=1;
**例子1：单表的MySQL UPDATE语句：**   UPDATE [LOW_PRIORITY] [IGNORE] tbl_name SET col_name1=expr1 [, col_name2=expr2 ...] [WHERE where_definition] [ORDER BY ...] [LIMIT row_count]
**例子2：多表的UPDATE语句：** UPDATE [LOW_PRIORITY] [IGNORE] table_references SET col_name1=expr1 [, col_name2=expr2 ...] [WHERE where_definition]
UPDATE语法可以用新值更新原有表行中的各列。SET子句指示要修改哪些列和要给予哪些值。WHERE子句指定应更新哪些行。如果没有WHERE子句，则更新所有的行。如果指定了ORDER BY子句，则按照被指定的顺序对行进行更新。LIMIT子句用于给定一个限值，限制可以被更新的行的数目。

 

### 5.8 增加字段

命令：**alter table** 表名 **add**字段 类型 其他; 例如：在表MyClass中添加了一个字段passtest，类型为int(4)，默认值为0   mysql> **alter table** MyClass **add** passtest **int(**4**) default** '0'
**加索引**   mysql> alter table 表名 add index 索引名 (字段名1[，字段名2 …]); 例子： mysql> alter table employee add index emp_name (name);
**加主关键字的索引**  mysql> alter table 表名 add primary key (字段名); 例子： mysql> alter table employee add primary key(id);
**加唯一限制条件的索引**   mysql> alter table 表名 add unique 索引名 (字段名); 例子： mysql> alter table employee add unique emp_name2(cardnumber);
**删除某个索引**   mysql> alter table 表名 drop index 索引名; 例子： mysql>alter table employee drop index emp_name;
**增加字段：** mysql> ALTER TABLE table_name ADD field_name field_type;
**修改原字段名称及类型：** mysql> ALTER TABLE table_name CHANGE old_field_name new_field_name field_type;
**删除字段：** MySQL ALTER TABLE table_name DROP field_name;

### 5.9 修改表名

命令：rename table 原表名 to 新表名;
例如：在表MyClass名字更改为YouClass   mysql> rename table MyClass to YouClass;
当你执行 RENAME 时，你不能有任何锁定的表或活动的事务。你同样也必须有对原初表的 ALTER 和 DROP 权限，以及对新表的 CREATE 和 INSERT 权限。
如果在多表更名中，MySQL 遭遇到任何错误，它将对所有被更名的表进行倒退更名，将每件事物退回到最初状态。
RENAME TABLE 在 MySQL 3.23.23 中被加入。

### 6、备份数据库

命令在DOS的[url=file://\\mysql\\bin]\\mysql\\bin[/url]目录下执行
**1.导出整个数据库** 导出文件默认是存在mysql\bin目录下   mysqldump -u 用户名 -p 数据库名 > 导出的文件名   mysqldump -u user_name -p123456 database_name > outfile_name.sql
**2.导出一个表**   mysqldump -u 用户名 -p 数据库名 表名> 导出的文件名   mysqldump -u user_name -p database_name table_name > outfile_name.sql
**3.导出一个数据库结构**   mysqldump -u user_name -p -d –add-drop-table database_name > outfile_name.sql   -d 没有数据 –add-drop-table 在每个create语句之前增加一个drop table
**4.带语言参数导出**   mysqldump -uroot -p –default-character-set=latin1 –set-charset=gbk –skip-opt database_name > outfile_name.sql
例如，将aaa库备份到文件back_aaa中： 　　[root@test1 root]# cd　/home/data/mysql 　　[root@test1 mysql]# mysqldump -u root -p --opt aaa > back_aaa

### 7.1 一个建库和建表的实例1

drop database if exists school; //如果存在SCHOOL则删除 SCHOOL 

create database school; //建立库SCHOOL 

use school; //打开库

create table teacher //建立表TEACHER 

(   id int(3) auto_increment not null primary key,   

name char(10) not null,   

address varchar(50) default ‘深圳’,  

 year date ); //建表结束
//以下为插入字段 

insert into teacher values(”,’allen’,'大连一中’,'1976-10-10′); 

insert into teacher values(”,’jack’,'大连二中’,'1975-12-23′);
如果你在mysql提示符键入上面的命令也可以，但不方便调试。 1、你可以将以上命令原样写入一个文本文件中，假设为school.sql，然后复制到c:\\下，并在DOS状态进入目录[url=file://\\mysql\\bin]\\mysql\\bin[/url]，然后键入以下命令：   mysql -uroot -p密码 < c:\\school.sql 如果成功，空出一行无任何显示；如有错误，会有提示。（以上命令已经调试，你只要将//的注释去掉即可使用）。
2、或者进入命令行后使用 mysql> source c:\\school.sql; 也可以将school.sql文件导入数据库中。

### 7.2 一个建库和建表的实例2

drop database if exists school; //如果存在SCHOOL则删除

 create database school; //建立库SCHOOL 

use school; //打开库SCHOOL 

create table teacher //建立表TEACHER 

(   

id int(3) auto_increment not null primary key,  

 name char(10) not null,   

address varchar(50) default ''深圳'',  

 year date ); //建表结束
//以下为插入字段

 insert into teacher values('''',''glchengang'',''深圳一中'',''1976-10-10''); 

insert into teacher values('''',''jack'',''深圳一中'',''1975-12-23'');
注：在建表中 1、将ID设为长度为3的数字字段:int(3)；并让它每个记录自动加一:auto_increment；并不能为空:not null；而且让他成为主字段primary key。
2、将NAME设为长度为10的字符字段
3、将ADDRESS设为长度50的字符字段，而且缺省值为深圳。
4、将YEAR设为日期字段。





# mysql-内连接、左连接、右连接以及全连接查询



####  一、内连接查询

##### 关键字：inner join on

##### 语句：select *from a_table a inner join b_table b on a.a_is=b.b_id

**说明**：组合两个表中的记录，返回关联字段相符的记录，也就是返回两个表的交集（阴影）部分。

![img](https://s2.loli.net/2022/03/09/npUjMXT1iHQN7DW.png)



![image-20211027165539105](https://s2.loli.net/2022/03/09/QC8MPXdA9b1NfUj.png)



#### 二、左连接查询 left join

##### 关键字：left join on / left outer join on

##### 语句：SELECT  * FROM a_table a left join b_table b ON a.a_id = b.b_id;

##### 说明： left join 是left outer join的简写，它的全称是左外连接，是外连接中的一种。 左(外)连接，左表(a_table)的记录将会全部表示出来，而右表(b_table)只会显示符合搜索条件的记录。右表记录不足的地方均为NULL

<img src="https://s2.loli.net/2022/03/09/rbAgTLIOyKjsH5h.png" alt="img" style="zoom:150%;" />

![image-20211027170527822](https://s2.loli.net/2022/03/09/MZDuT3BftkPVUCQ.png)

#### 三、右连接 right join

##### 关键字：right join on / right outer join on

##### 语句：SELECT  * FROM a_table a right outer join b_table b on a.a_id = b.b_id;

##### 说明：right join是right outer join的简写，它的全称是右外连接，是外连接中的一种。与左(外)连接相反，右(外)连接，左表(a_table)只会显示符合搜索条件的记录，而右表(b_table)的记录将会全部表示出来。左表记录不足的地方均为NULL。

<img src="https://s2.loli.net/2022/03/09/uSd3nY9icWURHNe.png" alt="img" style="zoom:150%;" />



![image-20211027170746217](https://s2.loli.net/2022/03/09/k3zteYiNdPUMj5Z.png)



#### 四、全连接 union

##### 关键字：union /union all

##### 语句：(select colum1,colum2...columN from tableA ) union (select colum1,colum2...columN from tableB )

         或 (select colum1,colum2...columN from tableA ) union all (select colum1,colum2...columN from tableB )；

union语句注意事项：

```sql
     1.通过union连接的SQL它们分别单独取出的列数必须相同；

     2.不要求合并的表列名称相同时，以第一个sql 表列名为准；

     3.使用union 时，完全相等的行，将会被合并，由于合并比较耗时，一般不直接使用 union 进行合并，而是通常采用union all 进行合并；

     4.被union 连接的sql 子句，单个子句中不用写order by ，因为不会有排序的效果。但可以对最终的结果集进行排序；

       (select id,name from A order by id) union all (select id,name from B order by id); //没有排序效果

       (select id,name from A ) union all (select id,name from B ) order by id; //有排序效果
```

<img src="https://s2.loli.net/2022/03/09/7Au6Ywxc9n8GjdZ.png" alt="image-20211027171337107" style="zoom:150%;" />





# **MYSQL 单表、多表查询**



笛卡尔积（或交叉连接）:
笛卡尔乘积是一个数学运算。假设我有两个集合 X 和 Y，那么 X 和 Y 的笛卡尔积就是 X 和 Y 的所有可能组合，也就是第一个对象来自于 X，第二个对象来自于 Y 的所有可能。组合的个数即为两个集合中元素个数的乘积数。
使用 CROSS JOIN表示交叉连接。它的作用就是可以把任意表进行连接，即使这两张表不相关。

### 1.多表联查

多表查询，也称为关联查询，指两个或更多个表一起完成查询操作。

前提条件：这些一起查询的表之间是有关系的（一对一、一对多），它们之间一定是有关联字段，这个关联字段可能建立了外键，也可能没有建立外键。

```mysql
SELECT	table1.column, table2.column
FROM	table1, table2
WHERE	table1.column1 = table2.column2;  #连接条件
```



#### 1.等值连接和非等值连接

```mysql
SELECT employees.employee_id, employees.last_name, 
       employees.department_id, departments.department_id,
       departments.location_id
FROM   employees, departments
WHERE  employees.department_id = departments.department_id;
```


表的别名：使用别名可以简化查询。列名前使用表名前缀可以提高查询效率。
使用别名后：

```mysql
SELECT e.employee_id, e.last_name, e.department_id,
       d.department_id, d.location_id
FROM   employees e , departments d
WHERE  e.department_id = d.department_id;
```


等值：是where条件那一行在两表中的值是相等的。
非等值：是where条件那一行的值不与另一表中的行相等，而是其他关系。

非等值例子：EMPLOYEES表中员工工资应在JOB_GRADES表的最高工资和最低工资之间。

```mysql
SELECT e.last_name, e.salary, j.grade_level
FROM   employees e, job_grades j
WHERE  e.salary BETWEEN j.lowest_sal AND j.highest_sal;
```



#### 2.自连接

当table1和table2本质上是同一张表，只是用取别名的方式虚拟成两张表以代表不同的意义。然后两个表再进行内连接，外连接等查询。

```mysql
SELECT CONCAT(worker.last_name ,' works for ' 
       , manager.last_name)
FROM   employees worker, employees manager
WHERE  worker.manager_id = manager.employee_id ;
```



#### 3.内连接&外连接

内连接: 合并具有同一列的两个以上的表的行, **结果集中不包含一个表与另一个表不匹配的行**

外连接: 两个表在连接过程中除了**返回满足连接条件的行以外还返回左（或右）表中不满足条件的行** ，这种连接称为左（或右） 外连接。没有匹配的行时, 结果表中相应的列为空(NULL)。

如果是左外连接，则连接条件中**左边的表也称为主表**，右边的表称为从表。

如果是右外连接，则连接条件中**右边的表也称为主表**，左边的表称为从表。

### 9种Join方式

![在这里插入图片描述](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261454301.png)

#### （1）inner

```mysql
SELECT  o.order_id, o.customer_id, o.order_date, o.amount, c.customer_name
FROM orders o
INNER JOIN customers c
ON o.customer_id = c.customer_id;
```


不包含不匹配的，指的是行，不是列属性。

![在这里插入图片描述](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261455754.png)

#### （2）LEFT JOIN

左外连接，则连接条件中左边的表也称为主表，右边的表称为从表。

```mysql
SELECT  o.order_id, o.customer_id, c.customer_id, o.order_date, o.amount, c.customer_name
FROM orders o
LEFT JOIN customers c
ON o.customer_id = c.customer_id;
```

![在这里插入图片描述](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261455683.png)



#### （4）RIGHT JION

右外连接，则连接条件中右边的表也称为主表，左边的表称为从表。

#### （5）LEFT JOIN WHERE IS NULL

左为主表，把两个表相同的部分行扣去

```mysql
SELECT  o.order_id, o.customer_id, c.customer_id, o.order_date, o.amount, c.customer_name
FROM orders o
LEFT JOIN customers c
ON o.customer_id = c.customer_id;
WHERE c.customer_id IS NULL
```



#### （6）RIGHT JOIN WHERE IS NULL

右为主表，把两个表相同的部分行扣去

##### UNION

合并查询结果
利用UNION关键字，将多条SELECT语句的结果组合成单个结果集。合并时，两个表对应的列数和数据类型必须相同，并且相互对应。各个SELECT语句之间使用UNION或UNION ALL关键字分隔。

- UNION 操作符返回两个查询的结果集的并集，去除重复记录。
- UNION ALL操作符返回两个查询的结果集的并集。对于两个结果集的重复部分，不去重。

这个博客介绍得很详细，例子也很清楚 [MYSQL多表查询](https://blog.csdn.net/weixin_42894555/article/details/137727363)

### 2.单表查询

```mysql
select 
    字段列表
from 
    表名列表 
where 
    条件列表
group by
    分组字段
having
    分组后条件
order by
    排序字段
limit
    分页限定
```

#### 条件查询

![在这里插入图片描述](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261459852.png)

```mysql
查询年龄等于18岁 或者 年龄等于20岁 或者 年龄等于22岁的学员信息

select * from stu where age = 18 or age = 20 or age = 22;
select * from stu where age in (18,20 ,22);

null值的比较不能使用 = 或者 != 。需要使用 is 或者 is not

select * from stu where english is null;
select * from stu where english is not null;
```



#### 模糊查询

模糊查询使用like关键字，可以使用通配符进行占位:

（1）_ : 代表单个任意字符

（2）% : 代表任意个数字符

```mysql
select * from stu where name like '_花%';
```



#### 排序查询

select 字段列表 from 表名 order by 排序字段名1 [排序方式1],排序字段名2 [排序方式2] …;
ASC ： 升序排列 （默认值）
DESC ： 降序排列
注：如果有多个排序条件，当前边的条件值一样时，才会根据第二条件进行排序

```mysql
查询学生信息，按照年龄升序排列
select * from stu order by age ;

查询学生信息，按照数学成绩降序排列

select * from stu order by math desc ;

查询学生信息，按照数学成绩降序排列，如果数学成绩一样，再按照英语成绩升序排列

select * from stu order by math desc , english asc ;
```



#### 聚合查询

函数名 功能
count(列名) 统计数量（一般选用不为null的列）
max(列名) 最大值
min(列名) 最小值
sum(列名) 求和
avg(列名) 平均值

```mysql
select 聚合函数名(列名) from 表;
注意：null 值不参与所有聚合函数运算


统计班级一共有多少个学生
select count(*) from stu;

查询数学成绩的最高分
select max(math) from stu;

查询数学成绩的最低分
select min(math) from stu;

查询数学成绩的总分
select sum(math) from stu;

查询数学成绩的平均分
select avg(math) from stu;

查询英语成绩的最低分
select min(english) from stu;
```



#### 分页查询

```mysql
select 字段列表 from 表名 limit  起始索引 , 查询条目数;
```

1
起始索引计算公式：
起始索引 = (当前页码 - 1) * 每页显示的条数

```mysql
从0开始查询，查询3条数据
select * from stu limit 0 , 3;

每页显示3条数据，查询第1页数据
select * from stu limit 0 , 3;

每页显示3条数据，查询第2页数据
select * from stu limit 3 , 3;

每页显示3条数据，查询第3页数据
select * from stu limit 6 , 3;
```



### GROUP BY

GROUP BY 语句在 SQL 中用于将来自数据库表的记录分组，以便可以对每个组执行**聚合函数**（如 COUNT(), MAX(), MIN(), SUM(), AVG() 等）。使用 GROUP BY 时，数据库会根据一个或多个列的值将结果集分为多个分组，在每个分组内可以独立地使用聚合函数。GROUP BY 通常与 SELECT 语句一起使用，以汇总每个分组的数据。
也就是说：分组查询是当我们需要按照某一类汇总时所做操作。

![在这里插入图片描述](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261502799.png)

例1：
假设有一个 orders 表，其中包含 order_date 和 amount 列。如果我们想知道每个日期的总销售额

```mysql
SELECT order_date, SUM(amount)
FROM orders
GROUP BY order_date;
```


根据 order_date 列的值将 orders 表中的记录分组，并计算每个日期的总销售额。

例2：
假设有一个名为 employees 的表，它有 department 和 salary 两列。如果你想知道每个部门的平均薪资，并按部门名排序，你的 SQL 语句可能如下：

```mysql
SELECT department, AVG(salary)
FROM employees
WHERE salary > 0
GROUP BY department
ORDER BY department;
```


上难度



![在这里插入图片描述](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261502827.png)

1.查询names字段出现次数最多的一个

```mysql
select names,count(names) as number from ceshi GROUP BY names ORDER BY count(names) desc
```

![在这里插入图片描述](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261503058.png)







