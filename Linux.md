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

 1.软硬件准备 

软件：推荐使用VMwear，我用的是VMwear 12

镜像：CentOS7 ,如果没有镜像可以在官网下载 ：http://isoredirect.centos.org/centos/7/isos/x86_64/CentOS-7-x86_64-DVD-1804.iso

![img](D:\MyNote\images\70.png)

硬件：因为是在宿主机上运行虚拟化软件安装centos，所以对宿主机的配置有一定的要求。最起码I5CPU双核、硬盘500G、内存4G以上。

![img](D:\MyNote\images\20180711223715242.png)

 2.虚拟机准备 

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

| 连接方式 | 连接网卡     | 连接本机 | 连接局域网 | 连接公网 |
| -------- | ------------ | -------- | ---------- | -------- |
| 桥接     | 本地真实网卡 | 可以     | 可以       | 可以     |
| NAT      | VMnet8       | 可以     | 不能       | 可以     |
| 仅主机   | VMnet1       | 可以     | 不能       | 不能     |

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

 3.安装CentOS 

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

 

# 2.常用操作

 ## 2.1.终端

问题：在目前的桌面系统中，如果需要关机可以通过“系统”“关机”进行关机，那么后期服务器都是命令行模式的，届时这种方式将不好用，那会要怎么关机呢？

![img](D:\MyNote\images\clip_image002.jpg)

答：可以通过命令行方式进行关机。命令的输入需要在 终端 中进行输入。

所谓终端，其实类似于windows下cmd命令行模式。在终端中可以输入需要执行的一些指令，同样可以通过终端进行关机（注意：以后在工作中很少会去使用关机命令，会使用重启比较多）。

终端的形式：

![img](D:\MyNote\images\clip_image003.png)

终端组成部分：

![img](D:\MyNote\images\clip_image005.jpg)

 如何使用终端命令进行关机？ 

在Linux中关机命令 有以下几个：shutdown -h now（正常关机）、halt（关闭内存）、init 0

## 2.2.在VMware备份系统

在vm中备份方式有2种：快照、克隆。

 快照 ：又称还原点，就是保存在拍快照时候的系统的状态（包含了所有的内容），在后期的时候随时可以恢复。【 侧重在于短期备份，需要频繁备份的时候可以使用快照，做快照的时候虚拟的操作系统一般处于开启状态 】

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

 克隆 ：就是复制的意思。【 侧重长期备份，做克隆的时候是必须得关闭 】

路径：先关机 – 右键需要克隆的虚拟机 – 管理 – 克隆

![img](D:\MyNote\images\clip_image011.png)

![img](D:\MyNote\images\clip_image012.png)

 

![img](D:\MyNote\images\clip_image013.png)

上述的名称和位置与之前新建虚拟机的时候是一样的含义。

等待克隆完成

![img](D:\MyNote\images\clip_image014.png)

 克隆好的服务器相关密码帐号等信息与被克隆的系统一致。 

# 3.Linux系统的文件

## 3.1文件与文件夹

**什么是文件？**

一般都是一个独立的东西，可以通过一些特定的工具进行打开，并且其中不能在包含除了文字以外的东西。例如：

![img](D:\MyNote\images\clip_image015.png)

 

**什么是文件夹？**

可以在其中包含其他文件的东西。

![img](D:\MyNote\images\clip_image016.png)

 

为什么先讲文件？

1:日常运维工作中，有近一半以上的工作内容 精力 其实都是对文件的操作。

2: Linux 本身也是一个基于文件形式表示的操作系统。

 Linux一切皆文件。 

①在windows是文件的，在Linux下同样也是文件；

②在windows不是文件的，在Linux下也是以文件的形式存储的；

日常学习中和日常工作中，对于文件的操作的都有哪些种类？

 创建文件、编辑文件、保存文件、关闭文件、重命名文件、删除文件、恢复文件。 

## 3.2.目录结构

![img](D:\MyNote\images\clip_image018.jpg)

目录结构：

Bin：全称binary，含义是二进制。该目录中存储的都是一些二进制文件，文件都是可以被运行的。

Dev：该目录中主要存放的是外接设备，例如盘、其他的光盘等。在其中的外接设备是不能直接被使用的，需要 挂载（类似windows下的分配盘符） 。

Etc：该目录主要存储一些配置文件。

Home：表示“家”，表示除了root用户以外其他用户的家目录，类似于windows下的User/用户目录。

Proc：process，表示进程，该目录中存储的是Linux运行时候的进程。

Root：该目录是root用户自己的家目录。

Sbin：全称super binary，该目录也是存储一些可以被执行的二进制文件，但是必须得有super权限的用户才能执行。

Tmp：表示“临时”的，当系统运行时候产生的临时文件会在这个目录存着。

Usr：存放的是用户自己安装的软件。类似于windows下的program files。

Var：存放的程序/系统的日志文件的目录。

Mnt：当外接设备需要挂载的时候，就需要挂载到mnt目录下。

![1667226855328](D:\MyNote\images\1667226855328.png)

![1667226902205](D:\MyNote\images\1667226902205.png)

![1667226923430](D:\MyNote\images\1667226923430.png)

![1667227100392](D:\MyNote\images\1667227100392.png)

![1667227123349](D:\MyNote\images\1667227123349.png)

# 4.基础指令

## 4.1指令与选项

什么是Linux的指令？

指在Linux终端（命令行）中输入的内容就称之为指令。

​         ![img](D:\MyNote\images\clip_image00121.png)  

一个完整的指令的标准格式：Linux通用的格式

 指令主体（空格） [ 选项] （空格） [操作对象] 

一个指令可以包含多个选项

操作对象也可以是多个

例如：需要让张三同学帮忙去楼下小卖铺买一瓶农夫山泉水和清风餐巾纸，在这个指令中“买东西”是指令的主体，买的水和餐巾纸是操作的对象，农夫山泉、清风是操作的选项。

## 4.2.ls指令

含义：ls （list）

 用法1 ：#ls

含义：列出当前工作目录下的所有文件/文件夹的名称

![img](D:\MyNote\images\clip_image003.jpg)

 

 用法2 ：#ls   路径 

含义：列出指定路径下的所有文件/文件夹的名称

关于路径（重要）：

路径可以分为两种：相对路径、绝对路径。

相对路径：相对首先得有一个参照物（一般就是当前的工作路径）；

 相对路径的写法：在相对路径中通常会用到2个符号“./”【表示当前目录下】、“../”【上一级目录下】。

绝对路径：绝对路径不需要参照物，直接从根“/”开始寻找对应路径；

​         ![img](D:\MyNote\images\clip_image0031.png)  

 用法3 ：#ls  选项   路径 

含义：在列出指定路径下的文件/文件夹的名称，并以指定的格式进行显示。

常见的语法：

​     \#ls -l 路径

​     \#ls -la 路径

选项解释： 

​      -l ：表示list，表示以详细列表的形式进行展示

​      -a ：表示显示所有的文件/文件夹（包含了隐藏文件/文件夹）

![img](D:\MyNote\images\clip_image005.png)

上述列表中的第一列字符表示文档的类型， 其中“ -”表示改行对应的文档类型为文件，“d”表示文档类型为文件夹。

![img](D:\MyNote\images\clip_image0106.png)

 在Linux 中隐藏文档一般都是以“.”开头。

 用法4 ：#ls -lh  路径 

含义：列出指定路径下的所有文件/文件夹的名称，以列表的形式并且在显示文档大小的时候以 可读性较高的形式显示 

参数含义：

![img](D:\MyNote\images\clip_image6007.png)

## 4.3.pwd指令

 用法：#pwd        （print working directory ，打印当前工作目录）

![img](D:\MyNote\images\clip_image008.png)

## 4.4.cd指令

命令：#cd     （change directory，改变目录）

作用：用于切换当前的工作目录的

 语法：#cd   路径 

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

语法1： #mkdir   路径   【路径，可以是文件夹名称也可以是包含名称的一个完整路径】 

案例：在当前路径下创建出目录“yunweihenniux”

​         ![img](D:\MyNote\images\clip_image00131.png)  

注意：ls列出的结果颜色说明， 其中蓝色的名称表示文件夹 ，黑色的表示文件， 绿色的其权限为拥有所有权限 。

案例：在指定路径下创建出一个文件夹“yunweihenniux”

![img](D:\MyNote\images\clip_image002.png)

 

语法2： #mkdir -p   路径 

含义： 当一次性创建多层不存在的目录的时候 ，添加-p参数，否则会报错

![img](D:\MyNote\images\clip_image004.jpg)

语法3： #mkdir   路径1   路径2   路径3 ….   【表示一次性创建多个目录】

![img](D:\MyNote\images\clip_image006.jpg)

## 4.6.touch指令

指令：touch  

作用：创建文件

语法： #touch   文件路径    【路径可以是直接的文件名也可以是路径】

案例：使用touch来在当前路径下创建一个文件，命名为Linux.txt

![img](D:\MyNote\images\clip_image0021.jpg)

案例：使用touch来同时创建多个文件

![img](D:\MyNote\images\clip_image0041.jpg)

案例：使用touch来在“Linux123”用户的家目录中创建文件，Linux.txt

![img](D:\MyNote\images\clip_image0051.png)

## 4.7.cp指令

指令：cp     （copy，复制）

作用：复制文件/文件夹到指定的位置

语法： #cp   被复制的文档路径   文档被复制到的路径 

案例：使用cp命令来复制一个文件

![img](D:\MyNote\images\clip_image0012.png)

 注意：Linux在复制过程中是可以重新对新位置的文件进行重命名的，但是如果不是必须的需要，则建议保持前后名称一致。 

案例：使用cp命令来复制一个文件夹

 注意：当使用cp命令进行文件夹复制操作的时候需要添加选项“-r”【-r 表示递归复制】，否则目录将被忽略

![img](D:\MyNote\images\clip_image0032.jpg)

## 4.8.mv指令

指令：mv  （move，移动，剪切）

作用：移动文档到新的位置

语法： #mv   需要移动的文档路径   需要保存的位置路径 

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

 注意：如果在删除的时候不想频繁的确认，则可以在指令中添加选项“-f ”，表示force（强制）。

![img](D:\MyNote\images\clip_image0093.jpg)

案例：删除一个文件夹

​         ![img](D:\MyNote\images\clip_image0901.png)  

 注意：删除一个目录的时候需要做递归删除，并且一般也不需要进行删除确认询问，所以移除目录的时候一般需要使用-rf 选项。

案例：删除多个文档

​         ![img](D:\MyNote\images\clip_image9001.png)  

案例：要删除一个目录下有公共特性的文档，例如都以Linux开头

​         ![img](D:\MyNote\images\clip_image0092.jpg)  

其中  *称之为通配符，意思表示任意的字符，Linux，则表示只要文件以Linux开头，后续字符则不管。

## 4.10.vim指令

指令：vim  （vim是一款文本编辑器）

语法： #vim   文件的路径 

作用：打开一个文件（可以不存在，也可以存在）

案例：使用vim来打开文件 

编辑：按a编辑文件，在光标后方添加内容；按i编辑文件，在光标前方添加内容；输入wq时保存并退出；

退出：先按esc，再按shift+冒号，输入q，按下回车即可；输入q!不保存并强制退出；

![img](D:\MyNote\images\clip_image00101.png)

## 4.11.输出重定向

 一般命令的输出都会显示在终端中，有些时候需要将一些命令的执行结果想要保存到文件中进行后续的分析 统计，则这时候需要使用到的输出重定向技术。

\>：覆盖输出，会覆盖掉原先的文件内容

\>>：追加输出，不会覆盖原始文件内容，会在原始内容末尾继续添加

 语法：# 正常执行的指令 > / >>  文件的路径 

注意：文件可以不存在，不存在则新建

案例：使用覆盖重定向，保存ls -la 的执行结果，保存到当前目录下的ls.txt

![img](D:\MyNote\images\clip_image01201.png)

案例：使用追加重定向，保存ls -la的执行结果到ls.txt中

![img](D:\MyNote\images\clip_image00122.png)

## 4.12.cat指令

 **作用1**：cat有直接打开一个文件的功能。 

 **语法1：**#cat   文件的路径 

![img](D:\MyNote\images\clip_image121001.png)

 **作用2**：cat还可以对文件进行合并 

 **语法2**：#cat   待合并的文件路径1   待合并的文件路径2 ….   文件路径n >   合并之后的文件路径 

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

Swap：用于临时内存c'j当系统真实内存不够用的时候可以临时使用磁盘空间来充当内存。

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

![img](D:\MyNote\images\qwps14.jpg)

## 6.4.ps -ef指令（重点）

指令：ps	
作用：主要是查看服务器的进程信息
选项含义：
	-e：等价于“-A”，表示列出全部的进程
	-f：显示全部的列（显示全字段）

执行结果：

![img](D:\MyNote\images\qwps15.jpg) 

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

![img](D:\MyNote\images\qwps16.jpg) 

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

![img](D:\MyNote\images\qwps17.jpg)

案例：搜索etc目录下所有的conf后缀文件
#find /etc -name *.conf

![img](D:\MyNote\images\qwps18.jpg)

案例：使用find来搜索/etc/sane.d/目录下所有的文件
#find /etc/sane.d/ -type f

![img](D:\MyNote\images\qwps19.jpg)

