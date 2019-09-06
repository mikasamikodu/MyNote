# 11.Mybatis

## 11.1.mybatis入门

​		搭建环境：

   * 创建maven工程，导入坐标；

   * 创建实体类及dao层接口；

   * 创建mybatis的主配置文件SqlMapConfig.xml；

   * 创建映射配置文件IUserDao.xml；

     ​	搭建环境时的注意事项：

* 在mybatis中，他把持久层操作也映射文件叫做Mapper；
* 在idea中创建目录时，包的创建是三级目录，如com.itheima.dao是com->itheima->dao三级目录；目录创建时是一级目录，如com.itheima.dao是com.itheima.dao一级目录；
* mybatis的映射配置文件位置必须和dao接口的包结构相同，如dao接口在com.itheima.dao下，则映射配置文件也要在com.itheima.dao下；
* 映射文件的mapper标签的namespace属性取值必须是dao接口的全限定类名com.itheima.dao.Dao；
* 映射文件的操作配置(select)，id属性的取值必须是dao接口的方法名；

## 11.2.入门案例

```java
public static void main(String[] args) throws Exception{
    //1.读取配置文件
    InputStream  in = Resources.getResourceAsStream("sqlMapConfig.xml");
    //2.创建sqlsessionfactory工厂
    SqlSessionFactoryBuilder builder = new SqlSessionFactoryBuilder();
    SqlSessionFactory sqlSessionFactory = builder.build(in);
    //3. 使用工厂生产sqlsession对象
    SqlSession session = sqlSessionFactory.openSession();
    //4.使用sqlsession创建dao接口的地代理对象
    IUserDao dao = session.getMapper(IUserDao.class);
    //5.使用代理对象执行方法
    List<User> users = dao.findAll();
    for(User user: users){
        System.out.println(user);
    }
    session.close();
    in.close();
   }
```

mybatis基于注解的入门案例：
把IUserDao.xml移除，在dao接口的方法上使用@Select注解，并且指定SQL语句
同时需要在SqlMapConfig.xml中的mapper配置时，使用class属性指定dao接口的全限定类名。
明确：
我们在实际开发中，都是越简便越好，所以都是采用不写dao实现类的方式。
不管使用XML还是注解配置。
但是Mybatis它是支持写dao实现类的。

##  11.3.MyBatis的CRUD

### 11.3.1.dao层

首先是：IUserDao.java

```java
import com.itheima.domain.User;
import java.util.List;
public interface IUserDao {
    /**
     * 查询所有用户
     * @return
     */
    List<User> findAll();
    /**
     * 保存用户信息
     * @param user
     */
    void save(User user);
    /**
     * 更新用户信息
     * @param user
     */
    void update(User user);
    /**
     * 根据id删除用户
     * @param id
     */
    void delete(Integer id);
    /**
     * 通过id查询用户信息
     * @param id
     * @return
     */
    User findById(Integer id);
    /**
     * 通过name查询用户
     * @param uasername
     * @return
     */
    List<User> findByName(String uasername);
    
    /**
     * 查询所有用户数量
     * @return
     */
    int findTotal(); 
     /**
     * 通过queryVo查询用户
     * @param vo  封装后的参数
     * @return 用户列表
     */
    List<User> findByVo(QueryVo vo);
}
```

### 11.3.2.xml文件

然后是IUserDao.xml

