# 8.Hibernate

## 8.1.介绍

![1559557610884](D:\MyNote\images\1559557610884.png)



![1559557700143](D:\MyNote\images\1559557700143.png)

## 8.2.初次使用

1.建立工程；

2.导入jar包；

​		jar包分为四部分，

- hibernate的核心jar包，即在hibernate文件夹下的hibernate3.jar；

- hibernate的必须的jar包，即在同路径下/lib/required的jar包；

- hibernate实现jpa规范的jar包，即同路径下/lib/jpa的jar包；

- 连接mysql用的jdbc的jar包；

  ![img](D:\MyNote\images\wps1.jpg)

3.创建数据库表；

```mysql
CREATE DATABASE DAY28;
USER DAY28;
CREATE TABLE `day28`.`t_user`( `id` INT NOT NULL AUTO_INCREMENT, `name` VARCHAR(20), `password` VARCHAR(20), PRIMARY KEY (`id`) ); 
```



4.建立ORM的映射文件；

​		文件来自hibernate文件夹下的/project/etc/hibernate.cfg.xml,这个是模板文件，将它复制进项目的src路径下即可。内容如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-configuration PUBLIC
 "-//Hibernate/Hibernate Configuration DTD 3.0//EN"
 "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">

<hibernate-configuration>
    <session-factory>
        <property name="hibernate.connection.driver_class">com.mysql.jdbc.Driver</property>
        <property name="hibernate.connection.username">root</property>
        <property name="hibernate.connection.password">root</property>
        <property name="hibernate.connection.url">jdbc:mysql://localhost:3306/day28</property>
        <!--show_sql：操作数据库时会打印sql语句-->
        <property name="show_sql">true</property>
        <!-- "format_sql"：打印sql语句前，对语句进行格式化 -->
        <property name="format_sql">true</property>
        <!-- hbm2ddl.auto:自动生成表结构 -->
        <property name="hbm2ddl.auto">update</property>
        <!-- hibernate.connection.autocommit:自动提交事务 -->
        <property name="hibernate.connection.autocommit">true</property>
		<!-- 引入实体类的ORM映射文件，路径是src后面的部分 -->
        <mapping resource="com/itheima/user/User.hbm.xml"/>
    </session-factory>
</hibernate-configuration>
```



上部新添加的的xml声明标签，中间的自带的dtd的引用，下面自己填的配置。

5.写一个实体类；

编写一个叫User的实体类，有3个属性，id,name,password；

6.编写这个实体类的映射文件；

文件与实体类放在同一路径下，名称是类名User+.hbm.xml，内容是:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-mapping PUBLIC 
    "-//Hibernate/Hibernate Mapping DTD 3.0//EN"
    "http://www.hibernate.org/dtd/hibernate-mapping-3.0.dtd">
<hibernate-mapping>
	<class name="com.itheima.user.User" table="t_user">
		<id name="id" column="id">
			<generator class="native"></generator>
		</id>
		<property name="name" column="name"></property>
		<property name="password" column="password"></property>
	</class>
</hibernate-mapping>
```



上部新添加的xml声明标签，中部的dtd引用来自于hibernate3.jar包中第一个包的最后一个dtd文件的dtd引用，下部是实体类与表的映射关系；

7.测试

```java
@Test
public void test02(){
    //读取配置文件
    Configuration config = new Configuration().configure();
    //根据配置文件，创建Factory
    SessionFactory factory = config.buildSessionFactory();
    //通过Factory获得操作数据库session对象
    Session session = factory.openSession();
    //操作数据库
    User user = new User();
    user.setName("tom");
    user.setPassword("1234");
    session.save(user);
    //关闭资源
    session.close();
    factory.close();
}
```



## 8.3.api详解

### 8.3.1.Configuration

​		Configuration是用户加载配置文件，Configuration调用configure()方法，加载src路径下hibernate.cfg.xml文件；如果配置文件不符合默认加载规则，我们可以调用configure(file)方法通过文件加载或configure(path)方法

通过路径加载。、

