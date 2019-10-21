# 5.Git

## 5.1. 初始化本地库

git init:初始化一个Git仓库；

![1551873642007](D:\MyNote\images\1551873642007.png)

ll .git/:查看隐藏文件内部文件；

![1551873839648](D:\MyNote\images\1551873839648.png)

上方目录即为刚初始化的git仓库。

## 5.2.查看资源

ll:将当前路径下的资源详情进行罗列；

![1551872356867](D:\MyNote\images\1551872356867.png)

ls -lA:将当前路径下所有资源（包含隐藏资源）全部罗列出来；

![1551872570026](D:\MyNote\images\1551872570026.png)

ls -s|less:分屏查看上述罗列的资源（可以按Ctrl+z退出）；

cd  一个路径：进入这个路径；

![1551873080816](D:\MyNote\images\1551873080816.png)

mkdir WeChat:在当前目录下创建一个名为WeChat的文件夹；

![1551873439290](D:\MyNote\images\1551873439290.png)

ls lA|less:分屏罗列所有资源（包含隐藏资源）

![1551939435305](D:\MyNote\images\1551939435305.png)

pwd:查看当前路径

![1571666978423](D:\MyNote\images\1571666978423.png)

## 5.3. 设置签名

*☆*  形式：

​	→ 用户名：tom

​	→ Email地址：goodmorning@163.com

:cry:  作用：区分开发人员身份

:arrow_forward: 辨析：这里设置的签名与登录远程库的账号（代码托管中心）的账号、密码没有任何关系

:anchor: 命令：

​	:balloon:  项目级别/仓库级别：仅仅在本地库范围有效

​		◇ git config user.name jojo

​		◇ git config user.email jojo@163.com

​		◇ 数据存储位置：git内部的config文件

![1551938837933](D:\MyNote\images\1551938837933.png)

​	:balloon: 系统用户级别：登录当前操作系统的用户范围

​		◇ git config --global user.name admin

​		◇ git config --global user.email admin@163.com

​		◇ 数据存放位置：~/.gitconfig

![1551939564133](D:\MyNote\images\1551939564133.png)

​	:diamonds:  优先级：

​		◇ 就近原则：项目级别优先于系统用户级别

​		◇ 二者都没有是不被允许的

## 5.4.文件提交流程

> git开头的命令都是git自有的，与Linux不互通

:arrow_forward: git status：查看工作区、暂存区状态

:arrow_forward: vim good.txt:如果不存在，则创建一个名为good.txt的文件；如果已经存在，则进入编辑模式

创建文件后，会进入文件内部：

![1551941992581](D:\MyNote\images\1551941992581.png)

按i进入编辑模式

按Esc切换命令行模式，退出文件命令是:wq

此时再次键入git status命令会显示有新文件出现，提示可通过git add filename提交该文件

:arrow_forward: git add good.txt：提交文件进入暂存区

:arrow_forward: git rm --cached good.txt：将文件从暂存区删除

:arrow_forward: git commit:将文件从暂存区提交到本地库

:arrow_forward: git commit  -m "this is a log":将文件从暂存区提交到本地库，同时提交日志

commit后会进入一个vim编辑器界面，编辑一些关于此次修改的消息（注释或目的等）。

按esc从编辑模式切换到命令行后，写入命令:set nu，回车，可显示行号。同样用:wq退出。

![1551943272725](D:\MyNote\images\1551943272725.png)

## 5.5.本地库历史版本

:arrow_forward: cat good.txt:查看文件内容

:arrow_forward: git commit  -m "My second commited file is success!" good.txt:新加的-m可以直接编辑此次修改的消息，不需要进入vim编辑器模式

:arrow_forward: git log:查看git本地库的历史版本

:arrow_forward: git log --pretty=oneline:以一行显示一个历史版本

:arrow_forward: git log --oneline:以一行显示一个历史版本

:arrow_forward: git reflog:用一行显示一条历史记录，并显示从当前版本转移到另一个版本时需要转移的次数。

（HEAD@{1}表明需要转移一次）

以上四条命令结果如下图：

![1551945691939](D:\MyNote\images\1551945691939.png)

:arrow_forward: 多屏控制方式：空格向下翻页，按b向上翻页，按q退出

:arrow_forward: git reset --hard 版本号：通过基于索引值的方式，将版本返回到过去或未来的某个版本

![1551947157664](D:\MyNote\images\1551947157664.png)

![1551947515830](D:\MyNote\images\1551947515830.png)

 :arrow_forward: git reset --hard HEAD^^：通过控制^的数量将版本返回过去的某个版本。返回后通过git log --oneline的方式将不能在查看未来的版本历史记录。

![1551948162498](D:\MyNote\images\1551948162498.png)

:arrow_forward: git reset --hard HEAD~1:通过控制波浪线后的数字来控制返回到过去的某个版本。

![1551948474125](D:\MyNote\images\1551948474125.png)

:arrow_forward: reset/Ctrl+L：清屏

:arrow_forward: reset 的三个参数详解：reset实质上就是控制HEAD指针指向不同的历史版本

​	☆  soft:	 在本地库修改指针，

