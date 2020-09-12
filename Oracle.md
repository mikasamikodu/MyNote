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

# 2.  创建表table

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

```sql
create table commodity_infom(
        Id  VARCHAR2(50) primary key,/*设置id为主键*/
        cindex integer not null,
        cname VARCHAR2(100) NOT NULL ,
        ckind varchar2(20) not null,
        ckindid varchar2(20) not null,
        ccategory varchar2(100) ,
        cprice number(5,2) not null,
        cstock integer not null,
        cimgurl varchar2(100) not null,
        cdescription varchar2(500),
        utemp1 varchar2(100),
        utemp2 varchar2(100),
        utemp3 varchar2(100)
);
```

## 1.1. 设置默认值

```sql
itime date not null default sysdate,--设置系统时间为默认值
ipraise integer default 0,--设置0为默认值
```



# 2. 创建序列sequence

```sql
create sequence commodity_infom_tb_seq minvalue 1 maxvalue 9999    
         increment by 1    
         start with 1;
 /*为表commodity_infom建立一个自动增长的序列，名称为commodity_infom_tb_seq，从1开始，最大9999，每次增长1*/
```

> 删除序列

```sql
DROP SEQUENCE commodity_infom_tb_seq  --删除序列
```



# 3. 创建触发器trigger

```sql
create or replace trigger commodity_infom_tb_tri
before insert on commodity_infom
for each row
begin
select  commodity_infom_tb_seq.nextval into :new.cindex from dual;
end;
 /*为表commodity_infom建立一个触发器，名称为commodity_infom_tb_tri，每次在表commodity_infom插入一行数据时触发这个触发器，会从序列中commodity_infom_tb_seq找到下一个值放入表commodity_infom的cindex列*/
```

> 删除触发器

```sql
DROP TRIGGER commodity_infom_tb_tri  --删除触发器
```

#  4.创建外键关联

```sql
create table commodity_infod(
        Id  VARCHAR2(50) primary key ,
        cmainid varchar2(50) not null references commodity_infom(id),
    	cpicture varchar2(100) not null,
        utemp1 varchar2(100),
        utemp2 varchar2(100),
        utemp3 varchar2(100)
);
/*将cmainid设置为主表commodity_infom的外键，用主表id进行关联*/
```

# 5. 修改列名与类型

```sql
alter table commodity_newsm rename column  cimgurl to  iimgurl;--修改列名
alter table 表名 modify (列名varchar(255));--修改列类型
--修改列类型也可以通过编辑表的列名和类型修改
alter table  表名  drop column 列名; --删除一列
alter table 表名  add 列名   类型   default   值 < not null>; --增加一列
```

# 6. 添加唯一约束

```sql
alter table user_infom
add constraint user_infom_name_unique unique(uname);
--为表user_infom的uname列添加唯一约束，名称为user_infom_name_unique
```

# 7. 添加外键约束

```sql
--普通外键约束（如果存在子表引用父表主键，则无法删除父表记录）
ALTER TABLE commodity_newsd ADD CONSTRAINT commodity_newsd_foreign_key FOREIGN KEY(imainid) REFERENCES commodity_newsm(id);
--级联外键约束（可删除存在引用的父表记录，而且同时把所有有引用的子表记录也删除）
ALTER TABLE commodity_newsd ADD CONSTRAINT commodity_newsd_foreign_key FOREIGN KEY(imainid) REFERENCES commodity_newsm(id) ON DELETE CASCADE;
--置空外键约束（可删除存在引用的父表记录，同时将子表中引用该父表主键的外键字段自动设为NULL，但该字段应
--允许空值）
ALTER TABLE commodity_newsd ADD CONSTRAINT commodity_newsd_foreign_key FOREIGN KEY(imainid) REFERENCES commodity_newsm(id) ON DELETE SET NULL;
```

# 8. java连接oracle

```java
private static String driver = "oracle.jdbc.driver.OracleDriver";
private static String url="jdbc:oracle:thin:@127.0.0.1:1521:orcl";
private static String username="websjkknow";
private static String password="websjkknow";
```



emp

![1599292113978](C:\Users\MyPC\AppData\Roaming\Typora\typora-user-images\1599292113978.png)



DEPT

![1599292155176](C:\Users\MyPC\AppData\Roaming\Typora\typora-user-images\1599292155176.png)

# 9.查看

## 9.1查看表结构

