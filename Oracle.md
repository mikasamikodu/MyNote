# 1.sql语句分类

+ select查询语句

+ DML语句(数据操作语言)

  ​	insert/update/delete/merge

+ DDL语句(数据定义语言)

  create/alter/drop/truncate

+ DCL语句(数据控制语言)

  grant/rovoke

+ 事务控制语句

  commit/rollback/savepoint

注意:oracle内部不能使用双引号，必须用单引号

oracle中主要数据类型有3种：

 + 字符型

   varchar(10) 定长的字符型数据

   char(10) 定长的字符型数据，占空间但是效率较高

   varchar2(10) 变长的字符型数据，不占空间但是效率稍低

 + 数值型

   number(4),不带小数点的数值型数据

   number(4,2),带2位小数点的数值型数据

 + 日期型

   date 日期型数据

# 2.数据库对象

| 对象名称 | 描述                                   |
| -------- | -------------------------------------- |
| 表       | 基本的数据存储对象，以行和列的形式存在 |
| 约束     | 执行数据校验，保证数据完整性的对象     |
| 视图     | 一个或多个 表数据的显示                |
| 索引     | 用于提高查询的速度                     |
| 同义词   | 对象的别名                             |



## 2.1.数据库对象的命名规则

+ 必须以字母开头
+ 可包括数字(0-9)，字母(a~z)和三个特殊字符(#_$)
+ 不要使用oracle的保留字
+ 同一用户下的对象不能同名，即使是不同的对象类型

# 4.事务

事务开始于第一个执行的DML语句
结束于:

+ COMMIT或ROLLBACK
+ DDL or DCL语句(隐式的提交事物)
+ 用户连接异常，或者用户断开连接(隐式的回滚)
+ 系统崩溃(隐式的回滚)

​        事务会在多种情况下结束。通常应该由产生事务的用户回话通过命令显示的控制事务的结束( COMMIT和ROLLBACK)，这样可以保证事务中数据改变的可控性。
​        除了用户直接控制事务外，其他的情况会隐式的结束事务。由于隐式结束事务的不可预料性，应尽量避免隐式的结束事务
​        Oracle中控制事务的主要命令式**COMMIT**和**ROLLBACK**命令，还有一个辅助的**SAVEPOINT**命令
​        使用**COMMIT和ROLLBACK来控制事务**，有如下的好处

+ 保证数据一致性，修改过的数据(不一致的数据)在没有提交之前其他的用户是不能看到的

+ 在数据永久性生效前重新查看修改的数据

+ 将相关的操作组织在一起。一-个事务中的相关数据改变或者全部成功，或者全部失败

  

## 4.1.事务自动处理的机制

+ 使用COMMIT和ROLLBACK命令可以显示的控制事务的结束。另外在一些时候，事务也会隐式的结束。隐式结束事务有两种方式:隐式提交和隐式回滚
+ 当下列情况发生时事务自动隐式提交: 
  + 执行一个DDL语句
  + 执行一个DCL语句
  + 从SQL*Plus正常退出

+ 当从SQL *PLUS中强行退出，客户端到服务器端的连接异常中断，或系统失败时,事务自动隐式回滚

+ 事务开始后，执行了一系列的DML操作。在事务结束之前，修改的数据可恢复
+ 当前的用户可以看到DML操作的结果,其他用户不能看到DML操作的结果

+ 被操作的数据被锁住，其他用户不能修改这些数据

## 4.2.SAVEPOINT

```sql
--标记点只在事务间有用，事务一旦提交或回滚了整个事务，则标记点会被全部清除
insert into dept values(50,'开发',1000);
SAVEPOINT A;
delete from dept d where deptno>30;
SAVEPOINT B;
update dept set dname='开发部' where deptno=50;
rollback to B;--回滚了更新的操作
commit;--提交了插入和删除的操作
rollback to A;--什么也没做
```



## 4.3.事务的特性

+ 一组单独的操作绑定成为一个工作单元
  + 提交后，事务处理的所有更改可以永久存在
  + 回滚后，事务处理的所有更改将被拋弃

+ 事务处理的ACID特性
  **Atomic:原子性，      Consistent:一致性,**
  **Isolated:隔离性，    Durable:永久性**
  **原子性**:就是事务应作为一个工作单元,事务处理完成，所有的工作要么都在数据库中保存下来，要么完全回滚，全部不保留;
  **一致性**：事务完成或者撤销后，都应该处于一致的状态;
  **隔离性**：多个事务同时进行，它们之间应该互不干扰.应该防止一个事务处理其他事务也要修改的数据时，不合理的存取和不完整的读取数据
  **永久性**：事务提交以后，所做的工作就被永久的保存下来



# 5. 序列

序列是用来维护数据库的主键数据

```sql
create sequence emp_sq 
minvalue 1 
maxvalue 9999
start with 1
increment by 1;
 /*为表emp建立一个自动增长的序列，名称为emp_sq，从1开始，最大9999，每次增长1*/
 
 --建好序列后，可以用  序列名.nextval表示下一个数值
 insert into emp (id,ename,sal) values(emp_sq.nextval, '张三', 11); 
 --这个序列的当前值可以在sys.dual中查
 select emp_sq.currval from sys.dual;
```

> 删除序列

```sql
DROP SEQUENCE commodity_infom_tb_seq  --删除序列
```



# 6.约束

1.约束必须建立在表上，但约束是一个数据库对象（即不是存在与表内或是表的一个附加物），没有表就没有约束
2.约束是在表上强制执行的数据校验规则，表内插入，修改或删除的数据必须符合相关字段上设置的这些检验条件, 也就是约束条件
3.约束条件可以是构建在一个表的单个字段上,也可以构建在一个表的多个字段.
4.当表中数据有相互依赖性时,可以保护相关的数据不被删除.
5.Oracle支持下面五类完整性约束:

+ primary key 主键约束(非空，唯一)
+ unique key 唯一约束
+ not null 非空约束
+ foreign key 外键约束
+ check 检察约束

创建约束有两种方式：1.建表的时候，2.建好表后通过修改表结构的方式添加约束
约束命名有2种方式，一种是用户命名，一种是oracle自己命名
除主键约束外，其他约束可同时存在多个

## 6.1. 唯一约束

唯一约束就是指被约束的一个或多个列的值不能相同，必须保持唯一

```sql
alter table users
add constraint u_user_name unique(uname);
--为表users的uname列添加唯一约束，u_user_name

create table commodity_infod(
        Id  VARCHAR2(50) primary key ,
    	cpicture varchar2(100) unique --建表时添加唯一约束,可以作用到单个字段，称为列级约束
);

create table names(
        Id  VARCHAR2(50) primary key ,
    	cfirstname varchar2(100) unique,
        clastname char(40),
        constraints u_name unique (cfirstname,clastname)--建表时添加唯一约束,可以作用到多个字段
);
--例如：
insert into names values(1, 'a', 'b');--成功
insert into names values(2, 'b', 'a');--成功
insert into names values(1, 'a', 'c');--成功
insert into names values(3, 'a', 'b');--失败
```

## 6.2. 外键约束

外键约束通常关系到两个表的两个字段间的约束
外键字段可以为空，且可以重复
建表时需要先建立父表，后建立带有外键约束的子表
添加数据时，需要先添加父表数据后添加子表数据
删除数据时，需要先删除子表数据后删除父表数据
删除表时，需要先删除子表后删除父表
父表中的主键或唯一键字段可以作为子表的外键
一对多和多对一就是靠主外键实现
一对一时，可以在设置外键时同时为外键字段设置唯一约束
多对多时需要引入关系表，在关系表中用两个表的主键作为外键或联合主键

```sql
--普通外键约束（如果存在子表引用父表主键，则无法删除父表记录），为commodity_newsd的imainid字段添加外键约束f_commodity_newsd，与commodity_newsm的id字段建立关联
ALTER TABLE commodity_newsd ADD CONSTRAINT f_commodity_newsd FOREIGN KEY(imainid) REFERENCES commodity_newsm(id);

--级联外键约束（可删除存在引用的父表记录，而且同时把所有有引用的子表记录也删除）
ALTER TABLE commodity_newsd ADD CONSTRAINT commodity_newsd_foreign_key FOREIGN KEY(imainid) REFERENCES commodity_newsm(id) ON DELETE CASCADE;

--置空外键约束（可删除存在引用的父表记录，同时将子表中引用该父表主键的外键字段自动设为NULL，但该字段应允许空值）
ALTER TABLE commodity_newsd ADD CONSTRAINT commodity_newsd_foreign_key FOREIGN KEY(imainid) REFERENCES commodity_newsm(id) ON DELETE SET NULL;


create table commodity_infod(
        Id  VARCHAR2(50) primary key ,
        cmainid varchar2(50) not null references commodity_infom(id),
    	cpicture varchar2(100) not null
);
/*将cmainid设置为主表commodity_infom的外键，用主表id进行关联*/

create table dept(
        Id  VARCHAR2(50) primary key ,
        cmainid varchar2(50),
    	cpicture varchar2(100),
        constraint fk_cpicture foreugn key references dept1(deptno)
);
```



## 6.3.主键约束

主键约束就是被约束的一个或多个列都不能为空，且值是唯一的，且每个表只能有一个主键
确定主键的方法：不要需要实体的业务数据作为主键，因为业务数据是可以变化的，应该找一个和实体无关的流水号当作主键
一对多和多对一就是靠主外键实现

```sql
--主键作用在一列上
create table commodity_infod(
        Id  VARCHAR2(50) primary key ,--该列为主键，本列非空，且值唯一
        cmainid varchar2(50),
    	cpicture varchar2(100)
);

--主键作用在多列上,被称为联合主键
create table commodity_infom(
        firstname  VARCHAR2(50),
        lastname varchar2(50),
    	cpicture number(100),
    	constraints pk_name primary key (firstname,lastname)
    --这两列为主键，这两列不能同时为空，且这两列值不能同时相同
);
--例如：
insert into names values('a', 'b', 1);--成功
insert into names values('a', 'c', 1);--成功
insert into names values('b', 'a', 1);--成功
insert into names values('a', 'b', 1);--失败
insert into names values('a', null, 1);--失败
```



# 7.索引

数据库中使用最多的是表，其次就是索引
什么是索引:

+ 方案(schema) 中的一个数据库对象
+ 在Oracle数据库中用来加速对表的查询
+ 通过使用快速路径访问方法快速定位数据，减少了磁盘的I/O
+ 索引是独立的数据库对象,并不与表存储在一起，而是与表独立存放
+ 索引记录了表的索引字段的值，也就是关键字，关键字始终与表的索引字段值相同，这种同步由Oracle数据库自动维护

## 7.1.创建索引

有两种方式：

+ 表内有主键约束或唯一约束的字段，数据库会自动为其创建索引

  ```sql
  alter table emp add  constranints ename_u unique (ename);--数据库会自动为ename字段添加索引
  alter table emp drop constranints ename_u;--数据库会自动为ename字段删除索引
  ```

  

+ 手动建立索引，表内经常被查询的字段可以建立索引

  ```sql
  create index i_emp_ename on emp(ename);
  drop index i_emp_ename;
  ```

  

# 8. 视图

+ 视图也就是**虚表**,实际上是-一个被命名了的查询，用于改变数据的**显示形式**，简化查询.访问视图与表的访问
  方式一样
+ 视图的好处:
  + 可以限制对数据的访问,让用户通过试图可以看到表中的一部分数据
  + 可以使复杂的查询变的简单
  + 提供了数据的独立性,让用户不用知道数据来源于处
  + 提供了对相同数据的不同显示

## 8.1.创建视图

```sql
--创建视图
create or replace view hr_view as select * from emp;
create or replace view mgr_view (empno,ename,job,mgr,hiredate,deptno)
as select empno,ename,job,mgr,hiredate,deptno from emp;--前后必须字段数量类型对应并一致 
create or replace view v_emp as 
select deptno,max(sal) maxsal,min(sal) minsal,avg(sal) avgsal from emp group by deptno;--使用组函数时需要在组函数的查询结果后添加别名

--创建只读的视图
create or replace view hr_view as select * from emp with read only;


--插入数据,数据实际是进入源表中了，不建议在视图中插入数据
insert into hr_view values(9000, '张三', '工程时', 1111, '12-8月-2020', 10);

--查询视图内容
select * from hr_view;
select * from hr_view where empno=1;
select empno,ename from hr_view where empno=1;

--查看视图结构
desc hr_view;

--删除视图,不会对源表数据产生影响
drop view hr_view;
```



## 8.2.行内视图

```sql
--行内视图,就是出现在FROM后面的于查询,也就是一个规图,但是该视图没有命名,不会在数据库中保存
--查询工资最高的前三个人的信息,这种方式被称为TOP-N分析法
--ROWNUM只能适用子<=的情况
SELECT ROWHUM,E.* FROM ( SELECT * FROM EMP ORDER BY SAL DESC) E WHERE ROFRTUM <= 3:

/*
(1) rownum对于等于某值的查询条件
如果希望找到学生表中第一条学生的信息，可以使用rownum=1作为条件。但是想找到学生表中第二条
学生的信息，使用rownum>2结果查不到数据。因为rownum都是从1开始，但是1以上的自然数在rownum
做等于判断是时认为都是false条件,所以无法查到rownum = n (2>1的自然数) */
select rownum , T.吉FROM student T where rownum = 1: .
--可以查询到数据
select rownum, id,name from student where rownum = 3;
--查询不到数据


/*
2) rownum对于大于某值的查询条件
如果想我到从第二行记录以后的记录，当使用rownum>2是查不出记录的，原因是由于rownum是一个总是
从1开始的伪列，0racle认为rownum>n(n>1的自然数)这种条件依旧不成立，所以查不到记录
*/
select rownum, id,name from student where rownum >2;
/*
那如何才能找到第二行以后的记录呀。可以使用以下的子查询方法来解决。注意子查询中的rownum必须
要有别名，否则还是不会查出记录来，这是因为rownum不是某个表的列，如果不起别名的话， 无法知道
rownum是子查询的列还是主查询的列。
*/
select * from (select rowmum NO，id, name from student) where NO >=2 AND NO<=4


--可以使用rowid在查询时获取数据修改权限，和使用for update时比较像
--rowid是物理地址，用于定位oracle中具体数据的物理存储位置
```



# 9.查询

## 9.1.查询

```sql
--oracle中sql语句不区分大小写，包括登录数据库时的用户名与密码
--在查询过程中，对于数值型的数据可以进行加减乘除的运算
select sal*12 from emp;

--为查询结果中的字段起别名（字段  as  别名或字段  别名）
select sal*12 as "年薪" from emp;
select sal*12    "年薪" from emp;

--在算术表达式中出现null，则结果必为null，null不等于0
--用||可以把查询结果中两列过多列字段合并到一起
select empno,ename,job,empno||ename||job "员工信息" from emp;

--在连接表达式中出现字符型数据，字符型数据就必须用'',而不能是""
--在连接表达式中出现null，就是原来的字符型数据是null
--任何类型的数据都支持null
--日期型数据支持加减的运算，一个日期加减一个整型数字，等于在这个日期上加减一个天数;如果是两个日期相减就是得到日期之间相差的天数，日期之间不能相加或乘除
--去重可以使用distinct关键字，案例：
select distinct deptno from emp;
select distinct deptno,job from emp;

--对于日期型数据，格式是敏感的，使用日期型数据的格式是dd-mm-yyyy(日-月-年)
--如果是中文版，格式是dd-mm月-yyyy
select 	empno from emp where hirdate='20-2月-2019';

--改变当前会话中的日期格式
alter session set nls_date_format='YYYY-MM-DD HH:Mi:SS'

--比较运算符：>,<,=,>=,<=,!=(不等于),<>(不等于)，between...and...,in (...), like '...',is null,
--is not null

--like 用于模糊匹配
select * from emp where ename like '%a%';--查找字符串中含有a的字符串
--%代表0或多个字符，_代表一个字符
select * from emp where ename like '%\%%' escape '\\';

--查找字符串中含有%的字符串。通过escape指定like里面的指定转义字符。

--排序 order by 
select * from emp order by ename;默认升序排列
select * from emp order by ename desc;降序排列
```



## 9.2.多表查询

多表查询对应不同的标准

### sql1992的标准：

### 9.2.1.等值查询

在父子表关系上，用等号(=)来连接两个表的两个字符或多个字符
示例：

```sql
select * from emp e,dept d where e.deptno=d.deptno;
select * from emp e,dept d where e.deptno=d.deptno and e.deptno=10;
select * from emp e,dept d,location l where e.deptno=d.deptno and d.loc_id=l.locid;
```



### 9.2.2.非等值查询

两个表之间没有父子关系，用!=来连接两个表

示例：

```sql
select e.empno,e.ename,e.sal,s.grade,s.losal,s.hisal
from emp e, salgrade s
where e.sal between s.losal and s.hisal;
```



### 9.2.3.自连接

通过别名，将一个表虚拟为两个表，并在这两个表上做等值查询

```sql
select * from emp a,emp b where a.empno=b.empno;
```



### 9.2.4.外连接

在等值查询的基础上，可以查询不满足等值条件的数据
	a.左外连接，可以右边表中不满足等值条件的数据查出来

```sql
select e.empno,e.ename,e.deptno,d.deptno,d.dname
from emp e,dept d where e.deptno(+)=d.deptno;

select e.empno,e.ename,e.deptno,d.deptno,d.dname
from emp e,dept d where d.deptno(+)=e.deptno;
```



​	b.右外连接，可以左边表中不满足等值条件的数据查出来

```sql
select e.empno,e.ename,e.deptno,d.deptno,d.dname
from emp e,dept d where e.deptno=d.deptno(+);

select e.empno,e.ename,e.deptno,d.deptno,d.dname
from emp e,dept d where d.deptno=e.deptno(+);
```



**注意：**加号不能同时出现在等号两侧

### sql1999新标准

### 9.2.1.交叉连接

即两个表的笛卡尔积

```sql
select e.*,d.* from emp  cross join dept d;
```



### 9.2.2.自然连接

在父子表关系上，自动地匹配两个表中列名完全相同的字段（参照列），在这些相同名称的字段上左等值查询，参照列在查询时不能限定表的别名

```sql
select e.empno,e.ename,deptno,d.dname from emp  natural join dept d;
```



注意：1.当两个表中无父子关系（即无参照列）时，查询结果就是两个表的笛卡尔积
			2.自然连接缺陷：查询时会将所有的参照列作为等值条件，如果某两个参照列类型不同，查询会出错

### 9.2.3.join......using

在自然连接基础上改进，以指定参照列作为等值条件

```sql
select e.empno,e.ename,deptno,d.dname from emp join dept d using(deptno) where e.empno=7369;
```



### 9.2.4.内连接

join...on,使用on里面指定的条件作为查询条件(on内的条件可以是任意条件)

```sql
select e.empno,e.ename,deptno,d.dname from emp join dept d on e.deptno=d.deptno where e.empno=7369;
```



使用join...on做n个等值查询，需要有n-1个join...on子句

```sql
select e.empno,e.ename,deptno,d.dname from emp 
join dept d on e.deptno=d.deptno 
join locations l on d.loc_id=l.locid 
where e.empno=7369;
```



使用join...on做非等值查询

```sql
select e.empno,e.ename,deptno,d.dname from emp 
join salgrade s on (e.sal between s.losal and s.hisal )
where e.empno=7369;
```



### 9.2.5.外连接

左外连接：left join...on可以把左边表中满足等值条件的数据查询出来

```sql
select e.empno,e.ename,e.deptno,d.dname from emp e
left join dept  d on e.deptno=d.deptno;
```



右外连接：right join...on可以把右边表中满足等值条件的数据查询出来

```sql
select e.empno,e.ename,e.deptno,d.dname from emp e
right join dept  d on e.deptno=d.deptno;
```



全外连接：full join...on可以把左右边表中满足等值条件的数据查询出来

```sql
select e.empno,e.ename,e.deptno,d.dname from emp e
full join dept  d on e.deptno=d.deptno;
```



### 9.2.6.union

使用union把两个结果集合成一个结果集,使用时union两侧的结果集字段数量及对应位置字段类型都必须一致
union会去除重复数据

```sql
select * from dept_bak 
union  
select * from dept;
```



union...all，不去除重复数据

```sql
select * from dept_bak 
union  all
select * from dept;
```



## 9.3.子查询

子查询分类是根据子查询返回结果分类的

### 9.3.1单行单列子查询

单行单列子查询需要使用单行比较运算符（如>,<,=.!=,>=,<=,<>）

```sql
--查询比7566员工的工资高的人的信息
--1.先查询7566员工的工资
select sal from emp where empno=7566;
--再查询比7566员工工资高的人的信息
select * from emp where sal > (select sal from emp where empno=7566);

--子查询中使用组函数，子查询结果仍是单行单列，也算单行单列子查询
select * from emp where sal > (select avg(sal) from emp);

--子查询中使用组函数，子查询结果是多行单列，就不算单行单列子查询
select * from emp where sal > (select avg(sal),deptno from emp group by deptno);

--子查询出现在having中，having是多分组后数据进行过滤
select max(sal),deptno from emp group by deptno having max(sal)>(select avg(sal) from emp);
```



### 9.3.2.多行单列子查询

多行单列子查询使用多行比较运算符in,any,all

```sql
--使用in操作符
select * from emo where deptno in (select deptno from dept);

--使用all操作符
-->all，大于查询结果中的最大值
select * from emo where deptno >all (select deptno from dept);
--<all,小于查询结果中最小值
select * from emo where deptno <all (select deptno from dept);

--使用any操作符
-->any，大于查询结果中的最小值
select * from emo where deptno >any (select deptno from dept);
--<any,小于查询结果中最大值
select * from emo where deptno <any (select deptno from dept);
```



### 9.3.3.多行多列子查询

多行多列子查询使用多行比较运算符in

```sql
--使用in操作符
--成对的比较
select * from emo where (sal,job) in (select sal,job from emp where empno=7566 or empno=7564) and empno not in (7566,7564);
--非成对的比较
select * from emo where 
sal in (select sal from emp where empno=7566 or empno=7564) and  
job in (select job from emp where empno=7566 or empno=7564) and 
empno not in (7566,7564);

--子查询出现在from后面，用来作为数据源的
select * from (select * from emp);
```



# 10.oracle练习题

```sql
1：找出各月最后一天受雇的所有雇员
 select * from emp wherehiredate=last_day(hiredate)
2：找出早于36年之前受雇的雇员
   select * from emp where add_months(hiredate,12*36)<sysdate
3：显示只有首字母大写的所有雇员的姓名
 select * from emp where ename=initcap(ename);
4：显示正好为5个字符的雇员姓名
 select * from emp where ename like '_____';
5：显示不带有‘R’的雇员姓名
 select * from emp where ename not  like '%R%';
6：显示所有雇员的姓名的前3个字符
 select ename,substr(ename,1,3) from emp;
7：显示所有雇员的姓名，用‘a’替换所有的‘A’
 select replace(ename,'A','a') from emp;
8：显示所有雇员的姓名以及满36年服务年限的日期
select ename,hiredate from emp where add_months(hiredate,12*36)<sysdate
9：显示雇员的详细资料，按姓名降序排序
 select * from emp order by ename desc ;
10：显示雇员姓名，根据其服务年限，将最老的雇员排在最前面
select ename,hiredate from emp order by hiredate asc;
11：显示所有雇员的姓名、工作和薪金，按工作降序排序，而工作相同的按薪金升序排序
select ename,job,sal from emp order by job desc,sal asc;
12：显示所有雇员的姓名和加入公司的年份和月份
   select ename,to_char(hiredate,'yyyyMM') fromemp;
13：显示在一个月为30天的情况下所有雇员的日薪金，忽略小数
select ename,trunc(sal/30) from emp;
select ename,floor(sal/30)from emp;
14：找出在（任何年份的）2月份受雇的所有雇员
select ename,hiredate from emp where to_char(hiredate,'MM')=2
select ename,hiredate from emp where to_char(hiredate,'MM')='02'
15：对于每个雇员，显示其加入公司的天数
selectename,hiredate,trunc(sysdate-hiredate) 入职天数 from emp;
16：显示姓名字段的任何位置，包含‘A’的所有雇员的姓名
 select * from emp where ename like '%A%';
17：以年、月和日显示所有雇员的服务年限
 select ename,
       hiredate,
       trunc(MONTHS_BETWEEN(sysdate,hiredate)/12) 年,
      trunc(MONTHS_BETWEEN(sysdate, hiredate))月,
       trunc(sysdate - hiredate) 日
  from emp;
  
  
连接查询
18: 列出至少有一个雇员的所有部门
       select count(*),deptno from emp group bydeptno having count(*)>=1;
    列出一个员工都没有的部门
      select * from dept where deptno!=all(selectdeptno from emp group by deptno);
19：列出薪金比“SMITH”多的所有雇员
     select * from emp where  sal>(select sal from emp whereename='SMITH');
22：列出各种工作的最低薪金,并且显示最低薪金大于1500的工作
      select job,min(sal) from emp group by jobhaving min(sal)>1500
23：列出薪金高于公司平均水平的所有雇员
      select * from emp where sal>(selectavg(sal) from emp)
24：列出与“SCOTT”从事相同工作的所有雇员  , 并且与scott是同一个部门的
      select * from emp where(job,deptno)=(select job,deptno from emp where ename='SMITH') and  ename!='SMITH';
25:  列出薪金高于在部门30的所有雇员的薪金
      select * from emp where sal>all(selectsal from emp where deptno=30)
      select * from emp where sal>(selectmax(sal) from emp where deptno=30)
27.列出每个部门雇员的数量
      select count(*),deptno from emp group bydeptno
30：列出各类别工作的最低工资
      select min(sal),job from emp group by job
31：列出各个部门的经理的最低薪金
        select deptno,min(sal) from emp WHEREjob='MANAGER'  group by deptno
32：列出按计算列排序的所有雇员的年薪
      select ename,12*(sal+nvl(comm,0)) 年薪 from emporder by 年薪  desc
20：列出所有雇员的姓名及其部门名
        select ename,dname from emp e,dept dwhere e.deptno=d.deptno
21：列出所有入职日期早于其直接上级的所有雇员
      selecte.ename,e.hiredate,s.ename,s.hiredate from emp e,emp s where e.mgr=s.empno ande.hiredate<s.hiredate
28:列出所有雇员的名称，部门名称和薪金
  select ename,dname,sal from emp e,dept d where e.deptno=d.deptno
29：列出从事同一种工作但不属于同一部门的这些员工
      select e1.ename,e1.job,e1.deptno,e2.ename,e2.job,e2.deptno  from emp e1,emp e2
           where e1.job=e2.job ande1.deptno!=e2.deptno
33:列出所有CLERK的姓名及其部门名称
        select ename,dname from emp e,dept dwhere e.deptno=d.deptno and e.job='CLERK'
34：列出薪金水平处于前四位的雇员
     selectt1.* from (select t.*,rownum rn from (select * from emp order by sal desc) t)t1
     wherern>=1 and rn<=4
35：查询出每个部门薪水最高的人的姓名、薪水、部门编号，并且按照部门编号升序排列
       select e.ename,e.sal,e.deptno from emp e,
     (selectmax(sal) ms,deptno from emp group by deptno) t
       where e.sal=t.ms and e.deptno=t.deptno    
求平均薪水最高的部门的部门编号
select avg(sal),deptno  from emp group by deptno
having avg(sal) =(select max(t.asal)  from (select avg(sal)asal, deptno from emp
group by deptno) t)

求平均薪水最高的部门的部门名字?
select dname
  from dept
 where deptno = (select deptno
                   from emp
                  group by deptno
                 having avg(sal) = (selectmax(t.asal)
                                     from (select avg(sal) asal,deptno
                                         from emp

                                           group by deptno) t))


求比普通员工的最高薪水还要高的经理人名称

SELECT ename,salfrom emp where sal>

(select max(sal)from emp where job='CLERK')

and job='MANAGER'

求部门平均薪水的等级

select t.deptno,t.asal, s.grade

  from (select avg(sal) asal, deptno from empgroup by deptno) t,

       salgrade s

 where t.asal between s.losal and s.hisal
```



# 11.数据库设计三范式

规范化的好处是最小冗余化，减少完整性问题

第一范式：一个表中不能含有重复列
第二范式：所有非主键字段都必须完全依赖表主键字段
第三范式：非主键字段不能依赖于任何非主键字段，即非主键字段之间不能存在相互依赖关系，改变其中一个字段不能影响到其他字段（例如单价、数量、总价：总价=单价*数量）

# 12.oracle函数

## 12.1数值型函数

1.返回绝对值abs()

**abs(x)**

功能：返回x的绝对值

参数：x，数字型表达式

返回：数字

示例：

```sql
select abs(100), abs(-100) from dual;
--返回100，100
```



2.返回正负值sign(x)

**sign(x)**

功能：返回x的正负值

参数：x,数字型表达式

返回：数字，若为正值返回1，负值返回-1，0返回0

示例：

```sql
select sign(100),sign(-100),sign(0) from dual;
--返回1,-1,0
```



3.返回较大的最小整数ceil(x)

**ceil(x)**
功能：返回大于等于x的最小整数值
参数：x，数字型表达式
返回：数字
示例：

```sql
select ceil(3.1),ceil(2.8+1.3),ceil(0) from dual;
--返回的是4,5,0
```



4.返回小于等于x的最大整数值floor(x)

**floor(x)**
功能：返回小于等于x的最大整数值
参数：x，数字型表达式
返回：数字
示例：

```sql
select floor(3.1),floor(2.8+1.3),floor(0) from dual;
--返回的是3，4，0
```



5.返回x的y次幂power(x,y)

**power(x,y)**
功能：返回x的y次幂
参数：x，y，数字型表达式
返回：数字
示例：

```sql
select power(2.5, 2),power(1.5, 0),power(20, -1) from dual;
--返回的是6.25，1，0.05
```



6.返回常量e的y次幂exp(y)

**exp(y)**
功能：返回常量e的y次幂(e为数学常量)
参数：x，数字型表达式
返回：数字
示例：

```sql
select exp(3),exp(0),exp(-3) from dual;
--返回的是20.0855369,1 ,0.049787068
```



相近的函数：power(x,y)，返回e的y次幂
相反的函数：ln(y)，返回以e为底的自然对数

7.返回以x为底的y的对数log(x,y)

**log(x,y)**
功能：返回以x为底的y的对数
参数：x,y，数字型表达式
条件：x,y,都必须大于0
返回：数字
示例：

```sql
select power(4,2),log(16,2),1/log(16,4) from dual;
--返回的是16,0.25,2
select power(6.5,3),log(274.625,3),1/log(power(6.5,3),6.5) from dual;
--返回的是274.625 ，  0.195642521   ，3
```



相近的函数：ln(y)，返回以e为底的y的对数（e为数学常量）

8.返回以e为底的y的对数ln(y)

**ln(y)**
功能：返回以e为底的y的对数（e为数学常量）
参数：y，数字型表达式
条件：y,都必须大于0
返回：数字
示例：

```sql
select exp(3),exp(-3),ln(20.0855369),ln(0.049787068) from dual;
--返回：20.0855369,0.049787068,3  ,   -3
```



相近的函数：log(x,y)，返回以x为底的y的对数
相反的函数：exp(y)，返回以e的y次幂

9.返回x除以y的余数mod(x,y)

**mod(x,y)**

功能：返回x除以y的余数
参数：x,y，数字型表达式
返回：数字
示例：

```sql
select mod(23,8),mod(24,8) from dual;
--返回：7，0
```



10.返回x四舍五入后的值round(x[,y])

**round(x[,y])**
功能：返回x四舍五入后的值
参数：x,y，数字型表达式，如果y是带有小数点的浮点数则只取整数部分，如果y>0则四舍五入为y位小数，如果y小于0则四舍五入到小数点向左第y位。
返回：数字
示例：

```sql
  select round(5555.6666,2.1),round(5555.6666,-2.6),round(5555.6666) from dual;
--返回：   5555.67            ,5600                 ,5556
```


相近的函数：trunc(x[,y])：返回截取后的值，用法同round(x[,y])，只是四舍五入

11.返回x截取后的值trunc(x[,y])

**trunc(x[,y])**
功能：返回x截取后的值
参数：x,y，数字型表达式,如果y不为整数则截取y整数部分，如果y>0则截取到y位小数，如果y小于0则截取到小数点向左第y位，小数前其它数据用0表示。
返回：数字
示例：

```sql
select trunc(5555.66666,2.1),trunc(5555.66666,-2.6),trunc(5555.033333)  from dual;
--返回：5555.66                  5500                   5555
```


相近的函数：round(x[,y])，返回截取后的值，用法同trunc(x[,y]),只是要做四舍五入

12.返回x的平方根sqrt(x)

**sqrt(x)**
功能：返回x的平方根
参数：x，数字型表达式
返回：数字
示例：

```sql
select sqrt(4),sqrt(10) from dual;
--返回 8，3.16227766
```



13.三角函数

**SIN(x)**
功能：返回一个数字的正弦值
示例：select sin(1.57079) from dual;
 返回：  1

SIGH(x)
功能：返回双曲正弦的值
示例：select sin(20),sinh(20) from dual;
返回：0.91294525, 242582598

COS(x)
功能：返回一个给定数字的余弦
示例：select cos(-3.1415927) from dual;
返回： -1

COSH(x)
功能：返回一个数字反余弦值
示例：select cosh(20) from dual;
返回：242582598

TAN
功能：返回数字的正切值
示例：select tan(20),tan(10) from dual;
返回：2.2371609 ,0.64836083

TANH
功能：返回数字n的双曲正切值
示例：select tanh(20),tan(20) from dual;
返回：1 ,2.2371609

ASIN(x)
功能：给出反正弦的值
示例：select asin(0.5) from dual;
返回：0.52359878

ACOS(x)
功能：给出反余弦的值
示例：select acos(-1) from dual;
返回：3.1415927

ATAN(x)
功能：返回一个数字的反正切值
示例 ：select atan(1) from dual;
返回：0.78539816



## 12.2.字符型函数

1.返回字符的ASCII码ASCII(x)

**ASCII(x)**
功能：返回字符表达式最左端字符的的ASCII码值
参数：x,字符型表达式
返回：数值型
示例：

```sql
select ascii('A') A,ascii('a') a,ascii(' ') space,ascii('示') hz from dual;
--A         A          SPACE        hz
--------- --------- --------- ---------
--65        97         32         51902
```



说明：在ascii()函数中 ，纯数字的字符串是不需要用‘ ’括起来，但是含有其他字符串就必须用' '括起来，否则会出错。如果最左端是汉字则只取汉字最左边的字符。

相反的函数：chr()

2.将ascii码转化为字符chr(x)

**chr(x)**
功能：将ascii码转化为字符
参数：x为0-255，整数
返回：字符型
示例：

```sql
select chr(54740) zhao,char(65) chr65 from dual;
--ZH C
-- -
--赵 A

```



相反的函数：ascii(x)

3.连接两个字符串concat(x,y)

**concat(x,y)**
功能：连接两个字符串
参数：x,y，字符型表达式
返回：字符型
示例：

```sql
select concat('010-', '88888888') '电话1','010-'||'88888888' '电话2' from   dual;
--电话1				电话2
----------------------------------
--010-88888888	  010-88888888
```



相近的实现：用||连接两个字符串。示例如上。

4.把每个单词的首字母大写initcap(x)

**initcap(x)**
功能：返回字符串，并将字符串的首字母大写，其余字符小写
参数：x,字符型表达式
返回：字符型
示例：

```sql
select initcap('smith abc aBC') from dual;
--Smith Abc Abc
```



5.把整个字符串转化为小写lower(x)

**lower(x)**
功能：.把整个字符串转化为小写
参数：x，字符型表达式
返回：字符型
示例：

```sql
select lower('AbCdEf') from dual;
--abcdef
```



相反函数：upper(x)，把字符全部转化为大写

6.把字符全部转化为大写upper(x)

**upper(x)**
功能：把字符全部转化为大写
参数：x，字符型表达式
返回：字符型
示例：

```sql
select upper('AbCdEf') from dual;
--ABCDEF
```



相反函数：lower(x)，将全部字符转化为小写

7.把每个单词首字母变为大写nls_initcap(x[,y])

**nls_initcap(x[,y])**
功能：返回字符串，并将字符串的首字母大写，其他字母小写
参数：x,字符型表达式
可选参数：y,即nls_param可选。
1.查询数据级的nls设置`select * from nls_database_parameters;`
2.例如：

指定排序的方式nls_sort:
nls_sort=SCHINESE_RADICAL_M（部首、笔画）
nls_sort=SCHINESE_STROKE_M（笔画、部首SCHINESE_PINYIN_M（拼音））

返回：字符型
示例：

```sql
select nls_initcap('ab cde') test,nls_initcap('a b c d e', 'nls_sort=SCHINESE_RADICAL_M') test1 from dual;
--Ab Cde, A B C D E
```



8.把整个字符串变为小写nls_lower(x[,y])

**nls_lower(x[,y])**
功能：将字符串全部变为小写
参数：x，字符型表达式
参数：y,即Nls_param可选，指定排序的方式(nls_sort=) 。
SCHINESE_RADICAL_M（部首、笔画）
SCHINESE_STROKE_M（笔画、部首SCHINESE_PINYIN_M（拼音））
返回：字符型
示例：

```sql
select nls_LOWER('ab cde') "test",nls_LOWER('a c b d e','nls_sort= SCHINESE_PINYIN_M') "test1" from dual;
返回：ab cde,a c b d e
```



9.把整个字符串转化为大写nls_upper(x[,y])

**nls_upper(x[,y])**
功能：返回字符串并将字符串的转换为大写;
参数：x字符型表达式
参数：y,即Nls_param可选，指定排序的方式(nls_sort=) 。
SCHINESE_RADICAL_M（部首、笔画）
SCHINESE_STROKE_M（笔画、部首SCHINESE_PINYIN_M（拼音））
返回：字符型
示例：

```sql
select NLS_UPPER('ab cde') "test",NLS_UPPER('a c b d e','nls_sort= SCHINESE_PINYIN_M') "test1" from dual;
返回：AB CDE,A C B D E
```



10.字符串中搜索字符的位置(全角算一个字符)instr(c1, c2[ ,x [,y]])

**instr(c1, c2[ ,x [,y]])**
功能：在一个字符串中搜索指定字符，返回发现字符的位置
说明：多字符字节（汉字，全角字符等）按照一个字节算
参数：
c1      被搜索的字符串
c2	  希望搜索的字符串
x		指定开始搜索的位置，默认为1
y		指定返回第y次出现的位置，默认为1
返回：数值
示例：

```sql
select instr('oracle traning', 'ra', 1, 2) from dual;
--9
select instr('重庆某软件公司', '某', 1, 1) a,instrb('重庆某软件公司', '某', 1, 1) b from dual;
--3,5
```



11.字符串中搜索字符的位置(全角算两个字符)instrb(c1, c2[ ,x [,y]])

**instrb(c1, c2[ ,x [,y]])**
功能：在一个字符串中搜索指定字符，返回发现字符的位置
说明：多字符字节（汉字，全角字符等）按照两个字节算
参数：
c1      被搜索的字符串
c2	  希望搜索的字符串
x		指定开始搜索的位置，默认为1
y		指定返回第y次出现的位置，默认为1
返回：数值
示例：

```sql
select instr('重庆某软件公司', '某', 1, 1) a,instrb('重庆某软件公司', '某', 1, 1) b from dual;
--3,5
```



12.返回字符串长度(全角算一个字符)length(x)

**length(x)**
功能：返回字符串长度
说明：多字节字符（汉字，全角字符等）按照一个字符计算
参数：x，字符串
返回：数值
示例：

```sql
select length('高乾坤'),length('北京市海淀区'), length('北京TO_CHAR') from dual;
--      3				6					 9
```



13.返回字符串长度(全角算两个字符)lengthb(x)

**lengthb(x)**
功能：返回字符串长度
说明：多字节字符（汉字，全角字符等）按照两个字符计算
参数：x，字符串
返回：数值
示例：

```sql
select lengthb('高乾坤'),lengthb('北京市海淀区'), lengthb('北京TO_CHAR') from dual;
--		6				12					  11
```



14.返回字符串长度（其他）lengthc(x)、length2(x)、length4(x)

**lengthc(x)、length2(x)、length4(x)**
功能：返回字符长度
说明：多字节字符（汉字、全角符等）全部按一个字节算
参数：x,字符串
返回：数值
示例：

```sql
SQL> select length('高乾竞'),length('北京市海锭区'),length('北京TO_CHAR') from dual;

Oracle中的字符函数中，有一类函数是求字符长度的函数，length、lengthB、lengthC、length2、length4几个函数中比较常用的是length、lengthB。

他们的含义分别是：
Length函数返回字符的个数，使用定义是给定的字符集来计算字符的个数
LENGTHB给出该字符串的byte
LENGTHC使用纯Unicode
LENGTH2使用UCS2
LENGTH4使用UCS4

下面使一些例子：
Select length('你好') from dual;  2

Select lengthB('你好'),lengthC('你好'),length2('你好'), length4('你好')  from dual; 
```



15.在左边添加字符lpad(c1, x[ ,c2])

**lpad(c1, x[ ,c2])**
功能：在字符串c1左边用字符串c2填充，直到c1长度达到x
参数：
c1		原字符串
c2		用于追加的字符串，默认是空格
x		  追加后字符串总长度
返回：字符串
说明：如果c1长度小于x，则返回c1左边x个字符
			如果大于则c1与c2连接，此时若c1长度大于x，则返回c1的右侧x个字符
示例：

```sql
select lpad('gao', 10, '*') from dual;
--*******gao
```



相似函数：rpad(c1, x[ ,c2])，在字符串右侧填充字符串
相反函数：ltrim()，删除左侧字符串

16.在右边添加字符rpad(c1, x[ ,c2])

**rpad(c1, x[ ,c2])**
功能：在字符串c1右边用字符串c2填充，直到c1长度达到x
参数：
c1		原字符串
c2		用于追加的字符串，默认是空格
x		  追加后字符串总长度
返回：字符串
说明：如果c1长度小于x，则返回c1左边x个字符
			如果c1长度大于x，则c1与c2连接，此时若c1长度大于x，则返回c1的左侧x个字符
			如果c1长度大于x，则c1与c2连接，此时若c1长度小于x，则将c1与多个c2连接直到达到长度x,然后返回c1的左侧x个字符

示例：

```sql
select rpad('gao', 10, '*') from dual;
--gao*******
```



相似函数：lpad(c1, x[ ,c2])，在字符串左侧填充字符串
相反函数：rtrim()，删除右侧字符串

17.删除左侧字符串ltrim(c1[ ,c2])

**ltrim(c1[ ,c2])**
功能：删除字符串c1左侧出现的所有c2
参数：	
c1		原字符串
c2		 追加的字符串，默认是空格
返回：字符型
示例：

```sql
select ltrim('++gao++', '+') from dual;
--gao++
```



相似的函数：rtrim(),删除右边的字符串
相反的函数：lpad()，在左侧添加字符串

18.删除右侧字符串rtrim(c1[ ,c2])

**rtrim(c1[ ,c2])**
功能：删除字符串c1右侧出现的所有c2
参数：	
c1		原字符串
c2		 追加的字符串，默认是空格
返回：字符型
示例：

```sql
select rtrim('++gao++', '+') from dual;
--++gao
```



相似的函数：ltrim(),删除左边的字符串
相反的函数：rpad()，在右侧添加字符串

19.替换子字符串replace(c1, c2[ ,c3])

**replace(c1, c2[ ,c3])**
功能：将字符串表达式中，部分相同的字符串，替换成新的字符串
参数：
c1 		原字符串
c2 		被替换的字符串
c3		 要替换成的字符串，默认是空格（即是要删除c2部分）
返回：字符型
示例：

```sql
select replace('he love you', 'he', 'i') from dual;
--i love you
```



20.字符串语音表示形式soundex(c1)

**soundex(c1)**
功能：返回字符串参数的语音表示形式
参数：c1，字符型
返回：字符串
说明：相对于一些读音相同，但是拼写不同的单词是非常有用的
计算语音的算法：

​	1.保留字符串的首字母，但是删除aehiowy
​	2.将下表对应数字赋给对应的字母：
​	、(1) 1：b、f、p、v 
　　(2) 2：c、g、k、q、s、x、z 
　　(3) 3：d、t 
　　(4) 4：l 
　　(5) 5：m、n 
　　(6) 6：r 

3. 如果字符串中存在拥有相同数字的2个以上（包含2个）的字母在一起（例如b和f），或者只有h或w，则删除其他的，只保留1个

   4.只返回前4个字节，不够用0填充 　

示例：

```sql
soundex('two'),soundex('too'),soundex('to')，他们的结果都是T000 
soundex('cap'),soundex('cup')，他们的结果都是C100 
soundex('house'),soundex('horse')，他们的结果都分别是H200，H620

```



21.截取字符串（全角算一个字符）substr(c1, n1[ ,n2])

**substr(c1, n1[ ,n2])**
功能：截取字符串
说明：多字节字符（汉字，全角字符等）算一个
参数：在字符串c1中，从n1开始截取字符串，截取到字符串末尾。若指定n2，则截取到n2位置。n2>n1
返回：字符型
示例：

```sql
select substr('13294097319', 4, 11) from dual;
-- 94097319
```



22.截取字符串（全角算两个字符）substrb(c1, n1[ ,n2])

**substrb(c1, n1[ ,n2])**
功能：截取字符串
说明：多字节字符（汉字，全角字符等）算两个
参数：在字符串c1中，从n1开始截取字符串，截取到字符串末尾。若指定n2，则截取到n2位置。n2>n1
返回：字符型
示例：

```sql
select substr('我手机132', 4),substr('我手机132', 4) from dual;
--		132					 机132
```



23.替换字符串translate(c1, c2, c3)

**translate(c1, c2, c3)**
功能：将字符串中，指定字符串换为新字符串
说明：多字符（汉字、全角字符等）按照一个计算
参数：
c1		希望被替换的字符或常量
c2		查询原始的字符集
c3		替换新的字符集，将c2对应顺序字符，替换为c3对应下表位置的字符
如果c3长度大于c2，则c3长出后面的字符无效
如果c3长度小于c2，则c2长出后面的字符替换为空（即删除）
如果c2中字符重复，则按照出现的首次位置进行替换
返回：字符型
示例：

```sql
select translate('he love you', 'he', 'i'),     --i  love you
translate('重庆的人', '重庆的', '上海男'), 		  --上海男人
translate('重庆的人', '重庆的重庆', '北京男士们'),   --北京男人
translate('重庆的人', '重庆的重庆', '1北京男士们'),  --1北京人
translate('重庆的人', '1重庆的重庆', '北京男士们')   --京男士人
 from dual;
```



24.删除左右两侧空格trim([c1 from ]c2)

**trim([c1 from ]c2)**
功能：删除字符串c2左右两侧的出现的字符串c1
参数：c2，删除前的字符串，c1，需要删除的字符串，默认为空格
返回：字符型
示例：

```sql
select trim('X' from 'XXXgaoXXX'),trim('X' from 'XXgaoXXgaoXX') from dual;
--      gao						   gaoXXgao
```



相似函数：LTRIM()删除左边出现的字符串  RTRIM()删除右边出现的字符串

## 12.3.日期函数

1.返回系统当前日期sysdate
**sysdate**
功能：返回系统当前日期
参数：无参数，无括号
返回：日期
示例：

```sql
select sysdate from dual;
	-- 2020-09-09
```



2.返回指定月数后的日期add_months(d1, n1)

**add_months(d1, n1)**
功能：返回在指定日期d1上添加n1个指定月数后的最新日期
参数：d1		日期型
			n1		数字型
示例：

```sql
select sysdate,add_months(sysdate, 3) from dual；
--		2008-11-5,2009-2-5
```



3.返回本月最后一天日期last_day(x)

**last_day(x)**
功能：返回本月最后一天日期
参数：x，日期型
返回：日期
示例：

```sql
select sysdate,last_day(sysdate) from dual;
--     2008-11-5，2008-11-30
```



4.返回两个日期间相隔的月数months_between(d1, d2)

**months_between(d1, d2)**
功能：返回两个日期间相隔的月数
参数：d1,d2，日期型
返回：数值型,若d1>d2,则返回正数。若d1<d2则返回负数
示例：

```sql
select sysdate,months_between(sysdate, to_date('2006-01-01', 'yyyy-MM-DD')) from dual;
--2008-11-5,34.16
```



5.返回时区对应的时间new_time(d1, c1, c2)

**new_time(d1, c1, c2)**
功能：返回d1在c1和c2所在时区的日期和时间
参数：d1，日期型
参数：c1, c2对应时区及其简写
    	 大西洋标准时间：AST或ADT   
  	  阿拉斯加_夏威夷时间：HST或HDT   
  	  英国夏令时：BST或BDT   
  	  美国山区时间：MST或MDT   
  	  美国中央时区：CST或CDT   
  	  新大陆标准时间：NST   
  	  美国东部时间：EST或EDT   
  	  太平洋标准时间：PST或PDT   
  	  格林威治标准时间：GMT   
  	  Yukou标准时间：YST或YDT 
返回：日期时间
示例：

```sql
select to_char(sysdate, 'yyyy.mm.dd hh24:mi:ss'),to_char(new_time(sysdate, 'PDT', 'GMT'), 'yyyy.mm.dd hh24:mi:ss') from dual;
--2008.11.05 20:11:58 2008.11.06 03:11:58
select sysdate bj_time,new_time(sysdate,'PDT','GMT') los_angles from dual;
返回：
BJ_TIME             LOS_ANGLES
------------------- -------------------
2008-11-05 20:11:58 2008-11-06 03:11:58
```



6.四舍五入后的期间第一天round(d1[ ,c1])

**round(d1[ ,c1])**
功能：给出日期d1按期间（参数c1）四舍五入后的期间的第一天日期（与数值四舍五入意思相近）
参数：d1，日期型，c1，为字符型，c1默认为j（即最近的0点日期）
参数表：c1对应参数
	最近0点日期: 取消参数c1或j
	最近的星期日：day或dy或d
	最近月初日期：month或mon或mm或rm 
	最近季日期：q
	最近年初日期：syear或year或yyyy或yyy或yy或y(多个y表示精度)  
	最近世纪初日期：cc或scc
返回：日期
示例：

```sql
select sysdate,			
round(sysdate, 'j'),
round(sysdate, 'd'), 
round(sysdate, 'mm'),
round(sysdate, 'q'), 
round(sysdate, 'year') from dual;
```



7.返回日期所在期间的第一天trunc(d1[ ,c1])

**trunc(d1[ ,c1])**
功能：返回日期d1所在期间（参数c1）的第一天日期
参数：d1，日期型，c1，字符型，c1默认是j（即当前日期）
参数表：c1对应参数
	最近0点日期: 取消参数c1或j
	最近的星期日：day或dy或d
	最近月初日期：month或mon或mm或rm 
	最近季日期：q
	最近年初日期：syear或year或yyyy或yyy或yy或y(多个y表示精度)  
	最近世纪初日期：cc或scc
返回：日期
示例：

```sql
select sysdate,			
trunc(sysdate, 'j'),
trunc(sysdate, 'd'), 
trunc(sysdate, 'mm'),
trunc(sysdate, 'q'), 
trunc(sysdate, 'year') from dual;
```



8.返回下周某一天的日期next_day(d1[ ,c1])

**next_day(d1[ ,c1])**
功能：返回日期d1在下周星期几（参数c1）的日期
参数：d1，日期型，c1，字符型，c1默认是j（即当前日期）
参数表：c1对应参数有星期一，星期二，星期三......
返回：日期
示例：

```sql
select sysdate,
next_day(sysdate, '星期一'),
next_day(sysdate, '星期二'),
next_day(sysdate, '星期三'),
next_day(sysdate, '星期四'),
next_day(sysdate, '星期五'),
next_day(sysdate, '星期六'),
next_day(sysdate, '星期日') from dual;
```



9.提取时间日期中数据extract(c1 from d1)

**extract(c1 from d1)**-
功能：日期/时间d1中，参数（c1）的值
参数：d1日期型(date)/日期时间型(timestamp)，c1为字符型参数
参数表：见示例
返回：字符
示例：

```sql
select 
extract(hour from timestamp'2001-2-16 2:38:40'),
extract(minute from timestamp'2001-2-16 2:38:40'),
extract(second from timestamp'2001-2-16 2:38:40'),
extract(day from timestamp'2001-2-16 2:38:40'),
extract(month from timestamp'2001-2-16 2:38:40'),
extract(year from timestamp'2001-2-16 2:38:40') from dual;

select extract(year from date'2001-2-16') from dual;

select extract(hour from timestamp timestamp sysdate),
extract(day from sysdate) from dual;
```



10.返回当前会话中的时间与日期localtimestamp

**localtimestamp**
功能：返回当前会话中的时间与日期
参数：无参数，无括号
返回：日期
示例：

```sql
select localtimestamp from dual;
--14-11月-08 12.35.37.453000 上午
```



11.返回当前会话时区中的时间与日期current_timestamp

**current_timestamp**
功能：以timestamp with time zone 数据类型返回当前会话时区的当前日期
参数：无参数，无括号
返回：日期
示例：

```sql
select current_timestamp from dual;
--14-11月-08 12.37.34.609000 上午 +08:00
```



12.返回当前会话时区中的日期current_date

**current_date**
功能：返回当前会话时区的当前日期
参数：无参数，无括号
返回：日期
示例：

```sql
select current_date from dual;
--2008-11-14
```



13.返回数据库时区设置dbtimezone

**dbtimezone**
功能：返回时区
参数：无参数，无括号
返回：字符型
示例：

```sql
select dbtimezong from dual;
--+00:00
```



14.返回当前会话时区sessiontimezone

**sessiontimezone**
功能：返回会话时区
参数：无参数，无括号
返回：字符型
示例：

```sql
select dbtimezone,sessiontimezone from dual;
--返回:+00:00   +08:00
```



15.变动日期时间数值interval c1 c2

**interval c1 c2**
功能：变动日期时间数值
参数：c1为数字字符串或日期时间字符串，c2为日期参数
参数表：c2参考示例
返回：日期时间格式的数值，前面多了一个+号	
以天或比天更小的单位时可用数值表达式借用，如1表示1天，1/24表示1小时，1/24/60表示1分钟
示例：

```sql
select 
trunc(sysdate) + (interval '1' second), --加1秒(1/24/60/60)
trunc(sysdate) + (interval '1' minute), --加1分钟(1/24/60)
trunc(sysdate) + (interval '1' hour), --加1小时(1/24)
trunc(sysdate) + (interval '1' day), --加1天(1)
trunc(sysdate) + (interval '1' month), --加1月
trunc(sysdate) + (interval '1' year), --加1年
trunc(sysdate) + (interval '1:02:03' hour to second), --加指定小时到秒上面
trunc(sysdate) + (interval '1:02' minute to second), --加指定分钟到秒上面
trunc(sysdate) + (interval '1:02' hour to minute), --加指定小时到分钟上面
trunc(sysdate) + (interval '2 01:02' day to minute) --加指定天数到分钟上面
from dual;
```



## 12.4.转换函数

1.字符串转换为rowid值chartorowid(c1)

**chartorowid(c1)**
功能：转换varchar2为rowid值
参数：c1，必须是长度18的字符串，字符串必须符合rowid的格式
返回：返回rowid值
示例：

```sql
select chartorowid('akjfbaskflbkjJNBD') from dual;
```



说明：在Oracle中，每一条记录都有一个rowid，rowid在整个数据库中是唯一的，rowid确定了每条记录是在Oracle中的哪一个数据文件、块、行上。在重复的记录中，可能所有列的内容都相同，但rowid不会相同.

2.rowid转化为字符串rowidtochar(x)

**rowidtochar(x)**
功能：转化rowid为varchar2型的字符串
参数：rowid，固定参数
返回：长度为18位的字符串
示例：

```sql
select rowidtochar(rowid) from dual;
```



3.字符串语言字符集转换convert(c1, set1, set2)

**convert(c1, set1, set2)**
功能：将字符串c1从原字符集set2转换为新字符集set2
参数：c1，字符串，set1,set2都是字符型参数
返回：字符串
示例：

```sql
select convert('strutz', 'we8hp', 'f7dec') from dual;
-- strutz
```



4.十六进制转换为二进制hextoraw(c1)

**hextoraw(c1)**
功能：十六进制转换为二进制
参数：c1，十六进制字符串
返回：二进制字符串
示例：

```sql
select hextoraw('A123') from dual;
```



5.二进制转换为十六进制rawtohex(c1)

**rawtohex(c1)**
功能：将一个二进制字符串转换为十六进制字符串
参数：c1，二进制字符串
返回：十六进制字符串
示例：

```sql
select rawtohex('11110000') from dual;
```



6.将日期或数据转化为字符串to_char(x[ ,c1 [,c2]])

**to_char(x[ ,c1 [,c2]])**
功能：将日期或数据转化为字符串
参数：
	x为日期或number型数据
	c1为格式参数
	c2为nls参数
	如果x为日期nlsparm=NLS_DATE_LANGUAGE  控制返回的月份和日份所使用的语言。
	如果x为数字nlsparm=NLS_NUMERIC_CHARACTERS  用来指定小数位和千分位的分隔符，以及货币符号。
	NLS_NUMERIC_CHARACTERS ="dg",  NLS_CURRENCY="string"

返回：varchar2型字符串
示例：

```sql
--x为数值时
to_char(1210.73, '9999.9') 返回 '1210.7' 
to_char(1210.73,  '9,999.99') 返回 '1,210.73' 
to_char(1210.73, '$9,999.00') 返回 '$1,210.73'  
to_char(21, '000099') 返回 '000021' 
to_char(852,'xxxx') 返回' 354'

--x为日期型
to_char(sysdate,'d') 每周第几天 
to_char(sysdate,'dd') 每月第几天 
to_char(sysdate,'ddd') 每年第几天 
to_char(sysdate,'ww') 每年第几周 
to_char(sysdate,'mm') 每年第几月 
to_char(sysdate,'q') 每年第几季 
to_char(sysdate,'yyyy') 年 

select to_char(sysdate,' PM yyyy-mm-dd hh24:mi:sssss AD year mon day ddd iw') FROM DUAL;
----------------------------------------------------------------------
--上午 2008-03-27 09:58:35917 公元 two thousand eight 3月 星期四 087 13

SELECT TO_CHAR(SYSTIMESTAMP,'HH24:MI:SS.FF5') FROM DUAL;
------------------------------
10:02:28.90000
SQL>SELECT TO_CHAR(SYSDATE,'DSDL') FROM DUAL
-----------------------------------
2008-03-27 2008年3月27日 星期四

【示例】带C3示例

select to_char(to_date('2002-08-26','yyyy-mm-dd'),'day','NLS_DATE_LANGUAGE = American') from dual; 
返回：monday 
```



7.字符串转换为日期型to_date(x[ ,c1 [ ,c2]])

**to_date(x)**
功能：字符串转换为日期型
参数：c2，c3,字符型参数
返回：字符串

 	如果x格式为日期型(date)格式时，则相同表达：date x
	 如果x格式为日期时间型(timestamp)格式时，则相同表达：timestamp x
示例：

```sql
select to_date('199912','yyyymm')
to_date('2000.05.20','yyyy.mm.dd'),
(date '2008-12-31') XXdate, 
to_date('2008-12-31 12:31:30','yyyy-mm-dd hh24:mi:ss'),
(timestamp '2008-12-31 12:31:30') XXtimestamp
from dual;
```



8.字符串转换为数字型to_number(x)

**to_number(x)**
功能：字符串转换为数字型
参数：c2，c3,字符型参数
返回：数字
示例：

```sql
select TO_NUMBER('199912'),TO_NUMBER('450.05') from dual;
```



9.半角转全角to_multi_byte(x)

**to_multi_byte(x)**
功能：半角转全角
参数：c1字符型
返回：字符串
示例：

```sql
SQL> select to_multi_byte('高A'), '高A' text from dual;

test 高A
----------
高Ａ  高A
```



10.全角转半角to_single_byte(x)

**to_single_byte(x)**
功能：全角转半角
参数：x字符型
返回：字符串
示例：

```sql
SQL> select to_multi_byte('高Ａ') text from dual;

test
----
高A
```



11.字符集名称转换为id nls_charset_id(x)

**nls_charset_id(x)**
功能：字符集名称转换为id
参数：x字符型
返回：数值型
示例：

```sql
sql> select nls_charset_id('zhs16gbk') from dual;

nls_charset_id('zhs16gbk')
--------------------------
     852
```



12.字符集id转换为名称 nls_charset_name(x)

**nls_charset_name(x)**
功能：字符集id转换为名称 
参数：x数值型
返回：字符型
示例：

```sql
sql> select nls_charset_name(852) from dual;

nls_char
--------
zhs16gbk
```



## 12.5.聚组函数

1.统计平均值avg([distinct|all  ]x)

**avg(distinct|all ]x)**
功能：统计数据表中选中行x列的平均值
参数：all表示对所有值求平均值，distinct表示先对选中行数据进行去重后再求平均值。默认为all。
参数：x数值型
返回：数值型
示例：

