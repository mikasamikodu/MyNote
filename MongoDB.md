# 1.安装

1.安装MongoDB安装包；

2.配置环境变量Path,添加值C:\SoftWare\MongoDB\Server\3.2\bin；

3.建议在c盘根目录建立文件夹data,然后在里面建立文件夹db。

​	也可以在其他盘根目录下建data文件夹，但是启动服务器时需要指定目录；

4.按Win+R，然后输入cmd并回车，打开Dos窗口，输入指令`mongod`即可开启MongoDB服务器；

​	**注意1**：32位Windos系统，启动服务器时，输入指令：`mongod --storageEngine=mmapv1`

​	**注意2**：如果第三步将data文件夹建在非c盘根目录，那就需要在启动服务器时指定文件夹所在路径。

​				指令：`mongod --dbpath d:/data/db ` 

​	**注意3**：服务器启动后，端口默认是27017。可以在启动服务器事通过指令`--port 123`指定服务器端口。

​				完整指令：`mongod --port 123`,指定服务器端口为123

5.保持第一个Dos窗口打开，然后打开第二个Dos窗口，输入指令`mongo`,即可连接服务器；

6.总结

​	数据库：

​		数据库服务器:主要是存储数据，通过指令`mongod`启动

​		数据库客户端:主要是操作服务器，对数据进行增删改查(crud)。通过指令`mongo`启动客户端

将MongoDB设置为系统服务。每次可自动启动，无需手动：

​	1.在上面第三步data目录下建一个log和db文件夹；

​	2.在MongoDB安装目录下，找到bin文件夹，在其同级目录下创建配置文件mongod.cfg;

​	3.向mongod.cfg中加入内容如下：

```cfg
systemLog:
	destination: file
	path: c:\data\log\mongod.log
storage:
	dbPath: c:\data\db
```



​	4.以管理员身份打开Dos窗口执行如下指令：

```xml
mongod --dbpath d:\data\db --logpath d:\data\log\mongod.log --install --serviceName "MongoDB"
```

 

之后在”服务“中找到MongoDB服务并启动。

如果启动失败，则在控制台执行指令`sc delete MongoDB`。删除服务。

然后重新执行上面的4个步骤。

## 1.1.连接数据库

标准 URI 连接语法：

```
mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][?options]]
```

- **mongodb://** 这是固定的格式，必须要指定。
- **username:password@** 可选项，如果设置，在连接数据库服务器之后，驱动都会尝试登陆这个数据库
- **host1** 必须的指定至少一个host, host1 是这个URI唯一要填写的。它指定了要连接服务器的地址。如果要连接复制集，请指定多个主机地址。
- **portX** 可选的指定端口，如果不填，默认为27017
- **/database** 如果指定username:password@，连接并验证登陆指定数据库。若不指定，默认打开 test 数据库。
- **?options** 是连接选项。如果不使用/database，则前面需要加上/。所有连接选项都是键值对name=value，键值对之间通过&或;（分号）隔开

标准的连接格式包含了多个选项(options)，如下所示：

| 选项                | 描述                                                         |
| :------------------ | :----------------------------------------------------------- |
| replicaSet=name     | 验证replica set的名称。 Impliesconnect=replicaSet.           |
| slaveOk=true\|false | true:在connect=direct模式下，驱动会连接第一台机器，即使这台服务器不是主。在connect=replicaSet模式下，驱动会发送所有的写请求到主并且把读取操作分布在其他从服务器。false: 在 connect=direct模式下，驱动会自动找寻主服务器. 在connect=replicaSet 模式下，驱动仅仅连接主服务器，并且所有的读写命令都连接到主服务器。 |
| safe=true\|false    | true: 在执行更新操作之后，驱动都会发送getLastError命令来确保更新成功。(还要参考 wtimeoutMS).false: 在每次更新之后，驱动不会发送getLastError来确保更新成功。 |
| w=n                 | 驱动添加 { w : n } 到getLastError命令. 应用于safe=true。     |
| wtimeoutMS=ms       | 驱动添加 { wtimeout : ms } 到 getlasterror 命令. 应用于 safe=true. |
| fsync=true\|false   | true: 驱动添加 { fsync : true } 到 getlasterror 命令.应用于 safe=true.false: 驱动不会添加到getLastError命令中。 |
| journal=true\|false | 如果设置为 true, 同步到 journal (在提交到数据库前写入到实体中). 应用于 safe=true |
| connectTimeoutMS=ms | 可以打开连接的时间。                                         |
| socketTimeoutMS=ms  | 发送和接受sockets的时间。                                    |

更多连接实例

连接本地数据库服务器，端口是默认的。

```
mongodb://localhost
```

使用用户名fred，密码foobar登录localhost的admin数据库。

```
mongodb://fred:foobar@localhost
```

使用用户名fred，密码foobar登录localhost的baz数据库。

