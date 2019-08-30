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






































































































































[typora使用教程]: https://www.jianshu.com/p/a6a6a22e9393

