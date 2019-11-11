# 6.struts02

## 6.1.搭建环境

### 6.1.1.加入jar包

（在路径：E:\jar\struts-2.3.20.3\lib\lib下面）

![1554087491344](D:\MyNote\images\1554087491344.png)

### 6.1.2.编写struts.xml文件

在类路径的顶层目录下，编写struts.xml文件

![1554087555343](D:\MyNote\images\1554087555343.png)

如果处于无网络环境，该文件可能产生警告。解决办法：

a. 在struts文件夹中找到lib下的一个jar包struts2-core-2.3.20.3.jar，然后进行解压缩，只需从里面去取出一个dtd文件struts-2.3.dtd即可；

b. 在WEB_INF目录下新建一个文件夹dtd，然后将dtd文件放入；

c. 在myeclipse的菜单栏中进入Window>preferences，然后搜索找到XML Catalog。

d. 点击右侧的Add；

![1554087670310](D:\MyNote\images\1554087670310.png)

e. 在location位置添加dtd的地址（只需点击下方的Workspace选择路径即可），然后将KeyType选为URI，在Key中填入http://struts.apache.org/dtds/struts-2.3.dtd即可。

### 6.1.3.编写struts的控制器

在web.xml中，编写struts的控制器

![1554087801404](D:\MyNote\images\1554087801404.png)

## 6.2.入门案例

### 6.2.1.编写struts.xml

开发阶段需要配置`struts.devMode` ,可以在修改代码后无需重启即可生效。package标签需继承struts-default才可以

![1554087931915](D:\MyNote\images\1554087931915.png)

### 6.2.2.编写类

动作类需要继承ActionSupport类

![1554088008117](D:\MyNote\images\1554088008117.png)

### 6.2.3.编写相关JSP

过滤器会拦截所有以.action结尾或无后缀的请求，如demo.action和demo

![1554088052493](D:\MyNote\images\1554088052493.png)

两个连接都跳转成功了。

## 6.3.入门案例内部执行过程

### 6.3.1.加载web.xml

Web应用启动tomcat时,会首先加载web.xml，检查内部servlet，filfter,listener路径是否正确，名称是否对应。

### 6.3.2.加载过滤器

加载web.xml时会同时初始化并实例化过滤器（实际上就是为了加载struts的过滤器，拦截所有访问动作的请求）。

### 6.3.3.加载struts.xml

初始化过滤器后，会继续加载struts.xml文件，建立动作与类之间的映射。

### 6.3.4.发送hello.action请求

在用户点击首页链接时，会向tomcat发送访问hello.action的请求。

### 6.3.5.拦截请求

当请求到达tomcat时，过滤器会拦截请求，并在struts.xml中查找相关动作。

### 6.3.6.实例化动作类

在struts.xml中查找到相应的类后进行实例化（每次找到都会创建一个新的实例），然后进行调用相应动作类，结果会产生返回值。

### 6.3.7.调动相关JSP

根据返回值在struts.xml中找到相应的视图页面进行调用，并向浏览器返回结果。

## 6.4.动作方法调用配置

### 6.4.1.自动布置

在struts.xml开始部分，与package标签同级，在struts开始标签内部

`<constant name="struts.devMode" value="true"></constant>`

### 6.4.2.动态方法调用

在struts.xml开始部分，与package标签同级，在struts开始标签内部

`<constant name="struts.enable.DynamicMethodInvocation" value="true"></constant>` 

### 6.4.3.使用通配符*

使用通配符*，配置动作方法 

*表示的是动作名称，当有和动作名称相匹配的时候可以用{出现的位置}来代替

a.

struts.xml:

```xml
<action name="*" class="com.itheima.web.action.UserAction" method="{1}">
	<result name="success">/{1}.jsp</result>
</action>
```

index.jsp:

```jsp
<a href="${pageContext.request.contextPath }/addUser.action">添加用户</a><br/>
<a href="${pageContext.request.contextPath }/updateUser.action">更新用户</a><br/>
<a href="${pageContext.request.contextPath }/deletUser.action">删除用户</a><br/>
<a href="${pageContext.request.contextPath }/findUser.action">查找用户</a><br/>
```

b.

struts.xml:

```xml
<action name="*_*" class="com.itheima.web.action.{2}Action" method="{1}{2}">
	<result name="success">/{1}{2}.jsp</result>
</action>
```

index.jsp:

```jsp
<a href="${pageContext.request.contextPath }/add_User.action">添加用户</a><br/>
<a href="${pageContext.request.contextPath }/update_User.action">更新用户</a><br/>
<a href="${pageContext.request.contextPath }/delete_User.action">删除用户</a><br/>
<a href="${pageContext.request.contextPath }/find_User.action">查找用户</a><br/>
```

​	

### 6.4.4.继承ActionSupport类

动作类需继承ActionSupport类，默认动作类会变为ActionSupport，默认方法是execute。

## 6.5.分文件编写配置文件

这样做的原因：

1、首先需要在struts.xml同一包中编写动作相关方法。当系统模块变多时，不同模块的动作在一个包会混杂在一起。

2、此时可以通过将不同模块的动作分包（package）而放来解决这种混乱的局面。

3、一个人编辑同一个文件时虽然不会混乱，但是当多人编写同一个配置文件时会变得混乱。所以可以采取分文件编写配置文件。

## 6.6.封装参数

### 6.6.1.静态封装

将参数以注入的方式封装在动作中，如图：

![1552552309970](D:\MyNote\images\1552552309970.png)

### 6.6.2.动态封装参数1

动作类正常配置，动作方法中同时封装了实体类的属性。动作方法如图：

![1552552502120](D:\MyNote\images\1552552502120.png)

​	动作类如图：

