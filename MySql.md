# MySql

# 1.相关操作

## 1.1.配置文件

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

![1570453121406](D:\MyNote\images\1570453121406.png)



2.在控制台输入`mysql --version` 回车即可查看mysql数据库版本。

![1570453216447](D:\MyNote\images\1570453216447.png)



## 1.5.语法规范

1.不区分大小写，建议关键字大写，列名、表名小写；

2.每条命令以分号(;)结尾；

3.每条命令根据需要进行缩进或换行；

4.写sql查询语句时，表名、列名可以用着重号(``)进行包裹，以表示这不是一个关键字；

5.注释

+ 单行注释：#注释
+ 单行注释：-- 注释(-与注释之间有空格)
+ 多行注释：/* 注释 */

## 1.6.MySql5.7版本安装

1、双击版本

2、选中<I accept ........>  再点击next

3、选中最下方的Custom   在点击next

4、依次点击MySQL Servers---->MySQL Server--->.....MySQL Server 5.7.17-x64 点击中间向右箭头

 ![img](D:\MyNote\images\2019011320430378.png) 

5、仅仅选中两个选项MySQL Server 和 Client Programs   点击next

6、点击Execute 等待几分钟

7、直到出现绿色小对号说明安装成功，点击next

8、确保Config Type 选项中的是Development Machine 点击next ![](D:\MyNote\images\image-20191206172509520.png) 

9、设置一个密码，这是MySQL的密码要牢记

 ![img](D:\MyNote\images\20190113204452291.png) 

 10、WindowsServer Name选项为mysql实例名称，无需更改Start the MySQLServer at System Startup选项为是否开机自启，可以不勾选

 ![img](D:\MyNote\images\2019011320312039.png) 

11、如图所示，点击next

 ![img](D:\MyNote\images\20190113203224533.png) 

12、 点击Execute，等待几分钟；直到全变绿色小对勾，点击Finish

 ![img](D:\MyNote\images\20190113203352395.png) 

13、 直到完成

注册码：

```sql
注册码

ccbfc13e-c31d-42ce-8939-3c7e63ed5417

a56ea5da-f30b-4fb1-8a05-95f346a9b20b

a0fe8645-3916-45d4-9976-cb6b88fecc6c

b70d7f66-dac2-4462-bf51-c4e9347da763
```



二、配置环境变量
1、MySQL的安装路径

 ![img](D:\MyNote\images\20190113204029997.png) 

# 2.常见命令

## 2.1.数据库

### 2.1.1.搜索所有库

```mysql
show databases;
```

查看mysql中有哪些数据库（名称）。

![1570450189754](D:\MyNote\images\1551872356868.png)



相关说明：information_schema,mysql,performance_schema,test这四个数据库是mysql自带的，前三个是不能操作的，里面数据带有系统相关设置；最后一个是可以修改的。

### 2.1.2.使用某一个库

```mysql
use test;
```

使用test数据库;

![1570450623872](D:\MyNote\images\1570450623872.png)



### 2.1.3.查看当前所在库

```mysql
select database();
```

查看当前所在数据库；

![1570451191134](D:\MyNote\images\1570451191134.png)



## 2.2.数据库表

### 2.2.1.搜索当前库所有表

```mysql
show tables;
```

在当前数据库查询当前数据库内所有数据库表名称并显示；

![1570450855805](D:\MyNote\images\1570450855805.png)



### 2.2.2.搜索其他库所有表

```mysql
show tables from mysql;
```

在当前数据库查询其他数据库内所有数据库表名称并显示；

![1570451040445](D:\MyNote\images\1570451040445.png)



### 2.2.3.创建表

```mysql
create table test(
	id int,
    name varchar(20)
);
```

创建名为test的数据库表，内部有2个字段，一个是int类型的名为id的字段，一个是varchar类型长度为20名为name的字段。

![1570451708754](D:\MyNote\images\1570451708754.png)



### 2.2.4.查看表结构

```mysql
desc test;
```

查看某表的表结构。

![1570451855709](D:\MyNote\images\1570451855709.png)



### 2.2.5.查看所有数据

```mysql
select * from test;
```

搜索test表并显示表内每个字段上的数据。

![1570452036520](D:\MyNote\images\1570452036520.png)



### 2.2.6.插入表数据

```mysql
insert into test (id,name)values(1,'tom');
```

向数据库表中插入数据，插入id和name这两个字段，对应值为1和tom。

![1570452207383](D:\MyNote\images\1570452207383.png)

### 2.2.7.更新表数据

