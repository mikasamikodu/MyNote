# 2． HTML

## 2.1.笔记

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <!--meta主要用于设置网站元数据
        charset 指定网页字符集
        name   指定数据的名称
        content   指定数据的内容

        keywords 表示网站关键字，可以同时指定多个关键字，关键字之间用,隔开
        <meta name="keywords" content="苏宁易购网上商城,苏宁电器,Suning,手机,电脑,冰箱,洗衣机,相机,数码,家居用品,鞋帽,化妆品,母婴用品,图书,食品,正品行货">
        description指定网站的描述。网站描述会显示是在搜索结果中，标题下方的描述文字便是网站描述
        <meta name="description" content="苏宁易购-综合网上购物平台，商品涵盖家电、手机、电脑、超市、母婴、服装、百货、海外购等品类。送货更准时、价格更超值、上新货更快，正品行货、全国联保、可门店自提，全网更低价，让您放心去喜欢！">
        title  指定网页所在标签页的标题，同时指定百度搜索结果的标题
        <meta http-equiv="refresh" content="3;url=https://www.baidu.com">3秒后跳转到百度，用于跳转网站
    -->
    <title>meta标签</title>
</head>
<body>

<!--段落标签，块元素
    浏览器解析网页时会对不符合规范网页内容进行修正
        例如：1.标签写在根元素外面
             2.p元素内嵌套块元素
             3.根元素中出现了除head或body外的标签
             。。。
-->
<p>段落标签</p>

<!--
    header标签：表示网页的头部，块元素
    main标签：表示网页的主体，块元素
    footer标签：表示网页的底部，块元素
    nav标签：表示网页导航，块元素
    aside标签：表示主体相关内容，如侧边栏，块元素
    article标签：表示独立的文章，块元素
    section标签：表示一个独立的区块，块元素
    span标签：无语义，一般表示选中的文字，行元素
    div标签：无语义，表示一个区块，主要用于布局，块元素
-->
<header>header标签</header>
<main>main标签</main>
<footer>footer标签</footer>
<nav>nav标签</nav>
<aside>aside标签</aside>
<article>article表示独立的文章</article>
<section>section表示一个独立的区块</section>
</body>
</html>
```



## 2.2. 无序序列ul

> *a*   :如何让无序序列的序号消失？

```css
<style type='text/css'>
li{
    list-style:none;
}
</style>
```



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<!--
    无序列表是一个项目的列表，此列项目使用粗体圆点（典型的小黑圆圈）进行标记。
    无序列表使用 <ul> 标签
    同样，有序列表也是一列项目，列表项目使用数字进行标记。 有序列表始于 <ol> 标签。每个列表项始于 <li> 标签。
    列表项使用数字来标记。
    自定义列表不仅仅是一列项目，而是项目及其注释的组合。
    自定义列表以 <dl> 标签开始。每个自定义列表项以 <dt> 开始。
                             每个自定义列表项的定义以 <dd> 开始
-->
<ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
</ul>
<ol>
    <li>Coffee</li>
    <li>Milk</li>
</ol>
<dl>
    <dt>Coffee</dt>
    <dd>- black hot drink</dd>
    <dt>Milk</dt>
    <dd>- white cold drink</dd>
</dl>
</body>
</html>
```



## 2.3. 音频audio

> 定义

定义声音，比如音乐或其他音频流。但是引入时默认用户无法暂停播放

> 示例

```html
<audio src="mp3/1.mp3" controls></audio>
```

> 属性

| 属性     | 值             | 描述                                                         |
| -------- | -------------- | ------------------------------------------------------------ |
| autoplay | autoplay       | 如果出现该属性，则音频在就绪后马上播放。但是大部分浏览器不支持，在谷歌浏览器有效 |
| controls | controls       | 如果出现该属性，则向用户显示控件，比如播放按钮。             |
| preload  | auto,meta,none | 如果出现该属性，则音频在页面加载时进行加载，并预备播放。如果使用 "autoplay"，则忽略该属性。 |
| loop     | loop           | 如果出现该属性，则每当音频结束时重新开始播放。               |
| src      | url            | 要播放的音频的 URL。                                         |
| muted    | muted          | 加了muted属性，**音频即使在播放的时候，也是没有声音**，除非用户手动调整控制面板的音量。 |