![1552552537812](D:\MyNote\images\1552552537812.png)

### 6.6.3.动态封装参数2

动作类正常配置，动作方法中将不再保留实体类的属性而是引入实体类。动作方法如图：

![1552552771630](D:\MyNote\images\1552552771630.png)

同时，JSP中需要改变，如图：

![1552552890258](D:\MyNote\images\1552552890258.png)

### 6.6.4.模型驱动

动作类正常配置，jsp同样正常配置，其他变化如下：

实现步骤：
​	 1.实现ModelDriven<T>接口

​	2.实现接口需要实现的方法

​	3.使用模型驱动方式时，必须自己将数据模型实例化

![1552553085143](D:\MyNote\images\1552553085143.png)

jsp配置如下：

![1552553256565](D:\MyNote\images\1552553256565.png)



## 6.7.类型转换器

举例：将日期类型格式由yyyy-mm-dd转换为mm/dd/yyyy

### 6.7.1.创建转换类

要求必须创建一个类并继承StrutsTypeConverter，代码如下：

```java
import java.text.DateFormat;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Map;

import org.apache.struts2.util.StrutsTypeConverter;

public class MyTypeConvert extends StrutsTypeConverter {
	
	private DateFormat format = new SimpleDateFormat("MM/dd/yyyy");
	/**日期数据转换器
	 * 参数解读：
	 * 	arg1:需要转换的参数
	 * 	arg2:目标类型
	 */

	@SuppressWarnings("rawtypes")
	@Override
	public Object convertFromString(Map arg0, String[] arg1, Class arg2) {
		//1. 检查arg1是否为空
		if(arg1 == null||arg1.length == 0){
			return null;
		}
		//2. 取出arg1的第一个参数
		String value = arg1[0];
		//3. 检查arg2的字节码是否是日期类型
		if(arg2 == java.util.Date.class){
		//4. 转换并返回结果
			try {
				return format.parse(value);
			} catch (ParseException e) {
				e.printStackTrace();
				return null;
			}
		}
		return null;
	}

	@SuppressWarnings("rawtypes")
	@Override
	public String convertToString(Map arg0, Object arg1) {
		//1. 首先判断arg1是否是日期类型
		if(arg1 instanceof Date){
		//2. 是则将其转换成指定的格式并返回
			Date date = (Date) arg1;
			return format.format(date);
		}
		return null;
	}

}
```



### 6.7.2.配置类型转换器

​	关于类型转换器的配置有两种方法，一种局部的，一种全局的。

1.局部的配置

在javabean类同路径下建立javabean类名-conversion.properties文件，内部内容如下：

```properties
birthday=com.itheima.utils.MyTypeConvert
```

2.全局的配置

在src路径下建立固定名称的xwork-conversion.properties文件，内容是：

```properties
java.util.Date=com.itheima.utils.MyTypeConvert
```

3.类型转换失败后的处理

​	类型转换失败后，转换视图是有conversionError拦截器控制的,因此动作类需要继承ActionSupport类。

​	当表单数据格式错误时，需要让页面回到原来的页面而不是跳转到一个系统出错的页面。此时可以在struts.xml配置一下用户输入信息格式有误时的结果。

```xml
<result name='input'>/register/jsp</result>
```

​	然后在表单页面添加如下代码，多了页面红框里面的提示:

![1553847690319](D:\MyNote\images\1553847690319.png)

页面变化：![1553847750857](D:\MyNote\images\1553847750857.png)



​	jsp部分除了上面这种处理办法，还有另外一种。就是使用struts特有的标签：

![1553848712468](D:\MyNote\images\1553848712468.png)

页面：

![1553848742791](D:\MyNote\images\1553848742791.png)

关于中文，还需要在javabean下添加一个以javabean名称命名的properties文件，内容：

```properties
invalid.fieldvalue.birthday=\u751F\u65E5\u683C\u5F0F\u65E0\u6548\uFF0C\u683C\u5F0F\uFF1Ayyyy-MM-dd
```



Invalid field value for field "birthday"》invalid.fieldvalue.birthday

## 6.8.数据验证

### 6.8.1编程式验证

​	在struts02中可以通过在动作类中：:one: 实现ActionSupport;:two: 重写validate方法来实现数据验证。

```java
public void validate(){
    if(StringUtils.isBlank(user.getUsername()))
        //使用commons-lang3.jar中的StringUtil方法的isEmpty进行字段的非空校验（不去字段内空格）
        //使用isBlank()同样可以（去除字段内空格）
        addFieldError("username", "请输入用户名！");
}
```

​	这种方法会在这个动作执行之前，进行数据验证。

​	要想实现让单个方法不进行数据验证可以在方法上方加注解`@SkipValidation`；如果只想让某个方法进行验证也可以是validate+动作名称即可(命名采用驼峰命名)，如validateRegister()。（动作名称指的是struts.xml中action的name属性）

![1556075241554](D:\MyNote\images\1556075241554.png)

### 6.8.2.声明式验证

:one:	全局的数据验证

在src路径下配置ActionClassName-validation.xml文件，内容格式如下：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE validators PUBLIC
	"-//Apache Struts//XWork Validator 1.0.3//EN"
	"http://struts.apache.org/dtds/xwork-validator-1.0.3.dtd">
<validation>
<!-- 基于字段的验证 -->
	<field name="username">
	<!-- field中name指定的是表单中name属性取值 -->
		<field-validator type="requiredstring">
		<!-- struts2中有许多内置验证器，requiredstring会验证输入内容是否为空，是否为空字符串，并且去除左右空格。-->
			<message>请输入用户名</message>
		</field-validator>
	</field>
    
    <!-- 基于验证器的验证 -->
	<validator type="requiredstring">
	<!-- 以注入的方式提供要验证的字段信息，setFieldName("password") -->
		<param name="fieldName">password</param>
		<message>请输入密码</message>
	</validator>