```
mongodb://fred:foobar@localhost/baz
```

连接 replica pair, 服务器1为example1.com服务器2为example2。

```
mongodb://example1.com:27017,example2.com:27017
```

连接 replica set 三台服务器 (端口 27017, 27018, 和27019):

```
mongodb://localhost,localhost:27018,localhost:27019
```

连接 replica set 三台服务器, 写入操作应用在主服务器 并且分布查询到从服务器。

```
mongodb://host1,host2,host3/?slaveOk=true
```

直接连接第一个服务器，无论是replica set一部分或者主服务器或者从服务器。

```
mongodb://host1,host2,host3/?connect=direct;slaveOk=true
```

当你的连接服务器有优先级，还需要列出所有服务器，你可以使用上述连接方式。

安全模式连接到localhost:

```
mongodb://localhost/?safe=true
```

以安全模式连接到replica set，并且等待至少两个复制服务器成功写入，超时时间设置为2秒。

```
mongodb://host1,host2,host3/?safe=true;w=2;wtimeoutMS=2000
```



# 2.CRUD

​		在MongoDB中有数据库，数据库下面有集合，集合下面有文档，数据库最小单位就是文档，我们主要操作的就是文档。

## 2.1.数据库-CRUD

### 2.1.1.CR

`show dbs`或`show datsbases` ：查询所有的数据库的名字及其大小

`db`: 查询当前所在数据库的名称

`use test`：使用test数据库，如果没有这个数据库就自动创建

数据库也通过名字来标识。数据库名可以是满足以下条件的任意UTF-8字符串。

- 不能是空字符串（"")。
- 不得含有' '（空格)、.、$、/、\和\0 (空字符)。
- 应全部小写。
- 最多64字节。

有一些数据库名是保留的，可以直接访问这些有特殊作用的数据库。

- **admin**： 从权限的角度来看，这是"root"数据库。要是将一个用户添加到这个数据库，这个用户自动继承所有数据库的权限。一些特定的服务器端命令也只能从这个数据库运行，比如列出所有的数据库或者关闭服务器。
- **local:** 这个数据永远不会被复制，可以用来存储限于本地单台服务器的任意集合
- **config**: 当Mongo用于分片设置时，config数据库在内部使用，用于保存分片的相关信息。

> **注意:** 在 MongoDB 中，集合只有在内容插入后才会创建! 就是说，创建集合(数据表)后要再插入一个文档(记录)，集合才会真正创建。

### 2.1.2.D

MongoDB 删除数据库的语法格式如下：

```sql
db.dropDatabase()
```



## 2.2.集合-CRUD

### 2.2.1.R

`show collections`：查询当前数据库中所有集合

文档键命名规范：

- 键不能含有\0 (空字符)。这个字符用来表示键的结尾。
- .和$有特别的意义，只有在特定环境下才能使用。
- 以下划线"_"开头的键是保留的(不是严格要求的)。

### 2.2.2.D

以下实例删除了 runoob 数据库中的集合 site：

```sql
> use runoob
switched to db runoob
> db.createCollection("runoob")     # 先创建集合，类似数据库中的表
> show tables             # show collections 命令会更加准确点
runoob
> db.runoob.drop()
true
> show tables
```



### 2.2.3.C

MongoDB 中使用 **createCollection()** 方法来创建集合。

语法格式：

```sql
db.createCollection(name, options)
```



实例

在 test 数据库中创建 runoob 集合：

```sql
> use test
switched to db test
> db.createCollection("runoob")
{ "ok" : 1 }
```



下面是带有几个关键参数的 createCollection() 的用法：

创建固定集合 mycol，整个集合空间大小 6142800 KB, 文档最大个数为 10000 个。

```sql
> db.createCollection("mycol", { capped : true, autoIndexId : true, size : 
   6142800, max : 10000 } )
{ "ok" : 1 }
```



## 2.3.文档-CRUD

### 2.3.1.C

`db.student.insert({name:"tom", age:18, gender:"male"})`：向当前数据库中student集合插入一条数据

`db`：代表当前数据库

`db.student`：表示对当前数据库中的student集合做操作，如果集合不存在就自动创建