> 提示

可以在开始标签和结束标签之间放置文本内容，这样老的浏览器就可以显示出不支持该标签的信息。

除了通过src指定还可以通过source指定资源所在

```html
<audio>    
    你浏览器不支持，请升级(提示语)    
    <source src=""/>
</audio>
老版浏览器支持的音频标签：embed，会在页面打开时自动播放
<embed src="source/a.mp3" type="audio/mp3"> </embed>
```



```html
兼容老版本浏览器办法
<audio controls>
    <source src="source/a.mp3"/><!--mp3目前大部分浏览器都支持-->
    <source src="source/a.mp3"/><!--ogg用于偏门浏览器支持-->
    <embed src="source/a.mp3" type="audio/mp3">
</audio>
```



## 2.4. 视频video

> 定义

定义视频，比如电影片段或其他视频流。

> 提示

可以在开始标签和结束标签之间放置文本内容，这样老的浏览器就可以显示出不支持该标签的信息。

> 示例

```html
<video src="movie.ogg" controls="controls">
您的浏览器不支持 video 标签。
</video>
<video>
        <source src="movie.mp4" type="video/mp4">
        <source src="movie.ogg" type="video/ogg">
        浏览器太老啦，该换了！
 </video>
```

> 属性

| 属性     | 值       | 描述                                                         |
| -------- | -------- | ------------------------------------------------------------ |
| autoplay | autoplay | 如果出现该属性，则视频在就绪后马上播放。                     |
| controls | controls | 如果出现该属性，则向用户显示控件，比如播放按钮。             |
| height   | pixels   | 设置视频播放器的高度。                                       |
| loop     | loop     | 如果出现该属性，则当媒介文件完成播放后再次开始播放。         |
| preload  | preload  | 如果出现该属性，则视频在页面加载时进行加载，并预备播放。如果使用 "autoplay"，则忽略该属性。 |
| src      | *url*    | 要播放的视频的 URL。                                         |
| width    | *pixels* | 设置视频播放器的宽度。                                       |



兼容老版本浏览器办法

```html
<video  controls width="500px" height="300px">
    <source src="source/4.mp4"/><!--mp4目前大部分浏览器都支持-->
    <source src="source/4.webm"/><!--webm用于偏门浏览器支持-->
    <embed src="source/4.mp4" type="audio/mp4">
</video>
```



## 2.5. 表格table

> 示例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
<!--        在现实生活中，我们经常使用表格来表示一些格式化数据
            例如课程表，人名单，成绩单
            同样在网页中，我们也需要使用表格，我们可以通过table标签来创建一个表格
-->
    </style>
</head>
<body>
<!--table标签创建表格-->
    <table border="1" align="center" width="30%">
<!--table标签内部的tr标签创建表格的一行-->
        <tr>
<!--            tr标签内部的td标签代表一个单元格-->
            <td>1</td>
<!--           rowspan 代表向下合并2个单元格 ，对应单元格位置是空的才可以-->
            <td rowspan="2">2</td>
<!--           colspan代表向右合并2个单元格 ，对应单元格位置是空的才可以-->
            <td colspan="2">3</td>
        </tr>
        <tr>
            <td>1</td>
            <td>3</td>
            <td>4</td>
        </tr>
        <tr>
            <td>1</td>
            <td>2</td>
            <td>3</td>
            <td>4</td>
        </tr>
    </table>