</validation>
```



名称实例：为UserAction这个动作类建立xml文件，名称为UserAction-validation.xml。

这个文件验证的是全局的。可以通过注解`@SkipValidation`让某些方法不进行验证。

:two:  局部的数据验证

在动作类所在包下建立xml文件，格式是动作类名称-动作名称-validation.xml（动作名称是指struts.xml中action的name属性），内容与上面相同。

 :three: 数据验证失败

1.检查validation文件名是否符合规则；

2.检查每个需要验证的字段的name是否与jsp页面的字段的name相等，顺便检查每个标签是否都是开标签和比标签对应，如果有不对应的，开发工具能不会给出提示; 

3.检查xml文件开头的struts的引用是否正确，不同版本struts的引用会有所不同；

struts的引用：

```xml
<!DOCTYPE validators PUBLIC
	"-//Apache Struts//XWork Validator 1.0.3//EN"
	"http://struts.apache.org/dtds/xwork-validator-1.0.3.dtd">
```



4.检查struts.xml中结果处理中是否有对input结果的处理；

5.检查实体类与动作类名称是否相符（如User与UserAction）;

6.检查动作类是否实现了ActionSupport；

7.如果采用了模型驱动的方式，检查是否有实现了`ModelDriven<T>` 的接口；

 :four: 案例

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE validators PUBLIC
	"-//Apache Struts//XWork Validator 1.0.3//EN"
	"http://struts.apache.org/dtds/xwork-validator-1.0.3.dtd">
<validators>
	<!-- 基于字段的验证 -->
	<field name="username">
		<!-- field中name指定的是表单中name属性取值 -->
		<field-validator type="requiredstring">
			<!-- struts2中有许多内置验证器，requiredstring会验证输入内容是否为空，是否为空字符串，并且去除左右空格。 -->
			<message>请输入用户名</message>
		</field-validator>
	</field>

	<field name="age">
		<field-validator type="int">
			<!-- 使用注入方式，设置最大值和最小值 -->
			<param name="min">18</param>
			<param name="max">100</param>
			<message>请输入18到100之间整数</message>
		</field-validator>
	</field>

	<field name="email">
		<field-validator type="email">
			<message>请输入正确的邮箱格式</message>
		</field-validator>
	</field>

	<field name="password">
		<field-validator type="requiredstring">
			<!-- 注入取消trim -->
			<param name="trim">false</param>
			<message>请输入密码</message>
		</field-validator>
		<field-validator type="requiredstring">
			<param name="minLength">3</param>
			<param name="maxLength">8</param>
			<message>请输入3到8位密码</message>
		</field-validator>
	</field>

	<!-- 确认密码与密码需保持一致，是2个字段的事，所以要使用基于验证器的方式 -->
	<validator type="expression">
		<param name="expression">
			<![CDATA[password==repassword]]>
		</param>
		<message>两次密码必须一致</message>
	</validator>

	<field name="score">
		<field-validator type="regex">
			<param name="regex">
				\d+
			</param>
			<message>请输入正确的成绩</message>
		</field-validator>
	</field>

	<field name="url">
		<field-validator type="url">
			<message>请输入正确格式的url</message>
		</field-validator>
	</field>

	<field name="gender">
		<!-- 只验证是否为null，不会去空格 -->
		<field-validator type="required">
			<message>请选择性别</message>
		</field-validator>
	</field>
</validators>
```



## 6.9.国际化i18n

### 6.9.1.r18n

1.编写配置文件

​	文件名称规则：`主文件名称_语言代码_国家代码.properties` ，名称没有规则，随意编写，如message，语言编码和国家代码需要自己搜索，通过百度或jdk手册查询，文件至少编辑2个。例如中国的和美国的，文件放置位置无规定；

![1556174992525](D:\MyNote\images\1556174992525.png)

2.读取配置文件

在测试类中通过类ResourceBundle的getBundle("文件所在包.主文件名称",Locale.国家常量)方法读取配置文件，在通过getString("key的name")。

![1556175183348](D:\MyNote\images\1556175183348.png)

3.在jsp页面配置

首先加载文件，在jsp文件开头部分：

```jsp
<%
Locale locale = request.getLocale();
ResourceBundle resource = ResourceBundle.getBundle("com.itheima.resource.message", locale);
 %>
```

然后将中文名成标签等需要国际化部分进行替换。

```jsp
  <head>
    <title><%=resource.getString("jsp.register.title") %></title>
  </head>
  <body>
   	<%=resource.getString("jsp.register.username") %>:<input type="text" name="username"/><br/>
   	<%=resource.getString("jsp.register.password") %>:<input type="password" name="password"/><br/>
   	<input type="submit" value="<%=resource.getString("jsp.register.button")%>"/>
  </body>
```

### 6.9.2.struts2中国际化

1.全局范围配置

在单独的package中添加消息资源包，可以设置为全局范围的。（消息资源包就用上方编写的就可以）

使用方式是首先在struts.xml中进行配置，在`<struts>`标签下添加：

```xml
<constant name="struts.custom.i18n.resources" value="com.itheima.resource.message"/>
```

在动作方法中可以通过`getText("key")` 获取消息资源包中的key值。

2.包范围配置

将消息资源包放在全局范围配置所在包的上一级包中时，不需要其他配置即可成为优先级高于全局配置的包范围配置。（消息资源包就用上方编写的就可以）

3.动作类范围

将消息资源包放在动作类所在包下面，资源包主文件名称需要改成动作类名。（消息资源包就用上方编写的就可以）

资源包位置配置如图：

![1556179280685](D:\MyNote\images\1556179280685.png)