```sql
环境：
create table table3(xm varchar(8),sal number(7,2));
insert into table3 values('gao',1111.11);
insert into table3 values('gao',1111.11);
insert into table3 values('zhu',5555.55);
commit;

执行统计：
select avg(distinct sal),avg(all sal),avg(sal) from table3;
结果：  3333.33  2592.59  2592.59
```



2.统计合计值sum([distinct|all  ]x)

**sum([distinct|all  ]x)**
功能：统计数据表中选中行x列的合计值
参数：all表示对所有值求合计值，distinct表示先对选中行数据进行去重后再求合计值。默认为all。
参数：x数值型
返回：数值型
示例：

```sql
环境：
create table table3(xm varchar(8),sal number(7,2));
insert into table3 values('gao',1111.11);
insert into table3 values('gao',1111.11);
insert into table3 values('zhu',5555.55);
commit;

执行统计：
select SUM(distinct sal),SUM(all sal),SUM(sal) from table3;
结果：  6666.66     7777.77     7777.77
```



3.统计标准误差stddev([distinct|all  ]x)

**stddev([distinct|all  ]x)**
功能：统计数据表中选中行x列的标准误差
参数：all表示对所有值求标准误差，distinct表示先对选中行数据进行去重后再求标准误差。默认为all。
参数：x,只能是数值型
返回：数值型
示例：