案例：使用find来搜索/etc/目录下所有的文件夹
#find /etc -type d

![img](D:\MyNote\images\qwps20.jpg)

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

## 6.13.uptime指令

作用：输出计算机的持续在线时间（计算机从开机到现在运行的时间）
语法：#uptime

![img](D:\MyNote\images\wpsq1.jpg)

## 6.14.uname指令

作用：获取计算机操作系统相关信息
语法1：#uname			获取操作系统的类型
语法2：#uname  -a		all，表示获取全部的系统信息（类型、全部主机名、内核版本、发布时间、开源计划）

![img](D:\MyNote\images\wpqs2.jpg)

## 6.15.netstat -tnlp指令
作用：查看网络连接状态
语法：#netstat -tnlp

选项说明：
	-t：表示只列出tcp协议的连接；
	-n：表示将地址从字母组合转化成ip地址，将协议转化成端口号来显示；
	-l：表示过滤出“state（状态）”列中其值为LISTEN（监听）的连接；
	-p：表示显示发起连接的进程pid和进程名称；

![img](D:\MyNote\images\wpsq3.jpg) 

## 6.16.man指令
作用：manual，手册（包含了Linux中全部命令手册，英文）
语法：#man 命令			（退出按下q键）

案例：通过man命令查询cp指令的用法
#man cp

## 6.17.小技巧

1.在命令行中快速删除光标前/后的同一行所有内容？   前：ctrl + u   后：ctrl + k

# 7.Vim

## 7.1.vi介绍
Vi编辑器是所有Unix及Linux系统下标准的编辑器，类似于windows系统下的notepad（记事本）编辑器，由于在Unix及Linux系统的任何版本，Vi编辑器是完全相同的，因此可以在其他任何介绍vi的地方都能进一步了解它，Vi也是Linux中最基本的文本编辑器，学会它后，我们将在Linux的世界里畅行无阻，尤其是在终端中。

关于vim：vi和vim都是Linux中的编辑器，不同的是，vim比较高级，可以视为vi的升级版本。vi使用于文本编辑，但是vim更适用于coding（写代码的）。

Vim重点是光标的移动，模式切换，删除，查找，替换，复制，粘贴，撤销命令的使用。

## 7.2.vim三种模式（重点）
Vim中存在三种模式（大众的认知）：命令模式、编辑模式（输入模式）、末行模式（尾行模式）。

命令模式：在该模式下是不能对文件直接编辑，可以输入快捷键进行一些操作（删除行，复制行，移动光标，粘贴等等）【打开文件之后默认进入的模式】；
编辑模式：在该模式下可以对文件的内容进行编辑；
末行模式：可以在末行输入命令来对文件进行操作（搜索、替换、保存、退出、撤销、高亮等等）；

Vim的打开文件的方式（4种，要求掌握的就前三种）：
#vim 文件路径					作用：打开指定的文件
#vim  +数字  文件的路径			作用：打开指定的文件，并且将光标移动到指定行
#vim  +/关键词  文件的路径		作用：打开指定的文件，并且高亮显示关键词
#vim 文件路径1 文件路径2 文件路径3   作用：同时打开多个文件

重点：先复制出一个/etc/passwd文件，复制当前家目录下（千万不要在etc下直接修改！！！）

后续一切vim命令都是基于/root/passwd文件进行操作。

![img](D:\MyNote\images\wpsp4.jpg) 

后续一切vim命令都是基于/root/passwd文件进行操作。

退出方式：输入:q按下回车即可

![img](D:\MyNote\images\wpsq5.jpg)

### 7.2.1.命令模式
注意：该模式是打开文件的第一个看到的模式（打开文件即可进入）
#### 7.2.1.1.光标移动
①光标移动到行首
按键：shift + 6 或 ^（T字母上面的6，不要按小键盘的6）

②光标移动到行尾
按键：shift + 4 或 $（R字母的左上角的4，不是小键盘的4）

③光标移动到首行
按键：gg

④光标移动到末行
按键：G

⑤翻屏
向上翻屏：按键ctrl + b   （before）	或 		PgUp
向下翻屏：按键ctrl + f	   （after）		或		PgDn

#### 7.2.1.2.复制操作
①复制光标所在行
按键：yy
粘贴：在想要粘贴的地方按下p键

②以光标所在行为准（包含当前行），向下复制指定的行数
按键：数字yy

③可视化复制
按键：ctrl + v（可视块）或V（可视行）或v（可视），然后按下↑↓←→方向键来选中需要复制的区块，按下y键进行复制，最后按下p键粘贴

#### 7.2.1.3.剪切/删除
①剪切/删除光标所在行
按键：dd			（删除之后下一行上移）
注意：dd严格意义上说是剪切命令，但是如果剪切了不粘贴就是删除的效果。

②剪切/删除光标所在行为准（包含当前行），向下删除/剪切指定的行
按键：数字dd		（删除之后下一行上移）

③剪切/删除光标所在的当前行之后的内容，但是删除之后下一行不上移
按键：D				（删除之后当前行会变成空白行）

④可视化删除
按键：ctrl + v（可视块）或V（可视行）或v（可视），上下左右移动，按下D表示删除选中行，d表示删选中块

#### 7.2.1.4.撤销/恢复
撤销：输入:u （不属于命令模式）  或者   u			（undo）
恢复：ctrl + r			恢复（取消）之前的撤销操作

#### 7.2.1.5.光标移动
①快速将光标移动到指定的行
按键：数字G    

②以当前光标为准向上/向下移动n行
按键：数字↑，数字↓

③以当前光标为准向左/向右移动n字符
按键：数字←，数字→

④末行模式下的快速移动方式：移动到指定的行
按键：输入英文“:”，其后输入行数数字，按下回车

### 7.2.2.模式切换（重点）

![img](D:\MyNote\images\wps1w.jpg)

### 7.2.3.末行模式
进入方式：由命令模式进入，按下“:”或者“/（表示查找）”即可进入
退出方式：
		a. 按下esc
		b. 连按2次esc键
		c. 删除末行全部输入字符

①保存操作（write）
输入：“:w”				保存文件
输入：“:w  路径”		另存为

②退出（quit）
输入：“:q”				退出文件

③保存并退出
输入：“:wq”				保存并且退出

④强制 （!）
输入：“:q!”				表示强制退出，刚才做的修改操作不做保存

⑤调用外部命令（了解）
输入：“:!外部命令”
例如：

![img](D:\MyNote\images\wps8q.jpg)

当外部命令执行结束之后按下任意键回到vim编辑器打开的内容

![img](D:\MyNote\images\wpsw7.jpg)

⑥搜索/查找
输入：“/关键词”
例如：我想在passwd文件中搜索“sbin”关键词

在搜索结果中切换上/下一个结果：N/n		（next）
如果需要取消高亮，则需要输入：“:nohl”【no highlight】

⑦替换
:s/搜索的关键词/新的内容				替换光标所在行的第一处符合条件的内容
:s/搜索的关键词/新的内容/g			替换光标所在行的全部符合条件的内容
:%s/搜索的关键词/新的内容			替换整个文档中每行第一个符合条件的内容
:%s/搜索的关键词/新的内容/g			替换整个文档的符合条件的内容

%表示整个文件
g表示全局（global）

⑧显示行号（临时）
输入：“:set nu”[number]
如果想取消显示，则输入：“:set nonu”

⑨扩展2：使用vim同时打开多个文件，在末行模式下进行切换文件
查看当前已经打开的文件名称：“:fil	es”

在%a的位置有2种显示可能
%a：a=active，表示当前正在打开的文件；
#：表示上一个打开的文件

切换文件的方式：
a. 如果需要指定切换文件的名称，则可以输入：“:open 已经打开的文件名”

b. 可以通过其他命令来切换上一个文件/下一个文件
输入：“:bn”切换到下一个文件（back next）
输入：“:bp”切换到上一个文件（back prev）

### 7.2.4.编辑模式

![img](D:\MyNote\images\awps9.jpg) 

重点看前2个进入方式：i（insert）、a（after）。

退出方式：按下esc键

### 7.2.5.实用功能
#### 7.2.5.1.代码着色

![img](D:\MyNote\images\wpsq10.jpg) 

案例：首先创建简单的c语言程序

如何控制着色显示与否？

显示：“:syntax on”			syn

tax：语法![img](D:\MyNote\images\wps1q1.jpg)

关闭显示：“:syntax off”

#### 7.2.5.2.vim的计算器
当在编辑文件的时候突然需要使用计算器去计算一些公式，则此时需要用计算器，但是需要退出，vim自身集成了一个简易的计算器。

a. 进入编辑模式
b. 按下按键“ctrl + R”，然后输入“=”，此时光标会变到最后一行
c. 输入需要计算的内容，按下回车

![img](D:\MyNote\images\wps12s.jpg) 

### 7.2.6.扩展
#### 7.2.6.1.vim配置*
Vim是一款编辑器，编辑器也是有配置文件的。
Vim配置有三种情况：
	a. 在文件打开的时候在末行模式下输入的配置（临时的）
	b. 个人配置文件（~/.vimrc，如果没有可以自行新建）
	c. 全局配置文件（vim自带，/etc/vimrc）

①新建好个人配置文件之后进入编辑

②在配置文件中进行配置
比如显示行号：set nu

![img](D:\MyNote\images\wps1w8.jpg)

配置好之后vim打开文件就会永远显示行号

#### 7.2.6.2.异常退出
什么是异常退出：在编辑文件之后并没有正常的去wq（保存退出），而是遇到突然关闭终端或者断电的情况，则会显示下面的效果，这个情况称之为异常退出：

![img](D:\MyNote\images\wps19.jpg) 

 

解决办法：将交换文件（在编程过程中产生的临时文件）删除掉即可

\#rm -f .passwd.swp

![img](D:\MyNote\images\wps20.jpg) 

#### 7.2.6.3.别名机制
作用：相当于创建一些属于自己的自定义命令

例如：在windows下有cls命令，在Linux下可能因为没有这个命令而不习惯清屏。现在可以通过别名机制来解决这个问题，可以自己创造出cls命令

别名机制依靠一个别名映射文件：~/.bashrc
#vim  ~/.bashrc

![img](D:\MyNote\images\wqps22.jpg)


注意：如果想新创造的命令生效，必须要重新登录当前用户。

#### 7.2.6.4.退出方式
回顾：之前vim中退出编辑的文件可以使用“:q”或者“:wq”。

除了上面的这个语法之外，vim还支持另外一个保存退出方法“:x”。

说明：
	①“:x”在文件没有修改的情况下，表示直接退出，在文件修改的情况下表示保存并退出；
	②如果文件没有被修改，但是使用wq进行退出的话，则文件的修改时间会被更新；但是如果文件没有被修改，使用x进行退出的话，则文件修改时间不会被更新的；主要是会混淆用户对文件的修改时间的认定。

因此建议以后使用“:x”来进行对文件的保存退出。
但是：不要使用X，不要使用X，不要使用X，X表示对文件进行加密操作。

# 8.Linux自有服务
自有服务，即不需要用户独立去安装的软件的服务，而是当系统安装好之后就可以直接使用的服务（内置）。
## 8.1.运行模式
运行模式也可以称之为运行级别。

在linux中存在一个进程：init （initialize，初始化），进程id是1。
查看进程：#ps -ef|grep init

![img](D:\MyNote\images\wps27.jpg)


该进程存在一个对应的配置文件：inittab（系统运行级别配置文件，位置/etc/inittab）

文件的主要内容：

![img](D:\MyNote\images\wps28.jpg)

根据上述的描述，可以得知，Centos6.5中存在7种运行级别/模式。
0 — 表示关机级别（不要将默认的运行级别设置成这个值）
1 — 单用户模式
2 — 多用户模式，不带NFS（Network File Syetem）
3 — 多用户模式，完全的多用户模式（不带桌面的，纯命令行模式）
4 — 没有被使用的模式（被保留模式）
5 — X11，完整的图形化界面模式
6 — 表示重启级别（不要将默认的运行级别设置成这个值）

与该级别相关的几个命令：
#init 0		表示关机
#init 3		表示切换到不带桌面的模式
#init 5		切换到图形界面
#init 6 		重启电脑
注意：init指令需要超级管理员的权限，普通用户无法执行。

这些命令其实都是调用的init进程，将数字（运行级别）传递给进程，进程去读配置文件执行对应的操作。

①切换到纯命令行模式下（临时切换，重启之后又恢复）
#init 3

![img](D:\MyNote\images\wps29.jpg)

切换之后需要输入用户名和密码，在输入密码的时候没有“*”提示输入，只要自己确认输入的密码没有错误，按下回车即可。

②回到桌面模式
#init 5

③设置模式永久为命令行模式

![img](D:\MyNote\images\wps30.jpg)

将/etc/inittab文件中的initdefault值设置成3，然后重启操作系统。

在linux中存在一个进程：init （initialize，初始化），进程id是1。

查看进程：#ps -ef|grep init

![img](D:\MyNote\images\wps23.jpg) 

该进程存在一个对应的配置文件：inittab（系统运行级别配置文件，位置/etc/inittab）

## 8.2.设置主机名

回顾：

\#hostname

\#hostname -f		FQDN（全限定域名）

①临时设置主机名（立竿见影），需要切换用户使之生效

\#hostname 设置的主机名