4.资源包查找顺序

struts获取配置使用的是就近原则。如果直接在页面上访问消息资源包则不会经过struts的action，不会触发类范围的和包范围的消息资源包，只会触发配置过的全局的消息资源包。而如果经过action则需要采取就近原则，有限使用动作类范围的。

5.在jsp中访问资源包

```jsp
<s:text name="key"></s:text>
```

如果资源包中不存在名为key的key，则会直接将key作为内容输出。

也可以在经过动作类时自由指定资源包位置：

```jsp
<s:i18n name="com.itheima.resource.message">
	<s:text name="key"></s:text>
</s:i18n>
```



当自由指定的包不存在时，会按照资源包的搜索顺序查找。如下：

![1556180174317](D:\MyNote\images\1556180174317.png)

## 6.10.自定义拦截器

定义方法：

​	1.定义一个类，并且这个类要继承AbstractInterceptor这个类；

```java
import com.opensymphony.xwork2.ActionInvocation;
import com.opensymphony.xwork2.interceptor.AbstractInterceptor;
public class Interapter1 extends AbstractInterceptor {
	public String intercept(ActionInvocation arg0) throws Exception {
		System.out.println("interapter1执行了");
		return null;
	}
}
```



​	2.在struts.xml需要使用这个拦截器的package中，声明这个拦截器，并在action中使用这个拦截器;

```xml
<package name="p1" extends="struts-default">
		<interceptors>
		<!-- 声明拦截器 -->
		</interceptors>
		<action name="save" class="com.itheima.web.action.Action1" method="save">
			<interceptor-ref name="demo1"></interceptor-ref>
			<!-- 使用拦截器 -->
			<result>/demo1.jsp</result>
		</action>
	</package>
```

​	3.在拦截后处理完数据就可以放行(放行语句：arg0.invoke())了，拦截器执行完需要返回结果视图（input,success等）；

```java
public String intercept(ActionInvocation arg0) throws Exception {
		System.out.println("interapter1执行了");
		String result = arg0.invoke();
		System.out.println("interapter放行了");
		return result;
	}
```

​	

拦截器在动作执行前，会进行拦截处理数据。然后放行执行动作。执行完动作，会再次经过拦截器处理数据。

如果有多个拦截器，如1,2,3，拦截器执行顺序为1，2，3，动作，页面，3，2，1，前面的1,2,3执行循序是由在action中配置的拦截器使用顺序决定的。

​	4.配置包内全局的结果视图

​	在package标签内部，

```xml
<global-results>
			<result name="input">/login.jsp</result>
</global-results>
```



​	全局的结果视图作用是当某个动作没有配置该视图时，会在全局的结果视图里搜索该视图，搜索到就使用。

​	5.配置自己的拦截器栈

```xml
<package name="p2" extends="struts-default">
    <interceptors>
        <interceptor name="checklogin" class="com.itheima.web.interapter.CheckLoginInterapter"></interceptor>
        <!--声明拦截器-->
        <interceptor-stack name="myDefaultStack">
            <!--配置拦截器栈-->
            <interceptor-ref name="defaultStack"></interceptor-ref>
            <interceptor-ref name="checklogin"></interceptor-ref>
        </interceptor-stack>
    </interceptors>
    <action name="showMain" class="com.itheima.web.action.Action2">
        <interceptor-ref name="myDefaultStack"></interceptor-ref>
        <!--使用拦截器栈-->
        <result>/main.jsp</result>
    </action>
	</package>
```



6.配置默认的拦截器使用栈后，会覆盖struts原来默认的。

在package标签内配置如下：

```xml
<default-interceptor-ref name="myDefaultStack"></default-interceptor-ref>
```



这样需要使用默认拦截器使用栈的动作就不需要自己另外配置拦截器了。

但是这样的设置会导致所有的动作都相当于配置了这个拦截器使用栈。可以通过在拦截器栈内的拦截器声明中配置参数excludeMethods或includeMethods来控制哪些动作需要被拦截，哪些不需被拦截。includeMethods控制需要拦截的动作，excludeMethods控制不需要拦截的动作。两者可以只配置一种。配置这两个参数时，有个前提，就是动作需要继承MethodFilterInterceptor这个类，这个类也继承自AbstractInterceptor。这个类的子类必须实现的方法是doIntercept。

```xml
<interceptors>
    <interceptor name="checklogin2" class="com.itheima.web.interapter.CheckLoginInterapter2"></interceptor>
    <interceptor-stack name="myDefaultStack">
        <interceptor-ref name="defaultStack"></interceptor-ref>
        <interceptor-ref name="checklogin2">
            <!--不拦截login动作-->
            <param name="excludeMethods">login</param>
        </interceptor-ref>
    </interceptor-stack>
</interceptors>
```



拦截器与动作：先有拦截器，后有动作，因此不能在拦截器中配置参数excludeMethods，includeMethods。所以我们需要在动作内进行声明。

```xml
<action name="login" class="com.itheima.web.action.Action2" method="login">
    <interceptor-ref name="myDefaultStack">
        <param name="checklogin2.excludeMethods">login</param>
    </interceptor-ref>
    <result type="redirectAction">showMain</result>
</action>
```



## 6.11.文件上传下载

### 6.11.1文件上传

1.form表单的要求；

​	a.请求方式method必须是post;

​	b.enctype属性取值必须是multipart/form-data；

​	c.提供一个文件上传域file；

2.配置struts.xml；

3.编写动作；