```sql
环境：
create table table3(xm varchar(8),sal number(7,2));
insert into table3 values('gao',1111.11);
insert into table3 values('gao',1111.11);
insert into table3 values('zhu',5555.55);
commit;

执行统计：
select STDDEV(distinct sal),STDDEV(all sal),STDDEV(sal) from table3;
结果：  3142.69366257674     2565.99863039714  2565.99863039714
```



4.统计方差variance([distinct|all  ]x)

**variance([distinct|all  ]x)**
功能：统计数据表中选中行x列的方差
参数：all表示对所有值求方差，distinct表示先对选中行数据进行去重后再求方差。默认为all。
参数：x,只能是数值型
返回：数值型
示例：

```sql
环境：
create table table3(xm varchar(8),sal number(7,2));
insert into table3 values('gao',1111.11);
insert into table3 values('gao',1111.11);
insert into table3 values('zhu',5555.55);
commit;

执行统计：
select VARIANCE(distinct sal),VARIANCE(all sal),VARIANCE(sal) from table3;
结果： 9876523.4568     6584348.9712     6584348.9712
```



5.统计所得到的行数count([distinct|all  ]x)

**count([distinct|all  ]x)**
功能：统计数据表中选中行x列的合计值
参数：* 表示对所有行都	统计，不管是否包含空值（null）
all表示对所有值求合计值，distinct表示先对选中行数据进行去重后再求合计值。默认为all。如果有all或distinct则会忽略空值。
参数：x,任意类型
返回：数值型，count(*)=sum(1)
示例：