``db.student.insert()`：代表插入一条数据

`{name:"tom", age:18, gender:"male"}`：一条Json类型的数据或一个文档对象

```sql
db.student.insert([
	{name:"tom", age:18, gender:"male"},
    {name:"tom", age:18, gender:"male"},
    {name:"tom", age:18, gender:"male"}
]);
--向当前数据库的student集合插入多条数据
```



每条数据插入之后会自动生成对应的_id，这个字段是这条数据的唯一标识。这个_id可以通过指令`ObjectId()`来生成。

![1582183391582](D:\MyNote\images\Css.md)

`db.student.insertOne()`：插入一个文档

`db.student.insertMany()`：插入多个文档

上面两条指令都是在MongoDB 3.2后增加的，用于区分插入一个和多个文档

文档键命名规范：

- 键不能含有\0 (空字符)。这个字符用来表示键的结尾。
- .和$有特别的意义，只有在特定环境下才能使用。
- 以下划线"_"开头的键是保留的(不是严格要求的)。

 插入文档你也可以使用 db.col.save(document) 命令。 

### 2.3.2.R

`db.student.find()`：查询当前集合中所有符合条件的文档，内部可以接受一个对象作为参数;

`find()`返回的是一个数组,所以可以通过指定数组下标取数，`db.student.find({age:18})[0];`

​			还可以通过`count()`,或`length()`得到数组大小；`db.student.find({age:18}).count();`

 `db.student.find({name:"张三", age:12});`

`db.student.find({_id:ObjectId("5e4e390e52b51ba561eb8cd2")})`

`db.student.findOne({age:18});`：返回查询结果中第一条，即返回的是一个对象



MongoDB 查询数据的语法格式如下：

```sql
db.collection.find(query, projection)
```

- **query** ：可选，使用查询操作符指定查询条件
- **projection** ：可选，使用投影操作符指定返回的键。查询时返回文档中所有键值， 只需省略该参数即可（默认省略）。

如果你需要以易读的方式来读取数据，可以使用 pretty() 方法，语法格式如下：

```sql
>db.col.find().pretty()
```

pretty() 方法以格式化的方式来显示所有文档。

MongoDB OR 条件语句使用了关键字 **$or**,语法格式如下：

```sql
>db.col.find(
   {
      $or: [
         {key1: value1}, {key2:value2}
      ]
   }
).pretty()
```



以下实例演示了 AND 和 OR 联合使用，类似常规 SQL 语句为： **'where likes>50 AND (by = '菜鸟教程' OR title = 'MongoDB 教程')'**

```sql
>db.col.find({"likes": {$gt:50}, $or: [{"by": "菜鸟教程"},{"title": "MongoDB 教程"}]}).pretty()
```



```sql
//MongoDB支持直接通过内嵌文档的属性进行查询，如果要查询内嵌文档则可以通过.的形式进行匹配,此时属性名是必须要加引号的，单引号和双引号都支持
db.user.find({"hobby.movies":"hero"})
```

### 2.3.3.U

MongoDB 使用 **update()** 和 **save()** 方法来更新集合中的文档。接下来让我们详细来看下两个函数的应用及其区别。

update() 方法用于更新已存在的文档。语法格式如下：

```
db.collection.update(
   <query>,
   <update>,
   {
     upsert: <boolean>,
     multi: <boolean>,
     writeConcern: <document>
   }
)
```

**参数说明：**

- **query** : update的查询条件，类似sql update查询内where后面的。
- **update** : update的对象和一些更新的操作符（如$,$inc...）等，也可以理解为sql update查询内set后面的
- **upsert** : 可选，这个参数的意思是，如果不存在update的记录，是否插入objNew,true为插入，默认是false，不插入。
- **multi** : 可选，mongodb 默认是false,只更新找到的第一条记录，如果这个参数为true,就把按条件查出来多条记录全部更新。
- **writeConcern** :可选，抛出异常的级别。

我们在集合 col 中插入如下数据：

```sql
>db.col.insert({
    title: 'MongoDB 教程', 
    description: 'MongoDB 是一个 Nosql 数据库',
    by: '菜鸟教程',
    url: 'http://www.runoob.com',
    tags: ['mongodb', 'database', 'NoSQL'],
    likes: 100
})
```

接着我们通过 update() 方法来更新标题(title):

```sql
>db.col.update({'title':'MongoDB 教程'},{$set:{'title':'MongoDB'}})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })   # 输出信息
```

以上语句只会修改第一条发现的文档，如果你要修改多条相同的文档，则需要设置 multi 参数为 true。

```sql
>db.col.update({'title':'MongoDB 教程'},{$set:{'title':'MongoDB'}},{multi:true})
```



```sql
只更新第一条记录：

db.col.update( { "count" : { $gt : 1 } } , { $set : { "test2" : "OK"} } );

全部更新：

db.col.update( { "count" : { $gt : 3 } } , { $set : { "test2" : "OK"} },false,true );

只添加第一条：

db.col.update( { "count" : { $gt : 4 } } , { $set : { "test5" : "OK"} },true,false );

全部添加进去:

db.col.update( { "count" : { $gt : 5 } } , { $set : { "test5" : "OK"} },true,true );

全部更新：

db.col.update( { "count" : { $gt : 15 } } , { $inc : { "count" : 1} },false,true );

只更新第一条记录：将count在原来基础上再加1

