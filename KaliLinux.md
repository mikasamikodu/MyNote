1.apt-get install linux-header-$(uname -r)

指令解读：

​	apt-get  install：到官网去执行安装的操作

​	install  linux-header:安装linux的头文件

​	-$(uname -r)：指定头文件所属的硬件平台，通过uname -r的指令查出来

2.1.apt-get update：更新linux的索引文件

# 3.更新源 升级软件和内核等

ISO文件下载地址：https://www.kali.org/downloads/

说下安装后的升级操作。下面的操作都是在root下进行的，避免有些指令不可用或文件打不开。

**1. 先确定自己是什么版本：lsb_release -a**

![img](D:\MyNote\images\658978-20170405133200675-1959000901.png)

**2. 用文本编辑器打开sources.list,手动添加下面的更新源（这里只写了中科大的源，可用，其他的在附录，可自行选择）**

```
root@HackerKali:/home/dnt# leafpad /etc/apt/sources.list
#中科大
deb http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib
deb-src http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib
```

**3..添加完毕后执行下面的更新指令，进行系统或者工具的更新**

```
root@HackerKali:/home/dnt# apt-get update && apt-get upgrade && apt-get dist-upgrade 
```

这里解释一下：

apt-get update //刷新源，获得最近的软件包的列表

apt-get upgrade //更新系统，系统将现有的Package升级,如果有相依性的问题,而此相依性需要安装其它新的Package或影响到其它Package的相依性时,此Package就不会被升级,会保留下来.

apt-get dist-upgrade //可以聪明的解决相依性的问题,如果有相依性问题,需要安装/移除新的Package,就会试着去安装/移除它. (所以通常这个会被认为是有点风险的升级，可以不用执行)

**4.清理安装包：apt-get clean**

**5.** **安装内核头文件**

方法1：输入命令：apt-get install linux-headers-$(uname -r)或者直接敲apt-get install linux-headers-在这时候你按键盘上的tab键，找你本系统的头文件安装即可

**如果找不到对应的内核头文件\**或者出现以下错误\**则进入方法2**

```
E: Unable to locate package linux-headers-4.6.0-kali1-amd64 
E: Couldn't find any package by glob 'linux-headers-4.6.0-kali1-amd64
E: Couldn't find any package by regex 'linux-headers-4.6.0-kali1-amd64
```

**内核头文件检测**

输入命令：`dpkg-query -s linux-headers-'``uname` `-r'`或者dpkg-query -s linux-headers-$(uname -r) 命令检查内核头文件是否成功安装

方法2：**下载内核头文件自己编译**