</body>
</html>
```



> 效果

![1551236855439](D:\MyNote\images\1551236855439.png)

> 定义与语法

<table> 标签定义 HTML 表格。

简单的 HTML 表格由 table 元素以及一个或多个 tr、th 或 td 元素组成。

tr 元素定义表格行，th 元素定义表头，td 元素定义表格单元。

更复杂的 HTML 表格也可能包括 caption、col、colgroup、thead、tfoot 以及 tbody 元素。

> 属性

| 属性                                                         | 值                                                        | 描述                                                         |
| ------------------------------------------------------------ | --------------------------------------------------------- | ------------------------------------------------------------ |
| [align](http://www.w3school.com.cn/tags/att_table_align.asp) | left、center、right                                       | 不赞成使用。请使用样式代替。规定表格相对周围元素的对齐方式。 |
| [bgcolor](http://www.w3school.com.cn/tags/att_table_bgcolor.asp) | rgb(x,x,x)、#xxxxxx、colorname                            | 不赞成使用。请使用样式代替。规定表格的背景颜色。             |
| [border](http://www.w3school.com.cn/tags/att_table_border.asp) | 数字                                                      | 规定表格边框的宽度。                                         |
| [cellpadding](http://www.w3school.com.cn/tags/att_table_cellpadding.asp) | 百分数、数字                                              | 规定单元边沿与其内容之间的空白。                             |
| [cellspacing](http://www.w3school.com.cn/tags/att_table_cellspacing.asp) | 百分数、数字                                              | 规定单元格之间的空白。                                       |
| [frame](http://www.w3school.com.cn/tags/att_table_frame.asp) | void、above、below、hsides、lhs、rhs、vsides、box、border | 规定外侧边框的哪个部分是可见的。                             |
| [rules](http://www.w3school.com.cn/tags/att_table_rules.asp) | nonegroupsrowscolsall                                     | 规定内侧边框的哪个部分是可见的。                             |
| [summary](http://www.w3school.com.cn/tags/att_table_summary.asp) | text                                                      | 规定表格的摘要。                                             |
| [width](http://www.w3school.com.cn/tags/att_table_width.asp) | 百分数、数字                                              | 规定表格的宽度。                                             |



## 2.6.链接标签

HTML使用标签 <a>来设置超文本链接。在标签<a> 中使用了href属性来描述链接的地址。默认情况下，链接将以以下形式出现在浏览器中：
	一个未访问过的链接显示为蓝色字体并带有下划线。
	访问过的链接显示为紫色并带有下划线。
	点击链接时，链接显示为红色并带有下划线。

```html
<a href="https://www.runoob.com/">访问菜鸟教程</a>
```



alt属性用于图片无法显示时而显示，同时搜索引擎会根据图片的alt属性识别图片

使用 target 属性，你可以定义被链接的文档在何处显示。默认值是_self
下面的这行会在新窗口打开文档：

```html
<a href="https://www.runoob.com/" target="_blank">访问菜鸟教程!</a>
```



id属性可用于创建在一个HTML文档书签标记。

> 提示: 书签是不以任何特殊的方式显示，在HTML文档中是不显示的，所以对于读者来说是隐藏的。>

```html
在HTML文档中插入ID:
<a id="tips">有用的提示部分</a>
在HTML文档中创建一个链接到"有用的提示部分(id="tips"）"：
<a href="#tips">访问有用的提示部分</a>
或者，从另一个页面创建一个链接到"有用的提示部分(id="tips"）"：
<a href="https://www.runoob.com/html/html-links.html#tips">
访问有用的提示部分</a>
```



HTML 中 href、src 区别
href 是 Hypertext Reference 的缩写，表示超文本引用。用来建立当前元素和文档之间的链接。常用的有：link、a。例如：`<link href="reset.css" rel="stylesheet"/>`
浏览器会识别该文档为 css 文档，并行下载该文档，并且不会停止对当前文档的处理。这也是建议使用 link，
而不采用 @import 加载 css 的原因。 src 是 source 的缩写，src 的内容是页面必不可少的一部分，是引入。
src 指向的内容会嵌入到文档中当前标签所在的位置。常用的有：img、script、iframe。
例如:`<script src="script.js"></script>`
当浏览器解析到该元素时，会暂停浏览器的渲染，直到该资源加载完毕。这也是将js脚本放在底部而不是头部得原因。
简而言之，src 用于替换当前元素；href 用于在当前文档和引用资源之间建立联系。

```html
使用#作为超链接的占位符，可以保持超链接的样式，不会变成普通的字
<a href="#">占位符，点击不跳转，只会回到页面顶部</a>
<a href="javascript:;">占位符，点击无反应</a>
```



**关于创建电子邮件链接时如何发送邮件内容**

在进行邮件内容发送时，需要使用关键字：**mailto**

示例如下：

```
<a href="mailto:zhangrr601@163.com?subject=这是邮件的主题&body=这是邮件的内容" rel="nofollow">发送邮件</a>
```



这样会调启系统默认的邮件程序发送给 zhangrr601@163.com，并且收件人那里已经填上了我邮箱的地址。

关于创建电子邮件链接时如何进行抄送，密送.

在进行抄送时，需要使用关键字：**cc**

在进行密送时，需要使用关键字：**bcc**

英文名称：Carbon Copy，又简称为 CC。在网络术语中，抄送就是将邮件同时发送给收信人以外的人，用户所写的邮件抄送一份给别人，对方可以看见该用户的 E-mail。同收件人地址栏一样，不可以超过 1024 个字符。一般来说，使用"抄送"服务时，多人抄送的电子邮件地址使用 **;** 分隔。

**密件抄送：**

英文名称：Blind Carbon Copy ，又称“盲抄送”，和抄送的唯一区别就是它能够让各个收件人无法查看到这封邮件同时还发送给了哪些人。密件抄送是个很实用的功能，假如一次向成百上千位收件人发送邮件，最好采用密件抄送方式，这样一来可以保护各个收件人的地址不被其他人轻易获得，二来可以使收件人节省下收取大量抄送的 E-mail 地址的时间。

示例如下：

```
<a href="mailto:zhangrr601@163.com?cc=someone@163.com&bcc=somebody@163.com" rel="nofollow">发送邮件</a>
```



nofollow 是 HTML 页面中 a 标签的属性值。这个标签的意义是告诉搜索引擎"不要追踪此网页上的链接或不要追踪此特定链接"。

nofollow 是 HTML 页面中 a 标签的属性值。它的出现为网站管理员提供了一种方式，即告诉搜索引擎"不要追踪此网页上的链接"或"不要追踪此特定链接"。这个标签的意义是告诉搜索引擎这个链接不是经过作者信任的，所以这个链接不是一个信任票。

参数说明：

| 参数                    | 描述             |
| :---------------------- | :--------------- |
| mailto:*name@email.com* | 邮件接收地址     |
| cc=*name@email.com*     | 抄送地址         |
| bcc=*name@email.com*    | 密件抄送地址     |
| subject=*subject text*  | 邮件主题         |
| body=*body text*        | 邮件内容         |
| ?                       | 第一个参数分隔符 |
| &                       | 其他参数分隔符   |

注：多个邮件地址用 **;** 隔开，空格用 **%20** 代替。

```
<a href="http://www.runoob.com/" target="_blank" rel="noopener noreferrer">访问菜鸟教程!</a> 
```

后面最好加上：

```
rel="noopener noreferrer"
```

意思是不会打开其他的网站，因为恶意病毒可能会修改你的浏览器空白页地址。

## 2.7.图片标签

在 HTML 中，图像由<img> 标签定义。

<img> 是空标签，意思是说，它只包含属性，并且没有闭合标签。

要在页面上显示图像，你需要使用源属性（src）。src 指 "source"。源属性的值是图像的 URL 地址。

**定义图像的语法是：**

```html
<img src="url" alt="some_text"/>
```



alt 属性用来为图像定义一串预备的可替换的文本。

替换文本属性的值是用户定义的。

```html
<img src="boat.gif" alt="Big Boat">
```



在浏览器无法载入图像时，替换文本属性告诉读者她们失去的信息。此时，浏览器将显示这个替代性的文本而不是图像。为页面上的图像都加上替换文本属性是个好习惯，这样有助于更好的显示信息，并且对于那些使用纯文本浏览器的人来说是非常有用的。

height（高度） 与 width（宽度）属性用于设置图像的高度与宽度。

属性值默认单位为像素:

```html
<img src="pulpit.jpg" alt="Pulpit rock" width="304" height="228">
```



**提示:** 指定图像的高度和宽度是一个很好的习惯。如果图像指定了高度宽度，页面加载时就会保留指定的尺寸。如果没有指定图片的大小，加载页面时有可能会破坏HTML页面的整体布局。

**HTML 图像标签**

| 标签   | 描述                       |
| :----- | :------------------------- |
| <img>  | 定义图像                   |
| <map>  | 定义图像地图               |
| <area> | 定义图像地图中的可点击区域 |



示例"[创建图像映射](https://www.runoob.com/try/try.php?filename=tryhtml_areamap)"中的代码：

```html
<map name="planetmap">
  <area shape="rect" coords="0,0,82,126" alt="Sun" href="sun.htm">
  <area shape="circle" coords="90,58,3" alt="Mercury" href="mercur.htm">
  <area shape="circle" coords="124,58,8" alt="Venus" href="venus.htm">