​		Configuration加载映射文件有2种方法，一种可以通过Configuration对象加载，但是不推荐，代码如下：

`configuration.addClass(User.class);` ；推荐的是另一种方式，在hibernate.cfg.xml配置文件中，使用mapping属性引入配置文件，代码如下：`<mapping resource="com/itheima/user/User.hbm.xml"/>`；

### 8.3.2.SessionFactory

​		SessionFactory 是创建session的工厂，根据Configuration配置信息创建SessionFactory的工厂类。通过SessionFactory获得Session有2种结果，一个是通过openSession()获取一个全新的Session对象；另一种是通过getCurrentSession()获取当前线程绑定的Session，这种方式的使用还需要在hibernate.cfg.xml配置文件中配置一下才可以，配置如下：

`<property name="hibernate.current_session_context_class">thread</property>` ,

内部的值暂时是thread。

​		getCurrentSession()类似于使用了ThreadLocal的Connection。

### 8.3.3.Session

​		session的增删改查；

- 增：

  ```java
  Configuration config = new Configuration().configure();
  //根据配置文件，创建Factory
  SessionFactory factory = config.buildSessionFactory();
  //通过Fac|tory获得操作数据库session对象
  Session session = factory.openSession();
  //操作数据库
  User user = new User();
  user.setName("tom");
  user.setPassword("1234");
  session.save(user);
  //关闭资源
  session.close();
  factory.close();
  ```



- 删：

  ```java
  Configuration config = new Configuration().configure();
  //根据配置文件，创建Factory
  SessionFactory factory = config.buildSessionFactory();
  //通过Fac|tory获得操作数据库session对象
  Session session = factory.openSession();
  //操作数据库
  Transaction transaction = session.beginTransaction();
  transaction.begin();
  //User user = new User();
  //user.setId(1);
  User user = (User)session.get(User.class, 1);
  session.delete(user);
  transaction.commit();
  //关闭资源
  session.close();
  factory.close();
  ```



- 改：

  ```java
  Configuration config = new Configuration().configure();
  //根据配置文件，创建Factory
  SessionFactory factory = config.buildSessionFactory();
  //通过Fac|tory获得操作数据库session对象
  Session session = factory.openSession();
  //操作数据库
  Transaction transaction = session.beginTransaction();
  transaction.begin();
  User user = (User)session.get(User.class, 1);
  user.setName("汤姆");
  session.update(user);
  transaction.commit();
  //关闭资源
  session.close();
  factory.close();
  ```

  

- 查-get()方法：这种方式是直接查出来并返回结果

  ```java
  Configuration config = new Configuration().configure();
  //根据配置文件，创建Factory
  SessionFactory factory = config.buildSessionFactory();
  //通过Fac|tory获得操作数据库session对象
  Session session = factory.openSession();
  //操作数据库
  User user = (User)session.get(User.class, 2);
  System.out.println(user.toString());
  //关闭资源
  session.close();
  factory.close();
  ```



- 查-load()方法：这种方法是使用代理，先不查，当需要使用对象的属性时才回去查，类似于懒加载技术。

  ```java
  Configuration config = new Configuration().configure();
  //根据配置文件，创建Factory
  SessionFactory factory = config.buildSessionFactory();
  //通过Fac|tory获得操作数据库session对象
  Session session = factory.openSession();
  //操作数据库
  User user = (User)session.load(User.class, 2);
  System.out.println(user.toString());
  //关闭资源
  session.close();
  factory.close();
  ```



- 查-HQL语言：hibernate query langage

  Query对象是封装HQL语言的对象，内部封装了查询细节。

  Query对象有list()方法，用于返回多行结果；

  ```java
  Configuration config = new Configuration().configure();
  //根据配置文件，创建Factory
  SessionFactory factory = config.buildSessionFactory();
  //通过Fac|tory获得操作数据库session对象
  Session session = factory.openSession();
  //操作数据库
  Query query = session.createQuery("from com.itheima.user.User");
  List<User> list = query.list();
  System.out.println(list.toString());
  //关闭资源
  session.close();
  factory.close();
  ```