```java
//表单提供的字段
private String username;
private File file;
private String fileFileName;//上传的文件名，上传字段名称+FileName 注意大小写
private String fileContentType;//上传文件的MIME类型，上传字段名称+ContentType,注意大小写
public String upload(){
    //1.拿到ServletContext
    ServletContext servlet = ServletActionContext.getServletContext();
    //2.调用realPath,根据一个虚拟目录路径获得其内部的一个真实目录路径
    String filePath = servlet.getRealPath("/WEB-INF/files");
    File file1 = new File(filePath);
    //3.检查目录是否存在，如果不存在就创建
    if(!file1.exists()){
        file1.mkdirs();
    }
    //4.将photo下载到服务器的文件夹内
    //通过拷贝将file的临时文件拷贝过去，但是临时文件还在。
    //FileUtils.copyFile(file, new File(file1, fileFileName));
    //通过剪切将file的临时文件剪切过去，此时临时文件已经不在了。
    file.renameTo(new File(file1, fileFileName));
    return null;
}
public String getUsername() {
    return username;
}
public void setUsername(String username) {
    this.username = username;
}
public File getFile() {
    return file;
}
public void setFile(File file) {
    this.file = file;
}
public String getFileFileName() {
    return fileFileName;
}
public void setFileFileName(String fileFileName) {
    this.fileFileName = fileFileName;
}
public String getFileContentType() {
    return fileContentType;
}
public void setFileContentType(String fileContentType) {
    this.fileContentType = fileContentType;
}
```



### 6.11.2.文件上传限制

struts有默认的文件上传大小，是2M。解除限制有几种方式。

第一种方式：修改struts2中的常量

```xml
<!--第一种方式：修改struts2中的常量，在default.properties中配的struts.multipart.maxSize=2097152-->
<constant name="struts.multipart.maxSize" value="5242880"></constant>
```

第二种方式：在拦截器使用声明中注入参数

虽然是有这种方式，但是不能用，可能是个bug。

```xml
<package name="p1" extends="struts-default">
    <action name="upload" class="com.itheima.web.aciton.UploadAction" method="upload">
        <interceptor-ref name="defaultStack">
            <param name="fileUpload.maxmumSize">31457280</param>
        </interceptor-ref>
        <result>/index.jsp</result>
    </action>
</package>
```

### 6.11.3.限制文件上传类型

1.限制文件扩展名

通过在拦截器使用栈中注入参数，控制允许上传的文件类型；

```xml
<interceptor-ref name="defaultStack">
    <param name="fileUpload.allowedExtensions">jpg,png,bmp</param>
</interceptor-ref> 
```



2.限制文件的MIME类型

通过在拦截器使用栈中注入参数，控制允许上传的文件类型；

```xml
<interceptor-ref name="defaultStack">
    <param name="fileUpload.allowedTypes">image/jpg,image/jpeg,image/png</param>
</interceptor-ref> 
```



3.错误提示

当文件类型不符合要求时会出现错误提示（前提是页面上有写动作错误提示）。如下：

![1556527615220](D:\MyNote\images\1556527615220.png)

为了让提示更加友好，可以这样做：

​	1.编写文件;

​		比如在src路径下编写文件fileUpload_message.properties，内容如下：

```xml
struts.message.error.content.type.not.allowed=\u4E0A\u4F20\u7684\u6587\u4EF6\u7C7B\u578B\u4E0D\u652F\u6301\: {0} "{1}" "{2}" {3}
```



​	2.在struts.xml中配置文件；

```xml
<constant name="struts.custom.i18n.resources" value="com.itheima.web.action.fileupload_message"></constant>
```



### 6.11.4.多文件上传

页面：

```jsp
<s:form action="upload2.action" enctype="multipart/form-data">
    <s:textfield name="username" label="用户名"/>
    <s:file name="file" label="头像"/>
    <s:file name="file" label="头像"/>
    <s:submit value="上传"/>
</s:form>
```



java：

```java
private String username;
private File[] file;
private String[] fileFileName;//上传的文件名，上传字段名称+FileName 注意大小写
private String[] fileContentType;//上传文件的MIME类型，上传字段名称+ContentType,注意大小写

public String upload(){
    //1.拿到ServletContext
    ServletContext servlet = ServletActionContext.getServletContext();
    //2.调用realPath,根据一个虚拟目录获得一个真实目录
    String filePath = servlet.getRealPath("/WEB-INF/files");
    File file1 = new File(filePath);
    //3.检查目录是否存在，如果不存在就创建
    if(!file1.exists()){
        file1.mkdirs();
    }
    //4.将photo放过去
    //通过拷贝将file的临时文件拷贝过去，但是临时文件还在。
    //		FileUtils.copyFile(file, new File(file1, fileFileName));

    //通过剪切将file的临时文件剪切过去，此时临时文件已经不在了。
    for(int i=0;i<file.length;i++){
        file[i].renameTo(new File(file1, fileFileName[i]));
    }
    return null;
}
```



### 6.11.5.文件下载

java:

```java
//注意：为inputstream指定名称时不能用in
private InputStream inputStream;	
public String download() throws Exception{
    //1.找到文件存储路径
    String filePath = ServletActionContext.getServletContext().getRealPath("/WEB-INF/files/download.jpg");
    //2.将文件放入一个inputstream中
    setInputStream(new FileInputStream(filePath));
    //返回成功
    return SUCCESS;
    //有一个叫stream的结果类型为我们把剩下的事情做完
}
public InputStream getInputStream() {
    return inputStream;
}
public void setInputStream(InputStream inputStream) {
    this.inputStream = inputStream;
}
```



struts.xml:

```xml
<action name="download" class="com.itheima.web.aciton.DownloadAction" method="download">
    <result name="success" type="stream">
        <!--给stream的结果类型注入参数：Content-Type  -->
        <param name="contentType">application/octet-stream</param>
        <!-- 告知客户以下载的方式打开 ，下载文件名称为file.jpg-->
        <param name="contentDisposition">attachment;filename=file.jpg</param>
        <!-- 注入字节输入流：取值要写动作类中的set方法名称 -->
        <param name="inputName">inputStream</param>
    </result>
</action>
```