db.col.update( { "count" : { $gt : 10 } } , { $inc : { "count" : 1} },false,false );
向数组中添加数据，不检查数组中是否已有该元素
db.user.update({username:"tangseng"},{$push:{"hobby.movies":"Interstellar"}})
向数组中添加数据，检查数组中是否已有该元素,已有则不再加入；若没有则将该元素加入数组
db.user.update({username:"tangseng"},{$addToSet:{"hobby.movies":"Interstellar"}})
```



`db.col.updateMany()`:更新所有符合条件的文档

`db.col.updateOne()`:更新第一个符合条件的文档

`db.col.replaceOne()`:替换第一个符合条件的文档

`db.col.replaceOne({name:"tom"},{name:"rose"})`:用rose替换tom	

### 2.3.4.D

remove() 方法的基本语法格式如下所示：

```sql
db.collection.remove(
   <query>,
   <justOne>
)
```

如果你的 MongoDB 是 2.6 版本以后的，语法格式如下：

```sql
db.collection.remove(
   <query>,
   {
     justOne: <boolean>,
     writeConcern: <document>
   }
)
```

**参数说明：**

- **query** :（可选）删除的文档的条件。
- **justOne** : （可选）如果设为 true 或 1，则只删除一个文档，如果不设置该参数，或使用默认值 false，则删除所有匹配条件的文档。
- **writeConcern** :（可选）抛出异常的级别。

以下文档我们执行两次插入操作：

```sql
>db.col.insert({title: 'MongoDB 教程', 
    description: 'MongoDB 是一个 Nosql 数据库',
    by: '菜鸟教程',
    url: 'http://www.runoob.com',
    tags: ['mongodb', 'database', 'NoSQL'],
    likes: 100
})
```



接下来我们移除 title 为 'MongoDB 教程' 的文档：

```sql
>db.col.remove({'title':'MongoDB 教程'})
WriteResult({ "nRemoved" : 2 })           # 删除了两条数据
>db.col.find()
……                                        # 没有数据
```



如果你只想删除第一条找到的记录可以设置 justOne 为 1，如下所示：

```sql
>db.COLLECTION_NAME.remove(DELETION_CRITERIA,1)
```

如果你想删除所有数据，可以使用以下方式（类似常规 SQL 的 truncate 命令）：

```sql
>db.col.remove({})
>db.col.find()
```



`db.student.deleteOne()`:删除第一个符合条件的文档

`db.student.deleteMany()`:删除所有符合条件的文档

# 3.条件操作符

如果你想获取 "col" 集合中 "likes" 大于 100 的数据，你可以使用以下命令：

```sql
db.col.find({likes : {$gt : 100}})
```



如果你想获取"col"集合中 "likes" 大于等于 100 的数据，你可以使用以下命令：

```sql
db.col.find({likes : {$gte : 100}})
```



如果你想获取"col"集合中 "likes" 小于 150 的数据，你可以使用以下命令：

```sql
db.col.find({likes : {$lt : 150}})
```



如果你想获取"col"集合中 "likes" 小于等于 150 的数据，你可以使用以下命令：

```sql
db.col.find({likes : {$lte : 150}})
```



如果你想获取"col"集合中 "likes" 大于100，小于 200 的数据，你可以使用以下命令：

```sql
db.col.find({likes : {$lt :200, $gt : 100}})
```



```sql
$eq  --------  equal  =

$gt -------- greater than  >

$gte --------- gt equal  >=

$lt -------- less than  <

$lte --------- lt equal  <=