​	有uniqueResult()方法，用于返回一行结果；

```java
Query query = session.createQuery("from com.itheima.user.User where id='2'");
User user = (User) query.uniqueResult();
```



有setFirstResult()和setMaxResults()进行分页

```java
Query query = session.createQuery("from com.itheima.user.User");
query.setFirstResult(0);
query.setMaxResults(2);
List<User> user = query.list();
System.out.println(user.toString());
```



- 查-Criteria：与HQL调用方式类似

  同样有list()方法

  ```java
  Configuration config = new Configuration().configure();
  //根据配置文件，创建Factory
  SessionFactory factory = config.buildSessionFactory();
  //通过Fac|tory获得操作数据库session对象
  Session session = factory.openSession();
  //操作数据库
  Criteria criteria = session.createCriteria(User.class);
  List<User> list = criteria.list();
  System.out.println(list.toString());
  //关闭资源
  session.close();
  factory.close();
  ```



​	同样有uniqueResult()方法

```java
Criteria criteria = session.createCriteria(User.class);
criteria.add(Restrictions.eq("name", "rose"));
User user = (User) criteria.uniqueResult();
System.out.println(user.toString());
```



他还可以设置条件：

```java
Criteria criteria = session.createCriteria(User.class);
criteria.add(Restrictions.eq("name", "rose"));//查询name=tom的数据
User user = (User) criteria.uniqueResult();
System.out.println(user.toString());
//----------------------------------------------------------------------------
Criteria criteria = session.createCriteria(User.class);
criteria.add(Restrictions.like("name", "%os%"));//查询like '%os%'的数据
List<User> list = criteria.list();
System.out.println(list.toString());
//--------------------------------------------------------------------------
Criteria criteria = session.createCriteria(User.class);
criteria.add(Restrictions.gt("id", 1));//查询id>1的数据
List<User> list = criteria.list();
System.out.println(list.toString());
/*  gt >
 * 	lt <
 * 	eq =
 * 	ge >=
 * 	le <=
 *  like
 *  between
 * */
```



​	

- 查-SQLQuery：支持原生的sql语句

  ```java
  Configuration config = new Configuration().configure();
  //根据配置文件，创建Factory
  SessionFactory factory = config.buildSessionFactory();
  //通过Fac|tory获得操作数据库session对象
  Session session = factory.openSession();
  //操作数据库
  SQLQuery query = session.createSQLQuery("select * from t_user");
  query.addEntity(User.class);//如果不加这一句就会list打印出一串地址
  List list = query.list();
  System.out.println(list.toString());
  //关闭资源
  session.close();
  factory.close();
  ```



- 事务相关

  - 开启事务是`session.beginTransaction();`;

  - 提交事务是

    ```java
    Transaction transaction = session.beginTransaction();
    transaction.commit();
    ```

  - 回滚事务是

    ```java
    Transaction transaction = session.beginTransaction();
    transaction.rollback();
    ```



- evict 将缓存中对象清除；
- clear 清空一级缓存

```java
User user = session.get(User.class, 1);
session.clear();
User user2 = session.get(User.class, 1);
//结果会打印两次，说明一级缓存被清空了
```



- refresh() 强制刷新一级缓存中的对象（用于解决缓存与数据库数据不同步的问题）

```java
User user = session.get(User.class, 1);
session.refresh();
//结果会打印两次，说明refresh()会将缓存中的对象与数据库同步，再次发送一次sql语句
```



- flush() 手动提交一级缓存中的对象

```java
User user = session.get(User.class, 1);
user.setName("tom")
session.flush();
//将一级缓存中的对象立刻提交到数据库
```



- saveOrUpdate():提交或更新数据库

```java
User user = new User();
user.setName("tom");
user.setPassword("1234");
session.saveOrUpdate(user);
//主键生成策略为native时，主键为空时，插入数据库
//主键生成策略为assigned时，主键为空时，报错
User user = new User();
user.setId(1);
user.setName("tomm");
user.setPassword("1234");
session.saveOrUpdate(user);
//主键生成策略为native时，主键不为空时，更新数据库
//主键生成策略为assigned且主键不为空时，根据主键查询数据库并在commit时会根据查询结果的有无进行插入或更新
```