​	☆  mixed:在本地库修改指针，重置暂存区

​	☆  hard:  在本地库修改指针，重置暂存区、工作区（本地文件）

:arrow_forward: rm god.txt:删除一个文件

前提：删除文件前已将文件提交到本地库。将文件删除删除后，需将删除的文件提交到暂存区，此时可通过git reset --hard HEAD将工作区与暂存区进行重置，文件将会恢复到未删除的状态。通过git reset HEAD将暂存区进行重置，文件将恢复到刚删除还未提交状态。

## 5.6.比较版本差异

> HEAD表示指针，表示指针指向某个历史版本

:arrow_forward:  git diff  文件名：比较文件内容与暂存区中内容差异

:arrow_forward: git diff HEAD^ 文件名:将文件与某个历史版本进行比较

![1552011563480](D:\MyNote\images\1552011563480.png)

## 5.7.分支操作

:black_flag: git branch -v:查看各个分支

:black_flag: git branch 分支名：创建一个分支

![1552013385911](D:\MyNote\images\1552013385911.png)

:black_flag: git checkout 分支名：切换分支

![1552013526328](D:\MyNote\images\1552013526328.png)

:black_flag: git merge 分支名：合并分支

合并分支操作流程：首先需要切换到接收有新内容分支的分支--git checkout 负责接收的分支的名字，然后是这个分支接收有新内容分支--git merge 有新内容分支的名字。

![1552014492435](D:\MyNote\images\1552014492435.png)

合并分支时，如果遇到冲突，会这样被标记出来：

![1552016089154](D:\MyNote\images\1552016089154.png)

可在命令行时，在鼠标所在行敲d即可删除当前行。将内容修改完成后即可退出。通过git add 文件名，将冲突解决。但是此时合并未结束，需要提交到本地库才可以。通过git commit -m "修改消息或提示"即可结束合并。命令最后不可加入文件名。

![1552016619703](D:\MyNote\images\1552016619703.png)

## 5.8.向github推送和拉取

:black_flag: git remote -v:查看github地址

:black_flag: git remote add origin https://github.com/mikasamikodu/WeChat.git:向本地库添加一个推送地址https://github.com/mikasamikodu/WeChat.git，并起别名为origin。以后本地库可以向这个github地址进行推送和拉取数据。

![1552030425593](D:\MyNote\images\1552030425593.png)

:black_flag: git push origin master:将master分支推送到origin地址

![1552031292559](D:\MyNote\images\1552031292559.png)

:black_flag: git clone github项目地址:将github上的项目克隆到本地的仓库

![1552031837564](D:\MyNote\images\1552031837564.png)

克隆有三个效果：

​	a.完美地把远程库下载到本地；

​	b.创建origin远程地址别名；

​	c.初始化本地库；

:black_flag: git push origin master:向origin地址发送master分支内容

第一次push可能不会成功，因为没有向项目里推送的权限。需要对方先邀请你加入团队然后才可以推送数据。

邀请方式：点击标记处的settings

![1552035095384](D:\MyNote\images\1552035095384.png)

然后进入另一个地方：

![1552035176522](D:\MyNote\images\1552035176522.png)

点击左侧的collabortors，在右侧的搜索框填写需要邀请的账号，出现后点击搜索框右侧的按钮即可。会发送一封邮件到对方的注册邮箱中。

:black_flag: git fetch 地址别名 分支名:从远程库上抓取数据

:black_flag: git merge 地址别名/分支名:合并数据

:black_flag: git checkout 地址别名 分支名:切换路径，查看从远程库上抓取下来的数据

要点：如果不是github远程库上最新版所做的修改，不能推送，必须先拉取。拉取后如果产生冲突，则按照“分支冲突”解决即可。

## 5.9.生成SSH密匙

1.进入当前用户的家目录：$cd~

2.删除.ssh目录：$rm -r .ssh/

3.运用命令生成.ssh密匙目录:$ssh-keygen -t rsa -C 登录github的邮箱名，中间需要设定一些东西，只需要回车就可以。

4.进入.ssh目录:cd .ssh/

5.查看内部文件：$ll

6.查看文件：$cat id_rsa.pub，将文件内容复制，打开github个人设置-SSH and GPG keys。点击SSH keys的右上角new ssh key,将复制的内容放入key的文本域。在title部分编写一个标题（如mykey）即可。

7.进入工作区测试：cd 工作区地址，并修改工作区文件并提交。

8.在本地添加一个github的ssh地址：$ git remote add origin_ssh github上ssh地址名

9.查看地址：$git remote -v,然后推送数据,此时还需要确认一次是否推送，写入yes回车即可，最后显示成功。

## 5.10.加入.gitignore文件

项目中有许多不需要放入代码仓库的文件，可以通过.gitignore来忽略这些文件。

1.首先找到.gitconfig（C:/User/Administrator/.gitconfig），然后在这里建立一个java.gitignore文件(名称随便，后缀固定)，在里面加入如下内容：