![img](D:\MyNote\images\awps1.jpg) 

②永久设置主机名（需要重启）

先找到一个文件

/etc/sysconfig/network		【主机名的配置文件】

![img](D:\MyNote\images\wps2qa.jpg) 

修改其中的HOSTNAME为自己需要设置的永久主机名

![img](D:\MyNote\images\wps3qq.jpg) 

③修改linux服务器的hosts文件，将yunwei指向本地（设置FQDN）

Hosts文件的位置：/etc/hosts

![img](D:\MyNote\images\wpsqz4.jpg) 

问题：不设置FQDN会怎么样？

​	①很多开源服务器软件（例如Apache）则无法启动，或出现报错；

​	②方便记忆，看到主机名对其作用有一个初步判断；

​	③如果不设置则会影响本地的域名的解析（本地访问）；

## 8.3.chkconfig

作用：相当于windows下“安全卫士”、“电脑管家”之类的安全辅助工具提供“开机启动项”的一个管理服务。

在linux下不是所有的软件安装完成之后都有开机启动服务，有的可能需要自己去添加。除此之外还可以查看和删除。

①开机启动服务查询

\#chkconfig --list

![img](D:\MyNote\images\wpsqw5.jpg) 

其中0-6表示各个启动级别

例如：以httpd为例，其3级别为关闭（off），则表示其在3启动形式下默认开机不启动

5对应的也是关闭，则表示其在桌面环境下也是开机不启动。

再例如：kdump服务，在2，3，4，5的级别下默认开机启动的，其他级别下默认开机不启动

②删除服务

\#chkconfig --del 服务名

例如删除httpd服务

![img](D:\MyNote\images\wps6qw.jpg) 

③添加开机启动服务

\#chkconfig --add 服务名			【必须要保证服务正常运行，才可以添加】

![img](D:\MyNote\images\qwwps7.jpg) 

④设置服务在某个级别下开机启动/不启动【重点命令】

#chkconfig --level 连在一起的启动级别 服务名on/off

案例：设置httpd服务在3，5级别下默认开机启动

![img](D:\MyNote\images\wpqs8.jpg) 

案例：设置httpd服务在5的级别下默认开机不启动

![img](D:\MyNote\images\wps9q.jpg) 

## 8.4.ntp服务

作用：ntp主要是用于对计算机的时间同步管理操作。 

时间是对服务器来说是很重要的，一般很多网站都需要读取服务器时间来记录相关信息，如果时间不准，则可能造成很大的影响。

例如：当前虚拟机里的linux时间就是不准确的

![img](D:\MyNote\images\wps10wq.jpg) 

同时服务器时间方式有2个：一次性同步（手动同步）、通过服务自动同步。

上游的概念：

![img](D:\MyNote\images\wpsq1q1.jpg) 

①一次性同步时间（简单）

#ntpdate 时间服务器的域名或ip地址

Ip地址查看可以访问：http://www.ntp.org.cn/pool.php

![img](D:\MyNote\images\wpqs12.jpg) 

②设置时间同步服务

服务名：ntpd

启动ntpd服务

​	#service ntpd start   或者  /etc/init.d/ntpd start

![img](D:\MyNote\images\wps13q.jpg) 

设置ntpd服务开机启动：

\# chkconfig --list|grep ntpd

\# chkconfig --level 35 ntpd on

![img](D:\MyNote\images\wpsq14.jpg) 

## 8.5.防火墙服务

防火墙：防范一些网络攻击。有软件防火墙、硬件防火墙之分。

![img](D:\MyNote\images\wps15q.jpg) 

防火墙选择让请求通过，从而保证网络安全性。

在当前的centos6.5中防火墙有一个名称：iptables 【7.x中默认使用的是firewalld】

①查看iptables是否开机启动

![img](D:\MyNote\images\wps16.jpg) 

②iptables服务启动/重启/关闭

\#service iptables start/restart/stop

/etc/init.d/iptables start /restart/stop

③查看iptables的状态（规则）

\# service iptables status

如果iptables没有启动，则提示服务没启动，如果已经启动，则显示防火墙的相关的规则信息

![img](D:\MyNote\images\wpsqw17.jpg) 

④查看规则的命令

\#iptables -L -n

含义：

​	-L：表示列出规则

​	-n：表示将单词表达形式改成数字形式显示

⑤简单设置防火墙规则

例如，需要允许80端口通过防火墙，则规则可以用以下的命令来设置

#iptables -I INPUT -p tcp --dport 80 -j ACCEPT   #允许访问80端口

Iptables：主命令

-I：表示将规则放到最前面

-A：add，添加规则（最后）

INPUT：进站请求【出站output】

-p：protocol，指定协议（icmp/tcp/udp）

--dport：指定端口号

-j：指定行为结果，允许（accept）/禁止（reject）/丢弃（drop）

![img](D:\MyNote\images\wpsqw18.jpg) 

添加完成之后需要保存操作：

/etc/init.d/iptables save

![img](D:\MyNote\images\wps1qw9.jpg) 

 

测试80端口访问：

![img](D:\MyNote\images\wps2qw0.jpg) 

## 8.6.rpm管理（重点）

作用：rpm的作用类似于windows上的电脑管家中“软件管理”、安全卫士里面“软件管家”等产品，主要作用是对linux服务器上的软件包进行对应管理操作，管理分为：查询、卸载、安装。

①查询某个软件的安装情况

#rpm -qa|grep 关键词

选项：

​	-q：查询，query

​	-a：全部，all

案例：查询linux上是否安装firefox

![img](D:\MyNote\images\wps2qw1.jpg) 

案例：查询是否安装qq

![img](D:\MyNote\images\wps2qw2.jpg) 

②卸载某个软件

\#rpm -e 软件的名称

![img](D:\MyNote\images\wps2qwq2.jpg) 

火狐卸载的时候是没有依赖关系的，所以可以直接卸载。

但是在卸载Apache的时候提示无法卸载：

![img](D:\MyNote\images\wpsqw24.jpg) 

当存在依赖关系的时候又不想去解决这个问题的时候可以：

\#rpm -e 软件包名 --nodeps

![img](D:\MyNote\images\wps2qwe5.jpg) 

③软件的安装

要想装软件，和windows下一样，先得找到安装包。

​	软件包的获得方式：

​		a. 去官网去下载；

​		b. 不介意老版本的话，可以从光盘（或者镜像文件）中读取；

此处以光盘文件为例：

查看块状设备的信息：

\#lsblk  （list block devices）		查看块状设备的信息	

![img](D:\MyNote\images\wps261q.jpg) 

Name：名称

Size：设备大小

Type：类型

MountPoint：挂载点（类似windows下盘符），需要使用**已经存在**的**空目录**作为挂载点

扩展：光盘的挂载和解挂

a. 解挂操作

​	命令：umount

​	语法：#umount 当前设备的挂载点（路径）

![img](D:\MyNote\images\wps2qw7.jpg) 

此时，相当于U盘在windows上已经被弹出了，但是没有拔下电脑USB接口。

b. 挂载光盘

​	命令：mount

​	语法：#mount 设备原始地址 要挂载的位置路径

设备原始地址：地址统一都在/dev下，然后根据大小确定具体name值，拼凑在一起组成原始地址，例如当前：“/dev/sr0”

要挂载的位置路径：挂载目录一般都在mnt下，也可以在mnt下建目录，此处以“/mnt/dvd”为例

![img](D:\MyNote\images\wps28qw.jpg) 

安装软件的命令：

#rpm -ivh 软件包完整                                               名称                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     

选项：

​	-i：install，安装

​	-v：显示进度条

​	-h：表示以“#”形式显示进度条

![img](D:\MyNote\images\wpsq29.jpg) 

## 8.7.计划任务（重点）

作用：操作系统不可能24小时都有人在操作，有些时候想在指定的时间点去执行任务（例如：每天夜里2点去重新启动Apache），此时不可能真有人每天夜里2点去执行命令，此时可以交给计划任务程序去执行操作。

语法：#crontab 选项

​	常用选项：

​		-l：list，列出指定用户的计划任务列表

​		-e：edit，编辑指定用户的计划任务列表

​		-u：user，指定的用户名，如果不指定，则表示当前用户

​		-r：remove，删除指定用户的计划任务列表

①列出

![img](D:\MyNote\images\wpsqw30.jpg) 

②编辑计划任务（重点）

计划任务的规则语法格式，以行为单位，一行则为一个计划：

分 时 日 月 周 需要执行的命令

例如：如果想要每天的0点0分执行reboot指令，则可以写成

0 0 * * * reboot

取值范围：

分：0~59

时：0~23

日：1~31

月：1~12

周：0~7，0和7表示星期天

四个符号：

*：表示取值范围中的每一个数字

-：做连续区间表达式的，要想表示1~7，则可以写成：1-7

/：表示每多少个，例如：想每10分钟一次，则可以在分的位置写：*/10

,：表示多个取值，比如想在1点，2点6点执行，则可以在时的位置写：1,2,6

问题1：每月1、10、22日的4:45重启network服务

45  4  1,10,22  *  *  service network restart 

问题2：每周六、周日的1:10重启network服务

10  1  *  *  6,0  service network restart

问题3：每天18:00至23:00之间每隔30分钟重启network服务

*/30  18-23  *  *  *  service network restart

问题4：每隔两天的上午8点到11点的第3和第15分钟执行一次重启

3,15  8-11  */2  *  *  reboot

案例：真实测试案例，每1分钟往root家目录中的RT.txt中输入当前的时间信息，为了看到效果使用追加输出

计划任务：*/1  *  *  *  *  ls ~>> /root/RT.txt

Crontab权限问题：本身是任何用户都可以创建自己的计划任务。

但是超级管理员可以通过配置来设置某些用户不允许设置计划任务 ：

配置文件位于（黑名单）：

​	/etc/cron.deny			里面写用户名，一行一个

![img](D:\MyNote\images\wpqws31.jpg) 

![img](D:\MyNote\images\wps32qw.jpg)  

还有一个配置文件：（白名单）

​	/etc/cron.allow		（本身不存在，自己创建）

注意：白名单优先级高于黑名单，如果一个用户同时存在两个名单文件中，则会被默认允许创建计划任务。

# 9.用户与用户组管理*
Linux系统是一个多用户多任务的操作系统，任何一个要使用系统资源的用户，都必须首先向系统管理员申请一个账号，然后以这个账号的身份进入系统。
用户的账号一方面可以帮助系统管理员对使用系统的用户进行跟踪，并控制他们对系统资源的访问；另一方面也可以帮助用户组织文件，并为用户提供安全性保护。
每个用户账号都拥有一个惟一的用户名和各自的密码。
用户在登录时键入正确的用户名和密码后，就能够进入系统和自己的主目录。
要想实现用户账号的管理，要完成的工作主要有如下几个方面：

用户账号的添加、删除、修改以及用户密码的管理。
用户组的管理。

注意三个文件：
/etc/passwd				存储用户的关键信息
/etc/group				存储用户组的关键信息
/etc/shadow				存储用户的密码信息

## 9.1.用户管理

### 9.1.1.添加用户
常用语法：#useradd 选项 用户名
常用选项：
	-g：表示指定用户的用户主组，选项的值可以是用户组的id，也可以是组名
	-G：表示指定用户的用户附加组，选项的值可以是用户组的id，也可以是组名
	-u：uid，用户的id（用户的标识符），系统默认会从500之后按顺序分配uid，如果不想使用系统分配的，可以通过该选项自定义【类似于腾讯QQ的自选靓号情况】
	-c comment：添加注释

案例：创建用户zhangsan，不带任何选项

![img](D:\MyNote\images\wps31.jpg) 

验证是否成功：
	a. 验证/etc/passwd的最后一行，查看是否有zhangsan的信息；
	b. 验证是否存在家目录（在Centos下创建好用户之后随之产生一个同名家目录）；

扩展：认识passwd文件


用户名:密码:用户ID:用户组ID:注释:家目录:解释器shell

用户名：创建新用户名称，后期登录的时候需要输入；
密码：此密码位置一般情况都是“x”，表示密码的占位；
用户ID：用户的识别符；
用户组ID：该用户所属的主组ID；
注释：解释该用户是做什么用的；
家目录：用户登录进入系统之后默认的位置；
解释器shell：等待用户进入系统之后，用户输入指令之后，该解释器会收集用户输入的指令，传递给内核处理；

注意：在不添加选项的时候，执行useradd之后会执行一系列的操作
	a. 创建同名的家目录；
	b. 创建同名的用户组；

案例：添加选项，创建用户lisi，让lisi属于501主组，附加组500，自选靓号666。

![img](D:\MyNote\images\wps1q.jpg) 

![img](D:\MyNote\images\wpsq2.jpg) 

![img](D:\MyNote\images\wps3q.jpg) 

注意：查看用户的主组可以查看passwd文件，查看附加组可以查看group文件。

### 9.1.2.修改用户

常用语法：#usermod 选项 用户名
Usermod：user modify，用户修改
常用选项：
	-g：表示指定用户的用户主组，选项的值可以是用户组的id，也可以是组名
	-G：表示指定用户的用户附加组，选项的值可以是用户组的id，也可以是组名
	-u：uid，用户的id（用户的标识符），系统默认会从500之后按顺序分配uid，如果不想使用系统分配的，可以通过该选项自定义【类似于腾讯QQ的自选靓号情况】
	-l：修改用户名