## 6.12.OGNL

### 6.12.1.OGNL简介

OGNL是Object Graphic Navigation Language（对象图导航语言）的缩写，它是一个单独的开源项目。 Struts2框架使用OGNL作为默认的表达式语言。

### 6.12.2.EL表达式自定义方法

1.写一个普通类，提供一个实现功能的方法，例如：

```java
public class OGNLDemo {
	public static String toUpperCase(String str){
		return str.toUpperCase();
	}
}
```



2.在WEB-INF目录中创建一个扩展名为.tld的xml文件，但文件不能放在classes和lib目录中。内容：

```xml
<taglib xmlns="http://java.sun.com/xml/ns/j2ee" 		   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://java.sun.com/xml/ns/j2ee   http://java.sun.com/xml/ns/j2ee/web-jsptaglibrary_2_0.xsd"
	version="2.0">
	<tlib-version>1.0</tlib-version><!-- 指定标签库或方法库版本号 -->
	<short-name>myfn</short-name><!-- 使用的短名称。对应的是taglib指令中的prefix -->
	<!-- uri:把当前的方法库绑定到一个uri地址上，在该网址上不一定存在方法库 -->
	<uri>http://www.itheima.com/functions/myfunction</uri>
	<function><!-- 自定义方法 -->
		<name>touppoercase</name><!-- 方法的名称，是jsp页面上使用的名称 -->
		<!-- 指定执行的类 -->
		<function-class>com.itheima.web.function.MyFunction</function-class>
		<!-- 指定执行的方法。方法名称必须和类中的方法名称保持一致
			注意：当方法有参数和返回值时：参数和返回值必须写类全名（除了基本数据类型）
		-->
		<function-signature>java.lang.String toUpperCase( java.lang.String )
        </function-signature>
	</function>
</taglib>
```



xml命名空间的引用来自于tomcat/webapps/examples/WEB-INF/jsp2下的一个扩张名为.tld的文件。

3.在jsp页面的使用

```jsp
<%@ page language="java" import="java.util.*" pageEncoding="UTF-8"%>
<%@ taglib uri="http://www.itheima.com/functions/myfunction"  prefix="myfn"%>
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
  <head>
    <title>My JSP 'index.jsp' starting page</title>
  </head>
  <body>
    abcde-->ABCDE
    <br/>
    ${myfn:touppoercase("abcde")}
  </body>
</html>
```



EL表达式的限制是在jsp页面只能使用静态方法。

注意：EL表达式原理就是调用了pageContext.findAttribute("name"),查找name的顺序是page(PageContext，即外面的大Map或动作类中设置的属性)--request--valueStack--session-application

### 6.12.3.OGNL的使用

1.首先引入struts2的标签；

```jsp
<%@ taglib uri="/struts-tags" prefix="s"%>
```

2.然后使用

- 2.1.输出值或使用方法

  ```jsp
  <s:property value="OGNL-Expression"/>-OGNL的表达式<br/>
  <s:property value="'OGNL-Expression'"/>-OGNL的字符串（加了单引号）<br/>
  <s:property value="'OGNL-Expression'.length()"/>
  		  -OGNL的字符串调用了获取字符串长度的方法<br/>
  ```

- 2.2.访问静态属性

  ```jsp
  <%--OGNL访问静态属性方式：@全类名@静态属性--%>
  <s:property value="@java.lang.Integer@MAX_VALUE"/><br/>
  ```

- 2.3.访问静态方法

  由于struts2对ognl访问静态方法默认是拒绝的，所以需要在struts.xml中配置一下才可以访问。

  ```xml
  <constant name="struts.ognl.allowStaticMethodAccess" value="true"/>
  ```

  现在可以在jsp中访问静态方法了，与访问静态属性方法相同

  ```jsp
  <s:property value="@java.lang.Math@random()"/><br/>
  ```

- 2.4.OGNL操作map和list

  ```jsp
  <%--
      OGNL操作map与list
    		使用的是s:radio的标签，创建list集合，{}相当于创建list集合，list属性的取值是一个OGNL的表达式
  --%>
  <s:radio name='gender' list="{'男','女'}"/><br/>
  <%--
      使用s:radio创建一个map，#{}表示一个map集合，1和0作为value给radio标签的value赋值，男和女作为key显示在页面
  --%>
  <s:radio name='gender' list="#{'1':'男','0':'女'}"/><br/>
  ```

  

3.OGNL在xml中的使用

```xml
<!-- ${}可以把中间的内容当成一个OGNL表达式对待 -->
<param name="contentDisposition">attachment;
    filename=${@java.net.URLEncoder@encode(filename, "UTF-8")}</param>
```



注意：OGNL表达式,查找name的顺序是page(PageContext)--request--valueStack(根中)--contextMap--session-application,OGNL表达式中如果不写#号时，它会从值栈的栈顶查找对应的属性。如果没有则会去ActionContext中在把value的值当作key去查找。

## 6.13.存取数据

### 6.13.1.ActionContext

这是一个map类型的存储结构

1.在ActionContext中存数据

```java
ActionContext context = ActionContext.getContext();
context.put("contextMap", "hello contextMap");
```



2.在session中存数据

```java
//第一种方式：获取key为isession的map
Map<String, Object> session = context.getSession();
session.put("session1", "hello session1");
//第二种方式：使用原始的HttpSession对象
HttpSession session2 = ServletActionContext.getRequest().getSession();
session2.setAttribute("session2", "hello session2");
```



3.在application中存数据