```sql
环境：
create table table3(xm varchar(8),sal number(7,2));
insert into table3 values('gao',1111.11);
insert into table3 values('gao',1111.11);
insert into table3 values('zhu',5555.55);
insert into table3 values('',1111.11);
insert into table3 values('zhu',0);
commit;

执行统计：
select count(*),count(xm),count(all xm),count(distinct sal),count(all sal),count(sal),sum(1) from table3;
结果：  5   4  4  3   5   5  5

```



6.统计最大值max([distinct|all  ]x)

**max([distinct|all  ]x)**
功能：统计数据表中选中行x列的最大值
参数：all表示对所有值求最大值，distinct表示先对选中行数据进行去重后再求最大值。默认为all。
参数：x,可以是日期，字符，数值型数据
返回：与x所属类型相同
示例：

```sql
环境：
create table table3(xm varchar(8),sal number(7,2));
insert into table3 values('gao',1111.11);
insert into table3 values('gao',1111.11);
insert into table3 values('zhu',5555.55);
insert into table3 values('',1111.11);
insert into table3 values('zhu',0);
commit;

执行统计：
select MAX(distinct sal),MAX(xm) from table3;
结果：5555.55   zhu

```



7.统计最小值min([distinct|all  ]x)

**min([distinct|all  ]x)**
功能：统计数据表中选中行x列的最小值
参数：all表示对所有值求最小值，distinct表示先对选中行数据进行去重后再求最小值。默认为all。
参数：x,可以是日期，字符，数值型数据
返回：与x所属类型相同，字符型数据在统计时会忽略空值(null)
示例：