案例：修改zhangsan用户主组为500，附加组改为501
#usermod -g 500 -G 501 zhangsan

案例：修改zhangsan用户用户名，改为wangerma
#usermod -l 新的用户名 旧的用户名
#usermod -l wangerma zhangsan

### 9.1.3.设置密码

Linux不允许没有密码的用户登录到系统，因此前面创建的用户目前都处于锁定状态，需要设置密码之后才能登录计算机。

常用语法：#passwd 用户名
案例：设置wangerma用户的密码

![img](D:\MyNote\images\wpsq4.jpg)

在设置密码的时候也是没有任何输入提示的，放心输入，确保两次输入的密码一致，按下回车即可。

也可以使用弱密码，但是不建议，否则会看到以下的提示：

![img](D:\MyNote\images\wpsq5q.jpg)


设置密码之后shadow文件中的体现：能够看出lisi用户没有密码的。

在设置用户密码之后可以登录帐号，例如此处需要登录wangerma
切换用户命令：#su [用户名]	（switch user）
如果用户名不指定则表示切换到root用户。

切换用户需要注意的事项：
	a. 从root往普通用户切换不需要密码，但是反之则需要root密码；
	b. 切换用户之后前后的工作路径是不变的；
	c. 普通用户没有办法访问root用户家目录，但是反之则可以；

### 9.1.4.删除用户

常用语法：#userdel 选项 用户名
Userdel：user delete（用户删除）
常用选项：
	-r：表示删除用户的同时，删除其家目录；
案例：删除wangerma用户

![img](D:\MyNote\images\wps1a.jpg)

注意：处于登录中的wangerma用户删除的时候提示删除失败，但是没有登录的lisi用户可以正常删除。

解决办法：简单粗暴，kill对应用户的全部进程

![img](D:\MyNote\images\qwps2.jpg)

提示：所有跟用户操作的命令（除passwd外）只有root超级管理员有权限执行。

## 9.2.用户组管理

每个用户都有一个用户组，系统可以对一个用户组中的所有用户进行集中管理。不同Linux 系统对用户组的规定有所不同，如Linux下的用户属于与它同名的用户组，这个用户组在创建用户时同时创建。

用户组的管理涉及用户组的添加、删除和修改。组的增加、删除和修改实际上就是对/etc/group文件的更新。

![img](D:\MyNote\images\awps3.jpg) 

文件结构：

用户组名:密码:用户组ID:组内用户名

密码：X表示占位符，虽然用户组可以设置密码，但是绝大部分的情况下不设置密码；

组内用户名：表示附加组是该组的用户名称；

### 9.2.1.用户组添加

常用语法：#groupadd 选项 用户组名

常用选项：

​	-g：类似用户添加里的“-u”，-g表示选择自己设置一个自定义的用户组ID数字，如果自己不指定，则默认从500之后递增； 

案例：使用groupadd指令创建一个新的用户组，命名为Administrators

![img](D:\MyNote\images\qwps4.jpg) 

### 9.2.2.用户组编辑

常用语法：#groupmod 选项 用户组名

常用选项：

​	-g：类似用户修改里的“-u”，-g表示选择自己设置一个自定义的用户组ID数字

​	-n：类似于用户修改“-l”，表示设置新的用户组的名称

案例：修改Administrators用户组，将组ID从502改成520，将名称改为admins

![img](D:\MyNote\images\qwps5.jpg) 

### 9.2.3.用户组删除

常用语法：#groupdel 用户组名

![img](D:\MyNote\images\qwps6.jpg) 

注意：当如果需要删除一个组，但是这个组是某个用户的主组时，则不允许删除；如果确实需要删除，则先从组内移出所有用户。

![img](D:\MyNote\images\qwps7.jpg) 

 # 10.网络设置

首先知道网卡配置文件位置：/etc/sysconfig/network-scripts

![img](D:\MyNote\images\qwps8.jpg) 

在目录中网卡的配置文件命名格式：ifcfg-网卡名称

![img](D:\MyNote\images\qwps9.jpg) 

ONBOOT：是否开机启动

BOOTPROTO：ip地址分配方式，DHCP表示动态主机分配协议

HWADDR：硬件地址，MAC地址

如果后续需要重启网卡怎么去操作呢？

  #service  network  restart  

![img](D:\MyNote\images\qwps10.jpg) 

在有的分支版本中可能没有service命令来快速操作服务，但是有一个共性的目录：/etc/init.d

这个目录中放着服务的快捷方式。

此处重启网卡命令还可以使用：

  #/etc/init.d/network restart

![img](D:\MyNote\images\qwps11.jpg) 

  扩展1：如果修改网卡的配置文件，但是配置文件的目录层次很深，此时可以在浅的目录中创建一个快捷方式（软连接），方便以后去查找

  #ln  -s   原始文件的路径 快捷方式的路径 

![img](D:\MyNote\images\1wps12.jpg) 

通过ls -l可以列出如下的效果：

![img](D:\MyNote\images\qwps13.jpg) 

其中，文件类型位置的“l”表示其类型为link（连接类型），后面的“->”指向的是原始文件路径。

扩展2：如何去重启单个网卡？ 

停止某个网卡：#ifdown 网卡名

开启某个网卡：#ifup 网卡名

例如：需要停止-启动（重启）eth0网卡，则可以输入

\#ifdown eth0

\#ifup eth0

提示：在实际工作的时候不要随意禁网卡。

# 11.ssh服务(重点)

ssh（secure shell，安全外壳协议），该协议有2个常用的作用：远程连接协议、远程文件传输协议。

协议使用端口号：默认是22

可以是被修改的，如果需要修改，则需要修改ssh服务的配置文件：

\#/etc/ssh/ssh_config

![img](D:\MyNote\images\qwps21.jpg) 

端口号可以修改，但是得注意2个事项：

​	a. 注意范围，端口范围是从0-65535；

​	b. 不能使用别的服务已经占用的端口；

服务启动/停止/重启

\#service sshd start/stop/restart

\#/etc/init.d/sshd start/stop/restart

![img](D:\MyNote\images\qwps22.jpg) 

## 11.1.远程终端

终端工具主要帮助运维人员连接远程的服务器，常见终端工具有：Xshell、secureCRT、Putty等。以putty为例：

①获取服务器ip地址，可以通过ifconfig命令进行查看，然后顺手测试ip的连接相通性

![img](D:\MyNote\images\qwps23.jpg) 

②打开putty，输入相关的信息

![img](D:\MyNote\images\wps24.jpg) 

 

③在弹出key确认的时候点击“是”，以后不会再提示

![img](D:\MyNote\images\wps25.jpg) 

 

④输入登录信息

![img](D:\MyNote\images\wps26.jpg) 

## 2、SSH服务文件传输

可视化的界面传输工具：Filezilla

安装好之后可以查看到桌面图标：

![img](D:\MyNote\images\qwps27.jpg) 

①选择“文件”- “站点管理器（Ctrl + S）”

![img](D:\MyNote\images\qwps28.jpg) 

②点击“文件”菜单下方的“▽”选择需要连接的服务器，连接好之后的效果

![img](D:\MyNote\images\qwps29.jpg) 

③从本地windows上传文件到linux中方式

支持直接拖拽文件，也可以右键本地需要上传的文件，然后点选“上传”即可

![img](D:\MyNote\images\qwps30.jpg) 

④下载linux文件到本地

支持服务器文件直接拖拽到本地，也可以在右侧窗口选择需要下载的文件，右键，点选“下载”。 

扩展3：通过命令行工具来传输文件/文件夹

工具：PSCP.exe（必须通过cmd命令行打开），为了使用方便可以将其放到环境变量目录中

如果不清楚哪些路径是环境变量路径，只需要将其放到C:/Windows目录下即可。

![img](D:\MyNote\images\qwps31.jpg) 

 

用法：

​	a. pscp 选项 用户名@linux主机地址:资源路径 windows本地的地址 （下载到win）

​	b. pscp 选项 资源路径 用户名@linux主机地址:远程路径	（上传到linux）

​	c. pscp 选项 -ls 用户名@linux主机地址 （列出远程路径下结构）

①下载到本地windows

要求将远程linux服务器下的/etc整个目录下载到本地E:\tmp下

\#pscp -r [root@192.168.21.128:/etc](mailto:root@192.168.21.128:/etc) E:\tmp

在CMD中输入之后输入密码

![img](D:\MyNote\images\wps32.jpg) 

![img](D:\MyNote\images\wps33.jpg) 

②上传文件到linux

将“E:\coursedocs\运维学科\北京运维01期\01-基础班\20180329_Linux自有服务”所有的内容传输到linux下root用户的家目录

\#pscp -r “E:\coursedocs\运维学科\北京运维01期\01-基础班\20180329_Linux自有服务” [root@192.168.21.128:/root](mailto:root@192.168.21.128:/root)

![img](D:\MyNote\images\wps34.jpg) 

# 11.文件权限管理

Linux的权限操作与用户、用户组是兄弟操作。

## 11.1.权限概述

总述：Linux系统一般将文件可存/取访问的身份分为3个类别：owner、group、others，且3种身份各有read、write、execute等权限。

### 11.1.1.权限概念

什么是权限？

在多用户（可以不同时）计算机系统的管理中，权限是指某个特定的用户具有特定的系统资源使用权力，像是文件夹、特定系统指令的使用或存储量的限制。

在Linux中分别有读、写、执行权限：

读权限：

​	对于文件夹来说，读权限影响用户是否能够列出目录结构

​	对于文件来说，读权限影响用户是否可以查看文件内容

写权限：

​	对文件夹来说，写权限影响用户是否可以在文件夹下“创建/删除/复制到/移动到”文档

​	对于文件来说，写权限影响用户是否可以编辑文件内容

执行权限：

​	一般都是对于文件来说，特别脚本文件。

### 11.1.2.身份介绍

**Owner身份（文件所有者，默认为文档的创建者）**

由于Linux是多用户、多任务的操作系统，因此可能常常有多人同时在某台主机上工作，但每个人均可在主机上设置文件的权限，让其成为个人的“私密文件”，即个人所有者。因为设置了适当的文件权限，除本人（文件所有者）之外的用户无法查看文件内容。 

例如某个MM给你发了一封Email情书，你将情书转为文件之后存档在自己的主文件夹中。为了不让别人看到情书的内容，你就能利用所有者的身份去设置文件的适当权限，这样，即使你的情敌想偷看你的情书内容也是做不到的。

**Group身份（与文件所有者同组的用户）**

与文件所有者同组最有用的功能就体现在多个团队在同一台主机上开发资源的时候。例如主机上有A、B两个团体，A中有a1,a2,a3三个成员，B中有b1,b2两个成员，这两个团体要共同完成一份报告F。由于设置了适当的权限，A、B团体中的成员都能互相修改对方的数据，但是团体C的成员则不能修改F的内容，甚至连查看的权限都没有。同时，团体的成员也能设置自己的私密文件，让团队的其它成员也读取不了文件数据。在Linux中，每个账户支持多个用户组。如用户a1、b1即可属于A用户组，也能属于B用户组【主组和附加组】。

**Others身份（其他人，相对于所有者）**

这个是个相对概念。打个比方，大明、二明、小明一家三兄弟住在一间房，房产证上的登记者是大明（owner所有者），那么，大明一家就是一个用户组，这个组有大明、二明、小明三个成员；另外有个人叫张三，和他们三没有关系，那么这个张三就是其他人了。

同时，大明、二明、小明有各自的房间，三者虽然能自由进出各自的房间，但是小明不能让大明看到自己的情书、日记等，这就是文件所有者（用户）的意义。

**Root用户（超级用户）**

在Linux中，还有一个神一样存在的用户，这就是root用户，因为在所有用户中它拥有最大的权限 ，所以管理着普通用户。

### 11.1.3.权限介绍

要设置权限，就需要知道文件的一些基本属性和权限的分配规则。在Linux中，ls命令常用来查看文件的属性，用于显示文件的文件名和相关属性。

\#ls -l 路径		【ls -l 等价于 ll】

![img](D:\MyNote\images\wps1qs.jpg) 

标红的部分就是Linux的文档权限属性信息。

Linux中存在用户、用户组和其他人概念，各自有不同的权限，对于一个文档来说，其权限具体分配如下：

![img](D:\MyNote\images\wpsqsd2.jpg)

十位字符表示含义：

第1位：表示文档类型，取值常见的有“d表示文件夹”、“-表示文件”、“l表示软连接”、“s表示套接字”等等；

第2-4位：表示文档所有者的权限情况，第2位表示读权限的情况，取值有r、-；第3位表示写权限的情况，w表示可写，-表示不可写，第4位表示执行权限的情况，取值有x、-。

第5-7位：表示与所有者同在一个组的用户的权限情况，第5位表示读权限的情况，取值有r、-；第6位表示写权限的情况，w表示可写，-表示不可写，第7位表示执行权限的情况，取值有x、-。

第8-10位：表示除了上面的前2部分的用户之外的其他用户的权限情况，第8位表示读权限的情况，取值有r、-；第9位表示写权限的情况，w表示可写，-表示不可写，第10位表示执行权限的情况，取值有x、-。

权限分配中,均是rwx的三个参数组合，且位置顺序不会变化。没有对应权限就用 – 代替。