$ne ----------- not equal  !=
```



**模糊查询**

查询 title 包含"教"字的文档：

```sql
db.col.find({title:/教/})
```

查询 title 字段以"教"字开头的文档：

```sql
db.col.find({title:/^教/})
```

查询 titl e字段以"教"字结尾的文档：

```sql
db.col.find({title:/教$/})
```



# 4.$type操作符

$type操作符是基于BSON类型来检索集合中匹配的数据类型，并返回结果。

MongoDB 中可以使用的类型如下表所示：

| **类型**                | **数字** | **备注**         |
| :---------------------- | :------- | :--------------- |
| Double                  | 1        |                  |
| String                  | 2        |                  |
| Object                  | 3        |                  |
| Array                   | 4        |                  |
| Binary data             | 5        |                  |
| Undefined               | 6        | 已废弃。         |
| Object id               | 7        |                  |
| Boolean                 | 8        |                  |
| Date                    | 9        |                  |
| Null                    | 10       |                  |
| Regular Expression      | 11       |                  |
| JavaScript              | 13       |                  |
| Symbol                  | 14       |                  |
| JavaScript (with scope) | 15       |                  |
| 32-bit integer          | 16       |                  |
| Timestamp               | 17       |                  |
| 64-bit integer          | 18       |                  |
| Min key                 | 255      | Query with `-1`. |
| Max key                 | 127      |                  |



如果想获取 "col" 集合中 title 为 String 的数据，你可以使用以下命令：

```sql
db.col.find({"title" : {$type : 2}})
或
db.col.find({"title" : {$type : 'string'}})
```

输出结果为：

```sql
{ "_id" : ObjectId("56066542ade2f21f36b0313a"), "title" : "PHP 教程", "description" : "PHP 是一种创建动态交互性站点的强有力的服务器端脚本语言。", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "php" ], "likes" : 200 }
{ "_id" : ObjectId("56066549ade2f21f36b0313b"), "title" : "Java 教程", "description" : "Java 是由Sun Microsystems公司于1995年5月推出的高级程序设计语言。", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "java" ], "likes" : 150 }
{ "_id" : ObjectId("5606654fade2f21f36b0313c"), "title" : "MongoDB 教程", "description" : "MongoDB 是一个 Nosql 数据库", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "mongodb" ], "likes" : 100 }
```



# 5.limit与skip方法

如果你需要在MongoDB中读取指定数量的数据记录，可以使用MongoDB的Limit方法，limit()方法接受一个数字参数，该参数指定从MongoDB中读取的记录条数。

**语法**

limit()方法基本语法如下所示：

```sql
>db.COLLECTION_NAME.find().limit(NUMBER)
```

 注：如果你们没有指定limit()方法中的参数则显示集合中的所有数据。 

我们除了可以使用limit()方法来读取指定数量的数据外，还可以使用skip()方法来跳过指定数量的数据，skip方法同样接受一个数字参数作为跳过的记录条数。

**语法**

skip() 方法脚本语法格式如下：

```
>db.COLLECTION_NAME.find().limit(NUMBER).skip(NUMBER)
```

**实例**

以下实例只会显示第二条文档数据

```sql
>db.col.find({},{"title":1,_id:0}).limit(1).skip(1)
{ "title" : "Java 教程" }
>
```

**注:**skip()方法默认参数为 0 。



# 6.sort()

在 MongoDB 中使用 sort() 方法对数据进行排序，sort() 方法可以通过参数指定排序的字段，并使用 1 和 -1 来指定排序的方式，其中 1 为升序排列，而 -1 是用于降序排列。

**语法**

sort()方法基本语法如下所示：

```sql
>db.COLLECTION_NAME.find().sort({KEY:1})
```



**实例**

col 集合中的数据如下：

```sql
{ "_id" : ObjectId("56066542ade2f21f36b0313a"), "title" : "PHP 教程", "description" : "PHP 是一种创建动态交互性站点的强有力的服务器端脚本语言。", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "php" ], "likes" : 200 }
{ "_id" : ObjectId("56066549ade2f21f36b0313b"), "title" : "Java 教程", "description" : "Java 是由Sun Microsystems公司于1995年5月推出的高级程序设计语言。", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "java" ], "likes" : 150 }
{ "_id" : ObjectId("5606654fade2f21f36b0313c"), "title" : "MongoDB 教程", "description" : "MongoDB 是一个 Nosql 数据库", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "mongodb" ], "likes" : 100 }
```



 以下实例演示了 col 集合中的数据按字段 likes 的降序排列： 

```sql
>db.col.find({},{"title":1,_id:0}).sort({"likes":-1})
{ "title" : "PHP 教程" }
{ "title" : "Java 教程" }
{ "title" : "MongoDB 教程" }
```

**投影**

`db.col.find({},{"title":1,_id:0})`:find()内查询条件为空，`{"title":1,_id:0}`表示查询结果显示title，不显示_id。

# 7.索引

索引通常能够极大的提高查询的效率，如果没有索引，MongoDB在读取数据时必须扫描集合中的每个文件并选取那些符合查询条件的记录。

这种扫描全集合的查询效率是非常低的，特别在处理大量的数据时，查询可以要花费几十秒甚至几分钟，这对网站的性能是非常致命的。

索引是特殊的数据结构，索引存储在一个易于遍历读取的数据集合中，索引是对数据库表中一列或多列的值进行排序的一种结构

## 7.1.createIndex() 方法

MongoDB使用 createIndex() 方法来创建索引。

> 注意在 3.0.0 版本前创建索引方法为 db.collection.ensureIndex()，之后的版本使用了 db.collection.createIndex() 方法，ensureIndex() 还能用，但只是 createIndex() 的别名。

**语法**

createIndex()方法基本语法格式如下所示：

```
>db.collection.createIndex(keys, options)
```

语法中 Key 值为你要创建的索引字段，1 为指定按升序创建索引，如果你想按降序来创建索引指定为 -1 即可。

**实例**

```sql
>db.col.createIndex({"title":1})
>
```



createIndex() 方法中你也可以设置使用多个字段创建索引（关系型数据库中称作复合索引）。

```sql
>db.col.createIndex({"title":1,"description":-1})
>
```



createIndex() 接收可选参数，可选参数列表如下：

| Parameter          | Type          | Description                                                  |
| :----------------- | :------------ | :----------------------------------------------------------- |
| background         | Boolean       | 建索引过程会阻塞其它数据库操作，background可指定以后台方式创建索引，即增加 "background" 可选参数。 "background" 默认值为**false**。 |
| unique             | Boolean       | 建立的索引是否唯一。指定为true创建唯一索引。默认值为**false**. |
| name               | string        | 索引的名称。如果未指定，MongoDB的通过连接索引的字段名和排序顺序生成一个索引名称。 |
| dropDups           | Boolean       | **3.0+版本已废弃。**在建立唯一索引时是否删除重复记录,指定 true 创建唯一索引。默认值为 **false**. |
| sparse             | Boolean       | 对文档中不存在的字段数据不启用索引；这个参数需要特别注意，如果设置为true的话，在索引字段中不会查询出不包含对应字段的文档.。默认值为 **false**. |
| expireAfterSeconds | integer       | 指定一个以秒为单位的数值，完成 TTL设定，设定集合的生存时间。 |
| v                  | index version | 索引的版本号。默认的索引版本取决于mongod创建索引时运行的版本。 |
| weights            | document      | 索引权重值，数值在 1 到 99,999 之间，表示该索引相对于其他索引字段的得分权重。 |
| default_language   | string        | 对于文本索引，该参数决定了停用词及词干和词器的规则的列表。 默认为英语 |
| language_override  | string        | 对于文本索引，该参数指定了包含在文档中的字段名，语言覆盖默认的language，默认值为 language. |

**实例**

在后台创建索引：

```sql
db.values.createIndex({open: 1, close: 1}, {background: true})
```

通过在创建索引时加 background:true 的选项，让创建工作在后台执行

## 7.2.索引相关操作

1、查看集合索引

```sql
db.col.getIndexes()
```

2、查看集合索引大小

```sql
db.col.totalIndexSize()
```

3、删除集合所有索引

```sql
db.col.dropIndexes()
```

4、删除集合指定索引

```sql
db.col.dropIndex("索引名称")
```



## 7.3.失效时间设置

利用 TTL 集合对存储的数据进行失效时间设置：经过指定的时间段后或在指定的时间点过期，MongoDB 独立线程去清除数据。类似于设置定时自动删除任务，可以清除历史记录或日志等前提条件，设置 Index 的关键字段为日期类型 new Date()。 

**例如数据记录中 createDate 为日期类型时：**

-  设置时间180秒后自动清除。
-  设置在创建记录后，180 秒左右删除。

```sql
db.col.createIndex({"createDate": 1},{expireAfterSeconds: 180})
```

**由记录中设定日期点清除。**

设置 A 记录在 2019 年 1 月 22 日晚上 11 点左右删除，A 记录中需添加 "ClearUpDate": new Date('Jan 22, 2019 23:00:00')，且 Index中expireAfterSeconds 设值为 0。

```sql
db.col.createIndex({"ClearUpDate": 1},{expireAfterSeconds: 0})
```

其他注意事项:

-  索引关键字段必须是 Date 类型。
-  非立即执行：扫描 Document 过期数据并删除是独立线程执行，默认 60s 扫描一次，删除也不一定是立即删除成功。
-  单字段索引，混合索引不支持。

# 8.聚合

MongoDB中聚合(aggregate)主要用于处理数据(诸如统计平均值,求和等)，并返回计算后的数据结果。有点类似sql语句中的 count(*)。

------

## 8.1.aggregate() 方法

MongoDB中聚合的方法使用aggregate()。

### 8.1.1.语法

aggregate() 方法的基本语法格式如下所示：

```sql
>db.COLLECTION_NAME.aggregate(AGGREGATE_OPERATION)
```

### 8.1.2.实例

集合中的数据如下：

```sql
{
   _id: ObjectId(7df78ad8902c)
   title: 'MongoDB Overview', 
   description: 'MongoDB is no sql database',
   by_user: 'runoob.com',
   url: 'http://www.runoob.com',
   tags: ['mongodb', 'database', 'NoSQL'],
   likes: 100
},
{
   _id: ObjectId(7df78ad8902d)
   title: 'NoSQL Overview', 
   description: 'No sql database is very fast',
   by_user: 'runoob.com',
   url: 'http://www.runoob.com',
   tags: ['mongodb', 'database', 'NoSQL'],
   likes: 10
},
{
   _id: ObjectId(7df78ad8902e)
   title: 'Neo4j Overview', 
   description: 'Neo4j is no sql database',
   by_user: 'Neo4j',
   url: 'http://www.neo4j.com',
   tags: ['neo4j', 'database', 'NoSQL'],
   likes: 750
},
```

现在我们通过以上集合计算每个作者所写的文章数，使用aggregate()计算结果如下：

```sql
> db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$sum : 1}}}])
{
   "result" : [
      {
         "_id" : "runoob.com",
         "num_tutorial" : 2
      },
      {
         "_id" : "Neo4j",
         "num_tutorial" : 1
      }
   ],
   "ok" : 1
}
>
```

以上实例类似sql语句：

```sql
 select by_user, count(*) from mycol group by by_user