```sql
环境：
create table table3(xm varchar(8),sal number(7,2));
insert into table3 values('gao',1111.11);
insert into table3 values('gao',1111.11);
insert into table3 values('zhu',5555.55);
insert into table3 values('',1111.11);
insert into table3 values('zhu',0);
commit;

执行统计：
select MIN(distinct sal),MIN(xm),MIN(distinct xm),MIN(all xm) from table3;
结果：0   gao  gao  gao
```



## 12.6其他函数

1.为空值赋值nvl(exp1, exp2)

**nvl(exp1, exp2)**
功能：若exp1为空则返回exp2;若exp1不为空则返回exp1
参数：两个参数类型需要保持一致
**nvl2(exp1, exp2, exp3)**
功能：若exp1不为空则返回exp1;若exp1为空则返回exp2;若exp2为空则返回exp3，若exp3与exp2类型不一致则将exp3类型转化为exp2的类型

2.条件取值decode()

**decode(条件,值1,翻译值1,值2,翻译值2,...值n,翻译值n,缺省值)**
功能：根据条件返回相应值
参数：c1, c2, ...,cn,字符型/数值型/日期型，必须类型相同或null
注：值1……n 不能为条件表达式,这种情况只能用case when then end解决　

含义解释：　　
　　decode(条件,值1,翻译值1,值2,翻译值2,...值n,翻译值n,缺省值)　　
　　该函数的含义如下：　　
　　IF 条件=值1 THEN
　　RETURN(翻译值1)
　　ELSIF 条件=值2 THEN
　　RETURN(翻译值2)
　　......
　　ELSIF 条件=值n THEN
　　RETURN(翻译值n)　　
　　ELSE
　　RETURN(缺省值)
　　END IF
　　
或：
　　when case 条件=值1 THEN
　　RETURN(翻译值1)
　　ElseCase 条件=值2 THEN
　　RETURN(翻译值2)
　　......
　　ElseCase 条件=值n THEN
　　RETURN(翻译值n)　　
　　ELSE
　　RETURN(缺省值)
　　END
示例：

```sql
·使用方法：　　
　　1、比较大小　　
　　select decode(sign(变量1-变量2),-1,变量1,变量2) from dual; --取较小值
　　sign()函数根据某个值是0、正数还是负数，分别返回0、1、-1　　
　　例如：
　　变量1=10，变量2=20
　　则sign(变量1-变量2)返回-1，decode解码结果为“变量1”，达到了取较小值的目的。
　　
　　2、表、视图结构转化　　
　　现有一个商品销售表sale，表结构为：　　
　　month　　　 char(6)　　　　　 --月份
　　sell　　　　number(10,2)　　　--月销售金额　　
　　现有数据为：　　
　　200001　　1000
　　200002　　1100
　　200003　　1200
　　200004　　1300
　　200005　　1400
　　200006　　1500
　　200007　　1600
　　200101　　1100
　　200202　　1200
　　200301　　1300
　　
　　想要转化为以下结构的数据：　　
　　year　　　char(4)　　　　　 --年份
　　month1　　number(10,2)　　　--1月销售金额
　　month2　　number(10,2)　　　--2月销售金额
　　month3　　number(10,2)　　　--3月销售金额
　　month4　　number(10,2)　　　--4月销售金额
　　month5　　number(10,2)　　　--5月销售金额
　　month6　　number(10,2)　　　--6月销售金额
　　month7　　number(10,2)　　　--7月销售金额
　　month8　　number(10,2)　　　--8月销售金额
　　month9　　number(10,2)　　　--9月销售金额
　　month10　　number(10,2)　　　--10月销售金额
　　month11　　number(10,2)　　　--11月销售金额
　　month12　　number(10,2)　　　--12月销售金额
　　
　　结构转化的SQL语句为：
　　
　　create or replace view
　　v_sale(year,month1,month2,month3,month4,month5,month6,　　
　　month7,month8,month9,month10,month11,month12)
　　as
　　select
　　substrb(month,1,4),
　　sum(decode(substrb(month,5,2),'01',sell,0)),
　　sum(decode(substrb(month,5,2),'02',sell,0)),
　　sum(decode(substrb(month,5,2),'03',sell,0)),
　　sum(decode(substrb(month,5,2),'04',sell,0)),
　　sum(decode(substrb(month,5,2),'05',sell,0)),
　　sum(decode(substrb(month,5,2),'06',sell,0)),
　　sum(decode(substrb(month,5,2),'07',sell,0)),
　　sum(decode(substrb(month,5,2),'08',sell,0)),
　　sum(decode(substrb(month,5,2),'09',sell,0)),
　　sum(decode(substrb(month,5,2),'10',sell,0)),
　　sum(decode(substrb(month,5,2),'11',sell,0)),
　　sum(decode(substrb(month,5,2),'12',sell,0))
　　from sale
　　group by substrb(month,1,4);
```