例如：以下一个文档权限是怎么样的？

![img](D:\MyNote\images\wpqers3.jpg) 

a. 其是文件夹类型

b. 所有者：拥有全部权限（读写执行）

c. 同组用户：可读、可执行

d. 其他用户：可读、可执行

## 11.2.权限设置

语法：#chmod 选项 权限模式 文档

注意事项：

​	常用选项：

​			-R：递归设置权限	（当文档类型为文件夹的时候）

​	权限模式：就是该文档需要设置的权限信息

​	文档：可以是文件，也可以是文件夹，可以是相对路径也可以是绝对路径。

注意点：如果想要给文档设置权限，操作者要么是root用户，要么就是文档的所有者。

### 11.2.1.字母形式

![img](D:\MyNote\images\wpzxs4.jpg) 

给谁设置：

​	u：表示所有者身份owner（user）

​	g：表示给所有者同组用户设置（group）

​	o：表示others，给其他用户设置权限

​	a：表示all，给所有人（包含ugo部分）设置权限

如果在设置权限的时候不指定给谁设置，则默认给所有用户设置

权限字符：

​	r：读

​	w：写

​	x：表示执行

​	-：表示没有权限

权限分配方式：

​	+：表示给具体的用户新增权限（相对当前）

​	-：表示删除用户的权限（相对当前）

​	=：表示将权限设置成具体的值（注重结果）【赋值】

例如：需要给anaconda-ks.cfg文件（-rw-------.）设置权限，要求所有者拥有全部的权限，同组用户拥有读和执行权限，其他用户只读权限。

答案：

①#chmod u+x,g+rx,o+r  anaconda-ks.cfg

![img](D:\MyNote\images\wqwps5.jpg) 

②#chmod u=rwx,g=rx,o=r  anaconda-ks.cfg

![img](D:\MyNote\images\wpqws6.jpg) 

提示：当文档拥有执行权限（任意部分），则其颜色在终端中是绿色。

\#chmod ug=rwx 形式，如果有两部分权限一样则可以合在一起写的

例如：如果anaconda-ks.cfg文件什么权限都没有，可以使用root用户设置所有人都有执行权限，则可以写成

​	①#chmod +x  anaconda-ks.cfg

​	②#chmod a=x  anaconda-ks.cfg

​	③#chmod a+x anaconda-ks.cfg

### 11.2.2.数字形式

经常会在一些技术性的网页上看到类似于#chmod 777  a.txt 这样的一个权限，这种形式称之为数字形式权限（777）。

读：r   4
写：w   2
执行：x   1
没有任何权限：0

![img](D:\MyNote\images\wpqws7.jpg) 

例如：需要给anaconda-ks.cfg设置权限，权限要求所有者拥有全部权限，同组用户拥有读执行权限，其他用户只读。

全部权限（u）：读+写+执行=4+2+1=7

读和执行（g）：读+执行=4+1=5

读权限（o）：读=4

由上得知权限为：754

\#chmod 754 anaconda-ks.cfg

![img](D:\MyNote\images\wpsqw8.jpg) 

面试题：用超级管理员设置文档的权限命令是#chmod -R 731 aaa，请问这个命令有没有什么不合理的地方？

拥有者：7=4+2+1=读+写+执行

同组用户：3=2+1=写+执行

其他用户：1=1=执行

注意：在写权限的时候千万不要设置类似于上面的这种“奇葩权限”。如果一个权限数字中但凡出现2与3的数字，则该权限有不合理的情况。

### 11.2.3.注意事项

使用root用户创建一个文件夹（/oo），权限默认，权限如下：

![img](D:\MyNote\images\aswps9.jpg) 

需要在oo目录下创建文件（oo/xx.txt），需要给777权限：

![img](D:\MyNote\images\aswps10.jpg) 

切换到test用户（不是文档所有者，也不是同组用户，属于other部分）：

问题1：test用户是否可以打开oo/xx.txt文件？【能打开】

问题2：test用户是否可以编辑oo/xx.txt文件？【可以】

问题3：test用户是否可以删除oo/xx.txt文件？【不可以，同样还不允许创建文件/文件夹、移动文件、重命名文件】

![img](D:\MyNote\images\adwps11.jpg) 

在Linux中，如果要删除一个文件，不是看文件有没有对应的权限，而是看文件所在的目录是否有写权限，如果有才可以删除。

## 11.3.属主与属组设置

属主：所属的用户（文件的主人）

属组：所属的用户组

![img](D:\MyNote\images\wpzxs12.jpg) 

前面的那个root就是属主

后面的那个root就是属组

这两项信息在文档创建的时候会使用创建者的信息（用户名、用户所属的主组名称）。

如果有时候去删除某个用户，则该用户对应的文档的属主和属组信息就需要去修改。

### 11.3.1.chown（重点）

作用：更改文档的所属用户

语法：#chown -R  username 文档路径

案例：将刚才root用户创建的oo目录，所有者更改为test

\#chown test oo/

![img](D:\MyNote\images\wpzxs13.jpg) 

### 11.3.2.chgrp（了解）

作用：更改文档的所属用户组

语法：#chgrp -R  groupname 文档的路径

案例：将刚才root用户创建的oo目录，所有者更改为test，并且将所属用户组也改为test

\#chgrp  test  oo/

![img](D:\MyNote\images\wpszx14.jpg) 

思考，如何通过一个命令实现既可以更改所属的用户，也可以修改所属的用户组呢？

答：可以实现的，通过chown命令

​	语法：#chown -R  username:groupname  文档路径

案例：要求只使用chown指令，将oo目录的所属用户和用户组改回成root，并且包含其子目录

![img](D:\MyNote\images\wpszx15.jpg) 

## 11.4.扩展

问题：reboot、shutdown、init、halt、user管理，在普通用户身份上都是操作不了，但是有些特殊的情况下又需要有执行权限。又不可能让root用户把自己的密码告诉普通用户，这个问题该怎么解决？

该问题是可以被解决的，可以使用sudo（switch user do）命令来进行权限设置。Sudo可以让管理员（root）事先定义某些特殊命令谁可以执行。

默认sudo中是没有除root之外用户的规则，要想使用则先配置sudo。

Sudo配置文件：/etc/sudoers

![img](D:\MyNote\images\wps1zx6.jpg) 

a. 配置sudo文件请使用“#visudo”，打开之后其使用方法和vim一致

b. 配置普通用户的权限

![img](D:\MyNote\images\wps1zx7.jpg) 

Root表示用户名，如果是用户组，则可以写成“%组名”

ALL：表示允许登录的主机（地址白名单）

(ALL)：表示以谁的身份执行，ALL表示root身份

ALL：表示当前用户可以执行的命令，多个命令可以使用“,”分割

案例：本身test用户不能添加用户，要求使用sudo配置，将其设置为可以添加用户，并且可以修改密码（但是不能修改root用户密码）。

注意：在写sudo规则的时候不建议写直接形式的命令，而是写命令的完整路径。

路径可以使用which命令来查看

语法：#which 指令名称

![img](D:\MyNote\images\wpszx18.jpg) 

![img](D:\MyNote\images\wps1zx9.jpg) 

![img](D:\MyNote\images\wpszx20.jpg) 

在添加好对应的规则之后就可以切换用户，切换到普通用户test，再去执行：

![img](D:\MyNote\images\wps2zx1.jpg) 

此时要想使用刚才的规则，则以以下命令进行：

#sudo 需要执行的指令

![img](D:\MyNote\images\wps2zx2.jpg) 

在输入sudo指令之后需要输入当前的用户密码进行确认的操作（不是root用户密码），输入之后在接下来5分钟内再次执行sudo指令不需要密码。

特别注意：此处按照案例要求，不能让test用户修改root密码，因此规则还需要调整，不然其可以修改root密码的：

禁止修改root密码的配置（先允许全部，再拒绝root密码设置）： /usr/bin/passwd [A-Za-z]*, !/usr/bin/passwd root

![img](D:\MyNote\images\wps23zx.jpg) 

补充：在普通用户下怎么查看自己具有哪些特殊权限呢？

#sudo -l

![img](D:\MyNote\images\wpszx24.jpg) 

最后：sudo不是任何Linux分支都有的命令，常见centos与ubuntu都存在sudo命令。

# 12.Linux的网络基础

## 12.1.网络相关概述

### 12.1.1.网络发展

**信息传递**

+ 远古时期，人们就通过简单的语言、壁画等方式交换信息

+ 千百年来，人们一直在用语言、图符、钟鼓、烟火、竹简、纸书等传递信息

+ 古代人的烽火狼烟、飞鸽传信、驿马邮递

+ 现代社会中，交通警的指挥手语、航海中的旗语等

+ 这些信息传递的基本方式都是依靠人的视觉与听觉 

**电的产生**

+ 1831年，法拉第制出了世界上最早的第一台发电机

+ 1866年，德国人西门子（Siemens）制成世界上第一台大功率发电机

+ 1837年，美国人塞缪乐·莫乐斯成功地研制出世界上第一台电磁式电报机

+ 1844年5月24日，莫乐斯在国会大厦联邦最高法院会议厅进行了“用莫尔斯电码”发出了人类历史上的第一份电报，从而实现了长途电报通信

**网络诞生**

+ 1957年，前苏联发射了第一颗人造卫星，震惊了美国

+ 1958年美国成立了国防部高级研究计划署（ARPA，Advanced Research Projects Agency），应对冷战形势，ARPA是一个管理机构，没有实验室和科学家

​                              ![img](D:\MyNote\images\wpsm1.jpg) 

+ 1969年，ARPANET（阿帕网）开始联机，因此1969年被称为Internet元年

**网络分类**（记忆）

+ 局域网（Local Area Network，LAN）是指范围在几百米到十几公里内办公楼群或校园内的计算机相互连接所构成的计算机网络。

+ 城域网（Metropolitan Area Network，MAN）所采用的技术基本上与局域网相类似，只是规模上要大一些。城域网既可以覆盖相距不远的几栋办公楼，也可以覆盖一个城。

+ 广域网（Wide Area Network，WAN）通常跨接很大的物理范围，如一个国家。

除了上述的划分，网络还可以按照所有者分为公网、私网是两种Internet的接入方式。公网接入方式：上网的计算机得到的IP地址是Internet上的非保留地址，公网的计算机和Internet上的其他计算机可随意互相访问。私网则反之。

### 12.1.2.ip地址(重点)

IP是英文Internet Protocol的缩写，意思是“网络之间互连的协议”，也就是为计算机网络相互连接进行通信而设计的协议。

IP地址类型分为：公有地址、私有地址。

**公有地址**

公有地址（Public address）由Inter NIC（Internet Network Information Center因特网信息中心）负责。这些IP地址分配给注册并向Inter NIC提出申请的组织机构。通过它直接访问因特网。

**私有地址**（重点）

私有地址（Private address）属于非注册地址，专门为组织机构内部使用。以下列出留用的内部私有地址： 

A类 10.0.0.0--10.255.255.255

B类 172.16.0.0--172.31.255.255

C类 192.168.0.0--192.168.255.255

IP地址按类型可以分为三类：

| 类别 | 最大网络数    | IP地址范围                | 最大主机数 | 私有IP地址范围              |
| ---- | ------------- | ------------------------- | ---------- | --------------------------- |
| A    | 126（2^7-2)   | 1.0.0.0-127.255.255.255   | 16777214   | 10.0.0.0-10.255.255.255     |
| B    | 16384(2^14)   | 128.0.0.0-191.255.255.255 | 65534      | 172.16.0.0-172.31.255.255   |
| C    | 2097152(2^21) | 192.0.0.0-223.255.255.255 | 254        | 192.168.0.0-192.168.255.255 |

网络运维相关技能：ip分类、子网划分、划分vlan、ACL、综合布线、各种Serve的搭建。

127.0.0.1			本机ip

### 12.1.3.网卡

![img](D:\MyNote\images\wps2m.jpg) 

网卡是一个网络组件，属于硬件范畴，主要负责计算机之间数据的封装和解封。

MAC地址：网卡的物理地址，网卡设备的编号，默认情况是全球唯一的（16进制）。

![img](D:\MyNote\images\mwps3.jpg) 

与IP地址的区别：

+ 长度不同。IP地址为32位，MAC地址为48位。

+ 分配依据不同。

* 网络寻址方式不同。OSI参考模型，ip地址是基于第三层工作（网络层），mac地址是第二层（数据链路层）

### 12.1.4.网线

网线是连接局域网必不可少的。在局域网中常见的网线主要有双绞线（RJ45接口）、铜轴电缆、光缆三种。

 

​                                                                 ![img](D:\MyNote\images\mwps4.jpg)

​																	               双绞线	

![img](D:\MyNote\images\mwps5.png)

​																				铜轴电缆

![img](D:\MyNote\images\mwps6.jpg)

​																				 光纤

### 12.1.5.交换机

交换机（Switch）意为“开关”，是一种用于电（光）信号转发的网络设备，交换机它可以为接入交换机的任意两个网络节点提供独享的电信号通路。

![img](D:\MyNote\images\mwps7.jpg) 

目前，交换机品牌比较有名的是：华为、华三（h3c）、思科、锐捷。

### 12.1.6.路由器

路由器（Router）又称网关设备（Gateway）是用于连接多个逻辑上分开、相对独立的网络。

