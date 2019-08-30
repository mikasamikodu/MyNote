# 4. oracle

> oracle内部不能使用双引号，必须用单引号

## 4.1.  创建表table

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

### 4.1.1. 设置默认值

```sql
itime date not null default sysdate,--设置系统时间为默认值
ipraise integer default 0,--设置0为默认值
```



## 4.2. 创建序列sequence

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



## 4.3. 创建触发器trigger

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

## 4.4. 创建外键关联

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

## 4.5. 修改列名与类型

```sql
alter table commodity_newsm rename column  cimgurl to  iimgurl;--修改列名
alter table 表名 modify (列名varchar(255));--修改列类型
--修改列类型也可以通过编辑表的列名和类型修改
alter table  表名  drop column 列名; --删除一列
alter table 表名  add 列名   类型   default   值 < not null>; --增加一列
```

## 4.6. 添加唯一约束

```sql
alter table user_infom
add constraint user_infom_name_unique unique(uname);
--为表user_infom的uname列添加唯一约束，名称为user_infom_name_unique
```

## 4.7. 添加外键约束

```sql
--普通外键约束（如果存在子表引用父表主键，则无法删除父表记录）
ALTER TABLE commodity_newsd ADD CONSTRAINT commodity_newsd_foreign_key FOREIGN KEY(imainid) REFERENCES commodity_newsm(id);
--级联外键约束（可删除存在引用的父表记录，而且同时把所有有引用的子表记录也删除）
ALTER TABLE commodity_newsd ADD CONSTRAINT commodity_newsd_foreign_key FOREIGN KEY(imainid) REFERENCES commodity_newsm(id) ON DELETE CASCADE;
--置空外键约束（可删除存在引用的父表记录，同时将子表中引用该父表主键的外键字段自动设为NULL，但该字段应
--允许空值）
ALTER TABLE commodity_newsd ADD CONSTRAINT commodity_newsd_foreign_key FOREIGN KEY(imainid) REFERENCES commodity_newsm(id) ON DELETE SET NULL;
```

## 4.8. java连接oracle

```java
private static String driver = "oracle.jdbc.driver.OracleDriver";
private static String url="jdbc:oracle:thin:@127.0.0.1:1521:orcl";
private static String username="websjkknow";
private static String password="websjkknow";
```