```java
//第一种方式：获取key为application的map
Map<String, Object> application = context.getApplication();
application.put("application1", "hello application1");
//第二种方式：使用原始的ServletContext对象
ServletContext application1 = ServletActionContext.getServletContext();
application1.setAttribute("application2", "hello application2");
```

4.在jsp页面取值

```jsp
<!-- 使用s:property获取ActionContext的数据，value属性的取值是一个OGNL的表达式 -->
<br/>----------获取大Map的数据--------------<br/>
<!-- 获取外围大map的key,方法是#key名称 -->
<s:property value="#contextMap"/><br/>
<!-- 获取外围大map中小map的key,方法是#大Map的key名称.小map的key名称 -->
<s:property value="#session.session1"/>
<s:property value="#application.application1"/>
```



### 6.13.2.ValueStack

这是一个list的存储结构

1.获取valueStack对象

1.1.获取HttpServletRequest对象，通过它的getAttribute()方法从域中取

```java
/1.获取HttpServletRequest对象
HttpServletRequest request = ServletActionContext.getRequest();
//2.通过它的getAttribute()方法从域中取
ValueStack valueStack1 = (ValueStack)request.getAttribute("struts.valueStack");
```



1.2.先获取ActionContext对象，再取出requestMap，然后通过map的get方法获取

```java
//1.先获取ActionContext对象
ActionContext context = ActionContext.getContext();
//2.再取出requestMap
Map<String, Object> requestMap = (Map<String, Object>) context.get("request");
//3.然后通过map的get方法获取（通过key获取对象的引用）
ValueStack valueStack2 = (ValueStack) requestMap.get("struts.valueStack");
```



1.3.使用ActionContext直接获取对象

```java
ValueStack valueStack3 = context.getValueStack();
```

2.存数据

2.1.用push()方法存数据

```java
valueStack3.push(new Student("test", 21));
```



2.2.用setValue()方法存数据

​	`setValue(String expr, Object value)`,`String expr`--ognl表达式,`Object value`--需要操作的数据,数据存哪里主要看第一个参数是否含有`#`,

第一个参数如果含有#则是操作contextMap中的数据:

```java
valueStack3.setValue("#name", "tom");
```



第一个参数如果不含有#则是操作valueStack中的数据:

```java
valueStack3.setValue("name", "tom");
```



2.3.用set()方法存数据

`set(String key, Object o)`,`String key`-- Map的key,'Object o'--map的value.如果栈顶是一個map元素，则直接把key作为map的key，把Object做为map的value存入，存入的是栈顶;如果栈顶不是一個map元素，则创建一个map元素，把key作为map的key，把Object做为map的value存入，存入的是栈顶

```java
valueStack3.set("test2", new Student("rose", 23));
```



3.在jsp页面取数据

```jsp
<!-- 获取valueStack中的元素
获取ValueStack中的值是直接写属性名字，不需要在前面加#
它是从栈顶向下逐项查找属性名称，一旦查到则停止查找
-->
<s:property value="name"/><br/>
<!-- 获取valueStack指定位置的属性值 -->
<s:property value="[2].name"/>
<!-- 获取通过set方法压入栈顶的rose里的name -->
<s:property value="test2.name"/><br/>
<!-- <s:property/>默认获取栈顶元素 -->
<s:property/>
<s:debug/>
```



![1558598859376](D:\MyNote\images\1558598859376.png)



![1558598765575](D:\MyNote\images\1558598765575.png)



![1558598810165](D:\MyNote\images\1558598810165.png)

第一个页面从第二个页面查找，结果是第三个页面。

`<s:property value="[2].name"/>` 的原理是使用了一个叫cutStack()的方法，这个方法需要1个参数，是[]中的值。如果是2，则这个方法会将栈顶对象减少2个，然后查找name属性，找到第一个并返回，也就是标签显示的结果。

## 6.14.迭代标签

1.s:iterator是struts2的迭代标签；

2.属性详解：

​	begin、end、step和jstl的forEach标签一样；

​	value:要遍历的集合，是个OGNL的表达式；

​	var:取值就是一个字符串，

​			如果写了该属性，则会把var值作为key，把当前遍历的元素作为value，存入ActionContext的大Map中；

​			如果不写该属性，把当前遍历的元素压入栈顶；

​	ststus:遍历时的一些计数信息，

​			int getIndex() 从0开始计数

​			int getCount() 从1开始

​			boolean isFirst() 是否是第一个

​			boolean isLast() 是否是最后一个

​			boolean isOdd() 是否是奇数

​			boolean isEven() 是否是偶数

3.实例

动作类部分：

```java
private List<Student> students;

	public String findAll(){
		students = new ArrayList<Student>();
		students.add(new Student("tom", 21));
		students.add(new Student("rose", 23));
		students.add(new Student("jack", 31));
		return SUCCESS;
	}
	
	public List<Student> getStudents() {
		return students;
	}

	public void setStudents(List<Student> students) {
		this.students = students;
	}
```



jsp页面部分：

```jsp
<table width="500px" border="2" align="center">
    <tr>
        <th>序号</th>
        <th>姓名</th>
        <th>年龄</th>
    </tr>
    <s:iterator value="students" var="s" status="vs">
        <tr>
            <td><s:property value="#vs.index"/></td>
            <td><s:property value="#s.name"/></td>
            <td><s:property value="#s.age"/></td>
        </tr>
    </s:iterator>
</table>
<hr/>
<table width="500px" border="2" align="center">
    <s:iterator value="students" status="vs">
        <tr>
            <td><s:property value="#vs.count"/></td>
            <td><s:property value="name"/></td>
            <td><s:property value="age"/></td>
        </tr>
    </s:iterator>
</table>
```



效果：

![1558926124970](D:\MyNote\images\1558926124970.png)

