# FileZilla

下面是FileZilla的使用教程：FileZilla是一款免费开源的FTP客户端软件，虽然它是免费软件，可性能却一点也不含糊，比起那些共享软件来有过之而无不及，具备大多数的FTP软件功能。其可控性、有条理的界面和管理多站点的简化方式、特别是它的传输速度，简直是出神入化，也是它最大的特色。总的来说是它一款出类拔萃的免费FTP客户端软件(Filezilla下载)。下面是FileZilla的使用教程：

# 1.快速连接

快速连接就是不需通过站点设置，直接输入IP地址、用户名及密码进行连接。所以它适合用在需要临时性连接的站点，并且快速连信息接会被保存，如果下次还想使用，就可以直接选择进行连接了，非常方便。通过快速连接工具栏输入相关信息，点击快速连接按钮就可以了
![这里写图片描述](D:\MyNote\images\703.png)

连接成功后，在左边看到的就是您电脑上的文件，右边就是空间上的文件，选中您要上传的文件，然后右击，选上传(如果是上传到空间上某个特定的文件夹，请先在右边打开那个文件夹，再上传)。

![1573997592175](D:\MyNote\images\12443.jpg)

下面给您详细的介绍一下Filezilla经常会用到的一些功能，有兴趣的可以了解下：

# 2.站点设置

要使用FTP工具来上传（下载）文件，首先必须要设定好FTP服务器的地址（IP地址）、授权访问的用户名及密码。下面我们将演示具体的参数设置：

通过菜单【文件】—>【站点管理器】或者CTRL+S键我们可以对要连接的FTP服务器进行具体的设置。

第一步：我们可以点击【新站点】按钮，输入站点的名称（它只是对FTP站点的一个说明）。

第二步：按照界面所示，先输入主机（FTP服务器的IP地址），登陆类型选择“一般”，不要选择匿名选项（匿名的意思就是不需要用户名和密码可以直接访问FTP服务器，但很多FTP服务器都禁止匿名访问)，然后分别输入用户和密码。另外对于端口号我们在没有特别要求的情况下不用管它，或者输入“21”也可以。

第三步：在高级选项卡我们可以设置默认的远程及本地目录，远程目录其实就是连上FTP服务器后默认打开的目录；而本地目录就是每次进入FTP软件后默认显示的本地文件目录（当然了，如果大家不太清楚或者感觉麻烦的话也可以先不设置远程及本地路径，系统将会使用自己的默认路径）。

以上这些参数都设置好之后，便可使用FTP进行文件上传下载了。

![这里写图片描述](D:\MyNote\images\20180828113752373.png)

# 2.连接FTP/上传（下载）文件

## 2.1.连接

通过上面的设置之后现在就可以连接服务器上传文件了。我们可以通过菜单【文件】—>【站点管理器】或者CTRL+S键进入站点管理器选择要连接的FTP服务器，点击【连接】按钮就可以了或者点击工具栏中的第一个按钮，打开站点管理器，进行选择。连接之后，便可选择目录或文件进行上传下载了。

## 2.2.上传下载

我们不仅可以传输单个文件，还可以传输多个文件甚至整个目录，主要有四种方法。

第一种：选中所要传输的文件或目录，直接拖拽到目的主机中就可以了；

第二种：在选中所要传输的文件或目录后，单击鼠标右键选择【传输】就可以了；

第三种：双击想要传输的文件就可以了；

第四种：将选中的文件或文件夹加入到传输队列中（可以直接拖放也使用鼠标右键），然后在进行传输。使用传输队列最大的好处是可以随时加入或删除传输的文件，并且对于需要经常更新的内容，允许你把它们放到队列中导出，等以后要传输的时候还可以通过导入功能调出之前保存的队列进行文件更新，就是有点复杂了，哈哈。不过要注意的是不同的文件上传到不同目录时，必须先将该目录打开之后再添加到要传的文件到队列之中。

# 3.其它功能及设置

## 3.1.站点导入

站点导入就是将之前版本的站点信息或其它FTP软件的站点信息导入进来，而不需要再进行重复的设置，这给广大的用户节省了时间，也减少了麻烦。通过菜单【站点】—>【导入】及【导出】我们就可以进行站点导入、导出操作了。

![这里写图片描述](D:\MyNote\images\20180828113816134.png)

FileZilla站点导入(只支持XML格式文件的导入)

FileZilla站点导出(支持管理器数据、设置数据及队列的导出)
![这里写图片描述](D:\MyNote\images\2018082811383195.png)

## 3.2.队列管理

