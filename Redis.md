# 1.Redis相关信息

## 1.1. **简介** 

 		Redis 是完全开源免费的，遵守BSD协议，是一个高性能(NOSQL)的key-value数据库,Redis是一个开源的使用ANSI [C语言](https://baike.baidu.com/item/C语言)编写、支持网络、可基于内存亦可持久化的日志型、Key-Value[数据库](https://baike.baidu.com/item/数据库)，并提供多种语言的API。 

### 1.1.1.BSD

[BSD](https://baike.baidu.com/item/BSD)是"Berkeley Software Distribution"的缩写，意思是"伯克利软件发行版"。

​		BSD开源协议是一个给于使用者很大自由的协议。可以自由的使用，修改源代码，也可以将修改后的代码作为开源或者专有软件再发布。BSD代码鼓励代码共享，但需要尊重代码作者的著作权。BSD由于允许使用者修改和重新发布代码，也允许使用或在BSD代码上开发商业软件发布和销售，因此是对商业集成很友好的协议。

Redis作者github地址： http://github.com/antirez 

### 1.1.2. **NoSQL介绍** 

 NoSQL，泛指非关系型的数据库。随着互联网web2.0网站的兴起，传统的关系数据库在应付web2.0网站，特别是超大规模和高并发的SNS类型的web2.0纯动态网站已经显得力不从心，暴露了很多难以克服的问题，而非关系型的数据库则由于其本身的特点得到了非常迅速的发展。**NoSQL数据库的产生就是为了解决大规模数据集合多重数据种类带来的挑战，尤其是大数据应用难题**。  

#### 1.1.2.1.NoSQL四大类

1.键值(**[*Key-Value*](https://baike.baidu.com/item/Key-Value)**)存储数据库
		这一类数据库主要会使用到一个哈希表，这个表中有一个特定的键和一个指针指向特定的数据。Key/value模型对于IT系统来说的优势在于简单、易部署。但是如果DBA只对部分值进行查询或更新的时候，Key/value就显得效率低下了。举例如：Tokyo Cabinet/Tyrant, Redis, Voldemort, Oracle BDB. 

2.列存储数据库
		这部分数据库通常是用来应对分布式存储的海量数据。键仍然存在，但是它们的特点是指向了多个列。这些列是由列家族来安排的。如：Cassandra, HBase, Riak.     

3.文档型数据库
		文档型数据库的灵感是来自于Lotus Notes办公软件的，而且它同第一种键值存储相类似。该类型的数据模型是版本化的文档，半结构化的文档以特定的格式存储，比如JSON。文档型数据库可 以看作是键值数据库的升级版，允许之间嵌套键值。而且文档型数据库比键值数据库的查询效率更高。如：CouchDB, MongoDb. 国内也有文档型数据库SequoiaDB，已经开源。

4.图形(Graph)数据库
		图形结构的数据库同其他行列以及刚性结构的SQL数据库不同，它是使用灵活的图形模型，并且能够扩展到多个服务器上。NoSQL数据库没有标准的查询语言(SQL)，因此进行数据库查询需要制定数据模型。许多NoSQL数据库都有REST式的数据接口或者查询API。[2]  如：Neo4J, InfoGrid, Infinite Graph.       

​		因此，我们总结NoSQL数据库在以下的这几种情况下比较适用：1、数据模型比较简单；2、需要灵活性更强的IT系统；3、对数据库性能要求较高；4、不需要高度的数据一致性；5、对于给定key，比较容易映射复杂值的环境。 

## 1.2.Redis特点

Redis 与其他 key - value 缓存产品有以下三个特点：

- Redis支持数据的持久化，可以将内存中的数据保存在磁盘中，重启的时候可以再次加载进行使用。
- Redis不仅仅支持简单的key-value类型的数据，同时还提供list，set，zset，hash等数据结构的存储。
- Redis支持数据的备份，集群等高可用功能。

**特点:**

- 性能极高 – Redis能读的速度是110000次/s,写的速度是81000次/s 。
- 丰富的数据类型 – Redis支持的类型 String, List, Hash, Set 及 Ordered Set 数据类型操作。
- 原子 – Redis的所有操作都是原子性的，意思就是要么成功执行要么失败完全不执行。单个操作是原子性的。多个操作也支持事务，即原子性，通过MULTI和EXEC指令包起来。
- 丰富的特性 – Redis还支持 publish/subscribe, 通知, key 过期等等特性。

**Redis是一个简单的，高效的，分布式的，基于内存的缓存工具。  架设好服务器后，通过网络连接（类似数据库），提供Key－Value式缓存服务**。

**简单，是Redis突出的特色。  简单可以保证核心功能的稳定和优异。** 

## 1.3.Redis总结

redis单个key 存入512M大小

redis支持多种类型的数据结构(string,list,hash.set.zset)

redis 是单线程   原子性    

redis可以持久化  因为使用了 RDB和AOF机制  

redis支持集群   而且redis 支持库(0-15) 16个库 

redis 还可以做消息队列  比如聊天室  IM 

企业级开发中:可以用作数据库、缓存(热点数据（经常会被查询，但是不经常被修改或者删除的数据)和消息中间件等大部分功能。

**优点：**  1. 丰富的数据结构

2.高速读写，redis使用自己实现的分离器，代码量很短，没有使用lock（MySQL），因此效率非常高。

**缺点：**  1. 持久化。Redis直接将数据存储到内存中，要将数据保存到磁盘上，Redis可以使用两种方式实现持久化过程。定时快照（snapshot）：每隔一段时间将整个数据库写到磁盘上，每次均是写全部数据，代价非常高。第二种方式基于语句追加（aof）：只追踪变化的数据，但是追加的log可能过大，同时所有的操作均重新执行一遍，回复速度慢。  2. 耗内存，占用内存过高。

## 1.4.**Redis安装**

**Windows安装**

https://jingyan.baidu.com/article/0f5fb099045b056d8334ea97.html

**Linux安装**

**安装Redis** 

官方网站：http://redis.io/ 

官方下载：http://redis.io/download 可以根据需要下载不同版本 

（域名后缀io属于国家域名，是british Indian Ocean territory，即英属印度洋领地）

**Redis安装** 

Redis是C语言开发，安装Redis需要先将官网下载的源码进行编译，编译依赖gcc环境，如果没有gcc环境，需要安装gcc 

![img](D:\MyNote\images\6140.png)

**安装gcc**

gcc的安装很简单，首先要确保root登录，其次就是Linux要能连外网



**注意：**运行yum时出现/var/run/yum.pid已被锁定,PID为xxxx的另一个程序正在运行的问题解决



**安装Redis**

命令1： wget http://download.redis.io/releases/redis-4.0.1.tar.gz

命令2：**tar zxvf redis-4.0.1.tar.gz**

命令3： **cd redis-4.0.1**

命令4（编译）： make   或 **make MALLOC=libc**      如下图代表成功：

![img](D:\MyNote\images\6141.png)

命令5：**make PREFIX=/usr/local/redis install**

（安装编译后的文件） 安装到指目录： 

**注意：**PREFIX必须大写、同时会自动为我们创建redis目录，并将结果安装此目录

命令6： **cd /usr/local/redis**  查看

命令7：查看bin目录下，如图：

![img](D:\MyNote\images\6142.png) 