## 8.4.主配置文件详解

### 8.4.1.hbm2ddl.auto

hbm2ddl.auto是自动生成表结构的配置策略；值有4个，分别是update,create,create-drop,validate。

update:最常用的取值，如果当前数据库就不存在表结构则自动创建表结构；

​			  如果存在表结构，且表结构与实体一致，则不做修改；

​			  如果存在表结构，但表结构与实体不一致，则修改表结构，并保留原有列；

create:很少使用的值，无论是否存在表结构，每次启动Hibernate都会重新创建表结构，数据会丢失。

create-drop:极少使用的值，无论是否存在表结构，每次启动Hibernate都会重新创建表结构，

​					  每次关闭Hibernate都会删除表结构，数据会丢失。

validate:很少使用的值，不会自动创建表结构，也不会自动维护表结构，只会校验表结构，如果表结构与实体			   不一致则抛出异常；

### 8.4.2.hibernate.dialect

hibernate.dialect是数据库方言的配置策略，例如MySql的方言，如下：

```xml
<!-- 
   数据库方言的配置策略：hibernate.dialect
   MySql的有三种：
    org.hibernate.dialect.MySQLDialect(一般选最短的)
    org.hibernate.dialect.MySQLInnoDBDialect
    org.hibernate.dialect.MySQLMyISAMDialect-->
<property name="hibernate.dialect">org.hibernate.dialect.MySQLDialect</property>
```



关于分页，MySql中使用的是limit，而oracle中使用的是rownum.

## 8.5.持久化类

### 8.5.1.编写规则

- 提供一个无参数 public访问控制符的构造器
- 提供一个标识属性，用于映射数据表的主键字段
- 所有属性都要提供public访问控制符的 set  get 方法(javaBean)
- 标识属性应尽量使用基本数据类型的包装类型
- 不要用final修饰实体 （将无法生成代理对象进行优化）

### 8.5.2.持久化对象的唯一标识 OID

- Java按地址区分同一个类的不同对象

- 关系数据库用主键区分同一条记录

- Hibernate使用OID来建立内存中的对象和数据库中记录的对应关系

  结论: 对象的OID和数据库的表的主键对应。为保证OID的唯一性，应该让Hibernate来为OID付值

### 8.5.3.区分自然主键和代理主键

- 主键需要具备: 不为空/不能重复/不能改变
  - 自然主键:	在业务中,某个属性符合主键的三个要求.那么该属性可以作为主键列
    - 代理主键: 	在业务中,不存符合以上3个条件的属性,那么就增加一个没有意义的列.作为主键

### 8.5.4.基本数据与包装类型

- 基本数据类型和包装类型对应hibernate的映射类型相同
- 基本类型无法表达null、数字类型的默认值为0。
- 包装类默认值是null。当对于默认值有业务意义的时候需要使用包装类。

### 8.5.5.主键生成策略

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-mapping PUBLIC 
    "-//Hibernate/Hibernate Mapping DTD 3.0//EN"
    "http://www.hibernate.org/dtd/hibernate-mapping-3.0.dtd">
