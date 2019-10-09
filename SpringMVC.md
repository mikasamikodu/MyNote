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

### 12.3.1.基本数据类型超链接

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



### 12.3.2.javabean类型表单

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



### 12.3.3.javabean类型表单2

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



## 12.5.返回值

jsp:

```jsp
<a href="user/testString">testString</a><br/>
<a href="user/testVoid">testVoid</a><br/>
<a href="user/testForward">testForward</a><br/>
<a href="user/testModelAndView">testModelAndView</a><br/>
```



java:

```java
@Controller
@RequestMapping("/user")
public class UserController {

    @RequestMapping("/testString")//返回值是String类型
    public String testString(Model model){
        System.out.println("testString");
        User user = new User();
        user.setName("张三");
        user.setPassword("12312");
        user.setAge(12);
        model.addAttribute("user", user);
        return "success";
    }
    @RequestMapping("/testModelAndView")//返回值是ModelAndView类型
    public ModelAndView testModelView(){
        System.out.println("testModelAndView");
        ModelAndView view = new ModelAndView();
        User user = new User();
        user.setName("张三");
        user.setPassword("12312");
        user.setAge(12);
        view.addObject("user", user);
        view.setViewName("success");
        return view;
    }
    @RequestMapping("/testVoid")//返回值是void类型
    public void testVoid(HttpServletRequest request, HttpServletResponse response) 
        throws Exception{
        System.out.println("testvoid");
        //request.getRequestDispatcher("/WEB-INF/pages/success.jsp")
        //		 .forward(request, response);//转发返回页面
        //response.sendRedirect(request.getContextPath()+"/index.jsp");
        //response.setCharacterEncoding("UTF-8");//重定向到页面
        response.setContentType("text/html;charset=UTF-8");
        response.getWriter().print("<h3>张三</h3>");//直接系那个页面输出内容
        return;
    }
    @RequestMapping("/testForward")//根据关键字返回页面
    public String testForward() throws Exception{
        System.out.println("testFarword");
        return "redirect:/index.jsp";
//      return "forward:/WEB-INF/pages/success.jsp";
    }
}
```

## 12.6.Json

jsp:

```jsp
	<script src="js/jquery.js"></script>//引入jquery文件
    <script>
        $(function(){
            $("#btn").click(function(){
                $.ajax({//发送ajax请求
                    url: "user/testAjax",
                    contentType: "application/json;charset=UTF-8",
                    data: '{"name":"tom","password":"1234","age":23}',
                    dataType: "json",
                    type: "post",
                    success: function(data){//处理返回数据
                        alert(data.toString());
                        alert(data.name);
                        alert(data.age);
                        alert(data.password);
                    }
                });
            });
           }
        )
    </script>
</head>
<body>
    <button id="btn">发送</button>
</body>
```



由于前端控制器会拦截所有访问请求，所以也会拦截对jquery文件的访问，阻止前端控制器对静态资源访问的拦截方法就是在springmvc.xml中配置mvc:resourses这个标签。jquery文件所在文件爱你家要放在wepapp文件夹下面：

```xml
 <!--设置前端控制器不拦截静态资源并指定哪些不拦截-->
<mvc:resources location="/js/" mapping="/js/**"/>
```



java:

```java
@RequestMapping("/testAjax")
public @ResponseBody User testAjax(@RequestBody User user){
    System.out.println("testAjax");
    user.setName("jack");
    user.setAge(10);
    return user;
}//@RequestBody将json数据封装到user中，@ResponseBody将user转换为json
```



要想将json数据封装进实体类中或将实体类转换为json，需要在pom.xml引入依赖：

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.9.1</version>
</dependency>
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-core</artifactId>
    <version>2.9.1</version>
</dependency>
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-annotations</artifactId>
    <version>2.9.1</version>
</dependency>
```



## 12.7.上传文件

###  12.7.1.传统意义的

jsp:

```jsp
 <h3>传统文件上传</h3>
<form action="file/upload" method="post" enctype="multipart/form-data">
    文件上传:<input type="file" name="upload"/><br/>
    <input type="submit" value="上传"/>
</form>
```



java:

```java
@RequestMapping("/upload")
public String upload(HttpServletRequest request) throws Exception{
    System.out.println("upload");
    String path = request.getSession().getServletContext().getRealPath("/uploads/");
    File file = new File(path);
    if(!file.exists()){
        file.mkdirs();
    }
    DiskFileItemFactory factory = new DiskFileItemFactory();
    ServletFileUpload upload = new ServletFileUpload(factory);
    List<FileItem> files = upload.parseRequest(request);//解析request,得到内容
    for(FileItem item:files){
        if(item.isFormField()){///判断是不是普通表单项

        }else{
            String name = item.getName();//得到文件名
            item.write(new File( path, name));//实现文件上传
            item.delete();//删除临时文件
        }
    }
    return "success";
}
```



### 12.7.2.springmvc的

jsp:

```jsp
<h3>springmvc统文件上传</h3>
<form action="file/upload2" method="post" enctype="multipart/form-data">
    文件上传:<input type="file" name="upload"/><br/>
    <input type="submit" value="上传"/>
</form>
```



springmvc.xml:springmvc专用上传文件的jar包

```xml
<bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver"></bean>
```



pom.xml:

```xml
<dependency>
      <groupId>commons-fileupload</groupId>
      <artifactId>commons-fileupload</artifactId>
      <version>1.4</version>
    </dependency>
    <dependency>
      <groupId>commons-io</groupId>
      <artifactId>commons-io</artifactId>
      <version>2.4</version>
    </dependency>