</map>
```

该段代码中的shape指的是点击区域的形状，coords指的应该是链接区域在图片中的坐标（像素为单位）

1、矩形：(左上角顶点坐标为(x1,y1)，右下角顶点坐标为(x2,y2))

```html
<area shape="rect" coords="x1,y1,x2,y2" href=url>
```

2、圆形：(圆心坐标为(X1,y1)，半径为r)

```php+HTML
<area shape="circle" coords="x1,y1,r" href=url>
```

3、多边形：(各顶点坐标依次为(x1,y1)、(x2,y2)、(x3,y3) ......)

```html
<area shape="poly" coords="x1,y1,x2,y2 ......" href=url>
```



常见图片：

​	jpeg(jpg):

​		支持颜色较丰富，不支持透明效果，不支持动图

​		一般用于显示照片

​	git:

​		支持颜色少，支持简单透明，支持动图

​		适合颜色单一的图片，动图

​	png：

​		支持颜色丰富，支持透明效果，不支持动图

​		适合颜色丰富，复杂透明的图片

​	上面选择方法：效果相同，选小的；效果不同选好的

​	webp:是谷歌新推出的专门用来显示网页中图片的格式

​		支持颜色丰富，支持透明效果，支持动图

​		具备所有优点还小，但是兼容性不好

​	base64:

​		将图片进行base64编码，这样可以将图片转化为字符，通过字符的形式引入图片

​		一般用于需要和网页一同加载的图片才需要

## 2.8.标题标签

标题标签,一般只用h1~h3,块元素
标题大小与字体大小的关系
1到6号标题与1到6号字体逆序对应，比如1号字体对应6号标题，2号字体对应5号标题。

```html
<h1>这是1号标题</h1>
<font size="6">这是6号字体文本</font>

