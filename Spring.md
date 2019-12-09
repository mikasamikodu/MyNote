# 1.组件注册

## 1.1.@Configuration

@Configuration告诉spring这是一个配置类，相当于配置文件。

```java
@Configuration
public class Configurations {}
```



## 1.2.@Bean

@Bean向ioc容器注册一个Bean，类型为返回值类型，id默认为方法名。

```java
@Bean
public Person person1() {
    return new Person("rose", 15);
}
```

**修改id**有两种方法：一是修改方法名，二是`@Bean("person2")`,这样id就修改为person2了。

@Bean("person2")还可以写成@Bean(value="person2")，@Bean(name="person2")

**在测试类获取bean**：

```java
AnnotationConfigApplicationContext context = 
    new AnnotationConfigApplicationContext(Configurations.class);
@org.junit.Test
public void test02() {
    Person person = (Person)context.getBean("person1");
}	
```



AnnotationConfigApplicationContext是通过注解获取配置文件的类。

**注**：除了@Bean可以向容器注册组件，还有@Service,@Repository,@Controller,@Component这几个注解

### 1.2.1.@Scope

值：singleton(单例模式)，prototype(多例模式)，request(同一次请求一个实例),session(同一个session中创建一个实例)

```java
@Scope("prototype")
@Bean
public Person person() {
    System.out.println("创建bean");
    return new Person("rose", 15);
}
```

**注**：bean是默认单例的bean。单例bean默认ioc容器启动是就实例化加入ioc容器，多例的则是在创建的时候才会实例化；

### 1.2.2.@Lazy

单例bean默认ioc容器启动是就实例化加入ioc容器，多例的则是在创建的时候才会实例化；
如果对单例bean使用@Lazy注解则单例bean也可以只在创建时实例化;

```java
@Lazy//单例bean默认ioc容器启动是就实例化加入ioc容器，多例的则是在创建的时候才会实例化；
//如果对单例bean使用@Lazy注解则单例bean也可以只在创建时实例化;
@Bean(name="person2")
public Person person1() {
    return new Person("rose", 15);
}
```



## 1.3.@ComponentScan

@ComponentScan用于指定扫描的包

```java
@ComponentScan(value="com.atguigu")
public class Configurations {}
```



value用于指定需要扫描的包，basePackages是它的别名，作用相同

Filter[] includeFilters():用于指定将哪些bean加入容器，值为实现接口TypeFilter的类

Filter[] excludeFilters():用于指定将哪些bean不加入容器，值为实现接口TypeFilter的类

useDefaultFilters：是否使用默认的Filter，默认为true

```java
public class MyFilter implements TypeFilter {
	@Override
	@SuppressWarnings("unused")
	public boolean match(MetadataReader metadataReader, MetadataReaderFactory metadataReaderFactory)
			throws IOException {
		//获取当前注解元信息
		AnnotationMetadata metadata = metadataReader.getAnnotationMetadata();
		//读取当前正在扫描的类信息
		ClassMetadata classMetadata = metadataReader.getClassMetadata();
		//返回类文件的路径
		Resource resource = metadataReader.getResource();
		String name = classMetadata.getClassName();
		//System.out.println("--->"+name);
		if(name.contains("dao")) {
			return true;
		}
		return false;
	}
}
```



Filter属性：

​	type的值:定义按照什么规则过滤bean，

​			FilterType.ANNOTATION(默认值，按照注解过滤),FilterType.ASSIGNABLE_TYPE(按照的类型过滤),

​			FilterType.ASPECTJ(按照ASPECTJ表达式过滤),FilterType.REGEX(按照正则表达式过),

​			FilterType.CUSTOM(按照自定义模式过滤)

​	value的值：是需要过滤的bean或需要匹配的规则bean

```java
@ComponentScan(value="com.atguigu",includeFilters = {
		@Filter (type=FilterType.CUSTOM,value=MyFilter.class)
}, useDefaultFilters=false)//按照MyFilter的规则过滤bean加入容器
@ComponentScan(value="com.atguigu",includeFilters = {
    @Filter (type=FilterType.ANNOTATION,value={Controller.class})
})//只将标注有@Controller注解的类加入ioc容器
```