```



java:MultipartFile的实例名必须与表单上传文件部分的name相同

```java
@RequestMapping("/upload2")
public String upload2(HttpServletRequest request, MultipartFile upload) throws Exception{
    System.out.println("upload2");
    String path = request.getSession().getServletContext().getRealPath("/uploads/");
    File file = new File(path);
    if(!file.exists()){
        file.mkdirs();
    }
    String name = upload.getOriginalFilename();//得到文件名
    upload.transferTo(new File(path, name));
    return "success";
}
```



### 12.7.3.跨服务器上传

这种方式上传与springmvc的方式相比只需改动java文件。

```java
@RequestMapping("/upload3")
public String upload3(MultipartFile upload) throws Exception{
    System.out.println("upload3");
    String path = "http://localhost:8080/day02_springmvc_fileupload/upload/";

    String name = upload.getOriginalFilename();//得到文件名
    Client client = Client.create();
    WebResource webResource = client.resource(path + name);
    webResource.put(upload.getBytes());
    return "success";
}
```



## 12.8.异常处理

index.jsp:

```jsp
<a href="user/testException">testException</a><br/>
```



java:

```java
@RequestMapping("/testException")
public String testException() throws SysException{
    System.out.println("testException");
    try{
        int a = 10/0;
    }catch(Exception e){
        e.printStackTrace();
        throw new SysException("查询用户失败！！");
    }
    return "success";
}
```



SysException.java:

```java
public class SysException extends Exception{
	
	private String message;
	
	public SysException(String message){
		this.message = message;
	}
	
	public void setMessage(String message){
		this.message = message;
	}
	public String getMessage(){
		return message;
	}
}
```



SysExceptionResolver.java:

```java
import org.springframework.web.servlet.HandlerExceptionResolver;
import org.springframework.web.servlet.ModelAndView;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class SysExceptionResolver implements HandlerExceptionResolver{
	
	public ModelAndView resolveException(HttpServletRequest request,HttpServletResponse response,Object handler,Exception ex){
		SysException e = null;
		if(ex instanceof SysException){
			e = (SysException)ex;
		}else{
			e = new SysException("系统正在维护！！");
		}
		ModelAndView view = new ModelAndView();
		view.addObject("errormsg", e.getMessage());
		view.setViewName("error");
		return view;
	}
}
```



springmvc.xml:

```xml
<context:component-scan base-package="com.itheima.controller"></context:component-scan>

    <!-- 视图解释类 -->
    <bean id="internalResourceViewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/pages/"/>
        <property name="suffix" value=".jsp"/><!--可为空,方便实现自已的依据扩展名来选择视图解释类的逻辑  -->
    </bean>
	<!--配置异常处理器-->
	<bean id="sysExceptionResolver" class="com.itheima.exception.SysExceptionResolver"></bean>
    <!-- 默认的注解映射的支持 -->
    <mvc:annotation-driven />
```



error.jsp:

```jsp
<body>
    ${errormsg}
</body>
```



## 12.9.拦截器

### 12.9.1.单个拦截器

index.jsp:

```jsp
<a href="user/testIntercepter">testIntercepter</a>
```



controller:

```java
@RequestMapping("/testIntercepter")
public String testIntercepter(){
    System.out.println("testIntercepter");
    return "success";
}
```



拦截器：

```java
import org.springframework.web.servlet.HandlerInterceptor;
import org.springframework.web.servlet.ModelAndView;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class MyInterceptor implements HandlerInterceptor{
	//在controller执行前执行
	public boolean preHandle(HttpServletRequest request,HttpServletResponse response,Object handler) throws Exception{
		System.out.println("interceptor执行了11--前面");
		return true;
     //request.getRequestDispacher("/WEB-INF/pages/error.jsp").forword(request,response);
        //return false;//这样页面 跳转到success.jsp，而是跳转到error.jsp
	}
    
    //在controller执行后，jsp页面前执行
	public void postHandle(HttpServletRequest request,HttpServletResponse response,Object handler,ModelAndView view) throws Exception{
		System.out.println("interceptor执行了11--后面");
	}//这里可以用上述方式跳转页面，但是无返回值
    //在jsp页面后执行
	public void afterCompletion(HttpServletRequest request,HttpServletResponse response,Object handler,Exception e) throws Exception{
		System.out.println("interceptor执行了11--最后");
	}//这里不可以跳转页面，无返回值
}
```



在springmvc.xml中配置拦截器：

```xml
<mvc:interceptors>
    <mvc:interceptor>
        <mvc:mapping path="/user/*"/>
        <bean class="com.itheima.interceptor.MyInterceptor"/>
    </mvc:interceptor>
</mvc:interceptors>
```



### 12.9.2.多个拦截器

拦截器执行顺序以在springmvc.xml中配置顺序为主。

如下：

```xml
<mvc:interceptors>
    <mvc:interceptor>
        <mvc:mapping path="/user/*"/>
        <bean class="com.itheima.interceptor.MyInterceptor"/>
    </mvc:interceptor>
    <mvc:interceptor>
        <mvc:mapping path="/**"/>
        <bean class="com.itheima.interceptor.MyInterceptor2"/>
    </mvc:interceptor>
</mvc:interceptors>
```



此时执行顺序是：

先执行MyInterceptor的preHandle()方法，然后MyInterceptor2的preHandle()方法，

随后是MyInterceptor2的postHandle()方法，MyInterceptor的preHandle()方法，

最后是MyInterceptor2的afterCompletion()方法，MyInterceptor的afterCompletion()方法，







