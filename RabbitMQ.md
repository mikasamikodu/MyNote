# 1.搭建环境

## 1.1.安装Erlang

官网： https://www.erlang.org/downloads 

安装其实没什么好讲的，就是下一步、下一步。

![img](D:\MyNote\images\C518E432111ED5CC5E7424DE0000C0B2.png)

注意安装的过程可能会弹出一个安装Microsoft Visual C++ 2013（或者其他版本）的弹框、我们只需要点击"Install(安装)"按钮进行安装即可

![img](D:\MyNote\images\2528B51B11CEC4E918DD84DB000050B2.png)

安装完成后我们就要来配置环境变量了

1、新建一个系统变量：变量名为ERLANG_HOME，变量值为安装Erlang的路径（路径中不要包含bin目录)

![image-20191115155901980](D:\MyNote\images\20191115155901980.png)

2、将新建的系统变量添加在Path中：格式为%ERLANG_HOME%\bin（这里我用的win10、win7添加path的不太一样）加入Path

3、然后我们打开cmd输入erl查看是Erlan是否安装好.

## 1.2.安装RabbitMQ

这个安装也没啥好讲的，都是下一步、下一步就好了。

安装完后我们开启后台管理插件

1、首先使用cmd进入sbin目录（我的sbin目录是：C:\Program Files\RabbitMQ Server\rabbitmq_server-3.7.7\sbin)

2、然后输入: rabbitmq-plugins.bat enable rabbitmq_management 开启插件

3、还是在sbin目下：输入 rabbitmq-server 启动RabbitMQ服务

RabbitMQ我已经启动了，为了演示重新启动了下，才出现红框中说我已经启动了的信息

最后我们在本地浏览器中输入：localhost:15672访问RabbitMQ的后台管理页面(初始化用户名和密码都是guest)

![img](D:\MyNote\images\10F06C32096B41205AF584DA0000D0B3.png)

## 1.3.添加用户

![image-20191115160422906](D:\MyNote\images\image-20191115160422906.png)

## 1.4.分配

首先是新建

![image-20191115160606056](D:\MyNote\images\image-20191115160606056.png)

然后点击新添加的数据/vhost_mmr进入设置界面：

![image-20191115160749014](D:\MyNote\images\image-20191115160749014.png)

# 2.消息队列模型

## 2.1. Simple Queue

队列模型

![image-20191115173758311](D:\MyNote\images\image-20191115173758311.png)

1.创建maven工程，pom.xml中加入依赖:

```xml
<dependency>
    <groupId>com.rabbitmq</groupId>
    <artifactId>amqp-client</artifactId>
    <version>5.7.3</version>
</dependency>
```

2.创建消息队列

```java
package com.rabbitmq.util;
import java.io.IOException;
import java.util.concurrent.TimeoutException;
import com.rabbitmq.client.Connection;
import com.rabbitmq.client.ConnectionFactory;
public class ConnectionUtil {
	public static Connection getConnection() throws IOException, TimeoutException {
		ConnectionFactory connectionFactory = new ConnectionFactory();
		connectionFactory.setHost("127.0.0.1");
		connectionFactory.setPort(5672);
		connectionFactory.setVirtualHost("/vhost_mmr");
		connectionFactory.setUsername("admin");
		connectionFactory.setPassword("admin");
		return connectionFactory.newConnection();
	}
}
```

3.创建生产者

```java
package com.rabbitmq.send;
import java.io.IOException;
import java.util.concurrent.TimeoutException;
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;
import com.rabbitmq.util.ConnectionUtil;
public class Send {
	private static final String QUEUE_NAME="test_simple_queue";
	public static void main(String[]args) throws IOException, TimeoutException {
		Connection conn = ConnectionUtil.getConnection();//创建连接		
		Channel channel = conn.createChannel();//创建频道
		channel.queueDeclare(QUEUE_NAME, false, false, false, null);
		String msg = "hello rabbitmq";	
		channel.basicPublish("", QUEUE_NAME, null, msg.getBytes());//发送消息
		System.out.println("send msg:"+msg);
		channel.close();
		conn.close();
	}
}
```

4.创建消费者