desc 表名;

例如：desc emp;查看emp这张表的表结构

## 9.2查询

```sql
oracle中sql语句不区分大小写，包括登录数据库时的用户名与密码

在查询过程中，对于数值型的数据可以进行加减乘除的运算

select sal*12 from emp;

为查询结果中的字段起别名（字段  as  别名或字段  别名）

select sal\*12 as "年薪" from emp;
select sal\*12  "年薪" from emp;

在算术表达式中出现null，则结果必为null，null不等于0

用||可以把查询结果中两列过多列字段合并到一起
select empno,ename,job,empno||ename||job "员工信息" from emp;

在连接表达式中出现字符型数据，字符型数据就必须用'',二不能是""
在连接表达式中出现null，就是原来的字符型数据是null
任何类型的数据都支持null

日期型数据支持加减的运算，一个日期加减一个整型数字，等于在这个日期上加减一个天数;如果是两个日期相减就是得到日期之间相差的天数，日期之间不能相加或乘除

去重可以使用distinct关键字，案例：
select distinct deptno from emp;
select distinct deptno,job from emp;

对于日期型数据，格式是敏感的，使用日期型数据的格式是dd-mm-yyyy(日-月-年)
如果是中文版，格式是dd-mm月-yyyy
select 	empno from emp where hirdate='20-2月-2019';

改变当前会话中的日期格式
alter session set nls_date_format='YYYY-MM-DD HH:Mi:SS'

比较运算符：>,<,=,>=,<=,!=(不等于),<>(不等于)，between...and...,in (...), like '...',is null,
is not null

like 用于模糊匹配
select * from emp where ename like '%a%';--查找字符串中含有a的字符串
%代表0或多个字符，_代表一个字符
select * from emp where ename like '%\%%' escape '\';
--查找字符串中含有%的字符串。通过escape指定like里面的指定转义字符。

--排序 order by 
select * from emp order by ename;默认升序排列
select * from emp order by ename desc;降序排列
```



# 11.oracle练习题

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
说明：如果c1长度小于x，则返回x1左边x个字符
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

SQL> select to_char(sysdate,' PM yyyy-mm-dd hh24:mi:sssss AD year mon day ddd iw') FROM DUAL;
TO_CHAR(SYSDATE,'PMYYYY-MM-DDH
--------------------------------------------------------------------------------
上午 2008-03-27 09:58:35917 公元 two thousand eight 3月 星期四 087 13
SQL> SELECT TO_CHAR(SYSTIMESTAMP,'HH24:MI:SS.FF5') FROM DUAL;
TO_CHAR(SYSTIMESTAMP,'HH24:MI:
------------------------------
10:02:28.90000
SQL>SELECT TO_CHAR(SYSDATE,'DS DL') FROM DUAL
TO_CHAR(SYSDATE,'DSDL')
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











14.ifelse功能

示例：

```sql
--第一种方法：
select ename,job,sal,
		case job
		 when 'CLERK' then 1.10*sal
		 when 'SALESMAN' then 1.45*sal
		 when 'MANAGER' then 1.30*sal
		 else sal
		 end as "修订工资数"
		 from emp;
--第二种方法
select ename,job,sal,
		decode(job,
              'CLERK',1.10*sal,
               'MANAGER',1.30*sal,
              'SALESMAN',1.45*sal,
              sal) as "修订工资数"
		 from emp;
```



所有组函数都是忽略空值的

avg()和sum()只用于数值计算，max(),min()除了数值还可以对字符进行计算



# 13.多表查询

多表查询对应不同的标准

sql1992的标准：

1.等值查询，在父子表关系上，用等号(=)来连接两个表的两个字符或多个字符
示例：

```sql
select * from emp e,dept d where e.deptno=d.deptno;
select * from emp e,dept d where e.deptno=d.deptno and e.deptno=10;
select * from emp e,dept d,location l where e.deptno=d.deptno and d.loc_id=l.locid;
```



2.非等值查询，两个表之间没有父子关系，用!=来连接两个表

示例：

```sql
select e.empno,e.ename,e.sal,s.grade,s.losal,s.hisal
from emp e, salgrade s
where e.sal between s.losal and s.hisal;
```



3.自连接，通过别名，将一个表虚拟为两个表，并在这两个表上做等值查询

```sql
select * from emp a,emp b where a.empno=b.empno;
```









