# 1.安装环境

## 1.1.安装VMVare

### 1.1.1.下载
1.进入vmvare官网http://www.vmvare.com/，点击左侧导航栏中的下载，再点击图中标记的Workstation Pro，如下图所示。![img](D:\MyNote\images\20180527104549862.png)  

2.根据操作系统选择合适的产品，在这里以Windows系统为例，点击转至下载，如下图所示。  ![img](D:\MyNote\images\20180527105003783.png) 

3.在1处可以选择版本，默认为最新版本。选择好版本后点击立即下载，下载速度很慢的话，建议科学上网。 

 ![img](D:\MyNote\images\20180527105133923.png)

### 1.1.2.安装
1.打开.exe文件， 即可开始安装。

 ![img](D:\MyNote\images\20180527111921280.png)

2.安装位置默认在C盘下，在这里我选择安装在F盘，安装路径尽量不要有中文。

 ![img](D:\MyNote\images\20180527111956198.png)

3.等待安装就好了。

 ![img](D:\MyNote\images\20180527112108236.png)

4.安装成功后，第一次运行程序会要求输入密钥，这个可以自己百度，下面分享我搜集的密钥

```tex
CG54H-D8D0H-H8DHY-C6X7X-N2KG6

ZC3WK-AFXEK-488JP-A7MQX-XL8YF

AC5XK-0ZD4H-088HP-9NQZV-ZG2R4

ZC5XK-A6E0M-080XQ-04ZZG-YF08D

ZY5H0-D3Y8K-M89EZ-AYPEG-MYUA8

FF590-2DX83-M81LZ-XDM7E-MKUT4

FF31K-AHZD1-H8ETZ-8WWEZ-WUUVA

CV7T2-6WY5Q-48EWP-ZXY7X-QGUWD

AALYG-20HVE-WHQ13-67MUP-XVMF3
```



​										 ![img](D:\MyNote\images\20180527112552321.png)

5.输入密钥后，如果成功的话将出现如下界面。

​										 ![img](D:\MyNote\images\20180527112720289.png) 

 ![img](D:\MyNote\images\20180527112728386.png)



## 1.2.安装VitralBox

### 1.2.1.下载

VirtualBox下载地址：https://www.virtualbox.org/wiki/Downloads