<h2>这是2号标题</h2>
<font size="5">这是5号字体文本</font>

<h3>这是3号标题</h3>
<font size="4">这是4号字体文本</font>

<h4>这是4号标题</h4>
<font size="3">这是3号字体文本</font>

<h5>这是5号标题</h5>
<font size="2">这是2号字体文本</font>

<h6>这是6号标题</h6>
<font size="1">这是1号字体文本</font>

```

效果：

![1583763419973](D:\MyNote\images\1583763419973.png)



```html
<!--hgroup-->
<hgroup>
    <h1>崩坏3</h1>
    <h2>琪亚娜</h2>
</hgroup>
```

效果：

![1583763549243](D:\MyNote\images\1583763549243.png)

## 2.9.文本格式化标签

| 标签   | 描述         |
| :----- | :----------- |
| b      | 定义粗体文本 |
| em     | 定义着重文字 |
| i      | 定义斜体字   |
| small  | 定义小号字   |
| strong | 定义加重语气 |
| sub    | 定义下标字   |
| sup    | 定义上标字   |
| ins    | 定义插入字   |
| del    | 定义删除字   |

**HTML "计算机输出" 标签**

| 标签 | 描述               |
| :--- | :----------------- |
| code | 定义计算机代码     |
| kbd  | 定义键盘码         |
| samp | 定义计算机代码样本 |
| var  | 定义变量           |
| pre  | 定义预格式文本     |

**HTML 引文, 引用, 及标签定义**

| 标签       | 描述               |
| :--------- | :----------------- |
| abbr       | 定义缩写           |
| address    | 定义地址           |
| bdo        | 定义文字方向       |
| blockquote | 定义长的引用       |
| q          | 定义短的引用语     |
| cite       | 定义引用、引证     |
| dfn        | 定义一个定义项目。 |

## 2.10.内联框架

```html
内联框架用于向当前页面引入另一个页面
src是指定引入页面的路径
frameborder指定内联框架的边框，0是没有，1是有边框
<iframe src="https://www.bilibili.com" frameborder="0" width="1000px" height="1500px"></iframe>
```