```

在上面的例子中，我们通过字段 by_user 字段对数据进行分组，并计算 by_user 字段相同值的总和。

下表展示了一些聚合的表达式:

| 表达式    | 描述                                           | 实例                                                         |
| :-------- | :--------------------------------------------- | :----------------------------------------------------------- |
| $sum      | 计算总和。                                     | db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$sum : "$likes"}}}]) |
| $avg      | 计算平均值                                     | db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$avg : "$likes"}}}]) |
| $min      | 获取集合中所有文档对应值得最小值。             | db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$min : "$likes"}}}]) |
| $max      | 获取集合中所有文档对应值得最大值。             | db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$max : "$likes"}}}]) |
| $push     | 在结果文档中插入值到一个数组中。               | db.mycol.aggregate([{$group : {_id : "$by_user", url : {$push: "$url"}}}]) |
| $addToSet | 在结果文档中插入值到一个数组中，但不创建副本。 | db.mycol.aggregate([{$group : {_id : "$by_user", url : {$addToSet : "$url"}}}]) |
| $first    | 根据资源文档的排序获取第一个文档数据。         | db.mycol.aggregate([{$group : {_id : "$by_user", first_url : {$first : "$url"}}}]) |
| $last     | 根据资源文档的排序获取最后一个文档数据         | db.mycol.aggregate([{$group : {_id : "$by_user", last_url : {$last : "$url"}}}]) |

------

## 8.2.管道的概念

管道在Unix和Linux中一般用于将当前命令的输出结果作为下一个命令的参数。

MongoDB的聚合管道将MongoDB文档在一个管道处理完毕后将结果传递给下一个管道处理。管道操作是可以重复的。

表达式：处理输入文档并输出。表达式是无状态的，只能用于计算当前聚合管道的文档，不能处理其它的文档。

这里我们介绍一下聚合框架中常用的几个操作：

- $project：修改输入文档的结构。可以用来重命名、增加或删除域，也可以用于创建计算结果以及嵌套文档。
- $match：用于过滤数据，只输出符合条件的文档。$match使用MongoDB的标准查询操作。
- $limit：用来限制MongoDB聚合管道返回的文档数。
- $skip：在聚合管道中跳过指定数量的文档，并返回余下的文档。
- $unwind：将文档中的某一个数组类型字段拆分成多条，每条包含数组中的一个值。
- $group：将集合中的文档分组，可用于统计结果。
- $sort：将输入文档排序后输出。
- $geoNear：输出接近某一地理位置的有序文档。

### 8.2.1.管道操作符实例

1、$project实例



```sql
db.article.aggregate(
    { $project : {
        title : 1 ,sql
        author : 1 ,
    }}
 );