当前版本：[VirtualBox](https://www.virtualbox.org/wiki/VirtualBox) 6.0.4

支持平台：windows、OS X、Linux、Solaris 

![1572699086727](D:\MyNote\images\1572699086727.png)

### 1.2.2.安装

1. 下载Windows下安装包
2. 启动安装程序

 ![img](D:\MyNote\images\13526392-efce7df98e6fffaf.png)

3.选择安装位置后继续

![img](D:\MyNote\images\13526392-b49fd7aeddcafd9a.png)

4.快捷方式及文件关联

![img](D:\MyNote\images\13526392-882ecc1efce4c633.png)

5.立即安装

![img](D:\MyNote\images\13526392-27941504399477ef.png)

6.开始安装

![img](D:\MyNote\images\13526392-73da5f6fcb9acf69.png)

7.勾选始终信任软件安装

![img](D:\MyNote\images\13526392-51dd4069c40b7346.png)

8.完成安装

![img](D:\MyNote\images\13526392-efce7df98e6fffaf.png)

9.启动界面

![img](D:\MyNote\images\13526392-7acfd57a20da26c2.png)

## 1.3.在vmvare安装centos

**1.软硬件准备**

软件：推荐使用VMwear，我用的是VMwear 12

镜像：CentOS7 ,如果没有镜像可以在官网下载 ：http://isoredirect.centos.org/centos/7/isos/x86_64/CentOS-7-x86_64-DVD-1804.iso

![img](D:\MyNote\images\70.png)

硬件：因为是在宿主机上运行虚拟化软件安装centos，所以对宿主机的配置有一定的要求。最起码I5CPU双核、硬盘500G、内存4G以上。

![img](D:\MyNote\images\20180711223715242.png)

**2.虚拟机准备**

1.打开VMwear选择新建虚拟机

![img](D:\MyNote\images\20180711223726365.png)

2.典型安装与自定义安装

典型安装：VMwear会将主流的配置应用在虚拟机的操作系统上，对于新手来很友好。

自定义安装：自定义安装可以针对性的把一些资源加强，把不需要的资源移除。避免资源的浪费。

这里我选择自定义安装。

![img](D:\MyNote\images\20180711223827626.png)

3.虚拟机兼容性选择

这里要注意兼容性，如果是VMwear12创建的虚拟机复制到VM11、10或者更低的版本会出现一不兼容的现象。如果是用VMwear10创建的虚拟机在VMwear12中打开则不会出现兼容性问题。

![img](D:\MyNote\images\2018071122384165311.png)

4.选择稍后安装操作系统

![img](D:\MyNote\images\20180711223854551.png)

5.操作系统的选择

这里选择之后安装的操作系统，正确的选择会让vm tools更好的兼容。这里选择linux下的CentOS

![img](D:\MyNote\images\20180711223907671.png)

6.虚拟机位置与命名

虚拟机名称就是一个名字，在虚拟机多的时候方便自己找到。

VMwear的默认位置是在C盘下，我这里改成F盘。

![img](D:\MyNote\images\20180711223917420.png)

7.处理器与内存的分配

处理器分配要根据自己的实际需求来分配。在使用过程中CPU不够的话是可以再增加的。这次只做安装CentOS演示，所以处理器与核心都选1.

![img](D:\MyNote\images\20180711223929865.png)

内存也是要根据实际的需求分配。我的宿主机内存是8G所以我给虚拟机分配2G内存。

![img](D:\MyNote\images\20180711223943268.png)

8.网络连接类型的选择，网络连接类型一共有桥接、NAT、仅主机和不联网四种。

桥接：选择桥接模式的话虚拟机和宿主机在网络上就是平级的关系，相当于连接在同一交换机上。

NAT：NAT模式就是虚拟机要联网得先通过宿主机才能和外面进行通信。

仅主机：虚拟机与宿主机直接连起来

桥接与NAT模式访问互联网过程，如下图所示

![img](D:\MyNote\images\20180711224004659.png) 

桥接与NAT区别

这里选择桥接模式

![img](D:\MyNote\images\20180711224016785.png)

9.其余两项按虚拟机默认选项即可

![img](D:\MyNote\images\20180711224042387.png)

10.磁盘容量

磁盘容量暂时分配100G即可后期可以随时增加，不要勾选立即分配所有磁盘，否则虚拟机会将100G直接分配给CentOS，会导致宿主机所剩硬盘容量减少。

勾选将虚拟磁盘拆分成多个文件，这样可以使虚拟机方便用储存设备拷贝复制。

![img](D:\MyNote\images\20180711224059391.png)

11.磁盘名称，默认即可

![img](D:\MyNote\images\20180711224115667.png)

12.取消不需要的硬件

点击自定义硬件

![img](D:\MyNote\images\2018071122413290.png)

选择声卡、打印机等不需要的硬件然后移除。

![img](D:\MyNote\images\20180711224147231.png)

13.点击完成，已经创建好虚拟机。

![img](D:\MyNote\images\20180711224200707.png)

**3.安装CentOS**

1.连接光盘

右击刚创建的虚拟机，选择设置

![img](D:\MyNote\images\20180711224217850.png)

先选择CD/DVD，再选择使用ISO映像文件，最后选择浏览找到下载好的镜像文件。启动时连接一定要勾选上后确定。

![img](D:\MyNote\images\20180711224233121.png)

2.开启虚拟机

![img](D:\MyNote\images\20180711224302639.png)

3.安装操作系统

开启虚拟机后会出现以下界面

1. Install CentOS 7 安装CentOS 7
2. Test this media & install CentOS 7 测试安装文件并安装CentOS 7
3. Troubleshooting 修复故障

选择第一项，安装直接CentOS 7，回车，进入下面的界面

![img](D:\MyNote\images\20180711224323926.png)

选择安装过程中使用的语言，这里选择英文、键盘选择美式键盘。点击Continue

![img](D:\MyNote\images\2018071122433632.png)

首先设置时间

![img](D:\MyNote\images\2018071122434772.png)

时区选择上海，查看时间是否正确。然后点击Done

![img](D:\MyNote\images\20180711224410105.png)

选择需要安装的软件

![img](D:\MyNote\images\20180711224421911.png)

选择 Server with Gui，然后点击Done

![img](D:\MyNote\images\20180711224438720.png)

选择安装位置，在这里可以进行磁盘划分。

![img](D:\MyNote\images\20180711224452307.png)

选择i wil configure partitioning（我将会配置分区），然后点击done

![img](D:\MyNote\images\20180711224505907.png)

如下图所示，点击加号，选择/boot，给boot分区分200M。最后点击Add

![img](D:\MyNote\images\20180711224522794.png)

然后以同样的办法给其他三个区分配好空间后点击Done

![img](D:\MyNote\images\20180711224533382.png)

然后会弹出摘要信息，点击AcceptChanges(接受更改)

![img](D:\MyNote\images\20180711224549412.png)

设置主机名与网卡信息

![img](D:\MyNote\images\20180711224603320.png)

首先要打开网卡，然后查看是否能获取到IP地址(我这里是桥接)，再更改主机名后点击Done。

![img](D:\MyNote\images\20180711224618785.png)

最后选择Begin Installation(开始安装)

![img](D:\MyNote\images\2018071122463197.png)

设置root密码

![img](D:\MyNote\images\2018071122464660.png)

设置root密码后点击Done

![img](D:\MyNote\images\20180711224658899.png)

点击USER CREATION 创建管理员用户

![img](D:\MyNote\images\20180711224711277.png)

输入用户名密码后点击Done

![img](D:\MyNote\images\2018071122472498.png)

等待系统安装完毕重启系统即可

![img](D:\MyNote\images\20180711224741348.png)

 

# 2.常用命令

 ## 2.1.终端

问题：在目前的桌面系统中，如果需要关机可以通过“系统”“关机”进行关机，那么后期服务器都是命令行模式的，届时这种方式将不好用，那会要怎么关机呢？

![img](D:\MyNote\images\clip_image002.jpg)

答：可以通过命令行方式进行关机。命令的输入需要在**终端**中进行输入。

所谓终端，其实类似于windows下cmd命令行模式。在终端中可以输入需要执行的一些指令，同样可以通过终端进行关机（注意：以后在工作中很少会去使用关机命令，会使用重启比较多）。

终端的形式：

![img](D:\MyNote\images\clip_image003.png)

终端组成部分：

![img](D:\MyNote\images\clip_image005.jpg)

**如何使用终端命令进行关机？**

在Linux中关机命令 有以下几个：shutdown -h now（正常关机）、halt（关闭内存）、init 0

## 2.2.在VMware备份系统

在vm中备份方式有2种：快照、克隆。

**快照**：又称还原点，就是保存在拍快照时候的系统的状态（包含了所有的内容），在后期的时候随时可以恢复。【**侧重在于短期备份，需要频繁备份的时候可以使用快照，做快照的时候虚拟的操作系统一般处于开启状态**】

①在菜单“虚拟机”-“快照”-“拍摄快照”

![img](D:\MyNote\images\clip_image006.png)

输入相关信息，点击拍摄快照

②搞事情

![img](D:\MyNote\images\clip_image007.png)

③使用快照恢复搞事情之前的状态

路径：虚拟机 – 快照 – 快照管理器

![img](D:\MyNote\images\clip_image009.jpg)

恢复好之后的状态：

![img](D:\MyNote\images\clip_image010.png)

**克隆**：就是复制的意思。【**侧重长期备份，做克隆的时候是必须得关闭**】

路径：先关机 – 右键需要克隆的虚拟机 – 管理 – 克隆

![img](D:\MyNote\images\clip_image011.png)

![img](D:\MyNote\images\clip_image012.png)

 

![img](D:\MyNote\images\clip_image013.png)

上述的名称和位置与之前新建虚拟机的时候是一样的含义。

等待克隆完成

![img](D:\MyNote\images\clip_image014.png)

**克隆好的服务器相关密码帐号等信息与被克隆的系统一致。**

# 3.Linux系统的文件

## 3.1文件与文件夹

什么是文件？

一般都是一个独立的东西，可以通过一些特定的工具进行打开，并且其中不能在包含除了文字以外的东西。例如：

![img](D:\MyNote\images\clip_image015.png)

 

什么是文件夹？

可以在其中包含其他文件的东西。

![img](D:\MyNote\images\clip_image016.png)

 

为什么先讲文件？

1:日常运维工作中，有近一半以上的工作内容 精力 其实都是对文件的操作。

2: Linux 本身也是一个基于文件形式表示的操作系统。

**Linux一切皆文件。**

①在windows是文件的，在Linux下同样也是文件；

②在windows不是文件的，在Linux下也是以文件的形式存储的；

日常学习中和日常工作中，对于文件的操作的都有哪些种类？

**创建文件、编辑文件、保存文件、关闭文件、重命名文件、删除文件、恢复文件。**

## 3.2.目录结构

![img](D:\MyNote\images\clip_image018.jpg)

目录结构：

Bin：全称binary，含义是二进制。该目录中存储的都是一些二进制文件，文件都是可以被运行的。

Dev：该目录中主要存放的是外接设备，例如盘、其他的光盘等。在其中的外接设备是不能直接被使用的，需要**挂载（类似windows下的分配盘符）**。

Etc：该目录主要存储一些配置文件。

Home：表示“家”，表示除了root用户以外其他用户的家目录，类似于windows下的User/用户目录。

Proc：process，表示进程，该目录中存储的是Linux运行时候的进程。

Root：该目录是root用户自己的家目录。

Sbin：全称super binary，该目录也是存储一些可以被执行的二进制文件，但是必须得有super权限的用户才能执行。

Tmp：表示“临时”的，当系统运行时候产生的临时文件会在这个目录存着。

Usr：存放的是用户自己安装的软件。类似于windows下的program files。

Var：存放的程序/系统的日志文件的目录。

Mnt：当外接设备需要挂载的时候，就需要挂载到mnt目录下。

# 4.基础指令

## 4.1指令与选项

什么是Linux的指令？

指在Linux终端（命令行）中输入的内容就称之为指令。

​         ![img](D:\MyNote\images\clip_image00121.png)  

一个完整的指令的标准格式：Linux通用的格式

**指令主体（空格） [**选项]**（空格） [操作对象]**

一个指令可以包含多个选项

操作对象也可以是多个

例如：需要让张三同学帮忙去楼下小卖铺买一瓶农夫山泉水和清风餐巾纸，在这个指令中“买东西”是指令的主体，买的水和餐巾纸是操作的对象，农夫山泉、清风是操作的选项。

## 4.2.ls指令

含义：ls （list）

**用法1**：#ls

含义：列出当前工作目录下的所有文件/文件夹的名称

![img](D:\MyNote\images\clip_image003.jpg)

 

**用法2**：#ls  **路径**

含义：列出指定路径下的所有文件/文件夹的名称

关于路径（重要）：

路径可以分为两种：相对路径、绝对路径。

相对路径：相对首先得有一个参照物（一般就是当前的工作路径）；

 相对路径的写法：在相对路径中通常会用到2个符号“./”【表示当前目录下】、“../”【上一级目录下】。

绝对路径：绝对路径不需要参照物，直接从根“/”开始寻找对应路径；

​         ![img](D:\MyNote\images\clip_image0031.png)  

**用法3**：#ls **选项** **路径**

含义：在列出指定路径下的文件/文件夹的名称，并以指定的格式进行显示。

常见的语法：

​     \#ls -l 路径

​     \#ls -la 路径

选项解释： 

​     **-l**：表示list，表示以详细列表的形式进行展示

​     **-a**：表示显示所有的文件/文件夹（包含了隐藏文件/文件夹）

![img](D:\MyNote\images\clip_image005.png)

上述列表中的第一列字符表示文档的类型，**其中“**-”表示改行对应的文档类型为文件，“d”表示文档类型为文件夹。

![img](D:\MyNote\images\clip_image0106.png)

**在Linux**中隐藏文档一般都是以“.”开头。

**用法4**：#ls -lh **路径**

含义：列出指定路径下的所有文件/文件夹的名称，以列表的形式并且在显示文档大小的时候以**可读性较高的形式显示**

参数含义：

![img](D:\MyNote\images\clip_image6007.png)

## 4.3.pwd指令

**用法：#pwd**      **（print working directory**，打印当前工作目录）

![img](D:\MyNote\images\clip_image008.png)

## 4.4.cd指令

命令：#cd     （change directory，改变目录）

作用：用于切换当前的工作目录的

**语法：#cd** **路径**

案例：当前在“/”下，需要使用绝对路径切换到/usr/local。

![img](D:\MyNote\images\clip_image009.png)

 

案例：当前在/usr/local下，需要使用相对路径切换目录到home目录下的Linux123用户家目录中去。

![img](D:\MyNote\images\clip_image0110.png)

 

补充：

在Linux中有一个特殊的符号“~”，表示当前用户的家目录。

切换的方式：#cd ~

![img](D:\MyNote\images\clip_image0111.png)

## 4.5.mkdir指令

指令：mkdir  （make directory，创建目录）

语法1：**#mkdir** **路径** **【路径，可以是文件夹名称也可以是包含名称的一个完整路径】**

案例：在当前路径下创建出目录“yunweihenniux”

​         ![img](D:\MyNote\images\clip_image00131.png)  

注意：ls列出的结果颜色说明，**其中蓝色的名称表示文件夹**，黑色的表示文件，**绿色的其权限为拥有所有权限**。

案例：在指定路径下创建出一个文件夹“yunweihenniux”

![img](D:\MyNote\images\clip_image002.png)

 

语法2：**#mkdir -p** **路径**

含义：**当一次性创建多层不存在的目录的时候**，添加-p参数，否则会报错

![img](D:\MyNote\images\clip_image004.jpg)

 

语法3：**#mkdir** **路径1** **路径2** **路径3 ….**  【表示一次性创建多个目录】

![img](D:\MyNote\images\clip_image006.jpg)

## 4.6.touch指令

指令：touch  

作用：创建文件

语法：**#touch** **文件路径**   【路径可以是直接的文件名也可以是路径】

案例：使用touch来在当前路径下创建一个文件，命名为Linux.txt

![img](D:\MyNote\images\clip_image0021.jpg)

案例：使用touch来同时创建多个文件

![img](D:\MyNote\images\clip_image0041.jpg)

案例：使用touch来在“Linux123”用户的家目录中创建文件，Linux.txt

![img](D:\MyNote\images\clip_image0051.png)

## 4.7.cp指令

指令：cp     （copy，复制）

作用：复制文件/文件夹到指定的位置

语法：**#cp** **被复制的文档路径** **文档被复制到的路径**

案例：使用cp命令来复制一个文件

![img](D:\MyNote\images\clip_image0012.png)

**注意：Linux在复制过程中是可以重新对新位置的文件进行重命名的，但是如果不是必须的需要，则建议保持前后名称一致。**

案例：使用cp命令来复制一个文件夹

**注意：当使用cp命令进行文件夹复制操作的时候需要添加选项“-r”【-r**表示递归复制】，否则目录将被忽略

![img](D:\MyNote\images\clip_image0032.jpg)

## 4.8.mv指令

指令：mv  （move，移动，剪切）

作用：移动文档到新的位置

语法：**#mv** **需要移动的文档路径** **需要保存的位置路径**

案例：使用mv命令移动一个文件

![img](D:\MyNote\images\clip_image0081.png)

案例：使用mv命令移动一个文件夹

![img](D:\MyNote\images\clip_image0082.png)

补充：在Linux中重命名的命令也是mv，语法和移动语法一样。

![img](D:\MyNote\images\clip_image0083.png)

## 4.9.rm指令

指令：rm （remove，移除、删除）

作用：移除/删除文档

语法：#rm 选项 需要移除的文档路径

选项：

​     -f：force，强制删除，不提示是否删除

​     -r：表示递归

案例：删除一个文件

![img](D:\MyNote\images\clip_image0091.png)

在删除的时候如果不带选项，会提示是否删除，如果需要确认则输入“y/yes”，否则输入“n/no”按下回车。

**注意：如果在删除的时候不想频繁的确认，则可以在指令中添加选项“-f**”，表示force（强制）。

![img](D:\MyNote\images\clip_image0093.jpg)

案例：删除一个文件夹

​         ![img](D:\MyNote\images\clip_image0901.png)  

**注意：删除一个目录的时候需要做递归删除，并且一般也不需要进行删除确认询问，所以移除目录的时候一般需要使用-rf**选项。

案例：删除多个文档

​         ![img](D:\MyNote\images\clip_image9001.png)  

案例：要删除一个目录下有公共特性的文档，例如都以Linux开头

​         ![img](D:\MyNote\images\clip_image0092.jpg)  

其中*****称之为通配符，意思表示任意的字符，Linux\*，则表示只要文件以Linux开头，后续字符则不管。

## 4.10.vim指令

指令：vim  （vim是一款文本编辑器）

语法：**#vim** **文件的路径**

作用：打开一个文件（可以不存在，也可以存在）

案例：使用vim来打开文件

退出打开的文件：在没有按下其他命令的时候，按下shift+英文冒号，输入q，按下回车即可

![img](D:\MyNote\images\clip_image00101.png)

编辑后，按ctrl+alt+w，然后按shift+:，输入q!不保存然后退出；输入wq时保存并退出。

## 4.11.输出重定向

**一般命令的输出都会显示在终端中，有些时候需要将一些命令的执行结果想要保存到文件中进行后续的分析**统计，则这时候需要使用到的输出重定向技术。

\>：覆盖输出，会覆盖掉原先的文件内容

\>>：追加输出，不会覆盖原始文件内容，会在原始内容末尾继续添加

**语法：#**正常执行的指令 > / >> **文件的路径**

注意：文件可以不存在，不存在则新建

案例：使用覆盖重定向，保存ls -la 的执行结果，保存到当前目录下的ls.txt

![img](D:\MyNote\images\clip_image01201.png)

案例：使用追加重定向，保存ls -la的执行结果到ls.txt中

![img](D:\MyNote\images\clip_image00122.png)

## 4.12.cat指令

**作用1：cat有直接打开一个文件的功能。**

**语法1：#cat** **文件的路径**

![img](D:\MyNote\images\clip_image121001.png)

**作用2：cat还可以对文件进行合并**

**语法2：#cat** **待合并的文件路径1** **待合并的文件路径2 ….** **文件路径n >** **合并之后的文件路径**

例如，合并3个文件，并存到一个文件中【配合输出重定向使用】

![img](D:\MyNote\images\clip_image00123.jpg)

# 5.进阶指令

## 5.1.df指令

作用：查看磁盘的空间

语法：#df -h      -h表示以可读性较高的形式展示大小

![img](D:\MyNote\images\wps12.jpg)

## 5.2.free指令

作用：查看内存使用情况

语法：#free -m -m表示以mb为单位查看

![img](D:\MyNote\images\wps2.jpg) 

剩余的真实可以用的内存为1665mb。

Swap：用于临时内存，当系统真实内存不够用的时候可以临时使用磁盘空间来充当内存。

## 5.3.head指令

作用：查看一个文件的前n行，如果不指定n，则默认显示前10行。
语法：#head -n 文件路径   【n表示数字】

![img](D:\MyNote\images\wps3.jpg)

## 5.4.tail指令

作用1：查看一个文件的未n行，如果n不指定默认显示后10行
语法：#tail -n 文件的路径    n同样表示数字

![img](D:\MyNote\images\wps5.jpg)

作用2：可以通过tail指令来查看一个文件的动态变化内容【变化的内容不能是用户手动增加的】
语法：#tail -f 文件路径
该命令一般用于查看系统的日志比较多。

意思就是用这个查看系统日志，当日志在增加时，终端这里也会同步增加。但是自己建个文件，然后添加内容是不行的。

## 5.5.less指令

作用：查看文件，以较少的内容进行输出，按下辅助功能键（数字+回车、空格键+上下方向键）查看更多
语法：#less 需要查看的文件路径

![img](D:\MyNote\images\wps6.jpg) 

在退出的只需要按下q键即可。

## 5.6.wc指令

作用：统计文件内容信息（包含行数、单词数、字节数）
语法：#wc -lwc 需要统计的文件路径
	-l：表示lines，行数
	-w：表示words，单词数   依照空格来判断单词数量
	-c：表示bytes，字节数

![img](D:\MyNote\images\wps7.jpg) 

## 5.7.date指令（重点）

作用：表示操作时间日期（读取、设置）
语法1：#date			输出的形式：2018年 3月 24日 星期六 15:54:28
语法2：#date  +%F	（等价于#date  “+%Y-%m-%d” ）	输出形式：2018-03-24
语法3：#date  “+%F %T”    引号表示让“年月日与时分秒”成为一个不可分割的整体
等价操作#date  “+%Y-%m-%d %H:%M:%S”
输出的形式：2018-03-24 16:01:00

语法4：获取之前或者之后的某个时间（备份）
#date  -d  “-1 day”  “+%Y-%m-%d %H:%M:%S”

符号的可选值：+（之后） 或者 - （之前）
单位的可选值：day（天）、month（月份）、year（年）

```tex
%F：表示完整的年月日
%T：表示完整的时分秒
%Y：表示四位年份
%m：表示两位月份（带前导0）
%d：表示日期（带前导0）
%H：表示小时（带前导0）
%M：表示分钟（带前导0）
%S：表示秒数（带前导0）
```

## 5.8.cal指令

作用：用来操作日历的
语法1：#cal	  等价于 #cal  -1		直接输出当前月份的日历
语法2：#cal  -3			表示输出上一个月+本月+下个月的日历
语法3：#cal  -y 年份  		表示输出某一个年份的日历

## 5.9.clear/ctrl+L指令

作用：清除终端中已经存在的命令和结果（信息）。
语法：clear或者快捷键：ctrl + L

需要注意的是，该命令并不是真的清除了之前的信息，而是把之前的信息的隐藏到了最上面，通过滚动条继续查看以前的信息。

## 5.10.管道（重要）

管道符：|
作用：管道一般可以用于“过滤”，“特殊”，“扩展处理”。
语法：管道不能单独使用，必须需要配合前面所讲的一些指令来一起使用，其作用主要是辅助作用。

①过滤案例（100%使用）：需要通过管道查询出根目录下包含“y”字母的文档名称。

```tex
#ls / | grep y
针对上面这个命令说明：
①以管道作为分界线，前面的命令有个输出，后面需要先输入，然后再过滤，最后再输出，通俗的讲就是管道前面的输出就是后面指令的输入；

②grep指令：主要用于过滤
```



②特殊用法案例：通过管道的操作方法来实现less的等价效果（了解）
之前通过less查看一个文件，可以#less 路径
现在通过管道还可以这么：#cat 路径|less

③扩展处理：请使用学过的命令，来统计某个目录下的文档的总个数？
答：#ls / | wc -l

# 6.高级指令

## 6.1.hostname指令

作用：操作服务器的主机名（读取、设置）
语法1：#hostname			含义：表示输出完整的主机名
语法2：#hostname  -f			含义：表示输出当前主机名中的FQDN（全限定域名）

![img](D:\MyNote\images\wps8.jpg) 

 

## 6.2.id指令

作用：查看一个用户的一些基本信息（包含用户id，用户组id，附加组id…），该指令如果不指定用户则默认当前用户。

语法1：#id		默认显示当前执行该命令的用户的基本信息

语法2：#id 用户名		显示指定用户的基本信息

![img](D:\MyNote\images\wps9.jpg) 

验证上述信息是否正确？

验证用户信息：通过文件/etc/passwd

验证用户组信息：通过文件/etc/group

![img](D:\MyNote\images\wps10.jpg)

## 6.3.whoami指令

作用：“我是谁？”显示当前登录的用户名，一般用于shell脚本，用于获取当前操作的用户名方便记录日志。
语法：#whoami

语法：#whoami

![img](file:///C:\Windows\TEMP\ksohtml15440\wps11.jpg) 

## 6.4.ps -ef指令（重点）

指令：ps	
作用：主要是查看服务器的进程信息
选项含义：
	-e：等价于“-A”，表示列出全部的进程
	-f：显示全部的列（显示全字段）

执行结果：

![img](file:///C:\Windows\TEMP\ksohtml15440\wps12.jpg) 

列的含义：

UID：该进程执行的用户id；

PID：进程id；

PPID：该进程的父级进程id，如果一个程序的父级进程找不到，该程序的进程称之为僵尸进程（parent process ID）；

C：Cpu的占用率，其形式是百分数；

STIME：进行的启动时间；

TTY：终端设备，发起该进程的设备识别符号，如果显示“?”则表示该进程并不是由终端设备发起；

TIME：进程的执行时间；

CMD：该进程的名称或者对应的路径；

案例：（100%使用的命令）在ps的结果中过滤出想要查看的进程状态
#ps -ef|grep “进程名称”

![img](D:\MyNote\images\wps13.jpg) 

 

再例如查看火狐浏览器的进程：

![img](D:\MyNote\images\wps14.jpg) 

 

## 6.5.top指令（重点）

作用：查看服务器的进程占的资源（100%使用）
语法：
	进入命令：#top			（动态显示）
	退出命令：按下q键

输出的结果：

![img](file:///C:\Windows\TEMP\ksohtml15440\wps15.jpg) 

表头含义：

PID：进程id；

USER：该进程对应的用户；

PR：优先级；

VIRT：虚拟内存；

RES：常驻内存；

SHR：共享内存；

​	计算一个进程实际使用的内存 = 常驻内存（RES）- 共享内存（SHR）

S：表示进程的状态status（sleeping，其中S表示睡眠，R表示运行）；

%CPU：表示CPU的占用百分比；

%MEM：表示内存的占用百分比；

TIME+：执行的时间；

COMMAND：进程的名称或者路径；

在运行top的时候，可以按下方便的快捷键：
M：表示将结果按照内存（MEM）从高到低进行降序排列；
P：表示将结果按照CPU使用率从高到低进行降序排列；
1：当服务器拥有多个cpu的时候可以使用“1”快捷键来切换是否展示显示各个cpu的详细信息；

## 6.6.du -sh指令
作用：查看目录的真实大小
语法：#du -sh 目录路径
选项含义：
	-s：summaries，只显示汇总的大小
	-h：表示以高可读性的形式进行显示

案例：统计“/root/yunweihenniux”目录的实际大小


案例：统计“/etc”目录实际大小

案例：统计“/root/yunweihenniux”目录的实际大小

![img](D:\MyNote\images\wps21.jpg) 

案例：统计“/etc”目录实际大小

![img](D:\MyNote\images\wps22.jpg) 

## 6.7.find指令
作用：用于查找文件（其参数有55个之多）
语法：#find 路径范围 选项 选项的值
选项：
	-name：按照文档名称进行搜索（支持模糊搜索）
	-type：按照文档的类型进行搜索
		文档类型：“-”表示文件（在使用find的时候需要用f来替换），“d”表示文件夹

案例：使用find来搜索httpd.conf
#find / -name httpd.conf

案例：搜索etc目录下所有的conf后缀文件
#find /etc -name *.conf

案例：使用find来搜索/etc/sane.d/目录下所有的文件
#find /etc/sane.d/ -type f

案例：使用find来搜索/etc/目录下所有的文件夹
#find /etc -type d

![img](file:///C:\Windows\TEMP\ksohtml12848\wps6.jpg) 

## 6.8.service指令（重点）

作用：用于控制一些软件的服务启动/停止/重启
语法：#service 服务名 start/stop/restart

例如：需要启动本机安装的Apache（网站服务器软件），其服务名httpd
#service httpd start

通过ps命令来检查httpd服务是否启动：

例如：需要启动本机安装的Apache（网站服务器软件），其服务名httpd

\#service httpd start

![img](D:\MyNote\images\wps17.jpg) 

通过ps命令来检查httpd服务是否启动：

![img](D:\MyNote\images\wps82.jpg)

## 6.9.kill指令（重点）

作用：表示杀死进程		（当遇到僵尸进程或者出于某些原因需要关闭进程的时候）
语法：#kill  进程PID		（语法需要配合ps一起使用）

案例：需要kill掉Apache的进程

![img](D:\MyNote\images\wps39.jpg) 

与kill命令作用相似但是比kill更加好用的杀死进程的命令：killall
语法：#killall 进程名称

![img](D:\MyNote\images\wps120.jpg)

## 6.10.ifconfig指令（重点）

作用：用于操作网卡相关的指令。
简单语法：#ifconfig		（获取网卡信息）

Eth0表示Linux中的一个网卡，eth0是其名称。Lo（loop，本地回还网卡，其ip地址一般都是127.0.0.1）也是一个网卡名称。

![img](D:\MyNote\images\wps11.jpg) 

注意：inet addr就是网卡的ip地址。信息）

![img](D:\MyNote\images\wps124.jpg) 

## 6.11.reboot指令

作用：重新启动计算机		
语法1：#reboot		重启
语法2：#reboot  -w   模拟重启，但是不重启（只写关机与开机的日志信息）但是不重启（只写关机与开机的日志信息）

## 6.12.shutdown指令

作用：关机			（慎用）
语法1：#shutdown -h now	“关机提示”  或者  #shutdown  -h 15:25  “关机提示”
案例：设置Linux系统关机时间在12:00


如果想要取消关机计划的话，则可以按照以下方式去尝试：
①针对于centos7.x之前的版本：ctrl+c
②针对于centos7.x（包含）之后的版本：#shutdown  -c

除了shutdown关机以外，还有以下几个关机命令：
#init 0
#halt

![img](D:\MyNote\images\wps133.jpg) 