```java
package com.rabbitmq.receive;
import java.io.IOException;
import java.util.concurrent.TimeoutException;
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;
import com.rabbitmq.client.DefaultConsumer;
import com.rabbitmq.client.Envelope;
import com.rabbitmq.client.AMQP.BasicProperties;
import com.rabbitmq.util.ConnectionUtil;
public class Receive {
	private static final String QUEUE_NAME="test_simple_queue";
	public static void main(String[]args) throws IOException, TimeoutException {
		Connection conn = ConnectionUtil.getConnection();//创建连接		
		Channel channel = conn.createChannel();//创建频道
		DefaultConsumer consumer = new DefaultConsumer(channel) {
			public void handleDelivery(String consumerTag, Envelope envelope, BasicProperties properties, byte[] body)
					throws IOException {
				String msg = new String(body,"utf-8");
				System.out.println("receive:"+msg);
			}
		};
		channel.basicConsume(QUEUE_NAME, true,consumer);
	}
}
```

生产者每生产一个消息，消费者就消费一个

## 2.2. Works  Queue 

Works  Queue --工作模式

 ![img](D:\MyNote\images\python-two.png) 

1.生产者

```java
public class Send {	
	private static final String QUEUE_NAME="test_work_queue";	
	public static void main(String[]args) throws IOException, TimeoutException, InterruptedException {
		
		Connection connection = ConnectionUtil.getConnection();
		Channel channel = connection.createChannel();
		channel.queueDeclare(QUEUE_NAME, false, false, false, null);
		int i=0;
		while(i<50) {
			String msg = "hello " + i;
			channel.basicPublish("", QUEUE_NAME, null, msg.getBytes());
			System.out.println(msg);
			Thread.sleep(50);
			i++;
		}
		channel.close();
		connection.close();
	}
}
```

2.消费者1

```java
public class Receive1 {
	private static final String QUEUE_NAME="test_work_queue";
	public static void main(String[] args) throws Exception {
		Connection connection = ConnectionUtil.getConnection();
		Channel channel = connection.createChannel();
		channel.queueDeclare(QUEUE_NAME, false, false, false, null);
		Consumer consumer = new DefaultConsumer(channel) {
			@Override
			public void handleDelivery(String consumerTag, Envelope envelope, BasicProperties properties, byte[] body)
					throws IOException {
				String msg = new String(body, "utf-8");
				System.out.println("[1] receive: " + msg);
				try {
					Thread.sleep(1000);
				}catch(Exception e){
					e.printStackTrace();
				}finally {
					System.out.println("[1] done.");
				}
			}
		};
		boolean autoAck = true;//自动应答
		channel.basicConsume(QUEUE_NAME, autoAck, consumer);
	}
}
```

消费者2

```java
public class Receive2 {
	private static final String QUEUE_NAME="test_work_queue";
	public static void main(String[] args) throws Exception {
		Connection connection = ConnectionUtil.getConnection();
		Channel channel = connection.createChannel();
		channel.queueDeclare(QUEUE_NAME, false, false, false, null);
		Consumer consumer = new DefaultConsumer(channel) {
			@Override
			public void handleDelivery(String consumerTag, Envelope envelope, BasicProperties properties, byte[] body)
					throws IOException {
				String msg = new String(body, "utf-8");
				System.out.println("[2] receive: " + msg);
				try {
					Thread.sleep(2000);
				}catch(Exception e){
					e.printStackTrace();
				}finally {
					System.out.println("[2] done.");
				}
			}
		};
		boolean autoAck = true;//自动应答
		channel.basicConsume(QUEUE_NAME, autoAck, consumer);
	}
}
```

生产者生产50个消息，消费者1虽然消费的快，但只消费了所有奇数的消息，消费者2消费了所有偶数的消息

### 2.2.1.公平分发

生产者

```java
public class Send {
	private static final String QUEUE_NAME="test_work_queue";
	public static void main(String[]args) throws IOException, TimeoutException, InterruptedException {
		Connection connection = ConnectionUtil.getConnection();
		Channel channel = connection.createChannel();
		channel.queueDeclare(QUEUE_NAME, false, false, false, null);
		/*
		 * 生产者每次发送一条消息，只有收到消费者的确认消息时才会发送下一条消息
		 * 每次同一消费者消费不能超过一条
		 * */
		int count = 1;
		channel.basicQos(count);
		int i=0;
		while(i<50) {
			String msg = "hello " + i;
			channel.basicPublish("", QUEUE_NAME, null, msg.getBytes());
			System.out.println(msg);
			Thread.sleep(50);
			i++;
		}
		channel.close();
		connection.close();
	}
}
```

