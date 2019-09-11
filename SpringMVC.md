# 12.SpringMVC

## 12.1.入门案例

### 12.1.1.index.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <h3>入门程序
    </h3>
    <a href="hello">入门程序</a>
</body>
</html>
```



### 12.1.2.web.xml

```xml
<!DOCTYPE web-app PUBLIC
 "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
 "http://java.sun.com/dtd/web-app_2_3.dtd" >

<web-app>
  <display-name>Archetype Created Web Application</display-name>

  <servlet>
    <servlet-name>dispatcherServlet</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>classpath:springmvc.xml</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
  </servlet>

  <servlet-mapping>
    <servlet-name>dispatcherServlet</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>
</web-app>
```



### 12.1.3.HelloController.java

```java
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
@Controller
public class HelloController {
    @RequestMapping(path="/hello")
    public String sayHello(){
        System.out.println("Hello SpringMVC!!!");
        return "success";
    }
}
```



### 12.1.4.springmvc.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans
        xmlns="http://www.springframework.org/schema/beans"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns:context="http://www.springframework.org/schema/context"
        xmlns:mvc="http://www.springframework.org/schema/mvc"
        xsi:schemaLocation="http://www.springframework.org/schema/beans
            http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
            http://www.springframework.org/schema/context
            http://www.springframework.org/schema/context/spring-context-3.0.xsd
            http://www.springframework.org/schema/mvc
            http://www.springframework.org/schema/mvc/spring-mvc-3.0.xsd">


    <!-- 自动扫描的包名 -->
    <context:component-scan base-package="com.itheima.controller"></context:component-scan>

    <!-- 默认的注解映射的支持 -->
    <mvc:annotation-driven />
    <!-- 视图解释类 -->
    <bean id="internalResourceViewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/pages/"/><!--需要扫描的页面所在包-->
        <property name="suffix" value=".jsp"/><!--可为空,方便实现自已的依据扩展名来选择视图解释类的逻辑  -->
    </bean>
</beans>
```



### 12.1.5.success.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <h3>跳转成功
    </h3>
</body>
</html>
```



开启服务器，首先加载web.xml,然后回根据servlet标签加载其中的前端控制器DispatcherServlet，同时根据init-param标签会将springmvc.xml进行初始化，根据load-on-startup标签会将配置文件只加载一次。而springmvc.xml会根据context:component-scan这个标签去扫描com.itheima.controller下的所有拥有@Controller标签的的类，并将这些类加入ioc容器。当浏览器访问index,.jsp时，点击链接，前端控制器DispatcherServlet会找到注解@RequestMapping且path="/hello"的方法，这个方法会处理来自页面的请求，并最终返回一个结果，然后前端控制器DispatcherServlet会找到视图解析器internalResourceViewResolver解析结果，将结果success根据内部标签内容/WEB-INF/pages/找到这个路径下，名字是success，结尾是.jsp的页面。

## 12.2.注解

### 12.2.1.RequestMapping

1.这个注解可以用在方法和类上；

2.属性path和value表示的属性含义一致,使用方式是path="/hello"或value="hello"；

3.method属性用于决定访问方式，如post或get，使用方式是method={RequestMethod.POST}；

4.param属性是决定请求时需要携带哪些参数,使用方式是param={"username"},此时超链接的href属性的值是/hello?username=11；

5.headers属性是用于限定消息头的条件，使用方式是headers={"Accept"},此时请求消息头中必须包含Accept这个消息头;

java:

```java
@RequestMapping("/param")
public class ParamController {

    @RequestMapping(path="/testParam")
    public String testParam(String username,Integer password){
        System.out.println("testParam");
        System.out.println("username:"+username);
        System.out.println("password:"+password);
        return "success";
    }
}
```



jsp:

```jsp
<a href="param/testParam?username=123&&password=12">请求参数绑定</a>
```



### 12.2.2.RequestParam

当jsp请求参数与请求方法中的参数中参数不一致时，可通过这个注解解决。

java:

```java
 @RequestMapping(path="/testRequestParam")
public String testRequestParam(@RequestParam(name="uname") String name){
    System.out.println("testRequestParam");
    System.out.println(name);
    return "success";
}
```



jsp:

```jsp
<a href="param/testRequestParam?uname=11">testRequestParam</a>
```



### 12.2.3.RequestBody

将请求参数封装到一个字符串中。

```jsp
<form action="param/testRequestBody" method="post">
    名字:<input type="text" name="name"/><br/>
    生日:<input type="text" name="age"/><br/>
    <input type="submit" value="提交"/><br/>
