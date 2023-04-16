# 一、搭建python环境

### 1.安装python解释器

https://www.python.org/   python官网

https://www.python.org/downloads/release/python-394/  下载链接

![1623937151677](F:\MyNote\images\1623937151677.png)

安装好之后可在开发程序找到python的文件夹，下面有四个文件：

![1623937575619](F:\MyNote\images\1623937575619.png)

分别是python自带的简单开发环境、交互式命令行、python的官方文档、python自带模块的说明文档

### 2.安装开发工具pycharm

Charm 在 Windows下是如何安装的。

这是 PyCharm 的下载地址：http://www.jetbrains.com/pycharm/download/#section=windows

进入该网站后，我们会看到如下界面:

![img](F:\MyNote\images\1525863037-6053-.png)

professional 表示专业版，community 是社区版，推荐安装社区版，因为是免费使用的。

1、当下载好以后，点击安装，记得修改安装路径，我这里放的是E盘，修改好以后，Next

![img](F:\MyNote\images\1525863037-5461-.png)

2、接下来是

![img](F:\MyNote\images\1525863037-4708-.png)

我们可以根据自己的电脑选择32位还是64位，目前应该基本都是64位系统吧

3、如下

![img](F:\MyNote\images\1525863038-8628-.png)

点击Install,然后就是静静的等待安装了。如果我们之前没有下载有Python解释器的话，在等待安装的时间我们得去下载python解释器，不然pycharm只是一副没有灵魂的驱壳

4、进入python官方网站：//www.python.org/

![img](F:\MyNote\images\1525863038-3244-.png)

点击Downloads,进入选择下载界面

5、如下所示，选择我们需要的python版本号，点击Download

![img](F:\MyNote\images\1525863038-6239-.png)

6、我选择的是python3.5.1，会看到如下界面

![img](F:\MyNote\images\1525863038-6907-.png)

因为我们需要用到的是Windows下的解释器，所以在Operating System中可以选择对应的Windows版本，有64位和32位可以选择，我选择的是画红线的这个，executable表示可执行版，需要安装后使用，embeddable表示嵌入版，就是解压以后就可以使用的版本。

可执行版安装比较简单，一直默认就好了。embeddable需要注意，当我们解压![img](F:\MyNote\images\1525863038-5228-.png)这个也是需要解压到同一路径的，这里面放着pip、setuptools等工具，如果不解压，我们将无法在pycharm中更新模块，比如需要用到pymysql，就无法下载。虽然也能用，但是就是"阉割版"的python解释器了。

如果是embeddable版，记得把解释器所在的路径添加到环境变量里，不然pycharm无法自动获得解释器位置。

7、添加环境变量

（1）右键我的电脑，点击属性，弹出如下界面

![img](F:\MyNote\images\1525863038-5928-.png)

（2）点击高级系统设置，出现下图

![img](F:\MyNote\images\1525863038-9558-.png)

（3）点击环境变量

![img](F:\MyNote\images\1525863038-3430-.png)

（4）找到系统变量里面的Path，编辑它，将python解释器所在路径粘贴到最后面，再加个分号。

![img](F:\MyNote\images\1525863038-1728-.png)

环境变量配置结束

8、这时候Pycharm也装好了，我们进入该软件。

![img](F:\MyNote\images\1525863039-3010-.png)

9、点击Create New Project，接下来是重点

![img](F:\MyNote\images\1525863039-3037-.png)

Location是我们存放工程的路径，点击![img](F:\MyNote\images\1525863039-5575-.png)这个三角符号，可以看到pycharm已经自动获取了Python 3.5。

![img](F:\MyNote\images\1525863039-5312-.png)

点击第一个![img](F:\MyNote\images\1525863039-7886-.png)我们可以选择Location的路径，比如

![img](F:\MyNote\images\1525863039-8791-.png)

记住，我们选择的路径需要为空，不然无法创建，第二个Location不用动它，是自动默认的，其余不用点，然后点击Create。出现如下界面，这是Pycharm在配置环境，静静等待。最后点击close关掉提示就好了。

![img](F:\MyNote\images\1525863039-9510-.png)

10、建立编译环境

![img](F:\MyNote\images\1525863039-4822-.png)

右键![img](F:\MyNote\images\1525863039-5988-.png)点击New,选择Python File

![img](F:\MyNote\images\1525863039-8465-.png)

给file取个名字，点击OK

![img](F:\MyNote\images\1525863040-3009-.png)

系统会默认生成hello.py

