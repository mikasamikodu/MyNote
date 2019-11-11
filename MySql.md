# MySql

# 1.相关操作

## 1.1配置文件

### 1.1.1.my.ini

在mysql根目录下，找到mysqld。下面内容是mysql服务端相关设置。

1.port：服务器监听的的端口号；

2.basedir:mysql安装时所在目录；

3.datadir:mysql存放数据的目录；

4.character-set-server:数据库字符编码；

5.default-storage-engine:数据库存储引擎；

6.sql-mode:数据库语法模式；

7.max_conntions:服务端最大连接数；

修改该文件内容后，需重启mysql数据库方可生效。

## 1.2.服务的启动与停止

### 1.2.1.通过控制面板

控制面板的查看方式需要设置为小图标，然后启动方式是

控制面板->管理工具->服务->Mysql，右键启动即可；

关闭只需右键停止即可。

### 1.2.2.通过控制台

按window+R，输入cmd，，呼叫控制台，输入net start mysql回车即可启动mysql服务；

输入net stop mysql回车即可关闭mysql服务。

## 1.3.进入服务端

### 1.3.1.通过客户端

按window键，点击所有程序，找到MySql，下面有客户端，双击打开会出现一个黑色控制台。这里打开的是root用户，输入root的密码即可登录。需要退出时可以按Ctrl+C或输入exit。

### 1.3.2.通过控制台

按window+R，输入cmd，呼叫控制台，输入mysql -h localhost -p 3306 -u 用户名 -p回车，输入密码，即可进入mysql数据库。也可输入mysql -u 用户名 -p回车，输入密码进入。需要退出时可以按Ctrl+C或输入exit。

### 1.3.3.注意

如果无法登录，则可能是Mysql环境变量配置有问题。找到系统环境变量Path，将Mysql的安装目录放在Path路径中最前面，并与下一个值用分号隔开。配置完成需要重新启动服务。

## 1.4.查看mysql版本

1.在控制台进入数据库后输入`select version();` 回车即可查看mysql数据库版本。

![1570453121406](E:\typora-document\MyNote\images\1570453121406.png)



2.在控制台输入`mysql --version` 回车即可查看mysql数据库版本。

![1570453216447](E:\typora-document\MyNote\images\1570453216447.png)



## 1.5.语法规范

1.不区分大小写，建议关键字大写，列名、表名小写；

2.每条命令以分号(;)结尾；

3.每条命令根据需要进行缩进或换行；

4.写sql查询语句时，表名、列名可以用着重号(``)进行包裹，以表示这不是一个关键字；

5.注释

+ 单行注释：#注释
+ 单行注释：-- 注释(-与注释之间有空格)
+ 多行注释：/* 注释 */

# 2.常见命令CRUD

## 2.1.数据库

### 2.1.1.搜索所有库

```mysql
show databases;
```

查看mysql中有哪些数据库（名称）。

![1570450189754](E:\typora-document\MyNote\images\1551872356868.png)



相关说明：information_schema,mysql,performance_schema,test这四个数据库是mysql自带的，前三个是不能操作的，里面数据带有系统相关设置；最后一个是可以修改的。

### 2.1.2.使用某一个库

```mysql
use test;
```

使用test数据库;

![1570450623872](E:\typora-document\MyNote\images\1570450623872.png)



### 2.1.3.查看当前所在库

```mysql
select database();
```

查看当前所在数据库；

![1570451191134](E:\typora-document\MyNote\images\1570451191134.png)



## 2.2.数据库表

### 2.2.1.搜索当前库所有表

```mysql
show tables;
```

在当前数据库查询当前数据库内所有数据库表名称并显示；

![1570450855805](E:\typora-document\MyNote\images\1570450855805.png)



### 2.2.2.搜索其他库所有表

```mysql
show tables from mysql;
```

在当前数据库查询其他数据库内所有数据库表名称并显示；

![1570451040445](E:\typora-document\MyNote\images\1570451040445.png)



### 2.2.3.创建表

```mysql
create table test(
	id int,
    name varchar(20)
);
```

创建名为test的数据库表，内部有2个字段，一个是int类型的名为id的字段，一个是varchar类型长度为20名为name的字段。

![1570451708754](E:\typora-document\MyNote\images\1570451708754.png)



### 2.2.4.查看表结构

```mysql
desc test;
```

查看某表的表结构。

![1570451855709](E:\typora-document\MyNote\images\1570451855709.png)



### 2.2.5.查看所有数据

```mysql
select * from test;
```

搜索test表并显示表内每个字段上的数据。

![1570452036520](E:\typora-document\MyNote\images\1570452036520.png)



### 2.2.6.插入表数据

```mysql
insert into test (id,name)values(1,'tom');
```

向数据库表中插入数据，插入id和name这两个字段，对应值为1和tom。

![1570452207383](E:\typora-document\MyNote\images\1570452207383.png)

### 2.2.7.更新表数据

```mysql
update test set name='rose' where id=1;
```

更新数据库表test中id=1所在行的数据，修改name所在列的值为rose。

![1570452542696](E:\typora-document\MyNote\images\1570452542696.png)



### 2.2.8.删除表数据

```mysql
delete from test where id=1;
```

从数据库表test中删除id=1所在行的一行数据。

![1570452766177](E:\typora-document\MyNote\images\1570452766177.png)



# 3.SqlYong的使用

1.修改查询部分字体大小方法：

+ 进入sqlyong,连接数据库，点击工具->首选项->字体编辑器，然后找到对应部分的	字体进行修改即可;

+ 在查询部分，按住ctrl键，然后滑动鼠标滚轮，同样可以修改字体大小；

  

# 4.DQL查询语言

## 4.1.起别名

```sql
select id as tid from test;
--为id起别名为tid
select id tid from test;
```

在列名后使用as关键字或空格来起别名。

![1570871313471](E:\typora-document\MyNote\images\1570871313471.png)

![1570871630159](E:\typora-document\MyNote\images\1570871630159.png)

## 4.2.去重

```sql
select distinct(name)  from test;
```

使用distinct关键字包裹列名即可去重。

![1570871829476](E:\typora-document\MyNote\images\1570871829476.png)

![1570871876571](E:\typora-document\MyNote\images\1570871876571.png)

![1570874235165](E:\typora-document\MyNote\images\1570874235165.png)

# 5.DML操作语言



# 6.DDL数据库操作语言



# 7.TCL事务语言



over不能单独使用，要和分析函数：rank(),dense_rank(),row_number()等一起使用。
其参数：over（partition by columnname1 order by columnname2）
含义：按columname1指定的字段进行分组排序，或者说按字段columnname1的值进行分组排序。
例如：employees表中，有两个部门的记录：department_id ＝10和20
select department_id，rank（） over（partition by department_id order by salary) from employees就是指在部门10中进行薪水的排名，在部门20中进行薪水排名。如果是partition by org_id，则是在整个公司内进行排名。

以下是个人见解：

sql中的over函数和row_numbert()函数配合使用，可生成行号。可对某一列的值进行排序，对于相同值的数据行进行分组排序。

执行语句：select row_number() over(order by AID DESC) as rowid,* from bb