MyFilter.java

```java
public class MyFilter implements TypeFilter {
	@Override
	public boolean match(MetadataReader metadataReader, MetadataReaderFactory metadataReaderFactory)
			throws IOException {
		//获取当前注解元信息
		AnnotationMetadata metadata = metadataReader.getAnnotationMetadata();
		//读取当前正在扫描的类信息
		ClassMetadata classMetadata = metadataReader.getClassMetadata();
		//返回类文件的路径
		Resource resource = metadataReader.getResource();
		String name = classMetadata.getClassName();
		//System.out.println("--->"+name);
		if(name.contains("dao")) {
			return true;
		}
		return false;
	}
}
```



**注1**：这个@ComponentScan可以写多个，即@@ComponentScans注解相同，这个注解内可以写多个@ComponentScan

**注2**：当多个filter同时存在时，按顺序执行

## 1.4.@Conditional

使用方式：

```java
@Conditional({WindowsCondition.class})
@Bean
public Person bill() {
    return new Person("Bill Gates", 63);
}
```



加载方法上满足条件WindowsCondition则可以生成bean。

WindowsCondition.java:

```java
import org.springframework.beans.factory.config.ConfigurableListableBeanFactory;
import org.springframework.beans.factory.support.BeanDefinitionRegistry;
import org.springframework.context.annotation.Condition;
import org.springframework.context.annotation.ConditionContext;
import org.springframework.core.env.Environment;
import org.springframework.core.type.AnnotatedTypeMetadata;

public class WindowsCondition implements Condition {
	@SuppressWarnings("unused")
	@Override
	public boolean matches(ConditionContext context, AnnotatedTypeMetadata metadata) {
		//判断是否是Windows系统
		//获取ioc使用的beanFactory
		ConfigurableListableBeanFactory beanFactory = context.getBeanFactory();
		//获取类加载器
		ClassLoader classLoader = context.getClassLoader();
		//获取bean定义的注册类
		BeanDefinitionRegistry registry = context.getRegistry();
		//获取当时环境变量
		Environment environment = context.getEnvironment();
		String property = environment.getProperty("os.name");
		if(property.contains("Windows")) {
			return true;
		}
		return false;
	}
}
```



## 1.5.组件注册方式

向ioc容器加入组件的方式
1)包扫描和注解标注（@Controller/@Repository/@Service/@Component），适合用在自己写的类上。 
2)@Bean导入第三方包组件，适合用来导入第三方包。
3)@Import(快速向容器中导入一个组件)
	1>可将bean直接加入容器。
		@Import({Color.class})
	2>实现ImportSelector接口，实现接口的方法返回导入组件的全类名，可将这个组件加入ioc容器
		@Import({MyImportSelector.class})
	3>实现ImportBeanDefinitionRegistrar接口，实现内部方法可手动注册bean到ioc容器
		@Import({MyImportBeanDefinitionRegistrar.class})
	4)实现FactoryBean接口，将需要注入的类在getObject()方法返回，将需要注入的类的类型在getObjectType()方法返回，然后将这个工厂类注入ioc容器即可。
		1>使用context.getBean(beanName)方法取出bean时会返回需要注入的那个bean，
		2>若想返回工厂类本身，context.getBean(beanName),只需在beanName前加&即可。

### 1.5.1@Import

@Import可将bean直接加入容器。

@Import({Color.class})：向ioc容器注入Color这个类

```java
@Import({Color.class})
@Configuration
public class Configurations {}
```



### 1.5.2.ImportSelector接口

实现ImportSelector接口，实现接口的方法返回导入组件的全类名，可将这个组件加入ioc容器

@Import({MyImportSelector.class}):向ioc容器中加入Blue这个类

```java
@Import({MyImportSelector.class})
@Configuration
public class Configurations {}
```



MyImportSelector.java