</form>
```



```java
@RequestMapping(path="/testRequestBody")
public String testRequestBody(@RequestBody String body){
    System.out.println("testRequestBody");
    System.out.println(body);
    return "success";
}//控制台输出name=11$age=11
```



### 12.2.4.PathVariable

当多个方法请求路径相同时，可通过其请求方式进行区别，例如一个路径是/user，请求方式是post，另一个是请求路径是/user，请求方式是get；如果请求方式也相同则可以通过路径后参数进行区分，如一个路径都是/user,请求方式是get，但其中一个路径是/user/10，请求方式是get。该注解就是获取请求路径后参数。

jsp:

```jsp
<a href="param/testPathVariable/10">testPathVariable</a>
```



java:

```java
@RequestMapping(path="/testPathVariable/{id}")
public String testPathVariable(@PathVariable(name="id") String body){
    System.out.println("testPathVariable");
    System.out.println(body);
    return "success";
}//控制台输出10
```



### 12.2.5.RequestHeder

获取请求头信息

jsp:

```jsp
<a href="param/testRequestHeder">testRequestHeder</a>
```



java:

```java
@RequestMapping(path="/testRequestHeder")
public String testRequestHeder(@RequestHeader(name="Accept") String body){
    System.out.println("testRequestHeder");
    System.out.println(body);
    return "success";
}
//控制台输出
//text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,a//pplication/signed-exchange;v=b3
```



### 12.2.6.CookieValue

获取浏览器中cookie的数据

JSP:

```jsp
<a href="param/testCookieValue">testCookieValue</a>
```



Java：

```java
@RequestMapping(path="/testCookieValue")
public String testCookieValue(@CookieValue(name="JSESSIONID") String cookie){
    System.out.println("testCookieValue");
    System.out.println(cookie);
    return "success";
}
//控制台输出3FFC8F5D339CF3BCE28F912CC0BE4501
```



### 12.2.7.ModelAttribute

该注解可以放在方法或方法参数上。放在方法上则可以在控制器执行请求方法前执行该方法，可以使实体类中未经过封装的属性保持数据库的数据不会变为空，方法需要返回值。放在参数上则可以没有返回值，但是需要将实体类封装在一个map中，在请求方法时需要在参数列表中定义一个map，里面有上一个方法中map中的数据。

jsp:

```jsp
<form action="param/testModelAttribute" method="post">
    名字:<input type="text" name="name"/><br/>
    <input type="submit" value="提交"/><br/>
</form>
```



java:放在方法上

```java
@RequestMapping(path="/testModelAttribute")
public String testModelAttribute(User user){
    System.out.println("testModelAttribute");
    System.out.println(user);
    return "success";
}
@ModelAttribute
public User showUser(String name){
    System.out.println("showUser");
    User user = new User();
    user.setName(name);
    user.setBirth(new Date());
    return user;
}
```



放在参数上：

```java
@RequestMapping(path="/testModelAttribute")
public String testModelAttribute(@ModelAttribute("abc") User user){
    System.out.println("testModelAttribute");
    System.out.println(user);
    return "success";
}
@ModelAttribute
public void showUser(String name, Map<String,User> map){
    System.out.println("showUser");
    User user = new User();
    user.setName(name);
    user.setBirth(new Date());
    map.put("abc", user);
}
```



### 12.2.8.SessionAttributes

将request域中的数据放入session域。

jsp:

```jsp
<a href="param/testSessionAttribute">SessionAttribute</a><br/>
<a href="param/getSessionAttribute">getSessionAttribute</a><br/>
<a href="param/deleteSessionAttribute">deleteSessionAttribute</a><br/>
```



java:

```java
@Controller
@RequestMapping("/param")
@SessionAttributes(value = {"message"}) //将request域中message存入session域
public class ParamController {
   @RequestMapping(path="/testSessionAttribute")
    public String testSessionAttribute(Model model){
        System.out.println("testSessionAttribute");
        model.addAttribute("message", "first");//将message存入request域
        return "success";
    }
    @RequestMapping(path="/getSessionAttribute")
    public String getSessionAttribute(ModelMap modelMap){
        System.out.println("getSessionAttribute");
        System.out.println(modelMap.get("message"));
        return "success";
    }
    @RequestMapping(path="/deleteSessionAttribute")
    public String deleteSessionAttribute(SessionStatus status){
        System.out.println("deleteSessionAttribute");
        status.setComplete();
        return "success";
    }
}
```



## 12.3.请求参数绑定

请求参数绑定就是指jsp页面请求时携带参数，可以通过超链接，表单等方式绑定，携带的参数类型有基本数据类型，集合数据类型，javabean的数据类型。jsp请求参数需要java方法中的参数名称一致。

### 12.3.1.超链接，基本数据类型

jsp：

```jsp
<a href="param/testParam?username=123&&password=12">请求参数绑定</a>
```



java:

请求方法：

```java
@RequestMapping(path="/testParam")
public String testParam(String username,Integer password){
    System.out.println("testParam");
    System.out.println("username:"+username);
    System.out.println("password:"+password);
    return "success";
}
```



### 12.3.2.表单，javabean类型

jsp:

```jsp
<form action="param/saveAccount" method="post">
    用户名:<input type="text" name="username"/><br/>
    密码:<input type="text" name="password"/><br/>
    金额:<input type="text" name="money"/><br/>
    <input type="submit" value="提交"/><br/>