<!-- package: 配置该配置文件中类所在的包 -->
<hibernate-mapping package="com.itheima.user">
    <!-- dynamic-insert:默认值是"false"，是否支持动态生成insert语句,该值为true时，
						MySql插入时如果有某一列没有值则不会插入这一列
  		 dynamic-update:默认值是"false",是否支持动态生成update语句 ,该值为true时，
						MySql更新时如果有某一列没有值则不会更新这一列-->
    <class name="User" table="t_user" dynamic-insert="false" dynamic-update="false">
        <!-- unsaved-value:当该属性为该值时，该属性被认为是null而不作处理 
             access:不推荐使用，如果将值设置为field，
            		则hibernate会绕过实体类的get,set方法通过反射直接操作实体类的属性-->
        <id name="id" column="id" unsaved-value="0" access="">
        <!-- generator:主键生成策略，有7个值
                    1.increment 由hibernate自己维护自动增长，底层通过先查询max值，再+1策略
                                不建议使用，存在线程并发问题
                    2.identity  hibernate底层采用数据库本身自动增长列，
                                例如：mysql sqlserver 都是auto_increment
                    3.sequence  hibernate底层采用数据库序列
                                例如：oracle 提供序列
                    4.hilo 	    hibernate自身的一种算法，可以提供生成id的功能
                    5.native    根据底层数据库的能力选择 identity、sequence 或者 hilo 中的一个。
                    ##以上策略使用整形，long, short 或者 int 类型
                    6.uuid 		采用字符串唯一值【】
                    ##以上策略 代理主键，有hibernate维护。
                    7.assigned 	适用于自然主键，由程序自己维护。 -->
            <generator class="native"></generator>
        </id>
        <!-- 
			insert: 默认为true，该属性是否加入insert语句
			update: 默认为true，该属性是否加入update语句
			length: 数据长度
			not-null: 默认为true,该列约束是否是空
			unique: 默认值为false，该列约束是否唯一
			precision: 数字小数位数
			scale: 数字有效数字位数			
		 -->
        <!--
			type:表达数据的类型
				 可以用三种方式指定属性
			java类型        数据库类型           hibernate
			java.lang.String  varchar          string
		-->
        <property name="name" column="name"></property>
        <property name="password" column="password"></property>
    </class>