![img](F:\MyNote\images\1525863040-6888-.png)

好了，至此，我们的初始工作基本完成。

11、我们来编译一下

![img](F:\MyNote\images\1525863040-9146-.png)

快捷键ctrl+shift+F10或者点击![img](F:\MyNote\images\1525863038-3561-.png)绿色三角形,就会编译，编译结果如下

![img](F:\MyNote\images\1525863040-6355-.png)

12、对了，因为我之前已经添加过了，所以可以直接编译，还有很重要的一步没说，不然pycharm无法找到解释器，将无法编译。

点击File,选择settings,点击![img](F:\MyNote\images\1525863040-8642-.png)

添加解释器

![img](F:\MyNote\images\1525863040-9577-.png)

最后点击Apply。等待系统配置。

如果我们需要添加新的模块，点击绿色+号

![img](F:\MyNote\images\1525863040-7805-.png)

然后直接搜索pymysql

![img](F:\MyNote\images\1525863040-2458-.png)

然后点安装

![img](F:\MyNote\images\1525863040-5220-.png)

以上就是pycharm的安装过程以及初始化，还有Python解释器的安装配置。

### 3.设置代码模板

File>>Settings>>Editor>>File and Code Templates,然后在右侧找到python script，就可以在右侧对应位置编写属于自己的代码模板

![1623938907520](F:\MyNote\images\1623938907520.png)



### 4、小提示

注释：`#111`，#号后面内容都是注释，不计入代码

三引号''' ''' 中的内容可以视为多行注释

可以在文件开头注明文件编码格式：

```python
#coding:utf-8
```



# 二、基础内容

### 1.输出函数print(520)

结果是输出520

内容可以是数字、字符串、含有运算符的表达式

例：`print(520)`、`print('hello world!')`、`print(1+3)`

### 2.输出到文件中

```python
fp=open('d:/111.txt','a+')#a+表示d:/111.txt如果没有就创建,存在就在后面追加内容
print(512,file=fp)#将打印的结果输出到d:/111.txt
fp.close()
```



### 3.转义字符

就是反斜杠+想要实现的转义功能字母（反斜杠\\）

例：`print('hello\nworld')`、`print('hello\tworld')`

原子符：不希望字符串内转义字符起作用，只需要在字符串前加一个r或R,但是字符串最后不可用出现单反斜杠

例：`print(r'hello\nworld')`、`print(R'hello\nworld')`

