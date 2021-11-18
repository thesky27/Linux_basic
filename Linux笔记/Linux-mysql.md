# 第一章MySQL数据库

**以下所有操作都是在虚拟机里ubuntu的终端里运行的**

### 一、MySQL基础

### 1.数据库概念

- 存储数据的仓库——数据库管理系统——本质是一个软件，作用是管理数据
- 存储方式有很多种
  - 文本文档——格式不明确，不安全
  - 电子表格——操作速度相对于数据库管理系统来说较慢

- 数据库可以被后台语言链接进行操作——使用python操作数据库

### 2.数据库管理系统

- 有很多的数据库管理系统——关系型数据库和非关系型数据库

##### 1.关系型数据库

- 关系型数据库——数据结构：表，一般是二维表。
  - 优点：容易维护，具有统一的结构，方便使用，sql语句通用，**存在数据约束安全**
  - 缺点：读写的性能差
  - 安全与性能不能兼得

##### 2.非关系型数据库

- 非关系型数据库——数据结构：文档与键值对（字典）
  - 优点：格式灵活，速度快——redis高速度，操作完毕可持久化到硬盘
  - 缺点：安全性能较差

- MongDB——用来存储海量数据，redis——告诉存取数据库，过期时间

### 3.MySQL简介

##### 1.体积小，速度快

![image-20210712190122677](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210712190122677.png)

- MySQL的默认端口是3306，一般不会对其作修改

- service mysql status——查看MySQL的服务是否处在开启状态，图中显示active(running)就是成功了。
- 如果是关闭状态，则service mysql start就可

![image-20210712190940893](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210712190940893.png)

##### 2.第一种进入MySQL的方式

- mysql -u用户名 -p进入到输入密码界面，注意输入密码是不可见的。下面是成功登陆后的界面

![image-20210712191244758](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210712191244758.png)

##### 3.第二种进入MySQL的方式——远程连接

- mysql -h要连接的服务器的ip  -pMySQL的端口（一般是3306） -u用户名 -p	然后输入密码进入

![](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210714130501405.png)

##### 4.MySQL的命令

***注意：下面命令中的数据库名，表名和字段名都必须用反引号引起来，为了省事，下文中的表名反引号没写！！！***

- 一个数据库软件里面可以有多个数据库，一个数据库中有很多的表格，表格中会含有字段
- MySQL中所有的命令建议大写，且结尾要有分号。

###### 4.1查看创建数据库

- show databases;——查看所有的数据库
- ``create database `数据库名`——创建数据库——数据库名要用反引号引起来——不知道什么是反引号去问百度``
- ``create database if not exists `数据库名`——无就创建，有就不会执行``

![image-20210712194340182](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210712194340182.png)

- ``drop database if not exists `数据库名`——无就不操作，有就执行``
- ``use `yige`——使用yige数据库，select database();——查询当前数据库。select user();——查询当前用户``
- show tables;——查询所有表格。跨库查询——``show tables from  ` 数据库名`。``
- show create table 表名——查询当初创建该表的语句

<img src="C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210712195111226.png" alt="image-20210712195111226" style="zoom: 67%;" />

###### 4.2查看创建表

- char和varchar的区别
  - char——长度是固定的，尾部空格不会保留
  - varchar——长度是不固定的，尾部空格会保留，空间好
- ``create table 表名(`字段名` 值，`字段名` 值，......);``
- desc 表名;——查看表结构，

###### 4.3修改表

- ``alter table 表名 add `age` int;——给该表名添加int型的age字段``
- ``alter table 表名 add (`age` int,`height` int);——给该表名添加多个字段``
- ``alter table 表名 modify `age` varchar(20);——给该表名的age字段从int型更改为varchar型``
- ``alter table 表名 change `age` `ages` varchar(30);——给该表名的age更名为ages，并修改为varchar型``
- ``alter table 表名 change `age` `ages` varchar(30), change `width` `widths` int, change `height` `heights` varchar(35);——给该表名修改多个字段``——且只能用change来修改多个字段

###### 4.4删除操作

- ``alter table 表名 drop `age`;——给该表名删除age字段``
- 删除多个字段方法与修改多个相同
- drop table 表名;——删除表

###### 4.5修改表的名字

- ``alter table 表名 rename 新表名;——修改表名``

### 4.MySQL数据查询

- ``select `字段名`,`字段名`...... from  `表名`;，``
- ``select `字段名`,`字段名`...... from `表名` where 条件（如`id=1`或者 `id`>=1001或者`name`!='张三'） and（或者or）;`` 

##### 4.1取别名

- 为一个表格创建另一个名字
- ``select `s`.`字段名` from  `表名` as `s`;``——s是别名，as也可以直接去掉
- ``select `字段名` as `别名` from  `表名`，``——为一个字段起别名
- 在select后可以加上表名.字段名，取别名是临时的，在别名生效时，原名不能用。