3.相等返回NULL,NULLIF (expr1, expr2)

 **NULLIF (expr1, expr2)**
功能：expr1和expr2相等返回NULL，不相等返回expr1

4.条件取值case when

语法：

```sql
case [<表达式>]
when <表达式条件值1> then <满足条件时返回值1> 
[when <表达式条件值2> then <满足条件时返回值2> 
……
[else  <不满足上述条件时返回值>]]
end
```



功能：当：<表达式>＝<表达式条件值1……n> 时，返回对应 <满足条件时返回值1……n> 
当<表达式条件值1……n>不为条件表达式时，与函数decode()相同，
decode(<表达式>,<表达式条件值1>,<满足条件时返回值1>,<表达式条件值2>,<满足条件时返回值2> ……,<不满足上述条件时返回值>)
参数：<表达式> 默认为true (逻辑型)
<表达式条件值1……n> 类型要与<表达式>类型一致，
若<表达式>为字符型，则<表达式条件值1……n>也要为字符型
注意点：

1、以CASE开头，以END结尾
2、分支中WHEN 后跟条件，THEN为显示结果
3、ELSE 为除此之外的默认情况，类似于高级语言程序中switch case的default，可以不加
4、END 后跟别名
5、只返回第一个符合条件的值,剩下的when部分将会被自动忽略，得注意条件先后顺序
示例：

```sql
建立环境：
create table xqb
(xqn number(1,0));
insert into xqb xqn values(1);
insert into xqb xqn values(2);
insert into xqb xqn values(3);
insert into xqb xqn values(4);
insert into xqb xqn values(5);
insert into xqb xqn values(6);
insert into xqb xqn values(7);
commit;

查询结果：
SELECT xqn, 
       CASE
          WHEN xqn = 1  THEN '星期一'
          WHEN xqn = 2  THEN '星期二'
          WHEN xqn = 3  THEN '星期三'
	  else '星期三以后'
       END 星期
FROM xqb

另类写法
SELECT xqn, 
       CASE xqn
          WHEN 1  THEN '星期一'
          WHEN 2  THEN '星期二'
          WHEN 3  THEN '星期三'
	  else '星期三以后'
       END 星期
FROM xqb


decode正确表达：
SELECT xqn, 
decode(xqn,1,'星期一',2,'星期二',3,'星期三','星期三以后') 星期
FROM xqb

decode错误表达：
SELECT xqn, 
decode(TRUE,xqn=1,'星期一',xqn=2,'星期二',xqn=3,'星期三','星期三以后') 星期
FROM xqb

组合条件表达：
SELECT xqn, 
       CASE
          WHEN xqn <= 1  THEN '星期一'
          WHEN xqn <= 2  THEN '星期二'   --条件同：not(xqn<=1) and xqn<=2
          WHEN xqn <= 3  THEN '星期三'   --条件同：not(xqn<=1 and xqn<=2) and xqn<=3
	  else '星期三以后'
       END 星期
FROM xqb
```



所有组函数都是忽略空值的

avg()和sum()只用于数值计算，max(),min()除了数值还可以对字符进行计算

# 13.同义词

同义词,就是数据库对象的一-个别名,可以简化访问其他用户的数据库对象

同义词是数据库对象的一个别名
同义词可以简化对对象的访问
通过使用同义词，可以:

+ 简化了引用另一个用户对象的方法(用户名.对象名)
+ 缩短了对象名称的长度
+ 同时屏蔽了对象的名称，使用户不知道最终的数据来源于那个对象
  语法: CREATE SYNONYM synonym_ name FOR object;

```sql
SELECT SYSDATE FROM sys.DUAL;

create or replace SYNONYM DUAL1 for SYS.DUAL;

SELECT SYSDATE FROM DUAL1;
```



# 14.PLSQL

​		PL/SQL也是一种程序语言,被称作支持SQL的程序语言(Program Languagl),是Oracle数据库对SQL语句的扩展，在普通的SQL语言中增加了编程语言的特点;
​		数据操作和查询语句被包含在PL/SQL代码的过程性单元中，经过逻辑判断、循环等操作完成复杂的功能或者计算

## 14.1.优点

​		使用PL/SQL可以编写具有很多高级功能的程序，虽然这些功能可以通过多个SQL语句来完成同样的功
能,但是PL/SQL具有如下的优点:

+ 使一组语句功能形成模块化程序开发
+ 使用过程性语言控制程序结构
+ 可以对程序中的错误进行处理
+ 具有较好的可移植性
+ 集成在数据库中,调用更快
+ 减少了网络的交互，有助于提高程序性能

## 14.2.PL/SQL程序库基本结构

​		PL/SQL中起作用的部分都是由基本块组成的基本块有四个组成部分

+ 声明部分:DECLARE -可选部分
  + 变量、常量、游标、用户定义异常声明
  + 注意：本部分注意声明初始化变量

+ 执行体开始部分:BEGIN -必要部分
  + SQL语句
  + PL/SQL语句
  + 注意：本部分可以为变量赋值，或使用变量

+ 异常处理部分:EXCEPTION-可选部分
  + 程序出现异常时，捕捉异常并处理异常
  + 注意：本部分可以使用变量
+ 执行体结束:END; -必要部分

**案例：**

```plsql
DECLARE
	--在declare部分声明变量，常量等
	--声明的规范:变量名称 变量类型[:=缺省值]
	--每行只能声明一个变量或常量
	V_DEPTNO NUMBER;
BEGIN
	--在begin部分写sql或plsql语句
	--在begin部分也可以使用declare声明变量常量
	DBMS_OUTPUT.put_line('欢迎使用PL/SQL，查询之前V_DEPTNO='||V_DEPTNO);
	SELECT DEPTNO INTO V_DEPTNO FROM EMP WHERE EMPNO=7369;--PL/SQL语句，完成赋值操作
	dbms_output.put_line('欢迎使用PL/SQL，查询之后V_DEPTNO='||V_DEPTNO);
	DELETE FROM EMP WHERE DEPTNO=V_DEPTNO;--SQL语句
	DELETE FROM DEPT WHERE DEPTNO=V_DEPTNO;--SQL语句
END;
/*
查询结果：
欢迎使用PL/SQL，查询之前V_DEPTNO=
欢迎使用PL/SQL，查询之后V_DEPTNO=20
*/
---------------------------------------------------------------------
DECLARE
	v_total_sal NUMBER(9,2) :=0;--pl/sql赋值语句
	c_tax_rate constant NUMBER(3,2) :=8.25;--常量只能被赋值一次
	v_gender CHAR(1);
	v_valid  BOOLEAN NOT NULL :=TRUE;
	v_b      BOOLEAN;
	v_num1   NUMBER(2) :=10;
	v_num2   NUMBER(2) :=10;
BEGIN
	dbms_output.put_line('v_total_sal='||v_total_sal);
	--=在这里相当于java中的==
	v_b := (v_num1=v_num2);
	if(v_b)  then
		dbms_output.put_line('OK！');
    else
    	dbms_output.put_line('NOT OK！');
    end if;
END;
```



## 14.3.变量

1.简单变量

+ 简单变量不包括任何组件，只能保存一个值
+ 基本类型包括三大类:字符，数字，日期
  + BINARY_INTEGER   整形数字
  + NUMBER [(precision, scale)]  数字类型
  + CHAR [(maximum_ length)]   定长字符类型
  + VARCHAR2(maximum length)    变长字符类型
  + DATE    日期类型
  + LONG   长字符类型
  + LONG RAW    长二进制类型
  + CLOB/ BLOB / BFILE    大对象类型(字符大对象，二进制大对象，操作系统文件大对象)
  + BOOLEAN    布尔类型，有效值为TRUE,FALSE,NULL

2.复合类型

​		复合变量也叫做组合变量.在复合变量中包含多个内部的组件，每个组件都可以单独存放值.一个复合变量可以存放多个值
​		与简单变量类型不同，复合变量类型不是数据库中已经存在的数据类型，所以复合变量在声明类型之前，首先要创建使用到的复合类型，然后将变量声明为复合变量
复合数据类型:

+ PL /SQL TABLES    表类型

使用案例：

```plsql
DECLARE
    --声明复合类型,声明一个名字是NAME_TABLE_TYPE的table类型，内部装varchar(6)的数据
	TYPE NAME_TABLE_TYPE IS TABLE OF VARCHAR(6) INDEX BY BINARY_INTEGER;
	
	--使用复合类型
	v_table1 NAME_TABLE_TYPE;
BEGIN
	--给表类型的变量赋值，可以通过索引来访问表类型的变量
	--表类型没有长度限制即v_table1(i)，i没有限制
	v_table1(1):='hello1';
	v_table1(2):='hello2';
	v_table1(3):='hello3';
	
	dbms_output.put_line('v_table1(1)='||v_table1(1)||
                         'v_table1(2)='||v_table1(2)||
                         'v_table1(3)='||v_table1(3));
END;
```



+ PL/SQL RECORDS    记录类型
  复合类型被创建后，可以被使用多次定义多个变量

​        复合类型中的RECODES类型是由多个组件组成的一种类型.包含一个或几个组件，每个组件称为一个域(FIELD)，域的数据类型可以是简单变量类型、另一个RECORD类型或PL/SQL的TABLE类型
​	    在使用RECORD变量时把多个域的集合作为一个逻辑单元使用,对记录类型变量赋值或引用，都需要使用“记录变量名.域名”的方式来实现
​	    主要用于从表中取出查询到的行数据
​	    记录类型可以包含-一个或多个域每个域相当于记录类型变量的一个属性.在使用记录变量类型时，实际.上是对记录类型变量的属性进行操作.每个域都可以是不同的数据类型,存放不同类型的数据

```plsql
DECLARE
    --声明记录类型变量
	TYPE NAME_RECORE_TYPE IS RECORD(
    	EMPNO NUMBER(4),
        ENAME VARCHAR2(20),
        JOB   VARCHAR2(20),
        MGR   NUMBER(4),
        HIREDATE DATE,
        SAL   NUMBER(8,2),
        COMM  NUMBER(8,2),
        DEPTNO NUMBER(4)
    );
	
	--使用复合类型
	v_record NAME_RECORE_TYPE;
BEGIN
	--给记录类型的变量赋值
	v_record.empno:= 7879;
	v_record.ename:='hello2';
	v_record.job:='hello3';
	v_record.hiredate:=to_date('1923-12-12','YYYY-MM-DD');
	
	dbms_output.put_line('v_record.empno='||v_record.empno||
                         'v_record.ename='||v_record.ename||
                         'v_record.hiredate='||to_char(v_record.hiredate, 'YYYY-MM-DD');
END;
```



+ %type类型

```plsql
/*除了可以使用已经确定的类型来声明变量,还可以使用%type, %rowtype来作为变量的类型
使用type来声明变量
当我们用%type来声明变量的时候,我们声明的变量是简单类型、表类型
%type的前面可以是一个前面已经声明过的简单类型的变量,也可以是一个表的字段，可以是复合类型变量*/
DECLARE
    --V_EMPNO    NUNBER(4) ;
    V_EMPNO    DATE;
    V_DEPTNO   V_EMPNO%TYPE;--V_DEPTNO的类型随V_EMPNO改变而改变
    v_empno    emp.empno%type;--使用emp表中empno作为v_empno的类型，同样后者会随前者类型改变而改变
BEGIN
    --V_EMPNO :=8000;
    --V_DEPTNO := 20;
    V_EMPNO :='12-4月-2020';
    V_DEPTNO := '12-4月-2020';
    DBMS_OUTPUT.put_line('V_ EMPNO ='||V_EMPNO||
                         ' ,V_ DEPTNO='||V_DEPTNO) ;
END ;

```



+ %rowtype类型

```plsql
-- %ROWTYPE的前面,可以是一个表名或表名声明的变量,也可以是前面声明的一个记录类型的变量(该变量必须要参照于一个表,而不能是自定义的记录类型)
DECLARE
    --%ROWYPE的前面是一个表名
    --使用%ROWTYPE的时候, 0racle做了两件事情:1.用DEPT表的字段及其类型来声明了一种记录类型，2.用这种记录来声明变量
    V_EMP    DEPT%ROWTYPE ;
BEGIN
    V_EMP.DEPTNO :=30;
    V_EMP.DNAME :='开发部':
    V_EMP.LOC :='北京';
    dbms_output.put_line('V_EMP.DEPTNO='||V_EMP.DEPTNO||' ,V_EMP.DNANE='||V_EMP.DNAME||' ,V_EMP.LOC='||V_EMP.LOC) ; 
END 
```



## 14.4.使用函数、组函数

```plsql
--使用函数
DECLARE
  v_date date := to_date('1902-09-11','yyyy-mm-dd');
BEGIN
  dbms_output.put_line('v_date=' || to_char(v_date,'yyyy-mm-dd'));

END;
----------------------------------
--使用组函数，但返回结果需要是一条记录
DECLARE
  v_empno emp.empno%type;
  v_maxsal number;
  v_minsal number;
BEGIN
  select empno,max(sal) maxsal,min(sal) minsal into v_empno,v_maxsal,v_minsal 
  from emp 
  group by empno 
  having max(sal)>3000;
  dbms_output.put_line('empno=' || v_empno || ',v_maxsal=' || v_maxsal || ',v_minsal=' || v_minsal);

END;
```



## 14.5.select

```plsql
--在plsql中使用select语句,它是用来把查询的结果通过info赋值到变量中
--select语句只能返回一条记录，（0条或多条都会报错，而且返回一条时需要配合使用into）
DECLARE
  v_empno emp.empno%type;
  v_ename emp.ename%type;
BEGIN
  --查询顺序与变量顺序必须一致
  select empno,ename into v_empno,v_ename from emp where empno=7369;
  dbms_output.put_line('v_empno=' || v_empno || 'v_ename=' || v_ename);

END;
----------------------------------
--用记录类型变量与select * 搭配使用
DECLARE
  v_emp emp%rowtype;
BEGIN
  select * into v_emp from emp where empno=7369;
  dbms_output.put_line('v_emp.empno=' || v_emp.empno);

END;
```