```mysql
update test set name='rose' where id=1;
```

更新数据库表test中id=1所在行的数据，修改name所在列的值为rose。

![1570452542696](D:\MyNote\images\1570452542696.png)



### 2.2.8.删除表数据

```mysql
delete from test where id=1;
```

从数据库表test中删除id=1所在行的一行数据。

![1570452766177](D:\MyNote\images\1570452766177.png)



## 2.3.起别名

```sql
select id as tid from test;
--为id起别名为tid
select id tid from test;
```

在列名后使用as关键字或空格来起别名。

![1570871313471](D:\MyNote\images\1570871313471.png)

![1570871630159](D:\MyNote\images\1570871630159.png)

## 2.4.去重

### 2.4.1.作用于单列

```sql
select distinct(name)  from test;
```

使用distinct关键字包裹列名即可去重。

![1570871829476](D:\MyNote\images\1570871829476.png)

![1570871876571](D:\MyNote\images\1570871876571.png)

![1570874235165](D:\MyNote\images\1570874235165.png)

### 2.4.2.作用于多列

```mysql
select distinct name, id from A
```

执行后结果如下：

![img](D:\MyNote\images\03222745-35f76ba1357f4add8cef03b246d9aee8.png)

实际上是根据name和id两个字段来去重的，这种方式Access和SQL Server同时支持。

```mysql
select distinct xing, ming from B
```

返回如下结果：

![img](D:\MyNote\images\33509-20151217095032599-428642167.png)

返回的结果为两行，这说明distinct并非是对xing和ming两列“字符串拼接”后再去重的，而是分别作用于了xing和ming列。

### 2.4.3.COUNT统计

```mysql
select count(distinct name) from A;	  --表中name去重后的数目， SQL Server支持，而Access不支持
```

count是不能统计多个字段的，下面的SQL在SQL Server和Access中都无法运行。

```mysql
select count(distinct name, id) from A;
```

若想使用，请使用嵌套查询，如下：

```mysql
select count(*) from (select distinct xing, name from B) AS M;
```

### 2.4.4.distinct须放在开头

```mysql
select id, distinct name from A;   --会提示错误，因为distinct必须放在开头
```

### 2.4.5.其他

distinct语句中select显示的字段只能是distinct指定的字段，其他字段是不可能出现的。例如，假如表A有“备注”列，如果想获取distinc name，以及对应的“备注”字段，想直接通过distinct是不可能实现的。但可以通过其他方法实现

## 2.5.+号作用

+号在sql中是运算符，分三种情况：

1.当+号两侧都是数字时，则两侧数字直接相加即可；

2.当+号两侧至少一侧为字符时，会试图将字符转换为数字，两侧都成功转换为数字则相加即可；转换失败的一侧记为0，然后两侧相加即可；

3.当+号有至少一侧为null时，结果一定时null；

# 3.SqlYong的使用

1.修改查询部分字体大小方法：

+ 进入sqlyong,连接数据库，点击工具->首选项->字体编辑器，然后找到对应部分的	字体进行修改即可;

+ 在查询部分，按住ctrl键，然后滑动鼠标滚轮，同样可以修改字体大小；


# 4.DQL查询语言

1.条件查询

```mysql
select 查询列表 from 表名 where 筛选条件
```

先执行from部分找到表数据，然后是where部分筛选数据，最后是select显示数据。

# 5.DML操作语言



# 6.DDL数据库操作语言



# 7.TCL事务语言



# 8.常见函数

## 8.1.concat

以下是个人见解：

sql中的over函数和row_numbert()函数配合使用，可生成行号。可对某一列的值进行排序，对于相同值的数据行进行分组排序。

执行语句：select row_number() over(order by AID DESC) as rowid,* from bb

over不能单独使用，要和分析函数：rank(),dense_rank(),row_number()等一起使用。 其参数：over（partition by columnname1 order by columnname2） 含义：按columname1指定的字段进行分组排序，或者说按字段columnname1的值进行分组排序。 例如：employees表中，有两个部门的记录：department_id ＝10和20

select department_id，rank（） over（partition by department_id order by salary) from employees就是指在部门10中进行薪水的排名，在部门20中进行薪水排名。如果是partition by org_id，则是在整个公司内进行排名。



# 9.mysql常见问题

## 9.1.mysql初始化密码

把文件解压到一个目录下

![1581492550132](D:\MyNote\images\1581492550132.png)

这是解压后的目录

![1581492585153](D:\MyNote\images\1581492585153.png)

将my.ini文件考进去