![img](D:\MyNote\images\mwps8.jpg)

​											       ![img](D:\MyNote\images\mwps9.jpg)

### 12.1.7.拓扑结构图

所谓“拓扑”就是把实体抽象成与其大小、形状无关的“点”，而把连接实体的线路抽象成“线”，进而以图的形式来表示这些点与线之间关系的方法，其目的在于研究这些点、线之间的相连关系。表示点和线之间关系的图被称为拓扑结构图。

常见的几种拓扑结构图：

 

![img](D:\MyNote\images\mwps10.jpg)  ![img](D:\MyNote\images\mwps11.jpg)

![img](D:\MyNote\images\mwps12.jpg)          ![img](D:\MyNote\images\mwps13.jpg)

![img](D:\MyNote\images\mwps14.jpg)         ![img](D:\MyNote\images\mwps15.jpg)

![img](D:\MyNote\images\mwps16.png)

## 12.2.网络相关命令

### 12.2.1.ping

作用：检测当前主机与目标主机之间的连通性（不是100%准确，有的服务器是禁ping）

语法：#ping 主机地址（ip地址、主机名、域名等）

例如：测试和baidu.com之间的连通性。

![img](D:\MyNote\images\mwps17.jpg) 

该命令可以跨平台，windows下也可以使用，语法一致。（区别在于Linux下默认一直发送，windows下默认发送4个数据包）

![img](D:\MyNote\images\mwps18.jpg) 

### 12.2.2.netstat

作用：表示查看网络的连接信息

语法：#netstat -tnlp		（-t：tcp协议，-n：将字母转化成数字，-l：列出状态为监听，-p：显示进程相关信息）

​	       #netstat -an	     （-a：表示全部，-n：将字母转化为数字）

TCP/IP协议需要使用这个命令。

### 12.2.3.traceroute

作用：查找当前主机与目标主机之间所有的网关（路由器，会给沿途各个路由器发送icmp数据包，路由器可能会不给响应）。

该命令不是内置命令，需要安装，但是目前的已经安装好了（之前选了开发工具）。

语法：#traceroute 主机地址

![img](D:\MyNote\images\mwps19.jpg) 

类似于查看快递的跟踪路由：

![img](D:\MyNote\images\mwps20.jpg) 

扩展：在windows下也有类似的命令：tracert 主机地址

![img](D:\MyNote\images\mwps21.jpg) 

在线工具网址：http://tool.chinaz.com

### 12.2.4.arp

地址解析协议，即ARP（Address Resolution Protocol），是根据IP地址获取（MAC）物理地址的协议。

![img](D:\MyNote\images\mwps22.jpg) 

当一个主机发送数据时，首先查看本机MAC地址缓存中有没有目标主机的MAC地址， 如果有就使用缓存中的结果；如果没有，ARP协议就会发出一个广播包，该广播包要求查询目标主机IP地址对应的MAC地址，拥有该IP地址的主机会发出回应，回应中包括了目标主机的MAC地址，这样发送方就得到了目标主机的MAC地址。如果目标主机不在本地子网中，则ARP解析到的MAC地址是默认网关的MAC地址。

常用语法：#arp -a  本地缓存mac表

​		           #arp -d  主机地址	删除指定的缓存记录

![img](D:\MyNote\images\mwps23.jpg) 

该命令在windows下同样适用。 

### 12.2.5.tcpdump(了解)

作用：抓包，抓取数据表

常用语法：

​	#tcpdump 协议 port 端口

​	#tcpdump 协议 port 端口 host 地址

​	#tcpdump -i 网卡设备名

查看22端口（ssh）的数据包：

![img](D:\MyNote\images\mwps24.jpg) 

00:09:17.xxxx	监听数据的时分秒

IP：使用的协议类型

192.168.21.1	数据包的一个方向（来自）

\>	数据的流向

192.168.21.136	数据包的另外一个方向（到达）

# 13.项目上线流程

## 13.1.服务器选配购买

项目上线服务器必须是外网服务器。

一般服务器有2种情况：购买真实服务器、购买云服务器。

购买真实服务器一次性成本过高，所以现在基本都是选择云服务器。

云服务的厂商：阿里云、腾讯云、知道创宇（加速乐）、华为云、盛大云、新浪云（sae）、亚马逊云等等。

以后以阿里云为例：

官网：http://www.aliyun.com

①打开阿里云官网，选择产品中的“云服务器ECS”

![img](D:\MyNote\images\mwps25.jpg) 

在页面上点击“立即购买”：

![img](D:\MyNote\images\mwps26.jpg) 

②选择具体的配置

![img](D:\MyNote\images\mwps27.jpg)

​														     一 

![img](D:\MyNote\images\mwps28.jpg)

​															二 

![img](D:\MyNote\images\mwps29.jpg)

​															三 

![img](D:\MyNote\images\mwps30.jpg)

​																四 

![img](D:\MyNote\images\mwps31.jpg)

​																五 

![img](D:\MyNote\images\mwps32.jpg)

​																六 

![img](D:\MyNote\images\mwps33.jpg)

​																七 

![img](D:\MyNote\images\mwps34.jpg)

 															八

安全组需要先在控制面板中创建，创建好之后才能在这里进行选择（安全组类似于防火墙，可以设置相关规则）：

![img](D:\MyNote\images\mwps35.jpg)

​														九 

![img](D:\MyNote\images\mwps36.jpg)

​														十 

![img](D:\MyNote\images\mwps37.jpg)

进入后台查看信息：

![img](D:\MyNote\images\mwps38.jpg) 

需要重置密码的话，则可以选择右侧“更多”选择“重置密码”，然后重启服务器，最后可以通过远程终端连接服务器：

![img](D:\MyNote\images\mwps39.jpg) 

## 13.2.域名购买

①在首页产品中找到域名注册

![img](D:\MyNote\images\mwps40.jpg) 

域名注册得先查看是否可以注册：

![img](D:\MyNote\images\mwps41.jpg) 

选择需要的域名：

![img](D:\MyNote\images\mwps42.jpg) 

确认购买信息：

![img](D:\MyNote\images\mwps43.jpg) 



![img](D:\MyNote\images\mwps44.jpg) 

购买之后就可以在后台控制面板中去查看域名情况。

## 13.3.域名备案

备案：当申请域名的人要想在国内使用域名，则需要向当地的通信管理局（省级）去申请报备。

备案前提：想要使用境内服务器的话，则必须得备案。

在管理后台点击“ICP备案系统”

![img](D:\MyNote\images\mwps45.jpg) 

点击新增主体备案：

![img](D:\MyNote\images\mwps46.jpg) 

 

填写完基本信息之后点击增加网站：

![img](D:\MyNote\images\mwps47.jpg) 

备案服务号可以在控制台顶部去获取：

![img](D:\MyNote\images\mwps48.jpg) 

 

申请到备案服务号之后填写继续：

![img](D:\MyNote\images\m4wps49.jpg) 

会让用户下载一个图片：网站真实性核验单

下载打印，填写好上传到阿里云备案系统中。

后面等待初审，初审通过之后继续下一步（初审时间一般1天即可）

拍照

![img](D:\MyNote\images\mwps50.jpg) 

上传照片

等待管局审核（到这个步骤基本是已经通过，审核周期一般是15个工作日）。

等待审核通过，就会收到工信部发送的短信与邮件通知，邮件中有备案号和备案密码（备案密码用于注销备案）。

## 13.4.域名解析

点击“解析”

![img](D:\MyNote\images\mwps51.jpg) 

解析：将域名绑定到一个服务器地址的操作

DNS：domain name server，用于将域名转化成ip地址的服务器。

![img](D:\MyNote\images\mwps52.jpg) 

点击右上角的添加记录：

![img](D:\MyNote\images\mwps53.jpg) 

选择记录：

![img](D:\MyNote\images\mwps54.jpg) 