## 14.6.DML、DDL、DCL

```plsql
--在plsql中使用DML语句或事务控制语言，与在oracle中使用无不同
BEGIN
  insert into emp values(9000,'张张','销售元',9022,'12-9月-2011',2000,1000,10);
  update emp set ename='张无' where empno=9000;
  delete from emp where empno=9000;
  commit;
  --rollback;
END;
----------------------------------
--在plsql中使用DDL语句或DCL语句要使用  execute immediate
create table users (userid number primary key,uname char(30));
drop table users;
BEGIN
  execute immediate 'create table users (userid number primary key,uname char(30))';
  execute immediate 'drop table users';
  
  execute immediate 'create table users (userid number primary key,uname char(30),sex char(2) check (sex in (''男'',''女'')))';
  execute immediate 'drop table users';
END;

```



## 14.7.判断

```plsql
--在plsql中使用if elsif else
DECLARE
  v_job emp.job%type;
  v_sal emp.sal%type;
  v_addsal v_sal%type;
BEGIN
  select job,sal into v_job,v_sal from emp where empno=7369;
  if ( v_job = 'CLERK' ) then
    v_addsal := v_sal * 1.2;
  elsif (v_job = 'SALESMAN') then
    v_addsal := v_sal * 1.5;
  else 
    v_addsal := v_sal * 2.0;
   end if;
   update emp set sal = v_addsal where empno=7369;
   commit;
END;

select distinct job from emp;
```



## 14.8.循环

```plsql
--在plsql中使用循环
DECLARE
       v_count number := 1;--初始值
BEGIN
  loop
      dbms_output.put_line('v_count=' || v_count);--循环体
      v_count := v_count+1;--迭代条件
      exit when v_count>10;--循环条件
  end loop;
END;
----------------------------------
--在plsql中使用循环,循环插入100条数据,奇数插入男，偶数插入女
DECLARE
  v_count number := 1;--初始值
  v_sex char(2);
  v_name users.uname%type;
BEGIN
  loop
      if ( mod(v_count,2) = 1 ) then
        v_sex := '男';
      else
        v_sex := '女';--循环体
      end if;
      v_name := '张' || v_count;
      insert into users values(v_count, v_name, v_sex);--循环体
      v_count := v_count+1;--迭代条件
      exit when v_count>100;--循环条件
  end loop;
  commit;
END;

----------------------------------
--在plsql中使用while循环
DECLARE
  v_count number := 1;--初始值
BEGIN
  while v_count<=10 loop    --循环条件
      dbms_output.put_line('v_count=' || v_count);--循环体
      v_count := v_count+1;--迭代条件
  end loop;
END;
----------------------------------
--在plsql中使用循环,循环插入100条数据,奇数插入男，偶数插入女
truncate table users;
DECLARE
  v_count number := 1;--初始值
  v_sex char(2);
  v_name users.uname%type;
BEGIN
  while v_count<=100 loop    --循环条件
      if ( mod(v_count,2) = 1 ) then
        v_sex := '男';
      else
        v_sex := '女';--循环体
      end if;
      v_name := '张' || v_count;
      insert into users values(v_count, v_name, v_sex);--循环体
      v_count := v_count+1;--迭代条件
  end loop;
  commit;
END;
select * from users;

-------------------------------
--在plsql中使用for循环,oracle会主动维护计数器
truncate table users;
DECLARE
  v_sex char(2);
  v_name users.uname%type;
BEGIN
  --oracle会自动维护计数器
  for v_count in 1..100 loop    --循环条件for v_count in reverse 1..100 loop先从100开始插入
      if ( mod(v_count,2) = 1 ) then
        v_sex := '男';
      else
        v_sex := '女';--循环体
      end if;
      v_name := '张' || v_count;
      insert into users values(v_count, v_name, v_sex);--循环体
  end loop;
  commit;
END;
select * from users;
```



## 14.9.游标

​		在执行增删改查时，Oracle会开辟一片内存空间来存储这些受影响的数据。这块区域就是游标区域。可用通过游标来分析这些受影响的数据。

​		游标4个属性：%ROWCOUNT,%ISOPEN,%FOUND,%NOTFOUND

​		游标分为两类，一种是隐式游标，另一种是显示游标

+ 隐式游标：增删改查都会有隐式游标，即可用通过隐式游标分析受影响的数据，隐式游标有统一SQL前缀，例如SQL%ROWCOUNT.

```plsql
DECLARE
  V_COUNT NUMBER;
BEGIN
  DELETE FROM emp WHERE deptno=10;
  
  V_COUNT := SQL%ROWCOUNT;
  DBMS_OUTPUT.put_line('V_COUNT=' || V_COUNT);--v_count=3
  rollback;
END;
```



+ 显式游标：用来从数据库中抓取多条数据

  在PL/SQL中，执行SQL语句有特殊要求，每次只能取一条且必须搭配into使用

  游标在打开前和关闭后都是无法使用的，强行使用会出现游标无效的错误

```plsql
--用loop与notfound来循环游标
declare
  --1.声明游标，一个显式游标，就是和一个sql语句绑死的
  CURSOR CUR_EMP IS SELECT * FROM EMP;
  --创建一个记录类型变量，用于操作游标内的每天数据
  v_emp emp%rowtype;
begin
  --2.打开游标，就是执行游标绑定的sql语句，并把受影响的数据放入游标区域
  OPEN CUR_EMP;
  
  --3.从游标取出一条数据放入记录类型变量中
  FETCH CUR_EMP INTO v_emp;
  
  --从记录类型变量中取数据
  DBMS_OUTPUT.put_line('v_emp.empno=' || v_emp.empno);
  
  --4.使用完游标，关闭游标并清空游标区域
  CLOSE CUR_EMP;
end;
---------------------------------------------
--用while与found来循环游标
--create or replace procedure cur_emp_pro is--创建一个存储过程，用来调试
declare
  CURSOR CUR_EMP IS SELECT * FROM EMP;
  v_emp emp%rowtype;
begin
  OPEN CUR_EMP;
  
  FETCH CUR_EMP INTO v_emp;
  
  while CUR_EMP%FOUND LOOP
    DBMS_OUTPUT.put_line('v_emp.empno=' || v_emp.empno);
    FETCH CUR_EMP INTO v_emp;
  END LOOP;
  DBMS_OUTPUT.put_line('总条数为' || CUR_EMP%rowcount);
  CLOSE CUR_EMP;
end;
-------------------------------------------------------------
--使用for循环可用简化游标开发，因为oracle会自动的声明记录类型变量，会open,close,fetch游标
declare
  CURSOR CUR_EMP IS SELECT * FROM EMP;
begin
  for v_emp in CUR_EMP LOOP
    DBMS_OUTPUT.put_line('v_emp.empno=' || v_emp.empno);
  END LOOP;
end;
```



## 14.10.异常处理

​		在plsql中发生异常，如果没有处理，异常就会呗传递给环境，进而中断程序。一旦发生异常，程序将会在异常代码处中断，后续代码不会被执行。

​		在plsql程序中，如果在begin部分出现异常，则会进入exception部分执行异常处理功能。如果我们捕获了异常并做了相应的处理，那程序就不会报错。

​		oracle异常类型有三种：

​		1.预定义异常，oracle已经为这种异常定义好了名称，我们在异常处理部分直接通过异常名称进行捕获。例如：NOT_DATA_FOUND  没有找到数据 ,TO_MANY_ROWS  数据太多  ,INVALID_CURSOR   无效的游标 ,ZERO_DIVDE  除数为0,DUP_VAL_ON_INDEX   唯一索引中插入了重复值,VALUE_ERROR   赋值异常

​		2.非预定义异常，因为违反了oracle的规则，oracle会产生报错信息（错误编号与错误信息），但时这类错误没有专有的名称。但是我们可用自己为这些异常定义名称，并将名称与oracle的错误信息绑定在一起。

```plsql
--定义异常
declare
  V_EXCEP EXCEPTION;
  PRAGMA EXCEPTION_INIT(V_EXCEP,-02292);
begin
  DELETE FROM DEPT WHERE DEPTNO=100;
EXCEPTION
  WHEN V_EXCEP THEN
    DBMS_OUTPUT.put_line('没有查询到数据');
  
  WHEN OTHERS THEN
    DBMS_OUTPUT.put_line('PLSQL发生了异常！');
end;
```

​		3.用户自定义异常，首先用户定义一个异常，然后当判断某个时刻程序违反了用户的规则时，我们可以手动提升一个异常，然后在异常处处理这个问题；

```plsql
-------------------------------------------------------------
--自定义异常
declare
  V_EXCEP EXCEPTION;
  PRAGMA EXCEPTION_INIT(V_EXCEP,-02292);
  v_emp_no number;
begin
  select empno into v_emp_no from emp where empno=12;
  if ( v_emp_no is null ) then
     raise V_EXCEP;--提升一个异常
  end if;
EXCEPTION
  WHEN V_EXCEP THEN
    DBMS_OUTPUT.put_line('没有查询到数据');
  
  WHEN OTHERS THEN
    DBMS_OUTPUT.put_line('PLSQL发生了异常！');
end;
```



处理异常

```plsql
declare
  v_code number(10);
  v_msg varchar2(255);
begin
  delete from emp where empno=a;
EXCEPTION
  WHEN OTHERS THEN
    v_code := SQLCODE;--获取错误编号
    V_MSG := SQLERRM;--获取错误信息
    INSERT INTO ERR_LOG VALUES(1,V_CODE,V_MSG,SYSDATE); 
    DBMS_OUTPUT.put_line('PLSQL发生了异常！');
end;
```



## 14.11程序单元

plsql程序，又名plsql程序单元，是数据库中命名的plsql块。有四类：

+ 过程--执行特定操作

+ 函数--进行复杂运算返回计算结果

+ 包--将逻辑上相关的过程和函数组织到一起

+ 触发器--通过触发事件执行相应操作

  以上四种程序单元都是基于declare..begin..exception..end的。

### 14.11.1.存储过程

当我们创建了一个存储过程时，就相当于创建了一个方法。为了让存储过程执行，需要先调用它才可以。

```plsql
create or replace procedure cur_emp_pro is
  CURSOR CUR_EMP IS SELECT * FROM EMP;
  v_emp emp%rowtype;
begin
  OPEN CUR_EMP;
  
  FETCH CUR_EMP INTO v_emp;
  
  while CUR_EMP%FOUND LOOP
    DBMS_OUTPUT.put_line('v_emp.empno=' || v_emp.empno);
    FETCH CUR_EMP INTO v_emp;
  END LOOP;
  DBMS_OUTPUT.put_line('总条数为' || CUR_EMP%rowcount);
  CLOSE CUR_EMP;
end;

1.直接在命令行运行
打开sqlplus，运行命令 exec cur_emp_pro;
set serveroutput on;--打开程序的输出显示
exec cur_emp_pro;
2.在匿名块中调用
begin
	cur_emp_pro
end;
```



创建带参数的存储过程

```plsql
--在匿名块中调用带参数的存储过程
--1.按参数名称调用
declare
  v_deptno number(4) := 50;
  v_dname varchar2(20) := '市场部';
  v_loc varchar2(10) := 'china';
begin
  --通过形参指向实参（p_deptno => v_deptno）来指定参数，不会限定参数的顺序
  add_dept(p_deptno => v_deptno,p_dname => v_dname,p_loc => v_loc);
end;
------------------------------------------------------------
--2.按参数顺序调用
declare
  v_deptno number(4) := 60;
  v_dname varchar2(20) := '市场部';
  v_loc varchar2(10) := 'china';
begin
    --按照函数参数的顺序添加参数
  add_dept(v_deptno,v_dname,v_loc);
end;
------------------------------------------------------------
--3.按混合方式调用
declare
  v_deptno number(4) := 70;
  v_dname varchar2(20) := '市场部';
  v_loc varchar2(10) := 'china';
begin
  add_dept(v_deptno,p_dname => v_dname,p_loc => v_loc);
end;
```



有输入输出类型参数的存储过程

```plsql
--作为oracel中过程的参数，除了有数据类型外，还有一种特殊的类型，即输入输出的类型(in,out,in out)
create or replace procedure param_test(p_in in varchar2,p_out out varchar2,p_in_out in out varchar2) is

begin
  DBMS_OUTPUT.put_line('p_in=' || p_in);
  DBMS_OUTPUT.put_line('p_out=' || p_out);
  DBMS_OUTPUT.put_line('p_in_out=' || p_in_out);
  
  --作为out类型的参数，可以在过程中被重新赋值，并且会被返回给调用者
  p_out := 'out类型的参数在过程中被重新赋值';
  p_in_out := 'in out类型的参数在过程中被重新赋值';
end;
------------------------------------------------------------
declare
  v_in varchar2(100) := 'in类型的参数的初始值';
  v_out varchar2(100) := 'out类型的参数的初始值';
  v_inout varchar2(100) := 'in out类型的参数的初始值';
begin
  param_test(v_in,v_out,v_inout);
  DBMS_OUTPUT.put_line('v_in=' || v_in);
  DBMS_OUTPUT.put_line('v_out=' || v_out);
  DBMS_OUTPUT.put_line('v_inout=' || v_inout);
end;
结果：
p_in=in类型的参数的初始值
p_out=
p_in_out=in out类型的参数的初始值
v_in=in类型的参数的初始值
v_out=out类型的参数在过程中被重新赋值
v_inout=in out类型的参数在过程中被重新赋值
```



### 14.11.2.函数

接受一个或多个参数，在函数中完成运算，最终为用户返回结果（oracle函数必须有返回结果）

```PLSQL
--创建函数
CREATE OR REPLACE FUNCTION ADD_COMM(P_JOB VARCHAR2,P_SAL EMP.SAL%TYPE) RETURN NUMBER IS
  V_ADDSAL EMP.COMM%type;
BEGIN
  if ( P_JOB = 'CLERK' ) then
    V_ADDSAL := P_SAL * 1.2;
  elsif (P_JOB = 'SALESMAN') then
    V_ADDSAL := P_SAL * 1.5;
  else 
    V_ADDSAL := P_SAL * 2.0;
   end if;
   RETURN V_ADDSAL;
END;
```



