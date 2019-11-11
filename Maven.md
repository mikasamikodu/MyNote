# 9.Maven

## 9.1. Maven的介绍

maven是一款服务于java平台的自动化构建工具

## 9.2.Maven的安装与配置

1.在官网下载Maven，然后解压；

2.配置环境变量。配置M2_HOME或MAVEN_HOME，值为bin目前的路径，然后在Path变量中加入

值%M2_HOME%\bin；

3.测试是否环境变量配置成功，在命令行写入命令`mvn -v` 即可完成测试；

## 9.3.创建Maven工程

### 9.3.1.创建约定的目录结构

+ 根目录：工程名
+ src目录：源码
+ pom.xml文件：Maven工程的核心配置文件
+ main目录：存放主程序
+ test目录：存放测试程序
+ java目录：存放java源文件
+ resourses目录：存放框架或其他工具的配置文件

目录结构：

Hello

​	|---src

​	|---|---main

​	|---|---|---java

​	|---|---|---resourses

​	|---|---test

​	|---|---|---java

​	|---|---|---resourses

​	|---pom.xml

pom.xml内容

```xml
<?xml version="1.0" ?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
   xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                       http://maven.apache.org/xsd/maven-4.0.0.xsd">  
    <modelVersion>4.0.0</modelVersion>  
    <groupId>com.atgui.maven</groupId>  
    <artifactId>Hello</artifactId>  
    <version>0.0.1-SNAPSHOT</version>  
    <name>Hello</name>
    <dependencies>  
        <dependency>  
            <groupId>junit</groupId>  
            <artifactId>junit</artifactId>  
            <version>4.0</version>  
            <scope>test</scope>
        </dependency> 
    </dependencies>  
</project>
```



## 9.4.Maven常用命令

- 注意：执行与构建过程相关的Maven命令，必须进入pom.xml所在目录。                                                       （与构建过程相关的：编译，打包，测试）
- 常用命令：
  - mvn clean:清理
  - mvn compile:编译主程序
  - mvn test-compile:编译测试程序
  - mvn test:执行测试
  - mvn package:打包
  - mvn install:安装
  - mvn site:生成站点

## 9.5.Maven仓库

1.开始编译时，Maven核心程序如果在 本地仓库找不到需要的插件，则会自动连接外网，到中央仓库去下载。如果连接失败，则构建失败。可以通过修改本地仓库位置让Maven核心程序在我们事先准备好的的目录下查找插件；

2.修改本地仓库位置步骤：

​	a.找到Maven解压目录\conf\settings.xml;

​	b.在settings.xml中找到localRepository标签；

​	c.将标签从注释中取出，并将内容替换为自己准备好的本地仓库位置，例如：

```xml
<localRepository>D:\Maven</localRepository>
```

3.仓库分类

- 本地仓库：当前电脑上部署的仓库目录，为当前电脑删给所有的maven工程服务；
- 远程仓库：
  - 私服：搭建在局域网的环境中，为局域网范围的maven工程服务；
  - 中央仓库：架设在internet上，为全世界的的maven工程服务；
  - 中央仓库镜像：为分担中央仓库流量，提升用户访问速度而在世界各地搭建的仓库；

4.仓库内容：maven工程

- maven自身需要的插件；
- 第三方框架或工具的jar包；
- 自己开发的maven工程；

## 9.6.Maven的核心概念

### 9.6.1.坐标

maven可以使用三个指定坐标唯一定位一个maven工程

- groupid:公司或组织域名倒序+项目名

  ```xml
  <groupId>com.atguigu.maven</groupId>
  ```

- artifactid:模块名

  ```xml
  <artifactId>Hello</artifactId>
  ```

  

- version:版本号

  ```xml
  <version>1.0.0</version>
  ```

maven工程坐标与本地仓库中路径的关系

```xml
<groupId>com.atguigu.maven</groupId>
<artifactId>Hello</artifactId>
<version>1.0.0</version>
```

这个工程在maven仓库路径下/com/atguigu/maven/Hello-1.0.0/Hello-1.0.0.jar

### 9.6.2.依赖管理

1.maven解析依赖信息时会到本地仓库中查找被依赖的jar包

对于自己的maven工程可以使用mvn install命令安装后就可以进入仓库

2.依赖范围scope

compile对主程序有效，对测试程序有效，参与打包

test对主程序无效，对测试程序有效，不参与打包。例如junit

provided对主程序有效，对测试程序有效，不参与打包，不参与部署，例如servlet-api.jar

3.依赖具有传递性