消费者1

```java
public class Receive1 {
	private static final String QUEUE_NAME="test_work_queue";
	public static void main(String[] args) throws Exception {
		Connection connection = ConnectionUtil.getConnection();
		Channel channel = connection.createChannel();
		channel.queueDeclare(QUEUE_NAME, false, false, false, null);
		channel.basicQos(1);
		Consumer consumer = new DefaultConsumer(channel) {
			@Override
			public void handleDelivery(String consumerTag, Envelope envelope, BasicProperties properties, byte[] body)
					throws IOException {
				String msg = new String(body, "utf-8");
				System.out.println("[1] receive: " + msg);
				try {
					Thread.sleep(1000);
				}catch(Exception e){
					e.printStackTrace();
				}finally {
					System.out.println("[1] done.");
					channel.basicAck(envelope.getDeliveryTag(), false);
				}
			}
		};
		boolean autoAck = false;//自动应答
		channel.basicConsume(QUEUE_NAME, autoAck, consumer);
	}
}
```

消费者2

```java
public class Receive2 {
	private static final String QUEUE_NAME="test_work_queue";
	public static void main(String[] args) throws Exception {
		Connection connection = ConnectionUtil.getConnection();
		Channel channel = connection.createChannel();
		channel.queueDeclare(QUEUE_NAME, false, false, false, null);
		channel.basicQos(1);
		Consumer consumer = new DefaultConsumer(channel) {
			@Override
			public void handleDelivery(String consumerTag, Envelope envelope, BasicProperties properties, byte[] body)
					throws IOException {
				String msg = new String(body, "utf-8");
				System.out.println("[2] receive: " + msg);
				try {
					Thread.sleep(2000);
				}catch(Exception e){
					e.printStackTrace();
				}finally {
					System.out.println("[2] done.");
					channel.basicAck(envelope.getDeliveryTag(), false);
				}
			}
		};
		boolean autoAck = false;//自动应答
		channel.basicConsume(QUEUE_NAME, autoAck, consumer);
	}
}
```

生产者生产50个消息，消费者1消费的快，消费了33个消息，消费者2消费了17个消息

### 2.2.2.消息应答

```java
boolean autoAck = false;//自动应答
channel.basicConsume(QUEUE_NAME, autoAck, consumer);
```



`boolean autoAck = true;` 自动确认模式，一旦消息队列将消息发送给消费者就会将消息从内存中删除这条消息。
此时如果杀死正在执行的消费者就会使正在出理消息丢失。

`boolean autoAck = true；` 手动模式，如果一个消费者消失，则消息队列会将消息发送给另一个消费者，rabbitmq支持消息的应答，消费者可以发送一个消息应答给消息队列，告诉他已经消费了一个消息，可以删除内存中的消息了。

默认值为false。

### 2.2.3.消息持久化

```java
boolean durable = false;
channel.queueDeclare(QUEUE_NAME, durable, false, false, null);
```



boolean durable = false;消息队列未持久化。

boolean durable = true;消息队列会持久化。

当运行一次消息队列的程序后，再修改durable为true是无法生效的。此时代码是没问题的，但是运行会出现异常。异常意思是因为已经定义了一个队列，所以不允许再修改队列的参数了或不允许重新定义这个队列。

解决办法是修改队列名称--即重新定义一个队列，或从服务端将该消息队列删除。

## 2.3.Publish/Subscribe