</hibernate-mapping>
```



type:表达数据的类型

| Java数据类型                       | Hibernate数据类型 | 标准SQL数据类型 (PS:对于不同的DB可能有所差异) |
| ---------------------------------- | ----------------- | --------------------------------------------- |
| byte、java.lang.Byte               | byte              | TINYINT                                       |
| short、java.lang.Short             | short             | SMALLINT                                      |
| int、java.lang.Integer             | integer           | INGEGER                                       |
| long、java.lang.Long               | long              | BIGINT                                        |
| float、java.lang.Float             | float             | FLOAT                                         |
| double、java.lang.Double           | double            | DOUBLE                                        |
| java.math.BigDecimal               | big_decimal       | NUMERIC                                       |
| char、java.lang.Character          | character         | CHAR(1)                                       |
| boolean、java.lang.Boolean         | boolean           | BIT                                           |
| java.lang.String                   | string            | VARCHAR                                       |
| boolean、java.lang.Boolean         | yes_no            | CHAR(1)('Y'或'N')                             |
| boolean、java.lang.Boolean         | true_false        | CHAR(1)('Y'或'N')                             |
| java.util.Date、java.sql.Date      | date              | DATE                                          |
| java.util.Date、java.sql.Time      | time              | TIME                                          |
| java.util.Date、java.sql.Timestamp | timestamp         | TIMESTAMP                                     |
| java.util.Calendar                 | calendar          | TIMESTAMP                                     |
| java.util.Calendar                 | calendar_date     | DATE                                          |
| byte[]                             | binary            | VARBINARY、BLOB                               |
| java.lang.String                   | text              | CLOB                                          |
| java.io.Serializable               | serializable      | VARBINARY、BLOB                               |
| java.sql.Clob                      | clob              | CLOB                                          |
| java.sql.Blob                      | blob              | BLOB                                          |
| java.lang.Class                    | class             | VARCHAR                                       |
| java.util.Locale                   | locale            | VARCHAR                                       |
| java.util.TimeZone                 | timezone          | VARCHAR                                       |
| java.util.Currency                 | currency          | VARCHAR                                       |



## 8.6.对象状态

在Hibernate中，对象有三种状态，他们的定义分别是：

瞬时态/临时态:

- 1.没有与Hibernate产生关联;
- 2.与数据库的记录没有产生关联(有关联就是与数据库中的id有对应);

持久态:

- 1.与Hibernate有关联；
- 2.对象有ID;

游离态/托管态:

- 1.没有与Hibernate产生关联;
- 2.对象有ID;

案例:

```java
@Test
public void test02(){
    //通过Fac|tory获得操作数据库session对象
    Session session = HibernateUtil.openSession();
    //操作数据库
    session.beginTransaction();
    User user = new User();//瞬时态
    user.setName("tom");//瞬时态
    user.setPassword("1234");//瞬时态
    session.save(user);//持久态

    session.getTransaction().commit();//持久态
    //关闭资源
    session.close();//游离态
}
```



对象状态之间的转换：

瞬时转持久：首先建立对象，然后对象调用save()方法即可；

瞬时转游离：首先建立对象，然后为对象指定一个数据库中已有的id；

持久转瞬时：:one: 首先通过session的get()方法得到一个对象，然后关闭session，将对象的id设置为null；

​						:two: 首先通过session的get()方法得到一个对象，然后对象调用evict()方法将对象与session的关联移							 除，再将对象的id设置为null；

持久转游离： :one: 首先通过session的get()方法得到一个对象,然后对象调用evict()方法将对象与session的关联移除;

​					   :two: 首先通过session的get()方法得到一个对象，然后关闭session;

游离转瞬时：首先通过session的get()方法得到一个对象，然后对象调用evict()方法将对象与session的关联移						除，再将对象的id设置为null;

游离转持久：首先通过session的get()方法得到一个对象，然后对象调用evict()方法将对象与session的关联移						除，再通过session更新对象；

## 8.7.一级缓存

学习缓存是为了更深层次的理解Hibernate中对象的操作。Hibernate中存在的缓存是为了提高效率。

Hibernate中缓存存在两种：

- 线程级别的缓存。session缓存，即本节内容；
- 进程级别的缓存。Hibernate   二级缓存；

sssion缓存：就是session对象中存在的缓存

一级缓存的快照：在从数据库中取出数据时，会将数据一式两份，一份作为缓存中的对象，一份作为快照中的对象，方便在session提交时作为对比。

​		save()与persist()方法是功能相同名称不同的两个方法。save()过时。

​		HQL查询结果不会使用一级缓存(测试：同一批量查询连续执行查看打印了多少条sql语句)，但是HQL批量查询结果会进入缓存(测试：先是批量查询然后查询结果中包含的一条，看打印了多少条sql语句)。

​		SQL查询结果如果封装进对象里，则会进入一级缓存；没有则不会进入一级缓存。

​		criteria对象与HQL结果一致，查询结果会进一级缓存，但是查询不会使用一级缓存。

## 8.8.多表设计

### 8.8.1.一对多与多对一

1.实体类

多的一方

```java
public class Order {

	private Integer id;
	private String  name;
	
	private Customer customer;
//get、set方法
```



一的一方

```java
public class Customer {