例如：需要将[www.linux123.xyz](http://www.linux123.xyz)解析到之前购买的云主机上，则解析可以设置如下：

![img](D:\MyNote\images\mwps55.jpg) 

解析之后可以通过在线ping命令检测效果：

![img](D:\MyNote\images\wps56.jpg) 

## 13.5.上传代码

此时需要使用上传工具：pscp，filezilla 

和之前使用的方式一样。

# 14.Shell基础 

## 14.1.关于shell

### 14.1.1.什么是shell

**什么是shell？**

Shell（外壳） 是一个用 C 语言编写的程序，它是用户使用 Linux 的桥梁。Shell 既是一种命令语言，又是一种程序设计语言。

Shell 是指一种应用程序，这个应用程序提供了一个界面，用户通过这个界面访问操作系统内核的服务。

**什么是脚本？**

脚本简单地说就是一条条的文字命令，这些文字命令是可以看到的（如可以用记事本打开查看、编辑）。

常见的脚本： JavaScript（JS，前端），VBScript， ASP，JSP，PHP（后端），SQL（数据库操作语言），Perl，Shell，python，Ruby，JavaFX，Lua等。

**为什么要学习和使用shell？**

Shell属于内置的脚本

程序开发的效率非常高，依赖于功能强大的命令可以迅速地完成开发任务（批处理）

语法简单，代码写起来比较轻松，简单易学

**常见的shell种类？**

在linux中有很多类型的shell，不同的shell具备不同的功能，shell还决定了脚本中函数的语法，Linux中默认的shell是/bin/bash（重点），流行的shell有ash、bash、ksh、csh、zsh等，不同的shell都有自己的特点以及用途。

**csh**

C shell 使用的是“类C”语法,csh是具有C语言风格的一种shell，其内部命令有52个，较为庞大。目前使用的并不多，已经被/bin/tcsh所取代。

**ksh**

Korn shell 的语法与 Bourne shell 相同，同时具备了 C shell 的易用特点。许多安装脚本都使用 ksh ，ksh有42条内部命令，与bash相比有一定的限制性。

**tcsh**

tcsh是csh的增强版，与 C shell 完全兼容。

**sh** 

是一个快捷方式，已经被/bin/bash所取代。

nologin 

指用户不能登录

![img](D:\MyNote\images\zwps1.jpg) 

**zsh**

目前Linux里最庞大的一种shell：zsh。它有84个内部命令，使用起来也比较复杂。一般情况下，不会使用该shell。

**bash**

大多数Linux系统默认使用的shell，bash shell 是 Bourne shell 的一个免费版本，它是最早的 Unix shell，bash还有一个特点，可以通过help命令来查看帮助。包含的功能几乎可以涵盖shell所具有的功能，所以一般的shell脚本都会指定它为执行路径。

### 14.1.2.shell入门

**编写规范：**

*代码规范：*

​	#!/bin/bash				[指定告知系统当前这个脚本要使用的shell解释器]

​	Shell相关指令

文件命名规范：

​	文件名.sh				.sh是linux下bash shell 的默认后缀

**使用流程：**

①创建.sh文件			touch/vim命令

②编写shell代码

③执行shell脚本			脚本必须得有执行权限(即x的权限)

**案例1**：创建test.sh，实现第一个shell脚本程序，输出hello world.

输出命令：#echo 123

注意：输出的内容如果包含字母和符号（不包含变量），则需要用引号包括起来。如果是纯数字可以包也可以不包。

![img](D:\MyNote\images\xwps2.jpg) 

 

![img](D:\MyNote\images\zwps3.jpg) 

注意，这里在运行时一定要写成 ./test.sh，而不是 test.sh，运行其它二进制的程序也一样，直接写 test.sh，Linux 系统会去 PATH（环境变量） 里寻找有没有叫 test.sh 的，而只有 /bin, /sbin, /usr/bin，/usr/sbin 等在 PATH 里，你的当前目录通常不在 PATH 里，所以写成 test.sh 是会找不到命令的，要用 ./test.sh 告诉系统说，就在当前目录找。

**案例2**：使用root用户帐号创建并执行test2.sh，实现创建一个shelltest用户，并在其家目录中新建文件try.html。

![img](D:\MyNote\images\zwps4.jpg) 

脚本执行的另外一个方式：/bin/bash 脚本的路径（了解）

![img](D:\MyNote\images\zwps5.jpg) 

Shell脚本分为简单的写法（简单命令的堆积）和复杂写法（程序的设计）

## 14.2.shell进阶（重点）

### 14.2.1.变量

#### 14.2.1.1.含义

a. 什么是量

量就是数据.

b. 什么是变量

数据可以发生改变就是变量.

在一个脚本周期内,其值可以发生改变的量就是变量.

c. 什么叫做一个脚本周期

一个脚本周期我们可以简单的理解为当前的shell文件

变量是shell中不可或缺的一部分，也是最基础、最重要的组成部分。

#### 14.2.1.2.定义与使用

**变量，先定义后使用。**

定义形如：class_name="yunwe "

使用形如：echo $class_name

变量就是由2部分组成,一个是变量名（左边），另外一部分是变量的值（右边）

**变量名和变量值是什么关系??**

变量名和变量值是使用和被使用关系; 我们的变量名来使用变量值;

在使用变量的时候一定需要在变量名前面添加一个$符号，该要求在其他语言中也存在的（例如php）。

**变量名的规范**

注意，变量名后面的等号左右不能有空格，这可能和你熟悉的所有编程语言都不一样。同时，变量名的命名须遵循如下规则：

命名只能使用英文字母，数字和下划线，首个字符不能以数字开头。

中间不能有空格，可以使用下划线“_”。

不能使用标点符号。

不能使用bash里的关键字（可用help命令查看保留关键字）。

问题：以下哪个shell变量名是合法的？

A. var		B.?var    C. user*name    D.echo

案例1：使用变量改写入门脚本中的第1个shell脚本。

![img](D:\MyNote\images\zwps6.jpg) 

![img](D:\MyNote\images\zwps7.jpg) 

关于单双引号的问题：

双引号能够识别变量，双引号能够实现转义（类似于“”）

单引号是不能识别变量，只会原样输出，单引号是不能转义的

案例2：定义一个变量，输出当前时间，要求格式为“年-月-日 时:分:秒”。

![img](D:\MyNote\images\zwps8.jpg) 

注意：反引号（esc键下方的那个键），当在脚本中需要执行一些指令并且将执行的结果赋给变量的时候需要使用“反引号”。

![img](D:\MyNote\images\zwps9.jpg) 

#### 14.2.1.3.只读变量(了解)

语法：readonly 变量名

案例：定义变量a并且其值为10，随后设置其为只读变量，再去尝试重新赋值

![img](D:\MyNote\images\zwps10.jpg) 

![img](D:\MyNote\images\zwps11.jpg) 

#### 14.2.1.4.接收用户输入

语法：read -p 提示信息  变量名

案例：编写一个脚本test6.sh，要求执行之后提示用户输入文件的名称（路径），然后自动为用户创建该文件

![img](D:\MyNote\images\zwps12.jpg) 

![img](D:\MyNote\images\zwps13.jpg) 

#### 14.2.1.5.删除变量(了解)

语法：unset 变量名

案例：定义变量b=20，再输出b的值，随后删除b，最后再输出下b

![img](D:\MyNote\images\zwps14.jpg) 

![img](D:\MyNote\images\zwps15.jpg) 

### 14.2.2.条件判断语句

老婆给当程序员的老公打电话：下班顺路买一斤包子带回来，如果看到卖西瓜的，买一个。当晚，程序员老公手捧一个包子进了家门…老婆怒道：你怎么就买了一个包子？！老公答曰：因为看到了卖西瓜的。

把程序员老婆的话当作一段需求分析一下吧。买一斤包子是一个确定无疑的需求项，无论后面是什么情况什么条件，前面这一斤包子是肯定要买的。看到卖西瓜的是一个条件判断，后面“买一个”是一个模糊不清的需求项，买一个什么呢？需求里没说啊。客户把这个当作开发人员默认了解的内容了。可是作为一个成熟合格的程序员，该老婆的丈夫应该马上跟进确认需求“买一个什么？”，要不然程序可怎么写呢？所以笑话里该程序员是不合格的，起码是不积极不负责的。在没有明确需求的情况下，他只能按照自己的理解来完成工作了。那比较可能的结果就有如下几种：

1 看到卖西瓜的，买一个西瓜

​	如果 看到卖西瓜的

​		那么

​		买一个西瓜

​	否则

​		买一斤包子

2 看到卖西瓜的，买一个包子

​	如果 看到卖西瓜的

​		那么

​		买一个包子

3 看到卖西瓜的，买一个卖西瓜的

4 看到卖西瓜的，买一个老婆一直想买的东西

5 看到卖西瓜的，随便买一个东西



上述1和2下面的条件汉字描述称之为“伪代码”，也是属于条件表达式的语法。

**语法1**（一个条件）：

if condition

then

  command1 

  command2

  ...

fi

**单行写法**（一般在命令行中执行的时候）：if [ condition ]; then command; fi

**语法2**（两个条件）：

if condition

then

  command1 

  command2

  ...

else

  command

fi

**语法3**（多个条件）：

if condition1

then

  command1

elif condition2 

then 

  command2

else

  commandN

fi

### 14.2.3.运算符

在shell中，运算符和其他编程脚本语言一样，常见的有算数运算符、关系运算符、

逻辑运算符、字符串运算符、文件测试运算符等

#### 14.2.3.1.算数运算符

下表列出了常用的算术运算符，假定变量 a 为 10，变量 b 为 20：

| 运算符 | 说明                                            | 举例                            |
| ------ | ----------------------------------------------- | ------------------------------- |
| +      | 加法                                            | `expr $a + $b` 结果为 30。      |
| -      | 减法                                            | `expr $a - $b` 结果为 -10。     |
| *      | 乘法                                            | `expr $a  $b` 结果为  200。     |
| /      | 除法                                            | `expr $b / $a` 结果为 2。       |
| %      | 取余                                            | `expr $b % $a` 结果为 0。       |
| =      | 赋值                                            | a=$b 将把变量 b 的值赋给 a。    |
| ==     | 相等。用于比较两个数字，相同则返回 true（真）。 | [ $a == $b ] 返回 false（假）。 |
| !=     | 不相等。用于比较两个数字，不相同则返回 true。   | [ $a != $b ] 返回 true。        |

注意：条件表达式要放在方括号之间，并且要有空格，例如: [$a==$b] 是错误的，必须写成 [ $a == $b ]。

原生bash不支持简单的数学运算，但是可以通过其他命令来实现，例如 awk 和 expr，expr 最常用。

expr 是一款表达式计算工具，使用它能完成表达式的求值操作。

例如，两个数相加(注意使用的是反引号 ` 而不是单引号 ')：

\#!/bin/bash

val=\`expr 2 + 2\`

echo "两数之和为 : $val"

两点注意：

表达式和运算符之间要有空格，例如 2+2 是不对的，必须写成 2 + 2，这与我们熟悉的大多数编程语言不一样。

完整的表达式要被 \` \`包含，注意这个字符不是常用的单引号，在 Esc 键下边。

![img](D:\MyNote\images\1wps16.jpg) 

![img](D:\MyNote\images\zwps17.jpg) 

#### 14.2.3.2.关系运算符

关系运算符只支持数字，不支持字符串，除非字符串的值是数字。

下表列出了常用的关系运算符，假定变量 a 为 10，变量 b 为 20：

| 运算符 | 说明                                                  | 举例                       |
| ------ | ----------------------------------------------------- | -------------------------- |
| -eq    | 检测两个数是否相等，相等返回 true。                   | [ $a -eq $b ] 返回 false。 |
| -ne    | 检测两个数是否相等，不相等返回 true。                 | [ $a -ne $b ] 返回 true。  |
| -gt    | 检测左边的数是否大于右边的，如果是，则返回 true。     | [ $a -gt $b ] 返回 false。 |
| -lt    | 检测左边的数是否小于右边的，如果是，则返回 true。     | [ $a -lt $b ] 返回 true。  |
| -ge    | 检测左边的数是否大于等于右边的，如果是，则返回 true。 | [ $a -ge $b ] 返回 false。 |
| -le    | 检测左边的数是否小于等于右边的，如果是，则返回 true。 | [ $a -le $b ] 返回 true。  |

-eq：equal

-ne：not equal

-gt：great than

-lt：less than

-ge：great than or equal

-le：less than or equal

案例：使用a=10，b=20来实现本案例

![img](D:\MyNote\images\zwps18.jpg) 

![img](D:\MyNote\images\zwps19.jpg) 

课堂作业：

写一个脚本，判断当前输入的用户是否存在。如果存在则提示“用户存在”否则提示“用户不存在”。

![img](D:\MyNote\images\zwps20.jpg) 

#### 14.2.3.3.逻辑运算符

下表列出了常用的布尔运算符，假定变量 a 为 10，变量 b 为 20：

| 运算符 | 说明                                                | 举例                                     |
| ------ | --------------------------------------------------- | ---------------------------------------- |
| !      | 非运算，表达式为 true 则返回 false，否则返回 true。 | [ ! false ] 返回 true。                  |
| -o     | 或（或者）运算，有一个表达式为 true 则返回 true。   | [ $a -lt 20 -o $b -gt 100 ] 返回 true。  |
| -a     | 与（并且）运算，两个表达式都为 true 才返回 true。   | [ $a -lt 20 -a $b -gt 100 ] 返回 false。 |

或运算：一个为真即为真，全部为假才是假

与运算：一个为假即为假，全部为真才是真

![img](D:\MyNote\images\zwps21.jpg) 

#### 14.2.3.4.字符串运算符

下表列出了常用的字符串运算符，假定变量 a 为 "abc"，变量 b 为 "efg"：

| 运算符 | 说明                                      | 举例                     |
| ------ | ----------------------------------------- | ------------------------ |
| =      | 检测两个字符串是否相等，相等返回 true。   | [ $a = $b ] 返回 false。 |
| !=     | 检测两个字符串是否相等，不相等返回 true。 | [ $a != $b ] 返回 true。 |
| -z     | 检测字符串长度是否为0，为0返回 true。     | [ -z $a ] 返回 false。   |
| -n     | 检测字符串长度是否为0，不为0返回 true。   | [ -n $a ] 返回 true。    |
| str    | 检测字符串是否为空，不为空返回 true。     | [ $a ] 返回 true。       |

案例：将上述的语法验证下

![img](D:\MyNote\images\zwps22.jpg) 

#### 14.2.3.5.文件测试运算符

文件测试运算符用于检测 Unix/Linux 文件的各种属性。

属性检测描述如下：

| 操作符  | 说明                                                         | 举例                      |
| ------- | ------------------------------------------------------------ | ------------------------- |
| -b file | 检测文件是否是块设备文件，如果是，则返回 true。              | [ -b $file ] 返回 false。 |
| -c file | 检测文件是否是字符设备文件，如果是，则返回 true。            | [ -c $file ] 返回 false。 |
| -d file | 检测文件是否是目录，如果是，则返回 true。                    | [ -d $file ] 返回 false。 |
| -f file | 检测文件是否是普通文件（既不是目录，也不是设备文件），<br />如果是，则返回 true。 | [ -f $file ] 返回 true。  |
| -g file | 检测文件是否设置了 SGID 位，如果是，则返回 true。            | [ -g $file ] 返回 false。 |
| -k file | 检测文件是否设置了粘着位(Sticky Bit)，如果是，则返回 true。  | [ -k $file ] 返回 false。 |
| -p file | 检测文件是否是有名管道，如果是，则返回 true。                | [ -p $file ] 返回 false。 |
| -u file | 检测文件是否设置了 SUID 位，如果是，则返回 true。            | [ -u $file ] 返回 false。 |
| -r file | 检测文件是否可读，如果是，则返回 true。                      | [ -r $file ] 返回 true。  |
| -w file | 检测文件是否可写，如果是，则返回 true。                      | [ -w $file ] 返回 true。  |
| -x file | 检测文件是否可执行，如果是，则返回 true。                    | [ -x $file ] 返回 true。  |
| -s file | 检测文件是否为空（文件大小是否大于0），不为空返回 true。     | [ -s $file ] 返回 true。  |
| -e file | 检测文件（包括目录）是否存在，如果是，则返回 true。          | [ -e $file ] 返回 true。  |

案例：测试上述标绿色的效果

![img](D:\MyNote\images\zwps23.jpg) 

注意：权限几个判断，如果只有一个部分符合，则认为是有权限的。

### 14.2.4.shell脚本附带选项

问题描述：在linux shell中如何处理tail -10 access.log这样的命令行选项？

步骤：

​	调用tail指令

​	系统把后续选项传递给tail

​	Tail先去打开指定的文件

​	取出最后10行

问题：自己写的shell是否也可以像内置命令一样传递一些选项呢？

答：可以的，传递方式与上述的描述是一样的，关键是怎么接收。例如：

传递：

\#./test.sh  a  b  c

接收：

在脚本中可以用“$1”来表示a，“$2”来表示b，以此类推。

接收可以用“$”加上选项对应的序号即可。

测试：编写test14.sh，传递a，b，c，输出其值

![img](D:\MyNote\images\zwps24.jpg) 

其实$1、$2是变量。

练习：创建自定义指令“user”，可以直接执行，要求该指令具备以下语法和功能：

​	a. #user -add 用户名			【添加用户】

​	b. #user -del 用户名			【删除用户及其家目录】

![img](D:\MyNote\images\zwps251.jpg) 

同时题目中要求是指令，所以可以再去添加个别名：

![img](D:\MyNote\images\zwps261.jpg)

# 15.MySQL基础 

## 15.1.关于数据库

### 15.1.1.什么是数据库

![img](D:\MyNote\images\wps1x.jpg) 

如果一个项目是动态（内容会变化的，网页后缀.jsp、.php、.shtml等）内容的话，则数据库是必不可少的一个环节。

### 15.1.2.MySQL简介

MySQL是一个关系型数据库管理系统，由瑞典MySQL AB 公司开发，2008年被Sun公司收购，目前属于 Oracle 旗下产品。MySQL 是最流行的数据库管理系统之一，在 WEB 应用方面，MySQL是最好的 RDBMS (Relational Database Management System，关系数据库管理系统) 应用软件。其和php是黄金搭档（LAMP/LNMP）。

### 15.1.3.常见数据库

目前市场上还有：Oracle（重量级的数据库）、MS SQL Server（微软）、Access（微软）、PostgreSQL、DB2、Mariadb（MySQL分支，完全兼容MySQL）。

## 15.2.MySQL的安装与初始化

操作之前先确保计算机时间准确。

### 15.2.1.Linux下安装

#### 15.2.1.1.源码包

1.1.*优点*

开源，如果有足够的能力，可以修改源代码

编译安装，更加适合自己的系统，稳定高效

1.2.*缺点*

安装步骤较多，容易出错

编译过程时间较长

**案例**：使用源码编译安装方式安装ncurses（一种常用的终端库）

**扩展**：解包

常用语法：

​		#tar -zxvf *.tar.gz		（大多数）

​		#tar -jxvf *.tar.bz2

选项含义：

-z或--gzip或--ungzip：通过gzip指令处理文件；

-x或--extract或--get：从文件中还原文件；

-v：显示操作过程；

-f或--file：指定一个文件；

-j：支持bzip2解压文件；

①先将软件包传递到服务器上“/usr/local/src”

![img](D:\MyNote\images\wps2x.jpg) 

②解压需要安装的源码包

\# tar -zxvf ncurses-6.1.tar.gz

![img](D:\MyNote\images\wps3x.jpg) 

③切换到源码文件夹，然后执行后续操作

配置（config/configure/bootstrap） → 编译（make/bootstrapd） → 安装（make install/bootstrapd install）

配置操作主要是指定软件的安装目录、需要的依赖在什么地方、指定不需要可选依赖、配置文件的路径、通用数据存储位置等等。

指定安装的路径：--prefix=路径

需要依赖的路径：--with-PACKAGE名=[包所在的路径]

不需要依赖：--without-PACHAGE名

\# ./configure --prefix=/usr/local/ncurses

![img](D:\MyNote\images\wps4x.jpg) 

\# make

![img](D:\MyNote\images\xwps5.jpg) 

\# make install

![img](D:\MyNote\images\xwps6.jpg) 

成功之后查看目录（可选）：

![img](D:\MyNote\images\xwps7.jpg) 

#### 15.2.1.2.二进制包(rpm)

​	优点: 包管理系统简单，只需要几个命令就可以实现包的安装，升级，查询和卸载

​	缺点: 经过编译，不再可以看到源代码

回顾rpm相关指令：

\#rpm -qa|grep 关键词

\#rpm -e 关键词 [--nodeps]

\#rpm -ivh 完整名称

\#rpm -Uvh 完整名称

#rpm -qf 文件路径			【查询指定文件属于哪个包】

![img](D:\MyNote\images\xwps8.jpg) 

案例：使用二进制包安装lynx（一款纯命令行的浏览器）

在光盘中就有这个包

![img](D:\MyNote\images\xwps9.jpg) 

例如查看百度：#lynx --dump [www.baidu.com](http://www.baidu.com)

#### 15.2.1.3. yum等傻瓜式安装

优点: 安装简单，快捷

缺点: 完全丧失了自定义性

注意：如果不更改软件来源的情况下，是需要联网才能使用yum的。

常用的yum指令：

\#yum  list  [installed]  		列出当前已经装的和可以装的软件（全部）

\#yum search	名    		搜索指定的关键词的包

\#yum [-y]  install  包名		安装指定的包（-y表示允许不再确认）

\#yum  [-y]  update  [包名]		更新指定的包，不指定包则更新全部软件

\#yum [-y]  remove  包名		卸载指定的包

案例：使用yum指令卸载火狐浏览器

\#yum remove firefox

![img](D:\MyNote\images\xwps10.jpg) 

案例：使用yum指令安装火狐浏览器

\#yum install firefox

### 15.2.2.安装MySQL（重点）

注：此处安装以yum安装为例

#### 15.2.2.1.MySQL安装

\#yum install mysql-server

![img](D:\MyNote\images\xwps11.jpg) 

完成的：

![img](D:\MyNote\images\xwps12.jpg) 

#### 15.2.2.2.MySQL初始化

\#service mysqld start

![img](D:\MyNote\images\xwps13.jpg) 

查看端口号（默认端口号3306）：

![img](D:\MyNote\images\xwps14.jpg) 

\# mysql_secure_installation

Enter current password for root (enter for none):请输入当前root用户的密码，如果没有按回车，注意此root并非linux的root用户。

Set root password?是否设置root密码？

需要设置的密码：qhabOfhlluB9

Remove anonymous users?是否移除匿名用户，选择移除（Y）

Disallow root login remotely?是否不允许root远程登录（默认不允许）

Remove test database and access to it?是否移除测试数据库（建议先不移除）

Reload privilege tables now?是否重新加载权限表（当我们更改了mysql用户相关的信息之后建议去重载权限）

![img](D:\MyNote\images\xwps15.jpg) 

#### 15.2.2.3.MySQL的启动控制

语法：service mysqld start/stop/restart

进入mysql的方式：

\#mysql  -u用户名  -p

退出MySQL到linux命令行：

mysql > exit

#### 15.2.2.4.默认文件位置(了解)

数据库存储目录：/var/lib/mysql

配置文件：/etc/my.cnf

![img](D:\MyNote\images\xwps16.jpg) 

# 16.MySQL基本操作

## 16.1.名词介绍

以Excel文件举例：

数据库：可以看作是整个excel文件。

数据表：可以看作是一个excel文件中的工作表。

行（记录）：可以看作是一个工作表中的一行

列（字段）：可以看作是一个工作表总的一列

## 16.2.库操作（重点）

以下命令在MySQL终端命令行中执行（大小写均可）：

SHOW DATABASES;				显示当前MySQL中全部的数据库

CREATE DATABASE 库名;			创建数据库

DROP DATABASE 库名;			删除数据库

USE 库名;					切换数据库

Show databases效果

![img](D:\MyNote\images\zzwps1.jpg) 

创建数据库：创建yunwei数据库

![img](D:\MyNote\images\zzwps2.jpg) 

删除数据库：删除yunwei数据库

![img](D:\MyNote\images\zzwps3.jpg) 

切换数据库：切换到test数据库

![img](D:\MyNote\images\zzwps4.jpg) 

## 16.3.表操作

SHOW TABLES;				显示当前数据库中所有的表名（必须先use数据库）	

CREATE TABLE 表名称				在当前数据库下创建数据表

(

列名称1 数据类型 [NOT NULL AUTO_INCREMENT],

列名称2 数据类型,

列名称3 数据类型,

....,

PRIMARY KEY(主键字段名)

);

常见的数据类型：int（整型）、char（定长字符）、varchar（不定长字符）。

主键一般就是序号所在的那一列（主键不能重复）。

DESC 表名;				描述一个数据表（查看表结构）

DROP TABLE [IF EXISTS] 表名;			删除一个数据表

案例：使用上述的语法

查看所有的数据表

![img](D:\MyNote\images\zzwps5.jpg) 

创建数据表（去test库中创建）

要求：表名xg，要求有字段如下：

​	Id字段，11位整型，不为空，自增，主键

​	Username字段，varchar类型，20长度

​	Password字段，char类型，32长度

SQL（standard query language）语句：

Create table xg(

​	Id int(11) not null auto_increment,

Username varchar(20),

Password char(32),

Primary key(id)

);

![img](D:\MyNote\images\zzwps6.jpg) 

查看表结构：

![img](D:\MyNote\images\zzwps7.jpg) 

删除数据表：

![img](D:\MyNote\images\zzwps8.jpg) 

## 16.4.记录/字段操作（重点）

### 16.4.1.增加记录

语法1：INSERT INTO 表名称 VALUES (值1, 值2,....);

语法2：INSERT INTO 表名称 (列1, 列2,...) VALUES (值1, 值2,....);

案例：往数据表xg表中新增一个记录username为zhangsan，password为123456（加密结果E10ADC3949BA59ABBE56E057F20F883E）

Sql语句：

insert into xg (username,password) values (‘zhangsan’,’E10ADC3949BA59ABBE56E057F20F883E’)

![img](D:\MyNote\images\zzwps9.jpg) 

要求前面的列名与值要一一对应。

### 16.4.2.更新记录

语法：UPDATE 表名称 SET 列名称1 = 新值1,列名称2 = 新值2… WHERE 列名称 = 某值;

案例：使用更新语句更新id大于等于2的记录，将其密码改为：25F9E794323B453885F5181F1B624D0B

SQL语句：

Update xg set password = ‘25F9E794323B453885F5181F1B624D0B’ where id >= 2;

![img](D:\MyNote\images\zzwps10.jpg) 

以后在执行影响行数的sql操作的时候一定需要注意条件是否写错或者漏写。

### 16.4.3.查询记录

SELECT 列名称1,列名称2… FROM 表名称 WHERE 条件;

SELECT * FROM 表名称 WHERE 条件;

案例：查询刚才新增的记录

只查询用户名和密码，并且是id=2的：

Select username,password from xg where id = 2;

![img](D:\MyNote\images\zzwps11.jpg) 

查询全部：

Select * from xg;

![img](D:\MyNote\images\zzwps12.jpg) 

### 16.4.4.删除记录

DELETE FROM 表名称 WHERE 列名称 = 值

案例：删除id为2的记录

Delete from xg where id = 2;

![img](D:\MyNote\images\zzwps13.jpg) 

## 16.5.备份与还原（重点）

### 16.5.1.备份（导出）

全量备份（数据+结构）：    #mysqldump -uroot -p123456 -A > 备份文件路径

指定库备份（数据+结构）：# mysqldump -uroot -p123456 库名 > 备份文件路径

多个库备份（数据+结构）：# mysqldump -uroot -p123456 --databases db1 db2 >  备份文件路径

案例：备份整个库

\# mysqldump -uroot -pqhabOfhlluB9 -A > /root/sql_201804061609.sql

![img](D:\MyNote\images\zzwps14.jpg) 

案例：每1分钟自动备份1次test数据库

![img](D:\MyNote\images\zzwps15.jpg) 

计划任务编写：

![img](D:\MyNote\images\zzwps16.jpg) 

等待几分钟观察目录情况：

![img](D:\MyNote\images\aawps17.jpg) 

### 16.5.2.还原（导入）

还原部分分（1）mysql命令行source方法 和 （2）系统命令行方法

**1.还原全部数据库:**

(1) mysql命令行：mysql> source 备份文件路径

(2) 系统命令行： #mysql -uroot -p123456 < 备份文件路径

**2.还原单个数据库(需指定数据库)**

(1) mysql> use 库名

mysql> source 备份文件路径

(2) #mysql -uroot -p123456 库名 < 备份文件路径

3.还原单个数据库的多个表(需指定数据库)

(1) mysql> use 库名

mysql> source 备份文件路径

(2) mysql -uroot -p123456 库名 < 备份文件路径

4.还原多个数据库，（一个备份文件里有多个数据库的备份，此时不需要指定数据库）

(1) mysql命令行：mysql> source 备份文件路径

(2) 系统命令行： mysql -uroot -p123456 < 备份文件路径

案例1：人为删除xg表（模拟数据表丢失），然后通过最后一次备份还原数据表。

先删除数据表

![img](D:\MyNote\images\zzwps18.jpg) 

还原操作：

![img](D:\MyNote\images\zzwps19.jpg) 

案例2：需要还原sql文件到test库（mobile.sql 31万条数据）

![img](D:\MyNote\images\zzwps20.jpg) 

设置Mysql连接字符集：

​	Mysql> set names utf8;			【三码一致，服务器端+传输过程中+客户端】

![img](D:\MyNote\images\zzwps21.jpg) 

# 17.Mysql扩展

## 17.1.mysql的远程管理工具

分为两大类：B/S架构、C/S架构。

B/S：B是指浏览器，S是指服务器。例如：百度搜索应用就属于BS架构软件。

C/S：C是指客户端，S是指服务器。例如：QQ、电脑端微信等应用程序都是CS架构。

在BS中，mysql有个典型的管理工具：PMA（phpMyAdmin）

![img](D:\MyNote\images\zzwps22.jpg) 

CS中比较典型的软件：navicat、mysql workbrach

![img](D:\MyNote\images\zzwps23.jpg) 

要解决的问题：允许mysql远程登录

![img](D:\MyNote\images\zzwps24.jpg) 

a. 先进入数据库选择mysql数据库；

b. 执行sql语句：select host,user from user;

![img](D:\MyNote\images\zzwps25.jpg) 

c. 将其中的一个记录的host值改为“%”，表示可以允许任何地方登录

![img](D:\MyNote\images\zzwps26.jpg) 

d. 刷新权限表或者重启mysql

​	刷新权限：mysql> flush privileges;

![img](D:\MyNote\images\zzwps27.jpg) 

e. navicat登录成功

![img](D:\MyNote\images\zzwps28.jpg) 

 

# 18.其他

**分区设备别名**

+ /dev/hda1 （IDE硬盘接口）

+ /dev/sda1 （SCSI硬盘接口\SAST硬盘接口）

IDE硬盘接口与SCSI硬盘接口已被淘汰，现在基本是SAST硬盘接口

例：/dev/sdb5   sd指的是SAST硬盘接口，b是指第二块SAST硬盘接口，5 是指第一个逻辑分区

**格式化**

格式化是为了将分区划分为4kb的block（块），用于装载数据

**分区**

+ 必须分区
  + / --根分区
  + swap分区--交换分区
    + 如果真实内存小于4GB，swap为内存的两倍
    + 如果真实内存大于4GB，swap与内存一致
    + 实验环境不大于2GB
+ 推荐分区
  + /boot--启动分区 1GB
+ 常用分区
  + /home--用于文件服务器
  + /www--用于Web服务器