## 1.基础知识

### 1.1.windows系统常用命令

+ md ： 创建文件夹
+ rd ： 删除文件夹
+ cd ： 到某个目录。如`cd ..`是到上一级目录，`cd /`是到根目录,使用时需要先在命令行输入需要去的盘符，如d盘就输入`d:`回车，之后输入`cd 需要去的目录`回车即可
+ notepad ： 打开记事本
+ regedt32 、 regedit： 打开注册表编辑器
+ ipconfig ： 查看网络连接信息
+ dir ： 列出目录下文件和文件夹
+ del ： 删除文件
+ exit ： 退出doc命令行

### 1.2.java特性

+ 三大特性 ： 封装、继承、多态

+ 健壮性

+ 跨平台性

+ java两大核心机制 ：

    +  Java虚拟机 ：

        + JVM是一个虚拟的计算机，具有指令集并使用不同的存储区域。负责执行指

            令，管理数据、内存、寄存器。

        + 对于不同的平台，有不同的虚拟机。 

        + 只有某平台提供了对应的java虚拟机，java程序才可在此平台运行

        + Java虚拟机机制屏蔽了底层运行平台的差别，实现了“一次编译，到处运行”

    + 垃圾收集机制

        + 不再使用的内存空间应回收—— 垃圾回收

            + 在C/C++等语言中，由程序员负责回收无用内存。

            + Java 语言消除了程序员回收无用内存空间的责任：它提供一种系统级线程跟踪存储空 

                间的分配情况。并在JVM空闲时，检查并释放那些可被释放的存储空间。

        + 垃圾回收在Java程序运行过程中自动进行，程序员无法精确控制和干预

### 1.3.搭建环境

+ **JDK** ： Java开发工具包，JDK是提供给Java开发人员使用的，其中包含了java的开发工具，也包括了 

    JRE。所以安装了JDK，就不用在单独安装JRE了。其中的开发工具包含编译工具(javac.exe) 和打包工具(jar.exe)等

+ **JRE** ： Java运行环境，包括Java虚拟机(JVM Java Virtual Machine)和Java程序所需的核心类库等， 

    如果想要**运行**一个开发好的Java程序，计算机中只需要安装JRE即可。

+ java官方网址 : www.oracle.com  、 java.sun.com 

+ 安装jdk步骤：

    + 傻瓜式安装，下一步即可。 

    + 建议：安装路径不要有中文或者空格等特殊符号。

    + 如果操作系统是64位的，软件尽量选择支持64位的（除非软件本身不区分）。 

    + 当提示安装 JRE 时，正常在JDK安装时已经装过了，但是为了后续使用Eclipse等开发 

        工具不报错，建议也根据提示安装JRE。

+ 配置环境变量 

    + 首先打开我的电脑--属性--高级系统设置--环境变量
    + 配置JAVA_HOME：
        +  C:\Program Files (x86)\Java\jdk1.8.0_91     // 要根据自己的实际jdk安装路径配置 
    + 配置PATH：
        +  %JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;
    + 配置CLASSPATH：
        + .;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;    //记得前面有个"." 

+ 测试安装是否成功 ： 打开cmd，输入`java -version`，出现java安装版本就是成功了

![D](D:\MyNote\images\安装方法.png)

+ java初体验 ： 

    + 打开记事本

    + 输入`class Test{ } `，然后将文件保存成Test.java，这个文件是存放java代码的文件， 称为源文件

    + 修改里面内容，并保存

        ```java
        public class Test{ 
        	public static void main(String[] args) { 
        		System.out.println(“Hello World!”); 
        	} 
        }
        ```

        

    + 打开cmd，输入`javac Test.java`回车，之后在当前目录下会出现一个Test.class文 件，该文件称为字节码文件，也是可以执行的java的程序

    + 输入`java Test` 回车。cmd会输出Hello World!

**注意**：

+ Java语言严格区分大小写。
+ Java源文件以“java”为扩展名。源文件的基本组成部分是类（class），如本例中的HelloWorld类。
+ Java应用程序的执行入口是main()方法。它有固定的书写格式：`public static void main(String[] args)  {...}`
+ Java方法由一条条语句构成，每个语句以英文分号结尾
+ 大括号都是成对出现的，缺一不可。
+ 一个源文件中最多只能有一个public类。其它类的个数不限，如果源文件包含一个public类，则文件名必须按该类名命名。

### 1.4.注释

+ 用于注解说明解释程序的文字就是注释。 
+ Java中的注释类型： 
    + 单行注释 : 案例`//注释文字`，被注释的文字，不会被JVM（java虚拟机）解释执行。 
    + 多行注释 ： 案例`/* 注释文字 */`，被注释的文字，不会被JVM（java虚拟机）解释执行。 多行注释里面不允许有多行注释嵌套。 
    + 文档注释 (java特有) ： 案例`/* 内容 **/`，注释内容可以被JDK提供的工具 javadoc 所解析，生成一套以网页文件形式体现的该程序的说明文档。 
+ 提高了代码的阅读性；调试程序的重要方法。 

### 1.5.api文档

+ API （Application Programming Interface,应用程序编程接口）是Java 提供的基本编程接口
+ Java语言提供了大量的基础类，因此Oracle 也为这些基础类提供了相应的API文档，用于告诉开发者如何使用这些类，以及这些类里包含的方法。
+ 下载API：http://www.oracle.com/technetwork/java/javase/downloads/index.html

### 1.6.常用开发工具

+ 入门： 记事本(notepad)、notepad++
+ 进阶： Eclipse
+ 熟练、常用、推荐： IntelliJ IDEA

## 2.基础语法

### 2.1.关键字与保留字

+ 关键字(keyword)的定义和特点:
  + 定义：被Java语言赋予了特殊含义，用做专门用途的字符串（单词）
  + 特点：关键字中所有字母都为小写

| 用于定义数据类型的关键字                         |            |           |              |          |
| ------------------------------------------------ | ---------- | --------- | ------------ | -------- |
| class                                            | interface  | enum      | byte         | short    |
| int                                              | long       | double    | float        | char     |
| boolean                                          | void       |           |              |          |
| **用于定义流程控制的关键字**                     |            |           |              |          |
| if                                               | else       | switch    | case         | default  |
| while                                            | do         | for       | break        | continue |
| return                                           |            |           |              |          |
| **用于定义访问权限修饰符的关键字**               |            |           |              |          |
| public                                           | private    | protected |              |          |
| **用于定义类，函数，变量修饰符的关键字**         |            |           |              |          |
| abstact                                          | final      | static    | synchronized |          |
| **用于定义类与类之间关系的关键字**               |            |           |              |          |
| extends                                          | implements |           |              |          |
| **用于定义建立实例及引用实例，判断实例的关键字** |            |           |              |          |
| new                                              | this       | super     | instanceof   |          |
| **用于异常处理的关键字**                         |            |           |              |          |
| try                                              | catch      | finally   | throw        | throws   |
| **用于包的关键字**                               |            |           |              |          |
| package                                          | import     |           |              |          |
| **其他修饰符关键字**                             |            |           |              |          |
| native                                           | strictfp   | transient | volatile     | assert   |
| **用于定义数据类型值的字面值**                   |            |           |              |          |
| true                                             | false      | null      |              |          |

+ Java保留字 ： 现有Java版本尚未使用，但以后版本可能会作为关键字使用。自己命名标识符时要避免使用这些保留字，如下：goto 、const

### 2.2.标识符

+ Java 对各种**变量**、**方法**和**类**等要素命名时使用的字符序列称为标识符
+ 技巧：凡是自己可以起名字的地方都叫标识符
+ 定义合法**标识符**规则： 
  + 由26个英文字母大小写，0-9，_或 $组成
  + 数字不可以开头
  + 不可以使用关键字和保留字，但能包含关键字和保留字
  + Java中严格区分大小写，长度无限制
  + 标识符不能包含空格
+ Java中的**名称**命名规范：
  + **包名**：多单词组成时所有字母都小写：xxxyyyzzz
  + **类名、接口名**：多单词组成时，所有单词的首字母大写：XxxYyyZzz
  + **变量名、方法名**：多单词组成时，第一个单词首字母小写，第二个单词开始每个单词首字母大写xxYyyZzz
  + **常量名**：所有字母都大写。多单词时每个单词用下划线连接：XXX_YYY_ZZZ
+ **注意1**：在起名字时，为了提高阅读性，要尽量有意义，“见名知意”。
+ **注意2**：java采用unicode字符集，因此标识符也可以使用汉字声明，但是不建议使用。 

### 2.3.变量

+ **概念：** 
  + 内存中的一个存储区域 
  + 该区域的数据可以在同一类型范围内不断变化
  + 变量是程序中最基本的存储单元。包含变量类型、变量名和存储的值
+ **作用：** 用于在内存中保存数据
+ **注意：** 
  + Java中每个变量必须先声明，后使用 
  + 使用变量名来访问这块区域的数据 
  + 变量的作用域：其定义所在的一对{ }内 
  + 变量只有在其作用域内才有效 
  + 同一个作用域内，不能定义重名的变量
+ **声明变量** ： 语法：<数据类型> <变量名称>，例如：`int var;`
+ **变量的赋值** ： <变量名称> = <值>，例如：`var = 10;`

#### 2.3.1.变量的分类

+ 按数据类型分类，每种在内存中分配了不同大小的内存空间。

  ![1676781302223](D:\MyNote\images\1676781302223.png)

+ 整数类型：

  + Java各整数类型有固定的表数范围和字段长度，不受具体OS的影响，以保证java程序的可移植性。
  + java的整型常量默认为 int 型，声明long型常量须后加‘l’或‘L
  + java程序中变量通常声明为int型，除非不足以表示较大的数，才使用long 

  ![1676781564167](D:\MyNote\images\1676781564167.png)

+ 浮点类型：

  + 与整数类型类似，Java 浮点类型也有固定的表数范围和字段长度，不受具体操作系统的影响。
  + 浮点型常量有两种表示形式：
    + 十进制数形式：如：5.12   512.0f   .512 (必须有小数点）
    + 科学计数法形式:如：5.12e2  512E2 100E-2
    + float:单精度，尾数可以精确到7位有效数字。很多情况下，精度很难满足需求。double:双精度，精度是float的两倍。通常采用此类型
    + Java的浮点型常量默认为double型，声明float型常量，须后加‘f’或‘F’

  ![1676781894563](D:\MyNote\images\1676781894563.png)

+ 字符类型 ： 

  + char 型数据用来表示通常意义上“字符”(2字节)
  + Java中的所有字符都使用Unicode编码，故一个字符可以存储一个字母，一个汉字，或其他书面语的一个字符
  + 字符型变量的三种表现形式： 
    + 字符常量是用单引号(‘ ’)括起来的单个字符。例如：char c1 = 'a'; char c2 = '中'; char c3 = '9';
    + Java中还允许使用转义字符‘\’来将其后的字符转变为特殊字符型常量。例如：char c3 = ‘\n’; // '\n'表示换行符
    + 直接使用 Unicode 值来表示字符型常量：‘\uXXXX’。其中，XXXX代表一个十六进制整数。如：\u000a 表示 \n。 
  + char类型是可以进行运算的。因为它都对应有Unicode码。 

+ 布尔类型 ：

  + boolean 类型用来判断逻辑条件，一般用于程序流程控制： 
    + if条件控制语句； 
    + while循环控制语句； 
    + do-while循环控制语句； 
    + for循环控制语句；
  + boolean类型数据只允许取值true和false，无null。 
    + 不可以使用0或非 0 的整数替代false和true，这点和C语言不同
    + Java虚拟机中没有任何供boolean值专用的字节码指令，Java语言表达所操作的boolean值，在编译之后都使用java虚拟机中的int数据类型来代替：true用1表示，false用0表示。  ———《java虚拟机规范 8版》

+ 字符串类型：

  + String不是基本数据类型，属于引用数据类型

  + 使用方式与基本数据类型一致。例如：String str = “abcd”;

  + 一个字符串可以串接另一个字符串，也可以直接串接其他类型的数据。例如：

    `str = str + “xyz” ; ` 

    `int n = 100;`

     `str = str + n;`

  

+ 基本数据类型转换：

  + **自动类型转换**：容量小的类型自动转换为容量大的数据类型。数据类型按容量大小排序为：

    ![1676782406316](D:\MyNote\images\1676782406316.png)

  + 有多种类型的数据混合运算时，系统首先自动将所有数据转换成容量最大的那种数据类型，然后再进行计算

  + byte,short,char之间不会相互转换，他们三者在计算时首先转换为int类型。 

  + boolean类型不能与其它数据类型运算

  + 当把任何基本数据类型的值和字符串(String)进行连接运算时(+)，基本数据类型的值将自动转化为字符串(String)类型

+ 强制类型转换 ： 

  + 自动类型转换的逆过程，将容量大的数据类型转换为容量小的数据类型。使用时要加上强制转换符：()，但可能造成精度降低或溢出,格外要注意。 
  + 通常，字符串不能直接转换为基本类型，但通过基本类型对应的包装类则可以实现把字符串转换成基本类型。如： String a = “43”; int i = Integer.parseInt(a); 
  + boolean类型不可以转换为其它的数据类型。

+ 按声明的位置，在方法体外，类体内声明的变量称为成员变量；在方法体内部声明的变量称为局部变量。

  + 二者都是有生命周期的，局部变量除形参外，需显式初始化

![1676781346746](D:\MyNote\images\1676781346746.png)

```java
 public class VariableTest {
 public static void main(String[] args) {
 int number1;
 number1 = 10;
 
 int number2;
 number2 = 20;
 
 int number3;
 number3 = number1 + number2;
 System.out.println("Number3 = " + number3);
 
 int number4 = 50;
 int number5 = number4 - number3;
 System.out.println("Number5 = " + number5);
 }
 }
```



### 2.4.进制

+ 所有数字在计算机底层都以**二进制**形式存在。 

+ 对于整数，有四种表示方式：

  + 二进制(binary)：0,1 ，满2进1.以0b或0B开头。 

  + 十进制(decimal)：0-9 ，满10进1。 

  + 八进制(octal)：0-7 ，满8进1. 以数字0开头表示。 

  + 十六进制(hex)：0-9及A-F，满16进1. 以0x或0X开头表示。此处的A-F不区分大小写。 

    如：0x21AF +1= 0X21B0

| 十进制      | 十六进制    | 八进制     | 二进制 |
| ----------- | ----------- | ---------- | ------ |
| 0           | 0           | 0          | 0      |
| 1           | 1           | 1          | 1      |
| 2           | 2           | 2          | 10     |
| 3           | 3           | 3          | 11     |
| 4           | 4           | 4          | 100    |
| 5           | 5           | 5          | 101    |
| 6           | 6           | 6          | 110    |
| 7           | 7           | 7          | 111    |
| 8           | 8           | 10(满8进1) | 1000   |
| 9           | 9           | 11         | 1001   |
| 10(满10进1) | A           | 12         | 1010   |
| 11          | B           | 13         | 1011   |
| 12          | C           | 14         | 1100   |
| 13          | D           | 15         | 1101   |
| 14          | E           | 16         | 1110   |
| 15          | F           | 17         | 1111   |
| 16          | 10(满16进1) | 20         | 10000  |
| 17          | 11          | 21         | 10001  |



+ **二进制** ： 
  + Java整数常量默认是int类型，当用二进制定义整数时，其第32位是符号位；当是long类型时，二进制默认占64位，第64位是符号位
  + 二进制的整数有如下三种形式：
    + 原码：直接将一个数值换成二进制数。最高位是符号位 
    + 负数的反码：是对原码按位取反，只是最高位（符号位）确定为1。 
    + 负数的补码：其反码加1。 
  + 计算机以二进制补码的形式保存所有的整数。 
    + 正数的原码、反码、补码都相同
    + 负数的补码是其反码+1

### 2.5.运算符

运算符是一种特殊的符号，用以表示数据的运算、赋值和比较等

+ 算术运算符 

  + 如果对负数取模，可以把模数负号忽略不记，如：5%-2=1。 但被模数是负数则不可忽略。此外，取模运算的结果不一定总是整数。 
  + 对于除号“/”，它的整数除和小数除是有区别的：整数之间做除法时，只保留整数部分而舍弃小数部分。 例如：int x=3510;x=x/1000*1000; x的结果是？
  + “+”除字符串相加功能外，还能把非字符串转换成字符串.例如：System.out.println(“5+5=”+5+5); //打印结果是5+5=55 

  ![1676783607880](D:\MyNote\images\1676783607880.png)

  

+ 赋值运算符 

  + 符号：= 
    + 当“=”两侧数据类型不一致时，可以使用自动类型转换或使用强制类型转换原则进行处理。
    + 支持连续赋值

  + 扩展赋值运算符： += , -=, *=, /=, %=

+ 比较运算符（关系运算符） 

  + 比较运算符的结果都是boolean型，也就是要么是true，要么是false
  + 比较运算符“==”不能误写成“=”

![1676783988838](D:\MyNote\images\1676783988838.png)

+ 逻辑运算符 

  + &—逻辑与 

  + | —逻辑或 

  + ！—逻辑非 

  + && —短路与 

  + || —短路或

  + ^ —逻辑异或 

  + 注意 ： 

    + 逻辑运算符用于连接布尔型表达式，在Java中不可以写成3<x<6，应该写成x>3 & x<6 。

    + “&”和“&&”的区别： 

      + 单&时，左边无论真假，右边都进行运算； 
      + 双&时，如果左边为真，右边参与运算，如果左边为假，那么右边不参与运算。

    + “|”和“||”的区别同理，||表示：当左边为真，右边不参与运算。

    + 异或( ^ )与或( | )的不同之处是：当左右都为true时，结果为false。 

      理解：异或，追求的是“异”!

![1676784088015](D:\MyNote\images\1676784088015.png)

+ 位运算符 
  + 位运算是直接对整数的二进制进行的运算

![1676784268021](D:\MyNote\images\1676784268021.png)

![1676784335684](D:\MyNote\images\1676784335684.png)

+ 三元运算符
  +  (条件表达式)?表达式1：表达式2；条件表达式为true，运算后的结果是表达式1；为false，运算后的结果是表达式2； 
  + 表达式1和表达式2为同种类型
  + 三元运算符与if-else的联系与区别： 
    + 三元运算符可简化if-else语句 
    + 三元运算符要求必须返回一个结果。 
    + if后的代码块可有多个语句

### 2.6.程序流程控制

流程控制语句是用来控制程序中各语句执行顺序的语句，可以把语句组合成能完成一定功能的小逻辑模块

其流程控制方式采用结构化程序设计中规定的三种基本流程结构，即：

+ 顺序结构
  + 程序从上到下逐行地执行，中间没有任何判断和跳转
  + Java中定义成员变量时采用合法的前向引用（只有前面定义的变量，后面可以使用）
+ 分支结构
  + 根据条件，选择性地执行某段代码。
  + 有if…else和switch-case两种分支语句。
+ 循环结构
  + 根据循环条件，重复性的执行某段代码。 
  + 有while、do…while、for三种循环语句
  + 注：JDK1.5提供了foreach循环，方便的遍历集合、数组元素

特殊关键字的使用：

+ **break**

  + break语句用于终止某个语句块的执行

    `{ ……
    	break;
    	……
    }`

  + break语句出现在多层嵌套的语句块中时，可以通过标签指明要终止的是哪一层语句块

    `label1: { ……
    label2: 	{ ……
    label3: 		{ ……
    				break label2;
    				……
    				}
    			}
    		}`

```java
public class BreakTest{
    public static void main(String args[]){
        for(int i = 0; i<10; i++){ 
            if(i==3) 
                break;
            System.out.println(" i =" + i);
        }
        System.out.println("Game Over!");
    }
}
```



+ **continue**
  + continue只能使用在循环结构中
  + continue语句用于跳过其所在循环语句块的一次执行，继续下一次循环
  + continue语句出现在多层嵌套的循环语句体中时，可以通过标签指明要跳过的是哪一层循环

```java
public class ContinueTest {
    public static void main(String args[]){
        for (int i = 0; i < 100; i++) {
            if (i%10==0)
            	continue;
            System.out.println(i);
        }
    }
}
```



+  **return**
  + return：并非专门用于结束循环的，它的功能是结束一个方法。 当一个方法执行到一个return语句时，这个方法将被结束。
  + 与break和continue不同的是，return直接结束整个方法，不管这个return处于多少层循环之内
+ **说明** ：
  + break只能用于switch语句和循环语句中。
  + continue 只能用于循环语句中。 
  + 二者功能类似，但continue是终止本次循环，break是终止本层循环。 
  + break、continue之后不能有其他的语句，因为程序永远不会执行其后的语句。 
  + 标号语句必须紧接在循环的头部。标号语句不能用在非循环语句的前面。 
  + 很多语言都有goto语句，goto语句可以随意将控制转移到程序中的任意一条语句上，然后执行它。但使程序容易出错。Java中的break和continue是不同于goto的。

#### 2.6.1.if语句

if语句三种格式

+ 条件表达式必须是布尔表达式（关系表达式或逻辑表达式）、布尔变量 
+ 语句块只有一条执行语句时，一对{}可以省略，但建议保留
+ if-else语句结构，根据需要可以嵌套使用
+ 当if-else结构是“多选一”时，最后的else是可选的，根据需要可以省略
+ 当多个条件是“互斥”关系时，条件判断语句及执行语句间顺序无所谓。当多个条件是“包含”关系时，“小上大下 / 子上父下”

```java
1. if(条件表达式){
	 执行代码块；
	}
2. if(条件表达式){
	 执行代码块1;
   }
   else{
     执行代码块2;
   }
3. if(条件表达式1){
     执行代码块1;
   }
   else if (条件表达式2){
     执行代码块2;
   }
   ……
   else{
     执行代码块n;
   }
案例：
public class AgeTest{
    public static void main(String args[]){
        int age = 75;
        if (age< 0) {
        	System.out.println("不可能！");
        } else if (age>250) {
        	System.out.println("是个妖怪！");
        } else {
        	System.out.println(“人家芳龄 " + age +" ,马马乎乎啦！");
        }
    }
}
```



<img src="D:\MyNote\images\1676785678935.png" alt="1676785678935" style="zoom:50%;" />

左边是第一种情况，右边是第二种情况，下边是第三种情况

<img src="D:\MyNote\images\1676785751164.png" alt="1676785751164" style="zoom:50%;" />

#### 2.6.2.switch-case结构

switch-case结构：

+ switch(表达式)中表达式的值必须是下述几种类型之一：byte，short，char，int，枚举 (jdk 5.0)，String (jdk 7.0)
+ case子句中的值必须是常量，不能是变量名或不确定的表达式值
+ 同一个switch语句，所有case子句中的常量值互不相同
+ break语句用来在执行完一个case分支后使程序跳出switch语句块；如果没有break，程序会顺序执行到switch结尾
+ default子句是**可任选的**。同时，位置也是灵活的。当没有匹配的case时，执行default
+ 如果判断的具体数值不多，而且符合byte、short 、char、int、String、枚举等几种类型。虽然两个语句都可以使用，建议使用swtich语句。因为效率稍高。 
+ 其他情况：对区间判断，对结果为boolean类型判断，使用if，if的使用范围更广。 也就是说，使用switch-case的，都可以改写为if-else。反之不成立。

```java
switch(表达式){
case 常量1:
    语句1;
    // break;
case 常量2:
    语句2;
    // break;
… …
case 常量N:
    语句N;
    // break;
default:
    语句;
    // break;
}
案例1：
public class SwitchTest {
    public static void main(String args[]) {
        int i = 1;
        switch (i) {
            case 0:
                System.out.println("zero");
                break;
            case 1:
                System.out.println("one");
                break;
            default:
            	System.out.println("default");
            	break;
        }
    }
}
案例2：
String season = "summer";
switch (season) {
    case "spring":
        System.out.println("春暖花开");
        break;
    case "summer":
        System.out.println("夏日炎炎");
        break;
    case "autumn":
        System.out.println("秋高气爽");
        break;
    case "winter":
        System.out.println("冬雪皑皑");
        break;
    default:
        System.out.println("季节输入有误");
        break;
}
```



#### 2.6.3.循环结构

+ 在某些条件满足的情况下，反复执行特定代码的功能
+ 有三类循环结构：
  + for 循环
  + while 循环
  + do-while 循环
+ 循环语句的四个组成部分：
  + 初始化部分(init_statement) 
  + 循环条件部分(test_exp) 
  + 循环体部分(body_statement) 
  + 迭代部分(alter_statement) 

<img src="D:\MyNote\images\1676785617976.png" alt="1676785617976" style="zoom:50%;" />

**for循环**：

+ 语法格式：
  + `for (①初始化部分; ②循环条件部分; ④迭代部分)｛
    ③循环体部分;
    ｝`
+ 执行过程是①-②-③-④-②-③-④-②-③-④-.....-② 
+ 说明：
  +  ②循环条件部分为boolean类型表达式，当值为false时，退出循环 
  +  ①初始化部分可以声明多个变量，但必须是同一个类型，用逗号分隔 
  +  ④可以有多个变量更新，用逗号分隔

```java
public class ForLoop {
    public static void main(String args[]) {
        int result = 0;
        for (int i = 1; i <= 100; i++) {
        	result += i;
        }
        System.out.println("result=" + result);
    }
}
```



**while循环**：

+ 语法格式：
  + `①初始化部分
    while(②循环条件部分)｛
    ③循环体部分;
    ④迭代部分;
    }` 
+ 执行过程是①-②-③-④-②-③-④-②-③-④-...-②
  +  注意不要忘记声明④迭代部分。否则，循环将不能结束，变成死循环。 
  +  for循环和while循环可以相互转换

```java
public class WhileLoop {
    public static void main(String args[]) {
        int result = 0;
        int i = 1;
        while (i <= 100) {
            result += i;
            i++;
        }
        System.out.println("result=" + result);
    }
}
```



**do-while循环**：

+ 语法格式：
  + `①初始化部分;
    do{
    ③循环体部分
    ④迭代部分
    }while(②循环条件部分);`
+ 执行过程是①-③-④-②-③-④-②-③-④-...②
+ 说明：do-while循环至少执行一次循环体。

```java
public class DoWhileLoop {
    public static void main(String args[]) {
        int result = 0, i = 1;
        do {
            result += i;
            i++;
        } while (i <= 100);
        System.out.println("result=" + result);
    }
}
```



**嵌套循环结构**：

+ 将一个循环放在另一个循环体内，就形成了嵌套循环。其中，for ,while ,do…while均可以作为外层循环或内层循环。
+ 实质上，嵌套循环就是把内层循环当成外层循环的循环体。当只有内层循环的循环条件为false时，才会完全跳出内层循环，才可结束外层的当次循环，开始下一次的循环。
+ 设外层循环次数为m次，内层为n次，则内层循环体实际上需要执行m*n次。 

## 3.数组

​		数组(Array)，是多个相同类型数据按一定顺序排列的集合，并使用一个名字命名，并通过编号的方式对这些数据进行统一管理。 

数组的常见概念 ：

+  数组名 

+  下标(或索引) 

+  元素 

+  数组的长度

  数组本身是引用数据类型，而数组中的元素可以是任何数据类型，包括基本数据类型和引用数据类型。 

  创建数组对象会在内存中开辟一整块连续的空间，而数组名中引用的是这块连续空间的首地址

  数组的长度一旦确定，就不能修改

  我们可以直接通过下标(或索引)的方式调用指定位置的元素，速度很快

数组的分类:

+ 按照维度：一维数组、二维数组、三维数组...
+ 按照元素的数据类型分：基本数据类型元素的数组、引用数据类型元素的数组(即对象数组)

### 3.1.一维数组

一维数组的声明方式：`type var[] ;`，例如： `int a[];`、`int[] a1;`、`double b[];`、`String[] c;`

Java语言中声明数组时不能指定其长度(数组中元素的数)， 例如： int a[5]; //非法

**动态初始化**：数组声明且为数组元素分配空间与赋值的操作分开进行

```java
String names[];//声明
names = new String[3];//分配空间
names[0] = “钱学森”;//赋值
names[1] = “邓稼先”;
names[2] = “袁隆平”;
```



**静态初始化**：在定义数组的同时就为数组元素分配空间并赋值。

例如： `int arr[] = new int[]{ 3, 9, 8}; `、`int[] arr = {3,9,8};`

定义并用运算符**new**为之分配空间后，才可以引用数组中的每个元素；

数组元素的引用方式：数组名[数组元素下标]

+ 数组元素下标可以是整型常量或整型表达式。如a[3] , b[i] , c[6*i]; 
+ 数组元素下标从0开始；长度为n的数组合法下标取值范围: 0 —>n-1；如int a[]=new int[3]; 可引用的数组元素为a[0]、a[1]、a[2]

每个数组都有一个属性**length**指明它的长度，例如：**a.length** 指明数组**a**的长度(元素个数)，注意数组一旦初始化，其长度是不可变的

数组是引用类型，它的元素相当于类的成员变量，因此数组一经分配空间，其中的每个元素也被按照成员变量同样的方式被隐式初始化。例如： 

```java
public class Test {
    public static void main(String argv[]){
        int a[]= new int[5];
        System.out.println(a[3]); //a[3]的默认值为0
    }
}
```



对于基本数据类型而言，默认初始化值各有不同。对于引用数据类型而言，默认初始化值为null(注意与0不同！)

<img src="D:\MyNote\images\1676803588982.png" alt="1676803588982" style="zoom:50%;" />

### 3.2.多维数组

Java 语言里提供了支持多维数组的语法。

如果说可以把一维数组当成几何中的线性图形，那么二维数组就相当于是一个表格，像右图Excel中的表格一样。 

<img src="D:\MyNote\images\1676803958914.png" alt="1676803958914" style="zoom:43%;" />

对于二维数组的理解，我们可以看成是一维数组array1又作为另一个一维数组array2的元素而存在。其实，从数组底层的运行机制来看，其实没有多维数组。

**二维数组**：数组中的数组

格式1（动态初始化）： `int[][] arr = new int[3][2]`

​		定义了名称为arr的二维数组，二维数组中有3个一维数组，每一个一维数组中有2个元素，一维数组的名称分别为arr[0], arr[1], arr[2]，给第一个一维数组1脚标位赋值为78写法是：arr[0][1] = 78; 

格式2（动态初始化）： `int[][] arr = new int[3][]; `

​		二维数组中有3个一维数组。每个一维数组都是默认初始化值null (注意：区别于格式1）可以对这个三个一维数组分别进行初始化，arr[0] = new int[3]; arr[1] = new int[1]; arr[2] = new int[2]; 

注： `int[][]arr = new int[][3]; //非法`

格式3（静态初始化）： `int[][] arr = new int[][]{{3,8,2},{2,7},{9,0,1,6}};`

​		定义一个名称为arr的二维数组，二维数组中有三个一维数组，每一个一维数组中具体元素也都已初始化，第一个一维数组 arr[0] = {3,8,2}; 第二个一维数组 arr[1] = {2,7}; 第三个一维数组 arr[2] = {9,0,1,6}; 第三个一维数组的长度表示方式：arr[2].length;

**注意**特殊写法情况：int[] x,y[]; x是一维数组，y是二维数组

Java中多维数组不必都是规则矩阵形式

### 3.3.常见算法

+ 数组元素的赋值(杨辉三角、回形数等)
+  求数值型数组中元素的最大值、最小值、平均数、总和等
+ 数组的复制、反转、查找(线性查找、二分法查找)
+ 数组元素的排序算法

**二分法查找算法**：

<img src="D:\MyNote\images\1676805405609.png" alt="1676805405609" style="zoom:50%;" />

```java
//二分法查找：要求此数组必须是有序的。
int[] arr3 = new int[]{-99,-54,-2,0,2,33,43,256,999};
boolean isFlag = true;
int number = 256;
//int number = 25;
int head = 0;//首索引位置
int end = arr3.length - 1;//尾索引位置
while(head <= end){
    int middle = (head + end) / 2;
    if(arr3[middle] == number){
        System.out.println("找到指定的元素，索引为：" + middle);
        isFlag = false;
        break;
    }else if(arr3[middle] > number){
        end = middle - 1;
    }else{//arr3[middle] < number
        head = middle + 1;
    }
}
if(isFlag){
	System.out.println("未找打指定的元素");
}
```



**排序算法**：假设含有n个记录的序列为{R1，R2，...,Rn},其相应的关键字序列为{K1，K2，...,Kn}。将这些记录重新排序为{Ri1,Ri2,...,Rin},使得相应的关键字值满足条Ki1<=Ki2<=...<=Kin,这样的一种操作称为排序。 通常来说，排序的目的是快速查找。 

**衡量排序算法的优劣：**

1.时间复杂度：分析关键字的比较次数和记录的移动次数 

2.空间复杂度：分析排序算法中需要多少辅助内存 

3.稳定性：若两个记录A和B的关键字值相等，但排序后A、B的先后次序保持不变，则称这种排序算法是稳定的

排序算法分类：内部排序和外部排序。

+ 内部排序：整个排序过程不需要借助于外部存储器（如磁盘等），所有排序操作都在内存中完成
+ 外部排序：参与排序的数据非常多，数据量非常大，计算机无法把整个排序过程放在内存中完成，必须借助于外部存储器（如磁盘）。外部排序最常见的是多路归并排序。可以认为外部排序是由多次内部排序组成

**十大内部排序算法**：

+  选择排序
  +  直接选择排序、堆排序 
+  交换排序
  +  冒泡排序、快速排序 
+  插入排序 
  +  直接插入排序、折半插入排序、Shell排序 
+  归并排序 
+  桶式排序 
+  基数排序

算法的5大特征： 

<img src="D:\MyNote\images\1676805917514.png" alt="1676805917514" style="zoom:50%;" />

说明：满足确定性的算法也称为：确定性算法。现在人们也关注更广泛的概念，例如考虑各种非确定性的算法，如并行算法、概率算法等。另外，人们也关注并不要求终止的计算描述，这种描述有时被称为过程（procedure）

**冒泡排序**：

**介绍**： 冒泡排序的原理非常简单，它重复地走访过要排序的数列，一次比较两个元素，如果他们的顺序错误就把他们交换过来。

**排序思想**：

1. 比较相邻的元素。如果第一个比第二个大（升序），就交换他们两个。 

2. 对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对。这步做完后，最后的元素会是最大的数。 

3. 针对所有的元素重复以上的步骤，除了最后一个。 

4. 持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较为止

**快速排序**：

**介绍**： 快速排序通常明显比同为O(nlogn)的其他算法更快，因此常被采用，而且快排采用了分治法的思想，所以在很多笔试面试中能经常看到快排的影子。可见掌握快排的重要性。 

快速排序（Quick Sort）由图灵奖获得者Tony Hoare发明，被列为20世纪十大算法之一，是迄今为止所有内排序算法中速度最快的一种。冒泡排序的升级版，交换排序的一种。快速排序的时间复杂度为O(nlog(n))。

**排序思想**： 

1. 从数列中挑出一个元素，称为"基准"（pivot）， 

2. 重新排序数列，所有元素比基准值小的摆放在基准前面，所有元素比基准值大的摆在基准的后面（相同的数可以到任一边）。在这个分区结束之后，该基准就处于数列的中间位置。这个称为分区（partition）操作。 

3. 递归地（recursive）把小于基准值元素的子数列和大于基准值元素的子数列排序。 

4. 递归的最底部情形，是数列的大小是零或一，也就是永远都已经被排序好了。虽然一直递归下去，但是这个算法总会结束，因为在每次的迭代（iteration）中，它至少会把一个元素摆到它最后的位置去。

![1676806501942](D:\MyNote\images\1676806501942.png)

![1676806710663](D:\MyNote\images\1676806710663.png)

![1676806732230](D:\MyNote\images\1676806732230.png)



**各种内部排序方法性能比较** ： 

1.**从平均时间而言**：快速排序最佳。但在最坏情况下时间性能不如堆排序和归并排序。 

2.**从算法简单性看**：由于直接选择排序、直接插入排序和冒泡排序的算法比较简单，将其认为是简单算法。对于Shell排序、堆排序、快速排序和归并排序算法，其算法比较复杂，认为是复杂排序。 

3.**从稳定性看**：直接插入排序、冒泡排序和归并排序时稳定的；而直接选择排序、快速排序、 Shell排序和堆排序是不稳定排序 

4.**从待排序的记录数n的大小看**，n较小时，宜采用简单排序；而n较大时宜采用改进排序

**排序算法的选择**：

(1)若n较小(如n≤50)，可采用**直接插入**或**直接选择排序**。 当记录规模较小时，直接插入排序较好；否则因为直接选择移动的记录数少于直接插入，应选直接选择排序为宜。 

(2)若文件初始状态基本有序(指正序)，则应选用**直接插入**、**冒泡**或随机的**快速排序**为宜； 

(3)若n较大，则应采用时间复杂度为O(nlgn)的排序方法：**快速排序**、**堆排序**或**归并排序**

### 3.4.Arrays工具类

java.util.Arrays类即为操作数组的工具类，包含了用来操作数组（比如排序和搜索）的各种方法

![1676807077741](D:\MyNote\images\1676807077741.png)

 java.util.Arrays类的sort()方法提供了数组元素排序功能：

```java
import java.util.Arrays;
public class SortTest {
    public static void main(String[] args) {
        int [] numbers = {5,900,1,5,77,30,64,700};
        Arrays.sort(numbers);
        for(int i = 0; i < numbers.length; i++){
        	System.out.println(numbers[i]);
        }
    }
}
```



**数组使用中的常见异常**：

+ 数组脚标越界异常(ArrayIndexOutOfBoundsException) ： 

```java
int[] arr = new int[2];
System.out.println(arr[2]);//访问到了数组中的不存在的脚标时发生
System.out.println(arr[-1]);
```

+ 空指针异常(NullPointerException) ： 

```java
int[] arr = null;
System.out.println(arr[0]);
arr引用没有指向实体，却在操作实体中的元素时。
```



## 4.面向对象编程

### 4.1.面向过程与面向对象

**何谓“面向对象”的编程思想？** 

​		首先解释一下“思想”。 先问你个问题：你想做个怎样的人？ 可能你会回答：我想做个好人，孝敬父母，尊重长辈，关爱亲朋…… 你看，这就是思想。这是你做人的思想，或者说，是你做人的原则。 做人有做人的原则，编程也有编程的原则。这些编程的原则呢，就是编程思想。 

面向过程(POP) 与 面向对象(OOP)

+  二者都是一种思想，面向对象是相对于面向过程而言的。面向过程，强调的是功能行为，以函数为最小单位，考虑怎么做。面向对象，将功能封装进对象，强调具备了功能的对象，以类/对象为最小单位，考虑谁来做。 
+  面向对象更加强调运用人类在日常的思维逻辑中采用的思想方法与原则，如抽象、分类、继承、聚合、多态等。 

**面向对象的三大特征**： 封装、继承 、多态 

![1676807919877](D:\MyNote\images\1676807919877.png)

**面向对象的思想概述**： 

+ 程序员从面向过程的执行者转化成了面向对象的指挥者
+ 面向对象分析方法分析问题的思路和步骤：
  + 根据问题需要，选择问题所针对的现实世界中的实体。
  + 从实体中寻找解决问题相关的属性和功能，这些属性和功能就形成了概念世界中的类。 
  + 把抽象的实体用计算机语言进行描述，形成计算机世界中类的定义。即借助某种程序语言，把类构造成计算机能够识别和处理的数据结构
  + 将类实例化成计算机世界中的对象。对象是计算机世界中解决问题的最终工具

### 4.2.类和对象

面向对象的思想概述：

+ 类(Class)和对象(Object)是面向对象的核心概念
  + 类是对一类事物的描述，是抽象的、概念上的定义
  + 对象是实际存在的该类事物的每个个体，因而也称为实例(instance)。
+ 万事万物皆对象
  + 可以理解为：类 = 抽象概念的人；对象 = 实实在在的某个人
  + 面向对象程序设计的重点是类的设计
  + 类的设计，其实就是定义类的成员的共有特征与行为
+ 现实世界的生物体，大到鲸鱼，小到蚂蚁，都是由最基本的细胞构成的。同理，Java代码世界是由诸多个不同功能的类构成的
+ 现实生物世界中的细胞又是由什么构成的呢？细胞核、细胞质、… 那么，Java中用类--class来描述事物也是如此。常见的类的成员有： 
  +  属 性：对应类中的成员变量 
  +  行 为：对应类中的成员方法 
  + Field = 属性 **=** 成员变量，Method = (成员)方法 = 函数

![1676808640575](D:\MyNote\images\1676808640575.png)

### 4.3.语法格式 

```java
修饰符 class 类名 {
    属性声明;
    方法声明;
}
说明：修饰符public：类可以被任意访问，类的正文要用{ }括起来
举例：
public class Person{
    private int age ; //声明私有变量 age
    public void showAge(int i) { //声明方法showAge( )
    	age = i;
    }
}
```



定义一个类的步骤：

1. 定义类（考虑修饰符、类名） 

2. 编写类的属性（考虑修饰符、属性类型、属性名、初始化值） 

3. 编写类的方法（考虑修饰符、返回值类型、方法名、形参等）

创建和使用方法：

1. 创建对象语法： 类名 对象名 = new 类名();
2. 使用“对象名.对象成员”的方式访问对象成员（包括属性和方法）

```java
举例: 
public class Zoo{
    public static void main(String args[]){
        //创建对象
        Animal xb=new Animal();
        xb.legs=4;//访问属性
        System.out.println(xb.legs);
        xb.eat();//访问方法
        xb.move();//访问方法
    }
}
```



说明： 如果创建了一个类的多个对象，对于类中定义的属性，每个对象都拥有各自的一套副本，且互不干扰。

**注意**： **类的访问机制**：

+ 在一个类中的访问机制：类中的方法可以直接访问类中的成员变量
+ static方法访问非static，编译不通过。
+ 在不同类中的访问机制：先创建要访问类的对象，再用对象访问类中定义的成员

### 4.4.内存解析

+ 堆（Heap），此内存区域的唯一目的就是存放对象实例，几乎所有的对象实例都在这里分配内存。这一点在Java虚拟机规范中的描述是：所有的对象实例以及数组都要在堆上分配。 
+ 通常所说的栈（Stack），是指虚拟机栈。虚拟机栈用于存储局部变量等。 局部变量表存放了编译期可知长度的各种基本数据类型（boolean、byte、char 、 short 、 int 、 float 、 long 、double）、对象引用reference类型，它不等同于对象本身，是对象在堆内存的首地址）。 方法执行完，自动释放。
+ 方法区（Method Area），用于存储已被虚拟机加载的类信息、常量、静态变量、即时编译器编译后的代码等数据。 

<img src="D:\MyNote\images\1676809347770.png" alt="1676809347770" style="zoom:67%;" />

![1676809376423](D:\MyNote\images\1676809376423.png)

**匿名对象** ：

+ 我们也可以不定义对象的句柄，而直接调用这个对象的方法。这样的对象叫做匿名对象。 如`new Person().shout(); `
+ 使用情况 
  + 如果对一个对象只需要进行一次方法调用，那么就可以使用匿名对象。 
  + 我们经常将匿名对象作为实参传递给一个方法调用

### 4.5.属性

语法格式： `修饰符 数据类型 属性名 = 初始化值 ; `

+ 说明1: 修饰符
  + 常用的权限修饰符有：private、缺省、protected、public
  + 其他修饰符：static、final (暂不考虑)
+ 说明2：数据类型
  + 任何基本数据类型(如int、Boolean) 或 任何引用数据类型
+ 说明3：属性名
  + 属于标识符，符合命名规则和规范即可

```java
public class Person{
    private int age; //声明private变量 age
    public String name = “Lila”; //声明public变量 name
}
```



变量的分类：成员变量与局部变量

+ 在方法体外，类体内声明的变量称为成员变量。 
+ 在方法体内部声明的变量称为局部变量。
+ 注意：二者在初始化值方面的异同**:**
  + 同：都有生命周期
  + 异：局部变量除形参外，均需显式初始化

<img src="D:\MyNote\images\1676809748969.png" alt="1676809748969" style="zoom:50%;" />

成员变量（属性）和局部变量的区别：

![1676809787040](D:\MyNote\images\1676809787040.png)

​		当一个对象被创建时，会对其中各种类型的成员变量自动进行初始化赋值。除了基本数据类型之外的变量类型都是引用类型，如上面的Person及前面讲过的数组。

<img src="D:\MyNote\images\1676809952537.png" alt="1676809952537" style="zoom:50%;" />

### 4.6.方法

​		方法是类或对象行为特征的抽象，用来完成某个功能操作。在某些语言中也称为函数或过程。 

​		将功能封装为方法的目的是，可以实现代码重用，简化代码 

​		Java里的方法不能独立存在，所有的方法必须定义在类里。

```java
public class Person{
    private int age;
    public int getAge() { //声明方法getAge()
    	return age; 
    }
    public void setAge(int i) { //声明方法setAge
    	age = i; //将参数i的值赋给类的成员变量age
    }
}
声明格式：
修饰符 返回值类型 方法名（参数类型 形参1, 参数类型 形参2, ….）｛
    方法体程序代码
    return 返回值;
｝
其中：
修饰符：public,缺省,private, protected等
返回值类型：
+没有返回值：void。
+有返回值，声明出返回值的类型。与方法体中“return 返回值”搭配使用
方法名：属于标识符，命名时遵循标识符命名规则和规范，“见名知意”
形参列表：可以包含零个，一个或多个参数。多个参数时，中间用“,”隔开
返回值：方法在执行完毕后返还给调用它的程序的数据。
```



方法的分类：按照是否有形参及返回值 

<img src="D:\MyNote\images\1676810113847.png" alt="1676810113847" style="zoom:50%;" />

方法通过方法名被调用，且只有被调用才会执行。 

注 意： 

+ 方法被调用一次，就会执行一次 
+ 没有具体返回值的情况，返回值类型用关键字void表示，那么方法体中可以不必使用return语句。如果使用，仅用来结束方法。 
+ 定义方法时，方法的结果应该返回给调用者，交由调用者处理。 
+ 方法中只能调用方法或属性，不可以在方法内部定义方法

**重载**

重载的概念： 在同一个类中，允许存在一个以上的同名方法，只要它们的参数个数或者参数类型不同即可。
重载的特点： 与返回值类型无关，只看参数列表，且参数列表必须不同。(参数个数或参数类型)。调用时，根据方法参数列表的不同来区别。

```java
重载示例：
//返回两个整数的和
int add(int x,int y){return x+y;}
//返回三个整数的和
int add(int x,int y,int z){return x+y+z;}
//返回两个小数的和
double add(double x,double y){return x+y;}
```



**可变个数的形参**

​		JavaSE 5.0 中提供了**Varargs(**variable number of arguments**)**机制，允许直接定义能和多个实参相匹配的形参。从而，可以用一种更简单的方式，来传递个数可变的实参

```java
//JDK 5.0以前：采用数组形参来定义方法，传入多个同一类型变量
public static void test(int a ,String[] books);
//JDK5.0：采用可变个数形参来定义方法，传入多个同一类型变量
public static void test(int a ,String…books);
```

**说明：** 

1. 声明格式：方法名(参数的类型名 ...参数名) 

2. 可变参数：方法参数部分指定类型的参数个数是可变多个：0个，1个或多个 

3. 可变个数形参的方法与同名的方法之间，彼此构成重载 

4. 可变参数方法的使用与方法参数部分使用数组是一致的 

5. 方法的参数部分有可变形参，需要放在形参声明的最后 

6. 在一个方法的形参位置，最多只能声明一个可变个数形参

方法，必须由其所在类或对象调用才有意义。若方法含有参数： 

+ **形参**：方法声明时的参数 
+ **实参：**方法调用时实际传给形参的参数值
+ Java的实参值如何传入方法呢？
  + Java里方法的参数传递方式只有一种：值传递。 即将实际参数值的副本（复制品）传入方法内，而参数本身不受影响。
  + 形参是基本数据类型：将实参基本数据类型变量的“数据值”传递给形参
  + 形参是引用数据类型：将实参引用数据类型变量的“地址值”传递给形参

**递归方法**

​		递归方法：一个方法体内调用它自身。方法递归包含了一种隐式的循环，它会重复执行某段代码，但这种重复执行无须循环控制。递归一定要向已知方向递归，否则这种递归就变成了无穷递归，类似于死循环。 

```java
//计算1-100之间所有自然数的和
public int sum(int num){
    if(num == 1){
    	return 1;
    }else{
    	return num + sum(num - 1);
    }
}
```



### 4.7.封装和隐藏

+ 为什么需要封装？封装的作用和含义？ 
  + 我要用洗衣机，只需要按一下开关和洗涤模式就可以了。有必要了解洗衣机内部的结构吗？有必要碰电动机吗？ 
  + 我要开车，… 
+ 我们程序设计追求“高内聚，低耦合”。 
  + 高内聚 ：类的内部数据操作细节自己完成，不允许外部干涉； 
  + 低耦合 ：仅对外暴露少量的方法用于使用。 
+ 隐藏对象内部的复杂性，只对外公开简单的接口。便于外界调用，从而提高系统的可扩展性、可维护性。通俗的说，把该隐藏的隐藏起来，该暴露的暴露出来。这就是封装性的设计思想

Java中通过将数据声明为私有的(private)，再提供公共的（public） 

方法:getXxx()和setXxx()实现对该属性的操作，以实现下述目的： 

+ 隐藏一个类中不需要对外提供的实现细节； 
+ 使用者只能通过事先定制好的方法来访问数据，可以方便地加入控制逻辑，限制对属性的不合理操作； 
+ 便于修改，增强代码的可维护性；

```java
class Animal {
    private int legs;// 将属性legs定义为private，只能被Animal类内部访问
    public void setLegs(int i) { // 在这里定义方法 eat() 和 move()
        if (i != 0 && i != 2 && i != 4) {
            System.out.println("Wrong number of legs!");
            return;
        }
        legs = i;
    }
    public int getLegs() {
        return legs;
    }
}
public class Zoo {
    public static void main(String args[]) {
        Animal xb = new Animal();
        xb.setLegs(4); // xb.setLegs(-1000);
        //xb.legs = -1000; // 非法
        System.out.println(xb.getLegs());
    }
}
```



​		Java权限修饰符public、protected、(缺省)、private置于类的成员定义前，用来限定对象对该类成员的访问权限。

![1676815006411](D:\MyNote\images\1676815006411.png)

对于class的权限修饰只可以用public和default(缺省)。 

+ public类可以在任意地方被访问。 
+ default类只可以被同一个包内部的类访问。

### 4.8.构造器

**特征**：

+ 它具有与类相同的名称
+ 它不声明返回值类型。（与声明为void不同）
+ 不能被static、final、synchronized、abstract、native修饰，不能有return语句返回值 

**作用**：创建对象；给对象进行初始化 

+ `Order o = new Order(); Person p = new Person(“Peter”,15);`
+ 如同我们规定每个“人”一出生就必须先洗澡，我们就可以在“人”的构造器中加入完成“洗澡”的程序代码，于是每个“人”一出生就会自动完成“洗澡”，程序就不必再在每个人刚出生时一个一个地告诉他们要“洗澡”了。

**语法格式** ：

```java
修饰符 类名 (参数列表) {
	初始化语句；
}
举例：
public class Animal {
    private int legs;
    // 构造器
    public Animal() {
    	legs = 4;
    } 
    public void setLegs(int i) {
    	legs = i;
    }
    public int getLegs() {
    	return legs;
    }
}
创建Animal类的实例：Animal a = new Animal();
调用构造器，将legs初始化为4。
```



根据参数不同，构造器可以分为如下两类：

+ 隐式无参构造器（系统默认提供） 
+ 显式定义一个或多个构造器（无参、有参） 

**注意** ： 

+ Java语言中，每个类都至少有一个构造器 
+ 默认构造器的修饰符与所属类的修饰符一致 
+ 一旦显式定义了构造器，则系统不再提供默认构造器 
+ 一个类可以创建多个重载的构造器 
+ 父类的构造器不可被子类继承

**构造器重载**：

+ 构造器一般用来创建对象的同时初始化对象。如

```java
class Person{
    String name;
    int age;
    public Person(String n , int a){ name=n; age=a;}
}
```

+ 构造器重载使得对象的创建更加灵活，方便创建各种不同的对象。

```java
public class Person{
    public Person(String name, int age, Date d) {this(name,age);…}
    public Person(String name, int age) {…}
    public Person(String name, Date d) {…}
    public Person(){…}
}
```

+ 构造器重载，参数列表必须不同

截止到目前，有很多位置都可以对类的属性赋值。总结这几个位置，并指明赋值的先后顺序。 

+ 赋值的位置： 

  ① 默认初始化 

  ② 显式初始化 

  ③ 构造器中初始化 

  ④ 通过“对象.属性“或“对象.方法”的方式赋值 

+ 赋值的先后顺序： ① - ② - ③ - ④

### 4.9.拓展知识

**JavaBean**：

+ JavaBean是一种Java语言写成的可重用组件。
+ 所谓javaBean，是指符合如下标准的Java类：
  + 类是公共的
  + 有一个无参的公共的构造器
  + 有属性，且有对应的get、set方法
+ 用户可以使用JavaBean将功能、处理、值、数据库访问和其他任何可以用Java代码创造的对象进行打包，并且其他的开发者可以通过内部的JSP页面、Servlet、其他JavaBean、applet程序或者应用来使用这些对象。用
  户可以认为JavaBean提供了一种随时随地的复制和粘贴的功能，而不用关心任何改变。

```java
public class JavaBean {
    private String name; // 属性一般定义为private
    private int age;
    public JavaBean() {
    }
    public int getAge() {
    	return age;
    }
    public void setAge(int a) {
    	age = a;
    }
    public String getName() {
    	return name;
    }
    public void setName(String n) {
    	name = n;
    }
}
```



**UML类图**

![1676818305218](D:\MyNote\images\1676818305218.png)

### 4.10.关键字

#### 4.10.1.this

+ 在Java中，this关键字比较难理解，它的作用和其词义很接近。 
  + 它在方法内部使用，即这个方法所属对象的引用； 
  + 它在构造器内部使用，表示该构造器正在初始化的对象。 

+ this 可以调用类的属性、方法和构造器 

+ 什么时候使用this关键字呢？ 
  + 当在方法内需要用到调用该方法的对象时，就用this。 具体的：我们可以用this来区分属性和局部变量。 

    比如：this.name = name;

+ 使用this，调用属性、方法
  + 在任意方法或构造器内，如果使用当前类的成员变量或成员方法可以在其前面添加this，增强程序的阅读性。不过，通常我们都习惯省略this。
  + 当形参与成员变量同名时，如果在方法内或构造器内需要使用成员变量，必须添加this来表明该变量是类的成员变量 
  + 使用this访问属性和方法时，如果在本类中未找到，会从父类中查找 

```java
class Person{ // 定义Person类
    private String name ;
    private int age ;
    public Person(String name,int age){
        this.name = name ; 
        this.age = age ; 
    }
    public void getInfo(){
        System.out.println("姓名：" + name) ;
        this.speak();
    }
    public void speak(){
    	System.out.println(“年龄：” + this.age);
    }
}
```

+ 使用this调用本类的构造器
  + this可以作为一个类中构造器相互调用的特殊格式

```java
class Person{ // 定义Person类
    private String name ;
    private int age ;
    public Person(){ // 无参构造器
    	System.out.println("新对象实例化") ;
    }
    public Person(String name){
        this(); // 调用本类中的无参构造器
        this.name = name ;
    }
    public Person(String name,int age){
        this(name) ; // 调用有一个参数的构造器
        this.age = age;
    }
    public String getInfo(){
    	return "姓名：" + name + "，年龄：" + age ;
    } 
}
```



**注意：**

+ 可以在类的构造器中使用"this(形参列表)"的方式，调用本类中重载的其他的构造器！ 

+ 明确：构造器中不能通过"this(形参列表)"的方式调用自身构造器 

+ 如果一个类中声明了n个构造器，则最多有 n - 1个构造器中使用了"this(形参列表)" 

+ "this(形参列表)"必须声明在类的构造器的首行！ 

+ 在类的一个构造器中，最多只能声明一个"this(形参列表)"

#### 4.10.2.super

在Java类中使用super来调用父类中的指定操作：

+ super可用于访问父类中定义的属性 

+ super可用于调用父类中定义的成员方法 

+ super可用于在子类构造器中调用父类的构造器

**注意**：

+ 尤其当子父类出现同名成员时，可以用super表明调用的是父类中的成员 

+ super的追溯不仅限于直接父类 

+ super和this的用法相像，this代表本类对象的引用，super代表父类的内存空间的标识

```java
class Person {
    protected String name= "张三";
    protected int age;
	public String getInfo() {
        return"Name: "+ name+ "\nage: "+ age;
        }
}
class Student extends Person {
    protected String name= "李四";
    private String school= "New Oriental";
    public String getSchool() {
    	return school;
    }
	public String getInfo() {
        return super.getInfo()+ "\nschool: "+ school;
    }
}
public class StudentTest {
    public static void main(String[] args) {
        Student st= new Student();
		System.out.println(st.getInfo());
    }
}
```

+ 子类中所有的构造器默认都会访问父类中空参数的构造器 

+ 当父类中没有空参数的构造器时，子类的构造器必须通过this(参数列表**)**或者super(参数列表)语句指定调用本类或者父类中相应的构造器。同时，只能”二选一”，且必须放在构造器的首行 
+ 如果子类构造器中既未显式调用父类或本类的构造器，且父类中又没有无参的构造器，则编译出错

**this和super的区别**

![1676897948810](D:\MyNote\images\1676897948810.png)

#### 4.10.3.package

+ package语句作为Java源文件的第一条语句，指明该文件中定义的类所在的包。(若缺省该语句，则指定为无名包)。它的格式为：`package 顶层包名.子包名 ;`

```java
举例：pack1\pack2\PackageTest.java
package pack1.pack2; //指定类PackageTest属于包pack1.pack2
public class PackageTest{
    public void display(){
    	System.out.println("in method display()");
    }
}
```

+ 包对应于文件系统的目录，package语句中，用 “.” 来指明包(目录)的层次； 
+ 包通常用小写单词标识。通常使用所在公司域名的倒置：com.atguigu.xxx

<img src="D:\MyNote\images\1676819027305.png" alt="1676819027305" style="zoom: 67%;" />

**作用：**

+ 包帮助管理大型软件系统：将功能相近的类划分到同一个包中。比如：MVC的设计模式
+ 包可以包含类和子包，划分项目层次，便于管理
+ 解决类命名冲突的问题
+ 控制访问权限

**MVC设计模式**：

​		MVC是常用的设计模式之一，将整个程序分为三个层次：视图模型层，控制器层，与数据模型层。这种将程序输入输出、数据处理，以及数据的展示分离开来的设计模式使程序结构变的灵活而且清晰，同时也描述了程序各个对象间的通信方式，降低了程序的耦合性。

+ 模型层 model 主要处理数据 

  \>数据对象封装 model.bean/domain 

  \>数据库操作类 model.dao 

  \>数据库             model.db

+ 控制层 controller 处理业务逻辑

  \>应用界面相关  	controller.activity 

  \>存放fragment 	controller.fragment 

  \>显示列表的适配器 controller.adapter 

  \>服务相关的  		controller.service 

  \>抽取的基类 		 controller.base

+ 视图层 view 显示数据

  \>相关工具类 view.utils 

  \>自定义view view.ui

<img src="D:\MyNote\images\1676819322475.png" alt="1676819322475" style="zoom:50%;" />

**JDK中主要的包介绍**

1. java.lang----包含一些Java语言的核心类，如String、Math、Integer、 System和
Thread，提供常用功能
2. java.net----包含执行与网络相关的操作的类和接口。
3. java.io ----包含能提供多种输入/输出功能的类。
4. java.util----包含一些实用工具类，如定义系统特性、接口的集合框架类、使用与日
期日历相关的函数。
5. java.text----包含了一些java格式化相关的类
6. java.sql----包含了java进行JDBC数据库编程的相关类/接口
7. java.awt----包含了构成抽象窗口工具集（abstract window toolkits）的多个类，这
些类被用来构建和管理应用程序的图形用户界面(GUI)。

#### 4.10.4.import

​		为使用定义在不同包中的Java类，需用import语句来引入指定包层次下所需要的类或全部类(.*)。import语句告诉编译器到哪里去寻找类。 语法格式： `import 包名. 类名;`

```java
import pack1.pack2.Test; //import pack1.pack2.*;表示引入pack1.pack2包中的所有结构
public class PackTest{
    public static void main(String args[]){
        Test t = new Test(); //Test类在pack1.pack2包中定义
        t.display();
    }
}
```

**注意：** 

1. 在源文件中使用import显式的导入指定包下的类或接口 

2. 声明在包的声明和类的声明之间。 

3. 如果需要导入多个类或接口，那么就并列显式多个import语句即可 

4. 举例：可以使用java.util.*的方式，一次性导入util包下所有的类或接口。 

5. 如果导入的类或接口是java.lang包下的，或者是当前包下的，则可以省略此import语句。 

6. 如果在代码中使用不同包下的同名的类。那么就需要使用类的全类名的方式指明调用的是哪个类。 

7. 如果已经导入java.a包下的类。那么如果需要使用a包的子包下的类的话，仍然需要导入。 

8. import static组合的使用：调用指定类或接口下的静态的属性或方法

#### 4.10.5.final

在Java中声明类、变量和方法时，可使用关键字final来修饰,表示“最终的”。

+ final标记的类不能被继承。提高安全性，提高程序的可读性。如String类、System类、StringBuffer类

+ final标记的方法不能被子类重写。比如：Object类中的getClass()。

+ final标记的变量(成员变量或局部变量)即称为常量。名称大写，且只能被赋值一次。final标记的成员变量必须在声明时或在每个构造器中或代码块中显式赋值，然后才能使用。

  `final double MY_PI = 3.14;`

 **final修饰类**：

```java
final class A{
}
class B extends A{ //错误，不能被继承。
}
中国古代，什么人不能有后代，就可以被final声明，称为“太监类”！
```

**final修饰方法**

```java
class A {
    public final void print() {
    	System.out.println("A");
    }
}
class B extends A {
    public void print() { // 错误，不能被重写。
    	System.out.println("尚硅谷");
    }
}
```

**final修饰变量**——常量

```java
class A {
    private final String INFO = "atguigu"; //声明常量
    public void print() {
        //The final field A.INFO cannot be assigned
        //INFO = "尚硅谷";
    }
}
常量名要大写，内容不可修改。——如同古代皇帝的圣旨。
static final：全局常量
```



**应用举例**

```java
public final class Test {
    public static int totalNumber = 5;
    public final int ID;
    public Test() {
    	ID = ++totalNumber; // 可在构造器中给final修饰的“变量”赋值
    }
    public static void main(String[] args) {
        Test t = new Test();
        System.out.println(t.ID);
        final int I = 10;
        final int J;
        J = 20;
        J = 30; // 非法
    }
}
```



### 4.11.继承性

​		为什么要有继承？多个类中存在相同属性和行为时，将这些内容抽取到单独一个类中，那么多个类无需再定义这些属性和行为，只要继承那个类即可。此处的多个类称为子类(派生类)，单独的这个类称为父类(基类或超类)。可以理解为:“子类is a 父类”。类继承语法规则： `class Subclass extendsSuperClass{}`

作用：

+ 继承的出现减少了代码冗余，提高了代码的复用性
+ 继承的出现，更有利于功能的扩展
+ 继承的出现让类与类之间产生了关系，提供了多态的前提

**注意**：不要仅为了获取其他类中某个功能而去继承

```java
为描述和处理个人信息，定义类Person:
class Person {
    public String name;
    public int age;
    public Date birthDate;
	public String getInfo() {
	//...
    }
}
为描述和处理学生信息，定义类Student:
class Student {
    public String name;
	public int age;
	public Date birthDate;
    public String school;
    public String getInfo() {
        // ...
    }
}
通过继承，简化Student类的定义：
class Student extends Person {
    public String school;
}
Student类继承了父类Person的所有属性和方法，并增加了一个属性school。Person中的属性和方法,Student都可以使用。
```



<img src="D:\MyNote\images\1676894915997.png" alt="1676894915997" style="zoom:50%;" /><img src="D:\MyNote\images\1676895044758.png" alt="1676895044758" style="zoom:50%;" /><img src="D:\MyNote\images\1676895121444.png" alt="1676895121444" style="zoom:60%;" />

+ 子类继承了父类，就继承了父类的方法和属性。
+ 在子类中，可以使用父类中定义的方法和属性，也可以创建新的数据和方法。 
+ 在Java 中，继承的关键字用的是“extends”，即子类不是父类的子集，而是对父类的“扩展”。

关于继承的规则： 子类不能直接访问父类中私有的(private)的成员变量和方法。

![1676895277968](D:\MyNote\images\1676895277968.png)

+ Java只支持单继承和多层继承，不允许多重继承
  + 一个子类只能有一个父类
  + 一个父类可以派生出多个子类

### 4.12.方法的重写

**定义**：在子类中可以根据需要对从父类中继承来的方法进行改造，也称为方法的重置、覆盖。在程序执行时，子类的方法将覆盖父类的方法。

**要求**：

1. 子类重写的方法必须和父类被重写的方法具有相同的方法名称、参数列表

2. 子类重写的方法的返回值类型不能大于父类被重写的方法的返回值类型 

3. 子类重写的方法使用的访问权限不能小于父类被重写的方法的访问权限，子类不能重写父类中声明为private权限的方法

4. 子类方法抛出的异常不能大于父类被重写方法的异常

**注意：** 

子类与父类中同名同参数的方法必须同时声明为非static的(即为重写)，或者同时声明为

static的（不是重写）。因为static方法是属于类的，子类无法覆盖父类的方法。

```java
public class Person {
    public String name;
    public intage;
    public String getInfo(){
        return "Name: "+ name + "\n" +"age: "+ age;
    }
}
public class Student extends Person {
    public String school;
	public String getInfo(){       //重写方法
        return  "Name: "+ name + "\nage: "+ age + "\nschool: "+ school;
	}
	public static void main(String args[]){
        Student s1=new Student();
        s1.name="Bob";
        s1.age=20;
        s1.school="school2";
        System.out.println(s1.getInfo());   //Name:Bobage:20  school:school2
    }
}
Person p1=new Person();
p1.getInfo();//调用Person类的getInfo()方法
Student s1=new Student();
s1.getInfo();//调用Student类的getInfo()方法
这是一种“多态性”：同名的方法，用不同的对象来区分调用的是哪一个方法。

```



### 4.13.访问权限修饰符

​		Java权限修饰符public、protected、(缺省)、private置于类的成员定义前，用来限定对象对该类成员的访问权限。

![1676896027474](D:\MyNote\images\1676896027474.png)

对于class的权限修饰只可以用public和default(缺省)。

+ public类可以在任意地方被访问。 

+ default类只可以被同一个包内部的类访问。

**访问控制举例并分析**

```java
class Parent{
    private int f1=1;
	int f2=2;
	protected int f3=3;
    public int f4=4;
    
    private   void fm1(){System.out.println("infm1()f1="+f1);}
              void fm2(){System.out.println("infm2()f2="+f2);}
    protected void fm3(){System.out.println("infm3()f3="+f3);}
    public    void fm4(){System.out.println("infm4()f4="+f4);}
}
class Child extends Parent{               //设父类和子类在同一个包内
    private int c1 = 21;
    public int c2 = 22;
    private void cm1(){System.out.println("in cm1() c1=" + c1);}
    public  void cm2(){System.out.println("in cm2() c2=" + c2);}
    public static void main(String[] args){
    	int i; 
		Parent  p = new Parent();
    	i = p.f2;		//i = p.f3;i = p.f4;
		p.fm2();        //p.fm3();p.fm4();
        Child  c = new Child();
        i= c.f2;		//i= c.f3;i= c.f4;
    	i= c.c1;		//i= c.c2;
        c.cm1();       // c.cm2();    c.fm2();   c.fm3();   c.fm4()
    }
}
父类Parent和子类Child在同一包中定义时：   
子类对象可以访问的数据：f2_default、f3_protected、f4_public、c1_private、c2_public
子类的对象可以调用的方法：fm2()_default、fm3()_protected、fm4()_public、cm1()_private、cm2()_public
```



### 4.14.子类对象的实例化过程

![1676898091514](D:\MyNote\images\1676898091514.png)

**思考**： 

1).为什么super(…)和this(…)调用语句不能同时在一个构造器中出现？ 

2).为什么super(…)或this(…)调用语句只能作为构造器中的第一句出现？

```java
class Creature {
    public Creature() {
    	System.out.println("Creature无参数的构造器");
    }
}
class Animal extends Creature {
    public Animal(String name) {
    	System.out.println("Animal带一个参数的构造器，该动物的name为" + name);
    }
    public Animal(String name, int age) {
        this(name);
        System.out.println("Animal带两个参数的构造器，其age为" + age);
    }
}
public class Wolf extends Animal {
    public Wolf() {
        super("灰太狼", 3);
        System.out.println("Wolf无参数的构造器");
    }
    public static void main(String[] args) {
    	new Wolf();
    }
}
```



### 4.15.多态性

​		多态性，是面向对象中最重要的概念，在Java中的体现： 对象的多态性：父类的引用指向子类的对象。可以直接应用在抽象类和接口上

​		Java引用变量有两个类型：编译时类型和运行时类型。编译时类型由声明该变量时使用的类型决定，运行时类型由实际赋给该变量的对象决定。简称：编译时，看左边；运行时，看右边

+ 若编译时类型和运行时类型不一致，就出现了对象的多态性(Polymorphism)
+ 多态情况下，“看左边”：看的是父类的引用（父类中不具备子类特有的方法）
                         “看右边”：看的是子类的对象（实际运行的是子类重写父类的方法）

​        对象的多态 —在Java中,子类的对象可以替代父类的对象使用

+ 一个变量只能有一种确定的数据类型 

+ 一个引用类型变量可能指向(引用)多种不同类型的对象

```java
Person p = new Student();
Object o = new Person();//Object类型的变量o，指向Person类型的对象
o = new Student(); //Object类型的变量o，指向Student类型的对象
```



子类可看做是特殊的父类，所以父类类型的引用可以指向子类的对象：向上转型(upcasting)。

一个引用类型变量如果声明为父类的类型，但实际引用的是子类对象，那么该变量就**不能**再访问子类中添加的属性和方法

```java
Student m = new Student();
m.school = “pku”; //合法,Student类有school成员变量
Person e = new Student(); 
e.school = “pku”; //非法,Person类没有school成员变量
属性是在编译时确定的，编译时e为Person类型，没有school成员变量，因而编译错误。
```



方法声明的形参类型为父类类型，可以使用子类的对象作为实参调用该方法

```java
public class Test {
    public void method(Person e) {
        // ……
        e.getInfo();
    }
    public static void main(Stirng args[]) {
        Test t = new Test();
        Student m = new Student();
        t.method(m); // 子类的对象m传送给父类类型的参数e
    }
}
```



**虚拟方法调用**

```java
正常的方法调用：
    Person e = new Person();
    e.getInfo();
    Student e = new Student();
    e.getInfo();
虚拟方法调用(多态情况下)：
	子类中定义了与父类同名同参数的方法，在多态情况下，将此时父类的方法称为虚拟方法，父类根据赋给它的不同子类对象，动态调用属于子类的该方法。这样的方法调用在编译期是无法确定的
 	Person e = new Student();
	e.getInfo(); //调用Student类的getInfo()方法
编译时类型和运行时类型：
    编译时e为Person类型，而方法的调用是在运行时确定的，所以调用的是Student类的getInfo()方法。——动态绑定
```



**注意**：**方法的重载与重写的区别**

​		重载，是指允许存在多个同名方法，而这些方法的参数不同。编译器根据方法不同的参数表，对同名方法的名称做修饰。对于编译器而言，这些同名方法就成了不同的方法。它们的调用地址在编译期就绑定了。Java的重载是可以包括父类和子类的，即子类可以重载父类的同名不同参数的方法。所以：对于重载而言，在方法调用之前，编译器就已经确定了所要调用的方法，这称为“早绑定”或“静态绑定”；

​		而对于多态，只有等到方法调用的那一刻，解释运行器才会确定所要调用的具体方法，这称为“晚绑定”或“动态绑定”。 

引用一句Bruce Eckel的话：“不要犯傻，如果它不是晚绑定，它就不是多态。”

作用：提高了代码的通用性，常称作接口重用

前提：需要存在继承或者实现关系；有方法的重写

成员方法：编译时：要查看引用变量所声明的类中是否有所调用的方法。运行时：调用实际new的对象所属的类中的重写方法。

成员变量：不具备多态性，只看引用变量所声明的类。

#### 1.15.1.instanceof 操作符

x instanceof A：检验x是否为类A的对象，返回值为boolean型。

+ 要求x所属的类与类A必须是子类和父类的关系，否则编译错误。 
+ 如果x属于类A的子类B，x instanceof A值也为true

```java
public class Person extends Object {…}
public class Student extends Person {…}
public class Graduate extends Person {…}
-------------------------------------------------------------------
public void method1(Person e) {
    if (e instanceof Person) 
    // 处理Person类及其子类对象
    if (e instanceof Student) 
    //处理Student类及其子类对象
    if (e instanceof Graduate)
    //处理Graduate类及其子类对象
}
```



#### 1.15.2.对象类型转换

**基本数据类型**的Casting：

+ **自动类型转换**：小的数据类型可以自动转换成大的数据类型，如 `long g=20; `，`double d=12.0f`
+ **强制类型转换：**可以把大的数据类型强制转换(casting)成小的数据类型，如`float f=(float)12.0; int a=(int)1200L `

对Java对象的强制类型转换称为造型

+ 从子类到父类的类型转换可以自动进行
+ 从父类到子类的类型转换必须通过造型(强制类型转换)实现
+ 无继承关系的引用类型间的转换是非法的
+ 在造型前可以使用instanceof操作符测试一个对象的类型

```java
public class Test {
    public void method(Person e) { // 设Person类中没有getschool() 方法
        // System.out.pritnln(e.getschool()); //非法,编译时错误
        if (e instanceof Student) {
            Student me = (Student) e; // 将e强制转换为Student类型
            System.out.pritnln(me.getschool());
        }
    }
    public static void main(String[] args){
        Test t = new Test();
        Student m = new Student();
        t.method(m);
    }
}
```



​		若子类重写了父类方法，就意味着子类里定义的方法彻底覆盖了父类里的同名方法，系统将不可能把父类里的方法转移到子类中。 对于实例变量则不存在这样的现象，即使子类里定义了与父类完全相同的实例变量，这个实例变量依然不可能覆盖父类中定义的实例变量

### 4.16.Object 类

​		Object类是所有Java类的根父类，如果在类的声明中未使用extends关键字指明其父类，则默认父类 

为java.lang.Object类

**主要结构**：

![1676904791272](D:\MyNote\images\1676904791272.png)

基本类型比较值:只要两个变量的值相等，即为true。 'int a=5; if(a==6){…}'

引用类型比较引用(是否指向同一个对象)：只有指向同一个对象时，==才返回true。 

```java
Person p1=new Person();
Person p2=new Person();
if (p1==p2){…}
用“==”进行比较时，符号两边的数据类型必须兼容(可自动转换的基本数据类型除外)，否则编译出错
```



**equals**()：所有类都继承了Object，也就获得了equals()方法。还可以重写。只能比较引用类型，其作用与“==”相同,比较是否指向同一个对象。格式:obj1.equals(obj2)

**特例**：当用equals()方法进行比较时，对类File、String、Date及包装类（Wrapper Class）来说，是比较类型及内容而不考虑引用的是否是同一个对象；原因：在这些类中重写了Object类的equals()方法

当自定义使用equals()时，可以重写。用于比较两个对象的“内容”是否都相等

重写equals()方法的**原则**：

+ 对称性：如果x.equals(y)返回是“true”，那么y.equals(x)也应该返回是“true”。
+ 自反性：x.equals(x)必须返回是“true”
+ 传递性：如果x.equals(y)返回是“true” ，而且y.equals(z)返回是“true”，那么z.equals(x)也应该返回是“true”
+ 一致性：如果x.equals(y)返回是“true” ，只要x和y内容一直不变，不管你重复x.equals(y)多少次，返回都是“true”。
+ 任何情况下，x.equals(null)，永远返回是“false” ； x.equals(和x不同类型的对象)永远返回是“false”。

```java
public class EqualsTest {
    public static void main(String[] args) {
        MyDate m1 = new MyDate(14, 3, 1976);
        MyDate m2 = new MyDate(14, 3, 1976);
        if (m1 == m2) {
        	System.out.println("m1==m2");
        } else {
        	System.out.println("m1!=m2"); // m1 != m2
        }
        if (m1.equals(m2)) {
        	System.out.println("m1 is equal to m2");// m1 is equal to m2
        } else {
        	System.out.println("m1 is not equal to m2");
        }
    }
}
```



**toString**() 方法：

​		toString()方法在Object类中定义，其返回值是String类型，返回类名和它的引用地址。在进行String与其它类型数据的连接操作时，自动调用toString()方法

```java
Date now=new Date();
System.out.println(“now=”+now); 相当于System.out.println(“now=”+now.toString());
```



可以根据需要在用户自定义类型中重写toString()方法，如String 类重写了toString()方法，返回字符串的值

```java
s1=“hello”;
System.out.println(s1);//相当于System.out.println(s1.toString());
```



基本类型数据转换为String类型时，调用了对应包装类的toString()方法

### 4.17.包装类

​		针对八种基本数据类型定义相应的引用类型—包装类（封装类） ，有了类的特点，就可以调用类中的方法，Java才是真正的面向对象

<img src="D:\MyNote\images\1676905338233.png" alt="1676905338233" style="zoom: 67%;" />

基本数据类型包装成包装类的实例 ---**装箱**

+ 通过包装类的构造器实现： `int i = 500; Integer t = new Integer(i);`
+ 还可以通过字符串参数构造包装类对象： `Float f = new Float(“4.56”);` 

获得包装类对象中包装的基本类型变量 ---**拆箱**

+ 调用包装类的.xxxValue()方法：`boolean b = bObj.booleanValue();`

JDK1.5之后，支持自动装箱，自动拆箱。但类型必须匹配

字符串转换成基本数据类型

+ 通过包装类的构造器实现： `int i = new Integer(“12”);`
+  通过包装类的parseXxx(String s)静态方法： `Float f = Float.parseFloat(“12.1”);`
+ 基本数据类型转换成字符串
  +  调用字符串重载的valueOf()方法：`String fstr = String.valueOf(2.34f);`
  +  更直接的方式：`String intStr = 5 + “”`

![1676905583526](D:\MyNote\images\1676905583526.png)

```java
int i = 500;
Integer t = new Integer(i);
装箱：包装类使得一个基本数据类型的数据变成了类。
有了类的特点，可以调用类中的方法。
String s = t.toString(); // s = “500“,t是类，有toString方法
String s1 = Integer.toString(314); // s1= “314“ 将数字转换成字符串。
String s2=“4.56”;
double ds=Double.parseDouble(s2); //将字符串转换成数字

拆箱：将数字包装类中内容变为基本数据类型。
int j = t.intValue(); // j = 500，intValue取出包装类中的数据
包装类在实际开发中用的最多的在于字符串变为基本数据类型。
String str1 = "30" ;
String str2 = "30.3" ;
int x = Integer.parseInt(str1) ; // 将字符串变为int型
float f = Float.parseFloat(str2) ; // 将字符串变为int型
```



### 4.18.static

如果想让一个类的所有实例共享数据，就用类变量！

```java
class Circle{
    private double radius;
    public Circle(double radius){
        this.radius=radius;
    }
    public double findArea(){
        return Math.PI*radius*radius;
    }
}
创建两个Circle对象
Circle c1=new Circle(2.0); //c1.radius=2.0
Circle c2=new Circle(3.0); //c2.radius=3.0

```

​		Circle类中的变量radius是一个实例变量(instance variable)，它属于类的每一个对象，不能被同一个类的不同对象所共享。上例中c1的radius独立于c2的radius，存储在不同的空间。c1中的radius变化不会影响c2的radius，反之亦然。

**类属性、类方法的设计思想**：

+ 类属性作为该类各个对象之间共享的变量。在设计类时,分析哪些属性不因对象的不同而改变，将这些属性设置为类属性。相应的方法设置为类方法。
+ 如果方法与调用者无关，则这样的方法通常被声明为类方法，由于不需要创建对象就可以调用类方法，从而简化了方法的调用。

使用范围： 在Java类中，可用static修饰属性、方法、代码块、内部类

被修饰后的成员具备以下特点：

+ 随着类的加载而加载 
+ 优先于对象存在 
+ 修饰的成员，被所有对象所共享 

+ 访问权限允许时，可不创建对象，直接被类调用

```java
class Circle {
    private double radius;
    public static String name = "这是一个圆";
    public static String getName() {
    	return name;
    }
    public Circle(double radius) {
    	this.radius = radius;
    }
    public double findArea() {
    	return Math.PI * radius * radius;
    }
    public void display() {
    	System.out.println("name:" + name + "radius:" + radius);
    }
}
public class StaticTest {
    public static void main(String[] args) {
        Circle c1 = new Circle(2.0);
        Circle c2 = new Circle(3.0);
        c1.display();
        c2.display();
    }
}

类变量：类变量（类属性）由该类的所有实例共享
class Person {
    private int id;
    public static int total = 0;
    public Person() {
        total++;
        id = total;
    }
    public static void main(String args[]){
        Person Tom=new Person();
        Tom.id=0;
        total=100; // 不用创建对象就可以访问静态成员
    }
}
public class StaticDemo {
    public static void main(String args[]) {
        Person.total = 100; // 不用创建对象就可以访问静态成员
        //访问方式：类名.类属性，类名.类方法
        System.out.println(Person.total);
        Person c = new Person();
        System.out.println(c.total); //输出101
	}
}
```



**类方法**：没有对象的实例时，可以用类名.方法名()的形式访问由static修饰的类方法。在static方法内部只能访问类的static修饰的属性或方法，不能访问类的非static的结构。因为不需要实例就可以访问static方法，因此static方法内部不能有this。(也不能有super ? YES!)static修饰的方法不能被重写。

#### 4.18.1.单例设计模式

​		设计模式是在大量的实践中总结和理论化之后优选的代码结构、编程风格、以及解决问题的思考方式。设计模免去我们自己再思考和摸索。就像是经典的棋谱，不同的棋局，我们用不同的棋谱。”套路”

​		所谓类的单例设计模式，就是采取一定的方法保证在整个的软件系统中，对某个类只能存在一个对象实例，并且该类只提供一个取得其对象实例的方法。如果我们要让类在一个虚拟机中只能产生一个对象，我们首先必须将类的构造器的访问权限设置为private，这样，就不能用new操作符在类的外部产生类的对象了，但在类内部仍可以产生该类的对象。因为在类的外部开始还无法得到类的对象，只能调用该类的某个静态方法以返回类内部创建的对象，静态方法只能访问类中的静态成员变量，所以，指向类内部产生的该类对象的变量也必须定义成静态的。

**饿汉式**：

```java
class Singleton {
    // 1.私有化构造器
    private Singleton() {
    }
    // 2.内部提供一个当前类的实例
    // 4.此实例也必须静态化
    private static Singleton single = new Singleton();
    // 3.提供公共的静态的方法，返回当前类的对象
    public static Singleton getInstance() {
    return single;
    }
}
```



**懒汉式**：

```java
class Singleton {
    // 1.私有化构造器
    private Singleton() {
    }
    // 2.内部提供一个当前类的实例
    // 4.此实例也必须静态化
    private static Singleton single;
    // 3.提供公共的静态的方法，返回当前类的对象
    public static Singleton getInstance() {
        if(single == null) {
        	single = new Singleton();
        }
        return single;
    }
}
懒汉式暂时还存在线程安全问题，学到多线程时，可修复
```

**优点：**由于单例模式只生成一个实例，减少了系统性能开销，当一个对象的产生需要比较多的资源时，如读取配置、产生其他依赖对象时，则可以通过在应用启动时直接产生一个单例对象，然后永久驻留内存的方式来解决。举例 java.lang.Runtime。

**应用场景**：

+  网站的计数器，一般也是单例模式实现，否则难以同步。 
+  应用程序的日志应用，一般都使用单例模式实现，这一般是由于共享的日志文件一直处于打开状态，因为只能有一个实例去操作，否则内容不好追加。 
+  数据库连接池的设计一般也是采用单例模式，因为数据库连接是一种数据库资源。 
+  项目中，读取配置文件的类，一般也只有一个对象。没有必要每次使用配置文件数据，都生成一个对象去读取。 
+  Application 也是单例的典型应用 
+  Windows的Task Manager (任务管理器)就是很典型的单例模式 
+  Windows的Recycle Bin (回收站)也是典型的单例应用。在整个系统运行过程中，回收站一直维护着仅有的一个实例。

**main方法**：

​		由于Java虚拟机需要调用类的main()方法，所以该方法的访问权限必须是public，又因为Java虚拟机在执行main()方法时不必创建对象，所以该方法必须是static的，该方法接收一个String类型的数组参数，该数组中保存执行Java命令时传递给所运行的类的参数。又因为main() 方法是静态的，我们不能直接访问该类中的非静态成员，必须创建该类的一个实例对象后，才能通过这个对象去访问类中的非静态成员，这种情况，我们在之前的例子中多次碰到。

```java
public class CommandPara {
    public static void main(String[] args) {
        for (int i = 0; i < args.length; i++) {
        	System.out.println("args[" + i + "] = " + args[i]);
        }
    }
}
//dos窗口运行程序CommandPara.java
java CommandPara “Tom" “Jerry" “Shkstart"
输出结果：
args[0] = Tom
args[1] = Jerry
args[2] = Shkstart
```

**代码块**：

+ 作用：对Java类或对象进行初始化

+ 分类： 一个类中代码块若有修饰符，则只能被static修饰，称为静态代码块(static block)，没有使用static修饰的，为非静态代码块。
+ static代码块通常用于初始化static的属性：

```java
class Person {
    public static int total;
    static {
        total = 100;//为total赋初值
    }
    …… //其它属性或方法声明
}
```

**静态代码块：**用static修饰的代码块

1. 可以有输出语句。 

2. 可以对类的属性、类的声明进行初始化操作。 

3. 不可以对非静态的属性初始化。即：不可以调用非静态的属性和方法。 

4. 若有多个静态的代码块，那么按照从上到下的顺序依次执行。 

5. 静态代码块的执行要先于非静态代码块。 

6. 静态代码块随着类的加载而加载，且只执行一次。 

**非静态代码块**：没有static修饰的代码块

1. 可以有输出语句。 

2. 可以对类的属性、类的声明进行初始化操作。 

3. 除了调用非静态的结构外，还可以调用静态的变量或方法。 

4. 若有多个非静态的代码块，那么按照从上到下的顺序依次执行。 

5. 每次创建对象的时候，都会执行一次。且先于构造器执行。

**静态初始化块举例** 

```java
class Person {
    public static int total;
    static {
        total = 100;
        System.out.println("in static block!");
    }
}
public class PersonTest {
    public static void main(String[] args) {
        System.out.println("total = " + Person.total);
        System.out.println("total = " + Person.total);
    }
}
输出：
in static block
total=100
total=100
```



总结：程序中成员变量赋值的执行顺序

1. 声明成员变量的默认初始化
2. 显式初始化、多个初始化块依次被执行（同级别下按先后顺序执行）
3. 构造器再对成员进行初始化操作
4. 通过”对象.属性”或”对象.方法”的方式，可多次给属性赋值

### 4.19.抽象类与抽象方法

​		随着继承层次中一个个新子类的定义，类变得越来越具体，而父类则更一般，更通用。类的设计应该保证父类和子类能够共享特征。有时将一个父类设计得非常抽象，以至于它没有具体的实例，这样的类叫做抽象类

+  用abstract关键字来修饰一个类，这个类叫做抽象类。
+  用abstract来修饰一个方法，该方法叫做抽象方法。 
+ 抽象方法：只有方法的声明，没有方法的实现。以分号结束： 比如：`public abstract void talk(); `
+  含有抽象方法的类必须被声明为抽象类。 
+  抽象类不能被实例化。抽象类是用来被继承的，抽象类的子类必须重写父类的抽象方法，并提供方法体。若没有重写全部的抽象方法，仍为抽象类。 
+  不能用abstract修饰变量、代码块、构造器； 
+  不能用abstract修饰私有方法、静态方法、final的方法、final的类

```java
abstract class A {
    abstract void m1();
    public void m2() {
    	System.out.println("A类中定义的m2方法");
    }
}
class B extends A {
    void m1() {
    	System.out.println("B类中定义的m1方法");
    }
}
public class Test {
    public static void main(String args[]) {
        A a = new B();
        a.m1();
        a.m2();
    }
}
```



**应用**：抽象类是用来模型化那些父类无法确定全部实现，而是由其子类提供具体实现的对象的类。

![1676988396321](D:\MyNote\images\1676988396321.png)

在航运公司系统中，Vehicle类需要定义两个方法分别计算运输工具的燃料效率和行驶距离。 

问题：卡车(Truck)和驳船(RiverBarge)的燃料效率和行驶距离的计算方法完全不同。Vehicle类不能提供计算方法，但子类可以

解决方案：Java允许类设计者指定：超类声明一个方法但不提供实现，该方法的实现由子类提供这样的方法称为抽象方法。有一个或更多抽象方法的类称为抽象类。

Vehicle是一个抽象类，有两个抽象方法

```java
public abstract class Vehicle{
    public abstract double calcFuelEfficiency(); //计算燃料效率的抽象方法
    public abstract double calcTripDistance(); //计算行驶距离的抽象方法
}
public class Truck extends Vehicle{
    public double calcFuelEfficiency( ) { //写出计算卡车的燃料效率的具体方法 }
    public double calcTripDistance( ) { //写出计算卡车行驶距离的具体方法 }
}
public class RiverBarge extends Vehicle{
    public double calcFuelEfficiency( ) { //写出计算驳船的燃料效率的具体方法 }
    public double calcTripDistance( ) { //写出计算驳船行驶距离的具体方法}
}
注意：抽象类不能实例化 new Vihicle()是非法的
```



#### 4.19.1.模板方法设计模式

​		抽象类体现的就是一种模板模式的设计，抽象类作为多个子类的通用模板，子类在抽象类的基础上进行扩展、改造，但子类总体上会保留抽象类的行为方式。

解决的问题：当功能内部一部分实现是确定的，一部分实现是不确定的。这时可以把不确定的部分暴露出去，让子类去实现。换句话说，在软件开发中实现一个算法时，整体步骤很固定、通用，这些步骤已经在父类中写好了。但是某些部分易变，易变部分可以抽象出来，供不同子类实现。这就是一种模板模式

```java
abstract class Template {
    public final void getTime() {
        long start = System.currentTimeMillis();
        code();
        long end = System.currentTimeMillis();
        System.out.println("执行时间是：" + (end - start));
    }
    public abstract void code();
}
class SubTemplate extends Template {
    public void code() {
        for (int i = 0; i < 10000; i++) {
        	System.out.println(i);
        }
    }
}
```

​		模板方法设计模式是编程中经常用得到的模式。各个框架、类库中都有他的影子，比如常见的有：

+  数据库访问的封装 
+  Junit单元测试 
+  JavaWeb的Servlet中关于doGet/doPost方法调用 
+  Hibernate中模板程序 
+  Spring中JDBCTemlate、HibernateTemplate等

### 4.20.接 口

+ 一方面，有时必须从几个类中派生出一个子类，继承它们所有的属性和方法。但是，Java不支持多重继承。有了接口，就可以得到多重继承的效果。 
+ 另一方面，有时必须从几个类中抽取出一些共同的行为特征，而它们之间又没有is-a的关系，仅仅是具有相同的行为特征而已。例如：鼠标、键盘、打印机、扫描仪、摄像头、充电器、MP3机、手机、数码相机、移动硬盘等都支持USB连接。 
+ 接口就是规范，定义的是一组规则，体现了现实世界中“如果你是/要...则必须能...”的思想。继承是一个"是不是"的关系，而接口实现则是 "能不能" 的关系。 
+ 接口的本质是契约，标准，规范，就像我们的法律一样。制定好后大家都要遵守。
+ 接口(interface)是抽象方法和常量值定义的集合。

接口的**特点**：

+ 用interface来定义。 
+ 接口中的所有成员变量都默认是由public static final修饰的。 
+ 接口中的所有抽象方法都默认是由public abstract修饰的。 
+ 接口中没有构造器。 
+ 接口采用多继承机制。

```java
public interface Runner {
    int ID = 1;
    void start();
    public void run();
    void stop();
}
等价于下面
public interface Runner {
    public static final int ID = 1;
    public abstract void start();
    public abstract void run();
    public abstract void stop();
}
```

+  定义Java类的语法格式：先写extends，后写implements

   `class SubClass extends SuperClass implements InterfaceA{ }`

+ 一个类可以实现多个接口，接口也可以继承其它接口。

+  实现接口的类中必须提供接口中所有方法的具体实现内容，方可实例化。否则，仍为抽象类。

+  接口的主要用途就是被实现类实现。（面向接口编程）

+  与继承关系类似，接口与实现类之间存在多态性

+  接口和类是并列关系，或者可以理解为一种特殊的类。从本质上讲，接口是一种特殊的抽象类，这种抽象类中只包含常量和方法的定义(JDK7.0及之前)，而没有变量和方法的实现

<img src="D:\MyNote\images\1676989431457.png" alt="1676989431457" style="zoom: 50%;" />

```java
interface Runner {
    public void start();
    public void run();
    public void stop();
}
class Person implements Runner {
    public void start() {
    // 准备工作：弯腰、蹬腿、咬牙、瞪眼
    // 开跑
    }
    public void run() {
    // 摆动手臂
    // 维持直线方向
    }
    public void stop() {
    // 减速直至停止、喝水。
    }
}
```

```java
一个类可以实现多个无关的接口
interface Runner { public void run();}
interface Swimmer {public double swim();}
class Creator{public int eat(){…}} 
class Man extends Creator implements Runner ,Swimmer{
    public void run() {……}
    public double swim() {……}
    public int eat() {……}
}
与继承关系类似，接口与实现类之间存在多态性
public class Test{
    public static void main(String args[]){
        Test t = new Test();
        Man m = new Man();
        t.m1(m);
        t.m2(m);
        t.m3(m);
    }
    public String m1(Runner f) { f.run(); }
    public void m2(Swimmer s) {s.swim();}
    public void m3(Creator a) {a.eat();}
}
```



#### 4.20.1.代理模式

​		代理模式是Java开发中使用较多的一种设计模式。代理设计就是为其他对象提供一种代理以控制对这个对象的访问。

```java
interface Network {
	public void browse();
}
// 被代理类
class RealServer implements Network {
    @Override
    public void browse() {
        System.out.println("真实服务器上网浏览信息");
    }
}
// 代理类
class ProxyServer implements Network {
    private Network network;
    public ProxyServer(Network network) {
    	this.network = network;
    }
    public void check() {
    	System.out.println("检查网络连接等操作");
    }
    public void browse() {
        check();
        network.browse();
    }
}
public class ProxyDemo {
    public static void main(String[] args) {
        Network net = new ProxyServer(new RealServer());
        net.browse();
    }
}
```

**应用场景**：

+  安全代理：屏蔽对真实角色的直接访问。
+  远程代理：通过代理类处理远程方法调用（RMI） 
+  延迟加载：先加载轻量级的代理对象，真正需要再加载真实对象

​        比如你要开发一个大文档查看软件，大文档中有大的图片，有可能一个图片有100MB，在打开文件时，不可能将所有的图片都显示出来，这样就可以使用代理模式，当需要查看图片时，用proxy来进行大图片的打开。

**分类**：

+  静态代理（静态定义代理类） 
+  动态代理（动态生成代理类） JDK自带的动态代理，需要反射等知识

**接口和抽象类之间的对比** 

![1676989932453](D:\MyNote\images\1676989932453.png)

在开发中，常看到一个类不是去继承一个已经实现好的类，而是要么继承抽象类，要么实现接口

**Java 8中关于接口的改进**：Java 8中，你可以为接口添加静态方法和默认方法。从技术角度来说，这是完
全合法的，只是它看起来违反了接口作为一个抽象定义的理念。

**静态方法：**使用 static 关键字修饰。可以通过接口直接调用静态方法，并执行其方法体。我们经常在相互一起使用的类中使用静态方法。你可以在标准库中找到像Collection/Collections或者Path/Paths这样成对的接口和类。 

**默认方法：**默认方法使用 default 关键字修饰。可以通过实现类对象来调用。 我们在已有的接口中提供新方法的同时，还保持了与旧版本代码的兼容性。 比如：java 8 API中对Collection、List、Comparator等接口提供了丰富的默认方法

```java
public interface AA {
    double PI = 3.14;
    public default void method() {
    	System.out.println("北京");
    }
    default String method1() {
    	return "上海";
    }
    public static void method2() {
    	System.out.println(“hello lambda!");
    }
}
```

**接口中的默认方法** 

​		若一个接口中定义了一个默认方法，而另外一个接口中也定义了一个同名同参数的方法（不管此方法是否是默认方法），在实现类同时实现了这两个接口时，会出现：接口冲突。解决办法：实现类必须覆盖接口中同名同参数的方法，来解决冲突。

​		若一个接口中定义了一个默认方法，而父类中也定义了一个同名同参数的非抽象方法，则不会出现冲突问题。因为此时遵守：**类优先原则。**接口中具有相同名称和参数的默认方法会被忽略。

### 4.21.内部类

+ 当一个事物的内部，还有一个部分需要一个完整的结构进行描述，而这个内部的完整的结构又只为外部事物提供服务，那么整个内部的完整结构最好使用内部类。
+ 在Java中，允许一个类的定义位于另一个类的内部，前者称为内部类，后者称为外部类。
+  Inner class一般用在定义它的类或语句块之内，在外部引用它时必须给出完整的名称。Inner class的名字不能与包含它的外部类类名相同；
+ **分类： 成员内部类**（static成员内部类和非static成员内部类）、 **局部内部类**（不谈修饰符）、匿名内部类

#### 4.21.1.成员内部类

**作为类的成员的角色：** 

+ 和外部类不同，Inner class还可以声明为**private**或**protected**； 

+ 可以调用外部类的结构 

+ Inner class 可以声明为**static**的，但此时就不能再使用外层类的非static的成员变量；

**作为类的角色**：

+ 可以在内部定义属性、方法、构造器等结构 

+ 可以声明为**abstract**类 ，因此可以被其它的内部类继承 

+ 可以声明为**final**的 

+ 编译以后生成OuterClass$InnerClass.class字节码文件（也适用于局部内部类） 

【注意】

1. 非static的成员内部类中的成员不能声明为static的，只有在外部类或static的成员 

内部类中才可声明static成员。 

2. 外部类访问成员内部类的成员，需要“内部类.成员”或“内部类对象.成员”的方式 

3. 成员内部类可以直接使用外部类的所有成员，包括私有的数据 

4. 当想要在外部类的静态成员部分使用内部类时，可以考虑内部类声明为静态的

```java
class Outer {
    private int s;
    public class Inner {
        public void mb() {
            s = 100;
            System.out.println("在内部类Inner中s=" + s);
        }
    }
    public void ma() {
        Inner i = new Inner();
        i.mb();
    }
}
public class InnerTest {
    public static void main(String args[]) {
        Outer o = new Outer();
        o.ma();
    }
}

public class Outer {
    private int s = 111;
    public class Inner {
        private int s = 222;
        public void mb(int s) {
            System.out.println(s); // 局部变量s
            System.out.println(this.s); // 内部类对象的属性s
            System.out.println(Outer.this.s); // 外部类对象属性s
    	}
    }
    public static void main(String args[]) {
        Outer a = new Outer();
        Outer.Inner b = a.new Inner();
        b.mb(333);
    }
}
```



#### 4.21.2.局部内部类 ：

**声明**

```java
class 外部类{
    方法(){
        class 局部内部类{
        }
    }
    {
        class 局部内部类{
        }
    }
}
```

**使用**

+ 只能在声明它的方法或代码块中使用，而且是先声明后使用。除此之外的任何地方都不能使用该类 
+ 但是它的对象可以通过外部方法的返回值返回使用，返回值类型只能是局部内部类的父类或父接口类型

**特点** 

+ 内部类仍然是一个独立的类，在编译之后内部类会被编译成独立的.class文件，但 是前面冠以外部类的类名和$符号，以及数字编号。 

+ 只能在声明它的方法或代码块中使用，而且是先声明后使用。除此之外的任何地方都不能使用该类。 

+ 局部内部类可以使用外部类的成员，包括私有的。 

+ 局部内部类可以使用外部方法的局部变量，但是必须是final的。由局部内部类和局部变量的声明周期不同所致。 

+ 局部内部类和局部变量地位类似，不能使用public,protected,缺省,private 

+ 局部内部类不能使用static修饰，因此也不能包含静态成员

#### 4.21.3.匿名内部类 

​		匿名内部类不能定义任何静态成员、方法和类，只能创建匿名内部类的一个实例。一个匿名内部类一定是在new的后面，用其隐含实现一个接口或实现一个类。
**格式**：

```java
new 父类构造器（实参列表）|实现接口(){
	//匿名内部类的类体部分
}
```



**特点**

+ 匿名内部类必须继承父类或实现接口
+ 匿名内部类只能有一个对象
+ 匿名内部类对象只能使用多态形式引用

```java
interface A{
    public abstract void fun1();
    }
    public class Outer{
        public static void main(String[] args) {
            new Outer().callInner(new A(){
            //接口是不能new但此处比较特殊是子类对象实现接口，只不过没有为对象取名
                public void fun1() {
                    System.out.println(“implement for fun1");
                }
            });// 两步写成一步了
        }
    public void callInner(A a) {
        a.fun1();
    }
}
```



### 4.22.异常

​		在使用计算机语言进行项目开发的过程中，即使程序员把代码写得尽善尽美，在系统的运行过程中仍然会遇到一些问题，因为很多问题不是靠代码能够避免的，比如：客户输入数据的格式，读取文件是否存在，网络是否始终保持通畅等等

异常：在Java语言中，将程序执行中发生的不正常情况称为“异常” 。 (开发过程中的语法错误和逻辑错误不是异常)

Java程序在执行过程中所发生的异常事件可分为两类：

+ **Error**：Java虚拟机无法解决的严重问题。如：JVM系统内部错误、资源 耗尽等严重情况。比如：StackOverflowError和OOM。一般不编写针对性 的代码进行处理。

+ **Exception:** 其它因编程错误或偶然的外在因素导致的一般性问题，可以使用针对性的代码进行处理。例如： 

  + 空指针访问 
  + 试图读取不存在的文件 

  + 网络连接中断 

  + 数组角标越界

​        对于这些错误，一般有两种**解决方法**：一是遇到错误就终止程序 的运行。另一种方法是由程序员在编写程序时，就考虑到错误的检测、错误消息的提示，以及错误的处理。 

捕获错误最理想的是在**编译期间**，但有的错误只有在**运行时**才会发生。比如：除数为0，数组下标越界等。

分类：编译时异常和运行时异常

<img src="D:\MyNote\images\1677135308559.png" alt="1677135308559" style="zoom: 80%;" />

蓝色：非受检(unchecked)异常
红色：受检(checked)异常

1.运行时异常

+ 是指编译器不要求强制处置的异常。一般是指编程时的逻辑错误，是程序员应该积极避免其出现的异常。**java.lang.RuntimeException**类及它的子类都是运行时异常

+ 对于这类异常，可以不作处理，因为这类异常很普遍，若全处理可能会对程序的可读性和运行效率产生影响

2.编译时异常

+ 是指编译器要求必须处置的异常。即程序在运行时由于外界因素造成的一般性异常。编译器要求Java程序必须捕获或声明所有编译时异常。 

+ 对于这类异常，如果程序不处理，可能会带来意想不到的结果。

#### 4.22.1.常见异常

+  java.lang.RuntimeException
  + ClassCastException 
  + ArrayIndexOutOfBoundsException
  + NullPointerException 
  + ArithmeticException 
  + NumberFormatException 
  + InputMismatchException 
  + 。。。 

+  java.io.IOExeption
  + FileNotFoundException
  + EOFException
+ java.lang.ClassNotFoundException 
+ java.lang.InterruptedException 
+ java.io.FileNotFoundException 
+ java.sql.SQLException

**ArrayIndexOutOfBoundsException**

```java
public class IndexOutExp {
    public static void main(String[] args) {
        String friends[] = { "lisa", "bily", "kessy" };
        for (int i = 0; i < 5; i++) {
        	System.out.println(friends[i]); // friends[4]?
        }
        System.out.println("\nthis is the end");
    }
}
程序IndexOutExp.java编译正确，运行结果：java IndexOutExp
lisa
bily
kessy
java.lang.ArrayIndexOutOfBoundsException
at Test7_1.main(Test7_1.java:5)
Exception in thread "main"
```

**NullPointerException**

```java
public class NullRef {
    int i = 1;
    public static void main(String[] args) {
        NullRef t = new NullRef();
        t = null;
        System.out.println(t.i);
    }
}
程序NullRef.java编译正确，运行结果：java NullRef
java.lang.NullPointerException
at NullRef.main(NullRef.java:6)
Exception in thread "main"
```

**ArithmeticException**

```java
public class DivideZero {
    int x;
    public static void main(String[] args) {
        int y;
        DivideZero c=new DivideZero();
        y=3/c.x; 
        System.out.println("program ends ok!");
    }
}
程序DivideZero.java编译正确，运行结果：java DivideZero
java.lang.ArithmeticException: / by zero
at DivideZero.main(DivideZero.java:6)
Exception in thread "main"
```

**ClassCastException**

```java
public class Order {
    public static void main(String[] args) {
        Object obj = new Date();
        Order order;
        order = (Order) obj;
        System.out.println(order);
    }
}
程序Person.java编译正确，运行结果：java Person
java.lang. java.lang.ClassCastException
at Person.main(Person.java:5)
Exception in thread "main"
```



#### 4.22.2.异常处理机制一

​		在编写程序时，经常要在可能出现错误的地方加上检测的代码，如进行x/y运算时，要检测分母为0，数据为空，输入的不是数据而是字符等。过多的if-else分支会导致程序的代码加长、臃肿，可读性差。因此采用异常处理机制。

​		Java采用的异常处理机制，是将异常处理的程序代码集中在一起，与正常的程序代码分开，使得程序简洁、优雅，并易于维护。

Java异常处理的方式：

+ 方式一：try-catch-finally
+ 方式二：throws + 异常类型

​        Java提供的是异常处理的**抓抛模型**。Java程序的执行过程中如出现异常，会生成一个异常类对象， 该异常对象将被提交给Java运行时系统，这个过程称为抛出 (throw)异常

异常对象的生成：

+ 由虚拟机**自动生成**：程序运行过程中，虚拟机检测到程序发生了问题，如果在当前代码中没有找到相应的处理程序，就会在后台自动创建一个对应异常类的实例对象并抛出——自动抛出

+ 由开发人员**手动创建**：Exception exception = new ClassCastException();——创建好的异常对象不抛出对程序没有任何影响，和创建一个普通对象一样

异常**处理机制**：为保证程序正常执行，代码必须对可能出现的异常进行处理。

<img src="D:\MyNote\images\1677136029728.png" alt="1677136029728" style="zoom:50%;" />

​		如果一个方法内抛出异常，该异常对象会被抛给调用者方法中处理。如果异常没有在调用者方法中处理，它继续被抛给这个调用 方法的上层方法。这个过程将一直继续下去，直到异常被处理。 这一过程称为捕获(catch)异常。如果一个异常回到main()方法，并且main()也不处理，则程序运行终止。 程序员通常只能处理Exception，而对Error无能为力。异常处理是通过try-catch-finally语句实现的。 

```java
try{
...... //可能产生异常的代码
}
catch( ExceptionName1 e ){
...... //当产生ExceptionName1型异常时的处置措施
}
catch( ExceptionName2 e ){
...... //当产生ExceptionName2型异常时的处置措施
}
[ finally{
...... //无论是否发生异常，都无条件执行的语句
} ]
```

**try**：捕获异常的第一步是用try{…}语句块选定捕获异常的范围，将可能出现异常的代码放在try语句块中。 

**catch** (Exceptiontype e)：在catch语句块中是对异常对象进行处理的代码。每个try语句块可以伴随一个或多个catch语句，用于处理可能产生的不同类型的异常对象。

​        如果明确知道产生的是何种异常，可以用该异常类作为catch的参数；也可以用其父类作为catch的参数。 比 如 ： 可 以 用 ArithmeticException 类 作 为 参 数 的 地 方 ， 就 可 以 用RuntimeException类作为参数，或者用所有异常的父类Exception类作为参数。 但不能是与ArithmeticException类无关的异常，如NullPointerException（catch中的语句将不会执行）。

捕获异常的有关信息：与其它对象一样，可以访问一个异常对象的成员变量或调用它的方法。

+ getMessage() 获取异常信息，返回字符串
+ printStackTrace() 获取异常类名和异常信息，以及异常出现在程序中的位置。返回值void。 

<img src="D:\MyNote\images\1677136301151.png" alt="1677136301151" style="zoom:80%;" />

**finally** 

+ 捕获异常的最后一步是通过finally语句为异常处理提供一个统一的出口，使得在控制流转到程序的其它部分以前，能够对程序的状态作统一的管理。 
+ 不论在try代码块中是否发生了异常事件，catch语句是否执 行，catch语句是否有异常，catch语句中是否有return，finally块中的语句都会被执行。 
+ finally语句和catch语句是任选的

<img src="D:\MyNote\images\1677136375931.png" alt="1677136375931" style="zoom:80%;" />

```java
public class IndexOutExp {
    public static void main(String[] args) {
        String friends[] = { "lisa", "bily", "kessy" };
        try {
            for (int i = 0; i < 5; i++) {
                System.out.println(friends[i]);
            }
        } catch (ArrayIndexOutOfBoundsException e) {
       		System.out.println("index err");
        }
        System.out.println("\nthis is the end");
    }
}
程序IndexOutExp.java运行结果：java IndexOutExp
lisa
bily
kessy
index err
this is the end

public class DivideZero1 {
    int x;
    public static void main(String[] args) {
        int y;
        DivideZero1 c = new DivideZero1();
        try {
        	y = 3 / c.x;
        } catch (ArithmeticException e) {
        	System.out.println("divide by zero error!");
        }
        System.out.println("program ends ok!");
    }
}
程序DivideZero1运行结果：java DivideZero1
divide by zero error!
program ends ok!
```



**不捕获异常时的情况**：

+ 前面使用的异常都是RuntimeException类或是它的子类，这些类的异常的特点是：即使没有使用try和catch捕获，Java自己也能捕获，并且编译通过( 但运行时会发生异常使得程序运行终止 )

+ 如果抛出的异常是IOException等类型的非运行时异常，则必须捕获，否则编译错误。也就是说，我们必须处理编译时异常，将异常进行捕捉，转化为运行时异常



#### 4.22.3.异常处理机制二

​		声明抛出异常是Java中处理异常的第二种方式。如果一个方法(中的语句执行时)可能生成某种异常，但是并不能确定如何处理这种异常，则此方法应显示地声明抛出异常，表明该方法将不对这些异常进行处理， 而由该方法的调用者负责处理。在方法声明中用throws语句可以声明抛出异常的列表，throws后面的异常类型可以是方法中产生的异常类型，也可以是它的父类。 

```java
public void readFile(String file) throws FileNotFoundException {
    ……
    // 读文件的操作可能产生FileNotFoundException类型的异常
    FileInputStream fis = new FileInputStream(file);
    ..……
}

import java.io.*;
public class ThrowsTest {
    public static void main(String[] args) {
        ThrowsTest t = new ThrowsTest();
        try {
            t.readFile();
        } catch (IOException e) {
            e.printStackTrace();
        }
	}
	public void readFile() throws IOException {
        FileInputStream in = new FileInputStream("atguigushk.txt");
        int b;
        b = in.read();
        while (b != -1) {
            System.out.print((char) b);
            b = in.read();
        }
        in.close();
    }
}
```

**重写方法声明抛出异常的原则**：重写方法不能抛出比被重写方法范围更大的异常类型。在多态的情况下， 对methodA()方法的调用-异常的捕获按父类声明的异常处理。

```java
public class A {
    public void methodA() throws IOException {
    ……
    } 
}
public class B1 extends A {
    public void methodA() throws FileNotFoundException {
    ……
    } 
}
public class B2 extends A {
    public void methodA() throws Exception { //报错
    ……
    } 
}
```

**手动抛出异常** 

​		Java异常类对象除在程序执行过程中出现异常时由系统自动生成并抛出，也可根据需要使用人工创建并抛出

+ 首先要生成异常类对象，然后通过throw语句实现抛出操作(提交给Java运行环境)。

`IOException e = new IOException();
throw e;`

+ 可以抛出的异常必须是Throwable或其子类的实例。下面的语句在编译时将会产生语法错误：`throw new String("want to throw");`

#### 4.22.4.用户自定义异常类

+  一般地，用户自定义异常类都是RuntimeException的子类。
+ 自定义异常类通常需要编写几个重载的构造器。 
+ 自定义异常需要提供serialVersionUID 
+ 自定义的异常通过throw抛出。 
+ 自定义异常最重要的是异常类的名字，当异常出现时，可以根据名字判断异常类型。

用户自定义异常类MyException，用于描述数据取值范围错误信息。用户自己的异常类**必须继承**现有的异常类

```java
例1
class MyException extends Exception {
    static final long serialVersionUID = 13465653435L;
    private int idnumber;
    public MyException(String message, int id) {
        super(message);
        this.idnumber = id;
    }
    public int getId() {
    	return idnumber;
    }
}
例2
public class MyExpTest {
    public void regist(int num) throws MyException {
    if (num < 0)
    	throw new MyException("人数为负值，不合理", 3);
    else
    	System.out.println("登记人数" + num);
    }
    public void manager() {
        try {
        	regist(100);
        } catch (MyException e) {
        	System.out.print("登记失败，出错种类" + e.getId());
        }
        System.out.print("本次登记操作结束");
    }
    public static void main(String args[]) {
        MyExpTest t = new MyExpTest();
        t.manager();
    }
}
```



## 5.多线程

学习要注重场景的使用，同一个知识点在不同场景使用方式可能不一样

### 5.1.程序、进程、线程

+ 程序(program)是为完成特定任务、用某种语言编写的一组指令的集合。即指一段静态的代码，静态对象
+ 进程(process)是程序的一次执行过程，或是正在运行的一个程序。是一个动态的过程：有它自身的产生、存在和消亡的过程。——生命周期
  + 如：运行中的QQ，运行中的MP3播放器 
  + 程序是静态的，进程是动态的 
  + 进程作为资源分配的单位，系统在运行时会为每个进程分配不同的内存区域
+ 线程(thread)，进程可进一步细化为线程，是一个程序内部的一条执行路径。
  + 若一个进程同一时间**并行**执行多个线程，就是支持多线程的 
  + 线程作为调度和执行的单位，每个线程拥有独立的运行栈和程序计数器(pc)，线程切换的开销小 
  + 一个进程中的多个线程共享相同的内存单元/内存地址空间它们从同一堆中分配对象，可以访问相同的变量和对象。这就使得线程间通信更简便、高效。但多个线程操作共享的系统资源可能就会带来安全的隐患。

单核CPU和多核CPU的理解：

+ 单核CPU，其实是一种假的多线程，因为在一个时间单元内，也只能执行一个线程的任务。例如：虽然有多车道，但是收费站只有一个工作人员在收费，只有收了费才能通过，那么CPU就好比收费人员。如果有某个人不想交钱，那么收费人员可以把他“挂起”（晾着他，等他想通了，准备好了钱，再去收费）。但是因为CPU时间单元特别短，因此感觉不出来
+ 如果是多核的话，才能更好的发挥多线程的效率。（现在的服务器都是多核的） 
+ 一个Java应用程序java.exe，其实至少有三个线程：main()主线程，gc()垃圾回收线程，异常处理线程。当然如果发生异常，会影响主线程

并行与并发：

+ **并行：**多个CPU同时执行多个任务。比如：多个人同时做不同的事
+ **并发：**一个CPU(采用时间片)同时执行多个任务。比如：秒杀、多个人做同一件事

**使用多线程的优点**：

1. 提高应用程序的响应。对图形化界面更有意义，可增强用户体验。
2. 提高计算机系统CPU的利用率
3. 改善程序结构。将既长又复杂的进程分为多个线程，独立运行，利于理解和修改

出现原因：

+ 程序需要同时执行两个或多个任务。 
+ 程序需要实现一些需要等待的任务时，如用户输入、文件读写操作、网络操作、搜索等。 
+ 需要一些后台运行的程序时。

### 5.2.线程的2种创建方式

Java语言的JVM允许程序运行多个线程，它通过java.lang.Thread类来体现

Thread类的特性 ：

1. 每个线程都是通过某个特定Thread对象的run()方法来完成具体操作的，经常把run()方法的主体称为**线程体**
2. 通过该Thread对象的start()方法来启动这个线程，而非直接调用run()

**Thread类**

**构造器**

1. Thread()：创建新的Thread对象
2. Thread(String threadname)：创建线程并指定线程实例名
3. Thread(Runnable target)：指定创建线程的目标对象，它实现了Runnable接口中的run方法
4. Thread(Runnable target, String name)：创建新的Thread对象

**创建线程的两种方式** 

JDK1.5之前创建新执行线程有两种方法：继承Thread类的方式、实现Runnable接口的方式

**方式一：继承Thread类**

1) 定义子类继承Thread类。
2) 子类中重写Thread类中的run方法。
3) 创建Thread子类对象，即创建了线程对象。
4) 调用线程对象start方法：启动线程，调用run方法

**子线程的创建和启动过程**

<img src="D:\MyNote\images\1677158381735.png" alt="1677158381735" style="zoom:50%;" />

**注意点：** 

1. 如果自己手动调用run()方法，那么就只是普通方法，没有启动多线程模式。 

2. run()方法由JVM调用，什么时候调用，执行的过程控制都有操作系统的CPU调度决定。 

3. 想要启动多线程，必须调用start方法。 

4. 一个线程对象只能调用一次start()方法启动，如果重复调用了，则将抛出以上的异常“IllegalThreadStateException”。

**方式二：实现Runnable接口**

1) 定义子类，实现Runnable接口。
2) 子类中重写Runnable接口中的run方法。
3) 通过Thread类含参构造器创建线程对象。
4) 将Runnable接口的子类对象作为实际参数传递给Thread类的构造器中。
5) 调用Thread类的start方法：开启线程，调用Runnable子类接口的run方法。

**两种方式的联系与区别**

**区别**：

1. 继承Thread：线程代码存放Thread子类run方法中
2. 实现Runnable：线程代码存在接口的子类的run方法

**实现方式的好处**：

1. 避免了单继承的局限性
2. 多个线程可以共享同一个接口实现类的对象，非常适合多个相同线程来处理同一份资源

Thread类的**有关方法**

1. **void start():** 启动线程，并执行对象的run()方法
2. **run():** 线程在被调度时执行的操作 
3. **String getName():** 返回线程的名称 
4. **void setName(String name)**:设置该线程名称 
5. **static Thread currentThread():** 返回当前线程。在Thread子类中就是this，通常用于主线程和Runnable实现类
6. **static void yield()**：线程让步，暂停当前正在执行的线程，把执行机会让给优先级相同或更高的线程，若队列中没有同优先级的线程，忽略此方法 
7. **join()** **：**当某个程序执行流中调用其他线程的 join() 方法时，调用线程将被阻塞，直到 join() 方法加入的 join 线程执行完为止，低优先级的线程也可以获得执行 
8. **static void sleep(long millis)**：(指定时间:毫秒) 令当前活动线程在指定时间段内放弃对CPU控制,使其他线程有机会被执行,时间到后重排队。 抛出InterruptedException异常 
9. **stop():** 强制线程生命期结束，不推荐使用 
10. **boolean isAlive()**：返回boolean，判断线程是否还活着

**调度策略**：**抢占式**：**高优先级的线程抢占**CPU

<img src="D:\MyNote\images\1677240192014.png" alt="1677240192014" style="zoom:80%;" />

Java的调度方法

+ 同优先级线程组成先进先出队列（先到先服务），使用时间片策略
+ 对高优先级，使用优先调度的抢占式策略

**线程的优先级等级**

+ MAX_PRIORITY：10 
+ MIN _PRIORITY：1 
+ NORM_PRIORITY：5

**涉及的方法** 

+ **getPriority()** **：**返回线程优先值 

+ **setPriority(int newPriority)** **：**改变线程的优先级

**说明** 

+ 线程创建时继承父线程的优先级 

+ 低优先级只是获得调度的概率低，并非一定是在高优先级线程之后才被调用

**补充：线程的分类**

Java中的线程分为两类：一种是**守护线程**，一种是**用户线程**。	

+ 它们在几乎每个方面都是相同的，唯一的区别是判断JVM何时离开。 

+ 守护线程是用来服务用户线程的，通过在start()方法前调用**thread.setDaemon(true**)可以把一个用户线程变成一个守护线程。 

+ Java垃圾回收就是一个典型的守护线程。 

+ 若JVM中都是守护线程，当前JVM将退出。 

+ 形象理解：兔死狗烹，鸟尽弓藏

**线程的生命周期**

JDK中用Thread.State类定义了线程的几种状态

​		要想实现多线程，必须在主线程中创建新的线程对象。Java语言使用Thread类及其子类的对象来表示线程，在它的一个完整的生命周期中通常要经历如下的五种状态：

+ **新建：** 当一个Thread类或其子类的对象被声明并创建时，新生的线程对象处于新建状态 
+ **就绪：**处于新建状态的线程被start()后，将进入线程队列等待CPU时间片，此时它已具备了运行的条件，只是没分配到CPU资源 

+ **运行：**当就绪的线程被调度并获得CPU资源时,便进入运行状态， run()方法定义了线程的操作和功能 

+ **阻塞：**在某种特殊情况下，被人为挂起或执行输入输出操作时，让出 CPU 并临时中止自己的执行，进入阻塞状态 

+ **死亡：**线程完成了它的全部工作或线程被提前强制性地中止或出现异常导致结束

![1677240555509](D:\MyNote\images\1677240555509.png)

### 5.3.线程的2种同步方式

多个线程执行的不确定性引起执行结果的不稳定，多个线程对账本的共享，会造成操作的不完整性，会破坏数据。

```java
class Ticket implements Runnable {
    private int tick = 100;
    public void run() {
        while (true) {
            if (tick > 0) {
            System.out.println(Thread.currentThread()
                               .getName() + "售出车票，tick号为：" + tick--);
            } else
                break;
        }
    }
}
class TicketDemo {
    public static void main(String[] args) {
        Ticket t = new Ticket();
        Thread t1 = new Thread(t);
        Thread t2 = new Thread(t);
        Thread t3 = new Thread(t);
        t1.setName("t1窗口");
        t2.setName("t2窗口");
        t3.setName("t3窗口");
        t1.start();
        t2.start();
        t3.start();
    }
}
```

<img src="D:\MyNote\images\1677240819303.png" alt="1677240819303" style="zoom: 50%;" />

1. 多线程出现了安全问题
2. 问题的原因：
当多条语句在操作同一个线程共享数据时，一个线程对多条语句只执行了一部分，还没有执行完，另一个线程参与进来执行。导致共享数据的错误。
3. 解决办法：
对多条操作共享数据的语句，只能让一个线程都执行完，在执行过程中，其他线程不可以参与执行。

**Synchronized**的使用方法

Java对于多线程的安全问题提供了专业的解决方式：同步机制

**1.** **同步代码块：**

```java
synchronized (对象){
// 需要被同步的代码；
}
```

2. synchronized还可以放在方法声明中，表示整个方法为同步方法。

```java
public synchronized void show (String name){ 
….
}
```

**同步机制中的锁**

**同步锁机制：**

​		在《Thinking in Java》中，是这么说的：对于并发工作，你需要某种方式来防止两个任务访问相同的资源（其实就是共享资源竞争）。 防止这种冲突的方法就是当资源被一个任务使用时，在其上加锁。第一个访问某项资源的任务必须锁定这项资源，使其他任务在其被解锁之前，就无法访问它了，而在其被解锁之时，另一个任务就可以锁定并使用它了

synchronized的锁是什么？

1.  任意对象都可以作为同步锁。所有对象都自动含有单一的锁（监视器）。 
2.  同步方法的锁：静态方法（类名.class）、非静态方法（this） 

3. 同步代码块：自己指定，很多时候也是指定为this或类名.class 

**注意：**

+ 必须确保使用同一个资源的**多个线程共用一把锁**，这个非常重要，否则就无法保证共享资源的安全
+ 一个线程类中的所有静态方法共用同一把锁（类名.class），所有非静态方法共用同一把锁（this），同步代码块（指定需谨慎）

**同步的范围**

1、如何找问题，即代码是否存在线程安全？（非常重要）

1）明确哪些代码是多线程运行的代码 

2）明确多个线程是否有共享数据 

3）明确多线程运行代码中是否有多条语句操作共享数据

2、如何解决呢？（非常重要）

​		对多条操作共享数据的语句，只能让一个线程都执行完，在执行过程中，其他线程不可以参与执行。 即所有操作共享数据的这些语句都要放在同步范围中

3、切记：

+ 范围太小：没锁住所有有安全问题的代码
+ 范围太大：没发挥多线程的功能。

**释放锁的操作**

+ 当前线程的同步方法、同步代码块执行结束。 

+ 当前线程在同步代码块、同步方法中遇到break、return终止了该代码块、该方法的继续执行。 

+ 当前线程在同步代码块、同步方法中出现了未处理的Error或Exception，导致异常结束。 

+ 当前线程在同步代码块、同步方法中执行了线程对象的**wait()**方法，当前线程暂停，并释放锁

**不会释放锁的操作**

+ 线程执行同步代码块或同步方法时，程序调用Thread.sleep()、Thread.yield()方法暂停当前线程的执行
+ 线程执行同步代码块时，其他线程调用了该线程的suspend()方法将该线程挂起，该线程不会释放锁（同步监视器）。 应尽量避免使用suspend()和resume()来控制线程

**单例设计模式之懒汉式**(线程安全)

```java
class Singleton {
    private static Singleton instance = null;
    private Singleton(){}
    public static Singleton getInstance(){
        if(instance==null){
            synchronized(Singleton.class){
                if(instance == null){
                	instance=new Singleton();
                } 
            } 
        }
        return instance;
    } 
}
public class SingletonTest{
    public static void main(String[] args){
        Singleton s1=Singleton.getInstance();
        Singleton s2=Singleton.getInstance();
        System.out.println(s1==s2);
    } 
}
```



**线程的死锁问题**

+ 不同的线程分别占用对方需要的同步资源不放弃，都在等待对方放弃自己需要的同步资源，就形成了线程的死锁 
+ 出现死锁后，不会出现异常，不会出现提示，只是所有的线程都处于阻塞状态，无法继续

解决方法：

+ 专门的算法、原则 

+ 尽量减少同步资源的定义 

+ 尽量避免嵌套同步

**Lock(锁)**

+ 从JDK 5.0开始，Java提供了更强大的线程同步机制——通过显式定义同步锁对象来实现同步。同步锁使用Lock对象充当。
+ java.util.concurrent.locks.Lock接口是控制多个线程对共享资源进行访问的工具。锁提供了对共享资源的独占访问，每次只能有一个线程对Lock对象加锁，线程开始访问共享资源之前应先获得Lock对象。
+ ReentrantLock 类实现了 Lock ，它拥有与 synchronized 相同的并发性和内存语义，在实现线程安全的控制中，比较常用的是ReentrantLock，可以显式加锁、释放锁

```
class A{
    private final ReentrantLock lock = new ReenTrantLock();
    public void m(){
        lock.lock();
        try{
            //保证线程安全的代码;
        }
        finally{
            lock.unlock(); 
        }
    }
}
注意：如果同步代码有异常，要将unlock()写入finally语句块
```

**synchronized** **与** **Lock** **的对比**

1. Lock是显式锁（手动开启和关闭锁，别忘记关闭锁），synchronized是隐式锁，出了作用域自动释放 

2. Lock只有代码块锁，synchronized有代码块锁和方法锁 

3. 使用Lock锁，JVM将花费较少的时间来调度线程，性能更好。并且具有更好的扩展性（提供更多的子类）

优先使用顺序：
Lock -> 同步代码块（已经进入了方法体，分配了相应资源）-> 同步方法（在方法体之外）

### 5.4.线程的通信

例 题：使用两个线程打印 1-100。线程1, 线程2 交替打印

```java
class Communication implements Runnable {
    int i = 1;
    public void run() {
        while (true) {
            synchronized (this) {
                notify();
                if (i <= 100) {
                    System.out.println(Thread.currentThread().getName() + ":" + i++);
                } else
                    break;
                try {
                    wait();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```



**wait()** **与** **notify()** **和** **notifyAll()**

+ **wait()**：令当前线程挂起并放弃CPU、同步资源并等待，使别的线程可访问并修改共享资源，而当前线程排队等候其他线程调用notify()或notifyAll()方法唤醒，唤醒后等待重新获得对监视器的所有权后才能继续执行。 

+ **notify()**：唤醒正在排队等待同步资源的线程中优先级最高者结束等待 

+ **notifyAll ()**：唤醒正在排队等待资源的所有线程结束等待

这三个方法只有在synchronized方法或synchronized代码块中才能使用，否则会报 java.lang.IllegalMonitorStateException异常。因为这三个方法必须有锁对象调用，而任意对象都可以作为synchronized的同步锁， 因此这三个方法只能在Object类中声明。

**wait()** **方法**

+ 在当前线程中调用方法： 对象名.wait() 

+ 使当前线程进入等待（某对象）状态 ，直到另一线程对该对象发出 notify (或notifyAll) 为止。 

+ 调用方法的必要条件：当前线程必须具有对该对象的监控权（加锁） 

+ **调用此方法后，当前线程将释放对象监控权 ，然后进入等待** 

+ 在当前线程被notify后，要重新获得监控权，然后从断点处继续代码的执行。

**notify()/notifyAll()**

+ 在当前线程中调用方法： 对象名.notify() 

+ 功能：唤醒等待该对象监控权的一个/所有线程。 

+ 调用方法的必要条件：当前线程必须具有对该对象的监控权（加锁）

**经典例题：生产者/消费者问题**

​		生产者(Productor)将产品交给店员(Clerk)，而消费者(Customer)从店员处取走产品，店员一次只能持有固定数量的产品(比如:20），如果生产者试图 生产更多的产品，店员会叫生产者停一下，如果店中有空位放产品了再通知生产者继续生产；如果店中没有产品了，店员会告诉消费者等一下，如果店中有产品了再通知消费者来取走产品。 

这里可能出现两个问题： 

+ 生产者比消费者快时，消费者会漏掉一些数据没有取到。 

+ 消费者比生产者快时，消费者会取相同的数据

```java
class Clerk { // 售货员
    private int product = 0;
    public synchronized void addProduct() {
        if (product >= 20) {
            try {
                wait();
            } catch (InterruptedException e){
                e.printStackTrace();
            }
        } else {
            product++;
            System.out.println("生产者生产了第" + product + "个产品");
            notifyAll();
        }
    }
    public synchronized void getProduct() {
        if (this.product <= 0) {
            try {
            	wait();
            } catch (InterruptedException e) {
            	e.printStackTrace();
            }
        } else {
            System.out.println("消费者取走了第" + product + "个产品");
            product--;
            notifyAll();
        }
    }
}

class Productor implements Runnable { // 生产者
    Clerk clerk;
    public Productor(Clerk clerk) {
    	this.clerk = clerk;
    }
    public void run() {
        System.out.println("生产者开始生产产品");
        while (true) {
            try {
            	Thread.sleep((int) Math.random() * 1000);
            } catch (InterruptedException e) {
            	e.printStackTrace();
            }
        	clerk.addProduct();
        }
    }
}

class Consumer implements Runnable { // 消费者
    Clerk clerk;
    public Consumer(Clerk clerk) {
    	this.clerk = clerk;
    }
    public void run() {
        System.out.println("消费者开始取走产品");
        while (true) {
            try {
            	Thread.sleep((int) Math.random() * 1000);
            } catch (InterruptedException e) {
            	e.printStackTrace();
            }
            clerk.getProduct();
        }
    }
}

public class ProductTest {
    public static void main(String[] args) {
        Clerk clerk = new Clerk();
        Thread productorThread = new Thread(new Productor(clerk));
        Thread consumerThread = new Thread(new Consumer(clerk));
        productorThread.start();
        consumerThread.start();
    }
}
```



### 5.5.JDK5.0新增线程创建方式

新增方式一：**实现Callable接口**

与使用Runnable相比， Callable功能更强大些 

+ 相比run()方法，可以有返回值 

+ 方法可以抛出异常 

+ 支持泛型的返回值 

+ 需要借助FutureTask类，比如获取返回结果

Future接口 

+ 可以对具体Runnable、Callable任务的执行结果进行取消、查询是否完成、获取结果等。 

+ FutrueTask是Futrue接口的唯一的实现类 

+ FutureTask 同时实现了Runnable, Future接口。它既可以作为Runnable被线程执行，又可以作为Future得到Callable的返回值

**新增方式二：使用线程池**

**背景：**经常创建和销毁、使用量特别大的资源，比如并发情况下的线程，对性能影响很大。 

**思路：**提前创建好多个线程，放入线程池中，使用时直接获取，使用完放回池中。可以避免频繁创建销毁、实现重复利用。类似生活中的公共交通工具。 

**好处：** 

+ 提高响应速度（减少了创建新线程的时间） 

+ 降低资源消耗（重复利用线程池中线程，不需要每次都创建） 

+ 便于线程管理 

+ corePoolSize：核心池的大小 

+ maximumPoolSize：最大线程数 

+ keepAliveTime：线程没有任务时最多保持多长时间后会终止

**线程池相关API**

+ JDK 5.0起提供了线程池相关API：**ExecutorService** 和 **Executors** 

+ ExecutorService：真正的线程池接口。常见子类ThreadPoolExecutor 
  + void execute(Runnable command) ：执行任务/命令，没有返回值，一般用来执行Runnable 
  + <T> Future<T> submit(Callable<T> task)：执行任务，有返回值，一般用来执行Callable 
  + void shutdown() ：关闭连接池 

+ Executors：工具类、线程池的工厂类，用于创建并返回不同类型的线程池 
  + Executors.newCachedThreadPool()：创建一个可根据需要创建新线程的线程池 
  + Executors.newFixedThreadPool(n); 创建一个可重用固定线程数的线程池 
  + Executors.newSingleThreadExecutor() ：创建一个只有一个线程的线程池 
  + Executors.newScheduledThreadPool(n)：创建一个线程池，它可安排在给定延迟后运行命令或者定期地执行

## 6.常用类

### 6.1.字符串相关的

#### 6.1.1.String

特性：

+ String类：代表字符串。Java 程序中的所有字符串字面值（如 "abc" ）都作为此类的实例实现。 

+ String是一个final类，代表不可变的字符序列。 

+ 字符串是常量，用双引号引起来表示。它们的值在创建之后不能更改。 

+ String对象的字符内容是存储在一个字符数组value[]中的
+ 字符串常量存储在字符串常量池，目的是共享
+ 字符串非常量对象存储在堆中。

```java
public final class String
    implements java.io.Serializable, Comparable<String>, CharSequence {
    /** The value is used for character storage. */
    private final char value[];
```

创建方式及底层实现：

```java
String str = "hello";
//本质上this.value = new char[0];
String s1 = new String(); 
//this.value = original.value;
String s2 = new String(String original); 
//this.value = Arrays.copyOf(value, value.length);
String s3 = new String(char[] a); 
String s4 = new String(char[] a,int startIndex,int count);
```

![1677591600338](D:\MyNote\images\1677591600338.png)

+ 常量与常量的拼接结果在常量池。且常量池中不会存在相同内容的常量。 

+ 只要其中有一个是变量，结果就在堆中 

+ 如果拼接的结果调用intern()方法，返回值就在常量池中

String**使用陷阱**

+ String s1 = "a";  

说明：在字符串常量池中创建了一个字面量为"a"的字符串。 

+ s1 = s1 + "b";  

说明：实际上原来的“a”字符串对象已经丢弃了，现在在堆空间中产生了一个字符串s1+"b"（也就是"ab")。如果多次执行这些改变串内容的操作，会导致大量副本字符串对象存留在内存中，降低效率。如果这样的操作放到循环中，会极大影响 程序的性能。 

+ String s2 = "ab"; 

说明：直接在字符串常量池中创建一个字面量为"ab"的字符串。 

+ String s3 = "a" + "b"; 

说明：s3指向字符串常量池中已经创建的"ab"的字符串。 

+ String s4 = s1.intern(); 

说明：堆空间的s1对象在调用intern()之后，会将常量池中已经存在的"ab"字符串赋值给s4。

**常用方法**

+ int length()：返回字符串的长度： return value.length
+ char charAt(int index)： 返回某索引处的字符return value[index]
+ String toLowerCase()：使用默认语言环境，将 String 中的所有字符转换为小写
+ String toUpperCase()：使用默认语言环境，将 String 中的所有字符转换为大写
+ String trim()：返回字符串的副本，忽略前导空白和尾部空白
+ boolean equals(Object obj)：比较字符串的内容是否相同
+ boolean equalsIgnoreCase(String anotherString)：与equals方法类似，忽略大小写
+ String concat(String str)：将指定字符串连接到此字符串的结尾。 等价于用“+”
+ int compareTo(String anotherString)：比较两个字符串的大小
+ String substring(int beginIndex)：返回一个新的字符串，它是此字符串的从beginIndex开始截取到最后的一个子字符串。
+ String substring(int beginIndex, int endIndex) ：返回一个新字符串，它是此字符串从beginIndex开始截取到endIndex(不包含)的一个子字符串。

+ boolean endsWith(String suffix)：测试此字符串是否以指定的后缀结束
+ boolean startsWith(String prefix)：测试此字符串是否以指定的前缀开始
+ boolean startsWith(String prefix, int toffset)：测试此字符串从指定索引开始的子字符串是否以指定前缀开始
+ boolean contains(CharSequence s)：当且仅当此字符串包含指定的 char 值序列时，返回 true
+ int indexOf(String str)：返回指定子字符串在此字符串中第一次出现处的索引
+ int indexOf(String str, int fromIndex)：返回指定子字符串在此字符串中第一次出现处的索引，从指定的索引开始
+ int lastIndexOf(String str)：返回指定子字符串在此字符串中最右边出现处的索引
+ int lastIndexOf(String str, int fromIndex)：返回指定子字符串在此字符串中最后一次出现处的索引，从指定的索引开始反向搜索

注：indexOf和lastIndexOf方法如果未找到都是返回-1

+ String replace(char oldChar, char newChar)：返回一个新的字符串，它是通过用 newChar 替换此字符串中出现的所有 oldChar 得到的。
+ String replace(CharSequence target, CharSequence replacement)：使用指定的字面值替换序列替换此字符串所有匹配字面值目标序列的子字符串。
+ String replaceAll(String regex, String replacement) ： 使用给定的replacement 替换此字符串所有匹配给定的正则表达式的子字符串。
+ String replaceFirst(String regex, String replacement) ： 使 用 给 定 的replacement 替换此字符串匹配给定的正则表达式的第一个子字符串。
+ boolean matches(String regex)：告知此字符串是否匹配给定的正则表达式。
+ String[] split(String regex)：根据给定正则表达式的匹配拆分此字符串。
+ String[] split(String regex, int limit)：根据匹配给定的正则表达式来拆分此字符串，最多不超过limit个，如果超过了，剩下的全部都放到最后一个元素中。

**String与基本数据类型转换**

字符串 -> 基本数据类型、包装类

+ Integer包装类的public static int parseInt(String s)：可以将由“数字”字符组成的字符串转换为整型。
+ 类似地,使用java.lang包中的Byte、Short、Long、Float、Double类调相应的类方法可以将由“数字”字符组成的字符串，转化为相应的基本数据类型。

基本数据类型、包装类 -> 字符串

+ 调用String类的public String valueOf(int n)可将int型转换为字符串
+ 相应的valueOf(byte b)、valueOf(long l)、valueOf(float f)、valueOf(double d)、valueOf(boolean b)可由参数的相应类型到字符串的转换

**String与字符数组转换**

 字符数组 -> 字符串

+ String 类的构造器：String(char[]) 和 String(char[]，int offset，int length) 分别用字符数组中的全部字符和部分字符创建字符串对象。
+ String(byte[])：通过使用平台的默认字符集解码指定的 byte 数组，构造一个新的 String。
+ String(byte[]，int offset，int length) ：用指定的字节数组的一部分，即从数组起始位置offset开始取length个字节构造一个字符串对象。

字符串 -> 字符数组

+ public char[] toCharArray()：将字符串中的全部字符存放在一个字符数组中的方法。
+ public void getChars(int srcBegin, int srcEnd, char[] dst, int dstBegin)：提供了将指定索引范围内的字符串存放到数组中的方法。
+ public byte[] getBytes() ：使用平台的默认字符集将此 String 编码为byte 序列，并将结果存储到一个新的 byte 数组中。
+ public byte[] getBytes(String charsetName) ：使用指定的字符集将此 String 编码到 byte 序列，并将结果存储到新的 byte 数组

#### 6.1.2.StringBuffer

+ java.lang.StringBuffer代表**可变的字符序列**，JDK1.0中声明，可以对字符串内容进行增删，此时不会产生新的对象。 

+ 很多方法与String相同。 

+ 作为参数传递时，方法内部可以改变值。

<img src="D:\MyNote\images\1677595525019.png" alt="1677595525019" style="zoom:67%;" />

StringBuffer类不同于String，其对象必须使用构造器生成。有三个构造器：

+ StringBuffer()：初始容量为16的字符串缓冲区
+ StringBuffer(int size)：构造指定容量的字符串缓冲区
+ StringBuffer(String str)：将内容初始化为指定字符串内容

```java
String s = new String("我喜欢学习"); 
StringBuffer buffer = new StringBuffer("我喜欢学习"); 
buffer.append("数学");
```

**常用方法** 

StringBuffer **append**(xxx)：提供了很多的append()方法，用于进行字符串拼接 

StringBuffer **delete**(int start,int end)：删除指定位置的内容 

StringBuffer **replace**(int start, int end, String str)：把[start,end)位置替换为str 

StringBuffer **insert**(int offset, xxx)：在指定位置插入xxx 

StringBuffer **reverse**() ：把当前字符序列逆转

public int **indexOf**(String str) 

public String **substring**(int start,int end) 

public int **length**() 

public char **charAt**(int n ) 

public void **setCharAt**(int n ,char ch)

+ 当append和insert时，如果原来value数组长度不够，可扩容。 

+ 如上这些方法支持方法链操作。 

+ 方法链的原理：

<img src="D:\MyNote\images\1677595650596.png" alt="1677595650596" style="zoom: 67%;" />

#### 6.1.3.StringBuilder

+ StringBuilder 和 StringBuffer 非常类似，均代表可变的字符序列，而且提供相关功能的方法也一样
+ 面试题：对比String、StringBuffer、StringBuilder
  + String(JDK1.0)：不可变字符序列
  + StringBuffer(JDK1.0)：可变字符序列、效率低、线程安全
  + StringBuilder(JDK 5.0)：可变字符序列、效率高、线程不安全

注意：作为参数传递的话，方法内部String不会改变其值，StringBuffer和StringBuilder会改变其值。

### 6.2.日期时间API

#### 6.2.1.JDK8之前

![1677595869425](D:\MyNote\images\1677595869425.png)

1. **java.lang.System类**
		System类提供的public static long currentTimeMillis()用来返回当前时间与1970年1月1日0时0分0秒之间以毫秒为单位的时间差。此方法适于计算时间差。
计算世界时间的主要标准有：
+ UTC(Coordinated Universal Time)
+ GMT(Greenwich Mean Time)
+ CST(Central Standard Time)

2. **java.util.Date类**

   表示特定的瞬间，精确到毫秒 

+ **构造器：** 
  + **Date()**：使用无参构造器创建的对象可以获取本地当前时间。 
  + **Date(long date)** ：使用一个毫秒数初始化时间

+ **常用方法** 
  + **getTime():**返回自 1970 年 1 月 1 日 00:00:00 GMT 以来此 Date 对象表示的毫秒数。 
  + **toString():**把此 Date 对象转换为以下形式的 String： dow mon dd hh:mm:ss zzz yyyy 其中： dow 是一周中的某一天 (Sun, Mon, Tue,  Wed, Thu, Fri, Sat)，zzz是时间标准。 
  + 其它很多方法都过时了。

```java
import java.util.Date;

Date date = new Date();
System.out.println(date);
System.out.println(System.currentTimeMillis());
System.out.println(date.getTime());
Date date1 = new Date(date.getTime());
System.out.println(date1.getTime());
System.out.println(date1.toString());
```

3. **java.text.SimpleDateFormat类**
		Date类的API不易于国际化，大部分被废弃了，java.text.SimpleDateFormat类是一个不与语言环境有关的方式来格式化和解析日期的具体类。 它允许进行格式化：日期->文本、解析：文本->日期

**格式化**：

+ SimpleDateFormat() ：默认的模式和语言环境创建对象
+ public SimpleDateFormat(String pattern)：该构造方法可以用参数pattern指定的格式创建一个对象，该对象调用：
+ public String format(Date date)：方法格式化时间对象date

**解析**：

+ public Date parse(String source)：从给定字符串的开始解析文本，以生成一个日期。

![1677596300078](D:\MyNote\images\1677596300078.png)

```java
Date date = new Date(); // 产生一个Date实例
// 产生一个formater格式化的实例
SimpleDateFormat formater = new SimpleDateFormat();
System.out.println(formater.format(date));// 打印输出默认的格式
SimpleDateFormat formater2 = new SimpleDateFormat("yyyy年MM月dd日 EEE 
HH:mm:ss");
System.out.println(formater2.format(date));
try {
// 实例化一个指定的格式对象
Date date2 = formater2.parse("2008年08月08日 星期一 08:08:08");
// 将指定的日期解析后格式化按指定的格式输出
System.out.println(date2.toString());
} catch (ParseException e) {
e.printStackTrace();
}
```

4. **java.util.Calendar(日历)类**

​         Calendar是一个抽象基类，主用用于完成日期字段之间相互操作的功能。获取Calendar实例的方法有两种：一种是使用Calendar.getInstance()方法 ；一种是调用它的子类GregorianCalendar的构造器。一个Calendar的实例是系统时间的抽象表示，通过get(int field)方法来取得想要的时间信息。比如YEAR、MONTH、DAY_OF_WEEK、HOUR_OF_DAY 、 MINUTE、SECOND.

+ public void set(int field,int value) 

+ public void add(int field,int amount) 

+ public final Date getTime() 

+ public final void setTime(Date date)

**注意**:

+ 获取月份时：一月是0，二月是1，以此类推，12月是11 

+ 获取星期时：周日是1，周二是2 ， 。。。。周六是7

```java
Calendar calendar = Calendar.getInstance();
// 从一个 Calendar 对象中获取 Date 对象
Date date = calendar.getTime();
// 使用给定的 Date 设置此 Calendar 的时间
date = new Date(234234235235L);
calendar.setTime(date);
calendar.set(Calendar.DAY_OF_MONTH, 8);
System.out.println("当前时间日设置为8后,时间是:" + calendar.getTime());
calendar.add(Calendar.HOUR, 2);
System.out.println("当前时间加2小时后,时间是:" + calendar.getTime());
calendar.add(Calendar.MONTH, -2);
System.out.println("当前日期减2个月后,时间是:" + calendar.getTime());
```



#### 6.2.2.JDK8现在

新日期时间API出现的背景：

​		如果我们可以跟别人说：“我们在1502643933071见面，别晚了！”那么就再简单不过了。但是我们希望时间与昼夜和四季有关，于是事情就变复杂了。JDK 1.0中包含了 一个java.util.Date类，但是它的大多数方法已经在JDK 1.1引入Calendar类之后被弃用了。而Calendar并不比Date好多少。它们面临的问题是：

+ 可变性：像日期和时间这样的类应该是不可变的。 

+ 偏移性：Date中的年份是从1900开始的，而月份都从0开始。 

+ 格式化：格式化只对Date有用，Calendar则不行。 

+ 此外，它们也不是线程安全的；不能处理闰秒等。

总结：对日期和时间的操作一直是Java程序员最痛苦的地方之一。

​		第三次引入的API是成功的，并且Java 8中引入的java.time API 已经纠正了过去的缺陷，将来很长一段时间内它都会为我们服务。Java 8 吸收了 Java-Time 的精华，以一个新的开始为 Java 创建优秀的 API。 新的 java.time 中包含了所有关于本地日期（LocalDate）、本地时间（LocalTime）、本地日期时间（LocalDateTime）、时区（ZonedDateTime） 和持续时间（Duration）的类。历史悠久的 Date 类新增了 toInstant() 方法， 用于把 Date 转换成新的表示形式。这些新增的本地化时间日期 API 大大简化了日期时间和本地化的管理。

**新时间日期**API：

java.time – 包含值对象的基础包 

java.time.chrono – 提供对不同的日历系统的访问 

java.time.format – 格式化和解析时间和日期 

java.time.temporal – 包括底层框架和扩展特性 

java.time.zone – 包含时区支持的类

说明：大多数开发者只会用到基础包和format包，也可能会用到temporal包。因此，尽管有68个新的公开类型，大多数开发者，大概将只会用到其中的三分之一。

​        LocalDate、LocalTime、LocalDateTime 类是其中较重要的几个类，它们的实例是不可变的对象，分别表示使用 ISO-8601日历系统的日期、时间、日期和时间。它们提供了简单的本地日期或时间，并不包含当前的时间信息，也不包含与时区相关的信息。

+ LocalDate代表IOS格式（yyyy-MM-dd）的日期,可以存储 生日、纪念日等日期。 

+ LocalTime表示一个时间，而不是日期。 

+ LocalDateTime是用来表示日期和时间的，这是一个最常用的类之一。

注：ISO-8601日历系统是国际标准化组织制定的现代公民的日期和时间的表示法，也就是公历。

![1678460786018](D:\MyNote\images\1678460786018.png)

 **瞬时：**Instant

​		Instant：时间线上的一个瞬时点。 这可能被用来记录应用程序中的事件时间戳。

​		在处理时间和日期的时候，我们通常会想到年,月,日,时,分,秒。然而，这只是时间的一个模型，是面向人类的。第二种通用模型是面向机器的，或者说是连 续的。在此模型中，时间线中的一个点表示为一个很大的数，这有利于计算机处理。在UNIX中，这个数从1970年开始，以秒为的单位；同样的，在Java中，也是从1970年开始，但以毫秒为单位。 

​		java.time包通过值类型Instant提供机器视图，不提供处理人类意义上的时间单位。Instant表示时间线上的一点，而不需要任何上下文信息，例如，时区。概念上讲，它只是简单的表示自1970年1月1日0时0分0秒（UTC）开始的秒数。因为java.time包是基于纳秒计算的，所以Instant的精度可以达到纳秒级。

(1 ns = 10-9 s) 1秒 = 1000毫秒 =10^6微秒=10^9纳秒

![1678461198506](D:\MyNote\images\1678461198506.png)

时间戳是指格林威治时间1970年01月01日00时00分00秒(北京时间1970年01月01日08时00分00秒)起至现在的总秒数

 **格式化与解析日期或时间**

java.time.format.DateTimeFormatter 类：该类提供了三种格式化方法：

+ 预定义的标准格式。如：`ISO_LOCAL_DATE_TIME;ISO_LOCAL_DATE;ISO_LOCAL_TIME`

+ 本地化相关的格式。如：ofLocalizedDateTime(FormatStyle.LONG)
+ 自定义的格式。如：ofPattern(“yyyy-MM-dd hh:mm:ss”)

![1678461497154](D:\MyNote\images\1678461497154.png)



**其它API**

+ ZoneId：该类中包含了所有的时区信息，一个时区的ID，如 Europe/Paris
+ ZonedDateTime：一个在ISO-8601日历系统时区的日期时间，如 2007-12-03T 10:15:30+01:00 Europe/Paris。
  + 其中每个时区都对应着ID，地区ID都为“{区域}/{城市}”的格式，例如：Asia/Shanghai等
+ Clock：使用时区提供对当前即时、日期和时间的访问的时钟。
+ 持续时间：Duration，用于计算两个“时间”间隔
+ 日期间隔：Period，用于计算两个“日期”间隔
+ TemporalAdjuster : 时间校正器。有时我们可能需要获取例如：将日期调整到“下一个工作日”等操作。
+ TemporalAdjusters : 该类通过静态方法(firstDayOfXxx()/lastDayOfXxx()/nextXxx())提供了大量的常用
  TemporalAdjuster 的实现。

```java
//ZoneId:类中包含了所有的时区信息
// ZoneId的getAvailableZoneIds():获取所有的ZoneId
Set<String> zoneIds = ZoneId.getAvailableZoneIds();
for (String s : zoneIds) {
	System.out.println(s);
}
// ZoneId的of():获取指定时区的时间
LocalDateTime localDateTime = LocalDateTime.now(ZoneId.of("Asia/Tokyo"));
System.out.println(localDateTime);
//ZonedDateTime:带时区的日期时间
// ZonedDateTime的now():获取本时区的ZonedDateTime对象
ZonedDateTime zonedDateTime = ZonedDateTime.now();
System.out.println(zonedDateTime);
// ZonedDateTime的now(ZoneId id):获取指定时区的ZonedDateTime对象
ZonedDateTime zonedDateTime1 = ZonedDateTime.now(ZoneId.of("Asia/Tokyo"));
System.out.println(zonedDateTime1);

//Duration:用于计算两个“时间”间隔，以秒和纳秒为基准
LocalTime localTime = LocalTime.now();
LocalTime localTime1 = LocalTime.of(15, 23, 32);
//between():静态方法，返回Duration对象，表示两个时间的间隔
Duration duration = Duration.between(localTime1, localTime);
System.out.println(duration);
System.out.println(duration.getSeconds());
System.out.println(duration.getNano());
LocalDateTime localDateTime = LocalDateTime.of(2016, 6, 12, 15, 23, 32);
LocalDateTime localDateTime1 = LocalDateTime.of(2017, 6, 12, 15, 23, 32);
Duration duration1 = Duration.between(localDateTime1, localDateTime);
System.out.println(duration1.toDays());

//Period:用于计算两个“日期”间隔，以年、月、日衡量
LocalDate localDate = LocalDate.now();
LocalDate localDate1 = LocalDate.of(2028, 3, 18);
Period period = Period.between(localDate, localDate1);
System.out.println(period);
System.out.println(period.getYears());
System.out.println(period.getMonths());
System.out.println(period.getDays());
Period period1 = period.withYears(2);
System.out.println(period1);

// TemporalAdjuster:时间校正器
// 获取当前日期的下一个周日是哪天？
TemporalAdjuster temporalAdjuster = TemporalAdjusters.next(DayOfWeek.SUNDAY);
LocalDateTime localDateTime = LocalDateTime.now().with(temporalAdjuster);
System.out.println(localDateTime);
// 获取下一个工作日是哪天？
LocalDate localDate = LocalDate.now().with(new TemporalAdjuster() {
@Override
public Temporal adjustInto(Temporal temporal) {
LocalDate date = (LocalDate) temporal;
if (date.getDayOfWeek().equals(DayOfWeek.FRIDAY)) {
return date.plusDays(3);
} else if (date.getDayOfWeek().equals(DayOfWeek.SATURDAY)) {
return date.plusDays(2);
} else {
return date.plusDays(1);
}
}
});
System.out.println("下一个工作日是：" + localDate);
```

**参考：**与传统日期处理的转换

![1678462303811](D:\MyNote\images\1678462303811.png)



#### 6.2.3.Java比较器

在Java中经常会涉及到对象数组的排序问题，那么就涉及到对象之间的比较问题。

Java实现对象排序的方式有两种：

+ 自然排序：java.lang.Comparable
+ 定制排序：java.util.Comparator

方式一：自然排序：java.lang.Comparable

+ Comparable接口强行对实现它的每个类的对象进行整体排序。这种排序被称为类的自然排序。
+ 实现 Comparable 的类必须实现 compareTo(Object obj) 方法，两个对象即通过 compareTo(Object obj) 方法的返回值来比较大小。如果当前对象this大于形参对象obj，则返回正整数，如果当前对象this小于形参对象obj，则返回负整数，如果当前对象this等于形参对象obj，则返回零。
+ 实现Comparable接口的对象列表（和数组）可以通过 Collections.sort 或Arrays.sort进行自动排序。实现此接口的对象可以用作有序映射中的键或有序集合中的元素，无需指定比较器。
+ 对于类 C 的每一个 e1 和 e2 来说，当且仅当 e1.compareTo(e2) == 0 与e1.equals(e2) 具有相同的 boolean 值时，类 C 的自然排序才叫做与 equals一致。建议（虽然不是必需的）最好使自然排序与 equals 一致。

**Comparable** **的典型实现**：(默认都是从小到大排列的) 

+ String：按照字符串中字符的Unicode值进行比较 

+ Character：按照字符的Unicode值来进行比较 

+ 数值类型对应的包装类以及BigInteger、BigDecimal：按照它们对应的数值大小进行比较 

+ Boolean：true 对应的包装类实例大于 false 对应的包装类实例 

+ Date、Time等：后面的日期时间比前面的日期时间大

```java
class Goods implements Comparable {
    private String name;
    private double price;
    //按照价格，比较商品的大小
    @Override
    public int compareTo(Object o) {
        if(o instanceof Goods) {
            Goods other = (Goods) o;
            if (this.price > other.price) {
                return 1;
            } else if (this.price < other.price) {
                return -1;
            }
            return 0;
        }
        throw new RuntimeException("输入的数据类型不一致");
    }
    //构造器、getter、setter、toString()方法略
}

public class ComparableTest{
    public static void main(String[] args) {
        Goods[] all = new Goods[4];
        all[0] = new Goods("《红楼梦》", 100);
        all[1] = new Goods("《西游记》", 80);
        all[2] = new Goods("《三国演义》", 140);
        all[3] = new Goods("《水浒传》", 120);
        Arrays.sort(all);
        System.out.println(Arrays.toString(all));
    }
}
```

**方式二：定制排序：**java.util.Comparator

+ 当元素的类型没有实现java.lang.Comparable接口而又不方便修改代码，或者实现了java.lang.Comparable接口的排序规则不适合当前的操作，那么可以考虑使用 Comparator 的对象来排序，强行对多个对象进行整体排序的比较。
+ 重写compare(Object o1,Object o2)方法，比较o1和o2的大小：如果方法返回正整数，则表示o1大于o2；如果返回0，表示相等；返回负整数，表示o1小于o2。
+ 可以将 Comparator 传递给 sort 方法（如 Collections.sort 或 Arrays.sort），从而允许在排序顺序上实现精确控制。
+ 还可以使用 Comparator 来控制某些数据结构（如有序 set或有序映射）的顺序，或者为那些没有自然顺序的对象 collection 提供排序。

```java
Goods[] all = new Goods[4];
all[0] = new Goods("War and Peace", 100);
all[1] = new Goods("Childhood", 80);
all[2] = new Goods("Scarlet and Black", 140);
all[3] = new Goods("Notre Dame de Paris", 120);
Arrays.sort(all, new Comparator() {
    @Override
    public int compare(Object o1, Object o2) {
        Goods g1 = (Goods) o1;
        Goods g2 = (Goods) o2;
        return g1.getName().compareTo(g2.getName());
    }
});
System.out.println(Arrays.toString(all));
```



#### 6.2.4.System类

​		System类代表系统，系统级的很多属性和控制方法都放置在该类的内部。 该类位于java.lang包。由于该类的构造器是private的，所以无法创建该类的对象，也就是无法实例化该类。其内部的成员变量和成员方法都是static的，所以也可以很方便的进行调用。 System类内部包含in、out和err三个成员变量，分别代表标准输入流 (键盘输入)，标准输出流(显示器)和标准错误输出流(显示器)。成员方法有四个：

+ **native long currentTimeMillis()**：

  该方法的作用是返回当前的计算机时间，时间的表达格式为当前计算机时间和GMT时间(格林威治时间)1970年1月1号0时0分0秒所差的毫秒数

+ **void exit(int status)**：

  该方法的作用是退出程序。其中status的值为0代表正常退出，非零代表异常退出。**使用该方法可以在图形界面编程中实现程序的退出功能**等。

+ **void gc()**：

  该方法的作用是请求系统进行垃圾回收。至于系统是否立刻回收，则取决于系统中垃圾回收算法的实现以及系统执行时的情况。

+ **String getProperty(String key)**：

  该方法的作用是获得系统中属性名为key的属性对应的值。系统中常见的属性名以及属性的作用如下表所示：

![1678463407288](D:\MyNote\images\1678463407288.png)

```java
String javaVersion = System.getProperty("java.version");
System.out.println("java的version:" + javaVersion);
String javaHome = System.getProperty("java.home");
System.out.println("java的home:" + javaHome);
String osName = System.getProperty("os.name");
System.out.println("os的name:" + osName);
String osVersion = System.getProperty("os.version");
System.out.println("os的version:" + osVersion);
String userName = System.getProperty("user.name");
System.out.println("user的name:" + userName);
String userHome = System.getProperty("user.home");
System.out.println("user的home:" + userHome);
String userDir = System.getProperty("user.dir");
System.out.println("user的dir:" + userDir);
```



#### 6.2.5.Math类

java.lang.Math提供了一系列静态方法用于科学计算。其方法的参数和返回值类型一般为double型

```java
abs 绝对值
acos,asin,atan,cos,sin,tan 三角函数
sqrt 平方根
pow(double a,doble b) a的b次幂
log 自然对数
exp e为底指数
max(double a,double b)
min(double a,double b)
random() 返回0.0到1.0的随机数
long round(double a) double型数据a转换为long型（四舍五入）
toDegrees(double angrad) 弧度—>角度
toRadians(double angdeg) 角度—>弧度
```



#### 6.2.6.BigInteger与BigDecimal

**BigInteger类**

​		Integer类作为int的包装类，能存储的最大整型值为2 31-1，Long类也是有限的， 最大为![1678463647059](D:\MyNote\images\1678463647059.png)。如果要表示再大的整数，不管是基本数据类型还是他们的包装类都无能为力，更不用说进行运算了。 

​		java.math包的BigInteger可以表示不可变的任意精度的整数。BigInteger 提供所有 Java 的基本整数操作符的对应物，并提供 java.lang.Math 的所有相关方法。另外，BigInteger 还提供以下运算：模算术、GCD 计算、质数测试、素数生成、位操作以及一些其他操作

构造器：**BigInteger**(String val)：根据字符串构建BigInteger对象

**常用方法** 

+ public BigInteger **abs**()：返回此 BigInteger 的绝对值的 BigInteger。 

+ BigInteger **add**(BigInteger val) ：返回其值为 (this + val) 的 BigInteger 

+ BigInteger **subtract**(BigInteger val) ：返回其值为 (this - val) 的 BigInteger 

+ BigInteger **multiply**(BigInteger val) ：返回其值为 (this * val) 的 BigInteger 

+ BigInteger **divide**(BigInteger val) ：返回其值为 (this / val) 的 BigInteger。整数相除只保留整数部分。 

+ BigInteger **remainder**(BigInteger val) ：返回其值为 (this % val) 的 BigInteger。 

+ BigInteger[] **divideAndRemainder**(BigInteger val)：返回包含 (this / val) 后跟 (this % val) 的两个 BigInteger 的数组。 

+ BigInteger **pow**(int exponent) ：返回其值为 (thisexponent) 的 BigInteger。

**BigDecimal类**

​		一般的Float类和Double类可以用来做科学计算或工程计算，但在商业计算中，要求数字精度比较高，故用到java.math.BigDecimal类。BigDecimal类支持不可变的、任意精度的有符号十进制定点数。 

**构造器**：

+ public BigDecimal(double val) 

+ public BigDecimal(String val)

**常用方法** 

+ public BigDecimal **add**(BigDecimal augend) 

+ public BigDecimal **subtract**(BigDecimal subtrahend) 

+ public BigDecimal **multiply**(BigDecimal multiplicand) 

+ public BigDecimal **divide**(BigDecimal divisor, int scale, int roundingMode)

```java
public void testBigInteger() {
    BigInteger bi = new BigInteger("12433241123");
    BigDecimal bd = new BigDecimal("12435.351");
    BigDecimal bd2 = new BigDecimal("11");
    System.out.println(bi);
    // System.out.println(bd.divide(bd2));
    System.out.println(bd.divide(bd2, BigDecimal.ROUND_HALF_UP));
    System.out.println(bd.divide(bd2, 15, BigDecimal.ROUND_HALF_UP));
}
```



## 7.枚举类与注解

### 7.1.枚举类

#### 7.1.1.使用

类的对象只有有限个，确定的。举例如下：

+ 星期：Monday(星期一)、......、Sunday(星期天) 

+ 性别：Man(男)、Woman(女) 

+ 季节：Spring(春节)......Winter(冬天) 

+ 支付方式：Cash（现金）、WeChatPay（微信）、Alipay(支付宝)、BankCard(银行卡)、CreditCard(信用卡) 

+ 就职状态：Busy、Free、Vocation、Dimission 

+ 订单状态：Nonpayment（未付款）、Paid（已付款）、Delivered（已发货）、 Return（退货）、Checked（已确认）Fulfilled（已配货）、 

+ 线程状态：创建、就绪、运行、阻塞、死亡

**当需要定义一组常量时，强烈建议使用枚举类**

​		JDK1.5之前需要自定义枚举类，JDK 1.5 新增的 **enum** **关键字**用于定义枚举类。若枚举只有一个对象, 则可以作为一种单例模式的实现方式。

**枚举类的属性** 

+ 枚举类对象的属性不应允许被改动, 所以应该使用 private final 修饰
+ 枚举类的使用 private final 修饰的属性应该在构造器中为其赋值
+ 若枚举类显式的定义了带参数的构造器, 则在列出枚举值时也必须对应的传入参数

#### 7.1.2.自定义枚举类

**JDK1.5之前自定义枚举类**

1. 私有化类的构造器，保证不能在类的外部创建其对象 

2. 在类的内部创建枚举类的实例。声明为：public static final  

3. 对象如果有实例变量，应该声明为private final，并在构造器中初始化

```java
class Season{
    private final String SEASONNAME;//季节的名称
    private final String SEASONDESC;//季节的描述
    private Season(String seasonName,String seasonDesc){
        this.SEASONNAME = seasonName;
        this.SEASONDESC = seasonDesc;
    }
    public static final Season SPRING = new Season("春天", "春暖花开");
    public static final Season SUMMER = new Season("夏天", "夏日炎炎");
    public static final Season AUTUMN = new Season("秋天", "秋高气爽");
    public static final Season WINTER = new Season("冬天", "白雪皑皑");
}
```



JDK 1.5使用**enum** **关键字**用于定义枚举类

+ 使用 enum 定义的枚举类默认继承了 java.lang.Enum类，因此不能再继承其他类 

+ 枚举类的构造器只能使用 private 权限修饰符 

+ 枚举类的所有实例必须在枚举类中显式列出(**,** **分隔** **;** **结尾**)。列出的实例系统会自动添加 public static final 修饰 

+ 必须在枚举类的第一行声明枚举类对象

​		JDK 1.5 中可以在 switch 表达式中使用Enum定义的枚举类的对象作为表达式, case 子句可以直接使用枚举值的名字, 无需添加枚举类作为限定。

```java
public enum SeasonEnum {
    SPRING("春天","春风又绿江南岸"),
    SUMMER("夏天","映日荷花别样红"),
    AUTUMN("秋天","秋水共长天一色"),
    WINTER("冬天","窗含西岭千秋雪");
    private final String seasonName;
    private final String seasonDesc;
    private SeasonEnum(String seasonName, String seasonDesc) {
        this.seasonName = seasonName;
        this.seasonDesc = seasonDesc;
    }
    public String getSeasonName() {
    	return seasonName;
    }
    public String getSeasonDesc() {
    	return seasonDesc;
    }
}
```



**主要方法**

![1678464814751](D:\MyNote\images\1678464814751.png)

+ values()方法：返回枚举类型的对象数组。该方法可以很方便地遍历所有的枚举值。
+ valueOf(String str)：可以把一个字符串转为对应的枚举类对象。要求字符串必须是枚举类对象的“名字”。如不是，会有运行时异常：IllegalArgumentException。
+ toString()：返回当前枚举类对象常量的名称

#### 7.1.3.实现接口

+ 和普通 Java 类一样，枚举类可以实现一个或多个接口 

+ 若每个枚举值在调用实现的接口方法呈现相同的行为方式，则只要统一实现该方法即可。 

+ 若需要每个枚举值在调用实现的接口方法呈现出不同的行为方式,  则可以让每个枚举值分别来实现该方法

### 7.2.注解

#### 7.2.1.示例

​		从 JDK 5.0 开始, Java 增加了对元数据(MetaData) 的支持, 也就是Annotation(注解) 。Annotation 其实就是代码里的**特殊标记**, 这些标记可以在编译, 类加载, 运行时被读取, 并执行相应的处理。通过使用 Annotation, 程序员 可以在不改变原有逻辑的情况下, 在源文件中嵌入一些补充信息。代码分析工具、开发工具和部署工具可以通过这些补充信息进行验证或者进行部署。Annotation 可以像修饰符一样被使用, 可用于修饰包,类, 构造器, 方法, 成员变量, 参数, 局部变量的声明, 这些信息被保存在 Annotation的 “name=value” 对中。

​		在JavaSE中，注解的使用目的比较简单，例如标记过时的功能，忽略警告等。在JavaEE/Android中注解占据了更重要的角色，例如用来配置应用程序的任何切面，代替JavaEE旧版中所遗留的繁冗代码和XML配置等。未来的开发模式都是基于注解的，JPA是基于注解的，Spring2.5以上都是基于注解的，Hibernate3.x以后也是基于注解的，现在的Struts2有一部分也是基于注解的了，注解是一种趋势，一定程度上可以说：框架 = 注解 + 反射 + 设计模式。

​		使用 Annotation 时要在其前面增加 @ 符号, 并**把该** **Annotation当成一个修饰符使用。**用于修饰它支持的程序元素

**示例一：生成文档相关的注解** 

@author 标明开发该类模块的作者，多个作者之间使用,分割 

@version 标明该类模块的版本 

@see 参考转向，也就是相关主题 

@since 从哪个版本开始增加的 

@param 对方法中某参数的说明，如果没有参数就不能写 

@return 对方法返回值的说明，如果方法的返回值类型是void就不能写 

@exception 对方法可能抛出的异常进行说明 ，如果方法没有用throws显式抛出的异常就不能写 

**其中** 

@param @return 和 @exception 这三个标记都是只用于方法的。 

@param的格式要求：@param 形参名 形参类型 形参说明 

@return 的格式要求：@return 返回值类型 返回值说明 

@exception的格式要求：@exception 异常类型 异常说明 

@param和@exception可以并列多个

```java
package com.annotation.javadoc;
    /**
    * @author shkstart
    * @version 1.0
    * @see Math.java
    */
    public class JavadocTest {
    /**
    * 程序的主方法，程序的入口
    * @param args String[] 命令行参数
    */
    public static void main(String[] args) {
    }
    /**
    * 求圆面积的方法
    * @param radius double 半径值
    * @return double 圆的面积
    */
    public static double getArea(double radius){
    return Math.PI * radius * radius;
    }
}
```

**示例二：在编译时进行格式检查(JDK内置的三个基本注解)**

+ **@Override:** 限定重写父类方法, 该注解只能用于方法 

+ **@Deprecated:** 用于表示所修饰的元素(类, 方法等)已过时。通常是因为所修饰的结构危险或存在更好的选择 

+ **@SuppressWarnings:** 抑制编译器警告

```java
package com.annotation.javadoc;
public class AnnotationTest{
    public static void main(String[] args) {
        @SuppressWarnings("unused")
        int a = 10;
    }
    @Deprecated
    public void print(){
    	System.out.println("过时的方法");
    }
    @Override
    public String toString() {
    	return "重写的toString方法()";
    }
}
```

**示例三：跟踪代码依赖性，实现替代配置文件功能**

Servlet3.0提供了注解(annotation),使得不再需要在web.xml文件中进行Servlet的部署。

```java
@WebServlet("/login")
public class LoginServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws
    ServletException, IOException { }
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws
    ServletException, IOException {
    	doGet(request, response);
    } 
}

<servlet>
    <servlet-name>LoginServlet</servlet-name>
    <servlet-class>com.servlet.LoginServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>LoginServlet</servlet-name>
    <url-pattern>/login</url-pattern>
</servlet-mapping>
```

**spring框架中关于“事务”的管理**

```java
@Transactional(propagation=Propagation.REQUIRES_NEW,isolation=Isolation.READ_COMMITTED,
               readOnly=false,timeout=3)
public void buyBook(String username, String isbn) {
    //1.查询书的单价
    int price = bookShopDao.findBookPriceByIsbn(isbn);
    //2. 更新库存
    bookShopDao.updateBookStock(isbn);
    //3. 更新用户的余额
    bookShopDao.updateUserAccount(username, price);
}

<!-- 配置事务属性 -->
<tx:advice transaction-manager="dataSourceTransactionManager" id="txAdvice">
<tx:attributes>
<!-- 配置每个方法使用的事务属性 -->
<tx:method name="buyBook" propagation="REQUIRES_NEW"
isolation="READ_COMMITTED" read-only="false" timeout="3" />
</tx:attributes>
</tx:advice>
```

#### 7.2.2.自定义注解

+ 定义新的 Annotation 类型使用 **@interface** 关键字
+ 自定义注解自动继承了java.lang.annotation.Annotation接口
+ Annotation 的成员变量在 Annotation 定义中以无参数方法的形式来声明。其方法名和返回值定义了该成员的名字和类型。我们称为配置参数。类型只能是八种基本数据类型、String类型、Class类型、enum类型、Annotation类型、以上所有类型的数组。
+ 可以在定义 Annotation 的成员变量时为其指定初始值, 指定成员变量的初始值可使用 default 关键字
+ 如果只有一个参数成员，建议使用参数名为value
+ 如果定义的注解含有配置参数，那么使用时必须指定参数值，除非它有默认值。格式是“参数名 = 参数值”
  ，如果只有一个参数成员，且名称为value，可以省略“value=”
+ 没有成员定义的 Annotation 称为标记; 包含成员变量的 Annotation 称为元数据 Annotation
  **注意**：自定义注解必须配上注解的信息处理流程才有意义。

```java
@MyAnnotation(value="尚硅谷")
public class MyAnnotationTest {
    public static void main(String[] args) {
        Class clazz = MyAnnotationTest.class;
        Annotation a = clazz.getAnnotation(MyAnnotation.class);
        MyAnnotation m = (MyAnnotation) a;
        String info = m.value();
        System.out.println(info);
    }
}
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
@interface MyAnnotation{
    String value() default "auguigu";
}
```

**JDK** **中的元注解** 

JDK 的元 Annotation 用于修饰其他 Annotation 定义。JDK5.0提供了4个标准的meta-annotation类型，分别是： 

**Retention** 、**Target** 、**Documented** 、**Inherited** 。元数据的理解： String name = “atguigu”;

​		**@Retention:** 只能用于修饰一个 Annotation 定义, 用于指定该 Annotation 的生命周期, @Rentention 包含一个 RetentionPolicy 类型的成员变量, 使用@Rentention 时必须为该 value 成员变量指定值:

+ RetentionPolicy.SOURCE:在源文件中有效（即源文件保留），编译器直接丢弃这种策略的注释
+ RetentionPolicy.CLASS:在class文件中有效（即class保留） ， 当运行 Java 程序时, JVM不会保留注解。 这是默认值
+ RetentionPolicy.RUNTIME:在运行时有效（即运行时保留），当运行 Java 程序时, JVM 会保留注释。程序可以通过反射获取该注释。

![1678466245304](D:\MyNote\images\1678466245304.png)

```java
public enum RetentionPolicy{
    SOURCE,
    CLASS,
    RUNTIME
}

@Retention(RetentionPolicy.SOURCE)
@interface MyAnnotation1{ }
@Retention(RetentionPolicy.RUNTIME)
@interface MyAnnotation2{ }
```

​		**@Target**: 用于修饰 Annotation 定义, 用于指定被修饰的 Annotation 能用于修饰哪些程序元素。 @Target 也包含一个名为 value 的成员变量

![1678466310147](D:\MyNote\images\1678466310147.png)

​		**@Documented:** 用于指定被该元 Annotation 修饰的 Annotation 类将被javadoc 工具提取成文档。默认情况下，javadoc是不包括注解的。 定义为Documented的注解必须设置**Retention值为RUNTIME**。 

​		**@Inherited**: 被它修饰的 Annotation 将具有**继承性**。如果某个类使用了被@Inherited 修饰的 Annotation, 则其子类将自动具有该注解。比如：如果把标有@Inherited注解的自定义的注解标注在类级别上，子类则可以继承父类类级别的注解。实际应用中，使用较少。

#### 7.2.3.利用反射获取注解信息

​		JDK 5.0 在 java.lang.reflect 包下新增了 **AnnotatedElement** **接口**, 该接口**代表程序中可以接受注解的程序元素** 。**当一个** **Annotation** **类型被定义为运行时** **Annotation** **后**, 该注解才是运行时可见, 当 class 文件被载入时保存在 class 文件中的 Annotation 才会被虚拟机读取。程序可以调用 AnnotatedElement对象的如下方法来访问 Annotation 信息。

![1678466526204](D:\MyNote\images\1678466526204.png)

​		Java 8对注解处理提供了两点改进：可重复的注解及可用于类型的注解。此外，反射也得到了加强，在Java8中能够得到方法参数的名称。这会简化标注在方法参数上的注解

**可重复注解示例：**

![1678466735363](D:\MyNote\images\1678466735363.png)

**类型注解**

​		JDK1.8之后，关于元注解@Target的参数类型ElementType枚举值多了两个： **TYPE_PARAMETER,TYPE_USE**。 在Java 8之前，注解只能是在声明的地方所使用，Java8开始，注解可以应用在任何地方。

+ ElementType.TYPE_PARAMETER 表示该注解能写在类型变量的声明语句中（如：泛型声明）。
+ ElementType.TYPE_USE 表示该注解能写在使用类型的任何语句中。 

```java
public class TestTypeDefine<@TypeDefine() U> {
    private U u;
    public <@TypeDefine() T> void test(T t){
    }
}
@Target({ElementType.TYPE_PARAMETER})
@interface TypeDefine{
}

@MyAnnotation
public class AnnotationTest<U> {
    @MyAnnotation
    private String name;
    public static void main(String[] args) {
        AnnotationTest<@MyAnnotation String> t = null;
        int a = (@MyAnnotation int) 2L;
        @MyAnnotation
        int b = 10;
    }
    public static <@MyAnnotation T> void method(T t) {
    }
    public static void test(@MyAnnotation String arg) throws @MyAnnotation Exception {
    }
}
@Target(ElementType.TYPE_USE)
@interface MyAnnotation {
}
```



## 8.集合

​		一方面， 面向对象语言对事物的体现都是以对象的形式，为了方便对多个对象的操作，就要对对象进行存储。另一方面，使用Array存储对象方面具有一些弊端，而Java 集合就像一种容器，可以动态地把多个对象的引用放入容器中。

**数组在内存存储方面的特点：** 1.数组初始化以后，长度就确定了。2.数组声明的类型，就决定了进行元素初始化时的类型。

**数组在存储数据方面的弊端：** 1.数组初始化以后，长度就不可变了，不便于扩展。2.数组中提供的属性和方法少，不便于进行添加、删除、插入等操作，且效率不高。同时无法直接获取存储元素的个数。3.数组存储的数据是有序的、可以重复的，即存储数据的特点单一 

Java 集合类可以用于存储数量不等的多个**对象**，还可用于保存具有映射关系的关联数组

**集合的使用场景**

![1678546574986](D:\MyNote\images\1678546574986.png)

Java 集合可分为 Collection 和 Map 两种体系：

+ **Collection**接口：单列数据，定义了存取一组对象的方法的集合 
  + **List**：元素有序、可重复的集合 
  + **Set**：元素无序、不可重复的集合 

+ **Map**接口：双列数据，保存具有映射关系“key-value对”的集合

**Collection**接口继承树

![1678546693406](D:\MyNote\images\1678546693406.png)

**Map**接口继承树

<img src="D:\MyNote\images\1678546762680.png" alt="1678546762680" style="zoom:50%;" />



### 8.1.Collection

​		Collection 接口是 List、Set 和 Queue 接口的父接口，该接口里定义的方法既可用于操作 Set 集合，也可用于操作 List 和 Queue 集合。JDK不提供此接口的任何直接实现，而是提供更具体的子接口(如：Set和List) 实现。在 Java5 之前，Java 集合会丢失容器中所有对象的数据类型，把所有对象都当成 Object 类型处理；从 JDK 5.0 增加了**泛型**以后，Java 集合可以记住容器中对象的数据类型。 

**接口方法**

1、添加 

+ add(Object obj) 

+ addAll(Collection coll) 

2、获取有效元素的个数 

+ int size() 

3、清空集合 

+ void clear() 

4、是否是空集合 

+ boolean isEmpty() 

5、是否包含某个元素 

+ boolean contains(Object obj)：是通过元素的equals方法来判断是否是同一个对象 

+ boolean containsAll(Collection c)：也是调用元素的equals方法来比较的。拿两个集合的元素挨个比较。

6、删除 

+ boolean remove(Object obj) ：通过元素的equals方法判断是否是要删除的那个元素。只会删除找到的第一个元素 

+ boolean removeAll(Collection coll)：取当前集合的差集 

7、取两个集合的交集 

+ boolean retainAll(Collection c)：把交集的结果存在当前集合中，不影响c 

8、集合是否相等 

+ boolean equals(Object obj) 

9、转成对象数组 

+ Object[] toArray() 

10、获取集合对象的哈希值 

+ hashCode() 

11、遍历 

+ iterator()：返回迭代器对象，用于集合遍历

 **Iterator**迭代器接口

​		Iterator对象称为迭代器(设计模式的一种)，主要用于遍历 Collection 集合中的元素。 GOF给迭代器模式的定义为：提供一种方法访问一个容器(container)对象中各个元素，而又不需暴露该对象的内部细节。**迭代器模式，就是为容器而生。**类似于“公交车上的售票员”、“火车上的乘务员”、“空姐”。 Collection接口继承java.lang.Iterable接口，该接口有一个iterator()方法，那么所有实现了Collection接口的集合类都有一个iterator()方法，用以返回一个实现了 Iterator接口的对象。 Iterator 仅用于遍历集合，Iterator 本身并不提供承装对象的能力。如果需要创建 Iterator 对象，则必须有一个被迭代的集合。集合对象每次调用iterator()方法都得到一个全新的迭代器对象，默认游标都在集合的第一个元素之前。

**Iterator**接口的方法

<img src="D:\MyNote\images\1678587712957.png" alt="1678587712957" style="zoom:80%;" />

<img src="D:\MyNote\images\1678587732616.png" alt="1678587732616" style="zoom:80%;" />

在调用it.next()方法之前必须要调用it.hasNext()进行检测。若不调用，且下一条记录无效，直接调用it.next()会抛出NoSuchElementException异常。

**迭代器的执行原理** 

```java
//hasNext():判断是否还有下一个元素
while(iterator.hasNext()){
    //next():①指针下移 ②将下移以后集合位置上的元素返回
    System.out.println(iterator.next());
}
```

**Iterator接口remove()方法**

```java
Iterator iter = coll.iterator();//回到起点
while(iter.hasNext()){
    Object obj = iter.next();
    if(obj.equals("Tom")){
    	iter.remove();
    }
}
```

注意： 

+ Iterator可以删除集合的元素，但是是遍历过程中通过迭代器对象的remove方法，不是集合对象的remove方法。 

+ 如果还未调用next()或在上一次调用 next 方法之后已经调用了 remove 方法，再调用remove都会报IllegalStateException。

**使用** **foreach** **循环遍历集合元素**

​		Java 5.0 提供了 foreach 循环迭代访问 Collection和数组。 遍历操作不需获取Collection或数组的长度，无需使用索引访问元素。遍历集合的底层调用Iterator完成操作。foreach还可以用来遍历数组。 

```java
for(Person person: persons){
    System.out.println(person.getName());
}
```



### 8.2.List

​		鉴于java数组中数组用来数据的局限性，我们用List来替代数组。List集合里元素是有序的、可重复的，每个元素都有对应的顺序索引，可以通过get()方法获取到对应索引位置的元素。常用的List接口实现类有ArrayList、LinkedList、Vector。

List除了从Collection中继承的方法还有一些自己独有的方法，可以根据索引操作List里面的元素。

+ void add(int index, Object ele):在index位置插入ele元素
+ boolean addAll(int index, Collection eles):从index位置开始将eles中的所有元素添加进来
+ Object get(int index):获取指定index位置的元素
+ int indexOf(Object obj):返回obj在集合中首次出现的位置
+ int lastIndexOf(Object obj):返回obj在当前集合中末次出现的位置
+ Object remove(int index):移除指定index位置的元素，并返回此元素
+ Object set(int index, Object ele):设置指定index位置的元素为ele
+ List subList(int fromIndex, int toIndex):返回从fromIndex到toIndex位置的子集合

#### 8.2.1.ArrayList

​		ArrayList是List接口的主要实现类，本质上是一个变长的数组。在jdk1.7和jdk1.8中实例创建方式表现不一样，1.7中创建时像是饿汉式，直接创建一个容量为10的数组；1.8中则是像懒汉式，先创建一个容量为0的数组，当向里面放入第一个元素时才会变成容量为10的数组。数组可以直接转化为List，Arrays.asList()，它返回的List集合不是ArrayList，而是一个固定长度的List集合。

#### 8.2.2.LinkedList

​		频繁插入与删除时可以选择LinkedList，效率较高。新增如下几个方法：

+ void addFirst(Object obj)：在第一个位置添加元素
+ void addLast(Object obj)：在最后一个位置添加元素
+ Object getFirst()：获取第一个位置的元素
+ Object getLast()：获取最后一个位置的元素
+ Object removeFirst()：移除第一个位置的元素并将其返回
+ Object removeLast()：移除最后一个位置的元素并将其返回

LinkedList的本质是双向链表。里面定义两个Node类型变量： first、last，分别用来记录LinkedList的第一个元素和最后一个元素。而Node除了可以保存当前元素数据，里面还定义了两个Node类型变量： prev、next，分别用来记录当前节点的上一个元素位置和下一个元素位置。

```java
private static class Node<E> {
    E item;
    Node<E> next;
    Node<E> prev;
    Node(Node<E> prev, E element, Node<E> next) {
        this.item = element;
        this.next = next;
        this.prev = prev;
    }
}
```

<img src="D:\MyNote\images\1678799612346.png" alt="1678799612346" style="zoom: 80%;" />

#### 8.2.3.Vector

​		Vector在jdk1.0时就有，结构与ArrayList一样。两者不同之处是Vector是线程安全的，而ArrayList是线程不安全的。

**注意**：使用List时，优先使用ArrayList；当插入、删除频繁时选择LinkedList；Vector效率比较低，总是比ArrayList慢，应尽量少用。

新增方法：

+ void addElement(Object obj)
+ void insertElementAt(Object obj,int index)
+ void setElementAt(Object obj,int index)
+ void removeElement(Object obj)
+ void removeAllElements()

### 8.3.Set

​		Set接口是Collection的子接口，set接口没有提供额外的方法 。Set 集合不允许包含相同的元素，如果试把两个相同的元素加入同一个Set 集合中，则添加操作失败。 Set 判断两个对象是否相同不是使用 == 运算符，而是根据 equals() 方法

#### 8.3.1.HashSet

+ HashSet 是 Set 接口的典型实现，大多数时候使用 Set 集合时都使用这个实现类。
+ HashSet 按 Hash 算法来存储集合中的元素，因此具有很好的存取、查找、删除性能。
+ HashSet 具有以下特点：
  + 不能保证元素的排列顺序
  + HashSet 不是线程安全的
  + 集合元素可以是 null
+ HashSet 集合判断两个元素相等的标准：两个对象通过 hashCode() 方法比较相等，并且两个对象的 equals() 方法返回值也相等。
+ 对于存放在Set容器中的对象，对应的类一定要重写equals()和hashCode(Object obj)方法，以实现对象相等规则。即：“相等的对象必须具有相等的散列码”。

向HashSet中添加元素的过程：

​		当向 HashSet 集合中存入一个元素时，HashSet 会调用该对象的 hashCode() 方法来得到该对象的 hashCode 值，然后根据 hashCode 值，通过某种散列函数决定该对象在 HashSet 底层数组中的存储位置。（这个散列函数会与底层数组的长度相计算得到在数组中的下标，并且这种散列函数计算还尽可能保证能均匀存储元素，越是散列分布，该散列函数设计的越好） 

​		如果两个元素的hashCode()值相等，会再继续调用equals方法，如果equals方法结果为true，添加失败；如果为false，那么会保存该元素，但是该数组的位置已经有元素了，那么会通过链表的方式继续链接 

​		如果两个元素的 equals() 方法返回 true，但它们的 hashCode() 返回值不相等，hashSet 将会把它们存储在不同的位置，但依然可以添加成功

​		HashSet底层也是数组，初始容量为16，当如果使用率超过0.75，（16*0.75=12） 就会扩大容量为原来的2倍。（16扩容为32，依次为64,128....等）

<img src="D:\MyNote\images\1678800402156.png" alt="1678800402156" style="zoom:80%;" />

**重写** **hashCode()** **方法的基本原则**

+ 在程序运行时，同一个对象多次调用 hashCode() 方法应该返回相同的值。 
+ 当两个对象的 equals() 方法比较返回 true 时，这两个对象的 hashCode() 方法的返回值也应相等。
+ 对象中用作 equals() 方法比较的 Field，都应该用来计算 hashCode 值。

**重写** **equals()** **方法的基本原则**

以自定义的Customer类为例，何时需要重写equals()？

​		当一个类有自己特有的“逻辑相等”概念,当改写equals()的时候，总是要改写hashCode()，根据一个类的equals方法（改写后），两个截然不 同的实例有可能在逻辑上是相等的，但是，根据Object.hashCode()方法，它们仅仅是两个对象。因此，违反了“相等的对象必须具有相等的散列码”。

**结论**：复写equals方法的时候一般都需要同时复写hashCode方法。通常参与计算hashCode的对象的属性也应该参与到equals()中进行计算。

**Eclipse/IDEA**工具里hashCode()的重写

以Eclipse/IDEA为例，在自定义类中可以调用工具自动重写equals和hashCode。 

问题：为什么用Eclipse/IDEA复写hashCode方法，有31这个数字？ 

+ 选择系数的时候要选择尽量大的系数。因为如果计算出来的hash地址越大，所谓的“冲突”就越少，查找起来效率也会提高。（减少冲突） 

+ 并且31只占用5bits,相乘造成数据溢出的概率较小。 

+ 31可以 由i*31== (i<<5)-1来表示,现在很多虚拟机里面都有做相关优化。（提高算法效率） 

+ 31是一个素数，素数作用就是如果我用一个数字来乘以这个素数，那么最终出来的结果只能被素数本身和被乘数还有1来整除！(减少冲突)

#### 8.3.2.LinkedHashSet

+ LinkedHashSet 是 HashSet 的子类 

+ LinkedHashSet 根据元素的 hashCode 值来决定元素的存储位置， 但它同时使用双向链表维护元素的次序，这使得元素看起来是以插入顺序保存的。 

+ LinkedHashSet插入性能略低于 HashSet，但在迭代访问 Set 里的全部元素时有很好的性能。 

+ LinkedHashSet 不允许集合元素重复。

LinkedHashSet**底层结构**

```java
Set set = new LinkedHashSet();
set.add(new String("AA"));
set.add(456);
set.add(456);
set.add(new Customer("刘德华", 1001));
```

<img src="D:\MyNote\images\1678804705811.png" alt="1678804705811" style="zoom:67%;" />

#### 8.3.3.TreeSet

+ TreeSet 是 SortedSet 接口的实现类，TreeSet 可以确保集合元素处于排序状态。 

+ TreeSet底层使用**红黑树**结构存储数据 

+ 新增的方法如下： (了解) 
  + Comparator comparator() 

  + Object first() 
  + Object last() 
  + Object lower(Object e) 
  + Object higher(Object e) 
  + SortedSet subSet(fromElement, toElement) 
  + SortedSet headSet(toElement) 
  + SortedSet tailSet(fromElement) 

+ TreeSet 两种排序方法：**自然排序**和**定制排序**。默认情况下，TreeSet 采用自然排序。
+ TreeSet和后面要讲的TreeMap采用红黑树的存储结构
+ 特点：有序，查询速度比List快

再具体就不说了，可以参看http://www.cnblogs.com/yangecnu/p/Introduce-Red-Black-Tree.html， 

对红黑树的讲解写得不错。

<img src="D:\MyNote\images\1678804865991.png" alt="1678804865991" style="zoom:67%;" />

#### 8.3.4.排 序

**自然排序**

+ **自然排序**：TreeSet 会调用集合元素的 compareTo(Object obj) 方法来比较元素之间的大小关系，然后将集合元素按升序(默认情况)排列 

+ 如果试图把一个对象添加到 TreeSet 时，则该对象的类必须实现 Comparable 接口。 
  + 实现 Comparable 的类必须实现 compareTo(Object obj) 方法，两个对象即通过 compareTo(Object obj) 方法的返回值来比较大小。 

+  Comparable 的典型实现： 
  + BigDecimal、BigInteger 以及所有的数值型对应的包装类：按它们对应的数值大小进行比较 
  + Character：按字符的 unicode值来进行比较 
  + Boolean：true 对应的包装类实例大于 false 对应的包装类实例 
  + String：按字符串中字符的 unicode 值进行比较 
  + Date、Time：后边的时间、日期比前面的时间、日期大

+ 向 TreeSet 中添加元素时，只有第一个元素无须比较compareTo()方法，后面添加的所有元素都会调用compareTo()方法进行比较。 

+ **因为只有相同类的两个实例才会比较大小，所以向** **TreeSet** **中添加的应该是同一个类的对象。** 

+ 对于 TreeSet 集合而言，它判断两个对象是否相等的唯一标准是：两个对象通过 compareTo(Object obj) 方法比较返回值。 

+ 当需要把一个对象放入 TreeSet 中，重写该对象对应的 equals() 方法时，应保证该方法与 compareTo(Object obj) 方法有一致的结果：如果两个对象通过equals() 方法比较返回 true，则通过 compareTo(Object obj) 方法比较应返回 0，否则，让人难以理解。

**定制排序**

+ TreeSet的自然排序要求元素所属的类实现Comparable接口，如果元素所属的类没有实现Comparable接口，或不希望按照升序(默认情况)的方式排列元素或希望按照 其它属性大小进行排序，则考虑使用定制排序。定制排序，通过Comparator接口来实现。需要重写compare(T o1,T o2)方法。 

+ 利用int compare(T o1,T o2)方法，比较o1和o2的大小：如果方法返回正整数，则表示o1大于o2；如果返回0，表示相等；返回负整数，表示o1小于o2。 

+ 要实现定制排序，需要将实现Comparator接口的实例作为形参传递给TreeSet的构造器。 

+ 此时，仍然只能向TreeSet中添加类型相同的对象。否则发生ClassCastException异常。 

+ 使用定制排序判断两个元素相等的标准是：通过Comparator比较两个元素返回了0。

### 8.4.Map

**Map接口继承树**

<img src="D:\MyNote\images\1678805246385.png" alt="1678805246385" style="zoom:50%;" />

+ Map与Collection并列存在。用于保存具有**映射关系**的数据:key-value 

+ Map 中的 key 和 value 都可以是任何引用类型的数据 

+ Map 中的 key 用Set来存放，**不允许重复**，即同一个 Map 对象所对应的类，须重写hashCode()和equals()方法 

+ 常用String类作为Map的“键” 

+ key 和 value 之间存在单向一对一关系，即通过指定的 key 总能找到唯一的、确定的 value 

+ Map接口的常用实现类：HashMap、TreeMap、LinkedHashMap和Properties。其中，HashMap是 Map 接口使用频率最高的实现类

**常用方法**

+ **添加、删除、修改操作：** 
  + Object put(Object key,Object value)：将指定key-value添加到(或修改)当前map对象中 
  + void putAll(Map m):将m中的所有key-value对存放到当前map中 
  + Object remove(Object key)：移除指定key的key-value对，并返回value 
  + void clear()：清空当前map中的所有数据 

+ **元素查询的操作：** 
  + Object get(Object key)：获取指定key对应的value 
  + boolean containsKey(Object key)：是否包含指定的key 
  + boolean containsValue(Object value)：是否包含指定的value 
  + int size()：返回map中key-value对的个数 
  + boolean isEmpty()：判断当前map是否为空 
  + boolean equals(Object obj)：判断当前map和参数对象obj是否相等 

+ **元视图操作的方法：** 
  + Set keySet()：返回所有key构成的Set集合 
  + Collection values()：返回所有value构成的Collection集合 
  + Set entrySet()：返回所有key-value对构成的Set集合

```java
Map map = new HashMap();
//map.put(..,..)省略
System.out.println("map的所有key:");
Set keys = map.keySet();// HashSet
for (Object key : keys) {
	System.out.println(key + "->" + map.get(key));
}
System.out.println("map的所有的value：");
Collection values = map.values();
Iterator iter = values.iterator();
while (iter.hasNext()) {
	System.out.println(iter.next());
}
System.out.println("map所有的映射关系：");
// 映射关系的类型是Map.Entry类型，它是Map接口的内部接口
Set mappings = map.entrySet();
for (Object mapping : mappings) {
    Map.Entry entry = (Map.Entry) mapping;
    System.out.println("key是：" + entry.getKey() + "，value是：" + entry.getValue());
}
```



#### 8.4.1.HashMap

+ HashMap是 Map 接口**使用频率最高**的实现类。 

+ 允许使用null键和null值，与HashSet一样，不保证映射的顺序。 

+ 所有的key构成的集合是Set:无序的、不可重复的。所以，key所在的类要重写： equals()和hashCode() 

+ 所有的value构成的集合是Collection:无序的、可以重复的。所以，value所在的类要重写：equals() 

+ 一个key-value构成一个entry 

+ 所有的entry构成的集合是Set:无序的、不可重复的 

+ HashMap **判断两个** **key** **相等的标准**是：两个 key 通过 equals() 方法返回 true，hashCode 值也相等。 

+ HashMap **判断两个** **value**相等的标准是：两个 value 通过 equals() 方法返回 true。

HashMap的存储结构

JDK 7及以前版本：HashMap是数组+链表结构(即为链地址法) ，主要说数组，hashcode相同是放在同一个索引下，多个元素重合时采用链表管理。

JDK 8版本发布以后：HashMap是数组+链表+红黑树实现，主要说数组，hashcode相同是放在同一个索引下，多个元素重合时采用链表管理，当一个链表元素数量超过8个时，链表再转变成红黑树。

Entry[] table 

![1678805855360](D:\MyNote\images\1678805855360.png)

此图为jdk7情况

![1678805916842](D:\MyNote\images\1678805916842.png)

**HashMap源码中的重要常量** 

**DEFAULT_INITIAL_CAPACITY :** HashMap的默认容量，16 

**MAXIMUM_CAPACITY** **：** HashMap的最大支持容量，2^30 

**DEFAULT_LOAD_FACTOR**：HashMap的默认加载因子 

**TREEIFY_THRESHOLD**：Bucket中链表长度大于该默认值，转化为红黑树 

**UNTREEIFY_THRESHOLD**：Bucket中红黑树存储的Node小于该默认值，转化为链表 

**MIN_TREEIFY_CAPACITY**：桶中的Node被树化时最小的hash表容量。（当桶中Node的数量大到需要变红黑树时，若hash表容量小于MIN_TREEIFY_CAPACITY时，此时应执行resize扩容操作这个MIN_TREEIFY_CAPACITY的值至少是TREEIFY_THRESHOLD的4倍。） 

**table**：存储元素的数组，总是2的n次幂 

**entrySet**：存储具体元素的集 

**size**：HashMap中存储的键值对的数量 

**modCount**：HashMap扩容和结构改变的次数。 

**threshold***：扩容的临界值，=容量*填充因子 

**loadFactor**：填充因子

**HashMap的存储结构：JDK 1.8之前**

+ HashMap的内部存储结构其实是**数组和链表的结合**。当实例化一个HashMap时，系统会创建一个长度为Capacity的Entry数组，这个长度在哈希表中被称为容量 (Capacity)，在这个数组中可以存放元素的位置我们称之为“桶”(bucket)，每个bucket都有自己的索引，系统可以根据索引快速的查找bucket中的元素。 

+ 每个bucket中存储一个元素，即一个Entry对象，但每一个Entry对象可以带一个引 用变量，用于指向下一个元素，因此，在一个桶中，就有可能生成一个Entry链。 而且新添加的元素作为链表的head。 

+ 添加元素的过程： 

  ​		向HashMap中添加entry1(key，value)，需要首先计算entry1中key的哈希值(根据key所在类的hashCode()计算得到)，此哈希值经过处理以后，得到在底层Entry[]数组中要存储的位置i。如果位置i上没有元素，则entry1直接添加成功。如果位置i上 已经存在entry2(或还有链表存在的entry3，entry4)，则需要通过循环的方法，依次 比较entry1中key和其他的entry。如果彼此hash值不同，则直接添加成功。如果hash值不同，继续比较二者是否equals。如果返回值为true，则使用entry1的value 去替换equals为true的entry的value。如果遍历一遍以后，发现所有的equals返回都为false,则entry1仍可添加成功。entry1指向原有的entry元素。

+ **HashMap****的扩容** 

  ​		当HashMap中的元素越来越多的时候，hash冲突的几率也就越来越高，因为数组的长度是固定的。所以为了提高查询的效率，就要对HashMap的数组进行扩容，而在 HashMap数组扩容之后，最消耗性能的点就出现了：原数组中的数据必须重新计算其在新数组中的位置，并放进去，这就是resize。 

+ HashMap什么时候进行扩容呢？

  ​		当HashMap中的元素个数超过数组大小(数组总大小length,不是数组中个数size)loadFactor 时 ， 就 会 进 行 数 组 扩 容 ， loadFactor 的默认 值 (DEFAULT_LOAD_FACTOR)为0.75，这是一个折中的取值。也就是说，默认情况下，数组大小(DEFAULT_INITIAL_CAPACITY)为16，那么当HashMap中元素个数 超过16\*0.75=12（这个值就是代码中的threshold值，也叫做临界值）的时候，就把 数组的大小扩展为 2*16=32，即扩大一倍，然后重新计算每个元素在数组中的位置，而这是一个非常消耗性能的操作，所以如果我们已经预知HashMap中元素的个数，那么预设元素的个数能够有效的提高HashMap的性能。

**HashMap的存储结构：JDK 1.8**

+ HashMap的内部存储结构其实是**数组+链表+树的结合**。当实例化一个HashMap时，会初始化initialCapacity和loadFactor，在put第一对映射关系 时，系统会创建一个长度为initialCapacity的Node数组，这个长度在哈希表中被称为容量(Capacity)，在这个数组中可以存放元素的位置我们称之“桶”(bucket)，每个bucket都有自己的索引，系统可以根据索引快速的查找bucket中的元素。 

+ 每个bucket中存储一个元素，即一个Node对象，但每一个Node对象可以带一个引用变量next，用于指向下一个元素，因此，在一个桶中，就有可能生成一个Node链。也可能是一个一个TreeNode对象，每一个TreeNode对象可以有两个叶子结点left和right，因此，在一个桶中，就有可能生成一个TreeNode树。而新添加的元素作为链表的last，或树的叶子结点。

+ 那么HashMap什么时候进行扩容和树形化呢？

  ​		当HashMap中的元素个数超过数组大小(数组总大小length,不是数组中个数size)loadFactor 时 ， 就会进行数组扩容 ， loadFactor 的默认 值 (DEFAULT_LOAD_FACTOR)为0.75，这是一个折中的取值。也就是说，默认 情况下，数组大小(DEFAULT_INITIAL_CAPACITY)为16，那么当HashMap中 元素个数超过16\*0.75=12（这个值就是代码中的threshold值，也叫做临界值）的时候，就把数组的大小扩展为 2*16=32，即扩大一倍，然后重新计算每个元素在数组中的位置，而这是一个非常消耗性能的操作，所以如果我们已经预知HashMap中元素的个数，那么预设元素的个数能够有效的提高HashMap的性能。 

  ​		当HashMap中的其中一个链的对象个数如果达到了8个，此时如果capacity没有达到64，那么HashMap会先扩容解决，如果已经达到了64，那么这个链会变成 树，结点类型由Node变成TreeNode类型。当然，如果当映射关系被移除后，下次resize方法时判断树的结点个数低于6个，也会把树再转为链表。

关于映射关系的key是否可以修改？answer：不要修改

​		映射关系存储到HashMap中会存储key的hash值，这样就不用在每次查找时重新计算每一个Entry或Node（TreeNode）的hash值了，因此如果已经put到Map中的映射关系，再修改key的属性，而这个属性又参与hashcode值的计算，那么会导致匹配不上。 

**总结：**JDK1.8相较于之前的变化：

1.HashMap map = new HashMap();//默认情况下，先不创建长度为16的数组 

2.当首次调用map.put()时，再创建长度为16的数组 

3.数组为Node类型，在jdk7中称为Entry类型 

4.形成链表结构时，新添加的key-value对在链表的尾部（七上八下） 

5.当数组指定索引位置的链表长度>8时，且map中的数组的长度> 64时，此索引位置上的所有key-value对使用红黑树进行存储。

**面试题**：负载因子值的大小，对HashMap有什么影响

+ 负载因子的大小决定了HashMap的数据密度。 

+ 负载因子越大密度越大，发生碰撞的几率越高，数组中的链表越容易长, 造成查询或插入时的比较次数增多，性能会下降。 

+ 负载因子越小，就越容易触发扩容，数据密度也越小，意味着发生碰撞的几率越小，数组中的链表也就越短，查询和插入时比较的次数也越小，性能会更高。但是会浪费一定的内容空间。而且经常扩容也会影响性能，建 议初始化预设大一点的空间。 

+ 按照其他语言的参考及研究经验，会考虑将负载因子设置为0.7~0.75，此时平均检索长度接近于常数。

#### 8.4.2.LinkedHashMap

​		LinkedHashMap 是 HashMap 的子类。在HashMap存储结构的基础上，使用了一对双向链表来记录添加元素的顺序。与LinkedHashSet类似，LinkedHashMap 可以维护 Map 的迭代顺序：迭代顺序与 Key-Value 对的插入顺序一致。

HashMap中的内部类：Node 

```java
static class Node<K,V> implements Map.Entry<K,V> {
    final int hash;
    final K key;
    V value;
    Node<K,V> next;
}
```

LinkedHashMap中的内部类：Entry

```java
static class Entry<K,V> extends HashMap.Node<K,V> {
    Entry<K,V> before, after;
    Entry(int hash, K key, V value, Node<K,V> next) {
    	super(hash, key, value, next);
    }
}
```



#### 8.4.3.TreeMap

+ TreeMap存储 Key-Value 对时，需要根据 key-value 对进行排序。TreeMap 可以保证所有的 Key-Value 对处于**有序**状态。 

+ TreeSet底层使用**红黑树**结构存储数据 

+ TreeMap 的 Key 的排序： 
  + **自然排序**：TreeMap 的所有的 Key 必须实现 Comparable 接口，而且所有的 Key 应该是同一个类的对象，否则将会抛出 ClasssCastException 
  + **定制排序**：创建 TreeMap 时，传入一个 Comparator 对象，该对象负责对TreeMap 中的所有 key 进行排序。此时不需要 Map 的 Key 实现Comparable 接口 

+ TreeMap判断两个**key**相等的标准：两个key通过compareTo()方法或者compare()方法返回0。

#### 8.4.4.Hashtable

+ Hashtable是个古老的 Map 实现类，JDK1.0就提供了。不同于HashMap，Hashtable是线程安全的。 

+ Hashtable实现原理和HashMap相同，功能相同。底层都使用哈希表结构，查询速度快，很多情况下可以互用。 

+ 与HashMap不同，Hashtable 不允许使用 null 作为 key 和 value 

+ 与HashMap一样，Hashtable 也不能保证其中 Key-Value 对的顺序 

+ Hashtable判断两个key相等、两个value相等的标准，与HashMap一致。

#### 8.4.5.Properties

+ Properties 类是 Hashtable 的子类，该对象用于处理属性文件 

+ 由于属性文件里的 key、value 都是字符串类型，所以 Properties 里的 key 和 value 都是字符串类型 

+ 存取数据时，建议使用setProperty(String key,String value)方法和getProperty(String key)方法

```java
Properties pros = new Properties();
pros.load(new FileInputStream("jdbc.properties"));
String user = pros.getProperty("user");
System.out.println(user);
```



### 8.7.Collections工具类

+ Collections 是一个操作 Set、List 和 Map 等集合的工具类 

+ Collections 中提供了一系列静态的方法对集合元素进行排序、查询和修改等操作，还提供了对集合对象设置不可变、对集合对象实现同步控制等方法 

+ **排序操作**：（均为static方法） 
  + reverse(List)：反转 List 中元素的顺序 
  + shuffle(List)：对 List 集合元素进行随机排序 
  + sort(List)：根据元素的自然顺序对指定 List 集合元素按升序排序 
  + sort(List，Comparator)：根据指定的 Comparator 产生的顺序对 List 集合元素进行排序 
  + swap(List，int， int)：将指定 list 集合中的 i 处元素和 j 处元素进行交换

**常用方法**

**查找、替换** 

+ Object max(Collection)：根据元素的自然顺序，返回给定集合中的最大元素 

+ Object max(Collection，Comparator)：根据 Comparator 指定的顺序，返回给定集合中的最大元素 

+ Object min(Collection) 

+ Object min(Collection，Comparator) 

+ int frequency(Collection，Object)：返回指定集合中指定元素的出现次数 

+ void copy(List dest,List src)：将src中的内容复制到dest中 

+ boolean replaceAll(List list，Object oldVal，Object newVal)：使用新值替换List 对象的所有旧值

**同步控制** 

​		Collections 类中提供了多个 synchronizedXxx() 方法，该方法可使将指定集合包装成线程同步的集合，从而可以解决多线程并发访问集合时的线程安全问题

![1679841080015](D:\MyNote\images\1679841080015.png)

**Enumeration**

Enumeration 接口是 Iterator 迭代器的 “古老版本”

![1679841114468](D:\MyNote\images\1679841114468.png)

```java
Enumeration stringEnum = new StringTokenizer("a-b*c-d-e-g", "-");
while(stringEnum.hasMoreElements()){
    Object obj = stringEnum.nextElement();
    System.out.println(obj); 
}
```



## 9.泛型

泛型：标签

举例： 

+ 中药店，每个抽屉外面贴着标签 

+ 超市购物架上很多瓶子，每个瓶子装的是什么，有标签 

+ 泛型的设计背景 

​	    集合容器类在设计阶段/声明阶段不能确定这个容器到底实际存的是什么类型的对象，所以在JDK1.5之前只能把元素类型设计为Object，JDK1.5之后使用泛型来解决。因为这个时候除了元素的类型不确定，其他的部分是确定的，例如关于这个元素如何保存，如何管理等是确定的，因此此时把元素的类型设计成一个参数，这个类型参数叫做泛型。Collection<E>，List<E>，ArrayList<E> 这个<E>就是类型参数，即泛型。

​		所谓泛型，就是允许在定义类、接口时通过一个标识表示类中某个属性的类型或者是某个方法的返回值及参数类型。这个类型参数将在使用时（例如，继承或实现这个接口，用这个类型声明变量、创建对象时）确定（即传入实际的类型参数，也称为类型实参）。

​		从JDK1.5以后，Java引入了“参数化类型（Parameterized type）”的概念，允许我们在创建集合时再指定集合元素的类型，正如：List<String>，这表明该List只能保存字符串类型的对象。 

​		JDK1.5改写了集合框架中的全部接口和类，为这些接口、类增加了泛型支持，从而可以在声明集合变量、创建集合对象时传入类型实参。

**引入原因**

1. 解决元素存储的安全性问题，好比商品、药品标签，不会弄错。 

2. 解决获取数据元素时，需要类型强制转换的问题，好比不用每回拿商品、药品都要辨别。 

​        Java泛型可以保证如果程序在编译时没有发出警告，运行时就不会产生ClassCastException异常。同时，代码更加简洁、健壮。 

**在集合中使用泛型**

```java
ArrayList<Integer> list = new ArrayList<>();//类型推断
list.add(78);
list.add(88);
list.add(77);
list.add(66);
//遍历方式一：
//for(Integer i : list){
//不需要强转
//System.out.println(i);
//}
//遍历方式二：
Iterator<Integer> iterator = list.iterator();
while(iterator.hasNext()){
	System.out.println(iterator.next());
}


Map<String,Integer> map = new HashMap<String,Integer>();
map.put("Tom1",34);
map.put("Tom2",44);
map.put("Tom3",33);
map.put("Tom4",32);
//添加失败
//map.put(33, "Tom");
Set<Entry<String,Integer>> entrySet = map.entrySet();
Iterator<Entry<String,Integer>> iterator = entrySet.iterator();
while(iterator.hasNext()){
    Entry<String,Integer> entry = iterator.next();
    System.out.println(entry.getKey() + "--->" + entry.getValue());
}
```



### 9.1.自定义泛型结构 

1.泛型的声明

​		interface List<T> 和 class GenTest<K,V> 。其中，T,K,V不代表值，而是表示类型。这里使用任意字母都可以。常用T表示，是Type的缩写。 

2.泛型的实例化：

​		一定要在类名后面指定类型参数的值（类型）。如：

```java
List<String> strList = new ArrayList<String>();
Iterator<Customer> iterator = customers.iterator();
```

T只能是类，不能用基本数据类型填充。但可以使用包装类填充。把一个集合中的内容限制为一个特定的数据类型，这就是generics背后的核心思想

```java
jdk1.5前
Comparable c = new Date();
System.out.println(c.compareTo("red"));

jdk1.5后
Comparable<Date> c = new Date();
System.out.println(c.compareTo("red"));   
体会：使用泛型的主要优点是能够在编译时而不是在运行时检测错误。    
```



1. 泛型类可能有多个参数，此时应将多个参数一起放在尖括号内。比如： <E1,E2,E3> 

2. 泛型类的构造器如下：public GenericClass(){}。 而下面是错误的：public GenericClass<E>(){} 

3. 实例化后，操作原来泛型位置的结构必须与指定的泛型类型一致。 

4. 泛型不同的引用不能相互赋值。 尽管在编译时ArrayList<String>和ArrayList<Integer>是两种类型，但是，在运行时只有一个ArrayList被加载到JVM中。 

5. 泛型如果不指定，将被擦除，泛型对应的类型均按照Object处理，但不等价于Object。**经验：**泛型要使用一路都用。要不用，一路都不要用。 

6. 如果泛型结构是一个接口或抽象类，则不可创建泛型类的对象。 

7. jdk1.7，泛型的简化操作：ArrayList<Fruit> flist = new ArrayList<>(); 

8. 泛型的指定中不能使用基本数据类型，可以使用包装类替换。

```java
class GenericTest {
    public static void main(String[] args) {
        // 1、使用时：类似于Object，不等同于Object
        ArrayList list = new ArrayList();
        // list.add(new Date());//有风险
        list.add("hello");
        test(list);// 泛型擦除，编译不会类型检查
        // ArrayList<Object> list2 = new ArrayList<Object>();
        // test(list2);//一旦指定Object，编译会类型检查，必须按照Object处理
    }
    public static void test(ArrayList<String> list) {
        String str = "";
        for (String s : list) {
        	str += s + ",";
        }
        System.out.println("元素:" + str);
    }
}
```



9. 在类/接口上声明的泛型，在本类或本接口中即代表某种类型，可以作为非静态属性的类型、非静态方法的参数类型、非静态方法的返回值类型。但在静态方法中不能使用类的泛型。 

10. 异常类不能是泛型的 

11. 不能使用new E[]。但是可以：E[] elements = (E[])new Object[capacity]; 

参考：ArrayList源码中声明：Object[] elementData，而非泛型参数类型数组。 

12.父类有泛型，子类可以选择保留泛型也可以选择指定泛型类型： 

+ 子类不保留父类的泛型：按需实现 
  + 没有类型 擦除 
  + 具体类型 

+ 子类保留父类的泛型：泛型子类 
  + 全部保留 
  + 部分保留 

结论：子类必须是“富二代”，子类除了指定或保留父类的泛型，还可以增加自己的泛型

```java
class Father<T1, T2> {
}
// 子类不保留父类的泛型
// 1)没有类型 擦除
class Son1 extends Father {// 等价于class Son extends Father<Object,Object>{
}
// 2)具体类型
class Son2 extends Father<Integer, String> {
}
// 子类保留父类的泛型
// 1)全部保留
class Son3<T1, T2> extends Father<T1, T2> {
}
// 2)部分保留
class Son4<T2> extends Father<Integer, T2> {
}

class Father<T1, T2> {
}
// 子类不保留父类的泛型
// 1)没有类型 擦除
class Son<A, B> extends Father{//等价于class Son extends Father<Object,Object>{
}
// 2)具体类型
class Son2<A, B> extends Father<Integer, String> {
}
// 子类保留父类的泛型
// 1)全部保留
class Son3<T1, T2, A, B> extends Father<T1, T2> {
}
// 2)部分保留
class Son4<T2, A, B> extends Father<Integer, T2> {
}

class Person<T> {
    // 使用T类型定义变量
    private T info;
    // 使用T类型定义一般方法
    public T getInfo() {
    	return info;
    }
    public void setInfo(T info) {
    	this.info = info;
    }
    // 使用T类型定义构造器
    public Person() {
    }
    public Person(T info) {
    	this.info = info;
    }
    // static的方法中不能声明泛型
    //public static void show(T t) {
    //
    //}
    // 不能在try-catch中使用泛型定义
    //public void test() {
    //	try {
    //
    //	} catch (MyException<T> ex) {
    //
    //	}
    //}
}
```



​		方法，也可以被泛型化，不管此时定义在其中的类是不是泛型类。在泛型方法中可以定义泛型参数，此时，参数的类型就是传入数据的类型。

### 9.2.泛型方法的格式

[访问权限] <泛型> 返回类型 方法名([泛型标识 参数名称]) 抛出的异常

泛型方法声明泛型时也可以指定上限

```java
public class DAO {
	public <E> E get(int id, E e) {
        E result = null;
        return result;
    }
}

public static <T> void fromArrayToCollection(T[] a, Collection<T> c) {
    for (T o : a) {
    	c.add(o);
    }
}
public static void main(String[] args) {
    Object[] ao = new Object[100];
    Collection<Object> co = new ArrayList<Object>();
    fromArrayToCollection(ao, co);
    String[] sa = new String[20];
    Collection<String> cs = new ArrayList<>();
    fromArrayToCollection(sa, cs);
    Collection<Double> cd = new ArrayList<>();
    // 下面代码中T是Double类，但sa是String类型，编译错误。
    // fromArrayToCollection(sa, cd);
    // 下面代码中T是Object类型，sa是String类型，可以赋值成功。
    fromArrayToCollection(sa, co);
}

class Creature{}
class Person extends Creature{}
class Man extends Person{}
class PersonTest {
    public static <T extends Person> void test(T t){
        System.out.println(t);
    }
    public static void main(String[] args) {
        test(new Person());
        test(new Man());
        //The method test(T) in the type PersonTest is not 
        //applicable for the arguments (Creature)
        test(new Creature());
    }
}
```



**泛型在继承上的体现**

如果B是A的一个子类型（子类或者子接口），而G是具有泛型声明的类或接口，G<B>并不是G<A>的子类型！

```java
public void testGenericAndSubClass() {
    Person[] persons = null;
    Man[] mans = null;
    // 而 Person[] 是 Man[] 的父类.
    persons = mans;
    Person p = mans[0];
    // 在泛型的集合上
    List<Person> personList = null;
    List<Man> manList = null;
    // personList = manList;(报错)
}
```



### 9.3.通配符的使用

1.使用类型**通配符：？** 

比如：List<?> ，Map<?,?> 

List<?>是List<String>、List<Object>等各种泛型List的父类。 

2.**读取**List<?>的对象list中的元素时，永远是安全的，因为不管list的真实类型是什么，它包含的都是Object。 

3.**写入**list中的元素时，不行。因为我们不知道c的元素类型，我们不能向其中添加对象。 

+ 唯一的例外是null，它是所有类型的成员。

+ **将任意元素加入到其中不是类型安全的**： 

Collection<?> c = new ArrayList<String>(); 

c.add(new Object()); // 编译时错误 

因为我们不知道c的元素类型，我们不能向其中添加对象。add方法有类型参数E作为集合的元素类型。我们传给add的任何参数都必须是一个未知类型的子类。因为我们不知道那是什么类型，所以我们无法传任何东西进去。 

+ **唯一的例外的是**null，它是所有类型的成员。 

+ **另一方面，我们可以调用**get()方法并使用其返回值。返回值是一个未知的类型，但是我们知道，它总是一个Object。

```java
public static void main(String[] args) {
    List<?> list = null;
    list = new ArrayList<String>();
    list = new ArrayList<Double>();
    // list.add(3);//编译不通过
    list.add(null);
    List<String> l1 = new ArrayList<String>();
    List<Integer> l2 = new ArrayList<Integer>();
    l1.add("尚硅谷");
    l2.add(15);
    read(l1);
    read(l2);
}
public static void read(List<?> list) {
    for (Object o : list) {
    	System.out.println(o);
    }
}
```



**注意**

1不能用在泛型方法声明上，返回值类型前面<>不能使用? 

`public static <?> void test(ArrayList<?> list){}`

2不能用在泛型类的声明上

`class GenericTypeClass<?>{}`

3不能用在创建对象上，右边属于创建集合对象

`ArrayList<?> list2 = new ArrayList<?>();`

### 9.4.通配符的限制

<?>允许所有泛型的引用调用。通配符指定上限，上限extends：使用时指定的类型必须是继承某个类，或者实现某个接口，即<=  。通配符指定下限，下限super：使用时指定的类型不能小于操作的类，即>=。

举例： 

+ <? extends Number> (无穷小 , Number]
  只允许泛型为Number及Number子类的引用调用
+ <? super Number> [Number , 无穷大)
  只允许泛型为Number及Number父类的引用调用
+ <? extends Comparable>
  只允许泛型为实现Comparable接口的实现类的引用调用

```java
public static void printCollection3(Collection<? extends Person> coll) {
    //Iterator只能用Iterator<?>或Iterator<? extends Person>.why?
    Iterator<?> iterator = coll.iterator();
    while (iterator.hasNext()) {
    	System.out.println(iterator.next());
    }
}
public static void printCollection4(Collection<? super Person> coll) {
    //Iterator只能用Iterator<?>或Iterator<? super Person>.why?
    Iterator<?> iterator = coll.iterator();
    while (iterator.hasNext()) {
    	System.out.println(iterator.next());
    }
}
```

**泛型应用举例：泛型嵌套**

```java
public static void main(String[] args) {
    HashMap<String, ArrayList<Citizen>> map = new HashMap<String, ArrayList<Citizen>>();
    ArrayList<Citizen> list = new ArrayList<Citizen>();
    list.add(new Citizen("刘恺威"));
    list.add(new Citizen("杨幂"));
    list.add(new Citizen("小糯米"));
    map.put("刘恺威", list);
    Set<Entry<String, ArrayList<Citizen>>> entrySet = map.entrySet();
    Iterator<Entry<String, ArrayList<Citizen>>> iterator = entrySet.iterator();
    while (iterator.hasNext()) {
        Entry<String, ArrayList<Citizen>> entry = iterator.next();
        String key = entry.getKey();
        ArrayList<Citizen> value = entry.getValue();
        System.out.println("户主：" + key);
        System.out.println("家庭成员：" + value);
    }
}
```



​		用户在设计类的时候往往会使用类的关联关系，例如，一个人中可以定义一个信息的属性，但是一个人可能有各种各样的信息（如联系方式、基本信息等），所以此信息属性的类型就可以通过泛型进行声明，然后只要设计相应的信息类即可。 

<img src="D:\MyNote\images\1680014035163.png" alt="1680014035163" style="zoom:67%;" />

## 10.IO流

### 10.1.File类

+ java.io.File类：文件和文件目录路径的抽象表示形式，与平台无关
+ File可以新增、删除、重命名文件或文件路径，但是不可以查看文件内容本身，要查看的话就需要输入/输出流
+ 想要在java中表示一个文件或文件路径就需要创建一个File对象，但是一个File对象对应的文件或文件路径却不一定真实存在
+ File对象可以作为一个参数，传递给流的构造器 

**构造器**

+ public File(String pathname)，以pathname为文件路径创建File对象。pathname可以是绝对路径或相对路径。如果是相对路径的话，默认路径会存储在系统属性user.dir中
  + 绝对路径： 示例：F:\书籍\网络\HTTP权威指南（中文版）.pdf
  + 相对路径：在F:\书籍时，相对路径是./网络\HTTP权威指南（中文版）.pdf；在F:时，相对路径是./书籍/网络\HTTP权威指南（中文版）.pdf
+ public File(String parent,String child)，以parent为父路径，以child为子路径创建File对象
+ public File(File parent,String child)，以一个父File对象和一个子路径创建File对象

**路径分隔符**

+ 路径中的每级目录之间用一个**路径分隔符**隔开。 

+ 路径分隔符和系统有关： 

+ windows和DOS系统默认使用“\”来表示 

+ UNIX和URL使用“/”来表示 

+ Java程序支持跨平台运行，因此路径分隔符要慎用。 

+ 为了解决这个隐患，File类提供了一个常量： 

**public static final String separator**。根据操作系统，动态的提供分隔符。 

+ 举例： 

```java
File file1 = new File("d:\\atguigu\\info.txt");
File file2 = new File("d:" + File.separator + "atguigu" + File.separator + "info.txt");
File file3 = new File("d:/atguigu");
```

**常用方法** 

**File类的获取功能** 

+ public String getAbsolutePath()：获取绝对路径 

+ public String getPath() ：获取路径 

+ public String getName() ：获取名称 

+ public String getParent()：获取上层文件目录路径。若无，返回null 

+ public long length() ：获取文件长度（即：字节数）。不能获取目录的长度。 

+ public long lastModified() ：获取最后一次的修改时间，毫秒值 

+ public String[] list() ：获取指定目录下的所有文件或者文件目录的名称数组 

+ public File[] listFiles() ：获取指定目录下的所有文件或者文件目录的File数组 

**File类的重命名功能** 

+ public boolean renameTo(File dest):把文件重命名为指定的文件路径

**File类的判断功能** 

+ public boolean isDirectory()：判断是否是文件目录 

+ public boolean isFile() ：判断是否是文件 

+ public boolean exists() ：判断是否存在 

+ public boolean canRead() ：判断是否可读 

+ public boolean canWrite() ：判断是否可写 

+ public boolean isHidden() ：判断是否隐藏

**File类的创建功能** 

+ public boolean createNewFile() ：创建文件。若文件存在，则不创建，返回false 

+ public boolean mkdir() ：创建文件目录。如果此文件目录存在，就不创建了。 如果此文件目录的上层目录不存在，也不创建。 

+ public boolean mkdirs() ：创建文件目录。如果上层文件目录不存在，一并创建 

**注意事项：如果你创建文件或者文件目录没有写盘符路径，那么，默认在项目路径下。**

**File类的删除功能** 

+ public boolean delete()：删除文件或者文件夹 

删除注意事项： 

Java中的删除不走**回收站**。 

要删除一个文件目录，请注意该文件目录内不能包含文件或者文件目录

![1680873665141](D:\MyNote\images\1680873665141.png)

```java
File dir1 = new File("D:/IOTest/dir1");
if (!dir1.exists()) { // 如果D:/IOTest/dir1不存在，就创建为目录
dir1.mkdir();
}
// 创建以dir1为父目录,名为"dir2"的File对象
File dir2 = new File(dir1, "dir2");
if (!dir2.exists()) { // 如果还不存在，就创建为目录
dir2.mkdirs();
}
File dir4 = new File(dir1, "dir3/dir4");
if (!dir4.exists()) {
dir4.mkdirs();
}
// 创建以dir2为父目录,名为"test.txt"的File对象
File file = new File(dir2, "test.txt");
if (!file.exists()) { // 如果还不存在，就创建为文件
file.createNewFile();
}
```



### 10.2.IO流原理及流的分类 

**原理**

+ I/O是Input/Output的缩写， I/O技术是非常实用的技术，用于处理设备之间的数据传输。如读/写文件，网络通讯等。
+ Java程序中，对于数据的输入/输出操作以“流(stream)” 的方式进行。
+ java.io包下提供了各种“流”类和接口，用以获取不同种类的数据，并通过标准的方法输入或输出数据。

+ 输入input：读取外部数据（磁盘、光盘等存储设备的数据）到程序（内存）中。
+ 输出output：将程序（内存）数据输出到磁盘、光盘等存储设备中。

**流的分类**

+ 按操作数据单位不同分为：字节流(8 bit)，字符流(16 bit)
+ 按数据流的流向不同分为：输入流，输出流
+ 按流的角色的不同分为：节点流，处理流

| (抽象基类) | 字节流       | 字符流 |
| ---------- | ------------ | ------ |
| 输入流     | InputStream  | Reader |
| 输出流     | OutputStream | Writer |

1. Java的IO流共涉及40多个类，实际上非常规则，都是从如下4个抽象基类派生的。
2. 由这四个类派生出来的子类名称都是以其父类名作为子类名后缀。

<img src="D:\MyNote\images\1680874126707.png" alt="1680874126707" style="zoom:67%;" />

![1680874151428](D:\MyNote\images\1680874151428.png)

![1680874213835](D:\MyNote\images\1680874213835.png)

**节点流和处理流**

节点流：直接从数据源或目的地读写数据

<img src="D:\MyNote\images\1680874308860.png" alt="1680874308860" style="zoom: 67%;" />

处理流：不直接连接到数据源或目的地，而是“连接”在已存在的流（节点流或处理流）之上，通过对数据的处理为程序提供更为强大的读写功能。

<img src="D:\MyNote\images\1680874382363.png" alt="1680874382363" style="zoom:67%;" />

**InputStream & Reader** 

+ InputStream 和 Reader 是所有输入流的基类。
+ InputStream（典型实现：FileInputStream）
  + int read()
  + int read(byte[] b)
  + int read(byte[] b, int off, int len)
+ Reader（典型实现：FileReader）
  + int read()
  + int read(char [] c)
  + int read(char [] c, int off, int len)
+ 程序中打开的文件 IO 资源不属于内存里的资源，垃圾回收机制无法回收该资源，所以应该显式关闭文件 IO 资源。
+ FileInputStream 从文件系统中的某个文件中获得输入字节。FileInputStream用于读取非文本数据之类的原始字节流。要读取字符流，需要使用 FileReader

**InputStream**

+ **int read()** 

  ​		从输入流中读取数据的下一个字节。返回 0 到 255 范围内的 int 字节值。如果因为已经到达流末尾而没有可用的字节，则返回值 -1。 

+ **int read(byte[] b)** 

  ​		从此输入流中将最多 b.length 个字节的数据读入一个 byte 数组中。如果因为已经到达流末尾而没有可用的字节，则返回值 -1。否则以整数形式返回实际读取的字节数。 

+ **int read(byte[] b, int off,int len)** 

  ​		将输入流中最多 len 个数据字节读入 byte 数组。尝试读取 len 个字节，但读取的字节也可能小于该值。以整数形式返回实际读取的字节数。如果因为流位于文件末尾而没有可用的字节，则返回值 -1。 

+ **public void close() throws IOException** 

  ​		关闭此输入流并释放与该流关联的所有系统资源。

**Reader**

+ **int read()** 

  ​		读取单个字符。作为整数读取的字符，范围在 0 到 65535 之间 (0x00-0xffff)（2个字节的Unicode码），如果已到达流的末尾，则返回 -1 

+ **int read(char[] cbuf)** 

  ​		将字符读入数组。如果已到达流的末尾，则返回 -1。否则返回本次读取的字符数。 

+ **int read(char[] cbuf,int off,int len)** 

  ​		将字符读入数组的某一部分。存到数组cbuf中，从off处开始存储，最多读len个字符。如果已到达流的末尾，则返回 -1。否则返回本次读取的字符数。 

+ **public void close() throws IOException** 

  ​		关闭此输入流并释放与该流关联的所有系统资源。 

**OutputStream & Writer**

+ OutputStream 和 Writer 也非常相似：
  + void write(int b/int c);
  + void write(byte[] b/char[] cbuf);
  + void write(byte[] b/char[] buff, int off, int len);
  + void flush();
  + void close(); 需要先刷新，再关闭此流
+ 因为字符流直接以字符作为操作单位，所以 Writer 可以用字符串来替换字符数组，即以 String 对象作为参数
  + void write(String str);
  + void write(String str, int off, int len);
+ FileOutputStream 从文件系统中的某个文件中获得输出字节。FileOutputStream 用于写出非文本数据之类的原始字节流。要写出字符流，需要使用 FileWriter

**OutputStream**

+ **void write(int b)** 

  ​		将指定的字节写入此输出流。write 的常规协定是：向输出流写入一个字节。要写入的字节是参数 b 的八个低位。b 的 24 个高位将被忽略。 即写入0~255范围的。 

+ **void write(byte[] b)** 

  ​		将 b.length 个字节从指定的 byte 数组写入此输出流。write(b) 的常规协定是：应该与调用 write(b, 0, b.length) 的效果完全相同。 

+ **void write(byte[] b,int off,int len)** 

  ​		将指定 byte 数组中从偏移量 off 开始的 len 个字节写入此输出流。 

+ **public void flush()throws IOException** 

  ​		刷新此输出流并强制写出所有缓冲的输出字节，调用此方法指示应将这些字节立即写入它们预期的目标。 

+ **public void close() throws IOException** 

  ​		关闭此输出流并释放与该流关联的所有系统资源。 

**Writer**

+ **void write(int c)** 

  ​		写入单个字符。要写入的字符包含在给定整数值的 16 个低位中，16 高位被忽略。 即写入0 到 65535 之间的Unicode码。 

+ **void write(char[] cbuf)** 

  ​		写入字符数组。 

+ **void write(char[] cbuf,int off,int len)** 

  ​		写入字符数组的某一部分。从off开始，写入len个字符 

+ **void write(String str)** 

  ​		写入字符串。 

+ **void write(String str,int off,int len)** 

  ​		写入字符串的某一部分。 

+ **void flush()** 

  ​		刷新该流的缓冲，则立即将它们写入预期目标。 

+ **public void close() throws IOException** 

  ​		关闭此输出流并释放与该流关联的所有系统资源。

### 10.3.节点流

**读取文件**

```java
1.建立一个流对象，将已存在的一个文件加载进流。
 FileReader fr = new FileReader(new File(“Test.txt”));
2.创建一个临时存放数据的数组。
 char[] ch = new char[1024];
3.调用流对象的读取方法将流中的数据读入到数组中。
 fr.read(ch);
4. 关闭资源。
 fr.close();

案例1：把文件放入刘中然后打印出来
FileReader fr = null;
try {
    fr = new FileReader(new File("c:\\test.txt"));
    char[] buf = new char[1024];
    int len;
    while ((len = fr.read(buf)) != -1) {
    	System.out.print(new String(buf, 0, len));
    }
} catch (IOException e) {
    System.out.println("read-Exception :" + e.getMessage());
} finally {
    if (fr != null) {
        try {
            fr.close();
        } catch (IOException e) {
            System.out.println("close-Exception :" + e.getMessage());
        }
    }
}

案例2：把文件放入流中并写入内容
FileWriter fw = null;
try {
    fw = new FileWriter(new File("Test.txt"));
    fw.write("atguigu-songhongkang");
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (fw != null)
        try {
            fw.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
}
```



注意：

+ 定义文件路径时，注意：可以用“/”或者“\”。 

+ 在写入一个文件时，如果使用构造器FileOutputStream(file)，则**目录下有同名文件将被覆盖。** 

+ 如果使用构造器FileOutputStream(file,true)，则目录下的同名文件不会被覆盖， **在文件内容末尾追加内容。** 

+ 在读取文件时，必须保证该文件已存在，否则报异常。 

+ 字节流操作字节，比如：.mp3，.avi，.rmvb，mp4，.jpg，.doc，.ppt 

+ 字符流操作字符，只能操作普通文本文件。最常见的文本文件：.txt，.java，.c，.cpp 等语言的源代码。尤其注意.doc,excel,ppt这些不是文本文件。

### 10.4.缓冲流

​		为了提高数据读写的速度，Java API提供了带缓冲功能的流类，在使用这些流类时，会创建一个内部缓冲区数组，缺省使用8192个字节(8Kb)的缓冲区。 

​		缓冲流要“套接”在相应的节点流之上，根据数据操作单位可以把缓冲流分为： 

+ **BufferedInputStream** **和** **BufferedOutputStream** 

+ **BufferedReader** **和** **BufferedWriter**

<img src="D:\MyNote\images\1681564558747.png" alt="1681564558747" style="zoom:67%;" />

+ 当读取数据时，数据按块读入缓冲区，其后的读操作则直接访问缓冲区 

+ 当使用BufferedInputStream读取字节文件时，BufferedInputStream会一次性从文件中读取8192个(8Kb)，存在缓冲区中，直到缓冲区装满了，才重新从文件中读取下一个8192个字节数组。 

+ 向流中写入字节时，不会直接写到文件，先写到缓冲区中直到缓冲区写满， BufferedOutputStream才会把缓冲区中的数据一次性写到文件里。使用方法flush()可以强制将缓冲区的内容全部写入输出流 

+ 关闭流的顺序和打开流的顺序相反。只要关闭最外层流即可，关闭最外层流也会相应关闭内层节点流 

+ flush()方法的使用：手动将buffer中内容写入文件 

+ 如果是带缓冲区的流对象的close()方法，不但会关闭流，还会在关闭流之前刷新缓冲区，关闭后不能再写出

<img src="D:\MyNote\images\1681564855999.png" alt="1681564855999" style="zoom:80%;" />

```java
BufferedReader br = null;
BufferedWriter bw = null;
try {
    // 创建缓冲流对象：它是处理流，是对节点流的包装
    br = new BufferedReader(new FileReader("d:\\IOTest\\source.txt"));
    bw = new BufferedWriter(new FileWriter("d:\\IOTest\\dest.txt"));
    String str;
    while ((str = br.readLine()) != null) { // 一次读取字符文本文件的一行字符
        bw.write(str); // 一次写入一行字符串
        bw.newLine(); // 写入行分隔符
    }
    bw.flush(); // 刷新缓冲区
} catch (IOException e) {
    e.printStackTrace();
} finally {
    // 关闭IO流对象
    try {
        if (bw != null) {
            bw.close(); // 关闭过滤流时,会自动关闭它所包装的底层节点流
        }
    } catch (IOException e) {
        e.printStackTrace();
    }
    try {
        if (br != null) {
            br.close();
        }
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```



### 10.5.转换流

+ 转换流提供了在字节流和字符流之间的转换 

+ Java API提供了两个转换流： 
  + **InputStreamReader**：将InputStream转换为Reader
  + **OutputStreamWriter**：将Writer转换为OutputStream

+ 字节流中的数据都是字符时，转成字符流操作更高效。 

+ 很多时候我们使用转换流来处理文件乱码问题。实现编码和解码的功能

**InputStreamReader** 

+ 实现将字节的输入流按指定字符集转换为字符的输入流。 

+ 需要和InputStream“套接”。 

+ 构造器 
  + **public InputStreamReader(InputStream in)** 
  + **public InputSreamReader(InputStream in,String charsetName)** 

如： Reader isr = new InputStreamReader(System.in,”gbk”); gbk指定字符集

**OutputStreamWriter** 

+ 实现将字符的输出流按指定字符集转换为字节的输出流。 

+ 需要和OutputStream“套接”。 

+ 构造器 
  + **public OutputStreamWriter(OutputStream out)** 
  + **public OutputSreamWriter(OutputStream out,String charsetName)**

```java
public void testMyInput() throws Exception {
    FileInputStream fis = new FileInputStream("dbcp.txt");
    FileOutputStream fos = new FileOutputStream("dbcp5.txt");
    InputStreamReader isr = new InputStreamReader(fis, "GBK");
    OutputStreamWriter osw = new OutputStreamWriter(fos, "GBK");
    BufferedReader br = new BufferedReader(isr);
    BufferedWriter bw = new BufferedWriter(osw);
    String str = null;
    while ((str = br.readLine()) != null) {
        bw.write(str);
        bw.newLine();
        bw.flush();
    }
    bw.close();
    br.close();
}
```

**补充：字符编码**

+ **编码表的由来** 

计算机只能识别二进制数据，早期由来是电信号。为了方便应用计算机，让它可以识别各个国家的文字。就将各个国家的文字用数字来表示，并一一对应，形成一张表。 这就是编码表。 

+ **常见的编码表** 
  + ASCII：美国标准信息交换码。 
    + 用一个字节的7位可以表示。 
  + ISO8859-1：拉丁码表。欧洲码表 
    + 用一个字节的8位表示。 
  + GB2312：中国的中文编码表。最多两个字节编码所有字符 
  + GBK：中国的中文编码表升级，融合了更多的中文文字符号。最多两个字节编码 
  + Unicode：国际标准码，融合了目前人类使用的所有字符。为每个字符分配唯一的字符码。所有的文字都用两个字节来表示。 
  + UTF-8：变长的编码方式，可用1-4个字节来表示一个字符。

![1681565581032](D:\MyNote\images\1681565581032.png)

+ 在**Unicode**出现之前，所有的字符集都是和具体编码方案绑定在一起的（即字符集≈编码方式），都是直接将字符和最终字节流绑定死了。 

+ GBK等双字节编码方式，用最高位是1或0表示两个字节和一个字节。

+ Unicode不完美，这里就有三个问题，一个是，我们已经知道，英文字母只用一个字节表示就够了，第二个问题是如何才能区别Unicode和ASCII？计算机怎么知道两个字节表示一个符号，而不是分别表示两个符号呢？第三个，如果 和GBK等双字节编码方式一样，用最高位是1或0表示两个字节和一个字节， 就少了很多值无法用于表示字符，不够表示所有字符。Unicode在很长一段时间内无法推广，直到互联网的出现。 

+ 面向传输的众多 UTF（UCS Transfer Format）标准出现了，顾名思义，UTF- 8就是每次8个位传输数据，而UTF-16就是每次16个位。这是为传输而设计的编码，并使编码无国界，这样就可以显示全世界上所有文化的字符了。 

+ Unicode只是定义了一个庞大的、全球通用的字符集，并为每个字符规定了唯一确定的编号，具体存储成什么样的字节流，取决于字符编码方案。推荐的Unicode编码是UTF-8和UTF-16。

```
Unicode符号范围 | UTF-8编码方式
(十六进制) | （二进制）
—————————————————————–
0000 0000-0000 007F | 0xxxxxxx（兼容原来的ASCII）
0000 0080-0000 07FF | 110xxxxx 10xxxxxx
0000 0800-0000 FFFF | 1110xxxx 10xxxxxx 10xxxxxx
0001 0000-0010 FFFF | 11110xxx 10xxxxxx 10xxxxxx 10xxxxxx
```

![1681565829534](D:\MyNote\images\1681565829534.png)

​		ANSI编码，通常指的是平台的默认编码，例如英文操作系统中是ISO-8859-1，中文系统是GBK。Unicode字符集只是定义了字符的集合和唯一编号，Unicode编码，则是对UTF-8、UCS-2/UTF-16等具体编码方案的统称而已，并不是具体的编码方案。

<img src="D:\MyNote\images\1681565924070.png" alt="1681565924070" style="zoom: 67%;" />

编码：字符串字节数组 

解码：字节数组字符串 

**转换流的编码应用** 

1. 可以将字符按指定编码格式存储 

2. 可以对文本数据按指定编码格式来解读 

3. 指定编码表的动作由构造器完成

### 10.6.标准输入输出-了解

+ System.in和System.out分别代表了系统标准的输入和输出设备 

+ 默认输入设备是：键盘，输出设备是：显示器 

+ System.in的类型是InputStream 

+ System.out的类型是PrintStream，其是OutputStream的子类FilterOutputStream 的子类 

+ 重定向：通过System类的setIn，setOut方法对默认设备进行改变。 

+ public static void **setIn**(InputStream in) 

+ public static void **setOut**(PrintStream out)

```java
System.out.println("请输入信息(退出输入e或exit):");
// 把"标准"输入流(键盘输入)这个字节流包装成字符流,再包装成缓冲流
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
String s = null;
try {
    while ((s = br.readLine()) != null) { // 读取用户输入的一行数据 --> 阻塞程序
        if ("e".equalsIgnoreCase(s) || "exit".equalsIgnoreCase(s)) {
            System.out.println("安全退出!!");
            break;
        }
        // 将读取到的整行字符串转成大写输出
        System.out.println("-->:" + s.toUpperCase());
        System.out.println("继续输入信息");
    }
} catch (IOException e) {
    e.printStackTrace();
} finally {
    try {
        if (br != null) {
            br.close(); // 关闭过滤流时,会自动关闭它包装的底层节点流
        }
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```



### 10.7.打印流-了解

+ 实现将基本数据类型的数据格式转化为字符串输出
+ 打印流：PrintStream和PrintWriter
+ 提供了一系列重载的print()和println()方法，用于多种数据类型的输出
+ PrintStream和PrintWriter的输出不会抛出IOException异常
+ PrintStream和PrintWriter有自动flush功能
+ PrintStream 打印的所有字符都使用平台的默认字符编码转换为字节。在需要写入字符而不是写入字节的情况下，应该使用 PrintWriter 类。
+ System.out返回的是PrintStream的实例

```java
PrintStream ps = null;
try {
    FileOutputStream fos = new FileOutputStream(new File("D:\\IO\\text.txt"));
    // 创建打印输出流,设置为自动刷新模式(写入换行符或字节 '\n' 时都会刷新输出缓冲区)
    ps = new PrintStream(fos, true);
    if (ps != null) {// 把标准输出流(控制台输出)改成文件
        System.setOut(ps);
    }
    for (int i = 0; i <= 255; i++) { // 输出ASCII字符
        System.out.print((char) i);
        if (i % 50 == 0) { // 每50个数据一行
            System.out.println(); // 换行
        }
    }
} catch (FileNotFoundException e) {
    e.printStackTrace();
} finally {
    if (ps != null) {
        ps.close();
    }
}
```



### 10.8.数据流-了解

+ 为了方便地操作Java语言的基本数据类型和String的数据，可以使用数据流。 

+ 数据流有两个类：(用于读取和写出基本数据类型、String类的数据） 
  + **DataInputStream** 和 **DataOutputStream** 
  + **分别“套接”在** **InputStream** **和** **OutputStream** **子类的流上** 

+ **DataInputStream**中的方法

  boolean readBoolean() 

  byte readByte() 

  char readChar() 

  float readFloat() 

  double readDouble() 

  short readShort() 

  long readLong() 

  int readInt() 

  String readUTF() void readFully(byte[] b) 

+ **DataOutputStream**中的方法

+ 将上述的方法的read改为相应的write即可。

```java
DataOutputStream dos = null;
try { // 创建连接到指定文件的数据输出流对象
    dos = new DataOutputStream(new FileOutputStream("destData.dat"));
    dos.writeUTF("我爱北京天安门"); // 写UTF字符串
    dos.writeBoolean(false); // 写入布尔值
    dos.writeLong(1234567890L); // 写入长整数
    System.out.println("写文件成功!");
} catch (IOException e) {
    e.printStackTrace();
} finally { // 关闭流对象
    try {
        if (dos != null) {
            // 关闭过滤流时,会自动关闭它包装的底层节点流
            dos.close();
        }
    } catch (IOException e) {
        e.printStackTrace();
    }
}


DataInputStream dis = null;
try {
    dis = new DataInputStream(new FileInputStream("destData.dat"));
    String info = dis.readUTF();
    boolean flag = dis.readBoolean();
    long time = dis.readLong();
    System.out.println(info);
    System.out.println(flag);
    System.out.println(time);
} catch (Exception e) {
    e.printStackTrace();
} finally {
    if (dis != null) {
        try {
            dis.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```



### 10.9.对象流

+ ObjectInputStream和OjbectOutputSteam
+ 用于存储和读取基本数据类型数据或对象的处理流。它的强大之处就是可以把Java中的对象写入到数据源中，也能把对象从数据源中还原回来。
+ 序列化：用ObjectOutputStream类保存基本类型数据或对象的机制
+ 反序列化：用ObjectInputStream类读取基本类型数据或对象的机制
+ ObjectOutputStream和ObjectInputStream不能序列化static和transient修饰的成员变量

**对象的序列化**

+ 对象序列化机制允许把内存中的Java对象转换成平台无关的二进制流，从而允许把这种二进制流持久地保存在磁盘上，或通过网络将这种二进制流传输到另一个网络节点。//当其它程序获取了这种二进制流，就可以恢复成原来的Java对象
+ 序列化的好处在于可将任何实现了Serializable接口的对象转化为字节数据，使其在保存和传输时可被还原
+ 序列化是 RMI（Remote Method Invoke – 远程方法调用）过程的参数和返回值都必须实现的机制，而 RMI 是 JavaEE 的基础。因此序列化机制是JavaEE 平台的基础
+ 如果需要让某个对象支持序列化机制，则必须让对象所属的类及其属性是可序列化的，为了让某个类是可序列化的，该类必须实现如下两个接口之一。否则，会抛出NotSerializableException异常
  + Serializable
  + Externalizable

+ 凡是实现Serializable接口的类都有一个表示序列化版本标识符的静态变量：
  + private static final long serialVersionUID;
  + serialVersionUID用来表明类的不同版本间的兼容性。简言之，其目的是以序列化对象进行版本控制，有关各版本反序列化时是否兼容。
+ 如果类没有显示定义这个静态常量，它的值是Java运行时环境根据类的内部细节自动生成的。若类的实例变量做了修改，serialVersionUID 可能发生变化。故建议，显式声明。
+ 简单来说，Java的序列化机制是通过在运行时判断类的serialVersionUID来验证版本一致性的。在进行反序列化时，JVM会把传来的字节流中的serialVersionUID与本地相应实体类的serialVersionUID进行比较，如果相同就认为是一致的，可以进行反序列化，否则就会出现序列化版本不一致的异常。(InvalidCastExcept ion)

**使用对象流序列化对象** 

+ 若某个类实现了 Serializable 接口，该类的对象就是可序列化的：
  + 创建一个 ObjectOutputStream
  + 调用 ObjectOutputStream 对象的 writeObject(对象) 方法输出可序列化对象
  + 注意写出一次，操作flush()一次
+ 反序列化
  + 创建一个 ObjectInputStream
  + 调用 readObject() 方法读取流中的对象
+ 强调：如果某个类的属性不是基本数据类型或 String 类型，而是另一个
  引用类型，那么这个引用类型必须是可序列化的，否则拥有该类型的
  Field 的类也不能序列化

```java
//序列化：将对象写入到磁盘或者进行网络传输。
//要求对象必须实现序列化
ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream(“data.txt"));
Person p = new Person("韩梅梅", 18, "中华大街", new Pet());
oos.writeObject(p);
oos.flush();
oos.close();
                                                                     
//反序列化：将磁盘中的对象数据源读出。
ObjectInputStream ois = new ObjectInputStream(new FileInputStream(“data.txt"));
Person p1 = (Person)ois.readObject();
System.out.println(p1.toString());
ois.close();     
```



### 10.10.随机存取文件流

**RandomAccessFile** **类** 

+ RandomAccessFile 声明在java.io包下，但直接继承于java.lang.Object类。并且它实现了DataInput、DataOutput这两个接口，也就意味着这个类既可以读也可以写。
+ RandomAccessFile 类支持 “随机访问” 的方式，程序可以直接跳到文件的任意地方来读、写文件
  + 支持只访问文件的部分内容
  + 可以向已存在的文件后追加内容
+ RandomAccessFile 对象包含一个记录指针，用以标示当前读写处的位置。RandomAccessFile 类对象可以自由移动记录指针：
  + long getFilePointer()：获取文件记录指针的当前位置
  + void seek(long pos)：将文件记录指针定位到 pos 位置

+ **构造器**
  + public RandomAccessFile(File file, String mode) 
  + public RandomAccessFile(String name, String mode)
+ 创建 RandomAccessFile 类实例需要指定一个 mode 参数，该参数指定 RandomAccessFile 的访问模式：
  + r: 以只读方式打开
  + rw：打开以便读取和写入
  + rwd:打开以便读取和写入；同步文件内容的更新
  + rws:打开以便读取和写入；同步文件内容和元数据的更新
+ 如果模式为只读r。则不会创建文件，而是会去读取一个已经存在的文件，如果读取的文件不存在则会出现异常。 如果模式为rw读写。如果文件不存在则会去创建文件，如果存在则不会创建

​        我们可以用RandomAccessFile这个类，来实现一个多线程断点下载的功能，用过下载工具的朋友们都知道，下载前都会建立两个临时文件，一个是与被下载文件大小相同的空文件，另一个是记录文件指针的位置文件，每次暂停的时候，都会保存上一次的指针，然后断点下载的时候，会继续从上一次的地方下载，从而实现断点下载或上传的功能，有兴趣的朋友们可以自己实现下。

**读取文件内容**

```java
RandomAccessFile raf = new RandomAccessFile(“test.txt”, “rw”）;
raf.seek(5);
byte [] b = new byte[1024];
int off = 0;
int len = 5;
raf.read(b, off, len);
String str = new String(b, 0, len);
System.out.println(str);
raf.close()
```

**写入文件内容**

```java
RandomAccessFile raf = new RandomAccessFile("test.txt", "rw");
raf.seek(5);
//先读出来
String temp = raf.readLine();
raf.seek(5);
raf.write("xyz".getBytes());
raf.write(temp.getBytes());
raf.close();


RandomAccessFile raf1 = new RandomAccessFile("hello.txt", "rw");
raf1.seek(5);
//方式一：
//StringBuilder info = new StringBuilder((int) file.length());
//byte[] buffer = new byte[10];
//int len;
//while((len = raf1.read(buffer)) != -1){
////info += new String(buffer,0,len);
//info.append(new String(buffer,0,len));
//}
//方式二：
ByteArrayOutputStream baos = new ByteArrayOutputStream();
byte[] buffer = new byte[10];
int len;
while((len = raf1.read(buffer)) != -1){
	baos.write(buffer, 0, len);
}
```

**总结**

+ 流是用来处理数据的。 

+ 处理数据时，一定要先明确**数据源**，与**数据目的地** 

+ 数据源可以是文件，可以是键盘。 

+ 数据目的地可以是文件、显示器或者其他设备。 

+ 而流只是在帮助数据进行传输,并对传输的数据进行处理，比如过滤处理、 转换处理等。

### 10.11. NIO.2中类的使用

+ Java NIO (New IO，Non-Blocking IO)是从Java 1.4版本开始引入的一套新的IO API，可以替代标准的Java IO API。NIO与原来的IO有同样的作用和目的，但是使用的方式完全不同，NIO支持面向缓冲区的(IO是面向流的)、基于通道的IO操作。NIO将以更加高效的方式进行文件的读写操作。
+ Java API中提供了两套NIO，一套是针对标准输入输出NIO，另一套就是网络编程NIO。
  + |-----java.nio.channels.Channel
    + |-----FileChannel:处理本地文件
    + |-----SocketChannel：TCP网络编程的客户端的Channel
    + |-----ServerSocketChannel:TCP网络编程的服务器端的Channel
    + |-----DatagramChannel：UDP网络编程中发送端和接收端的Channel

​        随着 JDK 7 的发布，Java对NIO进行了极大的扩展，增强了对文件处理和文件系统特性的支持，以至于我们称他们为 NIO.2。因为 NIO 提供的一些功能，NIO已经成为文件处理中越来越重要的部分

**核心API**

+ 早期的Java只提供了一个File类来访问文件系统，但File类的功能比较有限，所提供的方法性能也不高。而且，大多数方法在出错时仅返回失败，并不会提供异常信息。
+ NIO. 2为了弥补这种不足，引入了Path接口，代表一个平台无关的平台路径，描述了目录结构中文件的位置。Path可以看成是File类的升级版本，实际引用的资源也可以不存在。
+ 在以前IO操作都是这样写的:
  import java.io.File;
  File file = new File("index.html");
+ 但在Java7 中，我们可以这样写：
  import java.nio.file.Path; 
  import java.nio.file.Paths; 
  Path path = Paths.get("index.html");

+ 同时，NIO.2在java.nio.file包下还提供了Files、Paths工具类，Files包含了大量静态的工具方法来操作文件；Paths则包含了两个返回Path的静态工厂方法。
+ Paths 类提供的静态 get() 方法用来获取 Path 对象：
  + static Path get(String first, String … more) : 用于将多个字符串串连成路径
  + static Path get(URI uri): 返回指定uri对应的Path路径

**Path接口常用方法**

```java
String toString() ： 返回调用 Path 对象的字符串表示形式
boolean startsWith(String path) : 判断是否以 path 路径开始
boolean endsWith(String path) : 判断是否以 path 路径结束
boolean isAbsolute() : 判断是否是绝对路径
Path getParent() ：返回Path对象包含整个路径，不包含 Path 对象指定的文件路径
Path getRoot() ：返回调用 Path 对象的根路径
Path getFileName() : 返回与调用 Path 对象关联的文件名
int getNameCount() : 返回Path 根目录后面元素的数量
Path getName(int idx) : 返回指定索引位置 idx 的路径名称
Path toAbsolutePath() : 作为绝对路径返回调用 Path 对象
Path resolve(Path p) :合并两个路径，返回合并后的路径对应的Path对象
File toFile(): 将Path转化为File类的对象
```

**Files 类**

```java
java.nio.file.Files 用于操作文件或目录的工具类。
Files常用方法：
  Path copy(Path src, Path dest, CopyOption … how) : 文件的复制
  Path createDirectory(Path path, FileAttribute<?> … attr) : 创建一个目录
  Path createFile(Path path, FileAttribute<?> … arr) : 创建一个文件
  void delete(Path path) : 删除一个文件/目录，如果不存在，执行报错
  void deleteIfExists(Path path) : Path对应的文件/目录如果存在，执行删除
  Path move(Path src, Path dest, CopyOption…how) : 将 src 移动到 dest 位置
  long size(Path path) : 返回 path 指定文件的大小
Files常用方法：用于判断
  boolean exists(Path path, LinkOption … opts) : 判断文件是否存在
  boolean isDirectory(Path path, LinkOption … opts) : 判断是否是目录
  boolean isRegularFile(Path path, LinkOption … opts) : 判断是否是文件
  boolean isHidden(Path path) : 判断是否是隐藏文件
  boolean isReadable(Path path) : 判断文件是否可读
  boolean isWritable(Path path) : 判断文件是否可写
  boolean notExists(Path path, LinkOption … opts) : 判断文件是否不存在
Files常用方法：用于操作内容
  SeekableByteChannel newByteChannel(Path path, OpenOption…how) : 获取与指定文件的连接，
    其中how是指定打开方式。
  DirectoryStream<Path> newDirectoryStream(Path path) : 打开 path 指定的目录
  InputStream newInputStream(Path path, OpenOption…how):获取 InputStream 对象
  OutputStream newOutputStream(Path path, OpenOption…how) : 获取 OutputStream 对象
```



## 11.网络编程

​        Java是 Internet 上的语言，它从语言级上提供了对网络应用程序的支持，程序员能够很容易开发常见的网络应用程序。Java提供的网络类库，可以实现无痛的网络连接，联网的底层细节被隐藏在 Java 的本机安装系统里，由 JVM 进行控制。并且 Java 实现了一个跨平台的网络库，程序员面对的是一个统一的网络编程环境。

​		**计算机网络：** 把分布在不同地理区域的计算机与专门的外部设备用通信线路互连成一个规 模大、功能强的网络系统，从而使众多的计算机可以方便地互相传递信息、 共享硬件、软件、数据信息等资源。

​		**网络编程的目的：**直接或间接地通过网络协议与其它计算机实现数据交换，进行通讯。

​		**网络编程中有两个主要的问题：** 

+ 如何准确地定位网络上一台或多台主机；定位主机上的特定的应用
+ 找到主机后如何可靠高效地进行数据传输

通信方法

+ 通信双方地址
  + IP
  + 端口号
+ 一定的规则（即：网络通信协议。有两套参考模型）
  + OSI参考模型：模型过于理想化，未能在因特网上进行广泛推广
  + TCP/IP参考模型(或TCP/IP协议)：事实上的国际标准。

**网络通信协议**

<img src="D:\MyNote\images\1681569097141.png" alt="1681569097141" style="zoom:80%;" />

<img src="D:\MyNote\images\1681569126987.png" alt="1681569126987" style="zoom:67%;" />

### 11.1.IP与端口号

IP 地址：InetAddress

+ 唯一的标识 Internet 上的计算机（通信实体）
+ 本地回环地址(hostAddress)：127.0.0.1 主机名(hostName)：localhost
+ IP地址分类方式1：IPV4 和 IPV6
  + IPV4：4个字节组成，4个0-255。大概42亿，30亿都在北美，亚洲4亿。2011年初已经用尽。以点分十进制表示，如192.168.0.1
  + IPV6：128位（16个字节），写成8个无符号整数，每个整数用四个十六进制位表示，数之间用冒号（：）分开，如：3ffe:3201:1401:1280:c8ff:fe4d:db39:1984
+ IP地址分类方式2：公网地址(万维网使用)和私有地址(局域网使用)。192.168.开头的就是私有址址，范围即为192.168.0.0--192.168.255.255，专门为组织机构内部使用
+ 特点：不易记忆

**端口号**标识正在计算机上运行的进程（程序） 

+ 不同的进程有不同的端口号
+ 被规定为一个 16 位的整数 0~65535。
+ 端口分类：
  + 公认端口：0~1023。被预先定义的服务通信占用（如：HTTP占用端口80，FTP占用端口21，Telnet占用端口23）
  + 注册端口：1024~49151。分配给用户进程或应用程序。（如：Tomcat占用端口8080，MySQL占用端口3306，Oracle占用端口1521等）。
  + 动态/私有端口：49152~65535。

端口号与IP地址的组合得出一个网络套接字：Socket。

**InetAddress类**

+ Internet上的主机有两种方式表示地址： 
  + 域名(hostName)：www.atguigu.com 
  + IP 地址(hostAddress)：202.108.35.210 

+ InetAddress类主要表示IP地址，两个子类：Inet4Address、Inet6Address。 

+ InetAddress 类 对 象 含 有 一 个 Internet 主 机 地 址 的 域 名 和 IP 地 址 ： www.atguigu.com 和 202.108.35.210。 

+ 域名容易记忆，当在连接网络时输入一个主机的域名后，域名服务器(DNS) 负责将域名转化成IP地址，这样才能和主机建立连接。 -------域名解析

![1681569473847](D:\MyNote\images\1681569473847.png)

InetAddress类没有提供公共的构造器，而是提供了如下几个静态方法来获取
InetAddress实例

+ public static InetAddress getLocalHost()
+ public static InetAddress getByName(String host)

InetAddress提供了如下几个常用的方法

+ public String getHostAddress()：返回 IP 地址字符串（以文本表现形式）。
+ public String getHostName()：获取此 IP 地址的主机名
+ public boolean isReachable(int timeout)：测试是否可以达到该地址

![1681569631437](D:\MyNote\images\1681569631437.png)

### 11.2.网络协议

+ 网络通信协议
  计算机网络中实现通信必须有一些约定，即通信协议，对速率、传输代码、代码结构、传输控制步骤、出错控制等制定标准。
+ 问题：网络协议太复杂
  计算机网络通信涉及内容很多，比如指定源地址和目标地址，加密解密，压缩解压缩，差错控制，流量控制，路由控制，如何实现如此复杂的网络协议呢？
+ 通信协议分层的思想
  在制定协议时，把复杂成份分解成一些简单的成份，再将它们复合起来。最常用的复合方式是层次方式，即同层间可以通信、上一层可以调用下一层，而与再下一层不发生关系。各层互不影响，利于系统的开发和扩展。

**TCP/IP协议簇**

+ 传输层协议中有两个非常重要的协议：
  + 传输控制协议TCP(Transmission Control Protocol)
  + 用户数据报协议UDP(User Datagram Protocol)。
+ TCP/IP 以其两个主要协议：传输控制协议(TCP)和网络互联协议(IP)而得名，实际上是一组协议，包括多个具有不同功能且互为关联的协议。
+ IP(Internet Protocol)协议是网络层的主要协议，支持网络间互连的数据通信。
+ TCP/IP协议模型从更实用的角度出发，形成了高效的四层体系结构，即物理链路层、IP层、传输层和应用层。

**TCP** **和** **UDP**

TCP协议：

+ 使用TCP协议前，须先建立TCP连接，形成传输数据通道
+ 传输前，采用“三次握手”方式，点对点通信，是可靠的
+ TCP协议进行通信的两个应用进程：客户端、服务端。
+ 在连接中可进行大数据量的传输
+ 传输完毕，需释放已建立的连接，效率低

UDP协议：

+ 将数据、源、目的封装成数据包，不需要建立连接
+ 每个数据报的大小限制在64K内
+ 发送不管对方是否准备好，接收方收到也不确认，故是不可靠的
+ 可以广播发送
+ 发送数据结束时无需释放资源，开销小，速度快

![1681570542250](D:\MyNote\images\1681570542250.png)

![1681570563846](D:\MyNote\images\1681570563846.png)

### 11.3.Socket

+ 利用套接字(Socket)开发网络应用程序早已被广泛的采用，以至于成为事实上的标准。 

+ 网络上具有唯一标识的IP地址和端口号组合在一起才能构成唯一能识别的标识符套接字。 

+ 通信的两端都要有Socket，是两台机器间通信的端点。 

+ 网络通信其实就是Socket间的通信。 

+ Socket允许程序把网络连接当成一个流，数据在两个Socket间通过IO传输。 

+ 一般主动发起通信的应用程序属客户端，等待通信请求的为服务端。 

+ Socket分类： 
  + 流套接字（stream socket）：使用TCP提供可依赖的字节流服务 
  + 数据报套接字（datagram socket）：使用UDP提供“尽力而为”的数据报服务

Socket类的**常用构造器**：

+ public Socket(InetAddress address,int port)创建一个流套接字并将其连接到指定 IP 地址的指定端口号。
+ public Socket(String host,int port)创建一个流套接字并将其连接到指定主机上的指定端口号。

Socket类的**常用方法**：

+ public InputStream getInputStream()返回此套接字的输入流。可以用于接收网络消息
+ public OutputStream getOutputStream()返回此套接字的输出流。可以用于发送网络消息
+ public InetAddress getInetAddress()此套接字连接到的远程 IP 地址；如果套接字是未连接的，则返回 null。
+ public InetAddress getLocalAddress()获取套接字绑定的本地地址。 即本端的IP地址
+ public int getPort()此套接字连接到的远程端口号；如果尚未连接套接字，则返回 0。
+ public int getLocalPort()返回此套接字绑定到的本地端口。 如果尚未绑定套接字，则返回 -1。即本端的端口号。
+ public void close()关闭此套接字。套接字被关闭后，便不可在以后的网络连接中使用（即无法重新连接或重新绑定）。需要创建新的套接字对象。 关闭此套接字也将会关闭该套接字的 InputStream OutputStream。
+ public void shutdownInput()如果在套接字上调用 shutdownInput() 后从套接字输入流读取内容，则流将返回 EOF（文件结束符）。 即不能在从此套接字的输入流中接收任何数据。
+ public void shutdownOutput()禁用此套接字的输出流。对于 TCP 套接字，任何以前写入的数据都将被送，并且后跟 TCP 的正常连接终止序列。 如果在套接字上调用 shutdownOutput() 后写入套接字输出流，则该流将抛出 IOException。 即不能通过此套接字的输出流发送任何数据。

### 11.4.TCP网络编程

基于Socket的TCP编程

 Java语言的基于套接字编程分为服务端编程和客户端编程，其通信模型如图所示：

![1681648938629](D:\MyNote\images\1681648938629.png)

**客户端Socket的工作过程包含以下四个基本的步骤：**

+ 创建 Socket：根据指定服务端的 IP 地址或端口号构造 Socket 类对象。若服务器端响应，则建立客户端到服务器的通信线路。若连接失败，会出现异常。
+ 打开连接到 Socket 的输入/出流： 使用 getInputStream()方法获得输入流，使用getOutputStream()方法获得输出流，进行数据传输
+ 按照一定的协议对 Socket 进行读/写操作：通过输入流读取服务器放入线路的信息（但不能读取自己放入线路的信息），通过输出流将信息写入线程。
+ 关闭 Socket：断开客户端到服务器的连接，释放线路

**客户端创建Socket对象**

+ 客户端程序可以使用Socket类创建对象，创建的同时会自动向服务器方发起连接。Socket的构造器是：
  + Socket(String host,int port)throws UnknownHostException,IOException：向服务器(域名是host。端口号为port)发起TCP连接，若成功，则创建Socket对象，否则抛出异常。
  + Socket(InetAddress address,int port)throws IOException：根据InetAddress对象所表示的IP地址以及端口号port发起连接。
+ 客户端建立socketAtClient对象的过程就是向服务器发出套接字连接请求

```java
Socket s = new Socket(“192.168.40.165”,9999);
OutputStream out = s.getOutputStream();
out.write(" hello".getBytes());
s.close();
```

**服务器程序的工作过程包含以下四个基本的步骤：** 

+ 调用 ServerSocket(int port) ：创建一个服务器端套接字，并绑定到指定端口上。用于监听客户端的请求。
+ 调用 accept()：监听连接请求，如果客户端请求连接，则接受连接，返回通信套接字对象。
+ 调用 该Socket类对象的 getOutputStream() 和 getInputStream ()：获取输出流和输入流，开始网络数据的发送和接收。
+ 关闭ServerSocket和Socket对象：客户端访问结束，关闭通信套接字。

**服务器建立 ServerSocket 对象**

​		ServerSocket 对象负责等待客户端请求建立套接字连接，类似邮局某个窗口中的业务员。也就是说，服务器必须事先建立一个等待客户请求建立套接字连接的ServerSocket对象。所谓“接收”客户的套接字请求，就accept()方法会返回一个 Socket 对象

```java
ServerSocket ss = new ServerSocket(9999);
Socket s = ss.accept ();
InputStream in = s.getInputStream();
byte[] buf = new byte[1024];
int num = in.read(buf);
String str = new String(buf,0,num);
System.out.println(s.getInetAddress().toString()+”:”+str);
s.close();
ss.close();
```

![1681649383124](D:\MyNote\images\1681649383124.png)

**客户端—服务端**

客户端：1、自定义	2、浏览器

服务端： 1、自定义	2、Tomcat服务器

### 11.5. UDP网络编程

+ 类 DatagramSocket 和 DatagramPacket 实现了基于 UDP 协议网络程序。
+ UDP数据报通过数据报套接字 DatagramSocket 发送和接收，系统不保证UDP数据报一定能够安全送到目的地，也不能确定什么时候可以抵达。
+ DatagramPacket 对象封装了UDP数据报，在数据报中包含了发送端的IP地址和端口号以及接收端的IP地址和端口号。
+ UDP协议中每个数据报都给出了完整的地址信息，因此无须建立发送方和接收方的连接。如同发快递包裹一样。 

**DatagramSocket** **类的常用方法**

+ public DatagramSocket(int port)创建数据报套接字并将其绑定到本地主机上的指定端口。套接字将被绑定到通配符地址，IP 地址由内核来选择。
+ public DatagramSocket(int port,InetAddress laddr)创建数据报套接字，将其绑定到指定的本地地址。本地端口必须在 0 到 65535 之间（包括两者）。如果 IP 地址为 0.0.0.0，套接字将被绑定到通配符地址，IP 地址由内核选择。
+ public void close()关闭此数据报套接字。
+ public void send(DatagramPacket p)从此套接字发送数据报包。DatagramPacket 包含的信息指示：将要发送的数据、其长度、远程主机的 IP 地址和远程主机的端口号。
+ public void receive(DatagramPacket p)从此套接字接收数据报包。当此方法返回时，DatagramPacket的缓冲区填充了接收的数据。数据报包也包含发送方的 IP 地址和发送方机器上的端口号。 此方法在接收到数据报前一直阻塞。数据报包对象的 length 字段包含所接收信息的长度。如果信息比包的长度长，该信息将被截短。
+ public InetAddress getLocalAddress()获取套接字绑定的本地地址。
+ public int getLocalPort()返回此套接字绑定的本地主机上的端口号。
+ public InetAddress getInetAddress()返回此套接字连接的地址。如果套接字未连接，则返回 null。
+ public int getPort()返回此套接字的端口。如果套接字未连接，则返回 -1。

+ public DatagramPacket(byte[] buf,int length)构造 DatagramPacket，用来接收长度为 length 的数据包。 length 参数必须小于等于 buf.length。
+ public DatagramPacket(byte[] buf,int length,InetAddress address,int port)构造数据报包，用来将长度为 length 的包发送到指定主机上的指定端口号。length参数必须小于等于 buf.length。
+ public InetAddress getAddress()返回某台机器的 IP 地址，此数据报将要发往该机器或者是从该机器接收到的。
+ public int getPort()返回某台远程主机的端口号，此数据报将要发往该主机或者是从该主机接收到的。
+ public byte[] getData()返回数据缓冲区。接收到的或将要发送的数据从缓冲区中的偏移量 offset 处开始，持续 length 长度。
+ public int getLength()返回将要发送或接收到的数据的长度。

UDP网络通信

流 程：
1. DatagramSocket与DatagramPacket
2. 建立发送端，接收端
3. 建立数据包
4. 调用Socket的发送、接收方法
5. 关闭Socket

发送端与接收端是两个独立的运行程序

```java
发送端
DatagramSocket ds = null;
try {
    ds = new DatagramSocket();
    byte[] by = "hello,atguigu.com".getBytes();
    DatagramPacket dp = new DatagramPacket(by, 0, by.length, 
                                           InetAddress.getByName("127.0.0.1"), 10000);
    ds.send(dp);
} catch (Exception e) {
    e.printStackTrace();
} finally {
    if (ds != null)
        ds.close();
}


接收端
在接收端，要指定监听的端口。
DatagramSocket ds = null;
try {
    ds = new DatagramSocket(10000);
    byte[] by = new byte[1024];
    DatagramPacket dp = new DatagramPacket(by, by.length);
    ds.receive(dp);
    String str = new String(dp.getData(), 0, dp.getLength());
    System.out.println(str + "--" + dp.getAddress());
} catch (Exception e) {
    e.printStackTrace();
} finally {
    if (ds != null)
        ds.close();
}
```



### 11.6.URL编程

+ URL(Uniform Resource Locator)：统一资源定位符，它表示 Internet 上某一资源的地址。

+ 它是一种具体的URI，即URL可以用来标识一个资源，而且还指明了如何locate这个资源。

+ 通过 URL 我们可以访问 Internet 上的各种网络资源，比如最常见的 www，ftp 站点。浏览器通过解析给定的 URL 可以在网络上查找相应的文件或其他资源。

+ URL的基本结构由5部分组成：

  ​		 <传输协议>://<主机名>:<端口号>/<文件名>#片段名?参数列表

  例如: http://192.168.1.100:8080/helloworld/index.jsp#a?username=shkstart&password=123

  + #片段名：即锚点，例如看小说，直接定位到章节
  + 参数列表格式：参数名=参数值&参数名=参数值....

为了表示URL，java.net 中实现了类 URL。我们可以通过下面的构造器来初始化一个 URL 对象：

+ public URL (String spec)：通过一个表示URL地址的字符串可以构造一个URL对象。例如：URL url = new URL ("http://www. atguigu.com/"); 
+ public URL(URL context, String spec)：通过基 URL 和相对 URL 构造一个 URL 对象。例如：URL downloadUrl = new URL(url, “download.html")
+ public URL(String protocol, String host, String file); 例如：new URL("http", "www.atguigu.com", “download. html");
+ public URL(String protocol, String host, int port, String file); 例如: URL gamelan = new URL("http", "www.atguigu.com", 80, “download.html");
+ URL类的构造器都声明抛出非运行时异常，必须要对这一异常进行处理，通常是用 try-catch 语句进行捕获 

一个URL对象生成后，其属性是不能被改变的，但可以通过它给定的方法来获取这些属性：

+ public String getProtocol( ) 获取该URL的协议名
+ public String getHost( ) 获取该URL的主机名
+ public String getPort( ) 获取该URL的端口号
+ public String getPath( ) 获取该URL的文件路径
+ public String getFile( ) 获取该URL的文件名
+ public String getQuery( ) 获取该URL的查询名

```java
URL url = new URL("http://localhost:8080/examples/myTest.txt");
System.out.println("getProtocol() :"+url.getProtocol());
System.out.println("getHost() :"+url.getHost());
System.out.println("getPort() :"+url.getPort());
System.out.println("getPath() :"+url.getPath());
System.out.println("getFile() :"+url.getFile());
System.out.println("getQuery() :"+url.getQuery());
```

**针对HTTP协议的URLConnection类**

+ URL的方法 openStream()：能从网络上读取数据 

+ 若希望输出数据，例如向服务器端的 CGI （公共网关接口-Common Gateway  Interface-的简称，是用户浏览器和服务器端的应用程序进行连接的接口）程序发送一 些数据，则必须先与URL建立连接，然后才能对其进行读写，此时需要使用 URLConnection 。 

+ URLConnection：表示到URL所引用的远程对象的连接。当与一个URL建立连接时， 首先要在一个 URL 对象上通过方法 **openConnection()** 生成对应的 URLConnection 对象。如果连接过程失败，将产生IOException.  
  + URL netchinaren = new URL ("http://www.atguigu.com/index.shtml");  
  + URLConnectonn u = netchinaren.openConnection( ); 

通过URLConnection对象获取的输入流和输出流，即可以与现有的CGI程序进行交互。

+ public Object getContent( ) throws IOException
+ public int getContentLength( )
+ public String getContentType( )
+ public long getDate( )
+ public long getLastModified( )
+ public InputStream getInputStream( )throws IOException
+ public OutputSteram getOutputStream( )throws IOException

**URI、URL和URN的区别**

​		URI，是uniform resource identifier，统一资源标识符，用来唯一的标识一个资源。而URL是uniform resource locator，统一资源定位符，它是一种具体的URI，即URL可以用来标识一个资源，而且还指明了如何locate这个资源。而URN，uniform resource name，统一资源命名，是通过名字来标识资源，比如mailto:java-net@java.sun.com。也就是说，URI是以一种抽象的，高层次概念定义统一资源标识，而URL、URN则是具体的资源标识的方式。URL和URN都是一种URI。在Java的URI中，一个URI实例可以代表绝对的，也可以是相对的，只要它符合URI的语法规则。而URL类则不仅符合语义，还包含了定位该资源的信息，因此它不能是相对的

**小 结**

+ 位于网络中的计算机具有唯一的IP地址，这样不同的主机可以互相区分。
+ 客户端－服务器是一种最常见的网络应用程序模型。服务器是一个为其客户端提供某种特定服务的硬件或软件。客户机是一个用户应用程序，用于访问某台服务器提供的服务。端口号是对一个服务的访问场所，它用于区分同一物理计算机上的多个服务。套接字用于连接客户端和服务器，客户端和服务器之间的每个通信会话使用一个不同的套接字。TCP协议用于实现面向连接的会话。
+ Java 中有关网络方面的功能都定义在 java.net 程序包中。Java 用 InetAddress 对象表示 IP 地址，该对象里有两个字段：主机名(String) 和 IP 地址(int)。
+ 类 Socket 和 ServerSocket 实现了基于TCP协议的客户端－服务器程序。Socket是客户端和服务器之间的一个连接，连接创建的细节被隐藏了。这个连接提供了一个安全的数据传输通道，这是因为 TCP 协议可以解决数据在传送过程中的丢失、损坏、重复、乱序以及网络拥挤等问题，它保证数据可靠的传送。
+ 类 URL 和 URLConnection 提供了最高级网络应用。URL 的网络资源的位置来同一表示Internet 上各种网络资源。通过URL对象可以创建当前应用程序和 URL 表示的网络资源之间的连接，这样当前程序就可以读取网络资源数据，或者把自己的数据传送到网络上去。

## 12.反射机制

**Java Reflection**

​		Reflection（反射）是被视为动态语言的关键，反射机制允许程序在执行期借助于Reflection API取得任何类的内部信息，并能直接操作任意对象的内部属性及方法。加载完类之后，在堆内存的方法区中就产生了一个Class类型的对象（一个 类只有一个Class对象），这个对象就包含了完整的类的结构信息。我们可以通过这个对象看到类的结构。这个对象就像一面镜子，透过这个镜子看到类的结构，所以，我们形象的称之为：**反射**。

正常方式： 引入需要的”包类”名称 =>通过new实例化 =>取得实例化对象 

反射方式： 实例化对象 =>getClass()方法 =>得到完整的“包类”名称

**补充**

1、动态语言
		是一类在运行时可以改变其结构的语言：例如新的函数、对象、甚至代码可以被引进，已有的函数可以被删除或是其他结构上的变化。通俗点说就是在运行时代码可以根据某些条件改变自身结构。主要动态语言：Object-C、C#、JavaScript、PHP、Python、Erlang。
2、静态语言
		与动态语言相对应的，运行时结构不可变的语言就是静态语言。如Java、C、C++。

​		Java不是动态语言，但Java可以称之为“准动态语言”。即Java有一定的动态性，我们可以利用反射机制、字节码操作获得类似动态语言的特性。 Java的动态性让编程的时候更加灵活！

**Java反射机制提供的功能** 

+ 在运行时判断任意一个对象所属的类 

+ 在运行时构造任意一个类的对象 

+ 在运行时判断任意一个类所具有的成员变量和方法 

+ 在运行时获取泛型信息 

+ 在运行时调用任意一个对象的成员变量和方法 

+ 在运行时处理注解 

+ 生成动态代理

**主要API**

+ java.lang.Class:代表一个类
+ java.lang.reflect.Method:代表类的方法
+ java.lang.reflect.Field:代表类的成员变量
+ java.lang.reflect.Constructor:代表类的构造器

### 12.1.理解Class类

在Object类中定义了以下的方法，此方法将被所有子类继承：
● public final Class getClass()
以上的方法返回值的类型是一个Class类，此类是Java反射的源头，实际上所谓反射从程序的运行结果来看也很好理解，即：可以通过对象反射求出类的名称。

对象照镜子后可以得到的信息：某个类的属性、方法和构造器、某个类到底实现了哪些接口。对于每个类而言，JRE 都为其保留一个不变的 Class 类型的对象。一个 Class 对象包含
了特定某个结构(class/interface/enum/annotation/primitive type/void/[])的有关信息。

+ Class本身也是一个类
+ Class 对象只能由系统建立对象
+ 一个加载的类在 JVM 中只会有一个Class实例
+ 一个Class对象对应的是一个加载到JVM中的一个.class文件
+ 每个类的实例都会记得自己是由哪个 Class 实例所生成
+ 通过Class可以完整地得到一个类中的所有被加载的结构
+ Class类是Reflection的根源，针对任何你想动态加载、运行的类，唯有先获得相应的Class对象

**常用方法** 

![1681737032862](D:\MyNote\images\1681737032862.png)

```java
String str = "test4.Person";//test4.Person是test4包下的Person类
Class clazz = Class.forName(str);
Object obj = clazz.newInstance();
Field field = clazz.getField("name");
field.set(obj, "Peter");
Object name = field.get(obj);
System.out.println(name);
```

获取Class类的实例(四种方法)

1）前提：若已知具体的类，通过类的class属性获取，该方法最为安全可靠，程序性能最高
实例：Class clazz = String.class;
2）前提：已知某个类的实例，调用该实例的getClass()方法获取Class对象
实例：Class clazz = “www.atguigu.com”.getClass();
3）前提：已知一个类的全类名，且该类在类路径下，可通过Class类的静态方法forName()获取，可能抛出ClassNotFoundException
实例：Class clazz = Class.forName(“java.lang.String”);
4）其他方式(不做要求)
ClassLoader cl = this.getClass().getClassLoader();
Class clazz4 = cl.loadClass(“类的全类名”);

哪些类型可以有Class对象

（1）class：外部类，成员(成员内部类，静态内部类)，局部内部类，匿名内部类
（2）interface：接口
（3）[]：数组
（4）enum：枚举
（5）annotation：注解@interface
（6）primitive type：基本数据类型
（7）void

```java
Class c1 = Object.class;
Class c2 = Comparable.class;
Class c3 = String[].class;
Class c4 = int[][].class;
Class c5 = ElementType.class;
Class c6 = Override.class;
Class c7 = int.class;
Class c8 = void.class;
Class c9 = Class.class;
int[] a = new int[10];
int[] b = new int[100];
Class c10 = a.getClass();
Class c11 = b.getClass();
// 只要元素类型与维度一样，就是同一个Class
System.out.println(c10 == c11);
```



### 12.2.类的加载

**类的加载过程**--**了解**

**类的加载(Load)=>类的链接(Link)=>类的初始化(Initialize)**

**类的加载**：将类的class文件读入内存，并为之创建一个java.lang.Class对象。此过程由类加载器完成

**类的链接**：将类的二进制数据合并到JRE中 

**类的初始化**：JVM负责对类进行初始化 

**加载**：将class文件字节码内容加载到内存中，并将这些静态数据转换成方法区的运行时数据结构，然后生成一个代表这个类的java.lang.Class对象，作为方法区中类数据的访问入口（即引用地址）。所有需要访问和使用类数据只能通过这个Class对象。这个加载的过程需要类加载器参与。 

**链接**：将Java类的二进制代码合并到JVM的运行状态之中的过程。 

+ 验证：确保加载的类信息符合JVM规范，例如：以cafe开头，没有安全方面的问题 

+ 准备：正式为类变量（static）分配内存并**设置类变量默认初始值**的阶段，这些内存都将在方法区中进行分配。 

+ 解析：虚拟机常量池内的符号引用（常量名）替换为直接引用（地址）的过程。 

**初始化**：

+ 执行类构造器`<clinit>`()方法的过程。类构造器`<clinit>`()方法是由编译期自动收集类中所有类变量的赋值动作和静态代码块中的语句合并产生的。（类构造器是构造类信息的，不是构造该类对象的构造器）。
+ 当初始化一个类的时候，如果发现其父类还没有进行初始化，则需要先触发其父类的初始化。
+ 虚拟机会保证一个类的`<clinit>`()方法在多线程环境中被正确加锁和同步。

```java
public class ClassLoadingTest {
    public static void main(String[] args) {
        System.out.println(A.m);
    }
}
class A {
    static {
        m = 300;
    }
    static int m = 100;
}
//第二步：链接结束后m=0
//第三步：初始化后，m的值由<clinit>()方法执行决定
// 这个A的类构造器<clinit>()方法由类变量的赋值和静态代码块中的语句按照顺序合并产生，类似于
    // <clinit>(){
    // m = 300;
    // m = 100;
    // }
```

**类初始化的时机**--**了解**

**类的主动引用（一定会发生类的初始化）** 

+ 当虚拟机启动，先初始化main方法所在的类 

+ new一个类的对象 

+ 调用类的静态成员（除了final常量）和静态方法 

+ 使用java.lang.reflect包的方法对类进行反射调用 

+ 当初始化一个类，如果其父类没有被初始化，则先会初始化它的父类 

**类的被动引用（不会发生类的初始化）** 

+ 当访问一个静态域时，只有真正声明这个域的类才会被初始化 

+ 当通过子类引用父类的静态变量，不会导致子类初始化 

+ 通过数组定义类引用，不会触发此类的初始化 

+ 引用常量不会触发此类的初始化（常量在链接阶段就存入调用类的常量池中了）

```java
public class ClassLoadingTest {
    public static void main(String[] args) {
        // 主动引用：一定会导致A和Father的初始化
        // A a = new A();
        // System.out.println(A.m);
        // Class.forName("com.atguigu.java2.A");
        // 被动引用
        A[] array = new A[5];//不会导致A和Father的初始化
        // System.out.println(A.b);//只会初始化Father
        // System.out.println(A.M);//不会导致A和Father的初始化
    }
    static {
        System.out.println("main所在的类");
    }
}

class Father {
    static int b = 2;
    static {
        System.out.println("父类被加载");
    }
}
class A extends Father {
    static {
        System.out.println("子类被加载");
        m = 300;
    }
    static int m = 100;
    static final int M = 1;
}
```

![1681739509888](D:\MyNote\images\1681739509888.png)

**类加载器的作用**：

+ 类加载的作用：将class文件字节码内容加载到内存中，并将这些静态数据转换成方法区的运行时数据结构，然后在堆中生成一个代表这个类的java.lang.Class对象，作为方法区中类数据的访问入口。
+ 类缓存：标准的JavaSE类加载器可以按要求查找类，但一旦某个类被加载到类加载器中，它将维持加载（缓存）一段时间。不过JVM垃圾回收机制可以回收这些Class对象。

了解：**ClassLoader**

类加载器作用是用来把类(class)装载进内存的。JVM 规范定义了如下类型的类的加载器。

<img src="D:\MyNote\images\1681739693709.png" alt="1681739693709" style="zoom:80%;" />

**引导类加载器**：用C++编写的，是JVM自带的类加载器，负责Java平台核心库，用来装载核心类库。该加载器无法直接获取

**扩展类加载器**：负责jre/lib/ext目录下的jar包或java –D java.ext.dirs 指定目录下的jar包装入工作库 

**系统类加载器**：负责java –classpath 或 –D  java.class.path所指的目录下的类与jar包装入工作 ，是最常用的加载器

```java
//1.获取一个系统类加载器
ClassLoader classloader = ClassLoader.getSystemClassLoader();
System.out.println(classloader);
//2.获取系统类加载器的父类加载器，即扩展类加载器
classloader = classloader.getParent();
System.out.println(classloader);
//3.获取扩展类加载器的父类加载器，即引导类加载器
classloader = classloader.getParent();
System.out.println(classloader);
//4.测试当前类由哪个类加载器进行加载
classloader = Class.forName("exer2.ClassloaderDemo").getClassLoader();
System.out.println(classloader);
//5.测试JDK提供的Object类由哪个类加载器加载
classloader = Class.forName("java.lang.Object").getClassLoader();
System.out.println(classloader);
//6.关于类加载器的一个主要方法：getResourceAsStream(String str):获取类路径下的指定文件的输入流
InputStream in = null;
in = this.getClass().getClassLoader().getResourceAsStream("exer2\\test.properties");
System.out.println(in);
```



### 12.3.运行时类的对象

#### 12.3.1.创建方式

使用Class对象

创建类的对象：调用Class对象的newInstance()方法要 求： 

1）类必须有一个无参数的构造器。
2）类的构造器的访问权限需要足够。

**难道没有无参的构造器就不能创建对象了吗？** 

不是！只要在操作的时候明确的调用类中的构造器，并将参数传递进去之后，才可以实例化操作。 

步骤如下： 

1）通过Class类的**getDeclaredConstructor(Class … parameterTypes)**取得本类的指定形参类型的构造器 

2）向构造器的形参中传递一个对象数组进去，里面包含了构造器中所需的各个参数。 

3）通过Constructor实例化对象。

在Constructor类中存在一个方法`public T newInstance(Object... initargs)`

以上是反射机制应用最多的地方

```java
//1.根据全类名获取对应的Class对象
String name = “atguigu.java.Person";
Class clazz = null;
clazz = Class.forName(name);
//2.调用指定参数结构的构造器，生成Constructor的实例
Constructor con = clazz.getConstructor(String.class,Integer.class);
//3.通过Constructor的实例创建对应类的对象，并初始化类属性
Person p2 = (Person) con.newInstance("Peter",20);
System.out.println(p2);
```



#### 12.3.2.获取完整结构

**通过反射获取运行时类的完整结构**

Field、Method、Constructor、Superclass、Interface、Annotation

+ 实现的全部接口 

+ 所继承的父类 

+ 全部的构造器 

+ 全部的方法 

+ 全部的Field

使用反射可以取得：
1.**实现的全部接口**

+ public Class<?>[] getInterfaces() 

  确定此对象所表示的类或接口实现的接口。

2.**所继承的父类**

+ public Class<? Super T> getSuperclass()
  返回表示此 Class 所表示的实体（类、接口、基本类型）的父类的Class。

3.**全部的构造器**

+ public Constructor<T>[] getConstructors()
  返回此 Class 对象所表示的类的所有public构造方法。
+ public Constructor<T>[] getDeclaredConstructors()
  返回此 Class 对象表示的类声明的所有构造方法。
+ Constructor类中：
  + 取得修饰符: public int getModifiers();
  + 取得方法名称: public String getName();
  + 取得参数的类型：public Class<?>[] getParameterTypes();

4.**全部的方法**

+ public Method[] getDeclaredMethods()
  返回此Class对象所表示的类或接口的全部方法
+ public Method[] getMethods() 
  返回此Class对象所表示的类或接口的public的方法
+ Method类中：
  + public Class<?> getReturnType()取得全部的返回值
  + public Class<?>[] getParameterTypes()取得全部的参数
  + public int getModifiers()取得修饰符
  + public Class<?>[] getExceptionTypes()取得异常信息

5.**全部的Field**

+ public Field[] getFields() 
  返回此Class对象所表示的类或接口的public的Field。
+ public Field[] getDeclaredFields() 
  返回此Class对象所表示的类或接口的全部Field。
+ Field方法中：
  + public int getModifiers() 以整数形式返回此Field的修饰符
  + public Class<?> getType() 得到Field的属性类型
  + public String getName() 返回Field的名称。

6. Annotation相关
+ get Annotation(Class<T> annotationClass) 
+ getDeclaredAnnotations() 
7. 泛型相关
    获取父类泛型类型：Type getGenericSuperclass()
    泛型类型：ParameterizedType
    获取实际的泛型类型参数数组：getActualTypeArguments()
8. 类所在的包 Package getPackage()

小 结：
1.在实际的操作中，取得类的信息的操作代码，并不会经常开发。
2.一定要熟悉java.lang.reflect包的作用，反射机制。
3.如何取得属性、方法、构造器的名称，修饰符等。

#### 12.3.3.调用指定结构

1.**调用指定方法**

通过反射，调用类中的方法，通过Method类完成。步骤：
1.通过Class类的getMethod(String name,Class…parameterTypes)方法取得一个Method对象，并设置此方法操作时所需要的参数类型。

2.之后使用**Object invoke(Object obj, Object[] args)**进行调用，并向方法中传递要设置的obj对象的参数信息。

<img src="D:\MyNote\images\1681740840924.png" alt="1681740840924" style="zoom:80%;" />

**Object invoke(Object obj, Object … args)**

说明：
1.Object 对应原方法的返回值，若原方法无返回值，此时返回null
2.若原方法若为静态方法，此时形参Object obj可为null
3.若原方法形参列表为空，则Object[] args为null
4.若原方法声明为private,则需要在调用此invoke()方法前，显式调用方法对象的setAccessible(true)方法，将可访问private的方法

2.**调用指定属性**
在反射机制中，可以直接通过Field类操作类中的属性，通过Field类提供的set()和get()方法就可以完成设置和取得属性内容的操作。

+ public Field getField(String name) 返回此Class对象表示的类或接口的指定的public的Field。
+ public Field getDeclaredField(String name)返回此Class对象表示的类或接口的指定的Field。
+ 在Field中：
  + public Object get(Object obj) 取得指定对象obj上此Field的属性内容
  + public void set(Object obj,Object value) 设置指定对象obj上此Field的属性内容

关于**setAccessible**方法的使用

+ Method和Field、Constructor对象都有setAccessible()方法。
+ setAccessible启动和禁用访问安全检查的开关。
+ 参数值为true则指示反射的对象在使用时应该取消Java语言访问检查。
+ 提高反射的效率。如果代码中必须用反射，而该句代码需要频繁的被调用，那么请设置为true。
+ 使得原本无法访问的私有成员也可以访问 
+ 参数值为false则指示反射的对象应该实施Java语言访问检查。

### 12.4.动态代理

代理设计模式的原理: 
		使用一个代理将对象包装起来, 然后用该代理对象取代原始对象。任何对原始对象的调用都要通过代理。代理对象决定是否以及何时将方法调用转到原始对象上。
		之前为大家讲解过代理机制的操作，属于静态代理，特征是代理类和目标对象的类都是在编译期间确定下来，不利于程序的扩展。同时，每一个代理类只能为一个接口服务，这样一来程序开发中必然产生过多的代理。最
好可以通过一个代理类完成全部的代理功能。

+ 动态代理是指客户通过代理类来调用其它对象的方法，并且是在程序运行时根据需要动态创建目标类的代理对象。
+ 动态代理使用场合:
  + 调试
  + 远程方法调用
+ 动态代理相比于静态代理的优点：
  抽象角色中（接口）声明的所有方法都被转移到调用处理器一个集中的方法中处理，这样，我们可以更加灵活和统一的处理众多的方法。

**相关API**

**Proxy** ：专门完成代理的操作类，是所有动态代理类的父类。通过此类为一个或多个接口动态地生成实现类。

提供用于创建动态代理类和动态代理对象的静态方法

+ `static Class<?> getProxyClass(ClassLoader loader, Class<?>... interfaces) `创建一个动态代理类所对应的Class对象
+ `static Object newProxyInstance(ClassLoader loader, Class<?>[] interfaces, InvocationHandler h) `直接创建一个动态代理对象

loader是类加载器，interfaces是得到被代理类实现的全部接口，h是得到InvocationHandler接口的实现类实例

**动态代理步骤**

1.创建一个实现接口InvocationHandler的类，它必须实现invoke方法，以完成代理的具体操作。

```java
public Object invoke(Object theProxy, Method method, Object[] params) 
    throws Throwable{
    try{
        Object retval = method.invoke(targetObj, params);
        // Print out the result
        System.out.println(retval);
        return retval;
    }catch (Exception exc){}
}
theProxy--代理类的对象
method--要调用的方法
params--方法调用时所需要的参数
```

2.创建被代理的类以及接口 

<img src="D:\MyNote\images\1681741668914.png" alt="1681741668914" style="zoom:50%;" />

3.通过Proxy的静态方法

newProxyInstance(ClassLoader loader, Class[] interfaces, InvocationHandler h) 创建一个Subject接口代理

```java
RealSubject target = new RealSubject();
// Create a proxy to wrap the original implementation
DebugProxy proxy = new DebugProxy(target);
// Get a reference to the proxy through the Subject interface
Subject sub = (Subject) Proxy.newProxyInstance(
Subject.class.getClassLoader(),new Class[] { Subject.class }, proxy);
```

4.通过 Subject代理调用RealSubject实现类的方法
String info = sub.say(“Peter", 24);
System.out.println(info);

动态代理与AOP（Aspect Orient Programming)

前面介绍的Proxy和InvocationHandler，很难看出这种动态代理的优势，下面介绍一种更实用的动态代理机制

<img src="D:\MyNote\images\1681741806369.png" alt="1681741806369" style="zoom: 67%;" />

<img src="D:\MyNote\images\1681741826170.png" alt="1681741826170" style="zoom:67%;" />

**改进后的说明**：代码段1、代码段2、代码段3和深色代码段分离开了，但代码段1、2、3又和一个特定的方法A耦合了！最理想的效果是：代码块1、2、3既可以执行方法A，又无须在程序中以硬编码的方式直接调用深色代码的方法

```java
public interface Dog{
    void info();
    void run();
}

public class HuntingDog implements Dog{
    public void info(){
        System.out.println("我是一只猎狗");
    }
    public void run(){
        System.out.println("我奔跑迅速");
    }
}

public class DogUtil{
    public void method1(){
        System.out.println("=====模拟通用方法一=====");
    }
    public void method2(){
        System.out.println("=====模拟通用方法二=====");
    }
}

public class MyInvocationHandler implements InvocationHandler{
    // 需要被代理的对象
    private Object target;
    public void setTarget(Object target){
        this.target = target;
    }
    // 执行动态代理对象的所有方法时，都会被替换成执行如下的invoke方法
    public Object invoke(Object proxy, Method method, Object[] args)
        throws Exception{
        DogUtil du = new DogUtil();
        // 执行DogUtil对象中的method1。
        du.method1();
        // 以target作为主调来执行method方法
        Object result = method.invoke(target , args);
        // 执行DogUtil对象中的method2。
        du.method2();
        return result;
    }
}

public class MyProxyFactory{
    // 为指定target生成动态代理对象
    public static Object getProxy(Object target) throws Exception{
        // 创建一个MyInvokationHandler对象
        MyInvokationHandler handler = new MyInvokationHandler();
        // 为MyInvokationHandler设置target对象
        handler.setTarget(target);
        // 创建、并返回一个动态代理对象
        return Proxy.newProxyInstance(target.getClass().getClassLoader()
                                   , target.getClass().getInterfaces() , handler);
    }
}

public class Test{
    public static void main(String[] args) throws Exception{
        // 创建一个原始的HuntingDog对象，作为target
        Dog target = new HuntingDog();
        // 以指定的target来创建动态代理
        Dog dog = (Dog)MyProxyFactory.getProxy(target);
        dog.info();
        dog.run();
    }
}
```

​		使用Proxy生成一个动态代理时，往往并不会凭空产生一个动态代理，这样没有太大的意义。通常都是为指定的目标对象生成动态代理。这种动态代理在AOP中被称为AOP代理，AOP代理可代替目标对象，AOP代理包含了目标对象的全部方法。但AOP代理中的方法与目标对象的方法存在差异： **AOP**代理里的方法可以在执行目标方法之前、之后插入一些通用处理

<img src="D:\MyNote\images\1681742346016.png" alt="1681742346016" style="zoom:67%;" />

## 13.Java8新特性

​		Java 8 (又称为 jdk 1.8) 是 Java 语言开发的一个主要版本。Java 8 是oracle公司于2014年3月发布，可以看成是自Java 5 以来最具革命性的版本。Java 8为Java语言、编译器、类库、开发工具与JVM带来了大量新特性

![1681914419657](D:\MyNote\images\1681914419657.png)

+ 速度更快
+ 代码更少(增加了新的语法：Lambda 表达式)
+ 强大的 Stream API
+ 便于并行
+ 最大化减少空指针异常：Optional
+ Nashorn引擎，允许在JVM上运行JS应用

**并行流与串行流**

​		并行流就是把一个内容分成多个数据块，并用不同的线程分别处理每个数据块的流。相比较串行的流，并行的流可以很大程度上提高程序的执行效率。Java 8 中将并行进行了优化，我们可以很容易的对数据进行并行操作。 Stream API 可以声明性地通过 parallel() 与 sequential() 在并行流与顺序流之间进行切换。

### 13.1. Lambda表达式

​		Lambda 是一个匿名函数，我们可以把 Lambda 表达式理解为是一段可以传递的代码（将代码像数据一样进行传递）。使用它可以写出更简洁、更灵活的代码。作为一种更紧凑的代码风格，使Java的语言表达能力得到了提升。

从匿名类到 Lambda 的转换举例1

<img src="D:\MyNote\images\1681914625058.png" alt="1681914625058" style="zoom: 67%;" />

<img src="D:\MyNote\images\1681914643133.png" alt="1681914643133" style="zoom:67%;" />

举例2

<img src="D:\MyNote\images\1681914910793.png" alt="1681914910793" style="zoom:67%;" />

**语法**

Lambda 表达式：在Java 8 语言中引入的一种新的语法元素和操作符。这个操作符为 “->” ， 该操作符被称为 Lambda 操作符或箭头操作符。它将 Lambda 分为两个部分：
**左侧**：指定了 Lambda 表达式需要的参数列表
**右侧**：指定了 Lambda 体，是抽象方法的实现逻辑，也即Lambda 表达式要执行的功能

<img src="D:\MyNote\images\1681915219417.png" alt="1681915219417" style="zoom:67%;" />

<img src="D:\MyNote\images\1681915289686.png" alt="1681915289686" style="zoom:67%;" />

**类型推断**

上述 Lambda 表达式中的参数类型都是由编译器推断得出的。Lambda 表达式中无需指定类型，程序依然可以编译，这是因为 javac 根据程序的上下文，在后台推断出了参数的类型。Lambda 表达式的类型依赖于上下文环境，是由编译器推断出来的。这就是所谓的“类型推断”。

### 13.2.函数式接口

​		只包含一个抽象方法的接口，称为函数式接口。你可以通过 Lambda 表达式来创建该接口的对象。（若 Lambda 表达式抛出一个受检异常(即：非运行时异常)，那么该异常需要在目标接口的抽象方法上进行声明）。我们可以在一个接口上使用 **@FunctionalInterface** 注解，这样做可以检查它是否是一个函数式接口。同时javadoc 也会包含一条声明，说明这个接口是一个函数式接口。 在java.util.function包下定义了Java 8 的丰富的函数式接口。

​		Java从诞生日起就是一直倡导“一切皆对象”，在Java里面面向对象(OOP) 编程是一切。但是随着python、scala等语言的兴起和新技术的挑战，Java不 得不做出调整以便支持更加广泛的技术要求，也即java不但可以支持OOP还 可以支持OOF（面向函数编程） 。

​		在函数式编程语言当中，函数被当做一等公民对待。在将函数作为一等公民的编程语言中，Lambda表达式的类型是函数。但是在Java8中，有所不同。在 Java8中，Lambda表达式是对象，而不是函数，它们必须依附于一类特别的对象类型——函数式接口。简单的说，在Java8中，Lambda表达式就是一个函数式接口的实例。这就是Lambda表达式和函数式接口的关系。也就是说，只要一个对象是函数式接口的实例，那么该对象就可以用Lambda表达式来表示。所以以前用匿名实现类表示的现在都可以用Lambda表达式来写。

<img src="D:\MyNote\images\1681915687610.png" alt="1681915687610" style="zoom:67%;" />

**自定义函数式接口**

<img src="D:\MyNote\images\1681915712139.png" alt="1681915712139" style="zoom:50%;" />

**函数式接口中使用泛型：**

<img src="D:\MyNote\images\1681915735634.png" alt="1681915735634" style="zoom:50%;" />

**作为参数传递** **Lambda** **表达式**

<img src="D:\MyNote\images\1681915797745.png" alt="1681915797745" style="zoom:67%;" />

作为参数传递 Lambda 表达式：为了将 Lambda 表达式作为参数传递，接收Lambda表达式的参数类型必须是与该 Lambda 表达式兼容的函数式接口的类型。

**Java** **内置四大核心函数式接口**

![1681916076765](D:\MyNote\images\1681916076765.png)

**其他接口** 

![1681916126740](D:\MyNote\images\1681916126740.png)

### 13.3.方法引用与构造器引用

**方法引用**

+ 当要传递给Lambda体的操作，已经有实现的方法了，可以使用方法引用！
+ 方法引用可以看做是Lambda表达式深层次的表达。换句话说，方法引用就是Lambda表达式，也就是函数式接口的一个实例，通过方法的名字来指向一个方法，可以认为是Lambda表达式的一个语法糖。
+ 要求：实现接口的抽象方法的参数列表和返回值类型，必须与方法引用的方法的参数列表和返回值类型保持一致！
+ 格式：使用操作符 “::” 将类(或对象) 与 方法名分隔开来。
+ 如下三种主要使用情况：
  + 对象::实例方法名
  + 类::静态方法名
  + 类::实例方法名

![1683121267387](D:\MyNote\images\1683121267387.png)

BiPredicate是函数式接口，有一个抽象方法test

![1683121361882](D:\MyNote\images\1683121361882.png)

注意：当函数式接口方法的第一个参数是需要引用方法的调用者，并且第二个参数是需要引用方法的参数(或无参数)时：ClassName::methodName

**构造器引用**

**格式：** **ClassName::new**  

与函数式接口相结合，自动与函数式接口中方法兼容。可以把构造器引用赋值给定义的方法，要求构造器参数列表要与接口中抽象方法的参数列表一致！且方法的返回值即为构造器对应类的对象。

![1683122947598](D:\MyNote\images\1683122947598.png)

**数组引用** 

**格式：** **type[] :: new**

![1683123018570](D:\MyNote\images\1683123018570.png)

### 13.4.Stream API

+ Java8中有两大最为重要的改变。第一个是 Lambda 表达式；另外一个则是 Stream API。

+ Stream API ( java.util.stream) 把真正的函数式编程风格引入到Java中。这是目前为止对Java类库最好的补充，因为Stream API可以极大提高Java程序员的生产力，让程序员写出高效率、干净、简洁的代码。

+ Stream 是 Java8 中处理集合的关键抽象概念，它可以指定你希望对集合进行的操作，可以执行非常复杂的查找、过滤和映射数据等操作。 使用Stream API 对集合数据进行操作，就类似于使用 SQL 执行的数据库查询。
  也可以使用 Stream API 来并行执行操作。简言之，Stream API 提供了一种高效且易于使用的处理数据的方式。 

+ 实际开发中，项目中多数数据源都来自于Mysql，Oracle等。但现在数据源可以更多了，有MongDB，Radis等，而这些NoSQL的数据就需要 Java层面去处理。 

+ Stream 和 Collection 集合的区别：Collection 是一种静态的内存数据结构，而 Stream 是有关计算的。前者是主要面向内存，存储在内存中， 后者主要是面向 CPU，通过 CPU 实现计算。

+ **Stream**是数据渠道，用于操作数据源（集合、数组等）所生成的元素序列。 “集合讲的是数据，Stream讲的是计算！”

+ **注意：** 

  ①Stream 自己不会存储元素。 

  ②Stream 不会改变源对象。相反，他们会返回一个持有结果的新Stream。 

  ③Stream 操作是延迟执行的。这意味着他们会等到需要结果的时候才执行。

**Stream** **的操作三个步骤**

+ 1- 创建 Stream
  一个数据源（如：集合、数组），获取一个流
+ 2- 中间操作
  一个中间操作链，对数据源的数据进行处理
+ 3- 终止操作(终端操作)
  一旦执行终止操作，就执行中间操作链，并产生结果。之后，不会再被使用

创建 Stream方式一：通过集合

Java8 中的 Collection 接口被扩展，提供了两个获取流的方法： 

+ **default Stream stream() :** **返回一个顺序流** 

+ **default Stream parallelStream() :** **返回一个并行流**

创建 Stream方式二：通过数组

Java8 中的 Arrays 的静态方法 stream() 可以获取数组流：

+ **static  Stream stream(T[] array):** **返回一个流**

**重载形式，能够处理对应基本类型的数组：**

+ public static IntStream stream(int[] array) 

+ public static LongStream stream(long[] array) 

+ public static DoubleStream stream(double[] array)

创建 Stream方式三：通过Stream的of()

可以调用Stream类静态方法 of(), 通过显示值创建一个流。它可以接收任意数量的参数。

+ **public static Stream of(T... values) :** **返回一个流**

创建 Stream方式四：创建无限流

可以使用静态方法 Stream.iterate() 和 Stream.generate(),  创建无限流。 

+ 迭代
  public static<T> Stream<T> iterate(final T seed, final UnaryOperator<T> f) 
+ 生成
  public static<T> Stream<T> generate(Supplier<T> s)

```java
// 方式四：创建无限流
@Test
public void test4() {
    // 迭代
    // public static<T> Stream<T> iterate(final T seed, final UnaryOperator<T> f)
    Stream<Integer> stream = Stream.iterate(0, x -> x + 2);
    stream.limit(10).forEach(System.out::println);
    // 生成
    // public static<T> Stream<T> generate(Supplier<T> s)
    Stream<Double> stream1 = Stream.generate(Math::random);
    stream1.limit(10).forEach(System.out::println);
}
```

**Stream** **的中间操作**

多个中间操作可以连接起来形成一个流水线，除非流水线上触发终止操作，否则中间操作不会执行任何的处理！而在终止操作时一次性全部处理，称为“惰性求值”。

**1-筛选与切片**

![1683123624922](D:\MyNote\images\1683123624922.png)

**2-映 射**

![1683123693020](D:\MyNote\images\1683123693020.png)

**3-排序**

![1683123740668](D:\MyNote\images\1683123740668.png)

**Stream** **的终止操作** 

终端操作会从流的流水线生成结果。其结果可以是任何不是流的值，例如：List、Integer，甚至是 void。流进行了终止操作后，不能再次使用。 

**1-匹配与查找**

![1683123803365](D:\MyNote\images\1683123803365.png)

![1683123845965](D:\MyNote\images\1683123845965.png)

**2-归约**

![1683123879207](D:\MyNote\images\1683123879207.png)

备注：map 和 reduce 的连接通常称为 map-reduce 模式，因 Google用它来进行网络搜索而出名。

**3-收集**

![1683123945021](D:\MyNote\images\1683123945021.png)

Collector 接口中方法的实现决定了如何对流执行收集的操作(如收集到 List、Set、Map)。 

另外， Collectors 实用类提供了很多静态方法，可以方便地创建常见收集器实例， 具体方法与实例如下表：

![1683124014154](D:\MyNote\images\1683124014154.png)

![1683124054587](D:\MyNote\images\1683124054587.png)

### 13.5.Optional类

+ 到目前为止，臭名昭著的空指针异常是导致Java应用程序失败的最常见原因。以前，为了解决空指针异常，Google公司著名的Guava项目引入了Optional类，Guava通过使用检查空值的方式来防止代码污染，它鼓励程序员写更干净的代码。受到Google Guava的启发，Optional类已经成为Java 8类库的一部分。
+ Optional<T> 类(java.util.Optional) 是一个容器类，它可以保存类型T的值，代表这个值存在。或者仅仅保存null，表示这个值不存在。原来用 null 表示一个值不存在，现在 Optional 可以更好的表达这个概念。并且可以避免空指针异常。
+ Optional类的Javadoc描述如下：这是一个可以为null的容器对象。如果值存在则isPresent()方法会返回true，调用get()方法会返回该对象。



Optional提供很多有用的方法，这样我们就不用显式进行空值检测。

+ 创建Optional类对象的方法：
  + Optional.of(T t) : 创建一个 Optional 实例，t必须非空；
  + Optional.empty() : 创建一个空的 Optional 实例
  + Optional.ofNullable(T t)：t可以为null
+ 判断Optional容器中是否包含对象：
  + boolean isPresent() : 判断是否包含对象
  + void ifPresent(Consumer<? super T> consumer) ：如果有值，就执行Consumer接口的实现代码，并且该值会作为参数传给它。
+ 获取Optional容器的对象：
  + T get(): 如果调用对象包含值，返回该值，否则抛异常
  + T orElse(T other) ：如果有值则将其返回，否则返回指定的other对象。
  + T orElseGet(Supplier<? extends T> other) ：如果有值则将其返回，否则返回由Supplier接口实现提供的对象。
  + T orElseThrow(Supplier<? extends X> exceptionSupplier) ：如果有值则将其返回，否则抛出由Supplier接口实现提供的异常。

```java
@Test
public void test1() {
    Boy b = new Boy("张三");
    Optional<Girl> opt = Optional.ofNullable(b.getGrilFriend());
    // 如果女朋友存在就打印女朋友的信息
    opt.ifPresent(System.out::println);
}
@Test
public void test2() {
    Boy b = new Boy("张三");
    Optional<Girl> opt = Optional.ofNullable(b.getGrilFriend());
    // 如果有女朋友就返回他的女朋友，否则只能欣赏“嫦娥”了
    Girl girl = opt.orElse(new Girl("嫦娥"));
    System.out.println("他的女朋友是：" + girl.getName());
}

@Test
public void test3(){
    Optional<Employee> opt = Optional.of(new Employee("张三", 8888));
    //判断opt中员工对象是否满足条件，如果满足就保留，否则返回空
    Optional<Employee> emp = opt.filter(e -> e.getSalary()>10000);
    System.out.println(emp);
}
@Test
public void test4(){
    Optional<Employee> opt = Optional.of(new Employee("张三", 8888));
    //如果opt中员工对象不为空，就涨薪10%
    Optional<Employee> emp = opt.map(e -> 
                                     {e.setSalary(e.getSalary()%1.1);return e;});
    System.out.println(emp);
}
```



## 14.Java9、10、11新特性

### 14.1.Java 9

+ 经过4次跳票，历经曲折的Java 9 终于终于在2017年9月21日发布。
+ 从Java 9 这个版本开始，Java 的计划发布周期是 6 个月，下一个 Java 的主版本将于 2018 年 3 月发布，命名为 Java 18.3，紧接着再过六个月将发布 Java18.9。
+ 这意味着Java的更新从传统的以特性驱动的发布周期，转变为以时间驱动的（6 个月为周期）发布模式，并逐步的将 Oracle JDK 原商业特性进行开源。
+ 针对企业客户的需求，Oracle 将以三年为周期发布长期支持版本（long term support）。
+ Java 9 提供了超过150项新功能特性，包括备受期待的模块化系统、可交互的 REPL 工具：jshell，JDK 编译工具，Java 公共 API 和私有代码，以及安全增强、扩展提升、性能管理改善等。可以说Java 9是一个庞大的系统工程，完全做了一个整体改变。

Java 9 中有哪些不得不说的新特性

+ 模块化系统 

+ jShell命令 

+ 多版本兼容jar包 

+ 接口的私有方法 

+ 钻石操作符的使用升级 

+ 语法改进：try语句 

+ S tring存储结构变更 

+ 便利的集合特性：of() 

+ 增强的Stream API 

+ 全新的HTTP客户端API 

+ Deprecated的相关API 

+ javadoc的HTML 5支持 

+ Javascript引擎升级：Nashorn 

+ java的动态编译器

官方提供的新特性列表： 

https://docs.oracle.com/javase/9/whatsnew/toc.htm#JSNEW-GUID-C23AFD78-C777-460B-8ACE-58BE5EA681F6 

或参考 Open JDK 

http://openjdk.java.net/projects/jdk9/ 

在线Oracle JDK 9 Documentation 

https://docs.oracle.com/javase/9/

**JDK 8 的目录结构**

![1683124954982](D:\MyNote\images\1683124954982.png)

![1683124976322](D:\MyNote\images\1683124976322.png)

**JDK 9 的目录结构**

![1683125048365](D:\MyNote\images\1683125048365.png)

![1683125089131](D:\MyNote\images\1683125089131.png)

#### 14.1.1.模块化系统

谈到 Java 9 大家往往第一个想到的就是 Jigsaw 项目。众所周知，Java 已经发展超过 20 年（95 年最初发布），Java 和相关生态在不断丰富的同时也越来越暴露出一些问题：

+ Java 运行环境的膨胀和臃肿。每次JVM启动的时候，至少会有30～60MB的内存加载，主要原因是JVM需要加载rt.jar，不管其中的类是否被classloader加载，第一步整个jar都会被JVM加载到内存当中去（而模块化可以根据模块的需要加载程序运行需要的class）
+ 当代码库越来越大，创建复杂，盘根错节的“意大利面条式代码”的几率呈指数级的增长。不同版本的类库交叉依赖导致让人头疼的问题，这些都阻碍了 Java 开发和运行效率的提升。
+ 很难真正地对代码进行封装, 而系统并没有对不同部分（也就是 JAR 文件）之间的依赖关系有个明确的概念。每一个公共类都可以被类路径之下任何其它的公共类所访问到，这样就会导致无意中使用了并不想被公开访问的 API。
+ 本质上讲也就是说，用模块来管理各个package，通过声明某个package暴露，模块(module)的概念，其实就是package外再裹一层，不声明默认就是隐藏。因此，模块化使得代码组织上更安全，因为它可以指定哪些部分可以暴露，哪些部分隐藏。

**实现目标** 

+ 模块化的主要目的在于减少内存的开销 

+ 只须必要模块，而非全部jdk模块，可简化各种类库和大型应用的开发和维护 

+ 改进 Java SE 平台，使其可以适应不同大小的计算设备 

+ 改进其安全性，可维护性，提高性能

模块将由通常的类和新的模块声明文件（module-info.java）组成。该文件是位于 java代码结构的顶层，该模块描述符明确地定义了我们的模块需要什么依赖关系， 以及哪些模块被外部使用。在exports子句中未提及的所有包默认情况下将封装在模块中，不能在外部使用。

![1683468874517](D:\MyNote\images\1683468874517.png)

要想在java9demo模块中调用java9test模块下包中的结构，需要在java9test的module-info.java中声明： 

```java
/**
* @author songhongkang
* @create 2019 下午 11:57
*/
module java9test {
    //package we export
    exports com.atguigui.bean;
}
```

**exports**：控制着哪些包可以被其它模块访问到。所有不被导出的包默认**都被封装在模块里面。**

对应在java 9demo 模块的src 下创建module-info.java文件： 

```java
/**
* @author songhongkang
* @create 2019 下午 11:51
*/
module java9demo {
	requires java9test;
}
```

**requires**：指明对其它模块的依赖。



#### 14.1.2. jShell命令

**产生背景** 

像Python 和 Scala 之类的语言早就有交互式编程环境 REPL (read - evaluate - print - loop)了，以交互式的方式对语句和表达式进行求值。开发者只需要输入一些代码， 就可以在编译前获得对程序的反馈。而之前的Java版本要想执行代码，必须创建文件、声明类、提供测试方法方可实现。 

**设计理念** 

**即写即得、快速运行**

**实现目标** 

+ Java 9 中终于拥有了 REPL工具：jShell。让Java可以像脚本语言一样运行，从控制台启动jShell，利用jShell在没有创建类的情况下直接声明变量，计算表达式， 执行语句。即开发时可以在命令行里直接运行Java的代码，而无需创建Java文件，无需跟人解释”public static void main(String[] args)”这句废话。 

+ jShell也可以从文件中加载语句或者将语句保存到文件中。 

+ jShell也可以是tab键进行自动补全和自动添加分号。

**调出jShell**

<img src="D:\MyNote\images\1683469293996.png" alt="1683469293996" style="zoom:67%;" />

**获取帮助**

<img src="D:\MyNote\images\1683469338290.png" alt="1683469338290" style="zoom:80%;" />

**基本使用**

![1683469383655](D:\MyNote\images\1683469383655.png)

![1683469411815](D:\MyNote\images\1683469411815.png)

**导入指定的包**

![1683469440149](D:\MyNote\images\1683469440149.png)

**默认导入的包**

![1683469470141](D:\MyNote\images\1683469470141.png)

Tips：在JShell环境下，语句末尾的“;”是可选的。但推荐还是最好加上。提高代码可读性。

只需按下Tab键即可自动补全代码

<img src="D:\MyNote\images\1683469545437.png" alt="1683469545437"  />

列出当前session中所有有效的代码片段

![1683469605029](D:\MyNote\images\1683469605029.png)

列出当前session中所有创建过的变量

![1683469643505](D:\MyNote\images\1683469643505.png)

列出当前session中所有创建过的方法

![1683469664938](D:\MyNote\images\1683469664938.png)

使用外部代码编辑器来编写Java代码

![1683469701553](D:\MyNote\images\1683469701553.png)

Tips：我们还可以重新定义相同方法名和参数列表的方法，即为对现有方法的修改（或覆盖）。

使用**/open**命令调用：

![1683469755049](D:\MyNote\images\1683469755049.png)

**没有受检异常（编译时异常）**

![1683469785824](D:\MyNote\images\1683469785824.png)

说明：本来应该强迫我们捕获一个IOException，但却没有出现。因为jShell在后台为我们隐藏了。 

使用exit**退出jShell**

#### 14.1.3.接口的私有方法

Java8中规定接口中的方法除了抽象方法之外，还可以定义静态方法和默认的方法。一定程度上，扩展了接口的功能，此时的接口更像是一个抽象类。

在Java9中，接口更加的灵活和强大，连方法的访问权限修饰符都可以声明为private的了，此时方法将不会成为你对外暴露的API的一部分。

```java
interfaceMyInterface {
    voidnormalInterfaceMethod();
    defaultvoidmethodDefault1() {
        init();
    }
    publicdefaultvoidmethodDefault2() {
        init();
    }
// This method is not part of the public API exposed by MyInterface
    privatevoidinit() {
        System.out.println("默认方法中的通用操作");
    }
}


classMyInterfaceImpl implementsMyInterface {
    @Override
    publicvoidnormalInterfaceMethod() {
        System.out.println("实现接口的方法");
    }
}
publicclassMyInterfaceTest {
    publicstaticvoidmain(String[] args) {
        MyInterfaceImpl impl= newMyInterfaceImpl();impl.methodDefault1();
// impl.init();//不能调用
    }
}
```



#### 14.1.4.钻石操作符使用升级

我们将能够与匿名实现类共同使用钻石操作符（diamondoperator）在Java8 中如下的操作是会报错的：

```java
Comparator<Object> com = new Comparator<>(){
    
    @Override
    public int compare(Object o1, Object o2) {
        return 0;
    }
};

//编译报错信息：Cannotuse“<>”withanonymousinnerclasses.
```



Java 9中如下操作可以正常执行通过：

```java
// anonymous classes can now use type inference 
Comparator<Object> com = new Comparator<>(){
    @Override
    public int compare(Object o1, Object o2) {
        return 0;
    }
};
```



#### 14.1.5.try语句

Java 8 中，可以实现资源的自动关闭，但是要求执行后必须关闭的所有资源必须在try子句中初始化，否则编译不通过。如下例所示： 

```java
try(InputStreamReader reader = new InputStreamReader(System.in)){
    //读取数据细节省略
}catch (IOException e){
    e.printStackTrace();
}
```

Java 9 中，用资源语句编写try将更容易，我们可以在try子句中使用已经初始化过的资源，此时的资源是final的： 

```java
InputStreamReader reader = new InputStreamReader(System.in);
OutputStreamWriter writer = new OutputStreamWriter(System.out);
try (reader; writer) {
    //reader是final的，不可再被赋值
    //reader = null;
    //具体读写操作省略
} catch (IOException e) {
    e.printStackTrace();
}
```



#### 14.1.6.String存储结构变更

**Motivation**

The current implementation of the String class stores characters in a char  array, using two bytes (sixteen bits) for each character. Data gathered from  many different applications indicates that strings are a major component of  heap usage and, moreover, that most String objects contain only Latin-1  characters. Such characters require only one byte of storage, hence half of the  space in the internal char arrays of such String objects is going unused. 

**Description** 

We propose to change the internal representation of the String class from a  UTF-16 char array to a byte array plus an encoding-flag field. The new String  class will store characters encoded either as ISO-8859-1/Latin-1 (one byte per  character), or as UTF-16 (two bytes per character), based upon the contents  of the string. The encoding flag will indicate which encoding is used.

结论：String 再也不用 char[] 来存储啦，改成了 byte[] 加上编码标记，节约了一些空间。 

```java
public final class String
    implements java.io.Serializable, Comparable<String>, CharSequence {
    @Stable
    private final byte[] value;
}
```

那StringBuffer 和 StringBuilder 是否仍无动于衷呢？

String-related classes such as AbstractStringBuilder, StringBuilder,  and StringBuffer will be updated to use the same representation, as will the  HotSpot VM‘s intrinsic(固有的、内置的) string operations.

#### 14.1.7.快速创建只读集合

要创建一个只读、不可改变的集合，必须构造和分配它，然后添加元素，最后包装成一个不可修改的集合。 

```java
List<String> namesList = new ArrayList <>();
namesList.add("Joe");
namesList.add("Bob");
namesList.add("Bill");
namesList = Collections.unmodifiableList(namesList);
System.out.println(namesList);
```

缺点：我们一下写了五行。即：它不能表达为单个表达式。

```java
List<String> list = Collections.unmodifiableList(Arrays.asList("a", "b", "c"));
Set<String> set = Collections.unmodifiableSet(new HashSet<>(Arrays.asList("a", 
                                                                          "b", "c")));
// 如下操作不适用于jdk 8 及之前版本,适用于jdk 9
Map<String, Integer> map = Collections.unmodifiableMap(new HashMap<>() {
    {
        put("a", 1);
        put("b", 2);
        put("c", 3);
    }
});
map.forEach((k, v) -> System.out.println(k + ":" + v));
```

Java 9因此引入了方便的方法，这使得类似的事情更容易表达。

![1683471197867](D:\MyNote\images\1683471197867.png)

List firsnamesList = List.of(“Joe”,”Bob”,”Bill”); 

调用集合中静态方法of()，可以将不同数量的参数传输到此工厂方法中。此功能可用于Set和List，也可用于Map的类似形式。此时得到的集合，是不可变的：在创建后，继续添加元素到这些集合会导致 “UnsupportedOperationException” 。由于Java 8中接口方法的实现，可以直接在List，Set和Map的接口内定义这些方法， 便于调用。 

```java
List<String> list = List.of("a", "b", "c");
Set<String> set = Set.of("a", "b", "c");
Map<String, Integer> map1 = Map.of("Tom", 12, "Jerry", 21, "Lilei", 33, "HanMeimei", 18);
Map<String, Integer> map2 = Map.ofEntries(Map.entry("Tom", 89), 
Map.entry("Jim", 78), Map.entry("Tim", 98));
```

#### 14.1.8.InputStream 加强

InputStream 终于有了一个非常有用的方法：transferTo，可以用来将数据直接传输到 OutputStream，这是在处理原始数据流时非常常见的一种用法，如下示例。

```java
ClassLoader cl = this.getClass().getClassLoader();
try (InputStream is = cl.getResourceAsStream("hello.txt");
     OutputStream os = new FileOutputStream("src\\hello1.txt")) {
    is.transferTo(os); // 把输入流中的所有数据直接自动地复制到输出流中
} catch (IOException e) {
    e.printStackTrace();
}
```

#### 14.1.9.增强的 Stream API

​		Java 的 Steam API 是java标准库最好的改进之一，让开发者能够快速运算，从而能够有效的利用数据并行计算。Java 8 提供的 Steam 能够利用多核架构实现声明式的数据处理。
​		在 Java 9 中，Stream API 变得更好，Stream 接口中添加了 4 个新的方法：takeWhile, dropWhile, ofNullable，还有个 iterate 方法的新重载方法，可以让你提供一个 Predicate (判断条件)来指定什么时候结束迭代。
​		除了对 Stream 本身的扩展，Optional 和 Stream 之间的结合也得到了改进。现在可以通过 Optional 的新方法 stream() 将一个 Optional 对象转换为一个(可能是空的) Stream 对象。

**takeWhile()**

用于从 Stream 中获取一部分数据，接收一个 Predicate 来进行选择。在有序的Stream 中，takeWhile 返回从开头开始的尽量多的元素。 

```java
List<Integer> list = Arrays.asList(45, 43, 76, 87, 42, 77, 90, 73, 67, 88);
list.stream().takeWhile(x -> x < 50).forEach(System.out::println);
System.out.println();
list = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8);
list.stream().takeWhile(x -> x < 5).forEach(System.out::println);
```

**dropWhile()**

dropWhile 的行为与 takeWhile 相反，返回剩余的元素。 

```java
List<Integer> list = Arrays.asList(45, 43, 76, 87, 42, 77, 90, 73, 67, 88);
list.stream().dropWhile(x -> x < 50).forEach(System.out::println);
System.out.println();
list = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8);
list.stream().dropWhile(x -> x < 5).forEach(System.out::println);
```

**ofNullable()**

Java 8 中 Stream 不能完全为null，否则会报空指针异常。而 Java 9 中的 ofNullable 方法允许我们创建一个单元素 Stream，可以包含一个非空元素，也可以创建一个空Stream

```java
// 报NullPointerException
// Stream<Object> stream1 = Stream.of(null);
// System.out.println(stream1.count());
// 不报异常，允许通过
Stream<String> stringStream = Stream.of("AA", "BB", null);
System.out.println(stringStream.count());// 3
// 不报异常，允许通过
List<String> list = new ArrayList<>();
list.add("AA");
list.add(null);
System.out.println(list.stream().count());// 2
// ofNullable()：允许值为null
Stream<Object> stream1 = Stream.ofNullable(null);
System.out.println(stream1.count());// 0
Stream<String> stream = Stream.ofNullable("hello world");
System.out.println(stream.count());// 1
```

**iterate()**

这个 iterate 方法的新重载方法，可以让你提供一个 Predicate (判断条件)来指定什么时候结束迭代

```java
// 原来的控制终止方式：
Stream.iterate(1, i -> i + 1).limit(10).forEach(System.out::println);
// 现在的终止方式：
Stream.iterate(1, i -> i < 100, i -> i + 1).forEach(System.out::println);
```



#### 14.1.10.Optional获取Stream的方法

Optional类中stream()的使用

```java
List<String> list = new ArrayList<>();
list.add("Tom");
list.add("Jerry");
list.add("Tim");
Optional<List<String>> optional = Optional.ofNullable(list);
Stream<List<String>> stream = optional.stream();
stream.flatMap(x -> x.stream()).forEach(System.out::println);
```



#### 14.1.11.Nashorn

​		Nashorn 项目在 JDK 9 中得到改进，它为 Java 提供轻量级的 Javascript 运行时。 Nashorn 项目跟随 Netscape 的 Rhino 项目，目的是为了在 Java 中实现一个高性能但轻量级的 Javascript 运行时。Nashorn 项目使得 Java 应用能够嵌入 Javascript。它在 JDK 8 中为 Java 提供一个 Javascript 引擎。 

​		JDK 9 包含一个用来解析 Nashorn 的 ECMAScript 语法树的 API。这个 API 使得 IDE 和服务端框架不需要依赖 Nashorn 项目的内部实现类，就能够分析ECMAScript 代码。

<img src="D:\MyNote\images\1683555420403.png" alt="1683555420403" style="zoom:67%;" />

### 14.2.Java10

 		2018年3月21日，Oracle官方宣布Java10正式发布。需要注意的是 Java 9 和 Java 10 都不是 LTS (Long-Term-Support) 版本。和过去的 Java 大版本升级不同，这两个只有半年左右的开发和维护期。而未来的 Java 11，也就是 18.9 LTS，才是 Java 8 之后第一个 LTS 版本。JDK10一共定义了109个新特性，其中包含12个JEP（对于程序员来讲，真正的新特性其实就一个），还有一些新API和JVM规范以及JAVA语言规范上的改动。

JDK10的12个JEP（JDK Enhancement Proposal特性加强提议）参阅官方文档：http://openjdk.java.net/projects/jdk/10/

```java
286: Local-Variable Type Inference 局部变量类型推断
296: Consolidate the JDK Forest into a Single Repository JDK库的合并
304: Garbage-Collector Interface 统一的垃圾回收接口
307: Parallel Full GC for G1 为G1提供并行的Full GC
310: Application Class-Data Sharing 应用程序类数据（AppCDS）共享
312: Thread-Local Handshakes ThreadLocal握手交互
313: Remove the Native-Header Generation Tool (javah) 移除JDK中附带的javah工具
314: Additional Unicode Language-Tag Extensions 使用附加的Unicode语言标记扩展
316: Heap Allocation on Alternative Memory Devices 能将堆内存占用分配给用户指定
的备用内存设备
317: Experimental Java-Based JIT Compiler 使用基于Java的JIT编译器
319: Root Certificates 根证书
322: Time-Based Release Versioning 基于时间的发布版本
```

**一、局部变量类型推断** 

+ 产生背景
  开发者经常抱怨Java中引用代码的程度。局部变量的显示类型声明，常常被认为是不必须的，给一个好听的名字经常可以很清楚的表达出下面应该怎样继续。

+ 好处：
  减少了啰嗦和形式的代码，避免了信息冗余，而且对齐了变量名，更容易阅读！

  举例如下：

  + 场景一：类实例化时
    作为 Java开发者，在声明一个变量时，我们总是习惯了敲打两次变量类型，第一次用于声明变量类型，第二次用于构造器。
    `LinkedHashSet<Integer> set = new LinkedHashSet<>();`

  + 场景二：返回值类型含复杂泛型结构
    变量的声明类型书写复杂且较长，尤其是加上泛型的使用
    `Iterator<Map.Entry<Integer, Student>> iterator = set.iterator();`

  + 场景三：

    我们也经常声明一种变量，它只会被使用一次，而且是用在下一行代码中， 比如： 

```java
URL url = new URL("http://www.atguigu.com"); 
URLConnection connection = url.openConnection(); 
Reader reader = new BufferedReader(new InputStreamReader(connection.getInputStream())); 
```



尽管 IDE可以帮我们自动完成这些代码，但当变量总是跳来跳去的时候，可读性还是会受到影响，因为变量类型的名称由各种不同长度的字符组成。而且， 有时候开发人员会尽力避免声明中间变量，因为太多的类型声明只会分散注意力，不会带来额外的好处。

**适用于以下情况：** 

```java
//1.局部变量的初始化
var list = new ArrayList<>();
//2.增强for循环中的索引
for(var v : list) {
	System.out.println(v);
}
//3.传统for循环中
for(var i = 0;i < 100;i++) {
	System.out.println(i);
}
```

**在局部变量中使用时，如下情况不适用：** 

初始值为null 

![1683558533845](D:\MyNote\images\1683558533845.png)

方法引用

![1683558550413](D:\MyNote\images\1683558550413.png)

Lambda表达式

![1683558569066](D:\MyNote\images\1683558569066.png)

为数组静态初始化 

![1683558585185](D:\MyNote\images\1683558585185.png)

**不适用以下的结构中：** 

+ 情况1：没有初始化的局部变量声明 

+ 情况2：方法的返回类型 

+ 情况3：方法的参数类型 

+ 情况4：构造器的参数类型 

+ 情况5：属性 

+ 情况6：catch块

**工作原理**

在处理 var时，编译器先是查看表达式右边部分，并根据右边变量值的类型进行推断，作为左边变量的类型，然后将该类型写入字节码当中。

**注 意**：

1. var不是一个关键字

   你不需要担心变量名或方法名会与 var发生冲突，因为 var实际上并不是一个关键字，而是一个类型名，只有在编译器需要知道类型的地方才需要用到它。除此之外，它就是一个普通合法的标识符。也就是说，除了不能用它作为类名，其他的都可以，但极少人会用它作为类名。

2. 这不是JavaScript

   首先我要说明的是，var并不会改变Java是一门静态类型语言的事实。编译器负责推断出类型，并把结果写入字节码文件，就好像是开发人员自己敲入类型一样。下面是使用 IntelliJ（实际上是 Fernflower的反编译器）反编译器反编译出的代码：

```java
var url = new URL("http://www.atguigu.com");
var connection = url.openConnection();
var reader = new BufferedReader(new InputStreamReader(connection.getInputStream()));

反编译后
URL url = new URL("http://www.atguigu.com");
URLConnection connection = url.openConnection();
BufferedReader reader = new BufferedReader(
new InputStreamReader(connection.getInputStream()));

```

从代码来看，就好像之前已经声明了这些类型一样。事实上，这一特性只发生在编译阶段，与运行时无关，所以对运行时的性能不会产生任何影响。所以请放心，这不是 JavaScript。

**二、集合新增创建不可变集合的方法**

自 Java 9 开始，Jdk 里面为集合（List / Set / Map）都添加了 of (jdk9新增)和 copyOf (jdk10新增)方法，它们两个都用来创建不可变的集合，来看下它们的使用和区别。

```java
//示例1：
var list1 = List.of("Java", "Python", "C");
var copy1 = List.copyOf(list1);
System.out.println(list1 == copy1); // true
//示例2：
var list2 = new ArrayList<String>();
var copy2 = List.copyOf(list2);
System.out.println(list2 == copy2); // false
//示例1和2代码基本一致，为什么一个为true,一个为false?
```

​		从 源 码 分 析 ， 可 以 看 出 copyOf 方 法 会 先 判 断 来 源 集 合 是 不 是 AbstractImmutableList 类型的，如果是，就直接返回，如果不是，则调用 of 创 建一个新的集合。 示例2因为用的 new 创建的集合，不属于不可变 AbstractImmutableList 类的子类， 所以 copyOf 方法又创建了一个新的实例，所以为false。 

**注意**：使用of和copyOf创建的集合为不可变集合，不能进行添加、删除、替换、 排序等操作，不然会报 java.lang.UnsupportedOperationException 异常。 上面演示了 List 的 of 和 copyOf 方法，Set 和 Map 接口都有。 

### 14.3.Java11

北京时间 2018年9 月 26 日，Oracle 官方宣布 Java 11 正式发布。这是 Java 大版本周期变化后的第一个长期支持版本，非常值得关注。从官网即可下载,最新发布的 Java11 将带来 ZGC、Http Client 等重要特性，一共包含 17 个 JEP（JDK Enhancement Proposals，JDK 增强提案）。其实，总共更新不止17个，只是我们更关注如下的17个JEP更新。

![1683559271506](D:\MyNote\images\1683559271506.png)

**JDK 11** **将是一个 企业不可忽视的版本。**从时间节点来看，JDK 11 的发布正好处在 JDK 8 免费更新到期的前夕，同时 JDK 9、10 也陆续成为**“历史版本”** ，下面是 Oracle JDK 支持路线图：







## 其他

### 1.加载配置文件的方法

#### 1.1.Properties

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



##### 7.1.2.ResourceBundle

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

##### a.string

##### 1.indexOf()

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

#####  2.subString()

 1.通过subString()方法来进行字符串截取。 
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