4.OGNL的投影：添加过滤条件

a."?#":过滤所有符合条件的集合，如users.{?#this.age>19}

​	"^#":过滤第一个符合条件的集合，如users.{^#this.age>19}

​	"$#":过滤最后一个符合条件的集合，如users.{$#this.age>19}

实例：

```jsp
<s:iterator value="students.{?#this.age>22}" status="vs">
    <tr>
        <td><s:property value="#vs.count"/></td>
        <td><s:property value="name"/></td>
        <td><s:property value="age"/></td>
    </tr>
</s:iterator>
```

效果：

![1558926166862](D:\MyNote\images\1558926166862.png)



b.指定输出内容：students.{name}

实例：

```jsp
<table width="500px" border="2" align="center">
    <s:iterator value="students.{name}" status="vs">
        <tr>
            <td><s:property value="#vs.count"/></td>
            <td><s:property /></td>
            <td><s:property /></td>
        </tr>
    </s:iterator>
</table>
```



效果：

![1558927194912](D:\MyNote\images\1558927194912.png)

## 6.15.其他标签

1.s:set

​	value属性:取值是一个OGNL表达式

​	var属性：是一个普通字符串

这个标签是吧value属性的值作为value，吧var属性作为key，然后存到ActionContextMap中

实例：

```jsp
<s:set value="'test'" var="t"></s:set>
```



效果:

![1558937362426](D:\MyNote\images\1558937362426.png)

2.s:action

​	name属性:指定一个动作的名称，但不会执行

​	executeResult属性:指定是否执行动作，取值只有true,false

实例：

```jsp
<s:action name="action1" executeResult="true"></s:action>
```



效果：多了两个debug中间的东西和第一个debug了

![1558937459860](D:\MyNote\images\1558937459860.png)

3.s:if s:elseif s:else

​	test属性：指定判断条件，判定显示的数据

实例:

```jsp
<s:set value="'test11'" var="t"></s:set><br/>
<s:if test="#t=='test'">1</s:if>
<s:elseif test="#t=='test1'">2</s:elseif>
<s:else>3</s:else><br/>
```



效果：

![1558938288940](D:\MyNote\images\1558938288940.png)

4.s:url

​	value属性：将值输出到页面

​	action属性：将动作类的请求地址输出到页面

​	var属性：将action的值作为value，var的值作为key存入ActionContextMap中

实例：

```jsp
<s:url value="action1"></s:url><br/>
<s:url action="action1" var="action"></s:url><br/>
```



效果：

![1558938795490](D:\MyNote\images\1558938795490.png)

实例：

```jsp
<a href="<s:property value='#action'/>">#url</a><br/>
<a href="${pageContext.request.contextPath }/action1.action">pagecontext</a><br/>
```



它可以根据struts配置转换后缀名，如果在struts.xml中配置struts.actionextension，值为html，则可以让第二个实例中的第二条进行跳转并且连接后缀名变为html，第一条不能进行跳转。

效果：

![1558939210997](D:\MyNote\images\1558939210997.png)

在向ActionContextMap中放参数时，action里面还可以配置参数，相当于在连接后加参数。name的值是一个字符串，value的值是一个OGNL表达式。实例：

```jsp
<s:url action="action1" var="action">
    <s:param name="name" value="'tom'"></s:param>
</s:url><br/>
```



效果：

![1558941112753](D:\MyNote\images\1558941112753.png)

## 6.16.几种符号的使用

1.#

a.取用contextMap中的key值时使用，如`<s:property value="#name"/>`；

b.OGNL中创建Map对象时使用，如：`<s:radio list="${'male':'男','female':'女'}"/>`

2.$

a.jsp中el表达式的使用，如`${name}`;

b.在xml配置文件中，编写OGNL表达式时使用，如struts\.xml中：

${@java.net.URLEncoder.encode(filename)}

3.%

在struts2中，有些标签的value属性取值就是一个OGNL表达式，例如

`<s:property value="OGNL Expression" />`

还有一部分标签，value属性的取值就是普通字 符串，例如`<s:textfield value="username"/>`，如果想把一个普通的字符串强制看成时OGNL，就需要使用%{}把字符串套起来。

例如`<s:textfield value="%{username}"/>`。当然在`<s:property value="%{OGNL Expression}" />`也可以使用，但不会这么用。

## 6.17.令牌token

struts2中的令牌可以防止表单的重复提交。

使用它需要在2个地方进行配置，一个是struts.xml，一个是jsp中。

struts.xml：

```xml
<action name="login" class="com.itheima.web.action.TokenAction">
    <interceptor-ref name="defaultStack"></interceptor-ref>
    <interceptor-ref name="tokenSession"></interceptor-ref>
    <!-- <result>/success.jsp</result> 请求转发不行-->
    <result type="redirect">/success.jsp</result>
    <result name="invalid.token">/resubmit.jsp</result>
</action>
```



页面：

```jsp
<s:form action="login">
    <s:token></s:token>
    <s:textfield name="name" label="姓名"/>
    <s:submit value="提交"/>
</s:form>
```



## 6.18.用户管理案例

### 6.18.1.创建数据库与表

### 6.18.2.创建接口并实现

首先创建service层接口，然后创建dao层接口，实现service层并调用dao层接口，借此实现dao层接口。如果需要用到工具类则添加工具类，需要添加jar包添加jar包

### 6.18.3.进行struts工程的准备

添加struts的基础jar包，添加struts.xml，添加struts的核心过滤器

### 6.18.4.添加页面

将页面添加到webroot下，然后启动服务器测试项目有无问题

### 6.18.5.登录

1.在struts.xml中配置登录的动作;

2.编写登录动作类，继承ActionSupport,实现ModelDriven;

3.修改页面，为页面取值；