1.命令行中因为无法传递参数，所以不能调用函数

2.在匿名块中调用函数(这里可以用OUT类型参数)

函数的参数也有IN、OUT类型，但在函数中OUT类型参数使用不方便，所以在函数中只能用IN类型参数

```plsql
--调用函数
DECLARE
  V_RES NUMBER(9);
  V_STR VARCHAR2(40) := '是你觉得可能';
  V_LENGTH NUMBER(3);
BEGIN
  V_RES := ADD_COMM('CLERK', 1000);
  V_LENGTH := LENGTH(V_STR);
  DBMS_OUTPUT.put_line('V_RES=' || V_RES);
  DBMS_OUTPUT.put_line('V_LENGTH=' || V_LENGTH);
END;
```



3.在sql语句中使用函数(这里不可以用OUT类型参数，OUT类型参数必须是变量，但是sql语句中无法定义变量)

```sql
select job,sal,add_comm(job,sal) 奖金 from emp;
```



### 14.11.3包

​		包是一种特殊的PL/SQL程序，它并不是一个PL/SQL的存储程序块，而是由存储在一起的相关对象组成的
PL /SQL存储程序组(是一组过程，函数，变量，常量的集合)
​		包有两个独立的部分，包头和包体，需要分别定义，并且分别被保存在数据库中
​		包头包含了包中过程、函数、常量、变量的声明，在包头中不包括任何PL/SQL程序
​		包体是真正的过程、函数的执行部分定义，所有在包头中声明的过程，函数的程序主体都在包体内定义

​		包的调用，如`DBMS_OUTPUT.put_line('V_RES=' || V_RES);`

​		包头和包体是两种数据库对象，可以独立的存在

​		在删除时，可以分别删除：在删除包体时，包头不会受到影响。但是在删除包头时，相关的包体也会被删除
​		`DROP PACKAGE packae name;`
​		`DROP PACKAGE BODY packae name:`

### 14.11.4.触发器

​		触发器类似于函数和过程，同样是具有声明部分、执行部分和异常处理部分的命名PL/SQL块。

​		但与过程、函数不同的是，触发器是在事件发生时隐式的运行的，并且触发器不能接收参数;而过程/函数是用户显示调用的，可以接受参数
​		运行触发器的方式叫做触动( firing)，指在特定的事件发生的时候(前或后)自动运行定义好的PL/SQL程序
​		触发的事件可以是对数据库表的DML操作(INSERT、UPDATE或DELETE)或某个视图的操作
​		触发的事件也可以是系统事件，例如数据库的启动和关闭，以及一些DDL操作
​		触发器被作为触动触发器的事务的一部分，所以在触发器中不可以使用结束事务的事务控制语句

​		在Oracle数据库中主要有二种触发器类型:

+ DML触发器

  + DML触发器由DML语句触发，并且语句类型决定了DML触发器的类型
  + DML触发器类型主要包括INSERIT，UPDATE,DEL ETE三种触发器
  + 操作对象:表或者视图
  + 触发的时机包括:对表来说有before或after触发,对视图来说有INSTEAD OF
  + 触发范围包括:行级触发或语句级触发。行级触发是在每行数据操作时都会触发执行;
  + 可以设置WHEN子句，决定触发后是否执行触发器的执行部分;如果不设置WHEN字句，那么只要事件触发，就执行程序体
  + 语法格式

  语句级触发器：

  ```plsql
  CREATE OR REPLACE TRIGGER trigger_name 
  	timing
  	 event1 [or event2 or event3]
  	  on table_name
  	 when conditions
  [DECLARE]
  	声明变量
  BEGIN 
  	...
  END;
  说明:
  timing :表示触发时机可以是after或before
  Event1: 表示触发事件，例如: insert, delete， update
  When: 表示执行触发器的条件
  Tirgger body.触发器的执行体
  --------------------------------------------------------------
  --下面的例子创建了一个用于控制用户对表操作时间限制的触发器。规定了用户只有在工作时间才能对表进行操作
  CREATE OR REPLACE TRIGGER secure_emp
  	BEFORE INSERT ON emp 
  BEGIN
  	IF ((to_char(SYSDATE,'DY') IN ('星期日','星期六')) OR (to_char(SYSDATE,'HH24:MI')	not BETWEEN '08:00' AND '18:00')) THEN
  		RAISE_APPLICATION_ERROR(-20500, '你只能在工作时间对表进行操作') ;
  	END IF;
  END;
  --注意:
  --TO_CHAR(SYSDATE,"DY")将时间转化为星期的格式
  --TO_CHAR(SYSDATE,'HH24:MI')将时间转化为时间的格式
  --RAISE_APPLICATION_ERROR:这一语句升起一个用户定义错误，显示一条用户定义提示
  --错误号必须在当在-20000.. -20999之间
  --通过在周六或周日或08 :00到18 :00的时间段内向emp表插一条数据触发
  -------------------------------------------------------------
  --在插入、更新、删除emp表时都会触发此触发器
  CREATE OR REPLACE TRIGGER secure_emp2
    BEFORE INSERT OR UPDATE OR DELETE ON emp
  BEGIN
    --如果当前时间是周六或周日或时间不在8: 00-18: 00之间
    IF(to_char(SYSDATE,'DY') IN ('SAT','SUN')) OR (to_char(SYSDATE,'HH24') NOT BETWEEN
    '08' AND '18') THEN
      IF DELETING THEN
        RAISE_APPLICATION_ERROR (-20502, '你只能在工作时间删除员工表的数据') ;
      ELSIF INSERTING THEN
        RAISE_APPLICATION_ERROR (-20500, '你只能在工作时间插入员工表的数据') ;
      ELSIF UPDATING ('SAL') THEN
        RAISE_APPLICATION_ERROR (-20503, '你只能在工作时间更新员工表的数据');
      ELSE
        RAISE_APPLICATION_ERROR (-20504, '你只能在工作事件操作员工表的数据') ;
      END IF;
    END IF;
  END;
  ```



​	 行级触发器： 

```plsql
CREATE [OR REPLACE] TRIGGER trigger_name
	timing
	 event1 [OR event2 OR event3]
	  ON table_name
	[REFERENCING OLD AS old | NEW AS new]
FOR EACH ROW
	[WHEN (condition)]
[Declare]
	同样可以声明变量等
Begin
	。。。
end
说明:
FOR EACH ROW:表明对表中的每行数据操作时都会触发这个触发器REFERENCING子句是说明触发器替换值的前缀名，默认替换前的前缀名为old,替换后的前缀名为new。也可以自己声明替换前后变量的的前缀规则

CREATE OR REPLACE TRIGGER SAL_EMP
       BEFORE INSERT OR UPDATE OF SAL ON EMP 
       FOR EACH ROW
BEGIN
  IF NOT (:NEW.job in ('AD_PRES','AD_VP')) AND :NEW.sal > 15000
  THEN 
      RAISE_APPLICATION_ERROR(-20202, '员工不能获得这么多薪水');
  END IF;
END;
INSERT INTO EMP VALUES('9000','SUN','CLERK','7902','12-11月-2004',16000,300,20);
SELECT * FROM EMP;
----------------------------------------------------------
--写触发器，不允许降低员工工资
CREATE OR REPLACE TRIGGER SAL_EMP
       BEFORE UPDATE OF SAL ON EMP 
       FOR EACH ROW
BEGIN
  IF (:NEW.SAL < :OLD.SAL)
  THEN 
      RAISE_APPLICATION_ERROR(-20202, '不能降低员工薪水');
  END IF;
END;
update emp set sal=100 where empno=7369;
```



视图上的INSTEAD OF触发器

```plsql
CREATE OR REPLACE TRIGGER trigger_name
	INSTEAD OF
	event1 [or event2] ON table_name
    [REFERENCING OLD AS old|NEW AS new]
FOR EACH ROW
trigger_body
说明：
INSTEAD OF :被用于视图。当对视图进行DML操作时，对视图的DML操作会转化为对另外一些表的操作
案例：
-------------------------------------------------------------
CREATE OR REPLACE VIEW V_EMP_INFO
AS 
SELECT E.*,D.DNAME,D.LOC
FROM EMP E,DEPT D
WHERE E.DEPTNO=D.DEPTNO;
SELECT * FROM V_EMP_INFO;
-------------------------------------------------------------
CREATE OR REPLACE TRIGGER INSERT_EMPINFO
    INSTEAD OF INSERT ON V_EMP_INFO
    FOR EACH ROW
DECLARE
   V_COUNT NUMBER(1);
BEGIN
  SELECT COUNT(1) INTO V_COUNT FROM DEPT WHERE DEPTNO= :NEW.DEPTNO;
  IF ( V_COUNT < 1 ) THEN 
      INSERT INTO DEPT VALUES(:NEW.DEPTNO,'部门'||:NEW.DEPTNO,'北京');
  ELSE
      UPDATE DEPT SET DNAME=:NEW.DNAME,LOC=:NEW.LOC WHERE DEPTNO=:NEW.DEPTNO;
  END IF;
  INSERT INTO EMP VALUES (:NEW.EMPNO,:NEW.ENAME,:NEW.JOB,:NEW.MGR,:NEW.HIREDATE,:NEW.SAL,:NEW.COMM,:NEW.DEPTNO);
END;


INSERT INTO V_EMP_INFO VALUES(8001,'大和','CLERK',7902,'13-12月-2020',1200,100,70,'销售部','伦敦');

SELECT * FROM EMP; 
SELECT * FROM DEPT;

```



管理触发器

```PLSQL
--启用或者禁用某个触发器
ALTER TRIGGER trigger_ name DISABLE | ENABLE
--启用或者禁用某个对象上的所有触发器
ALTER TABLE table_ name DISABLE | ENABLE ALL TRIGGERS
--重编译触发器
ALTER TRIGGER trigger_ name COMPILE
```



+ 系统触发器

  用户触发事件:

  + CREATE, ALTER，或者DROP命令
  + 登录或者退出数据库连接

  系统触发事件:

  + 启动、关闭数据库
  + 特殊错误发生

```plsql
CREATE OR REPLACE TRIGGER trigger_name
	timing
		[database event1 [or database event2 ...] ]
		ON {DATABASE|SCHEMA}
trigger_body


CREATE TABLE log_trig_table(
userid VARCHAR(20),
log_date DATE,
action VARCHAR(20)
);
--登录触发器，plsql登录时向表内插入一条数据
CREATE OR REPLACE TRIGGER TRI_LOGON
	AFTER LOGON ON SCHEMA
BEGIN
	INSERT INTO log_trig_table VALUES(USER,SYSDATE,'Logging on');
END;
--登出触发器，plsql登出时向表内插入一条数据
CREATE OR REPLACE TRIGGER TRI_LOGOFF
	BEFORE LOGOFF ON SCHEMA
BEGIN
	INSERT INTO log_trig_table VALUES(USER,SYSDATE,'Logging off');
END;
```



+ 作用

  触发器主要用于下列情况:

  + 安全性方面，确定用户的操作是否可以继续执行
  + 产生对数据值修改的审计，将修改的信息记录下来，产生数据改动记录
  + 提供更灵活的完整性校验规则，能根据复杂的规则校验数据
  + 提供表数据的同步复制，使多个表的数据同步
  + 事件日志记录，记录数据库的重要操作

# 15.DML语句

+ dml语句会引起数据的事务
+ 事务可以以回滚的方式(rollback)结束，所有操作被放弃，回滚到事务开始之前的状态
+ 事务可以以提交的方式(commit)结束，所有对数据库的修改都会被保存，其他用户也可以看到数据库的改变。
+ 在事务没有结束前，只有修改者自己可以看到数据库的改变，其他用户是看不到的。

## 15.1.插入

```sql
--插入数据
insert into dept(deptno,dname,loc) values(14, '销售部', 'china');
--插入部分字段
insert into dept(deptno,dname) values(14, '销售部');
--一次插入多条数据
insert into dept select * from dept;
```



## 15.2.删除

```sql
--删除一条或多条数据，可回滚
delete from dept where deptno=10;
```



## 15.3.更新

```sql
--在更新时，在事务未提交前，正在修改的数据是被锁住的，其他用户是无法修改该条数据的
update emp set ename='张三1' where empno=7566;
```



## 15.4.合并

```sql
merge into dept_back d
using dept s
on (d.deptno=s.deptno)
when matched then
	update set d.dname=s.dname ,d.loc=s.loc
when not matched then
	insert values(s.deptno,s.dname,s.loc);
```



# 16.DDL语句

## 16.1.  建表

```sql
--第一种方式建表
create table commodity_infom(
        Id  VARCHAR2(50) primary key,
        ccategory varchar2(100) ,
        cprice number(5,2) not null,
        cstock integer not null default 0 
);
--primary key设置当前字段为主键
--default 0 设置当前字段的默认值
--not null 设置当前字段不能为空

create table commodity_infom as select * from commodity_infom_tmp;
```



## 16.2.改表

```sql
--修改字段名或类型
alter table commodity_newsm rename column  cimgurl to  iimgurl;--修改字段名
--对表进行重命名，只能是表的所有者才可以修改，其他人（包含dba）都不可做这个操作
alter table commodity_newsm rename to 新表名;
alter table 表名 modify 列名 varchar(255);--修改字段类型

--删除字段
alter table  表名  drop column 列名; 

--增加字段
alter table 表名  add 列名 类型 default 值 not null; 

--查询字段
desc 表名；
```



## 16.3.删表

```sql
--清空表内数据，并将整个表结构删除
drop table 表名;

--清空表内数据，不可回滚（所以慎用）
truncate table 表名;
```


**注意**：truncate与delete的区别

1.区别比较大的，表面上看逻辑上是一样的。
truncate相当于是drop表以后建了一个同样定义的表（包括相关的约束和索引等）。
delete只是删除了表中的数据，在存储上来说只是在数据块上做了一个标记而已，数据没有真正删除，而且高水位线等还是和原来一样。 

2.truncate只删除对象数据而不删除对象的元数据，拉低高水位，在系统表里把相关的extend标记为未使用，而不写undo，无法恢复。
delete删除数据，要标记被delete的所有数据块，要写undo，可以恢复。
数据量大的话truncate比delete会快很多 