```java
import org.springframework.context.annotation.ImportSelector;
import org.springframework.core.type.AnnotationMetadata;
public class MyImportSelector implements ImportSelector {
	@Override
	public String[] selectImports(AnnotationMetadata importingClassMetadata) {
		//importingClassMetadata可以拿到配置类中注解的所有bean	
        //方法不可以返回null值(会出现异常)，但可以返回{}空数组。
		return new String[] {"com.atguigu.bean.Blue"};
	}
}
```



### 1.5.3.ImportBeanDefinitionRegistrar接口

实现ImportBeanDefinitionRegistrar接口，实现内部方法可手动注册bean到ioc容器

@Import({MyImportBeanDefinitionRegistrar.class})：向容器注入Red这个类

```java
@Import({MyImportBeanDefinitionRegistrar.class})
@Configuration
public class Configurations {}
```



MyImportBeanDefinitionRegistrar.java:

```java
import org.springframework.beans.factory.support.BeanDefinitionRegistry;
import org.springframework.beans.factory.support.RootBeanDefinition;
import org.springframework.context.annotation.ImportBeanDefinitionRegistrar;
import org.springframework.core.type.AnnotationMetadata;
import com.atguigu.bean.Red;
public class MyImportBeanDefinitionRegistrar implements ImportBeanDefinitionRegistrar {
	/*
	 * importingClassMetadata是当前类的注解信息
	 * BeanDefinitionRegistry:BeanDefinition的注册类
	 * 		注册需要加入容器的bean时调用registry.registerBeanDefinition()
	 * */
    @Override
	public void registerBeanDefinitions(AnnotationMetadata importingClassMetadata, BeanDefinitionRegistry registry) {
		boolean flag = registry.containsBeanDefinition("com.atguigu.bean.Blue");
		if(flag) {
			RootBeanDefinition red = new RootBeanDefinition(Red.class);
			registry.registerBeanDefinition("red", red);
		}
	}
}
```



### 1.5.4.FactoryBean接口

实现FactoryBean接口，将需要注入的类在getObject()方法返回，将需要注入的类的类型在getObjectType()方法返回，然后将这个工厂类注入ioc容器即可。

+ 使用context.getBean(beanName)方法取出bean时会返回需要注入的那个bean
+ 若想返回工厂类本身，context.getBean(beanName),只需在beanName前加&即可。

```java
@Bean
public MyFactoryBean myFactoryBean() {
    return new MyFactoryBean();
}
```



MyFactoryBean.java

```java
import org.springframework.beans.factory.FactoryBean;
public class MyFactoryBean implements FactoryBean<Color> {
	@Override
	public Color getObject() throws Exception {
		return new Color();
	}
	@Override
	public Class<?> getObjectType() {
		return Color.class;
	}
	@Override
	public boolean isSingleton() {
		return true;
	}
}
```



test.java:

```java
@org.junit.Test
	public void test04() {
		String[] names = context.getBeanDefinitionNames();
		for(String name:names) {
			System.out.println(name);
		}//输出的bean包含Color这个类
		Object bean = context.getBean("myFactoryBean");
		Object bean3 = context.getBean("myFactoryBean");
		System.out.println(bean.getClass());//输出结果为class com.atguigu.bean.Color
		System.out.println(bean==bean3);//结果为true,单例bean
		Object bean2 = context.getBean("&myFactoryBean");
		System.out.println(bean2.getClass());//class com.atguigu.bean.MyFactoryBean
	}
```



# 2.生命周期

使用@Bean创建对象，会经历创建--初始化--销毁的过程

1.@initMethod和@destroyMethod

+ 使用@initMethod指定初始化时执行的方法	
  + 创建单实例时，会在容器创建时创建bean
  + 建多实例时，会在容器创建时创建bean，而是在调用这个bean时创建bean

 * 使用@destroyMethod指定销毁时执行的方法

   + 创建单实例时，会在容器销毁时销毁bean

   + 创建多实例时，不会在容器销毁时销毁bean

2.接口InitializingBean和接口DisposableBean

+ 通过实现接口InitializingBean中的afterPropertiesSet()来定义初始化逻辑

 * 	     通过实现接口DisposableBean中的destroy()来定义销毁逻辑

3.@PostConstruct和@PreDestroy