```

这样的话结果中就只还有_id,tilte和author三个字段了，默认情况下_id字段是被包含的，如果要想不包含_id话可以这样:

```sql
db.article.aggregate(
    { $project : {
        _id : 0 ,
        title : 1 ,
        author : 1
    }});
```

2.$match实例

```sql
db.articles.aggregate( [
                        { $match : { score : { $gt : 70, $lte : 90 } } },
                        { $group: { _id: null, count: { $sum: 1 } } }
                       ] );
```

$match用于获取分数大于70小于或等于90记录，然后将符合条件的记录送到下一阶段$group管道操作符进行处理。

3.$skip实例

```sql
db.article.aggregate(
    { $skip : 5 });
```

经过$skip管道操作符处理后，前五个文档被"过滤"掉。

# 9.Mongoose

mongoose是通过nodejs中的mongoose模块操作MongoDB.

1.下载安装Mongoose模块    
	`npm i mongoose --save`或`npm install nongoose`

2.在项目中引入Mongoose模块    
	`var mongoose = require("mongoose");`

3.连接MongDB数据库    
	`mongoose.connect('mongodb://数据库ip地址:端口号/数据库名',{useMongoClient: true})`    

​	端口号如果是默认端口号就可以省略--监听MongoDB数据库的连接状态    

​	--在MongoDB的对象中，有一个属性叫connection，该属性就是表示数据库连接状态的       

​	 通过监听该属性的状态就可以监听数据库的连接与断开    

​	数据库连接成功事件：`mongoose.connection.once("open", function(){})`    

​	数据库连接断开事件：`mongoose.connection.once("close", function(){})`

## 连接数据库

```js
var mongoose = require("mongoose");
mongoose.connect("mongodb://127.0.0.1/mongoose_test", 
                 { useNewUrlParser: true, useUnifiedTopology: true });
