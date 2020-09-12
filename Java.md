# 1.加载配置文件的方法

## 1.1.Properties

通过jdk提供的java.util.Properties类。

此类继承自java.util.HashTable，即实现了Map接口，所以，可使用相应的方法来操作属性文件，但不建议使用像put、putAll这两个方法，因为put方法不仅允许存入String类型的value，还可以存入Object类型的。因此java.util.Properties类提供了getProperty()和setProperty()方法来操作属性文件，同时使用store或save(已过时)来保存属性值（把属性值写入.properties配置文件）。在使用之前，还需要加载属性文件，它提供了两个方法：load和loadFromXML。
load有两个方法的重载：load(InputStream inStream)、load(Reader reader)，所以，可根据不同的方式来加载属性文件。

可根据不同的方式来获取InputStream，如：

 1、通过当前类加载器的getResourceAsStream方法获取

```java
InputStream inStream = TestProperties.class.getClassLoader().getResourceAsStream("test.properties");  
```



2、从文件获取

```java
InputStream inStream = new FileInputStream(new File("filePath"));  
```



 3、也是通过类加载器来获取，和第一种一样

```java
InputStream in = ClassLoader.getSystemResourceAsStream("filePath"); 
```



 4、在servlet中，还可以通过context来获取InputStream

```java
InputStream in = context.getResourceAsStream("filePath");  
```



 5、通过URL来获取

```java
URL url = new URL("path");  
InputStream inStream = url.openStream();  
```



### 7.1.2.ResourceBundle

通过java.util.ResourceBundle类来读取，这种方式比使用Properties要方便一些。

 1、通过ResourceBundle.getBundle()静态方法来获取（ResourceBundle是一个抽象类），这种方式来获取properties属性文件不需要加.properties后缀名，只需要文件名即可。

```java
ResourceBundle resource = ResourceBundle.getBundle("com/mmq/test");
//test为属性文件名，放在包com.mmq下，如果是放在src下，直接用test即可  
String key = resource.getString("username");  
```



 2、从InputStream中读取，获取InputStream的方法和上面一样，不再赘述。

```java
ResourceBundle resource = new PropertyResourceBundle(inStream);  
```



 注意：在使用中遇到的最大的问题可能是配置文件的路径问题，如果配置文件入在当前类所在的包下，那么需要使用包名限定，如：test.properties入在com.mmq包下，则要使用com/mmq/test.properties（通过Properties来获取）或com/mmq/test（通过ResourceBundle来获取）；属性文件在src根目录下，则直接使用test.properties或test即可。

文件配置如下：

![properties](D:\MyNote\images\properties.png)

# a.string

## 1.indexOf()

indexOf() 方法有以下四种形式：

public int indexOf(int ch): 返回指定字符在字符串中第一次出现处的索引，如果此字符串中没有这样的字符，则返回 -1。

public int indexOf(int ch, int fromIndex): 返回从 fromIndex 位置开始查找指定字符在字符串中第一次出现处的索引，如果此字符串中没有这样的字符，则返回 -1。

int indexOf(String str): 返回指定字符在字符串中第一次出现处的索引，如果此字符串中没有这样的字符，则返回 -1。

int indexOf(String str, int fromIndex): 返回从 fromIndex 位置开始查找指定字符在字符串中第一次出现处的索引，如果此字符串中没有这样的字符，则返回 -1。

```java

public class Test {
	public static void main(String[] args) {
		String Str = new String("hello,this is a test");
        String SubStr1 = new String("is");
        String SubStr2 = new String("test");
 
        System.out.print("查找字符i 第一次出现的位置 :" );
        System.out.println(Str.indexOf( 'i' ));
        System.out.print("从第10个位置查找字符 s 第一次出现的位置 :" );
        System.out.println(Str.indexOf( 's', 10 ));
        System.out.print("子字符串 SubStr1 第一次出现的位置:" );
        System.out.println( Str.indexOf( SubStr1 ));
        System.out.print("从第十五个位置开始搜索子字符串 SubStr1 第一次出现的位置 :" );
        System.out.println( Str.indexOf( SubStr1, 11 ));
        System.out.print("子字符串 SubStr2 第一次出现的位置 :" );
        System.out.println(Str.indexOf( SubStr2 ));
	}
```



运行结果如下：

 ![img](D:\MyNote\images\20180808093551523.jpg) 

##  2.subString()

 **1.通过subString()方法来进行字符串截取。** 
subString通过不同的参数来提供不同的截取方式 
1.1只传一个参数, 将字符串从索引号为2开始截取，一直到字符串末尾。（索引值从0开始）；  

```java
String sb = "bbbdsajjds";
sb.substring(2);
//结果：bdsajjds
```



 1.2传入2个索引值, 从索引号2开始到索引好4结束（并且不包含索引4截取在内，也就是说实际截取的是2和3号字符）；  

```java
String sb = "bbbdsajjds";
sb.substring(2, 4);
//结果：bd
```