```
# Compiled class file
*.class

# Log file
*.log

# BlueJ files
*.ctxt

# Mobile Tools for Java (J2ME)
.mtj.tmp/

# Package Files #
*.jar
*.war
*.nar
*.ear
*.zip
*.tar.gz
*.rar

# virtual machine crash logs, see http://www.java.com/en/download/help/error_hotspot.xml
hs_err_pid*
.classpath
.project
.setting
target
```



2.将java.gitignore的文件路径加入.gitconfig文件

打开.gitconfig文件，新建一个[core]，在下面加入如下路径：

excludesfile = C:/User/Administrator/java..gitignore。路径要用/连接，不能用\。

完成后可在eclipse中查看，路径window>preferences>team>git>configration>user settings。

## 5.11.通过eclipse使用git

### 5.11.1初始化本地库

在工程名上右击>team>share project>git>勾选左上角的单选框，如下：

![1552356505435](D:\MyNote\images\1552356505435.png)

勾选后，页面会变化，如下：

![1552356578010](D:\MyNote\images\1552356578010.png)

点击工程，下方的create Repository会由不可编辑变为可编辑状态，若编辑路径，可改变这个工程git本地库的位置。勾选工程，点击create按钮，然后点击finish即可将工程加入本地库。

### 5.11.2.设置签名

在菜单栏中，找到window，然后window>preferences>team>git>configuration如下：

![1552357017102](D:\MyNote\images\1552357017102.png)

在右侧界面选择user settings中,location位置不可编辑，是全局的gitconfig文件，负责管理本地所有git本地库。点击右侧的Add Entry...可以在key-value中添加数据，编辑gitconfig的配置文件。添加键值对如下：

![1552357287579](D:\MyNote\images\1552357287579.png)

全部完成后，点击apply即可完成设置。在repository setting中可以查看已经添加到git的工程的配置。

### 5.11.3.添加.gitignore文件

参考5.10

### 5.11.4.add and commit

首先修改文件，文件将会变化，如下：

![1552357744301](D:\MyNote\images\1552357744301.png)



然后在此文件上右击>team>add to index，此时文件将会被加入暂存区。

也可以直接commit，同样右击>team>commit，如下：

![1552357877562](D:\MyNote\images\1552357877562.png)

unstaged changes区是修改后未加入暂存区的文件，staged changes区是修改后已加入暂存区的文件，

commit message指的是修改的日志，最后点击右下角的commit,即可将修改提交到本地库。

### 5.11.5.push

右击项目>team>remote>push，结果如下：

![1552358152220](D:\MyNote\images\1552358152220.png)

此时需要将远程库的地址加入URI的文本框（确保远程库上已有这个项目的远程库），hosts与repository path，将会根据uri自动填充。然后在user和password中写上远程库的用户名与密码，并勾选左下角的store in secure store，可以在本地存储远程库的用户名与密码。点击next，如下：

![1552358649740](D:\MyNote\images\1552358649740.png)

点击途中红框处的add add branches spec，课件给所有分支选中添加到下方的框中，点击next,可编辑修改日志，如下：

![1552358781933](D:\MyNote\images\1552358781933.png)

也可以直接点击finish完成推送（中间会有几秒等待时间才会返回结果，点击close关闭结果界面即可）。

### 5.11.6.克隆

在左侧项目处右击>import>git>projects from git>clone uri，结果如下：

![1552359607103](D:\MyNote\images\1552359607103.png)

操作同上，将远程库地址复制放入uri中，填写user and passowrd，勾选store in secure store，点击next,选择需要clone的分支，点击next，选择本地库放置位置（最好选择eclipse的项目放置位置，方便eclipse管理），加入工程名称，点击确定，点击next，结果如下：

![1552360239841](D:\MyNote\images\1552360239841.png)

这是要求选择向eclipse导入项目的方式，选第三个import as general project，点击next，点击finish即可。

此时目录结构松散难以使用，点击右键>configure>convert to meven project即可。此方法只适用于meven工程。

### 5.11.7.解决冲突

同时修改同一项目的2个本地库，将其中一个修改提交，并推送到远程库，另一项目推送会失败：

![1552361706285](D:\MyNote\images\1552361706285.png)

此时，需要先拉取下来远程库资源，解决冲突在推送。先拉取内容，	点击右键>team>

第二个pull，将远程库的地址放入uri中，填写user和pasword，用远程库的用户名与密码，勾选左下角的框。

产生冲突时，如下：

![1552362149178](D:\MyNote\images\1552362149178.png)

可通过右击>team>merge pool,结果如下：

![1552370845074](D:\MyNote\images\1552370845074.png)

对比两侧内容，左侧可以修改，右侧不可修改，修改左侧内容。将内容修改完毕，进行提交，最后push到远程库即可。

### 5.11.8.管理分支

首先创建分支，右键>team>new branch，填写新分支名称，点击finish即可。之后可以正常提交并推送分支。

可以通过右键>team>switch to>master切换分支。

如果远程库上有分支，但是本地库没有，则需要如此做：

首先切换到主分支，然后右键>team>switch to>other,结果如下：

![1552372175314](D:\MyNote\images\1552372175314.png)

点击remote tracking,将本地库没有的分支选中，点击下方的check out,然后选择如下：

![1552372253798](D:\MyNote\images\1552372253798.png)

点击即可。