反例：``print(r'hello\nworld\')``

### 4.标识符与保留字

+ 变量、函数、类、模块和其他对象起的名字就是标识符
+ 规则：
  + 标识符由字母、数字、下划线组成
  + 不能以数字开头
  + 严格区分大小写
  + 不能有下列保留字

```python
['False', 'None', 'True', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
```



### 5.变量的定义与使用

a.变量就是内存中带有标签的盒子，作用是存储特定数据

例：`name = '玛丽亚'`

b.变量由三部分组成：

+ 标识：表示对象所存储的内存地址，使用内置函数id(obj)获取
+ 类型：表示的是对象的数据类型，使用内置函数type(obj)获取
+ 值：表示对象所存储的具体数据，使用print(obj)将值打印

name='玛丽亚'

name:89834234

type:str

value:'玛丽亚'

c.变量在多次赋值后，变量名会指向新的内存空间

```python
name='玛丽亚'
print('id:', id(name), '    type:', type(name), '   值:', name)
#结果：id: 24025760     type: <class 'str'>    值: 玛丽亚
name='王碧云'
print('id:', id(name), '    type:', type(name), '   值:', name)
#结果：id: 24247728     type: <class 'str'>    值: 王碧云
```



### 6.数据类型

常用数据类型：

+ 整数类型	->int	->例：98
+ 浮点数类型	->float    ->例：98.0
+ 布尔类型    ->bool    ->True,False
+ 字符串类型    ->str    ->例：'python'    

#### 6.1.整数类型

可以表示正数、负数和零
整数不同进制的表示方式

+ 十进制： 默认的进制
+ 二进制：以0b开头
+ 八进制：以0o开头
+ 十六进制：以0x开头

| 进制     | 基本数                                    | 逢几进一 | 表示形式  |
| -------- | ----------------------------------------- | -------- | --------- |
| 十进制   | 0，1，2，3，4，5，6，7，8，9              | 10       | 110       |
| 二进制   | 0，1                                      | 2        | 0b1110110 |
| 八进制   | 0，1，2，3，4，5，6，7                    | 8        | 0o144     |
| 十六进制 | 0，1，2，3，4，5，6，7，8，9，A,B,C,D,E,F | 16       | 0x65      |



#### 6.2.浮点数类型

浮点数类型由整数部分和小数部分组成
浮点数存储存在不精确性，因为使用浮点数计算时可能会出现小数位数不确定的情况‘

```python
print(1.1+2.2)#3.3000000000000003
print(1.1+2.1)#3.2
```



解决办法是导入模块Decimal

```python
from decimal import Decimal
print(Decimal('1.1')+Decimal('2.2'))
```



#### 6.3.布尔类型

用来表示真或假的值，True为真，False为假。而且布尔值可以转化为整数，True=1，False=0

以下对象的布尔值都是False:False,数值0,None,空字符串，空列表，空字典，空元组，空集合

例：

```python
print(bool(''))#False
print(bool(None))#False
print(bool([]))#False，空列表
print(bool(list()))#False，空列表
print(bool(()))#False，空元组
print(bool(tuple()))#False，空元组
print(bool({}))#False，空字典
print(bool(dict{}))#False，空字典
print(bool(set()))#False，空集合
```



#### 6.4.字符串类型

字符串类型又被称为不可变的字符序列

可以使用单引号' '、双引号" "、三引号''' '''或""" """来定义

单引号和双引号的字符串必须在一行

三引号的字符串可以在连续的多行

例：

```python
str='hello world'
str="hello world"
str='''hello world'''
str='''hello 
	   world'''
```



### 7.数据类型转换

目的是将不同的数据类型拼接在一起

| 函数名  | 作用                           | 注意事项                                                     | 举例                       |
| ------- | :----------------------------- | ------------------------------------------------------------ | -------------------------- |
| str()   | 将其他数据类型转换为字符串类型 | 也可以用引号转换                                             | str(123)<br />'123'        |
| int()   | 将其他数据类型转换为数字类型   | 1.文字类和小数类字符串无法转换为整数<br />2.浮点类转换为整数，会去除小数点后数字 | int('123')<br />int(12.1)  |
| float() | 将其他数据类型转换为浮点数类型 | 1.文字类无法转换为整数<br />2.整数转换为浮点数，小数点后面以0结尾 | float('9.1')<br />float(8) |



### 8.输入函数input(obj)

作用：接收用户的输入

返回值：字符串类型

接收方式：用=的形式将接受结果放入变量

参数：用户输入时的提示语

```python
name=input('你的名字是：\n')
print(name)
#在控制台输入'张三'，按回车返回'张三'
```



### 9.运算符

标准运算符

加+、减-、乘*、除/、整除//

取余运算符%

幂运算符**

赋值运算符=：支持链式赋值(a=b=c=10，a、b、c的地址相等)，
支持系列解包赋值(a,b,c=10,20,30等同于a=10  b=20  c=30)

比较运算符：正常的>,<,>=,<=,==,!=都是用来比较对象的值

is,is not是用来比较对象的id

例：

```python
a=10
b=10
print(a==b)#True，a、b值相等
print(a is b)#True，a、b的id相等
```



布尔运算符：有and,or,not,in,not in

```python
print(10 and 10)#True
print(10 and 0)#False
print(10 or 0)#True
print(0 or 0)#False
print(not False)#True
print(not True)#False
print(1 in [1,2,3])#True
print(1 not in [1,2,3])#False
print('w' in 'hellow')#True
print('w' not in 'hellow')#False
```



位运算符：按位与&,按位或|,左移运算符<<,右移运算符>>，计算时需先将数据转换为二进制再计算

按位与&：对应位数都是1，结果数位才是1，否则是0

按位或|：对应位数都是0，结果数位才是0，否则是1

左移运算符<<：高位移除舍弃，低位补0，即结果乘以2

右移运算符>>：低位移除舍弃，高位补0，即结果除以2

例：

```python
print(4&8)#0
print(4|8)#12
print(4<<1)#8
print(4<<2)#16
print(4>>1)#2
```



10.分支结构-判断结构

```python
grade=int(input('请输入成绩：'))
if grade<60:
    print('成绩评定不合格')
elif grade<80:#判断条件可以写成60<=grade<80
    print('成绩评定良')
else:
    print('成绩评定优')
    
    
grade=int(input('请输入成绩：'))
if grade<60:
    print('成绩评定不合格')
	if grade<70:
    	print('成绩评定A')
     else:
        print('成绩评定B')
else:
    print('成绩评定优')
```