</form>
```



java:

javabean:

```java
import java.io.Serializable;
public class Account implements Serializable {
    private String username;
    private String password;
    private double money;
```



请求方法：

```java
@RequestMapping(path="/saveAccount")
public String saveAccount(Account account){
    System.out.println("saveAccount");
    System.out.println(account);
    return "success";
}
```



### 12.3.3.表单，javabean类型2

javabean内含有javabean（account中含有user）：

jsp:

```jsp
<form action="param/saveAccount" method="post">
    用户名:<input type="text" name="username"/><br/>
    密码:<input type="text" name="password"/><br/>
    金额:<input type="text" name="money"/><br/>
    名字:<input type="text" name="user.name"/><br/>
    生日:<input type="text" name="user.birth"/><br/>
    <input type="submit" value="提交"/><br/>
</form>
```



javabean:

Account.java:

```java
import java.io.Serializable;
public class Account implements Serializable {
    private String username;
    private String password;
    private double money;
    private User user;
```



User.java:

```java
import java.io.Serializable;
public class User implements Serializable {
    private String name;
    private String birth;
```



在web.xml中配置过滤器,表单需要时post请求：

```xml
<filter>
    <filter-name>characterEncodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
        <param-name>encoding</param-name>
        <param-value>UTF-8</param-value>
    </init-param>
</filter>

<filter-mapping>
    <filter-name>characterEncodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```



### 12.3.4.表单，集合类型

jsp:

```jsp
 <form action="param/saveAccount" method="post">
     用户名:<input type="text" name="username"/><br/>
     密码:<input type="text" name="password"/><br/>
     金额:<input type="text" name="money"/><br/>
     名字:<input type="text" name="list[0].name"/><br/>
     生日:<input type="text" name="list[0].birth"/><br/>
     名字:<input type="text" name="map['one'].name"/><br/>
     生日:<input type="text" name="map['one'].birth"/><br/>
     <input type="submit" value="提交"/><br/>
</form>
```

java:

Account.java:

```java
import java.io.Serializable;
import java.util.List;
import java.util.Map;
public class Account implements Serializable {
    private String username;
    private String password;
    private double money;
    private List<User> list;
    private Map<String,User> map;
```



User.java:

```java
import java.io.Serializable;
public class User implements Serializable {
    private String name;
    private String birth;
```



## 12.4.自定义类型转换器

​		假设将String类型转换为日期类型

​		首先定义一个类，并继承Converter<String, Date>，Converter<String, Date>里面的泛型String是转换来源的类型，Date是转换目标。继承之后在重写的方法内进行数据的处理。参数s是转换数据来源，方法返回值是转换目标。

```java
import org.springframework.core.convert.converter.Converter;
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.Date;
public class DateConverter implements Converter<String, Date> {
    @Override
    public Date convert(String s) {
        if(s==null){
            throw new RuntimeException("请输入数据！！！");
        }
        DateFormat format = new SimpleDateFormat("yyyy-MM-dd");
        try {
            return format.parse(s);
        }catch(Exception e){
            throw new RuntimeException("数据类型转换异常！！");
        }
    }
}
```



然后在springmvc中声明这个转换器,声明方式是先写一个ConversionServiceFactoryBean的bean，然后在内部写property的标签内容。

```xml
 <bean id="conversionServiceFactoryBean" class="org.springframework.context.support.ConversionServiceFactoryBean">
     <property name="converters">
         <set>
             <bean class="com.itheima.utils.DateConverter"/>
         </set>
     </property>
</bean>
```



声明类型转换器后，还需要启用这个转换器，是在mvc:annotation-driven标签内使用conversion-service属性进行启用的。

```xml
<mvc:annotation-driven conversion-service="conversionServiceFactoryBean"/>
```