##### 4.2.多表查询

###### 4.2.1内连接

- 主要是做了笛卡尔积的运算
- ``select  `字段名`  from  `表名`  inner join `表名`;``
- ``select  `字段名`  from  `表名` ,`表名`;``
- 但是会造成数据冗余，where是会遍历每一条数据
- 当作连接查询和筛选查询的时候用on，而不用where，用join连接两个表

###### 4.2.2左连接

- ``select  *  from  `表名1`  left join `表名2` on 条件;``
- 这会将表1的所有数据展示出来，而只展示表2中符合条件的数据，不符合条件的就会为NULL
- 从左到右，先展示表1，后展示表2
- 右连接同理——right join

###### 4.2.3全连接

- 查询语句 union 查询语句
- 将查询的结果合并到一起

###### 4.2.4对查询的结果进行处理

- 查询语句 order by 字段名 （desc）——升序（降序）
- 如果字段名是多个，则是先从左到右依次进行排序
- 查询语句 limit 数字——得到前 数字 条数据
- 查询语句 limit 数字1，数字2——得到从第数字1开始，往下查询 数字2 条数据

###### 4.2.5对查询的结果做分组

![image-20210804173945295](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210804173945295.png)

![image-20210804174108631](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210804174108631.png)



##### 5.MySQL执行顺序

![image-20210804170146821](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210804170146821.png)

##### 6.总结

- 内连接：方式是笛卡尔积，不适合多表查询
- 外连接：包括左连接、右连接、和全连接，常用左连接，全连接一般用来去重
- 其他查询：限制行数limit、排序和分组
- 子表查询：可以用join(连接)或者是where(条件)

### 5.MySQL表关系和表约束

##### 1.字段数据处理

- 插入——``insert into   `表名`  (`字段名`,`字段名`...)values (数据),(数据)...;``
- 删除——``delete from  `表名`  条件(比如where `id` =4);``

##### 2.表约束

- 非空约束——``alter table 表名 modify `age` varchar(20) not null;``——给该表名的age字段设置为·不能是空的
- 唯一约束：唯一的字段不能重复，不写会有默认值
  - 设置键名——``alter table 表名 add constraint `键名` unique key (`字段`);``
  - 如果要删除则将add改为drop，``alter table 表名 drop  key `约束名`;``
  - ``alter table 表名 add unique key (`id`);``——设置唯一键
- 主键约束：定义该字段的数据都是唯一的值并且不能为空。
  - 可先设置唯一约束，再加上非空约束，代表是PRI。
  - ``alter table 表名 add primary key (`字段名`);``
  - ``alter table 表名 drop primary key (`字段名`);``——删除时会保留非空特性
  - 如果表格没有定义主键，则第一个添加非空加唯一的视为主键
  - 此时可以继续添加主键，添加后，主键就不再是先前的那个
- 自增约束：自动编号，默认起始值为1，必须配合主键使用。
  - ``alter table 表名 change `age` `age` int auto_increment;``
  - ``alter table 表名 change `age` `age` noy null;``
- 默认约束：设置默认值
  - ``alter table 表名 alter `age` set default 18;``
  - ``alter table 表名 alter `age` drop default ;``——``alter table 表名 alter `age` set default NULL;``恢复默认状态
  - 创建表格默认字段都有默认值——NULL
- 外键约束：保持数据的完整性、一致性
  - 外键必须关联到主键，关联表中的数据类型与主键必须一致。
  - 

##### 3.表关系

- 一对多：通过外键保证数据的一致性
- 一对一：外键加唯一键
- 多对多：创建中间表进行记录

##### 4.其他补充

- CTRL+insert——复制，shift+insert——粘贴，这是对于终端来说的

表的创建——从一开始就可以赋值主键

![image-20210805150059610](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210805150059610.png)

设置一对一的关系

<img src="C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210805150923648.png" alt="image-20210805150923648" style="zoom:80%;" />

最后面的 on delete cascade关系是删除一个，一对一的另一个也会被删除

![image-20210805151311511](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210805151311511.png)

创建联合主键，也就是中间表的多对多关系

![image-20210805151625695](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210805151625695.png)

### 6.MySQL函数

- ``select  max(`字段名`)  from  `表名` ;``——max函数
- ``select  sum(`字段名`)  from  `表名` ;``——sum函数
- 同理还有count(*)，average等函数，可以直接在网上去查

### 7.MySQL优化

- 当数据量足够大时，可以通过优化执行顺序来缩短时间
- 尽量避免整表扫描如select *
- 建立合适的索引，使用适合的存储引擎
- 在join中尽量使用小表left join大表
- 除非必要，尽量不要使用order by/group by和desc去重，尽量用索引代替

### 4.事务与视图

- 将某几个·操作绑定在一起，要么全做，要么全不做
- 视图可以看作一张虚拟表，因为三范式，会存在多张表，查询语句比较复杂