Publish/Subscribe--发布/订阅模式

 ![img](https://www.rabbitmq.com/img/tutorials/python-three-overall.png) 

特性：

1. 一个生产者，多个消费者
2. 每个消费者都有自己的队列
3. 生产者没有直接将消息发送给队列，而是发送给交换机  转发器exchanges
4. 每个队列都要绑定在交换机上
5. 生产者发送的消息经过交换机到达队列，就能实现一个消息被多个消费者消费

生产者：

```java
public class Send {
	private static final String EXCHANGE_NAME="test_exchange_fanout";
	public static void main(String[]args) throws IOException, TimeoutException, InterruptedException {
		Connection connection = ConnectionUtil.getConnection();
		Channel channel = connection.createChannel();
		
		channel.exchangeDeclare(EXCHANGE_NAME, "fanout");
		
		String msg = "hello";
		channel.basicPublish(EXCHANGE_NAME, "", null, msg.getBytes());
		System.out.println("send:"+msg);
		channel.close();
		connection.close();
	}
}
```

消费者1：

```java
public class Receive1 {
	private static final String QUEUE_NAME="test_queue_email";
	private static final String EXCHANGE_NAME="test_exchange_fanout";
	public static void main(String[] args) throws Exception {
		Connection connection = ConnectionUtil.getConnection();
		Channel channel = connection.createChannel();
		
		channel.queueDeclare(QUEUE_NAME, false, false, false, null);
		channel.queueBind(QUEUE_NAME, EXCHANGE_NAME, "");
		
		channel.basicQos(1);
		Consumer consumer = new DefaultConsumer(channel) {
			@Override
			public void handleDelivery(String consumerTag, Envelope envelope, BasicProperties properties, byte[] body)
					throws IOException {
				String msg = new String(body, "utf-8");
				System.out.println("[1] receive: " + msg);
				try {
					Thread.sleep(1000);
				}catch(Exception e){
					e.printStackTrace();
				}finally {
					System.out.println("[1] done.");
					channel.basicAck(envelope.getDeliveryTag(), false);
				}
			}
		};
		boolean flag = false;
		channel.basicConsume(QUEUE_NAME, flag, consumer);
	}
}
```



生产者每发送一条消息，每个消费者都可以得到一条消息。

## 2.4.Exchange

Exchange--交换机  转发器

`channel.basicPublish("", QUEUE_NAME, null, msg.getBytes());//发送消息` ，第一个参数是指定交换机名称，""代表的是匿名发布消息。

`channel.exchangeDeclare(EXCHANGE_NAME, "fanout");` ,"fanout"代表不处理路由键；"direct"代表处理路由键。

## 2.5.Routing

Routing--路由模式

 ![img](D:\MyNote\images\python-four.png) 

生产者：

```java
public class Send {
	private static final String EXCHANGE_NAME="test_exchange_direct";
	public static void main(String[]args) throws IOException, TimeoutException, InterruptedException {
		Connection connection = ConnectionUtil.getConnection();
		Channel channel = connection.createChannel();
		
		channel.exchangeDeclare(EXCHANGE_NAME, "direct");
		
		String msg = "hello direct";
		String routingKey = "info";
		channel.basicPublish(EXCHANGE_NAME, routingKey, null, msg.getBytes());
		System.out.println("send:"+msg);
		channel.close();
		connection.close();
	}
}
```



消费者1：

```java
public class Receive1 {
	private static final String QUEUE_NAME="test_queue_direct_1";
	private static final String EXCHANGE_NAME="test_exchange_direct";
	public static void main(String[] args) throws Exception {
		Connection connection = ConnectionUtil.getConnection();
		Channel channel = connection.createChannel();
		
		channel.queueDeclare(QUEUE_NAME, false, false, false, null);
		channel.queueBind(QUEUE_NAME, EXCHANGE_NAME, "error");
		
		channel.basicQos(1);
		Consumer consumer = new DefaultConsumer(channel) {
			@Override
			public void handleDelivery(String consumerTag, Envelope envelope, BasicProperties properties, byte[] body)
					throws IOException {
				String msg = new String(body, "utf-8");
				System.out.println("[1] receive: " + msg);
				try {
					Thread.sleep(1000);
				}catch(Exception e){
					e.printStackTrace();
				}finally {
					System.out.println("[1] done.");
					channel.basicAck(envelope.getDeliveryTag(), false);
				}
			}
		};
		boolean flag = false;
		channel.basicConsume(QUEUE_NAME, flag, consumer);
	}
}
```



消费者2：

```java
public class Receive2 {
	private static final String QUEUE_NAME="test_queue_direct_2";
	private static final String EXCHANGE_NAME="test_exchange_direct";
	public static void main(String[] args) throws Exception {
		Connection connection = ConnectionUtil.getConnection();
		Channel channel = connection.createChannel();
		
		channel.queueDeclare(QUEUE_NAME, false, false, false, null);
		channel.queueBind(QUEUE_NAME, EXCHANGE_NAME, "error");
		channel.queueBind(QUEUE_NAME, EXCHANGE_NAME, "info");
		channel.queueBind(QUEUE_NAME, EXCHANGE_NAME, "warning");
		
		channel.basicQos(1);
		Consumer consumer = new DefaultConsumer(channel) {
			@Override
			public void handleDelivery(String consumerTag, Envelope envelope, BasicProperties properties, byte[] body)
					throws IOException {
				String msg = new String(body, "utf-8");
				System.out.println("[2] receive: " + msg);
				try {
					Thread.sleep(1000);
				}catch(Exception e){
					e.printStackTrace();
				}finally {
					System.out.println("[2] done.");
					channel.basicAck(envelope.getDeliveryTag(), false);
				}
			}
		};
		boolean flag = false;
		channel.basicConsume(QUEUE_NAME, flag, consumer);
	}
}
```



生产者发送消息时会携带一个key，消息中的key匹配上消费者中的key，则该消息可以被该消费者消费，否则不能被消费。例如生产者发送了一个消息携带error的key，1,2两个消费者都可以消费该消息；生产者第二次发送一个消息携带info的key，只有2的消费者可以消费key。

## 2.6. Topics

Topics--主题模式

![img](https://www.rabbitmq.com/img/tutorials/python-five.png) 

生产者：

```java
public class Send {
	private static final String EXCHANGE_NAME="test_exchange_topics";
	public static void main(String[]args) throws IOException, TimeoutException, InterruptedException {
		Connection connection = ConnectionUtil.getConnection();
		Channel channel = connection.createChannel();
		
		channel.exchangeDeclare(EXCHANGE_NAME, "topic");
		
		String msg = "hello topic";
		String routingKey = "goods.del";
		channel.basicPublish(EXCHANGE_NAME, routingKey, null, msg.getBytes());
		System.out.println("send:"+msg);
		channel.close();
		connection.close();
	}
}
```



消费者1：

```java
public class Receive1 {
	private static final String QUEUE_NAME="test_queue_topics_1";
	private static final String EXCHANGE_NAME="test_exchange_topics";
	public static void main(String[] args) throws Exception {
		Connection connection = ConnectionUtil.getConnection();
		Channel channel = connection.createChannel();
		
		channel.queueDeclare(QUEUE_NAME, false, false, false, null);
		channel.queueBind(QUEUE_NAME, EXCHANGE_NAME, "goods.add");
		
		channel.basicQos(1);
		Consumer consumer = new DefaultConsumer(channel) {
			@Override
			public void handleDelivery(String consumerTag, Envelope envelope, BasicProperties properties, byte[] body)
					throws IOException {
				String msg = new String(body, "utf-8");
				System.out.println("[1] receive: " + msg);
				try {
					Thread.sleep(1000);
				}catch(Exception e){
					e.printStackTrace();
				}finally {
					System.out.println("[1] done.");
					channel.basicAck(envelope.getDeliveryTag(), false);
				}
			}
		};
		boolean flag = false;
		channel.basicConsume(QUEUE_NAME, flag, consumer);
	}
}
```



消费者2：

```java
public class Receive2 {
	private static final String QUEUE_NAME="test_queue_topics_2";
	private static final String EXCHANGE_NAME="test_exchange_topics";
	public static void main(String[] args) throws Exception {
		Connection connection = ConnectionUtil.getConnection();
		Channel channel = connection.createChannel();
		
		channel.queueDeclare(QUEUE_NAME, false, false, false, null);
		channel.queueBind(QUEUE_NAME, EXCHANGE_NAME, "goods.#");
		
		channel.basicQos(1);
		Consumer consumer = new DefaultConsumer(channel) {
			@Override
			public void handleDelivery(String consumerTag, Envelope envelope, BasicProperties properties, byte[] body)
					throws IOException {
				String msg = new String(body, "utf-8");
				System.out.println("[2] receive: " + msg);
				try {
					Thread.sleep(1000);
				}catch(Exception e){
					e.printStackTrace();
				}finally {
					System.out.println("[2] done.");
					channel.basicAck(envelope.getDeliveryTag(), false);
				}
			}
		};
		boolean flag = false;
		channel.basicConsume(QUEUE_NAME, flag, consumer);
	}
}
```



#代表匹配一个或多个，*代表匹配一个。

生产者发送消息携带goods.add的主题key，如果消息可以完全匹配消费者主题则可以被消费，因此1,2,消费者都可以消费这条消息；生产者发送消息携带goods.delete的主题key，1不能消费，2可以消费。

# 3.消息确认机制

在rabbitMQ中，通过持久化数据可以结局服务器异常导致数据丢失的情况

问题：生产者将消息发送出去之后，消息是否到达rabbitMQ服务器，默认情况下是不知道的。

rabbitMQ在这方面有两套机制：一是利用AMQP实现事务机制；二是Confirm模式。

## 3.1.事务机制

事务机制有3个方法，txSelect,txCommit,txRollback

txSelect:用户将当前channel设置为transation模式；

txCommit:用于提交事务；

txRollback:用于回滚事务；

以简单模型为例：

生产者：

```java
public class Send {
	private static final String QUEUE_NAME="test_queue_tx";
	public static void main(String[]args) throws IOException, TimeoutException {
		Connection conn = ConnectionUtil.getConnection();//创建连接	
		Channel channel = conn.createChannel();//创建频道
		channel.queueDeclare(QUEUE_NAME, false, false, false, null);
		try {
			channel.txSelect();
			String msg = "hello rabbitmq";
			channel.basicPublish("", QUEUE_NAME, null, msg.getBytes());//发送消息
			System.out.println("send msg:"+msg);
			int a = 1/0;
			channel.txCommit();
		}catch(Exception e) {
			channel.txRollback();
			System.out.println("msg rollback");
			e.printStackTrace();
		}
		channel.close();
		conn.close();
	}
}
```



消费者：

```java
public class Receive {
	private static final String QUEUE_NAME="test_queue_tx";
	public static void main(String[]args) throws IOException, TimeoutException {		
		Connection conn = ConnectionUtil.getConnection();//创建连接
		Channel channel = conn.createChannel();//创建频道
		DefaultConsumer consumer = new DefaultConsumer(channel) {
			@Override
			public void handleDelivery(String consumerTag, Envelope envelope, BasicProperties properties, byte[] body)
					throws IOException {
				String msg = new String(body,"utf-8");
				System.out.println("receive:"+msg);
			}
		};
		channel.basicConsume(QUEUE_NAME, true,consumer);
	}
}
```



## 3.2.Confirm模式

Confirm模式最大的好处在于它是异步的。

开启Confirm模式方法：channel.confirmSelect()

编程模式：

1.普通的   发一条    waitForConfirms()

2.批量的   发一批   waitForConfirms

3.异步confirm模式，提供一种回调方法

以简单模式为例：

第一种：

生产者：

```java
public class Send {
	private static final String QUEUE_NAME="test_queue_confirm_1";
	public static void main(String[]args) throws Exception {
		
		Connection conn = ConnectionUtil.getConnection();
		Channel channel = conn.createChannel();
		channel.queueDeclare(QUEUE_NAME, false, false, false, null);
		channel.confirmSelect();
		
		String msg = "hello rabbitmq";
		channel.basicPublish("", QUEUE_NAME, null, msg.getBytes());
		System.out.println("send msg:"+msg);
		
		if(channel.waitForConfirms()) {
			System.out.println("msg send OK");
		}else{
			System.out.println("msg send OK");
		}
		channel.close();
		conn.close();
	}
}
```



第二种：

生产者：

```java
public class Send {
	private static final String QUEUE_NAME="test_queue_confirm_1";
	public static void main(String[]args) throws Exception {
		
		Connection conn = ConnectionUtil.getConnection();
		Channel channel = conn.createChannel();
		channel.queueDeclare(QUEUE_NAME, false, false, false, null);
		channel.confirmSelect();
		
		for(int i=0;i<10;i++) {
			String msg = "hello rabbitmq batch "+i;
			channel.basicPublish("", QUEUE_NAME, null, msg.getBytes());
		}
		
		if(channel.waitForConfirms()) {
			System.out.println("msg send OK");
		}else{
			System.out.println("msg send OK");
		}
		channel.close();
		conn.close();
	}
}
```



第三种：

生产者：

```java
public class Send2 {
	private static final String QUEUE_NAME="test_queue_confirm_2";
	public static void main(String[]args) throws Exception {
		
		Connection conn = ConnectionUtil.getConnection();
		Channel channel = conn.createChannel();
		channel.queueDeclare(QUEUE_NAME, false, false, false, null);
		channel.confirmSelect();
		
		SortedSet<Long> confirmSet = Collections.synchronizedSortedSet(new TreeSet<Long>());
		channel.addConfirmListener(new ConfirmListener() {
			@Override//消息消费失败调这边
			public void handleNack(long arg0, boolean arg1) throws IOException {
				if(arg1) {
					System.out.println("handleNack----multiple");
					confirmSet.headSet(arg0+1).clear();
				}else {
					System.out.println("handleNack----multiple false");
					confirmSet.remove(arg0);
				}
			}
			@Override	//消息消费成功调这边
			public void handleAck(long arg0, boolean arg1) throws IOException {
				if(arg1) {
					System.out.println("handleAck----multiple");
					confirmSet.headSet(arg0+1).clear();
				}else {
					System.out.println("handleAck----multiple false");
					confirmSet.remove(arg0);
				}
			}
		});
		String msg = "hello rabbitmq confirmSet";
		while (true) {
			long seqNo = channel.getNextPublishSeqNo();
			channel.basicPublish("", QUEUE_NAME, null, msg.getBytes());
			confirmSet.add(seqNo);
		}
	}
}
```



# 4.mq在spring中的使用

依赖：

```xml
<dependency>
    <groupId>com.rabbitmq</groupId>
    <artifactId>amqp-client</artifactId>
    <version>4.0.2</version>
</dependency>
<dependency>
    <groupId>org.springframework.amqp</groupId>
    <artifactId>spring-rabbit</artifactId>
    <version>1.7.5.RELEASE</version>
</dependency>
```



spring配置文件：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:rabbit="http://www.springframework.org/schema/rabbit"
	xsi:schemaLocation="http://www.springframework.org/schema/beans
						http://www.springframework.org/schema/beans/spring-beans-4.0.xsd
						http://www.springframework.org/schema/rabbit
						http://www.springframework.org/schema/rabbit/spring-rabbit-1.7.xsd">
	<!-- 定义rabbit连接工厂 -->
	<rabbit:connection-factory id="connectionFactory" host="127.0.0.1"
							   username="admin" password="admin" virtual-host="/vhost_mmr"/>
	<!-- 定义rabbit模板，用于连接工厂及定义交换机 -->
	<rabbit:template id="amqpTemplate" connection-factory="connectionFactory"
					 exchange="fanoutExchange"/>
	<!-- MQ的管理，包含队列，交换机 声明 -->
	<rabbit:admin connection-factory="connectionFactory"/>
	<!-- 定义队列，可自动声明 -->
	<rabbit:queue name="myQueue" auto-declare="true" durable="true"/>
	<!-- 定义交换器，自动声明 -->
	<rabbit:fanout-exchange name="fanoutExchange" auto-declare="true">
		<rabbit:bindings>
			<rabbit:binding queue="myQueue"></rabbit:binding>
		</rabbit:bindings>
	</rabbit:fanout-exchange>
	<!-- 队列监听 -->
	<rabbit:listener-container connection-factory="connectionFactory">
		<rabbit:listener ref="receive" method="listener" queue-names="myQueue"/>
	</rabbit:listener-container>
	
	<bean id="receive" class="com.rabbitmq.spring.Receive"></bean>
</beans>
```



生产者：

```java
import org.springframework.amqp.rabbit.core.RabbitTemplate;
import org.springframework.context.support.AbstractApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;
public class Send {
	public static void main(String[]args) throws Exception{
		@SuppressWarnings("resource")
		AbstractApplicationContext app = new ClassPathXmlApplicationContext("classpath:context.xml");
		RabbitTemplate  rabbit = app.getBean(RabbitTemplate.class);
		String msg = "hello rabbit";
		rabbit.convertAndSend(msg);
		System.out.println("生产者："+msg);
		Thread.sleep(1000);
		app.destroy();
	}
}
```



消费者：

```java
public class Receive {

	public void listener(String msg) {
		System.out.println("消费者:"+msg);
	}
}
```