+ @PostConstruct在bean创建完成并属性赋值完成，然后执行初始化方法

 * 	  @PreDestroy在容器销毁之前通知我们进行清理工作

## 2.1.@initMethod和@destroyMethod

+ 使用@initMethod指定初始化时执行的方法	
  + 创建单实例时，会在容器创建时创建bean
  + 建多实例时，会在容器创建时创建bean，而是在调用这个bean时创建bean

 * 使用@destroyMethod指定销毁时执行的方法

   + 创建单实例时，会在容器销毁时销毁bean

   + 创建多实例时，不会在容器销毁时销毁bean

```java
@Configuration
public class Configurations {
    @Bean(initMethod="init",destroyMethod="destory")
    public MyInit myInit() {
        return new MyInit();
    }
}
```



MyInit.java:

```java
public class MyInit {
	public MyInit() {
		System.out.println("MyInit创建了");
	}	
	public void init() {
		System.out.println("MyInit初始化了");
	}	
	public void destory() {
		System.out.println("MyInit销毁了");
	}
}
```



## 2.2.InitializingBean和DisposableBean

+ 通过实现接口InitializingBean中的afterPropertiesSet()来定义初始化逻辑

 * 	通过实现接口DisposableBean中的destroy()来定义销毁逻辑

```java
@Configuration
public class Configurations {
    @Bean
	public MyInitializingBean myInitializingBean() {
		return new MyInitializingBean();
	}
}
```



MyInitializingBean.java:

```java
import org.springframework.beans.factory.DisposableBean;
import org.springframework.beans.factory.InitializingBean;
public class MyInitializingBean implements InitializingBean,DisposableBean{
	public MyInitializingBean() {
		System.out.println("MyInitializingBean创建了");
	}
	@Override
	public void destroy() throws Exception {
		System.out.println("MyInitializingBean销毁了");
	}
	@Override
	public void afterPropertiesSet() throws Exception {
		System.out.println("MyInitializingBean配置了参数，初始化了");
	}
}
```



## 2.3.@PostConstruct和@PreDestroy

+ @PostConstruct在bean创建完成并属性赋值完成，然后执行初始化方法

 * 	@PreDestroy在容器销毁之前通知我们进行清理工作

```java
@Configuration
public class Configurations {
    @Bean
	public MyPostConstruct myPostConstruct() {
		return new MyPostConstruct();
	}
}
```



MyPostConstruct.java:

```java
import javax.annotation.PostConstruct;
import javax.annotation.PreDestroy;
public class MyPostConstruct {
	public MyPostConstruct() {
		System.out.println("MyPostConstruct创建了");
	}	
	@PostConstruct
	public void init() {
		System.out.println("MyPostConstruct初始化了");
	}	
	@PreDestroy
	public void destory() {
		System.out.println("MyPostConstruct销毁了");
	}
}
```



## 2.4.BeanPostProcessor

实现BeanPostProcessor接口：bean的后置处理器

在bean初始化前后做一些处理

+ postProcessBeforeInitialization:在初始化前做点处理
+ postProcessAfterInitialization:在初始化后做点处理

```java
@Configuration
public class Configurations {
    @Bean
	public MyBeanPostProcessor myBeanPostProcessor() {
		return new MyBeanPostProcessor();
	}
}
```



MyBeanPostProcessor.java:

```java
import org.springframework.beans.BeansException;
import org.springframework.beans.factory.config.BeanPostProcessor;
import org.springframework.stereotype.Component;
public class MyBeanPostProcessor implements BeanPostProcessor {
	@Override
	public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
		System.out.println("Before,class..."+beanName+"初始化了，=>>"+bean);
		return bean;
	}
	@Override
	public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
		System.out.println("After,class..."+beanName+"初始化了，=>>"+bean);
		return bean;
	}
}
```



运行测试类结果：

```java
Before,class...myInitializingBean初始化了，=>>com.atguigu.bean.MyInitializingBean@3bbc39f8
MyInitializingBean配置了参数，初始化了
After,class...myInitializingBean初始化了，=>>com.atguigu.bean.MyInitializingBean@3bbc39f8
MyInitializingBean销毁了
```