在一个工程里加入Jar包的依赖，所有引用或依赖这个的工程的工程就都有这个依赖了（仅限于scope为compile的），如果某个工程不需要这个依赖，则可以在这个jar包所在依赖里配置如下：

```xml
<exclusions>
	<exclusion>
    	<groupId></groupId>
        <artifactId></artifactId>
    </exclusion>
</exclusions>
```



4.依赖的冲突

情景1：当同一jar包因为依赖的关系有不同版本出现时，maven会采用就近原则，采用路径最短的方式。

a工程中有logging-1.1的依赖，b工程依赖了a工程，而b工程使用的是logging-1.2的依赖，c工程依赖了b工程，此时c工程里有2个版本的logging的依赖，c->b->logging-1.2是2步，c->b->c->logging-1.1是3步，因此采用b工程的jar包。

情景2：在情景1中当路径相同时，采取声明优先原则，采用dependency先声明的。

5.依赖的版本号管理

举例：当依赖spring的多个jar包依赖需要统一升级版本号时，只需在project标签内使用properties标签，并在内部使用自定义标签定义spring同一的版本号，然后在spring的各个依赖的版本号位置version标签内使用`${自定义标签}` 即可统一管理版本号了。

### 9.6.3.生命周期

1. maven各个构建关节不能打乱，必须按照既定的正确顺序来执行；
2. maven的核心程序中定义了抽象的生命周期，生命周期的各个阶段都由插件完成；
3. maven每次自动化构建都会从生命周期的最初的位置开始执行；

### 9.6.4.继承

原因：由于test范围的依赖不能传递，所以必然分散在各个工程模块中，会出现版本不一致，因此需要同一这个依赖的版本；

解决：将这个依赖统一提取到“父工程”中，在子工程中声明这个依赖时不指定依赖版本号，以父工程统一指定为准，便于修改；

操作方法：

1.创建一个maven工程作为父工程，打包方式是pom；

父工程建立后的pom.xml 内容：

```xml
<modelVersion>4.0.0</modelVersion>
<groupId>com.atguigu.maven</groupId>
<artifactId>Parent</artifactId>
<version>0.0.1-SNAPSHOT</version>
<packaging>pom</packaging>
```



2.在子工程中声明对父工程的声明；

对子工程 pom.xml的修改

```xml
<parent>
    <groupId>com.atguigu.maven</groupId>
    <artifactId>Parent</artifactId>
    <version>0.0.1-SNAPSHOT</version>

    <!-- 指定父工程的pom文件 -->
    <relativePath>../Parent/pom.xml</relativePath>
</parent>
```



3.将子工程中的坐标与父工程坐标中重复的内容删除；

对子工程 pom.xml的修改

```xml
<artifactId>Hello</artifactId> 
<!--
删除子工程中
	<groupId>com.atguigu.maven</groupId
    <version>0.0.1-SNAPSHOT</version>
-->
```



4.在父工程统一管理这个依赖；

父工程的修改：

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>junit</groupId>  
            <artifactId>junit</artifactId>  
            <version>4.0</version>  
            <scope>test</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```



5.在子工程中删除这个依赖的版本号部分；

删除子工程中关于版本号部分：

```xml
<dependencies>  
    <dependency>  
        <groupId>junit</groupId>  
        <artifactId>junit</artifactId>  
        <scope>test</scope>
    </dependency> 
</dependencies>  
```

### 9.6.5.聚合

作用：一键安装各个模块工程

 配置方式：在一个”总的聚合工程“中配置各个参与聚合的模块

```xml
<modules>
    <module>../Hello</module>
</modules>
```

模块无先后顺序，maven可识别其依赖顺序

使用方式：在聚合工程的pom.xml右键—》run as->maven install

## 9.7.eclipse中的maven

因为maven在eclipse中已经内置，所以只需要进行一下设置即可在eclipse中使用maven。

1.installations:点击右上角添加，选择自己安装的maven路径

![1563779490646](D:\MyNote\images\1563779490646.png)

2.user settings:修改相关路径，更换为自己安装的maven的settings.xml中位置，目的是更换本地仓库位置

![1563779836316](D:\MyNote\images\1563779836316.png)



技巧：

加快打包速度或工程创建速度方法，将maven的镜像修改为阿里的镜像。修改maven的setting.xml文件。内容：

```xml
<mirrors>
    <mirror>
        <id>alimaven</id>
        <name>aliyun maven</name>
        <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
        <mirrorOf>central</mirrorOf>        
    </mirror>
</mirrors>
```