队列管理就是对所传输的文件及目录进行的一些功能设置，包括队列的保存，载入、清除、恢复和传输等，可以说是比较重要的功能。FileZilla的队列功能比较简单，其中队列的保存及载入功能，可以通过菜单【文件】—>【导入】及【导出】来实现，就是麻烦了一些。

![这里写图片描述](D:\MyNote\images\20180828113842666.png)

​															FileZilla队列导出画面

## 3.3.文件夹内容比较

文件夹内容比较就是对两台不同的机器上的相关目录下的内容进行比较，然后把不相同的内容显示出来，这对于保持版本一致性非常有用。通过菜单【查看】—>【比较目录】我们就可以比较出两个目录下不同的内容。

![这里写图片描述](D:\MyNote\images\20180828113853252.png)

​																FileZilla文件目录比较功能

## 3.4.断点续传

断点续传功能可以说几乎是每个FTP软件必备的功能，也可以说是最基本和重要的功能了。它的实质就是当传输文件过程中，由于各种原因使得传输过程发生异常，产生中断，在系统恢复正常后，FTP软件能够在之前发生中断的位置继续传输文件，直到数据传送完毕为止。通过菜单【编辑】—>【设置】的对已存在文件的操作选项我们就可以设置断点续传。

![这里写图片描述](D:\MyNote\images\20180828113905797.png)

​																FileZilla断点续传设置画面

## 3.5.速度限制

速度限制功能就是当网络比较拥挤或FTP站点有特定要求的时候，对文件的上传和下载的速度进行具体的限制。通过菜单【编辑】—>【设置】的对已存在文件的操作选项，我们就可以设置速度限制了。

![这里写图片描述](D:\MyNote\images\20180828113925567.png)

​															FileZilla速度限制画面（0表示没有限制）

## 3.6.文件过滤器

过滤器功能简单的说就是将符合条件的待传输文件及目录进行传输，我们可以通过设置扩展名、优先级类表等来控制文件的传输。通过菜单【查看】—>【文件过滤器】我们就可以对传输的文件进行选择。（但是感觉好像不起作用）

![这里写图片描述](D:\MyNote\images\20180828113943366.png)

​																	FileZilla过滤器画面

## 3.7.快速拖放

快速拖放功能是大多数FTP软件都支持的功能，它主要就是为了用户操作的方便。

## 3.8.多语言支持

FileZilla3.0标准版支持包括中文简体在内的多语言界面。通过菜单【编辑】—>【设置】的语言选项，我们就可以设置使用的语言。

![这里写图片描述](D:\MyNote\images\20180828113953977.png)

​																	FileZilla语言设置画面

## 3.9.备份恢复功能

备份恢复功能是针对FTP软件的设置、站点列表等信息内容的备份及恢复。通过菜单【文件】—>【导入】及【导出】功能我们就可以进行信息的备份和恢复。

## 3.10.文件关联

许多用户在使用FTP软件传输文件的时候，突然发现了一些错误想要修改，但是如果要在调用相关的软件打开，又比较麻烦，所以很多FTP软件就通过文件关联来让用户直接调用相关软件打开要修改的文件，方便了用户的操作。通过菜单【编辑】—>【设置】的正在编辑文件选项，我们就可以设置关联程序。

![这里写图片描述](D:\MyNote\images\705.png)

​																			FileZilla文件关联画面

## 3.11.防掉线

所谓防掉线或者说反空闲、闲置保护功能就是让计算机在空闲状态下每隔一段时间向FTP服务器发送一段特定信息，以便让FTP服务器知道自己还是活动的，从而并且FTP服务器断开对自己的连接。通过菜单【编辑】—>【设置】的FTP选项，我们就可以设置相关的参数。

![这里写图片描述](D:\MyNote\images\706.png)

​																	FileZilla反空闲设置画面

## 3.12.远程管理

远程管理简单的说就是在远程FTP服务器上也可以自由的新建、删除、打开文件或目录等操作。这都是方便性的体现。

## 3.13分组管理

分组管理就是将多个不同的FTP服务器放在同一个组（就相当于目录）中，这样可以更加便于用户的管理。在新建站点的时候，我们就可以先建组，然后再建立新的站点保存在组中。

![这里写图片描述](D:\MyNote\images\702.png)

​															FileZilla组管理画面

## 3.14.文件存在处理

文件存在处理就是当传输文件过程中，如果遇到相同文件名的文件怎么处理?FileZilla共提供了七种方。通过菜单【传输】—>【对已存在文件的默认操作】我们就可以进行相关的设置。

![这里写图片描述](D:\MyNote\images\701.png)

​														FileZilla文件存在处理