mongoose.connection.once("open", function(){
    console.log("数据库连接成功");
});
mongoose.connection.once("close", function(){
    console.log("数据库连接断开");
});
//断开连接，
mongoose.disconnect();
```



## 创建Schema,model与文档

```js
let mongoose = require("mongoose");
mongoose.connect("mongodb://127.0.0.1/mongoose_test", { useNewUrlParser: true, useUnifiedTopology: true });
mongoose.connection.once("open", function(){
    console.log("数据库连接成功");
});
let Schema = mongoose.Schema;
let stuSchema = new Schema({
    name: String,
    age: Number,
    gender: {
        type: String,
        default: "female"
    },
    address: String
});
//数据库中插入文档时，如果文档名是单数，则数据库会将其变为复数
let stuModel = mongoose.model('student', stuSchema);
stuModel.create({
    name: "孙悟空",
    age: 18,
    gender: "male",
    address: "花果山"
}, function (error) {
    if(!error){
        console.log("插入成功");
    }
})
```



## 文档创建

```js
/*
MyModel.create(docs, [callback])
    --用于创建一个或多个文档
    参数
        docs：一个或多个文档对象
        [callback]：回调函数
*/
stuModel.create({
    name: "孙悟空",
    age: 18,
    gender: "male",
    address: "花果山"
}, function (error) {
    if(!error){
        console.log("插入成功");
    }
})

/*
document的方法
        save(options, callback)
        get()：获取文档中指定的属性值
        set()：设置文档中指定的属性值
        toJSON()：将文档对象转换为一个Json对象	
        toObjct()：将文档对象转换为一个Object对象
*/
let stu = new stuModel({
    name: "孙悟空",
    age: 19,
    gender: "male",
    address: "花果山"
});
stu.save(function(error){
    if(!error){
        console.log("保存成功");
    }
});
stuModel.findOne({name: "孙悟空"}, function(error, doc){
    if(!error){
        doc.age = 22;
        doc.save();
    }
});

```



## 文档查询

```js
/*
 Model.find(conditions, projection, options, callback)
    --将符合条件的所有文档返回,返回的总是一个数组
    Model.findById(conditions, projection, options, callback)
    --通过id返回文档
    Model.findOne(conditions, projection, options, callback)
    --将符合条件的第一个文档返回
    --conditions：查询条件
    --projection：投影，返回的查询结果
    --options：skip,limit
    --callback： 回调函数，必填
*/
/*
stuModel.find({name: "孙悟空"}, function(error, doc){
    if(!error){
        console.log(doc);
    }
})
*/
//搜索name=孙悟空的文档，限制每次只返回10，跳过前面的0调，返回无异常就打印查询结果
stuModel.find({name: "孙悟空"}, null, {limit: 10, skip: 0}, function(error, doc){
    if(!error){
        console.log(doc);
        // console.log(doc[0]);
        // console.log(doc[0].name);
        //查询结果就是文档对象
        //document对象就是model的实例
        //console.log(doc instanceof stuModel);
    }
})
/*
搜索name=孙悟空的文档，限制只返回每条文档的name与age列,但不返回id列，每次查询只返回10条文档，跳过前面的0条文档，返回无异常就打印查询结果
stuModel.find({name: "孙悟空"}, 'name age -_id', {limit: 10, skip: 0}, function(error, doc){
    if(!error){
        console.log(doc);
    }
})
只返回第一个符合条件的文档
stuModel.findOne({}, function(error, doc){
    if(!error){
        console.log(doc.name);
    }
})
只返回id为12345的文档
stuModel.findById("12345", function(error, doc){
    if(!error){
        console.log(doc.name);
    }
})
*/
```



## 文档更新

```js
/*
Model.update(conditions， doc, options, callback)
    Model.updateMany(conditions， doc, options, callback)
    Model.updateOne(conditions， doc, options, callback)
    Model.replaceOne(conditions， doc, options, callback)
    --conditions查询条件
    --doc 修改后的对象
    --options 配置参数
    --callback 回调函数
*/
stuModel.update({name:"孙悟空"}, {$set: {name: 20}}, {multi: false}, function(error){
    if(!error){
        console.log("修改成功");
    }
})

/*
document的方法
	updateOne(update, options, callback)
        updateMany(update, options, callback)
*/
stuModel.findOne({name: "孙悟空"}, function(error, doc){
    if(!error){
        doc.updateOne({$set: {age: 20}}, function(error){
            console.log("修改成功");
        });
    }
});
```



## 文档删除

```js
/*
Model.deleteOne(conditions, callback)
    Model.deleteMany(conditions, callback)
    Model.remove(conditions, callback)
*/
stuModel.deleteOne({name: "孙悟空"}, function(error){
    if(!error){
        console.log("删除成功");
    }
})

/*
document的方法 
	 remove(callback)
*/
stuModel.findOne({name: "孙悟空"}, function(error, doc){
    if(!error){
        doc.remove(function(error){
            console.log("删除成功");
        });
    }
});
```