注：xml文件的路径必须与其对应的java文件路径相同,如IUserDao.java的路径是com.itheima.dao.IUserDao.java，则IUserDao.xml路径是com.itheima.dao.IUserDao.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper
        PUBLIC  "-//mybatis.org/DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.itheima.dao.IUserDao">
    <!-- 查询所有 -->
    <select id="findAll" resultType="com.itheima.domain.User">
        select * from user
    </select>

    <!-- 通过id查询用户信息 -->
    <select id="findById" resultType="com.itheima.domain.User" parameterType="Integer">
        select * from user where id=#{id}
    </select>

    <!-- 通过name查询用户信息 -->
    <select id="findByName" resultType="com.itheima.domain.User" parameterType="java.lang.String">
        select * from user where username like #{usernsme}
   <!--select * from user where username like '${value}' 
	   value是固定写法，不可更改，与#{username}(kegenggai username)不一样，
	   这里的sql利用的底层是statement,上面的sql用的是prepatedstatement-->
    </select>

    <!-- 保存用户信息 -->
    <insert id="save" parameterType="com.itheima.domain.User">
         <!--保存后返回新增用户id-->
        <selectKey keyProperty="id" keyColumn="id" order="AFTER" resultType="int">
            select last_insert_id();
        </selectKey>
        insert into user (username, birthday, sex, address) values(#{username}, #{birthday}, #{sex}, #{address})
    </insert>

    <!-- 更新用户信息 -->
    <update id="update" parameterType="com.itheima.domain.User">
        update user set username=#{username}, birthday=#{birthday}, sex=#{sex}, address=#{address} where id=#{id}
    </update>

    <!-- 删除用户 -->
    <delete id="delete" parameterType="java.lang.Integer">
        delete from user where id=#{id}
    </delete>
    
    <!-- 使用聚合函数查询用户数量 -->
    <select id="findTotal" resultType="int">
        select count(*) from user
    </select>
    
    <!-- 通过queryVo查询用户信息 -->
    <select id="findByVo" resultType="com.itheima.domain.User" parameterType="com.itheima.domain.QueryVo">
        select * from user where username like #{user.username}
    </select>
</mapper>
```

注意：当实体类属性与数据库字段不匹配的时候可通过配置resultMap来让双方进行匹配。    如果配置了resultMap，则已经配置好的sql语句的resultType需要改为resultMap，    值就是配置的resultMap。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper
        PUBLIC  "-//mybatis.org/DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.itheima.dao.IUserDao">
    <!--当实体类属性与数据库字段不匹配的时候可通过配置resultMap来让双方进行匹配。
        如果配置了resultMap，则已经配置好的sql语句的resultType需要改为resultMap，
        值就是配置的resultMap-->
    <resultMap id="userMap" type="com.itheima.domain.User">
        <!--主键配置property是类的属性,column是数据库的字段-->
        <id property="id" column="id"></id>
        <result property="username" column="username"></result>
        <result property="birthday" column="birthday"></result>
        <result property="sex" column="sex"></result>
        <result property="address" column="address"></result>
    </resultMap>
    <!-- 查询所有 -->
    <select id="findAll" resultMap="userMap">
        select * from user
    </select>

    <!-- 通过id查询用户信息 -->
    <select id="findById" resultMap="userMap" parameterType="Integer">
        select * from user where id=#{id}
    </select>

    <!-- 通过queryVo查询用户信息 -->
    <select id="findByVo" resultMap="userMap" parameterType="com.itheima.domain.QueryVo">
        select * from user where username like #{user.username}
    </select>

    <!-- 通过name查询用户信息 -->
    <select id="findByName" resultMap="userMap" parameterType="java.lang.String">
        select * from user where username like #{usernsme}
--          select * from user where username like '${value}' value是固定写法，不可更改，与#{username}(kegenggai username)不一样，z利用的底层是statement,上面用的是prepatedstatement
    </select>

    <!-- 保存用户信息 -->
    <insert id="save" parameterType="com.itheima.domain.User">
        <!--保存后返回新增用户id-->
        <selectKey keyProperty="id" keyColumn="id" order="AFTER" resultType="int">
            select last_insert_id();
        </selectKey>
        insert into user (username, birthday, sex, address) values(#{username}, #{birthday}, #{sex}, #{address})
    </insert>

    <!-- 更新用户信息 -->
    <update id="update" parameterType="com.itheima.domain.User">
        update user set username=#{username}, birthday=#{birthday}, sex=#{sex}, address=#{address} where id=#{id}
    </update>

    <!-- 删除用户 -->
    <delete id="delete" parameterType="java.lang.Integer">
        delete from user where id=#{id}
    </delete>

    <!-- 使用聚合函数查询用户数量 -->
    <select id="findTotal" resultType="int">
        select count(*) from user
    </select>
</mapper>   
```



### 11.3.3.测试

最后是测试类MyBatisTest.java

```java
import com.itheima.dao.IUserDao;
import com.itheima.domain.User;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.junit.After;
import org.junit.Before;
import org.junit.Test;
import java.io.InputStream;
import java.util.Date;
import java.util.List;
public class MybatisTest {
    private InputStream in = null;
    private SqlSession sql = null;
    private IUserDao dao = null;
    @Before
    public void init() throws Exception{
        in = Resources.getResourceAsStream("sqlMapConfig.xml");
        sql = new SqlSessionFactoryBuilder().build(in).openSession();
        dao = sql.getMapper(IUserDao.class);
    }
    @After
    public void destory() throws Exception{
        sql.commit();
        if(sql!=null){
            sql.close();
        }
        if(in!=null){
            in.close();
        }
    }
    @Test//测试查询所有用户信息的方法
    public void testfindAll(){
        List<User> users = dao.findAll();
        for(User user: users){
            System.out.println(user);
        }
    }

    @Test//测试通过id查询用户信息的方法
    public void testfindById(){
        User user = dao.findById(41);
        System.out.println(user);
    }
    @Test//测试通过name查询用户信息的方法
    public void testfindByName(){
        List<User> users = dao.findByName("%王%");
        for(User user: users) {
            System.out.println(user);
        }
    }
     @Test//测试通过queryVo查询用户信息的方法
    public void testfindByVo(){
        QueryVo vo = new QueryVo();
        User u = new User();
        u.setUsername("%王%");
        vo.setUser(u);
        List<User> users = dao.findByVo(vo);
        for(User user: users) {
            System.out.println(user);
        }
    }
   
    @Test//测试保存用户信息的方法
    public void testSave(){
        User user = new User();
        user.setUsername("jack last insertid");
        user.setBirthday(new Date());
        user.setAddress("北京");
        user.setSex("男");
        System.out.println("保存之前"+user);
        dao.save(user);
        System.out.println(user);
    }
    @Test//测试更新用户信息的方法
    public void testUpdate(){
        User user = new User();
        user.setId(53);
        user.setUsername("rose");
        user.setBirthday(new Date());
        user.setAddress("沈阳");
        user.setSex("女");
        dao.update(user);
    }
    @Test//测试删除用户信息的方法
    public void  testDelete(){
        dao.delete(52);
    }   
    @Test//测试用户数量的方法
    public void  testFindTotal(){
        System.out.println(dao.findTotal());
    }
}
```

### 11.3.4.附录：

#### 11.3.4.1.实体类

```java
import java.io.Serializable;
import java.util.Date;
public class User implements Serializable {
    private Integer id;
    private String username;
    private Date birthday;
    private String sex;
    private String address;
   //..get()+..set()
}
```

#### 11.3.4.2.数据库

表user

![1567134584113](E:\typora-document\MyNote\images\1567134584113.png)

#### 11.3.4.3.主配置文件

mybatis的主配置文件主要是配置数据库连接及相关环境，还有与dao层java文件对应的xml文件位置。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration
        PUBLIC  "-//mybatis.org/DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--配置环境-->
    <environments default="mysql">
        <!-- 配置mysql环境 -->
        <environment id="mysql">
            <!-- 配置事务的类型 -->
            <transactionManager type="JDBC"></transactionManager>
            <dataSource type="POOLED">
                <!-- 配置数据库连接基本信息 -->
                <property name="driver" value="com.mysql.jdbc.Driver"></property>
                <property name="url" value="jdbc:mysql://localhost:3306/conn"></property>
                <property name="username" value="root"></property>
                <property name="password" value="root"></property>
            </dataSource>
        </environment>
    </environments>

    <mappers>
        <mapper resource="com/itheima/dao/IUserDao.xml"></mapper>
    </mappers>
</configuration>
```



#### 11.3.4.4.pom.xml

```xml
<dependencies>
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.4.5</version>
    </dependency>
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.11</version>
    </dependency>
    <dependency>
        <groupId>log4j</groupId>
        <artifactId>log4j</artifactId>
        <version>1.2.12</version>
    </dependency>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
    </dependency>
</dependencies>
```



#### 11.3.4.5.实体类

```java
public class QueryVo {
    private User user;
 //..get()+..set()
}
```

####  11.3.4.6.实现dao接口

首先去掉QueryVo这个类，然后写个类实现IUserDao,并重写内部方法 。

UserDaoImpl.java

```java
import com.itheima.dao.IUserDao;
import com.itheima.domain.User;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import java.util.List;
public class UserDaoImpl implements IUserDao {
    private SqlSession session;
    public UserDaoImpl(SqlSession session){
        this.session = session;
    }
    public List<User> findAll() {
        List<User> users = session.selectList("com.itheima.dao.IUserDao.findAll");
        return users;
    }
    public void save(User user) {
        session.insert("com.itheima.dao.IUserDao.save", user);
    }
    public void update(User user) {
        session.update("com.itheima.dao.IUserDao.update", user);
    }
    public void delete(Integer id) {
        session.delete("com.itheima.dao.IUserDao.delete", id);
    }
    public User findById(Integer id) {
        User user = session.selectOne("com.itheima.dao.IUserDao.findById", id);
        return user;
    }
    public List<User> findByName(String username) {
        List<User> users = session.selectList("com.itheima.dao.IUserDao.findByName", username);
        return users;
    }
    public int findTotal() {
        Integer count = session.selectOne("com.itheima.dao.IUserDao.findTotal");
        return count;
    }
}
```



重写的测试类MabitsTest.java

```java
public class MybatisTest {
    private InputStream in = null;
    private SqlSession sql = null;
    private UserDaoImpl dao = null;
    @Before
    public void init() throws Exception{
        in = Resources.getResourceAsStream("sqlMapConfig.xml");
        sql = new SqlSessionFactoryBuilder().build(in).openSession();
        dao = new UserDaoImpl(sql);
    }
    @After
    public void destory() throws Exception{
        sql.commit();
        if(sql!=null){
            sql.close();
        }
        if(in!=null){
            in.close();
        }
    }
    @Test//测试查询所有用户信息的方法
    public void testFindAll(){
        List<User> users = dao.findAll();
        for(User user: users){
            System.out.println(user);
        }
    }

    @Test//测试通过id查询用户信息的方法
    public void testFindById(){
        User user = dao.findById(42);
        System.out.println(user);
    }
    @Test//测试通过name查询用户信息的方法
    public void testFindByName(){
        List<User> users = dao.findByName("%王%");
        for(User user: users) {
            System.out.println(user);
        }
    }
    @Test//测试保存用户信息的方法
    public void testSave(){
        User user = new User();
        user.setUsername("jack2");
        user.setBirthday(new Date());
        user.setAddress("北京");
        user.setSex("男");
        System.out.println("保存之前"+user);
        dao.save(user);
        System.out.println(user);
    }
    @Test//测试更新用户信息的方法
    public void testUpdate(){
        User user = new User();
        user.setId(53);
        user.setUsername("rose");
        user.setBirthday(new Date());
        user.setAddress("沈阳");
        user.setSex("女");
        dao.update(user);
    }
    @Test//测试删除用户信息的方法
    public void  testDelete(){
        dao.delete(53);
    }
    @Test//测试用户数量的方法
    public void  testFindTotal(){
        System.out.println(dao.findTotal());
    }
}

```



查看DefaultSqlSession的源码方法，在sqlsession的类名上右键，选择diagrams,在sqlsession上右键，选择show Implementtations,选择DefaultSqlSession，然后点击DefaultSqlSession，在菜单栏下方会出现DefaultSqlSession的类路径，双击DefaultSqlSession即可进入他的源码。

## 11.4.标签

### 11.4.1.properties标签

以主配置文件为例,在configuration标签内添加了properties标签，内部是未改动的主配置文件中dataSource标签内的property标签内容，此时添加properties标签后，datasouce标签内的property标签内容也换了，value属性换为el表达式${}：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration
        PUBLIC  "-//mybatis.org/DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <properties>
        <property name="driver" value="com.mysql.jdbc.Driver"></property>
        <property name="url" value="jdbc:mysql://localhost:3306/conn"></property>
        <property name="username" value="root"></property>
        <property name="password" value="root"></property>
    </properties>
    <!--配置环境-->
    <environments default="mysql">
        <!-- 配置mysql环境 -->
        <environment id="mysql">
            <!-- 配置事务的类型 -->
            <transactionManager type="JDBC"></transactionManager>
            <dataSource type="POOLED">
                <!-- 配置数据库连接基本信息 -->
                <property name="driver" value="${driver}"></property>
                <property name="url" value="${url}"></property>
                <property name="username" value="${username}"></property>
                <property name="password" value="${password}"></property>
            </dataSource>
        </environment>
    </environments>

    <mappers>
        <mapper resource="com/itheima/dao/IUserDao.xml"></mapper>
    </mappers>
</configuration>
```



此外还可以将properties标签单独做一个preoperties文件，放在resources下面，而主配置文件中只需配置properties的标签并在其内部设置一个属性resource来指定properties文件的位置，名称。

主配置文件：

```xml
<properties resource="jdbc.properties"></properties>
```

properties文件:

```properties
driver=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/conn
username=root
password=root
```



### 11.4.2.typeAliases标签

作用是为类名起别名，例如int或Integer可以只用写一个类名，不需要写全路径名称。但是它只能配置domain中的类名。

主配置文件configuration标签内：

```xml
<typeAliases>
    <!--typeAlias用于配置别名，type属性指定实体类的全限定类名，alias用于指定别名，当这个类指定了别名时，写的是就不再区分大小写-->
    <!--<typeAlias type="com.itheima.domain.User" alias="user"></typeAlias>-->
    <!--用于指定需要起别名的包，当指定之后，该包下所有类都会起别名，别名就是类名,不区分大小写-->
    <package name="com.itheima.domain"></package>
</typeAliases>
<mappers>
    <!--<mapper resource="com/itheima/dao/IUserDao.xml"></mapper>-->
    <!--package标签用于指定dao接口所在包，当指定了这个标签之后就不需要再写mapper或resource，class了。-->
    <package name="com.itheima.dao"></package>
</mappers>
```

IUserDao.xml：

```xml
<!-- 查询所有 resultType内部可以填写user,USER,uSer,UsEr-->
<select id="findAll" resultType="user">
    select * from user
</select>
```



### 11.4.3.if标签

IUserDao.xml

```xml
<!--if标签-->
<select id="findByCondition" resultType="user" parameterType="user">
    select * from user where 1=1
    <if test="username!=null">
        and username = #{username}
    </if>
</select>
```

测试类：

```java
@Test//测试查询所有用户信息的方法
public void testFindByCondition(){
    User u = new User();
    u.setUsername("老王");
    u.setSex("女");
    List<User> users = dao.findByCondition(u);
    for(User user: users){
        System.out.println(user);
    }
}
```



### 11.4.4.where标签

IUserDao.xml:

```xml
<select id="findByCondition" resultType="user" parameterType="user">
    select * from user
    <where>
        <if test="username!=null">
            and username = #{username}
        </if>
        <if test="sex!=null">
            and sex = #{sex}
        </if>
    </where>
</select>
```



测试类部分与11.4.3部分相同

### 11.4.5.foreach标签

IUserDao.xml':

```xml
<select id="findByList" resultType="user" parameterType="com.itheima.domain.QueryVo">
    select * from user
    <where>
        <if test="list!=null and list.size()>0">
            <foreach collection="list" open="and id in (" close=")" separator="," item="ids">
                #{ids}
            </foreach>
        </if>
    </where>
</select>
```

#{ids}中的ids名称来源取决于foreach标签中的item。

测试类:

```java
@Test//测试根据条件查询用户信息的方法
public void testFindByList(){
    QueryVo vo = new QueryVo();
    List<Integer> list = new ArrayList<Integer>();
    list.add(41);
    list.add(42);
    list.add(43);
    vo.setList(list);
    List<User> users = dao.findByList(vo);
    for(User user: users){
        System.out.println(user);
    }
}
```



### 11.4.6.sql标签

IUserDao.xml：

```xml
<!--作用是抽取重复的sql内容-->
<sql id="defaultUser">
    select * from user
</sql>

<select id="findByList" resultType="user" parameterType="com.itheima.domain.QueryVo">
    <include refid="defaultUser"></include>
    <where>
        <if test="list!=null and list.size()>0">
            <foreach collection="list" open="and id in (" close=")" separator="," item="ids">
                #{ids}
            </foreach>
        </if>
    </where>
</select>
```

测试类与11.4.5部分相同

## 11.5.连接池

连接池作用是减少获取连接所消耗的时间，mybatis中给提供了三种方式的配置，配置的位置是 sqlMapCofig.xml中的dataSource标签，type属性是表示采用何种连接池方式。type属性取值有三种：

1.POOLED：采用传统的javax.sql.DataSource规范中的连接池，mybatis中有针对规范的实现。

2.UNPOOLED:采用传统的获取连接方式，虽然也实现了规范中的连接池接口，但是未使用。

3.JNDI:采用服务器提供的JNDI技术实现，来获取DataSource对象。不同服务器不同实现方式。需要注意它只能是		    在web工程或maven中的war工程中使用，tomcat的实现方式是dbcp连接池。

## 11.6.多表查询

表与表之间的关系有四种：一对一、一对多、多对一、多对多

### 11.6.1.一对多

多表查询之一对多示例：用户与账户

关系：一个用户可能有多个账户，一个账户属于一个用户，多个账户可属于一个用户

测试步骤： 

1.建表，用户表和账户表，让用户表与账户表之间具有一对多的关系，需要使用外键在账户表中添加。

2.建实体类，用户类和账户类，让用户类与账户表之间具有一对多的关系。

3.建立两个配置文件：用户的配置文件和账户的配置文件

4.实现配置：查询用户时可以同时包含用户名下的账户信息，查询账户时可以得到所属用户的信息

#### 11.6.1.1.数据库

用户表user：

![1567479105106](E:\typora-document\MyNote\images\1567479105106.png)

账户表account：

![1567479167397](E:\typora-document\MyNote\images\1567479167397.png)

账户表外键关系：

![1567578952033](E:\typora-document\MyNote\images\1567578952033.png)

用户表与账户表通过账户表的外键进行关联。

#### 11.6.1.2.实体类

用户类：通过accounts存储与当前用户对象有关联的账户，使用户类与账户类有关联

```java
import java.io.Serializable;
import java.util.Date;
import java.util.List;
public class User implements Serializable {
    private Integer id;
    private String username;
    private Date birthday;
    private String sex;
    private String address;
    private List<Account> accounts;
    //..get()+..set()
    //toString()-->不包含accounts
```

账户类：通过users存储当前账户对象所属的用户，使用户类与账户类有关联

```java
import java.io.Serializable;
public class Account implements Serializable {
    private Integer id;
    private Integer uid;
    private double money;
    private User user;
    //..get()+..set()
    //toString()-->不包含user
}
```

#### 11.6.1.3.配置文件

用户配置文件：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper
        PUBLIC  "-//mybatis.org/DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.itheima.dao.IUserDao">

    <resultMap id="userMap" type="user">
        <id property="id" column="id"></id>
        <result column="username" property="username"></result>
        <result property="address" column="address"></result>
        <result column="sex" property="sex"></result>
        <result property="birthday" column="birthday"></result>
        <collection property="accounts" ofType="account">
            <id column="aid" property="id"></id>
            <result property="uid" column="uid"></result>
            <result column="money" property="money"></result>
        </collection>
    </resultMap>
    <!-- 查询所有 -->
    <select id="findAll" resultMap="userMap">
        select u.*,a.id as aid,a.uid,a.money from user u left OUTER join account a on a.uid = u.id
    </select>

    <!-- 通过id查询用户信息 -->
    <select id="findById" resultType="com.itheima.domain.User" parameterType="Integer">
        select * from user where id=#{id}
    </select>
</mapper>
```



账户配置文件：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper
        PUBLIC  "-//mybatis.org/DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.itheima.dao.IAccountDao">
    <resultMap id="accountMap" type="account">
        <id property="id" column="aid"></id>
        <result column="uid" property="uid"></result>
        <result property="money" column="money"></result>
        <association property="user" column="uid" javaType="user">
            <id column="id" property="id"></id>
            <result property="username" column="username"></result>
            <result column="address" property="address"></result>
            <result property="sex" column="sex"></result>
            <result column="birthday" property="birthday"></result>
        </association>
    </resultMap>

    <!-- 查询所有 -->
    <select id="findAll" resultMap="accountMap">
       select u.*,a.id as aid,a.uid,a.money from user u,account a where u.id=a.uid;
    </select>
    <select id="findAccountUser" resultType="accountUser">
        select a.*,u.username as username,u.address as address,a.money as money from user u,account a where u.id=a.uid
    </select>
</mapper>
```



### 11.6.2.多对多

多表查询之多对多示例：用户与角色

关系：一个用户可能有多个角色，一个角色有多个用户

测试步骤： 

1.建表，用户表和角色表，让用户表与角色表之间具有多对多关系，因此需要有一个中间表，中间表包含两个表的主键，这两个主键在中间表里是外键

2.建实体类，用户类和角色类，让用户类与角色类都体现多对多的关系，彼此有一个包含对方引用的集合。

3.建立两个配置文件：用户的配置文件和账户的配置文件

4.实现配置：查询用户时可以同时包含用户名下的角色信息，查询角色时可以得到角色所赋予的用户相关信息

#### 11.6.2.1.数据库

用户表即11.6.1中的用户表

角色表role：

![1567578536068](E:\typora-document\MyNote\images\1567578536068.png)

中间表user_role：

![1567578595383](E:\typora-document\MyNote\images\1567578595383.png)

中间表的外键关系：中间表包含两个表的主键，这两个主键在中间表里是外键

![1567578696494](E:\typora-document\MyNote\images\1567578696494.png)



#### 11.6.2.2.实体类：

用户类:通过accounts存储与当前用户对象有关联的账户，使用户类与账户类有关

```java
import java.io.Serializable;
import java.util.Date;
import java.util.List;
public class User implements Serializable {
    private Integer id;
    private String username;
    private Date birthday;
    private String sex;
    private String address;
    private List<Role> roles;
    //..get()+..set()
    //toString()-->不包含roles
}
```



角色类：

```java
import java.io.Serializable;
import java.util.List;
public class Role implements Serializable {
    private Integer id;
    private String roleName;
    private String roleDesc;
    private List<User> users;
    //..get()+..set()
    //toString()-->不包含users
}
```

#### 11.6.2.3.配置文件

IUserDao.xml:

```xml
<mapper namespace="com.itheima.dao.IUserDao">

    <resultMap id="userMap" type="user">
        <id property="id" column="id"></id>
        <result column="username" property="username"></result>
        <result property="address" column="address"></result>
        <result column="sex" property="sex"></result>
        <result property="birthday" column="birthday"></result>
        <collection property="roles" ofType="role">
            <id column="rid" property="id"></id>
            <result property="roleName" column="role_name"></result>
            <result column="role_desc" property="roleDesc"></result>
        </collection>
    </resultMap>
    <!-- 查询所有用户 -->
    <select id="findAll" resultMap="userMap">
        select u.*,r.id as rid,r.role_name,r.role_desc from user u
            left join user_role ur on u.id=ur.uid
            left join role r on r.id=ur.rid
    </select>
</mapper>
```



IRoleDao.xml:

```xml
<mapper namespace="com.itheima.dao.IRoleDao">

    <resultMap id="roleMap" type="role">
        <id property="id" column="rid"></id>
        <result column="role_name" property="roleName"></result>
        <result property="roleDesc" column="role_desc"></result>
        <collection property="users" ofType="user">
            <id property="id" column="id"></id>
            <result column="username" property="username"></result>
            <result property="address" column="address"></result>
            <result column="sex" property="sex"></result>
            <result property="birthday" column="birthday"></result>
        </collection>
    </resultMap>
    <!-- 查询所有角色 -->
    <select id="findAll" resultMap="roleMap">
        select r.id as rid,r.role_name,r.role_desc,u.* from role r
	      left join user_role ur on r.id=ur.rid
	      left join user u on u.id=ur.uid
    </select>
</mapper>
```



#### 11.6.2.4.测试类

用户测试类：

```java
import com.itheima.dao.IUserDao;
import com.itheima.domain.User;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.junit.After;
import org.junit.Before;
import org.junit.Test;
import java.io.InputStream;
import java.util.Date;
import java.util.List;
public class UserTest {
    private InputStream in = null;
    private SqlSession sql = null;
    private IUserDao dao = null;
    @Before
    public void init() throws Exception{
        in = Resources.getResourceAsStream("sqlMapConfig.xml");
        sql = new SqlSessionFactoryBuilder().build(in).openSession();
        dao = sql.getMapper(IUserDao.class);
    }
    @After
    public void destory() throws Exception{
        sql.commit();
        if(sql!=null){
            sql.close();
        }
        if(in!=null){
            in.close();
        }
    }
    @Test//测试查询所有用户信息的方法
    public void testfindAll(){
        List<User> users = dao.findAll();
        for(User user: users){
            System.out.println("-------------");
            System.out.println(user);
            System.out.println(user.getRoles());
        }
    }
}
```



角色测试类：

```java
@Test//测试查询所有角色信息的方法
public void testfindAll(){
    List<Role> roles = dao.findAll();
    for(Role role: roles){
        System.out.println("-------------");
        System.out.println(role);
        System.out.println(role.getUsers());
    }
}
```



## 11.7.延迟加载

延迟加载定义：在需要使用数据时才会发起查询，不用时不查询，即按需查询（懒加载）。

立即加载定义：不管用不用，只要调用方法就会发起查询。

四种表关系：一对一，多对一，一对多，多对多

一对一，多对一通常采用立即加载，多对一和多对多通常采用延迟加载

### 11.7.1.一对一

以11.6.1为例进行修改

IAccountDao.xml:以下涉及的部分

```xml
<resultMap id="accountMap" type="account">
    <id property="id" column="id"></id>
    <result column="uid" property="uid"></result>
    <result property="money" column="money"></result>
    <association property="user" column="uid" javaType="user" select="com.itheima.dao.IUserDao.findById"></association>
</resultMap>

<!-- 查询所有角色 -->
<select id="findAll" resultMap="accountMap">
    select * from account
</select>
```



mybatis默认延迟加载是不生效的，需要在sqlMapConfig.xml文件进行配置，如下：

```xml
<configuration>
    <settings>
        <setting name="lazyLoadingEnabled" value="true"/><!--这个是必须的-->
        <setting name="aggressiveLazyLoading" value="true"/><!--这个不是必须的因为版本问题-->
    </settings>
```

其他相关配置如数据库表，实体类，测试类，dao层接口都保持原样。

### 11.7.2.一对多

以11.6.1为例进行修改

IUserDao.xml:以下涉及的部分

```xml
<resultMap id="userMap" type="user">
    <id property="id" column="id"></id>
    <result column="username" property="username"></result>
    <result property="address" column="address"></result>
    <result column="sex" property="sex"></result>
    <result property="birthday" column="birthday"></result>
    <collection property="accounts" ofType="account" select="com.itheima.dao.IAccountDao.findByUid" column="id"></collection>
</resultMap>
<!-- 查询所有 -->
<select id="findAll" resultMap="userMap">
    select * from user
</select>
```

## 11.8.缓存

缓存定义：存在于内存中的临时数据

使用缓存的原因：减少与数据库的交互次数，提高执行效率

适合使用缓存的数据的特征：

​		a.经常查询且修改频率小；

​		b.数据正确与否对最终结果影响不大；（如商品库存，车票）

不适合使用缓存的数据的特征：

​		a.数据改动频率高；

​		b.数据正确与否对最终结果影响很大；（如银行汇率，股市牌价）

### 11.8.1.一级缓存

 		一级缓存就是指mybatis中sqlsession中对象的缓存。当我们执行查询后，查询结果同时会存入sqlsession提供的一个区域。这个区域是一个map的结构。当需要再次去执行同样的查询时，mybatis会先到sqlsession中查询是否有数据，如果有就会从sqlsession中取。当sqlsession消失，则一级缓存消失。

测试案例：

```java
User user1 = dao.findById(41);
//    sql.close();
//    sql = factory.openSession();
//    dao = sql.getMapper(IUserDao.class);//关闭sqlsession再重新打开
sql.clearCache();//清除sqlsession中的缓存
User user2 = dao.findById(41);
System.out.println(user1==user2);
```



使一级缓存消失的方法有两种，一种是关闭sqlsession再重新打开，另一种就是清除sqlsession中的缓存。

### 11.8.2.二级缓存

​		二级缓存就是mybatis中sqlsessionfactory的缓存，由同一个sqlsessionfactory创建的sqlsession会共享其缓存。

二级缓存使用步骤：

​	1.让mybatis支持二级缓存（在SqlSessionConfig.xml文件中配置）;

配置cacheEnabled：

```xml
<configuration> 	 
    <settings>
        <setting name="cacheEnabled" value="true"></setting>
    </settings>
```



​	2.让当前映射文件支持二级缓存（在IUserDao.xml中配置）；

配置cache：

```xml
<mapper namespace="com.itheima.dao.IUserDao">
    <cache/>
```



​	3.让当前的操作支持二级缓存（在select标签内配置）

配置useCache：

```xml
 <!-- 通过id查询用户信息 -->
<select id="findById" resultType="user" parameterType="Integer" useCache="true">
    select * from user where id=#{id}
</select>
```



测试方法：

```java
@Test
public void testTheFirstCache(){
    SqlSession sql1 = factory.openSession();
    IUserDao dao1 = sql1.getMapper(IUserDao.class);
    User user1 = dao1.findById(41);
    sql1.close();
    SqlSession sql2 = factory.openSession();
    IUserDao dao2 = sql2.getMapper(IUserDao.class);
    User user2 = dao2.findById(41);
    System.out.println(user1==user2);
}
```



## 11.9.注解开发

### 11.9.1.增删改查

1.主配置文件sqlMapConfig.xml：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration
        PUBLIC  "-//mybatis.org/DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <typeAliases>
        <package name="com.itheima.domain"></package>
    </typeAliases>
    <!--配置环境-->
    <environments default="mysql">
        <!-- 配置mysql环境 -->
        <environment id="mysql">
            <!-- 配置事务的类型 -->
            <transactionManager type="JDBC"></transactionManager>
            <dataSource type="POOLED">
                <!-- 配置数据库连接基本信息 -->
                <property name="driver" value="com.mysql.jdbc.Driver"></property>
                <property name="url" value="jdbc:mysql://localhost:3306/conn"></property>
                <property name="username" value="root"></property>
                <property name="password" value="root"></property>
            </dataSource>
        </environment>
    </environments>

    <mappers>
        <package name="com.itheima.dao"></package>
    </mappers>
</configuration>
```



2.实体类User.java:

```java
import java.io.Serializable;
import java.util.Date;
import java.util.List;

public class User implements Serializable {
    private Integer id;
    private String username;
    private Date birthday;
    private String sex;
    private String address;
    //..get()+..set()+toString()
} 
```

3.接口IUserDao.java：

```java
import com.itheima.domain.User;
import org.apache.ibatis.annotations.Select;

import java.util.List;

public interface IUserDao {
    /**
     * 查询所有用户
     * @Select @Insert @Update @Delete
     */
    @Select("select * from user")
    List<User> findAll();
    @Select("select * from user where id=#{id}")
    User findById(Integer id);
    @Select("select * from user where username like #{username}")
    List<User> findByName(String username);
    @Select("select count(*) from user")
    Integer findCount();
    @Delete("delete  from user where id=#{id}")
    void delete(Integer id);
    @Insert("insert into user (username,address,sex,birthday) values(#{username},#{address},#{sex},#{birthday})")
    void save(User user);
    @Update("update user set username=#{username},address=#{address},sex=#{sex},birthday=#{birthday} where id=#{id}")
    void update(User user);

}
```



当实体类属性与数据库字段不一致时（如id和userid），可使用Results注解解决这个问题。

```java
  @Select("select * from user")
    @Results(id="userMap",value={
            @Result(id=true,column = "id",property = "id"),
            @Result(column = "username",property = "userName"),
            @Result(id=true,column = "sex",property = "sex"),
            @Result(id=true,column = "address",property = "address"),
            @Result(id=true,column = "birthday",property = "birthday"),
    })
    List<User> findAll();
    @Select("select * from user where id=#{id}")
    @ResultMap(value={"userMap"})
    User findById(Integer id);
```





4.测试类：

```java
import com.itheima.dao.IUserDao;
import com.itheima.domain.User;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.junit.After;
import org.junit.Before;
import org.junit.Test;
import java.io.InputStream;
import java.util.Date;
import java.util.List;

public class UserTest {

    public static void main(String[] args) throws Exception{
        InputStream in = Resources.getResourceAsStream("sqlMapConfig.xml");
        SqlSessionFactory factory =  new SqlSessionFactoryBuilder().build(in);
        SqlSession sql = factory.openSession();
        IUserDao dao = sql.getMapper(IUserDao.class);
 //        List<User> users = dao.findAll();
//        for (User user: users) {
//            System.out.println(user);
//        }
//        User user = new User();
//        user.setUsername("tom3");
//        user.setAddress("天通苑");
//        user.setSex("男");
//        user.setBirthday(new Date());
//        dao.save(user);
//        User user = dao.findById(58);
//        System.out.println(user);
//        user.setUsername("tom31");
//        user.setAddress("天通苑");
//        user.setSex("男");
//        user.setBirthday(new Date());
//        dao.update(user);
//        System.out.println(dao.findById(58));
//        dao.delete(58);
//        List<User>  users = dao.findByName("%王%");
//        for (User user: users) {
//            System.out.println(user);
//        }
        System.out.println(dao.findCount());
        sql.commit();
        sql.close();
        in.close();     
    }
}
```



### 11.9.2.一对一

IAccountDao.java:

```java
import com.itheima.domain.Account;
import org.apache.ibatis.annotations.One;
import org.apache.ibatis.annotations.Result;
import org.apache.ibatis.annotations.Results;
import org.apache.ibatis.annotations.Select;
import org.apache.ibatis.mapping.FetchType;

import java.util.List;

public interface IAccountDao {

    /**
     * 查询所有帐户
     *
     */
    @Select("select * from account")
    @Results(id="accountMap",value={
            @Result(id=true,column="id",property = "id"),
            @Result(column="uid",property = "uid"),
            @Result(column="money",property = "money"),
            @Result(property = "user",column = "uid", one = @One(select = "com.itheima.dao.IUserDao.findById",fetchType = FetchType.EAGER))
    })
    List<Account> findAll();

    @Select("select * from account where uid=#{uid}")
    Account findByUid(Integer uid);
}
```



### 11.9.3.多对多

IUserDao.java:

```java
import com.itheima.domain.User;
import org.apache.ibatis.annotations.*;
import org.apache.ibatis.mapping.FetchType;

import java.util.List;

public interface IUserDao {
    /**
     * 查询所有用户
     *
     */
    @Select("select * from user")
    @Results(id="userMap",value={
            @Result(id=true,column="id",property = "id"),
            @Result(column="username",property = "username"),
            @Result(column="address",property = "address"),
            @Result(column="sex",property = "sex"),
            @Result(column="birthday",property = "birthday"),
            @Result(property = "accounts",column = "id", many = @Many(select = "com.itheima.dao.IAccountDao.findByUid",fetchType = FetchType.LAZY))
    })
    List<User> findAll();

    /**
     * 通过id查询用户信息
     * @param id 用户id
     * @return 用户信息
     */
    @Select("select * from user where id = #{id}")
    User findById(Integer id);
}
```



### 11.9.4.缓存

一级缓存默认开启，二级缓存需要两个步骤，首先是在sqlMapConfig.xml文件汇总的settings的setting标签中配置cacheEnabled，值为true，这个值默认也是true

```xml
<configuration>
    <settings>
       <setting name="cacheEnabled" value="true"></setting>
    </settings>
```



然后是在需要使用的dao层接口进行注解：

```java
@CacheNamespace(blocking = true)
public interface IUserDao {
```










































































[typora使用教程]: https://www.jianshu.com/p/a6a6a22e9393