1.下载inux-kbuild,链接:(http://http.kali.org/kali/pool/main/l/linux/)具体版本参见自己的主机；

2.编译linux-kbuild; 

```
dkpg -i linux-kbuild-4.6_4.6.1-2kali1_amd64.deb
如果出现错误：dpkg: error: dpkg status database is locked by another process
则执行命令：sudo rm -rf /var/lib/dpkg/lock
```

3.下载linux-header-common和主机版本对应的linux-header。(执行uname -r命令查看主机版本)

链接（http://http.kali.org/kali/pool/main/l/linux/）,具体版本参见自己的主机

4.首先编译linux-header-common 

```
dkpg -i linux-headers-4.6.0-kali1-common_4.6.1-5kali4_amd64.deb
```

5.最后编译linux-header 

```
dkpg -i linux-headers-4.6.0-kali1-amd64_4.6.1-5kali4_amd64.deb
```

这一步可能会报错，提示依赖compiler未安装。

安装apt-get install linux-compiler-gcc-xx(版本号保持提示缺少的版本号)，再编译header即可。

```
6.检测内核头文件
```

dpkg-query -s linux-headers-$(uname -r)

**6.** **开启sshd**

```
vi /etc/ssh/sshd_config
```

1.增加一行`PermitRootLogin yes`
2.将`#PasswordAuthentication no`改为`PasswordAuthentication yes`

![img](D:\MyNote\images\504727-20170920100709681-406266053.png)

按esc 输入`:wq!`保存文件。

```
/etc/init.d/ssh start #启动sshd
/etc/init.d/ssh status #查看SSH服务状态是否正常运行
```

在其他机器ssh连接即可

### 附录：

**---------------------------------Kali 2.0 ---更新源-----------------------------------**

**kali-rolling版本：（中科大的就够用了，个人按需吧）

```
#中科大
deb http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib
deb-src http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib

#阿里云
#deb http://mirrors.aliyun.com/kali kali-rolling main non-free contrib
#deb-src http://mirrors.aliyun.com/kali kali-rolling main non-free contrib

#清华大学
#deb http://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free
#deb-src https://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free

#浙大
#deb http://mirrors.zju.edu.cn/kali kali-rolling main contrib non-free
#deb-src http://mirrors.zju.edu.cn/kali kali-rolling main contrib non-free

#东软大学
#deb http://mirrors.neusoft.edu.cn/kali kali-rolling/main non-free contrib
#deb-src http://mirrors.neusoft.edu.cn/kali kali-rolling/main non-free contrib

#官方源
#deb http://http.kali.org/kali kali-rolling main non-free contrib
#deb-src http://http.kali.org/kali kali-rolling main non-free contrib

#重庆大学
#deb http://http.kali.org/kali kali-rolling main non-free contrib
#deb-src http://http.kali.org/kali kali-rolling main non-free contrib
```



**sana版本：（其实你把上面的版本都改成sana就可以了）**

**#科大的云**
**deb http://mirrors.ustc.edu.cn/kali sana main non-free contrib**
**deb-src http://mirrors.ustc.edu.cn/kali sana main non-free contrib**
**deb http://mirrors.ustc.edu.cn/kali-security sana/updates main contrib non-free**


**#阿里云**
**deb http://mirrors.aliyun.com/kali sana main non-free contrib**
**deb-src http://mirrors.aliyun.com/kali sana main non-free contrib**
**deb http://mirrors.aliyun.com/kali-security sana/updates main contrib non-free**



**----------------------------------Kali 1.0--更新源-------------------------------------**

```
#官方源
deb http://http.kali.org/kali kali main non-free contrib
deb-src http://http.kali.org/kali kali main non-free contrib
deb http://security.kali.org/kali-security kali/updates main contrib non-free

#中科大kali源
deb http://mirrors.ustc.edu.cn/kali kali main non-free contrib
deb-src http://mirrors.ustc.edu.cn/kali kali main non-free contrib
deb http://mirrors.ustc.edu.cn/kali-security kali/updates main contrib non-free

#新加坡kali源
deb http://mirror.nus.edu.sg/kali/kali/ kali main non-free contrib
deb-src http://mirror.nus.edu.sg/kali/kali/ kali main non-free contrib
deb http://security.kali.org/kali-security kali/updates main contrib non-free
deb http://mirror.nus.edu.sg/kali/kali-security kali/updates main contrib non-free
deb-src http://mirror.nus.edu.sg/kali/kali-security kali/updates main contrib non-free

#阿里云kali源
deb http://mirrors.aliyun.com/kali kali main non-free contrib
deb-src http://mirrors.aliyun.com/kali kali main non-free contrib
deb http://mirrors.aliyun.com/kali-security kali/updates main contrib non-free

#163 Kali源
deb http://mirrors.163.com/debian wheezy main non-free contrib 
deb-src http://mirrors.163.com/debian wheezy main non-free contrib 
deb http://mirrors.163.com/debian wheezy-proposed-updates main non-free contrib 
deb-src http://mirrors.163.com/debian wheezy-proposed-updates main non-free contrib 
deb-src http://mirrors.163.com/debian-security wheezy/updates main non-free contrib 
deb http://mirrors.163.com/debian-security wheezy/updates main non-free contrib


#上海交大 Kali源 (比较慢，直接忽略)
#deb http://ftp.sjtu.edu.cn/debian wheezy main non-free contrib
#deb-src http://ftp.sjtu.edu.cn/debian wheezy main non-free contrib 
#deb http://ftp.sjtu.edu.cn/debian wheezy-proposed-updates main non-free contrib 
#deb-src http://ftp.sjtu.edu.cn/debian wheezy-proposed-updates main non-free contrib 
#deb http://ftp.sjtu.edu.cn/debian-security wheezy/updates main non-free contrib 
#deb-src http://ftp.sjtu.edu.cn/debian-security wheezy/updates main non-free contrib
```



​	