![1581492618357](D:\MyNote\images\1581492618357.png)

双击打开my.ini

找到这两行更改成自己的解压路径保存

![1581492662823](D:\MyNote\images\1581492662823.png)

右键此电脑，选择属性

![1581492953147](D:\MyNote\images\1581492953147.png)

点击左侧菜单栏中高级系统设置，然后配置环境变量

![1581493040054](D:\MyNote\images\1581493040054.png)

![1581493095995](D:\MyNote\images\1581493095995.png)

环境变量  新建 变量值是解压文件的路径

![1581493127622](D:\MyNote\images\1581493127622.png)

Path 单击path编辑

![1581493230038](D:\MyNote\images\1581493230038.png)

新建

![1581493162904](D:\MyNote\images\1581493162904.png)

之后 用管理员身份打开cmd进入文件路径

![1581493316945](D:\MyNote\images\1581493316945.png)

打开命令行窗口，在里面输入：mysqld --install

这个命令是安装服务, 执行完后, 提示英文的成功, 这时候你可以在你的 windows 服务中看到 MySQL 的服务，移除服务命令为：mysqld remove

接着输入：

```mysql
mysqld --initialize --console
```



执行这一步，是因为在MySQL5.7中没有data文件夹，需要用这几个命令产生data文件夹，并且初始化随机登陆密码/neiaAkuH4v!

执行完会出现一大片英文，看不懂没关系，在最后面看到有一个 [email protected]: 后面有一连串的字母数字符号, 这是 MySQL 为你自动生成的随机密码. 要记下来, root就是登陆的用户名，一会我们登陆 MySQL 数据库的时候要用（或者直接按下enter进入）

**启动mysql服务**

在安装后只有启动了mysql服务才能用，

命令行输入：

```mysql
net start mysql
```



 ![1581493444730](D:\MyNote\images\1581493444730.png)

**修改默认密码**

之前系统随机生成的密码只能用来登陆，然后修改密码，用不了mysql，只有修改了才能用

启动了mysql服务后

然后执行 `mysql -uroot -p` ，输入上面得到的密码进入，用该密码登录后，必须马上修改新的密码，不然会报如下错误：

mysql> use mysql;
ERROR 1820 (HY000): You must reset your password using ALTER USER statement before executing this statement.
如果你想要设置一个简单的测试密码的话，比如设置为123456，会提示这个错误，报错的意思就是你的密码不符合要求

mysql> alter user 'root'@'localhost' identified by '123456';
ERROR 1819 (HY000): Your password does not satisfy the current policy requirements
这个其实与validate_password_policy的值有关。

validate_password_policy有以下取值：

默认是1，即MEDIUM，所以刚开始设置的密码必须符合长度，且必须含有数字，小写或大写字母，特殊字符。
有时候，只是为了自己测试，不想密码设置得那么复杂，譬如说，我只想设置root的密码为123456。
必须修改两个全局参数：

首先，修改validate_password_policy参数的值

mysql> set global validate_password_policy=0;
Query OK, 0 rows affected (0.00 sec)

validate_password_length(密码长度)参数默认为8，我们修改为1

mysql> set global validate_password_length=1;
Query OK, 0 rows affected (0.00 sec)

完成之后再次执行修改密码语句即可成功

mysql> alter user 'root'@'localhost' identified by '123456';
Query OK, 0 rows affected (0.00 sec)

至此mysql已经全部安装配置完成了，可以直接用了，可以查看原有的那些数据库。

停止服务的命令:exit

之后再次登陆mysql直接输入修改后的密码就能进入了

## 9.2.root用户密码忘记

1: 通过任务管理器或者服务管理，关掉mysqld(服务进程) 

2: 通过命令行+特殊参数开启mysqld mysqld -- 

defaults-file="D:\ProgramFiles\mysql\MySQLServer5.7Data\my.ini" --skip-grant-tables 

3: 此时，mysqld服务进程已经打开。并且不需要权限检查 

4: mysql -uroot 无密码登陆服务器。另启动一 个客户端进行 

5: 修改权限表 

（1） use mysql; 

（2）update user set authentication_string=password('新密码') where user='root' and Host='localhost'; 

（3）flush privileges; 

6: 通过任务管理器，关掉mysqld服务进程。 

7: 再次通过服务管理，打开mysql服务。 8: 即可用修改后的新密码登陆。 

## 9.3.mysql命令报“不是内部或外部命令”

如果输入mysql命令报“不是内部或外部命令”，把mysql安装目录的bin目录配置到环境变量path中。