	private Integer id;
	private String  name;
//在1对多中少的一方可通过使用set集合表示多的一方
	private Set<Order> order = new HashSet<Order>();
//get、set方法
```



2.配置实体类的映射文件

Order.hbm.xml

```xml
<hibernate-mapping package="com.itheima.user">
	<class name="Order" table="t_order">
		<id name="id" column="id">
			<generator class="native"></generator>
		</id>
		<property name="name" column="name" type="string"></property>
	<!-- many-to-one: 表示多对一的关系
		 name: 表示引用的属性的名称
		 column: 外键的列名
		 class: 引用的类的完整类名
		  -->
	<many-to-one name="customer" class="Customer" column="cid"></many-to-one>
	</class>
</hibernate-mapping>
```



Customer.hbm.xml

```xml
<hibernate-mapping package="com.itheima.user">
	<class name="Customer" table="t_customer">
		<id name="id" column="id">
			<generator class="native"></generator>
		</id>
		<property name="name" column="name"></property>
	<!-- set: 表示一对多的关系
		 name:集合属性的名称
		 inverse: 是否将关系的维护反转给对方，默认值：false
		 		  值为true时，此方将放弃维护外键关系
		 cascade: 级联操作
		 	save-update: 级联保存，级联修改，保存A同时保存B
		 	delete: 级联删除，删除A同时删除B，则AB都不存在
		 	delete-orphan: 孤儿删除，解除关系，同时将B删除，A存在的；
		 	（同时配置多项需要用逗号分隔，例如：
		 	cascade="save-update,delete"）
		 	all: save-update和delete的整合
		 	all-delete-orphan: 三个的整合
	 -->
	<set name="order" inverse="true" cascade="save-update">
	<!-- key: 用来表示外键
		 column: 外键的值
	-->
		<key column="cid"></key>
		<!-- one-to-many: 用来表示Customer与order的关系
			 class: 表示关联的另一方的完整类名 -->
		<one-to-many class="Order"/>
	</set>
	</class>
</hibernate-mapping>
```



3.多表关系添加

```java
@Test
//多表关系=》增
//前三条打印insert语句，维护对象与外键
//后两句update语句有一次维护外键
//维护对象时，会自动维护另一方的关系
//多次维护解决办法是单纯指定关系由一方来维护，另一方不用维护
//注意： 外键的维护能否放弃只能由非外键的对象来放弃

//维护一方对象时，会自动维护另一方对象
//配置了inverse后，
//删除会报错，因为Customer已经不再维护外键了，直接删除会导致order一方引用无效的id，违反外键的约束
public void test04(){
    //通过Factory获得操作数据库session对象
    Session session = HibernateUtil.openSession();
    //操作数据库
    session.beginTransaction();
    Customer customer = new Customer();
    customer.setName("tom");

    Order order1 = new Order();
    order1.setName("香蕉");
    Order order2 = new Order();
    order2.setName("葡萄");

    //customer.getOrder().add(order1); //配置了inverse后，
    //customer.getOrder().add(order2); //配置了inverse后， 
	order1.setCustomer(customer);
	order2.setCustomer(customer);
    
    session.save(order1);
    session.save(order2);
    session.save(customer);
    session.getTransaction().commit();
    //关闭资源
    session.close();
}
```





4.多表关系删除

```java
Customer customer = (Customer)session.get(Customer.class, 4);
Set<Order> set = customer.getOrder(); //配置了inverse后，
for(Order order: set){ 				  //配置了inverse后，
    order.setCustomer(null);		  //配置了inverse后，
}										
session.delete(customer);
```

5.cascade="save-update"的demo

```java
@Test
public void test06(){
    //通过Factory获得操作数据库session对象
    Session session = HibernateUtil.openSession();
    //操作数据库
    session.beginTransaction();
    Customer customer = (Customer)session.get(Customer.class, 5);
    for(Order order: customer.getOrder()){
        order.setName("西瓜");
    }
    session.getTransaction().commit();
    //关闭资源
    session.close();
}
```



6.cascade="delete"的demo

```java
/*
 * cascade:delete
 * 注意：cascade不能在两边都配置级联删除，否则删除一方，会导致两方都会被删除
* */
@Test
public void test07(){
    //通过Factory获得操作数据库session对象
    Session session = HibernateUtil.openSession();
    //操作数据库
    session.beginTransaction();
    Customer customer = (Customer)session.get(Customer.class, 5);
    session.delete(customer);
    session.getTransaction().commit();
    //关闭资源
    session.close();
}
```

7.cascade="delete"的demo

```java
/*
 * cascade:delete-orphan
 * 
 * */
@Test
public void test08(){
    //通过Factory获得操作数据库session对象
    Session session = HibernateUtil.openSession();
    //操作数据库
    session.beginTransaction();
    Customer customer = (Customer)session.get(Customer.class, 6);
    Iterator<Order> iterator = customer.getOrder().iterator();
    //注意：删除订单时，不可以使用customer.setOrder(null);或customer.setOrder(new HashSet());
    while(iterator.hasNext()){//遍历customer的订单，并将订单删除=>并维护关系
        iterator.next();
        iterator.remove();
    }
    session.getTransaction().commit();
    //关闭资源
    session.close();
}
```



### 8.8.2.多对多





### 8.8.3.一对一