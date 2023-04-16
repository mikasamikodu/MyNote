# 3.Css

## 3.1. 开头

css 层叠样式表    

​	网页实际是一个多层结构，通过css可以分别为网页每一层来设置样式        

​	最终我们看到的是最上面的一层    

​	css就是设置网页元素的样式元素选择器：

```html
<style type="text/css">
    div{
        height:100px;
        background-color: #ddd;
        border: 1px solid #fff;
        margin: 50px 0px;
        display: none;
    }
    /*
    	这时css的注释
    */
</style>
```



文档流：(normal flow)    
	网页是一个多层的结构，一层叠一层    
	通过css可以为每一层设置样式    
	用户只能看到最上面一层    这些层中，最底下的一层成为文档流，文档流是网页的基础        
	我们所创建的元素默认在文档流中进行排列    

对于我们来说文档主要有2种状态        
	在文档流中或不在文档流中    

元素在文档流中有什么特点 

​	块元素            
​		块元素在文档中会独占一行            
​		默认宽度是父元素的全部（会把父元素撑满）            
​		默认高度由内容撑满（即被子元素撑满）        

​	行内元素            
​		行内元素在文档中不会独占一行，只占自身大小            
​		行内元素在页面中自左向右排列，同时会自上向下排列

## 3.2. display

> 定义

display 属性规定元素应该生成的框的类型。

### 可能的值

| 值                 | 描述                                                         |
| :----------------- | :----------------------------------------------------------- |
| none               | 此元素不会被显示。                                           |
| block              | 此元素将显示为块级元素，此元素前后会带有换行符。             |
| inline             | 默认。此元素会被显示为内联元素，元素前后没有换行符。         |
| inline-block       | 行内块元素。（CSS2.1 新增的值）                              |
| list-item          | 此元素会作为列表显示。                                       |
| run-in             | 此元素会根据上下文作为块级元素或内联元素显示。               |
| compact            | CSS 中有值 compact，不过由于缺乏广泛支持，已经从 CSS2.1 中删除。 |
| marker             | CSS 中有值 marker，不过由于缺乏广泛支持，已经从 CSS2.1 中删除。 |
| table              | 此元素会作为块级表格来显示（类似 <table>），表格前后带有换行符。 |
| inline-table       | 此元素会作为内联表格来显示（类似 <table>），表格前后没有换行符。 |
| table-row-group    | 此元素会作为一个或多个行的分组来显示（类似 <tbody>）。       |
| table-header-group | 此元素会作为一个或多个行的分组来显示（类似 <thead>）。       |
| table-footer-group | 此元素会作为一个或多个行的分组来显示（类似 <tfoot>）。       |
| table-row          | 此元素会作为一个表格行显示（类似 <tr>）。                    |
| table-column-group | 此元素会作为一个或多个列的分组来显示（类似 <colgroup>）。    |
| table-column       | 此元素会作为一个单元格列显示（类似 <col>）                   |
| table-cell         | 此元素会作为一个表格单元格显示（类似 <td> 和 <th>）          |
| table-caption      | 此元素会作为一个表格标题显示（类似 <caption>）               |
| inherit            | 规定应该从父元素继承 display 属性的值。                      |

## 3.3.position

### 3.3.1.相对定位

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        body{
            font-size: 60px;
        }
        .box1{
            width: 200px;
            height: 200px;
            background-color: #bfa;
        }

        .box2{
            width: 200px;
            height: 200px;
            background-color: orange;

            /*
                定位（position）
                    - 定位是一种更加高级的布局手段
                    - 通过定位可以将元素摆放到页面的任意位置
                    - 使用position属性来设置定位
                        可选值：
                            static 默认值，元素是静止的没有开启定位
                            relative 开启元素的相对定位
                            absolute 开启元素的绝对定位
                            fixed 开启元素的固定定位
                            sticky 开启元素的粘滞定位
                    - 相对定位：
                        - 当元素的position属性值设置为relative时则开启了元素的相对定位
                        - 相对定位的特点：
                            1.元素开启相对定位以后，如果不设置偏移量元素不会发生任何的变化
                            2.相对定位是参照于元素在文档流中的位置进行定位的
                            3.相对定位会提升元素的层级
                            4.相对定位不会使元素脱离文档流
                            5.相对定位不会改变元素的性质块还是块，行内还是行内
                    - 偏移量（offset）
                        - 当元素开启了定位以后，可以通过偏移量来设置元素的位置
                            top
                                - 定位元素和定位位置上边的距离
                            bottom
                                - 定位元素和定位位置下边的距离
                                - 定位元素垂直方向的位置由top和bottom两个属性来控制
                                    通常情况下我们只会使用其中一
                                - top值越大，定位元素越向下移动
                                - bottom值越大，定位元素越向上移动
                            left
                                - 定位元素和定位位置的左侧距离
                            right
                                - 定位元素和定位位置的右侧距离
                                - 定位元素水平方向的位置由left和right两个属性控制
                                    通常情况下只会使用一个
                                - left越大元素越靠右
                                - right越大元素越靠左
              */
            
            position: relative;

            left: 100px;
            top: -200px;

        }

        .box3{
            width: 200px;
            height: 200px;
            background-color: yellow;

        }
    </style>
</head>
<body>

    <div class="box1">1</div>
    <div class="box2">2</div>
    <div class="box3">3</div>
    
</body>
</html>
```



### 3.3.2.绝对定位

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        body{
            font-size: 60px;
        }
        .box1{
            width: 200px;
            height: 200px;
            background-color: #bfa;
        }

        .box2{
            width: 200px;
            height: 200px;
            background-color: orange;

           /* 
            绝对定位
                - 当元素的position属性值设置为absolute时，则开启了元素的绝对定位
                - 绝对定位的特点：
                    1.开启绝对定位后，如果不设置偏移量元素的位置不会发生变化
                    2.开启绝对定位后，元素会从文档流中脱离
                    3.绝对定位会改变元素的性质，行内变成块，块的宽高被内容撑开
                    4.绝对定位会使元素提升一个层级
                    5.绝对定位元素是相对于其包含块进行定位的
                    包含块( containing block )
                        - 正常情况下：
                            包含块就是离当前元素最近的祖先块元素
                            <div> <div></div> </div>
                            <div><span><em>hello</em></span></div>
                        - 绝对定位的包含块:
                            包含块就是离它最近的开启了定位的祖先元素，
                                如果所有的祖先元素都没有开启定位则根元素就是它的包含块
                        - html（根元素、初始包含块）
            */

            position: absolute;
            /* left: 0;
            top: 0; */
            bottom: 0;
            right: 0;
        }

        .box3{
            width: 200px;
            height: 200px;
            background-color: yellow;

        }

        .box4{
            width: 400px;
            height: 400px;
            background-color: tomato;
            position: relative;
        }
        
        .box5{
            width: 300px;
            height: 300px;
            background-color: aliceblue;
            /* position: relative; */
        }
    </style>
</head>
<body>

    <div class="box1">1</div>

    <div class="box4">
        4
        <div class="box5">
            5
            <div class="box2">2</div>
        </div>
    </div>
    <div class="box3">3</div>
    
</body>
</html>
```



### 3.3.3.固定定位

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        body{
            font-size: 60px;
            height: 2000px;
        }
        .box1{
            width: 200px;
            height: 200px;
            background-color: #bfa;
        }

        .box2{
            width: 200px;
            height: 200px;
            background-color: orange;
            /*
                固定定位：
                    - 将元素的position属性设置为fixed则开启了元素的固定定位
                    - 固定定位也是一种绝对定位，所以固定定位的大部分特点都和绝对定位一样
                        唯一不同的是固定定位永远参照于浏览器的视口进行定位
                        固定定位的元素不会随网页的滚动条滚动
              */

            position: fixed;

            left: 0;
            top: 0;



        }

        .box3{
            width: 200px;
            height: 200px;
            background-color: yellow;

        }

        .box4{
            width: 400px;
            height: 400px;
            background-color: tomato;

        }
        
        .box5{
            width: 300px;
            height: 300px;
            background-color: aliceblue;
        }
    </style>
</head>
<body>
    <div class="box1">1</div>
    <div class="box4">
        4
        <div class="box5">
            5
            <div class="box2">2</div>
        </div>
    </div>
    <div class="box3">3</div>   
</body>
</html>
```



### 3.3.4.粘滞定位

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>导航条</title>
    <link rel="stylesheet" href="./css/reset.css">
    <style>

        body{
            height: 3000px;
        }
        
        /* 设置nav的大小 */
        .nav{

            /* 设置宽度和高度 */
            width: 1210px;
            height: 48px;
            /* 设置背景颜色 */
            background-color: #E8E7E3;

            margin:100px auto;

            /* 
                粘滞定位
                    - 当元素的position属性设置为sticky时则开启了元素的粘滞定位
                    - 粘滞定位和相对定位的特点基本一致，
                        不同的是粘滞定位可以在元素到达某个位置时将其固定
             */

             position: sticky;
             top: 10px;

        }

        /* 设置nav中li */
        .nav li{
            /* 设置li向左浮动，已使菜单横向排列 */
            float: left;
            /* 设置li的高度 */
            /* height: 48px; */
            /* 将文字在父元素中垂直居中 */
            line-height: 48px;

        }

        /* 设置a的样式 */
        .nav a{
            /* 将a转换为块元素 */
            display: block;
            /* 去除下划线 */
            text-decoration: none;
            /* 设置字体颜色 */
            color: #777777;
            /* 修改字体大小 */
            font-size: 18px;

            padding: 0 39px;
        }

        .nav li:last-child a{
            padding: 0 42px 0 41px;
        }

        /* 设置鼠标移入的效果 */
        .nav a:hover{
            background-color: #3F3F3F;
            color: #E8E7E3;
        }
    </style>
</head>

<body>
    <!-- 创建导航条的结构 -->
    <ul class="nav">
        <li>
            <a href="#">HTML/CSS</a>
        </li>
        <li>
            <a href="#">Browser Side</a>
        </li>
        <li>
            <a href="#">Server Side</a>
        </li>
        <li>
            <a href="#">Programming</a>
        </li>
        <li>
            <a href="#">XML</a>
        </li>
        <li>
            <a href="#">Web Building</a>
        </li>
        <li>
            <a href="#">Reference</a>
        </li>
    </ul>
</body>
</html>
```



### 3.3.5.绝对定位的布局

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>

    <style>
        .box1{
            width: 500px;
            height: 500px;
            background-color: #bfa;

            position: relative;
        }

        .box2{
            width: 100px;
            height: 100px;
            background-color: orange;
            position: absolute;
            margin: auto;
            /* 
                水平布局
                    left + margin-left + border-left + padding-left + width + padding-right + border-right + margin-right + right = 包含块的内容区的宽度
                - 当我们开启了绝对定位后:
                    水平方向的布局等式就需要添加left 和 right 两个值
                        此时规则和之前一样只是多添加了两个值：
                            当发生过度约束：
                                如果9个值中没有 auto 则自动调整right值以使等式满足
                                如果有auto，则自动调整auto的值以使等式满足
                        - 可设置auto的值
                            margin width left right
                        - 因为left 和 right的值默认是auto，所以如果不指定left和right
                            则等式不满足时，会自动调整这两个值
                    垂直方向布局的等式的也必须要满足
                        top + margin-top/bottom + padding-top/bottom + border-top/bottom + height = 包含块的高度
            
             */

             left: 0;
             right: 0;

             top: 0;
             bottom: 0;
            /*left: auto;*/
            /*right: auto;*/
            /*bottom: auto;*/
            /*top: auto;*/
        }
    </style>
</head>
<body>
<div class="box1">
    <div class="box2"></div>
</div> 
</body>
</html>
```



### 3.3.6.元素的层级

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        body{
            font-size: 60px;
        }
        .box1{
            width: 200px;
            height: 200px;
            background-color: #bfa;
            position: absolute;
            /* 
                对于开启了定位元素，可以通过z-index属性来指定元素的层级
                    z-index需要一个整数作为参数，值越大元素的层级越高
                        元素的层级越高越优先显示
                    如果元素的层级一样，则优先显示靠下的元素
                    祖先的元素的层级再高也不会盖住后代元素
             */
             /* z-index: 3; */
        }

        .box2{
            width: 200px;
            height: 200px;
            background-color: rgba(255 , 0, 0, .3);
            position: absolute;
            top: 50px;
            left: 50px;
            /* z-index: 3; */

        }

        .box3{
            width: 200px;
            height: 200px;
            background-color: yellow;
            position: absolute;
            top: 100px;
            left: 100px;
            z-index: 3;

        }

        .box4{
            width: 100px;
            height: 100px;
            background-color: orange;
            position: absolute;
        }
    </style>
</head>
<body>

    <div class="box1">1</div>
    <div class="box2">2</div>
    <div class="box3">3
        <div class="box4">4</div>
    </div>

    
</body>
</html>
```



## 3.4.font

### 3.4.1.字体

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>

        /* 
        font-face可以将服务器中的字体直接提供给用户去使用 
            问题：
                1.加载速度
                2.版权
                3.字体格式
        
        */
        @font-face {
                /* 指定字体的名字 */
            font-family:'myfont' ;
            /* 服务器中字体的路径 */
            src: url('./font/ZCOOLKuaiLe-Regular.ttf') format("truetype");
        }

        p{
            /* 
            字体相关的样式 
                color 用来设置字体颜色
                font-size 字体的大小
                    和font-size相关的单位
                    em 相当于当前元素的一个font-size
                    rem 相对于根元素的一个font-size
                font-family 字体族（字体的格式）
                    可选值：
                        serif  衬线字体
                        sans-serif 非衬线字体
                        monospace 等宽字体
                            - 指定字体的类别，浏览器会自动使用该类别下的字体
                    - font-family 可以同时指定多个字体，多个字体间使用,隔开
                        字体生效时优先使用第一个，第一个无法使用则使用第二个 以此类推
                        Microsoft YaHei,Heiti SC,tahoma,arial,Hiragino Sans GB,"\5B8B\4F53",sans-serif
            */
            color: blue;
            font-size: 40px;

            /* font-family: 'Courier New', Courier, monospace; */
            font-family: myfont;
        }
    </style>
</head>
<body>
    <p>
        今天天气真不错，Hello Hello How are you！
    </p>
</body>
</html>
```



### 3.4.2.图标字体

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="./source/css/all.css">
<!--    图标字体(iconfont)
            -在网页中经常需要使用一些图标，可以通过图片来引入图标
                但是图片本身比较大，非常不灵活
            -使用图标时，我们可以将图标设置为字体，然后通过@font-face的形式对字体进行引入
            --这样我们就可以通过字体的形式使用图标了
       fontawesome的使用步骤:
        1.下载http://fontawesome.com;
        2.解压并将里面的css和webfonts引入项目中，
            注意：这两个文件夹需要在同一级目录下；
        3.在网页中通过link引入第二步中css下的all.css；
        4.通过class使用图标字体，
            在class开头使用fas或fab开头，后面空格，之后说需要使用的图标的名字
            案例：
                class="fas fa-bell"
                class="fab fa-accessible-icon"
-->
</head>
<body>
<i class="fas fa-bell" style="font-size: 30px;color: red;"></i>
</body>
</html>
```



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <link rel="stylesheet" href="./fa/css/all.css">
    <style>
        li{
            list-style: none;
        }

        li::before{
            /* 
                通过伪元素来设置图标字体
                    1.找到要设置图标的元素通过before或after选中
                    2.在content中设置字体的编码
                    3.设置字体的样式
                        fab
                        font-family: 'Font Awesome 5 Brands';
                        fas
                        font-family: 'Font Awesome 5 Free';
                        font-weight: 900; 
            */
            content: '\f1b0';
            /* font-family: 'Font Awesome 5 Brands'; */
            font-family: 'Font Awesome 5 Free';
            font-weight: 900; 
            color: blue;
            margin-right: 10px;
        }
    </style>
</head>
<body>

    <!-- <i class="fas fa-cat"></i> -->

    <ul>
        <li>锄禾日当午</li>
        <li>汗滴禾下土</li>
        <li>谁知盘中餐</li>
        <li>粒粒皆辛苦</li>
    </ul>

    <!-- 
        通过实体来使用图标字体：
            &#x图标的编码;
     -->
    <span class="fas">&#xf0f3;</span>
    
</body>
</html>
```



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <link rel="stylesheet" href="./iconfont/iconfont.css">
    <style>
        i.iconfont{
            font-size: 100px;
        }
/*		首先在阿里上下载纯色的图标，然后引入css，之后按照下面示例使用即可
        */
        /*第一种用法*/
        p::before{
            content: '\e625';
            font-family: 'iconfont';
            font-size: 100px;
        }
    </style>
</head>
<body>
<!--第二种用法-->
    <i class="iconfont">&#xe61c;</i>
    <i class="iconfont">&#xe622;</i>
    <i class="iconfont">&#xe623;</i>
<!--第三种用法-->
    <i class="iconfont icon-qitalaji"></i>

    <p>Hello</p>
</body>
</html>
```



### 3.4.3.行高

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div{
            font-size: 50px;

            /* 可以将行高设置为和高度一样的值，使单行文字在一个元素中垂直居中 */
            line-height: 200px;

            /* 
                行高（line height）
                    - 行高指的是文字占有的实际高度
                    - 可以通过line-height来设置行高
                        行高可以直接指定一个大小（px em）
                        也可以直接为行高设置一个整数
                            如果是一个整数的话，行高将会是字体的指定的倍数
                    - 行高经常还用来设置文字的行间距
                        行间距 = 行高 - 字体大小
                字体框
                    - 字体框就是字体存在的格子，设置font-size实际上就是在设置字体框的高度
                行高会在字体框的上下平均分配
            */

            border: 1px red solid;

            /* line-height: 1.33; */
            /* line-height: 1; */
            /* line-height: 10 */
        }
    </style>
</head>
<body>
    
    <div>今天天气这不错 Hello hello 今天天气这不错 Hello hello 今天天气这不错 Hello hello 今天天气这不错 Hello hello</div>

</body>
</html>
```



### 3.4.4.字体的简写属性

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div{
            border: 1px red solid;


            /* 
                font 可以设置字体相关的所有属性
                    语法：
                        font: 字体大小/行高 字体族
                        行高 可以省略不写 如果不写使用默认值
            
            */

            /* font-size: 50px;
            font-family: 'Times New Roman', Times, serif; */
            font-weight: bold;
            /* font: 50px/2  微软雅黑, 'Times New Roman', Times, serif; */
            /* font: normal normal 50px/2  微软雅黑, 'Times New Roman', Times, serif; */
            font: bold italic 50px/2  微软雅黑, 'Times New Roman', Times, serif;
            /* font:50px 'Times New Roman', Times, serif;
            line-height: 2; */

            /* font-size: 50px; */

            /* font-weight 字重 字体的加粗 
                可选值：
                    normal 默认值 不加粗
                    bold 加粗
                    100-900 九个级别（没什么用）
                font-style 字体的风格
                    normal 正常的
                    italic 斜体
            */
            /* font-weight: bold; */
            /* font-weight: 500;
            font-style: italic; */
        }
    </style>
</head>
<body>  
    <div>今天天气真不错 Hello hello</div> 
</body>
</html>
```



### 3.4.5.水平对齐与垂直对齐

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div{
            width: 800px;
            border: 1px red solid;

            /* 
                text-align 文本的水平对齐
                    可选值：
                        left 左侧对齐
                        right 右对齐
                        center 居中对齐
                        justify 两端对齐
            */
            /* text-align: justify; */

            font-size: 50px;
        }

        span{
            font-size: 20px;
            border: 1px blue solid;

                /*
                vertical-align 设置元素垂直对齐的方式
                    可选值：
                        baseline 默认值 基线对齐
                        top 顶部对齐
                        bottom 底部对齐
                        middle 居中对齐
                */
            vertical-align:baseline; 
        }

        p{
            border: 1px red solid;

        }
/*当图片与父元素之间有间距但又不是外边距和内边距时，可通过设置vertical-align为非baseline值来去除间距
        */
        img{
            vertical-align: bottom;
        }
    </style>
</head>
<body>
    
<div>
    今天天气 Helloyx<span>真不错 Hello</span>！
</div>

    <!-- <div>
        Lorem ipsum dolor, sit amet consectetur adipisicing elit. Illo nihil iure at ab atque nostrum molestiae totam porro, dolorem maiores repudiandae molestias veritatis, eligendi laudantium incidunt dolores corporis? Quibusdam, consequatur.
    </div> -->
    <p>
       <img src="./img/an.jpg" alt=""> 
    </p>

</body>
</html>
```



### 3.4.6.字体阴影

**CSS3 text-shadow 属性**

**实例**

基础的文本阴影效果：

```css
h1{
	text-shadow: 5px 5px 5px #FF0000;
}
```



**语法**

```css
text-shadow: h-shadow v-shadow blur color;
```



 **注释：**text-shadow 属性向文本添加一个或多个阴影。该属性是逗号分隔的阴影列表，每个阴影有两个或三个长度值和一个可选的颜色值进行规定。省略的长度是 0。 

| 值         | 描述                             |
| :--------- | :------------------------------- |
| *h-shadow* | 必需。水平阴影的位置。允许负值。 |
| *v-shadow* | 必需。垂直阴影的位置。允许负值。 |
| *blur*     | 可选。模糊的距离。               |
| *color*    | 可选。阴影的颜色。               |



###  3.4.7.white-space

 规定段落中的文本不进行换行： 

```css
p
  {
  white-space: nowrap
  }
```



**定义和用法**

white-space 属性设置如何处理元素内的空白。

这个属性声明建立布局过程中如何处理元素中的空白符。值 pre-wrap 和 pre-line 是 CSS 2.1 中新增的。

**可能的值**

| 值       | 描述                                                         |
| :------- | :----------------------------------------------------------- |
| normal   | 默认。空白会被浏览器忽略。                                   |
| pre      | 空白会被浏览器保留。其行为方式类似 HTML 中的 <pre> 标签。    |
| nowrap   | 文本不会换行，文本会在在同一行上继续，直到遇到 <br> 标签为止。 |
| pre-wrap | 保留空白符序列，但是正常地进行换行。                         |
| pre-line | 合并空白符序列，但是保留换行符。                             |
| inherit  | 规定应该从父元素继承 white-space 属性的值。                  |



### 3.4.8.text-wrap

 不允许换行： 

```css
p.test {text-wrap:none;}
```



**定义和用法**

text-wrap 属性规定文本的换行（折行）规则。

| 值           | 描述                                                         |
| :----------- | :----------------------------------------------------------- |
| normal       | 只在允许的换行点进行换行。                                   |
| none         | 不换行。元素无法容纳的文本会溢出。                           |
| unrestricted | 在任意两个字符间换行。                                       |
| suppress     | 压缩元素中的换行。浏览器只在行中没有其他有效换行点时进行换行。 |



## 3.5.背景

### 3.5.1.background-image

background-image：用于设置背景图片
                -可同时设置背景图片与背景颜色，这样背景颜色就会成为背景图片的背景色
                -如果背景图片小于元素，则图片会在元素内平铺至占满元素
                -如果背景图片大于元素，则背景图片的一部分将不能显示
                -果背景图片等于元素，则背景图片可正常显示

### 3.5.2.background-repeat

background-repeat：设置背景图片的平铺方式
                   可选值：
                     repeat：默认值，在横向和纵向上平铺
                     no-repeat：不平铺，只显示一张图片
                     repeat-x： 在横向上平铺
                     repeat-y： 在纵向上平铺

### 3.5.3.background-position

background-position：指定背景图片的位置
                通过指定偏移量指定图片位置：水平偏移量 垂直偏移量
                设置方式：
                    偏移量可通过top, bottom,left,right,center进行指定
                    指定时必须指定两个值，如果只指定一个值，则第二个值默认是center
                    偏移量除了通过方位名词指定也可通过数字指定

### 3.5.4.background-clip

background-clip：指定背景范围
                    可选值：
                        border-box：默认值，背景会出现在边框下边
                        content-box：背景只会出现在内容区
                        padding-box：背景会出现在内容区和内边距

### 3.5.5.background-origin

background-origin： 指定背景图片偏移量计算的原点
                    可选值：
                        padding-box：默认值，背景图片偏移量从内边距开始计算
                        content-box：背景图片偏移量从内容区开始计算
                        border-box：背景图片偏移量从边框开始计算

### 3.5.6.background-size

background-size：指定背景图片大小
                第一个值表示高度，第二个值表示宽度
                如果只指定一个，则另一个为auto
                可选值：
                    contain：图片比例不变，将图片在元素中完整显示
                    cover：  图片比例不变，，将元素铺满

### 3.5.7.background-attachment

background-attachment：图片依附元素的方式
                    可选值：
                        scroll：默认值，随元素滚动
                        fixed：固定在元素某一处，不随元素滚动

### 3.5.8.background

background：背景的简写属性，所有与背景相关的属性都可以在这里指定

```css
background: red url('./images/1.jpg') center center/contain border-box contain-box no-repeat
background-color background-image background-position/background-size background-origin background-clip background-repeat
```



上述样式无顺序要求，没有规定哪个属性是必须的
        规定；1.background-size必须在background-position后面，以/隔开
             2.background-origin background-clip必须一起出现且顺序不能变	

上述各属性的案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .box{
            width: 500px;
            height: 500px;
            background-color: deepskyblue;
            /*background-image：用于设置背景图片
                -可同时设置背景图片与背景颜色，这样背景颜色就会成为背景图片的背景色
                -如果背景图片小于元素，则图片会在元素内平铺至占满元素
                -如果背景图片大于元素，则背景图片的一部分将不能显示
                -果背景图片等于元素，则背景图片可正常显示
            */
            background-image: url("./images/1.jpg");
            /*
                background-repeat：设置背景图片的平铺方式
                   可选值：
                     repeat：默认值，在横向和纵向上平铺
                     no-repeat：不平铺，只显示一张图片
                     repeat-x： 在横向上平铺
                     repeat-y： 在纵向上平铺
            */
            background-repeat: no-repeat;
            /*background-position：指定背景图片的位置
                通过指定偏移量指定图片位置：水平偏移量 垂直偏移量
                设置方式：
                    偏移量可通过top, bottom,left,right,center进行指定
                    指定时必须指定两个值，如果只指定一个值，则第二个值默认是center
                    偏移量除了通过方位名词指定也可通过数字指定
            */
            /*background-position: left center;*/
            /*
                background-clip：指定背景范围
                    可选值：
                        border-box：默认值，背景会出现在边框下边
                        content-box：背景只会出现在内容区
                        padding-box：背景会出现在内容区和内边距
            */
            background-clip: border-box;
            border: 10px red double;
            padding: 5px;
            /*
                background-origin： 指定背景图片偏移量计算的原点
                    可选值：
                        padding-box：默认值，背景图片偏移量从内边距开始计算
                        content-box：背景图片偏移量从内容区开始计算
                        border-box：背景图片偏移量从边框开始计算
            */
            background-origin: padding-box;
            /*background-size：指定背景图片大小
                第一个值表示高度，第二个值表示宽度
                如果只指定一个，则另一个为auto
                可选值：
                    contain：图片比例不变，将图片在元素中完整显示
                    cover：  图片比例不变，，将元素铺满

            */
            background-size: contain;
            overflow: scroll;
        }
        .box1{
            width: 300px;
            height: 1000px;
            background-image: url("./images/300.jpg");
            background-size: 300px;
            background-origin: padding-box;
            background-repeat: no-repeat;
            margin: 10px;
            /*
                background-attachment：图片依附元素的方式
                    可选值：
                        scroll：默认值，随元素滚动
                        fixed：固定在元素某一处，不随元素滚动
            */
            background-attachment: fixed;
        /*
          background：背景的简写属性，所有与背景相关的属性都可以在这里指定

          background: red url('./images/1.jpg') center center/contain border-box contain-box no-repeat
        background-color background-image background-position/background-size background-origin background-clip background-repeat
        上述样式无顺序要求，没有规定哪个属性是必须的
            规定；1.background-size必须在background-position后面，以/隔开
                 2.background-origin background-clip必须一起出现且顺序不能变
          */
        }
    </style>
</head>
<body>
<div class="box">
    <div class="box1"></div>
</div>
</body>
</html>
```



### 3.5.9.雪碧图

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        a{
            width: 93px;
            height: 29px;
            display: block;
        }
        a:link{
            background-image: url("./images/link.png");
        }
        a:hover{
            background-image: url("./images/hover.png");
        }
        a:active{
            background-image: url("./images/active.png");
        }
        /*
               图片属于网页中的外部资源，外部资源都需要浏览器单独发送请求加载，
                   浏览器加载外部资源时是按需加载的，用则加载，不用则不加载
                   像我们上边的练习link会首先加载，而hover和active会在指定状态触发时才会加载

             */
    </style>
</head>
<body>
<a href="javascript:;"></a>
</body>
</html>
```



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        a:link{
            width: 93px;
            height: 29px;
            display: block;
            background-image: url("./images/btn.png");
            background-position: 0 0;
        }
        a:hover{
            background-position: -93px 0;
        }
        a:active{
            background-position: -186px 0;
        }
        .box{
            width: 130px;
            height: 50px;
            background-image: url("./images/amazon-sprite_.png");
            background-position: 0 0;
        }
        /*
        解决图片闪烁的问题：
            可以将多个小图片统一保存到一个大图片中，然后通过调整background-position来显示的图片
            这样图片会同时加载到网页中 就可以有效的避免出现闪烁的问题
            这个技术在网页中应用十分广泛，被称为CSS-Sprite，这种图我们称为雪碧图
        雪碧图的使用步骤：
            1.先确定要使用的图标
            2.测量图标的大小
            3.根据测量结果创建一个元素
            4.将雪碧图设置为元素的背景图片
            5.设置一个偏移量以显示正确的图片
        雪碧图的特点：
            一次性将多个图片加载进页面，降低请求的次数，加快访问速度，提升用户的体验
 */
        .box1{
            width: 45px;
            height: 30px;
            background-image: url("./images/amazon-sprite_.png");
            background-position: -57px -338px;
        }
    </style>
</head>
<body>
<a href="javascript:;"></a>
<div class="box"></div>
<div class="box1"></div>
</body>
</html>
```



### 3.5.10.线性渐变

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .box{
            width: 200px;
            height: 200px;
            /*
                线性渐变可以设置一些复杂的背景颜色，可以实现从一个颜色向其他颜色过渡的效果
                渐变是图片，需要通过background-image设置
                线性渐变，颜色通过一条直线变化linear-gradient()
                linear-gradient(red, yellow)：红色在开头，黄色在结尾，中间是过渡
                指定线性渐变的方向：
                   to top/to left/to right/to bottom案例: linear-gradient(to top, red, yellow);
                   to  top left/to top right/to bottom left/to bottom right....案例: linear-gradient(to top left, red, yellow);
                   deg：表示度数，案例：linear-gradient(45deg, red, yellow)
                   turn：表示一圈，案例：linear-gradient(0.3turn, red, yellow)

                   渐变可以同时指定多个颜色。多个颜色默认是平均分布的
                   可以手动调整颜色分布情况：
            */
            /*background-image: linear-gradient(0.2turn, red, yellow, blue);*/
            /*从上向下，80像素以上为纯红色，120像素以下为纯黄色，中间部分为过渡*/
            /*background-image: linear-gradient(red 80px, yellow 120px);*/
            /*repeating-linear-gradient：可以平铺的线性渐变，由于80像素到120像素中间的40像素为过渡区域，因此这40像素会从上到下重复5次*/
            background-image: repeating-linear-gradient(red 80px, yellow 120px);
        }
    </style>
</head>
<body>
<div class="box"></div>
</body>
</html>
```



### 3.5.11.径向渐变

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .box{
            width: 300px;
            height: 300px;
            /*
                radial-gradient()：径向渐变，产生放射性效果，如太阳般
                默认情况下径向渐变的形状会根据元素的形状来计算
                    正方形-圆形
                    长方形-椭圆形
                    案例：
                    以元素中心为径向渐变原点，半径100的圆，从内向外由红边黄，非渐变部分为黄色
                    background-image: radial-gradient(100px 100px, red, yellow);
                    以元素中心为径向渐变原点，半径100的圆，从内向外由红边黄，非渐变部分为黄色
                    background-image: radial-gradient(100px, red, yellow);
                    以元素中心为径向渐变原点，椭圆，从内向外由红边黄，非渐变部分为黄色
                    background-image: radial-gradient(100px 200px, red, yellow);
                -可手动指定径向渐变的形状
                    circle-圆形
                    ellipse-椭圆形
                    案例：background-image: radial-gradient(ellipse, red, yellow);

                以元素中心为径向渐变原点，半径100的圆从内向外由红边黄，并将中心渐变部分从内向外重复，每半径100px重复一次
                repeating-radial-gradient(100px 100px, red, yellow);

                手动指定径向渐变原点
                设置径向渐变原点为元素左上角(0,0)位置，并作出半径为100px的径向渐变圆
                background-image: radial-gradient(100px 100px at 0 0, red, yellow);
                设置径向渐变原点为元素中心位置，并作出半径为100px的径向渐变圆
                background-image: radial-gradient(100px 100px at center center, red, yellow);
                设置径向渐变原点为元素中心位置，并作出径向渐变圆
                background-image: radial-gradient(at center center, red, yellow);

                最终语法：
                    radial-gradient(大小 at 位置,颜色 位置,颜色 位置,颜色 位置);颜色可写多个
                    大小可选值：
                        circle-圆形
                        ellipse-椭圆形
                        像素
                        closest-side  近边
                        closest-corner  近角
                        farthest-side   远边
                        farthest-corner  远角
                   位置：
                    top bottom left right center 像素
            		大小和位置都是可选的，可以都不写或写其一
            */
            background-image: radial-gradient(at center center, red, yellow);
        }
    </style>
</head>
<body>
<div class="box"></div>
</body>
</html>
```



## 3.6.弹性盒子

### 3.6.1.flex简介

### 3.6.2.flex-direction

### 3.6.3.flex-grow

### 3.6.4.flex-shrink

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="utf-8">
    <title>弹性盒子</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            list-style: none;
        }
        /* 
            flex（弹性盒，伸缩盒）
                --是css中一种布局手段，主要是代替浮动来完成页面的布局
                --flex可以是元素具有弹性，让元素跟随页面大小改变而改变
                --弹性容器
                    --要使用容器就必须先将一个元素设置为弹性容器
                    --可以通过display设置弹性容器
                        display: flex;      设置为块级弹性容器
                        display: inline-flex; 设置为行内弹性容器
                --弹性元素
                    --弹性容器的子元素就是弹性元素
                    --弹性元素可同时设置为弹性容器
        */
        
        ul {
            /* width: 900px; */
            width: 200px;
            border: 2px solid red;
            margin: 100px auto;
            /* 将元素设置为弹性容器 */
            display: flex;
            /* 
                flex-direction；设置弹性容器中元素的排列方式
                    可选值：
                        row: 默认值，弹性元素在容器中水平排列（自左向右）
                        row-reverse：弹性元素在容器中水平排列（自右向左）
                        column：弹性元素在容器中垂直排列（自上向下）
                        column-reverse：弹性元素在容器中垂直排列（自下向上）
                
                主轴：弹性元素的排列方向
                侧轴：与主轴垂直的方向就是了
            */
            flex-direction: row;
        }
        
        li {
            width: 100px;
            line-height: 100px;
            background-color: aqua;
            text-align: center;
            font-size: 40px;
            /* 
                弹性元素的属性：
                    flex-grow：指定弹性元素伸展的系数
                        -当父元素还有剩余空间时，子元素如何伸展
                        -父元素的剩余空间，会按照比例分配
                        -默认值是0
                    flex-shrink：指定弹性元素的收缩系数
                        当父元素空间不足以容纳所有子元素时，如何对其子元素处理呢
            */
            /* flex-grow: 1;当弹性元素有三个，剩余空间为300px时，每个元素宽度增加100px*/
            flex-shrink: 1;
             /* flex-grow: 0;
            flex-shrink: 0; */
         /* 
                flex-basis:指定元素在主轴上的基础长度
                    如果主轴是横向的，则指定的是弹性元素的宽度
                    如果主轴是竖向的，则指定的是弹性元素的高度
                    默认值为auto,表示参考元素自身的宽高
                    如果传递了一个具体参数，则以该值为准
            */
            /* flex-basis: auto; */
            /* 
                flex：可以设置弹性元素上的三个样式
                    顺序：增长 缩减 基础长度
                    可选值：
                        initial->flex: 0 1 auto;
                        auto->flex: 1 1 auto;
                        none->auto->flex: 0 0 auto;弹性元素无弹性
            */
            flex: initial;
            /* order:可以指定弹性元素的排列顺序 */
            order: 3
        }
        
        li:nth-child(2) {
            background-color: rgb(21, 144, 192);
            order: 1;
        }
        
        li:nth-child(3) {
            background-color: rgb(150, 36, 202);
            order: 2;
        }
    </style>
</head>

<body>
    <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
    </ul>
</body>

</html>
```



### 3.6.5.flex-wrap

### 3.6.6.justify-content

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="utf-8">
    <title>弹性盒子</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            list-style: none;
        }
        
        ul {
            /* width: 200px; */
            width: 900px;
            border: 2px solid red;
            margin: 100px auto;
            display: flex;
            /* 
                flex-wrap:设置弹性元素在容器内是否可以自动换行
                    可选值：
                        nowrap： 默认值，不自动换行
                        wrap: 自动换行
                        wrap-reverse: 自动换行，但是是自下向上换行
            */
            /* flex-wrap: wrap-reverse; */
            /* 
                justify-content：设置如何分配主轴上的空白空间
                    可选值：
                        flex-start: 默认值，弹性元素沿主轴起边排列
                        flex-end: 弹性元素沿主轴终边排列
                        center：弹性元素居中排列
                        space-around：弹性容器的空白空间均匀分布在弹性元素的两侧
                        space-evenly: 弹性容器的空白空间均匀分布在弹性元素的一侧
                        space-between：弹性容器的空白空间均匀分布在弹性元素之间
            */
            justify-content: space-between
        }
        
        li {
            width: 100px;
            line-height: 100px;
            background-color: aqua;
            text-align: center;
            font-size: 40px;
            flex-grow: 0;
            flex-shrink: 0;
        }
        
        li:nth-child(2) {
            background-color: rgb(21, 144, 192);
        }
        
        li:nth-child(3) {
            background-color: rgb(150, 36, 202);
        }
    </style>
</head>

<body>
    <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
    </ul>
</body>

</html>
```



### 3.6.7.align-items

### 3.6.8.align-content

### 3.6.9.align-self

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="utf-8">
    <title>弹性盒子</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            list-style: none;
        }
        
        ul {
            width: 600px;
            height: 500px;
            border: 2px solid red;
            margin: 50px auto;
            display: flex;
            flex-wrap: wrap;
            /* 
                align-items: 规定元素如何在辅轴上排列
                    可选值：
                        stretch:默认值，将元素的长度设置为相同的
                        flex-start：元素不会延长，在辅轴起边对齐
                        flex-end: 元素不会延长，在辅轴起边对齐;
                        center: 居中对齐
                        baseline：基线对齐
            */
            align-items: baseline;
            /* 
                align-content：设置如何分配辅轴上的空白空间
                    可选值：
                        flex-start: 默认值，弹性元素沿辅轴起边排列
                        flex-end: 弹性元素沿辅轴终边排列
                        center：弹性元素居中排列
                        space-around：弹性容器的空白空间均匀分布在弹性元素的两侧
                        space-evenly: 弹性容器的空白空间均匀分布在弹性元素的一侧
                        space-between：弹性容器的空白空间均匀分布在弹性元素之间
            */
            align-content: center;
        }
        
        li {
            width: 200px;
            line-height: 100px;
            background-color: aqua;
            text-align: center;
            font-size: 40px;
            flex-shrink: 0;
            flex-grow: 0;
        }
        
        li:nth-child(2) {
            background-color: rgb(21, 144, 192);
            /* 与align-items对应，是用于弹性元素的样式，可覆盖其对应弹性容器自己的align-items的设置 */
            align-self: center;
        }
        
        li:nth-child(3) {
            background-color: rgb(150, 36, 202);
        }
        
        li:nth-child(4) {
            background-color: orange;
        }
        
        li:nth-child(5) {
            background-color: chocolate;
        }
    </style>
</head>

<body>
    <ul>
        <li>
            <div>1</div>
        </li>
        <li>
            <div>2</div>
            <div>2</div>
        </li>
        <li>
            <div>3</div>
            <div>3</div>
            <div>3</div>
        </li>
        <li>
            <div>1</div>
        </li>
        <li>
            <div>2</div>
            <div>2</div>
        </li>
    </ul>
</body>

</html>
```



## 3.7.浮动

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .div1{
            width: 100px;
            height: 100px;
            background-color: #339933;
            float: left;
        }
        .div2{
            width: 100px;
            height: 100px;
            background-color: #225599;
            float: left;
        }
        .div3{
            width: 100px;
            height: 100px;
            background-color: #993355;
            float: left;
        }
    /*
        float:通过浮动可以是一个元素向其父元素的左侧或右侧移动
            通过float属性可以设置元素的浮动
            可选值：
                none：默认值，元素不浮动
                left：元素向左浮动
                right：元素向右浮动
            注意：元素浮动之后，水平布局的等式将不需要强制成立
            原因：元素浮动之后，会完全从文档流中脱离，不再占用文档流中位置
                  所以元素下边的还在文档流中的元素会自动向上移动
           浮动的特点：
                1.元素浮动之后，会完全从文档流中脱离，不再占用文档流中位置
                2.设置浮动后，一个元素向其父元素的左侧或右侧移动
                3.浮动元素默认不会从父元素中脱离
                4.浮动元素向左或向右移动时，不会超过其前面的浮动元素
                5.如果浮动元素的上边的元素没有设置浮动，则该浮动元素不能进行上移
                6.浮动元素不会超过它上边浮动的兄弟元素，最多和其同样高
        浮动其他的特点：
                浮动元素不会盖住文字，文字会自动环绕再浮动元素的周围
                因此可以利用这个特点做文字环绕图片的效果
            脱离文档流的元素特点：
                块元素：
                    1.块元素将不会再独占一行；
                    2.脱离文档流后，块元素宽度与高度将会又内容撑开；
                行内元素;
                    脱离文档流后，特点与块元素脱离后相同
                元素脱离文档流后会变成display: inline-block的特点,即不再区分块元素与行内元素
    */
    </style>
</head>
<body>
<div class="div1"></div>
<div class="div2"></div>
<div class="div3"></div>
    <p>元素浮动之后，会完全从文档流中脱离，不再占用文档流中位置元素浮动之后，会完全从文档流中脱离，不再占用文档流中位置元素浮动之后，会完全从文档流中脱离，不再占用文档流中位置元素浮动之后，会完全从文档流中脱离，不再占用文档流中位置元素浮动之后，会完全从文档流中脱离，不再占用文档流中位置元素浮动之后，会完全从文档流中脱离，不再占用文档流中位置元素浮动之后，会完全从文档流中脱离，不再占用文档流中位置元素浮动之后，会完全从文档流中脱离，不再占用文档流中位置元素浮动之后，会完全从文档流中脱离，不再占用文档流中位置元素浮动之后，会完全从文档流中脱离，不再占用文档流中位置元素浮动之后，会完全从文档流中脱离，不再占用文档流中位置元素浮动之后，会完全从文档流中脱离，不再占用文档流中位置元素浮动之后，会完全从文档流中脱离，不再占用文档流中位置元素浮动之后，会完全从文档流中脱离，不再占用文档流中位置元素浮动之后，会完全从文档流中脱离，不再占用文档流中位置元素浮动之</p>
<span class="span1">11111</span>
<span class="span2">22222</span>
</body>
</html>
```

### 3.7.1.高度塌陷与BFC

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        .outer{
            border: 10px red solid;

            /* 
                BFC(Block Formatting Context) 块级格式化环境
                    - BFC是一个CSS中的一个隐含的属性，可以为一个元素开启BFC
                        开启BFC该元素会变成一个独立的布局区域
                    - 元素开启BFC后的特点：
                        1.开启BFC的元素不会被浮动元素所覆盖
                        2.开启BFC的元素子元素和父元素外边距不会重叠
                        3.开启BFC的元素可以包含浮动的子元素
                    - 可以通过一些特殊方式来开启元素的BFC：
                        1、设置元素的浮动（不推荐）
                        2、将元素设置为行内块元素（不推荐）
                        3、将元素的overflow设置为一个非visible的值
                            - 常用的方式 为元素设置 overflow:hidden 开启其BFC 以使其可以包含浮动元素
            
             */

             /* float: left; */
             /* display: inline-block; */
             overflow: hidden;
        }

        .inner{
            width: 100px;
            height: 100px;
            background-color: #bfa;

            /* 
                高度塌陷的问题：
                    在浮动布局中，父元素的高度默认是被子元素撑开的，
                        当子元素浮动后，其会完全脱离文档流，子元素从文档流中脱离
                        将会无法撑起父元素的高度，导致父元素的高度丢失
                    父元素高度丢失以后，其下的元素会自动上移，导致页面的布局混乱
                    所以高度塌陷是浮动布局中比较常见的一个问题，这个问题我们必须要进行处理！
             */
            float: left;
        }
    </style>
</head>
<body>

    <div class="outer">

        <div class="inner"></div>

    </div>

    <div style="width: 200px;height: 200px;background-color:yellow;"></div>
    
</body>
</html>
```



### 3.7.2.clear

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>

        div{
            font-size: 50px;
        }

        .box1{
            width: 200px;
            height: 200px;
            background-color: #bfa;
            float: left;
        }

        .box2{
            width: 400px;
            height: 150px;
            background-color: #ff0;
            float: left;
        }

        .box3{
            width: 200px;
            height: 200px;
            background-color: orange;
            /* 
                由于box1的浮动，导致box3位置上移
                    也就是box3收到了box1浮动的影响，位置发生了改变
                如果我们不希望某个元素因为其他元素浮动的影响而改变位置，
                    可以通过clear属性来清除浮动元素对当前元素所产生的影响
                clear
                    - 作用：清除浮动元素对当前元素所产生的影响
                    - 可选值：
                        left 清除左侧浮动元素对当前元素的影响
                        right 清除右侧浮动元素对当前元素的影响
                        both 清除两侧中最大影响的那侧
                    原理：
                        设置清除浮动以后，浏览器会自动为元素添加一个上外边距，
                            以使其位置不受其他元素的影响
             */

             /*clear: both;*/
        }
    </style>
</head>
<body>

    <div class="box1">1</div>
    <div class="box2">2</div>
<!--    <div class="box3">3</div>-->
<!--    <span style="width:500px; height:400px; background-color: red; display: block"></span>-->
    
</body>
</html>
```



### 3.7.3.高度塌陷的最终解决方案

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
<!--        clear 只针对浮动-->
        .box1{
            border: 10px red solid;

            /* overflow: hidden; */
        }

        .box2{
            width: 100px;
            height: 100px;
            background-color: #bfa;
            float: left;
        }

        .box3{
            clear: both;
        }

        .box1::after{
            content: '';
            clear: both;
            display: block;
        }
        /*通过使用伪类::after在父元素的最后添加内容，并使内容变为块元素并清除浮动可解决高度塌陷问题*/
    </style>
</head>
<body>

    <div class="box1">
        <div class="box2"></div>
        <!-- <div class="box3"></div> -->
    </div>
    
</body>
</html>
```



### 3.7.4.解决外边距重叠问题

div内有一个div，两者同时有宽高，但父元素更高更宽时，子元素添加margin-top时，会使得父元素也一起向下移动。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        .box1{
            width: 200px;
            height: 200px;
            background-color: #bfa;
        }

        /* .box1::before{
            content: '';
            display: table;
        } */

        .box2{
            width: 100px;
            height: 100px;
            background-color: orange;
            margin-top: 100px;
        }

/* clearfix 这个样式可以同时解决高度塌陷和外边距重叠的问题，当你在遇到这些问题时，直接使用clearfix这个类即可 */
        .clearfix::before,
        .clearfix::after{
            content: '';
            display: table;
            clear: both;
        }
    </style>
</head>
<body>

    <div class="box1 clearfix">
        <div class="box2"></div>
    </div>
    
</body>
</html>
```



## 3.8.justify-content

> 实例

在弹性盒对象的 <div> 元素中的各项周围留有空白：

```css
div
{
    display: flex;
    justify-content: space-around;
}
```

> 定义与用法

justify-content 用于设置或检索弹性盒子元素在主轴（横轴）方向上的对齐方式。

> 属性值

| 值            | 描述                                             |
| ------------- | ------------------------------------------------ |
| flex-start    | 默认值。项目位于容器的开头。                     |
| flex-end      | 项目位于容器的结尾。                             |
| center        | 项目位于容器的中心。                             |
| space-between | 项目位于各行之间留有空白的容器内。               |
| space-around  | 项目位于各行之前、之间、之后都留有空白的容器内。 |
| initial       | 设置该属性为它的默认值。                         |
| inherit       | 从父元素继承该属性。                             |

## 3.9.align-items

> 实例

居中对齐弹性盒的各项 <div> 元素：

`div {     display: flex;     align-items:center; }`

> 定义与用法

align-items 属性定义flex子项在flex容器的当前行的侧轴（纵轴）方向上的对齐方式。

> 属性值

| 值         | 描述                                                         |
| ---------- | ------------------------------------------------------------ |
| stretch    | 默认值。元素被拉伸以适应容器。如果指定侧轴大小的属性值为'auto'，则其值会使项目的边距盒的尺寸尽可能接近所在行的尺寸，但同时会遵照'min/max-width/height'属性的限制。 |
| center     | 元素位于容器的中心。弹性盒子元素在该行的侧轴（纵轴）上居中放置。（如果该行的尺寸小于弹性盒子元素的尺寸，则会向两个方向溢出相同的长度）。 |
| flex-start | 元素位于容器的开头。弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴起始边界。 |
| flex-end   | 元素位于容器的结尾。弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴结束边界。 |
| baseline   | 元素位于容器的基线上。如弹性盒子元素的行内轴与侧轴为同一条，则该值与'flex-start'等效。其它情况下，该值将参与基线对齐。 |
| initial    | 设置该属性为它的默认值。                                     |
| inherit    | 从父元素继承该属性。                                         |



## 3.10.选择器

样式的继承：我们为一个元素设置样式，同时也会应用到它的后代元素中继承发生在祖先与后代之间的继承的设计是为了方便我们进行开发    

利用继承可以将一些通用样式统一设置在共同的祖先元素上 ，这样只需一次即可让所有元素都有该样式 注意：并不是所有的样式都会被继承    

例如：背景相关的(background-*)，布局相关的

### 3.10.1.元素选择器：

​	作用：根据标签名选中指定元素；    
​	语法；标签名{}    
​	案例：p{color: red;}

### 3.10.2.id选择器：

​	作用：根据元素的id属性选中一个元素,id不可重复    
​	语法：#标签id属性值{}    
​	案例：#aa{color: red;}    

```html
<p id="aa">1111</p>
```



### 3.10.3.class选择器：

​	作用：根据元素的class属性值选中一组元素,一个class中可以同时定义多个值，之中间以空格分开    
​	语法：#标签class属性值{}    
​	案例：.aa{color: red;}    

```html
<p class="aa">1111</p>
```



### 3.10.4.通配选择器：

​	作用：选中所有选择器    
​	语法：*{}    

​	案例：*{color:red;}

### 3.10.5.交集选择器：

​	作用：选择同时符合多个条件的元素    

​	语法：选择器1选择器2选择器3{}    

​	案例：div.aa{color:red;}

### 3.10.6.并集选择器：

并集选择器又名选择器分组    

​	作用：同时选择多个符合条件的元素    
​	语法：选择器1,选择器2,选择器3{}    
​	案例：div,.aa{color:red;}

### 3.10.7.关系选择器：    

​	父元素：直接包含子元素的元素叫父元素    
​	子元素：直接被父元素包含的元素叫子元素    
​	祖先元素：直接或间接被包含子元素的元素叫祖先元素             
​						一个元素的父元素也是他的祖先元素    

​	后代元素：直接或间接被祖先元素包含的元素叫后代元素             
​						子元素也是他的后代元素    
​	兄弟元素：拥有相同的父元素d的元素叫兄弟元素    

#### 3.10.7.1.子元素选择器：        

​	作用：选择指定父元素的下一层中指定的某个子元素 ，两者之间只差一层   
​	语法：选父元素>子元素{}        
​	案例：div>span{color:red;}    

#### 3.10.7.2.后代元素选择器：        

​	作用：选择指定元素的所有指定后代元素 ，两者之间可差多层   
​	语法：祖先 后代{}        
​	案例：div span{color:red;}    

#### 3.10.7.3.后一个兄弟元素选择器：    

​	作用：选择下一个兄弟元素，必须是挨着的兄弟,中间不能有其他元素    
​	语法：前一个 + 后一个{}    
​	案例：div + span{color:red;}

#### 3.10.7.4.后面所有兄弟元素选择器：    

​	作用：后面所有兄弟元素    
​	语法：前一个 ~ 后一个{}    
​	案例：div ~ span{color:red;}

### 3.10.8.属性选择器：    

​	[属性名]：选择含有指定属性的元素
​	[属性名=属性值]：选择含有指定属性和指定属性值的元素    
​	[属性名^=属性值]：选择含有指定属性且属性值以指定值开头的元素
​	[属性名$=属性值]：选择含有指定属性且属性值以指定值结尾的元素
​	[属性名*=属性值]：选择含有指定属性且属性值含有指定值的元素伪类选择器  

### 3.10.9.伪类选择器  

伪类是用来描述一个元素的特殊状态，例如：被点击的元素，第一个元素，最后一个元素    

伪类一般使用冒号开头        
	:first-child：选择第一个子元素        
	:last-child：选择最后一个子元素      

​	:nth-last-child(n)：从后向前数选择第n个元素  
​	:nth-child(n)：从前向后数选择第n个子元素,                       
​				   如果值是n，代表正无穷，也就是全选中                       
​				   如果值是2n或even，代表偶数正无穷，也就是偶数全选中                       
​				   如果值是2n+1或odd，代表奇数正无穷，也就是奇数全选中            
​	以上这些伪类是根据所有子元素进行排序计算  （需要元素先满足左边的条件 ，然后满足右边伪类选择器的条件然后是自己的条件。）   
​	

:first-of-type：选择第一个子元素        
:last-of-type：选择最后一个子元素        
:nth-of-type(n)：选择第n个子元素           
这些伪类功能与上述类似，但是不同的是他们是同类型子元素进行排序计算的        
案例：

```html
<ul>
    <span></span>                
    <li></li>                
    <li></li>                
    <li></li>           
</ul>      
```

ul>li:first-child会先选中ul后的所有元素，然后是在所有元素中选出第一个元素，最后是检查这个元素标签是否li，但是上述情形中，ul后第一个元素的标签是span，所以没有元素被选中       
ul>li:first-of-type会选中ul后的所有元素，然后是在所有元素中选择元素标签是li的元素，不计算除li外的元素（span），最后是在剩下的元素中选择第一个元素,所以ul后第一个li被选中了       
:not()：否定伪类，将符合条件的元素从选择器中剔除       
	案例：ul>li:not(:nth-child(3))：先选中ul后的所有元素，然后是在所有元素中选中第3个元素，最后是从所有元    	素中剔除刚刚选中的那个，选中剩下的元素
:link：用来表示未访问过的链接(其实应该是正常的链接)            
	案例：a:link{color:red}        
:visited：用来表示访问过的链接，该选择器内只可修改颜色            
	案例：a:visited{color:red}        
:hover：表示鼠标移入的状态        
:active：表示鼠标点击        
:link和:visited是超链接独有的，:hover和:active是所有元素都可以使用的

### 3.10.10.伪元素选择器：

​	表示页面  一些特殊的并不真实的存在的元素     
​	伪元素使用::开头     :
​	:first-letter:表示第一个字母     
​	::first-line:表示第一行     
​	::selection表示选中的内容         
​		案例：p::selection{color: green}         
​		效果：选中的内容字体变为绿色     
​	::before 元素的开始     
​	::after 元素的结尾         
​		before和after必须结合content使用，content可以在元素开始或结尾添加内容，
​		然后before和after才会起作用     
​	案例：div::before{content: 'abc';color: red;}     
​	效果：在div元素前方会添加内容abc，并且abc颜色会是红色

选择器练习网址： https://flukeout.github.io/ 

### 3.10.12.选择器权重

样式的冲突：当我们通过不同的选择器，并且为相同的样式设置不同的值时，此时就会发生样式的冲突发生样式的冲突时会以选择器的权重决定

选择器大的权重：            			正确的算法       简单的算法    

​			内联样式                			1,0,0,0         	1000    
​			id选择器                 			0,1,0,0         	100    
​			类，伪类，属性选择器      0,0,1,0             10    
​			元素选择器              			0,0,0,1             1   
​			通配选择器              			0,0,0,0    
​			继承的样式              			无优先级    
比较选择器优先级时需要将所有优先级的权重进行相加，最后优先级越高越优先显示    
选择器累加不会超过其优先级的数量级，即类选择器最大不超过10，即使是11个类选择器相加也达不到10    
也就是说选择器越具体优先级越高    
优先级权重相同时，优先使用后面的样式    
可以在某些样式后买你加 !important，则该样式会获得最高优先级权重，会超过内联样式，需谨慎使用        
​	案例：#id{color: red !important;}

## 3.11.长度单位

长度单位：   
	em：        
		em是根据元素的字体大小来计算的        
		1em=1font-size        
		em会根据字体大小改变，字体默认是16px        
		案例：

```css
div{                
    width: 10em;                
    height: 10em;                
    background-color: red               
}
```



​         此时div是一个160px的正方形,div的样式里如果添加font-size: 10px;则div会变成100px的正方形    	 

  rem：        
​         rem是根据根元素的字体大小进行计算        
​         案例：   

```css
div{            
    width: 10rem;            
    height: 10rem;            
    background-color: red        
}  
```



​         此时div是一个160px的正方形,样式里如果添加html{font-size: 10px;}，则div会变成100px的正方形



## 3.12.盒模型

盒模型、盒子模型、框模型（box model）
- CSS将页面中的所有元素都设置为了一个矩形的盒子
- 将元素设置为矩形的盒子后，对页面的布局就变成将不同的盒子摆放到不同的位置
- 每一个盒子都由一下几个部分组成：
内容区（content）
内边距（padding）
边框（border）
外边距（margin）

内容区（content），元素中的所有的子元素和文本内容都在内容区中排列
	内容区的大小由width 和 height两个属性来设置
	width 设置内容区的宽度
	height 设置内容区的高度

边框（border），边框属于盒子边缘，边框里边属于盒子内部，出了边框都是盒子的外部
	**边框的大小会影响到整个盒子的大小**
	要设置边框，需要至少设置三个样式：
		边框的宽度 border-width
		边框的颜色 border-color
		边框的样式 border-style

### 3.12.1.边框

```html
  
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        .box1{
            width: 200px;
            height: 200px;
            background-color: #bfa;

            /* 
                边框
                    边框的宽度 border-width
                    边框的颜色 border-color
                    边框的样式 border-style
             */

             /* 
             border-width: 10px; 
                默认值，一般都是 3个像素
                border-width可以用来指定四个方向的边框的宽度
                    值的情况
                        四个值：上 右 下 左
                        三个值：上 左右 下
                        两个值：上下 左右
                        一个值：上下左右
                    
                除了border-width还有一组 border-xxx-width
                    xxx可以是 top right bottom left
                    用来单独指定某一个边的宽度
                    
             */
             /* border-width: 10px; */
             /* border-top-width: 10px;
             border-left-width: 30px; */

            color: red;
            /*border-bottom: red solid 1px;*/

             /* 
                border-color用来指定边框的颜色，同样可以分别指定四个边的边框
                    规则和border-width一样
                border-color也可以省略不写，如果省略了则自动使用color的颜色值
              */
             /* border-color: orange red yellow green;
             border-color: orange; */


            /* 
                border-style 指定边框的样式
                    solid 表示实线
                    dotted 点状虚线
                    dashed 虚线
                    double 双线
                    border-style的默认值是none 表示没有边框
             */
             /* border-style: solid dotted dashed double;
             border-style: solid; */

             /* border-width: 10px;
             border-color: orange;
             border-style: solid; */

             /* 
                border简写属性，通过该属性可以同时设置边框所有的相关样式，并且没有顺序要求
                除了border以外还有四个 border-xxx
                    border-top
                    border-right
                    border-bottom
                    border-left
              */
              /* border: solid 10px orange; */
              /* border-top: 10px solid red;
              border-left: 10px solid red;
              border-bottom: 10px solid red; */

              border: 10px red solid;
              border-right: none;
        }
    </style>
</head>
<body>
    <div class="box1"></div>
</body>
</html>
```



### 3.12.2.内边距

- 内边距的设置会影响到盒子的大小
- 背景颜色会延伸到内边距上
- 一共盒子的可见框的大小，由内容区 内边距 和 边框共同决定
- 所以在计算盒子大小时，需要将这三个区域加到一起计算

​                

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        .box1{
            width: 200px;
            height: 200px;
            background-color: transparent;
            border: 10px orange solid;

            /* 
                内边距（padding）
                    - 内容区和边框之间的距离是内边距
                    - 一共有四个方向的内边距：
                        padding-top
                        padding-right
                        padding-bottom
                        padding-left
                    - 内边距的设置会影响到盒子的大小
                    - 背景颜色会延伸到内边距上
                一共盒子的可见框的大小，由内容区 内边距 和 边框共同决定，
                    所以在计算盒子大小时，需要将这三个区域加到一起计算
             */

             /* padding-top: 100px;
             padding-left: 100px;
             padding-right: 100px;
             padding-bottom: 100px; */

             /* 
                padding 内边距的简写属性，可以同时指定四个方向的内边距
                    规则和border-width 一样
              */

              padding: 10px ;
        }

        .inner{
            width: 100%;
            height: 100%;
            background-color: yellow;
        }
    </style>
</head>
<body>
    <div class="box1">
        <div class="inner"></div>
    </div>
</body>
</html>
```



### 3.12.3.外边距

- 外边距不会影响盒子可见框的大小
- 但是外边距会影响盒子的位置
- 默认情况下如果我们设置的左和上外边距则会移动元素自身而设置下和右外边距会移动其他元素



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        .box1{
            width: 200px;
            height: 200px;
            background-color: #bfa;
            border: 10px red solid;

            /* 
                外边距（margin）
                    - 外边距不会影响盒子可见框的大小
                    - 但是外边距会影响盒子的位置
                    - 一共有四个方向的外边距：
                        margin-top
                            - 上外边距，设置一个正值，元素会向下移动
                        margin-right
                            - 默认情况下设置margin-right不会产生任何效果
                        margin-bottom
                            - 下外边距，设置一个正值，其下边的元素会向下移动
                        margin-left
                            - 左外边距，设置一个正值，元素会向右移动
                        - margin也可以设置负值，如果是负值则元素会向相反的方向移动
                    - 元素在页面中是按照自左向右的顺序排列的，
                        所以默认情况下如果我们设置的左和上外边距则会移动元素自身
                        而设置下和右外边距会移动其他元素
                    - margin的简写属性
                        margin 可以同时设置四个方向的外边距 ，用法和padding一样
                    - margin会影响到盒子实际占用空间
             */

             /* margin-top: 100px;
             margin-left: 100px;
             margin-bottom: 100px; */

             /* margin-bottom: 100px; */
             /* margin-top: -100px; */
             /* margin-left: -100px; */
             /* margin-bottom: -100px; */

             /* margin-right: 0px; */

             margin: 100px;

        }

        .box2{
            width: 220px;
            height: 220px;
            background-color: yellow
        }
    </style>
</head>
<body>
    <div class="box1"></div>
    <div class="box2"></div>
</body>
</html>
```



### 3.12.4.水平布局

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        .outer{
            width: 800px;
            height: 200px;
            border: 10px red solid;
        }

        .inner{
            /* width: auto;  width的值默认就是auto*/
            width: 100px;
            height: 200px;
            background-color: #bfa;
            /*margin-right: auto;*/
            /*margin-left: auto;*/
            /* margin-left: 100px;
            margin-right: 400px */
            /* 
                元素的水平方向的布局：
                    元素在其父元素中水平方向的位置由以下几个属性共同决定“
                        margin-left
                        border-left
                        padding-left
                        width
                        padding-right
                        border-right
                        margin-right
                    一个元素在其父元素中，水平布局必须要满足以下的等式
margin-left+border-left+padding-left+width+padding-right+border-right+margin-right = 其父元素内容区的宽度 （必须满足）
                0 + 0 + 0 + 800 + 0 + 0 + 0 = 800
                0 + 0 + 0 + 200 + 0 + 0 + 600 = 800
                100 + 0 + 0 + 200 + 0 + 0 + 400 = 800
                100 + 0 + 0 + 200 + 0 + 0 + 500 = 800
                    - 以上等式必须满足，如果相加结果使等式不成立，则称为过度约束，则等式会自动调整
                        - 调整的情况：
                            - 如果这七个值中没有为 auto 的情况，则浏览器会自动调整margin-right值以使等式满足
                    - 这七个值中有三个值和设置为auto
                        width
                        margin-left
                        maring-right
                        - 如果某个值为auto，则会自动调整为auto的那个值以使等式成立
                            0 + 0 + 0 + auto + 0 + 0 + 0 = 800  auto = 800
                            0 + 0 + 0 + auto + 0 + 0 + 200 = 800  auto = 600
                            200 + 0 + 0 + auto + 0 + 0 + 200 = 800  auto = 400
                            auto + 0 + 0 + 200 + 0 + 0 + 200 = 800  auto = 400
                            auto + 0 + 0 + 200 + 0 + 0 + auto = 800  auto = 300
                        - 如果将一个宽度和一个外边距设置为auto，则宽度会调整到最大，设置为auto的外边距会自动为0
                        - 如果将三个值都设置为auto，则外边距都是0，宽度最大
                        - 如果将两个外边距设置为auto，宽度固定值，则会将外边距设置为相同的值
                            所以我们经常利用这个特点来使一个元素在其父元素中水平居中
                            示例：
                                width:xxxpx;
                                margin:0 auto;
             */
        }
    </style>
</head>
<body>

    <div class="outer">

        <div class="inner"></div>

    </div>
    
</body>
</html>
```



### 3.12.5.垂直布局

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <link rel="stylesheet" href="../stone/css/reset.css">
    <style>
        
        .outer{
            background-color: #bfa;
            height: 600px;
            /* 
                默认情况下父元素的高度被内容撑开
             */
        }

        .inner{
            width: 100px;
            background-color: yellow;
            height: 100px;
            margin-bottom: 100px;
            
        }

        .box1{
            width: 200px;
            height: 200px;
            background-color: #bfa;
            /* 
                子元素是在父元素的内容区中排列的，
                    如果子元素的大小超过了父元素，则子元素会从父元素中溢出
                    使用 overflow 属性来设置父元素如何处理溢出的子元素
                    可选值：
                        visible，默认值 子元素会从父元素中溢出，在父元素外部的位置显示
                        hidden 溢出内容将会被裁剪不会显示
                        scroll 生成两个滚动条，通过滚动条来查看完整的内容
                        auto 根据需要生成滚动条
                overflow-x: 
                overflow-y:
             */
            overflow: auto;

            
        }

        .box2{
            width: 100px;
            height: 400px;
            background-color: orange;
        }
    
    </style>
</head>
<body>
    <!-- <div class="outer">
        <div class="inner"></div>
        <div class="inner"></div>
    </div> -->
    <div class="box1">在我的后园，可以看见墙外有两株树，一株是枣树，还有一株也是枣树。</div>
    <div class="box1">在我的后园，可以看见墙外有两株树，一株是枣树，还有一株也是枣树。</div>
    <div class="box1">在我的后园，可以看见墙外有两株树，一株是枣树，还有一株也是枣树。</div>
    <div class="box1">在我的后园，可以看见墙外有两株树，一株是枣树，还有一株也是枣树。</div>
    <div class="box1">在我的后园，可以看见墙外有两株树，一株是枣树，还有一株也是枣树。</div>
    </body>
</html>
```



### 3.12.6.外边距的折叠

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        .box1 , .box2{
            width: 200px;
            height: 200px;
            font-size: 100px;
        }

        /* 
            垂直外边距的重叠（折叠）
                - 相邻的垂直方向外边距会发生重叠现象
                - 兄弟元素
                    - 兄弟元素间的相邻垂直外边距会取两者之间的较大值（两者都是正值）
                    - 特殊情况：
                        如果相邻的外边距一正一负，则取两者的和
                        如果相邻的外边距都是负值，则取两者中绝对值较大的
                    - 兄弟元素之间的外边距的重叠，对于开发是有利的，所以我们不需要进行处理
                - 父子元素
                    - 父子元素间相邻外边距，子元素的会传递给父元素（上外边距）
                    - 父子外边距的折叠会影响到页面的布局，必须要进行处理
        
         */

        .box1{
            background-color: #bfa;

            /* 设置一个下外边距 */
            margin-bottom: -100px;
            margin-left: auto;
            margin-right: auto;
        }

        .box2{
            background-color: orange;

            /* 设置一个上外边距 */
            margin-top: 100px;
        }

        .box3{
            width: 200px;
            height: 200px;
            background-color: #bfa;
            /* padding-top: 100px; */
            /* border-top: 1px #bfa solid; */
        }

        .box4{
            width: 100px;
            height: 100px;
            background-color: orange;
            margin-top: 100px;
        }
    </style>
</head>
<body>
    <div class="box1">
    </div>
    <div class="box2"></div>
    <!-- <div class="box1"></div>
    <div class="box2"></div> -->  
</body>
</html>
```



### 3.12.6.行内元素的盒模型

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        .s1{
            background-color: yellow;

            /* 
                行内元素的盒模型
                    - 行内元素不支持设置宽度和高度
                    - 行内元素可以设置padding，但是垂直方向padding不会影响页面的布局
                    - 行内元素可以设置border，垂直方向的border不会影响页面的布局
                    - 行内元素可以设置margin，垂直方向的margin不会影响布局
             */
             /* width: 100px;
             height: 100px; */

             /* padding: 100px; */

             /* border: 100px solid red; */

             margin: 100px;
        }

        .box1{
            width: 200px;
            height: 200px;
            background-color: #bfa;
        }

        a{
            /* 
                display 用来设置元素显示的类型
                    可选值：
                        inline 将元素设置为行内元素
                        block 将元素设置为块元素
                        inline-block 将元素设置为行内块元素 
                                行内块，既可以设置宽度和高度又不会独占一行
                        table 将元素设置为一个表格
                        none 元素不在页面中显示
                visibility 用来设置元素的显示状态
                    可选值：
                        visible 默认值，元素在页面中正常显示
                        hidden 元素在页面中隐藏 不显示，但是依然占据页面的位置
             */
            display: block;

            visibility: hidden;

            width: 100px;
            height: 100px;
            background-color: orange;
        }
    </style>
</head>
<body>

    <a href="javascript:;">超链接</a>
    <a href="javascript:;">超链接</a>


    <span class="s1">我是span</span>
    <span class="s1">我是span</span>
    
    <div class="box1"></div>
</body>
</html>
```



### 3.12.7.默认样式

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
     <link rel="stylesheet" href="../stone/css/reset.css">
<!--    <link rel="stylesheet" href="./css/normalize.css">-->

    <!-- 
        重置样式表：专门用来对浏览器的样式进行重置的
            reset.css 直接去除了浏览器的默认样式
            normalize.css 对默认样式进行了统一
     -->
    <style>
        /* 
            默认样式：
                - 通常情况，浏览器都会为元素设置一些默认样式
                - 默认样式的存在会影响到页面的布局，
                    通常情况下编写网页时必须要去除浏览器的默认样式（PC端的页面）
         */

        /* body{
            margin: 0;
        }
        p{
            margin: 0;
        }
        ul{
            margin: 0;
            padding: 0;
            /* 去除项目符号 * /
            list-style:none; 
        } */

        /* *{
            margin: 0;
            padding: 0;
        } */


        .box1{
            width: 100px;
            height: 100px;
            border: 1px solid black;
        }
    </style>
</head>
<body>
   
<div class="box1"></div>
<p>我是一个段落</p>
<p>我是一个段落</p>
<p>我是一个段落</p>
<ul>
    <li>列表项1</li>
    <li>列表项2</li>
    <li>列表项3</li>
</ul>
</body>
</html>
```



### 3.12.8.盒模型尺寸

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        div{
            width: 100px;
            height: 100px;
            background-color: #393;
            /*border: 10px solid red;*/
            /*
                默认情况下，盒子大小是由内容区，边框，内外边距共同决定的
                box-sizing：指定盒模型尺寸的计算方式
                    可选值：
                        content-box：默认值，有高度和宽度决定内容区大小
                        border-box:宽度与高度用来设置盒模型可见框的大小
                                    width和height指的是内容区，边框，内外边距的总大小，
            */
            box-sizing: border-box;
        }
    </style>
</head>
<body>
<div></div>
</body>
</html>
```



### 3.12.9.轮廓线

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        div{
            width: 100px;
            height: 100px;
            background-color: #393;
            outline: 10px solid red;
            /*
                outline：用于设置元素的轮廓线，用法与border相同
                轮廓与边框不同之处：轮廓不会影响到边框大小
                添加border会使得内容区下移，保证元素默认外边距不变
                添加outline并不会使得内容区下移，保证元素默认外边距会变
            */           
        }
    </style>
</head>
<body>
<div></div>
</body>
</html>
```



### 3.12.9.阴影效果

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        div{
            width: 100px;
            height: 100px;
            background-color: #393;
            /*
                box-shadow：设置元素得的阴影效果，阴影不会影响布局效果，一般阴影会在元素正下方，看不见
                    第一个值：阴影的水平偏移量，正值为向右偏移，负值为向左偏移
                    第一个值：阴影的水平偏移量，正值为向右偏移，负值为向左偏移
                    第三个值：阴影的模糊半径
                    第四个值：阴影的颜色
            */
            box-shadow: 9px 9px 5px rgba(23,33,44, .3);
        }
    </style>
</head>
<body>
<div></div>
</body>
</html>
```



![1584190779726](D:\MyNote\images\1584190779726.png)

### 3.12.10.圆角

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        div{
            width: 100px;
            height: 100px;
            background-color: #393;
            /*
                border-radius：用于设置圆角，圆角设置的圆的半径大小,
                    四个值时，左上，右上，右下，左下
                    三个值时，左上，右上/左下，右下
                    两个值时，左上/右下，右上/左下
                    一个值时，左上/右下/右上/左下
                border-top-left-radius: 设置元素左上角圆角半径
                border-top-right-radius: 设置元素右上角圆角半径
                border-bottom-right-radius: 设置元素右下角圆角半径
                border-bottom-left-radius: 设置元素左下角圆角半径
                border-radius: 10px;
                border-radius: 50%;将元素设置为一个圆形
                */
            border-radius: 50%;
        }
    </style>
</head>
<body>
<div></div>
</body>
</html>
```



## 3.16.动画

### 3.16.1.过渡效果

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        .box1{
            width: 700px;
            height: 700px;
            background-color: #999999;
        }
        .box1 div{
            width: 100px;
            height: 100px;
            background-color: #b9cb41;
            /*transition: all 2s;*/
            margin-bottom: 100px;
        /*    transition:过渡,
                --通过过渡,可以指定一个属性发生变化的切换方式
                --通过过渡可以创建一些非常好的效果,很好的提升用户体验
        */
            /*transition-property: 指定需要执行过渡效果的属性;
                   多属性之间可以使用逗号隔开,如果所有属性都需要过渡效果,则可以使用all关键字,
                   大部分属性都支持过渡效果
            */
            transition-property: all;
            /*transition-property: height, width;*/
            /*transition-duration: 指定执行过渡的持续时间;
                指定的时间单位是秒(s)和毫秒(ms)
                如果需要对不同属性执行不同过渡时间,可以在transition-property中将属性分开写,在transition-duration中按照位置写对应时间即可
            */
            transition-duration: 2s;
            /*transition-duration: 1s, 2s;*/
            /*transition-timing-function: 指定过渡的时序函数,即过渡的执行方式
                    可选值:
                        ease:默认值,慢速开始,先加速后减速停止,贝塞尔曲线对应cubic-bezier(.25, .1, .25, 1)
                        linear:匀速运动,贝塞尔曲线对应cubic-bezier(0, 0, 0, 1)
                        ease-in: 加速运动,慢速开始,加速然后停止
                        ease-out: 减速运动,高速开始,减速然后停止
                        ease-in-out:,慢速开始,先加速后减速停止,变化比ease剧烈
                        cubic-bezier(x1, y1, x2, y2):贝塞尔曲线,参考网址:https://cubic-bezier.com
                        steps(4):分步执行过渡效果,每过一秒执行一次效果,4次后效果执行完毕,
                                 内部可以有两个参数,第一个指定执行步数,第二个指定在时间段开始前执行,还是之后执行
                        steps(4, start):在时间段开始时就执行一次
                        steps(4, end):在时间段结束时就执行一次,默认值

            ;*/
            /*transition-timing-function: ease;*/
            /*transition-delay: ; 过渡效果的延迟时间,当触发过渡效果时,等待指定的延迟时间,再进行效果的过渡*/
        }
        .box2{
            /*transition-timing-function: steps(4, start);*/
            /*transition-delay: ; 过渡效果的延迟时间,当触发过渡效果时,等待指定的延迟时间,再进行效果的过渡*/
            /*transition-delay: 1s;*/
            /*transition可以将需要设置的东西一起设置,但是如果指定了两个时间的,后面的时间是延迟时间*/
            transition: all 2s ease-in 1s;
        }
        .box3{
            background-color: aqua;
        }
        .box1:hover div{
            /*width: 200px;*/
            /*height: 200px;*/
            margin-left: 600px;
        }
    </style>
</head>
<body>
<div class="box1">
    <div class="box2"></div>
    <div class="box3"></div>
</div>
</body>
</html>
```



### 3.16.2.动画

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        .box1{
            width: 700px;
            height: 700px;
            background-color: #999999;
        }
        .box1 div{
            width: 100px;
            height: 100px;
            background-color: #b9cb41;
            margin-bottom: 100px;
        }
        .box2{
            /*设置动画*/
            /*animation-name:指定要对当前元素生效的名字*/
            animation-name: test;
            /*animation-duration:指定动画执行时间*/
            animation-duration: 2s;
            /*animation-delay:指定动画执行需要延迟的时间*/
            animation-delay: 1s;
            /*animation-timing-function:指定动画的时序函数*/
            animation-timing-function: ease-in;
            /*animation-iteration-count:指定动画的迭代器,或动画执行次数
                可选值:
                    数值: 执行的次数,默认是1
                    infinite: 无限次
            */
            animation-iteration-count: 3;
            /*animation-direction:指定动画的执行方向
                 可选值:
                    normal: 默认是从from向to方向运行,每次执行方向相同
                    reverse:反着来,从to向from方向运行,每次执行方向相同
                    alternate: 去时是从from向to方向运行,重复执行时会反方向运行,即从to向from方向运行
                    alternate-reverse:去时是从to向from方向运行,重复执行时会反方向运行,即从from向to方向运行
            */
            animation-direction: alternate;
            /*animation-play-state:指定动画的播放状态,
                可选值:
                    running: 默认值,动画执行
                    paused: 动画暂停
            */
            /*animation-play-state: initial;*/
            /*animation-fill-mode:动画的填充方式
                可选值:
                    none: 默认值,动画执行完毕元素回到原来位置
                    forwards: 动画执行结束,元素停在动画结束位置
                    backwards: 动画延时等待时,元素会处于开始位置,如果动画效果有颜色,则颜色会在等地延迟时就会有from的颜色变化,而不是保持元素原来颜色
                    both: 结合了forwards与backwards的特性
            */
            animation-fill-mode: both;
            /*  animation: 动画的简写方式,只对两个时间的位置有要求*/
            /*animation: test 2s 2 1s alternate;*/
        }
        .box1:hover div{
            /*margin-left: 600px;*/
            animation-play-state: paused;
        }

        /*动画:
            动画与过渡类似,都可以实现一些动态效果
                不同的是过渡需要在某个属性发生变化时才会触发
                动画可以自动触发
            设置动画就必须先设置一个关键帧,关键帧设置了动画的每一个执行步骤
        */
        @keyframes test {
            /*from表示动画开始的位置,也可以用0%表示*/
            from{
                margin-left: 0;
                background-color: red;
            }
            /*to表示动画结束的位置,也可以用100%表示*/
            to{
                background-color: #b9cb41;
                margin-left: 600px;
            }
        }
    </style>
</head>
<body>
<div class="box1">
    <div class="box2"></div>
</div>
</body>
</html>
```



### 3.16.3.变形-平移

x轴与y轴的平移

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        body{
            background-color: #dedede;
        }
        .box1{
            width: 200px;
            height: 200px;
            background-color: rgb(123, 216, 221);
            margin: 0 auto;
            transform: translateX(50%) ;
        }
        .box2{
            width: 200px;
            height: 200px;
            background-color: rgb(23, 116, 121);
            margin: 0 auto;
        }
    /*    变形:指通过css改变元素的形状或位置
            -变形不会影响到元素的布局
            -transform用于设置元素的变形效果
                 -平移:
                    translateX(): 沿着x轴方向平移,元素移动时,原来的位置还占着,移动后的位置不会脱离文档流,但也不会挤压其他元素,但会覆盖其他元素
                    translateY(): 沿着y轴方向平移
                    translateZ(): 沿着z轴方向平移
                       平移元素时所使用的百分比是相对于自身大小的
    */
        .box3{
            background-color: #b9cb41;
            position: absolute;
            /*top: 0;这种方式只适用于元素宽高确定的情况
            left: 0;
            right: 0;
            bottom: 0;
            margin: auto;*/
            top: 50%;
            left: 50%;
            transform: translateX(-50%) translateY(-50%);
        /*    这种方式适用于不确定元素宽高确定的情况*/
        }
        .box4,.box5{
            width: 220px;
            height: 300px;
            background-color: #FFF;
            float: left;
            margin: 0 10px;
            transition: all .3s;
        }
        .box4:hover, .box5:hover{
            transform: translateY(-5px);
            box-shadow: 0 0 5px rgba(0, 0, 0, .4);
        }
    </style>
</head>
<body>
<div class="box1"></div>
<div class="box2"></div>
<div class="box3">1111111111111111</div>
<div class="box4"></div>
<div class="box5"></div>
</body>
</html>
```



z轴的平移

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        html{
            /*设置当前网页的视距为800像素人眼距离网页的距离*/
            perspective: 800px;
        }
        body{
            border: 1px solid red;
        }
        .box1{
            width: 100px;
            height: 100px;
            background-color: #b9cb41;
            margin: 100px auto;
            transition: .3s;
        }
        body:hover .box1{
            /*
                z轴平移,调整元素在z轴方向的位置,正常情况下就是调整元素与人眼之间的距离
                    距离越大,元素离人越近
                z轴平移属于立体效果(近大远小),默认情况下网页是不支持透视的,如果需要看到效果就必须设置网页的视距
            */
            transform: translateZ(600px);
        }
    </style>
</head>
<body>
<div class="box1"></div>
</body>
</html>
```



### 3.16.4.变形-旋转

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        html{
            /*设置当前网页的视距为800像素人眼距离网页的距离*/
            perspective: 800px;
        }
        body{
            border: 1px solid red;
        }
        .box1{
            width: 100px;
            height: 100px;
            background-color: #b9cb41;
            margin: 100px auto;
            transition: .3s;
            /*animation: test 1s ease-in-out infinite;*/
        }
        /*@keyframes test {
            from{
                transform: rotateY(180deg)  translateZ(400px)
            }
            to{
                transform: rotateY(90deg)  translateZ(0px)
            }
        }*/
        body:hover .box1{
            /*
                通过旋转可以使元素沿着x,y,z轴旋转指定的角度
                    rotateX()
                    rotateY()
                    rotateZ()
                        旋转的角度可以是720deg(720度,即2圈),1turn(一圈).200grad(相当于180度,半圈)
            */
            transform:  rotateY(180deg)  translateZ(400px);
            /*transform: translateX(100px) rotateY(180deg)  ;*/
            /*backface-visibility:设置元素背面是否可见*/
            backface-visibility: visible;
        }
    </style>
</head>
<body>
<div class="box1"></div>
</body>
</html>
```



### 3.16.5.缩放

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .box1{
            width: 100px;
            height: 100px;
            background-color: greenyellow;
            margin: 100px auto;
            transition: transform .5s;
            /*设置变形的原点*/
            transform-origin: 0 0 ;
        }
        .box1:hover{
            /*
                对元素进行缩放的函数
                    scaleX(): 水平方向的缩放
                    scaleY(): 垂直方向的缩放
                    scale(): 水平垂直两个方向的缩放
            */
            transform: scale(.2);
        }
    </style>
</head>
<body>
<div class="box1"></div>
</body>
</html>
```



### 3.17.less

```less
//这个是less中的注释，不会被解析到css中
// 通过@import可以将其他less文件引入到这里面
@import"sysnx.less"
/*
    这个是css的注释，会被解析到css中
*/
body{
    background-color: silver;
    div{
        width: 100px;
        height: 100px;
        background-color: rgb(117, 189, 199);
    }
}
// 变量，可以在变量中存储一个任意的数值
// 并且我们可以在需要时任意修改变量中的值
// 变量的语法：@变量名
@a:100px;
@b:red;
@c:box4;
.box3{
    width: @a;
}
.@{c}{
    width: @a;
    height: $width;
    background-color: @b;
}

.box1{
    .box2{
        color: red;
    }
    >.box3{
        color: red;
    }
    +.box4{
        color: red;
    }
    // &代表外层的父元素
    &:hover div{
        color: red;
    }
    div &:hover.box2{
        color: red;
    }
}
.p1{
    width: 100px;
    height: 100px;
}
// :extend()为当前选择器扩展指定的选择器的样式(选择器分组)
.p2:extend(.p1){
    color: red;
}
.p3{
    // 直接对直送的样式进行引用，这里就相当于将p1的样式在这里进行了复制
    // mixin：混合，将p2中独有的样式复制过来
    .p2();
}
// 使用类选择器可以在选择器后面添加一对括号，这时我们就创建了一个mixin
.p4(){//这个是一个混合函数，不会出现在css中，而是供其他选择器引用
    width: 100px;
    height: 100px;
    background-color: red;
}
.p5{
    .p4();
}
// 混合函数，在混合函数中是可以传参的,可以设置默认值(@s:200px)
.test2(@s){
    width: @s;
}
.test{
    // 调用混合函数时就必须按照顺序填写参数，也可以按照变量名:值(@s:200px)的方式传参
    .test2(200px);
}
// 在less中所有的数值都可以直接运算,包含加减乘除
.bo{
    width: 100px + 120px;
}
```



## 3.17.像素

### 3.17.1.像素

像素：

​      -屏幕是由一个个发光的点组成的，这些点就是像素；

​      -分辨率，：1920*1080就是指屏幕中的小点数量

​      -在前端开发中像素分为物理像素和css像素

​      -物理像素就是上述的小点

​      -css像素就是编写html时用到的像素

​        -浏览器在在显示网页时，需要先将css像素转化为物理像素再显示

​        -css像素最终由几个屋里像素组成，需要由浏览器决定

​        -默认情况下，在pc端，一个css像素-一个物理像素

​      

​      视口（viewport）：

​        -视口就是屏幕中显示网页的区域

​        -可以通过查看视口大小判断css像素与物理像素的比值

​        -默认情况下

​          视口宽度

​            css像素 1920

​            物理像素 1920

​            此时两者比例是1：1

​        -放大两倍的情况下

​          视口宽度

​            css像素  960

​            物理像素 1920

​             此时两者比例是1：2

​        -因此我们可以通过改变视口大小改变两者的像素比

### 3.17.2.手机像素

手机像素：

​      -在不同屏幕上，单位像素是不一样的，像素越小屏幕越清晰

​      笔记本屏幕  24寸  1920*1080

​      iphone6屏幕 4.7寸 750*1334

​      智能手机的像素点远小于计算机的像素点

​      问题：一个宽度是980的网页如何在苹果6中显示呢？

​      默认情况下，移动端网页都会将视口设定为980像素

​        以确保网页可以在移动端可以正常显示，但是如果网页宽度超过980时

​        移动端会自动将网页进行缩放以确保可以完整显示网页



​      所以大部分pc端网站都可以在移动端正常浏览，但是体验一般不会好

​        为解决这个问题，dd啊部分网站  都会专门为移动端设计一个网页

### 3.17.3.完美视口

移动端默认视口是980px(css像素)

​        默认情况下，移动端的像素比就是 980/移动端宽度（980/750）

​        如果我们在网页中编写移动端代码，这样在980的视口下，像素是非常不好的

​          会导致网页内容非常小

​        所以编写移动端网页时必须确保有一个比较合理的像素比

​          1css像素对应2个物理像素

​          1css像素对应3个物理像素

​        可以通过meta标签设置视口大小

​        每一款移动设备设计时，都会有一个最佳的像素比

​          一般只需要将像素比设置为改制就可以得到一个最佳效果

​          将像素比转化为最佳像素比的视口可以称之为完美视口

​        将视口设置为完美视口

​		` <meta name="viewport" content="width=device-width, initial-scale=1.0">`

​        结论：以后写移动端网页时，先写这个就可以了

## 3.18.less

### 3.18.1.简介

less是一门css的预处理语言 --less是css的增强版,
        通过less可以编写更少的代码实现更强大的样式 --在less中添加了许多d的新特性,
        例如对变量的支持,
        对mixin的支持 --less语法上和css差不多,
        但是less增添了许多对css的扩展 所以l浏览器无法直接执行less代码,
        要执行就必须先转换成css代码再由浏览器执行

### 3.18.2.选择器的嵌套

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Title</title>
	<style type="text/less">
		html{
			body{
				/* less的嵌套语法,less支持选择器之间的相互嵌套 */
			}
		}
	</style>
	
</head>

<body>	
    /* 通过引入less.js，同时将css类型改为text/less就可以在html中写less了，如同css*/
	<script src="./less.min.js"></script>
</body>

</html>
```



### 3.18.3.less的加减乘除

### 3.18.4.less的mixin函数

### 3.18.5.less的变量

### 3.18.6.less的避免编译

```less
// 通过@import可以将其他less文件引入到这里面
@import"sysnx.less"
//这个是less中的注释，不会被解析到css中
/*
    这个是css的注释，会被解析到css中
*/
body{
    background-color: silver;
    div{
        width: 100px;
        height: 100px;
        background-color: rgb(117, 189, 199);
    }
}
// 变量，可以在变量中存储一个任意的数值
// 并且我们可以在需要时任意修改变量中的值
// 变量的语法：@变量名:变量值
@a:100px;	//可以代表属性值
@m:margin;	//可以代表属性名，不推荐
@b:red;		
@c:box4;	//可以代表选择器名字，不推荐
.box3{
    width: @a;//可以代表属性值
}
//可以代表选择器名字
.@{c}{
    width: @a;
    height: $width;
    background-color: @b;
}

.bo1{
    @{m}: 100px + 120px;//可以代表属性名，不推荐
}
.box1{
    .box2{
        color: red;
    }
    >.box3{
        color: red;
    }
    +.box4{
        color: red;
    }
    // &代表外层的父元素，不加&的话代表这个选择器与父元素是父子关系
    &:hover div{
        color: red;
    }
    div &:hover.box2{
        color: red;
    }
}
.p1{
    width: 100px;
    height: 100px;
}
// :extend()为当前选择器扩展指定的选择器的样式(选择器分组)
.p2:extend(.p1){
    color: red;
}
.p3{
    // 直接对直送的样式进行引用，这里就相当于将p1的样式在这里进行了复制
    // mixin：混合，将p2中独有的样式复制过来
    .p2();
}
// 使用类选择器可以在选择器后面添加一对括号，这时我们就创建了一个mixin
.p4(){//这个是一个混合函数，不会出现在css中，而是供其他选择器引用
    width: 100px;
    height: 100px;
    background-color: red;
}
.p5{
    .p4();
}
//mixin函数，不带参数的,且会在css中显示的
.p{}
//mixin函数，不带参数的,且不会在css中显示的
.p(){}
//mixin函数，带参数的（可有多个参数），使用这个mixin时必须传对应数量的参数
.p(@s){}
//mixin函数，带参数的,且参数有默认值的
.p(@s:100px){}
//有了默认值，使用mixin时参数就不是必须的了
//当有多个参数时，参数与值位置需对应，但是如果.p(@s:100px);在传参时指定参数值对应的参数名就可以只传
//对应位置的参数
// mixin函数，又名混合函数，在混合函数中是可以传参的,可以设置默认值(@s:200px)
.test2(@s){
    width: @s;
}
.test{
    // 调用混合函数时就必须按照顺序填写参数，也可以按照变量名:值(@s:200px)的方式传参
    .test2(200px);
}
// 在less中所有的数值都可以直接运算,包含加减乘除
.bo{
    width: 100px + 120px;
}
.po{
    width: ~"calc(100px+100)";//通过在~"内容"可以避免less对其进行编译，而是保持原样
}
```



### 3.18.7.mixin函数的匹配模式

```less
.triangle(@_){//使用@_去匹配第一个形参
	width: 0;
	height: 0;
	overflow: hidden;
}
.triangle(R, @w, @c){//三角朝向右侧的三角
	
	border-style: dashed  dashed dashed solid;
	border-color: transparent transparent transparent @c;
	border-width: @w;
	
}

.triangle(L, @w, @c){//三角朝向左侧的三角
	border-style: dashed solid dashed dashed;
	border-color: transparent @c transparent transparent;
	border-width: @w;
}

//使用函数
.border{
	.triangle(R, 100px, pink);//向左侧的三角
}
//使用函数
.border{
	.triangle(R, 100px, pink);//向左侧的三角
}
.border1(@a, @b, @c){
	border: @arguments;//@arguments就代表了上面的三个形参
}
.border2{
	.border1(1px,solid, red);
}
```



## 3.7.统一样式表.css

```css
/*! normalize.css v8.0.1 | MIT License | github.com/necolas/normalize.css */

/* Document
   ========================================================================== */

/**
 * 1. Correct the line height in all browsers.
 * 2. Prevent adjustments of font size after orientation changes in iOS.
 */

html {
  line-height: 1.15; /* 1 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

/* Sections
   ========================================================================== */

/**
 * Remove the margin in all browsers.
 */

body {
  margin: 0;
}

/**
 * Render the `main` element consistently in IE.
 */

main {
  display: block;
}

/**
 * Correct the font size and margin on `h1` elements within `section` and
 * `article` contexts in Chrome, Firefox, and Safari.
 */

h1 {
  font-size: 2em;
  margin: 0.67em 0;
}

/* Grouping content
   ========================================================================== */

/**
 * 1. Add the correct box sizing in Firefox.
 * 2. Show the overflow in Edge and IE.
 */

hr {
  box-sizing: content-box; /* 1 */
  height: 0; /* 1 */
  overflow: visible; /* 2 */
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

pre {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/* Text-level semantics
   ========================================================================== */

/**
 * Remove the gray background on active links in IE 10.
 */

a {
  background-color: transparent;
}

/**
 * 1. Remove the bottom border in Chrome 57-
 * 2. Add the correct text decoration in Chrome, Edge, IE, Opera, and Safari.
 */

abbr[title] {
  border-bottom: none; /* 1 */
  text-decoration: underline; /* 2 */
  text-decoration: underline dotted; /* 2 */
}

/**
 * Add the correct font weight in Chrome, Edge, and Safari.
 */

b,
strong {
  font-weight: bolder;
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

code,
kbd,
samp {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/**
 * Add the correct font size in all browsers.
 */

small {
  font-size: 80%;
}

/**
 * Prevent `sub` and `sup` elements from affecting the line height in
 * all browsers.
 */

sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}

/* Embedded content
   ========================================================================== */

/**
 * Remove the border on images inside links in IE 10.
 */

img {
  border-style: none;
}

/* Forms
   ========================================================================== */

/**
 * 1. Change the font styles in all browsers.
 * 2. Remove the margin in Firefox and Safari.
 */

button,
input,
optgroup,
select,
textarea {
  font-family: inherit; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

/**
 * Show the overflow in IE.
 * 1. Show the overflow in Edge.
 */

button,
input { /* 1 */
  overflow: visible;
}

/**
 * Remove the inheritance of text transform in Edge, Firefox, and IE.
 * 1. Remove the inheritance of text transform in Firefox.
 */

button,
select { /* 1 */
  text-transform: none;
}

/**
 * Correct the inability to style clickable types in iOS and Safari.
 */

button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}

/**
 * Remove the inner border and padding in Firefox.
 */

button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

/**
 * Restore the focus styles unset by the previous rule.
 */

button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
  outline: 1px dotted ButtonText;
}

/**
 * Correct the padding in Firefox.
 */

fieldset {
  padding: 0.35em 0.75em 0.625em;
}

/**
 * 1. Correct the text wrapping in Edge and IE.
 * 2. Correct the color inheritance from `fieldset` elements in IE.
 * 3. Remove the padding so developers are not caught out when they zero out
 *    `fieldset` elements in all browsers.
 */

legend {
  box-sizing: border-box; /* 1 */
  color: inherit; /* 2 */
  display: table; /* 1 */
  max-width: 100%; /* 1 */
  padding: 0; /* 3 */
  white-space: normal; /* 1 */
}

/**
 * Add the correct vertical alignment in Chrome, Firefox, and Opera.
 */

progress {
  vertical-align: baseline;
}

/**
 * Remove the default vertical scrollbar in IE 10+.
 */

textarea {
  overflow: auto;
}

/**
 * 1. Add the correct box sizing in IE 10.
 * 2. Remove the padding in IE 10.
 */

[type="checkbox"],
[type="radio"] {
  box-sizing: border-box; /* 1 */
  padding: 0; /* 2 */
}

/**
 * Correct the cursor style of increment and decrement buttons in Chrome.
 */

[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/**
 * 1. Correct the odd appearance in Chrome and Safari.
 * 2. Correct the outline style in Safari.
 */

[type="search"] {
  -webkit-appearance: textfield; /* 1 */
  outline-offset: -2px; /* 2 */
}

/**
 * Remove the inner padding in Chrome and Safari on macOS.
 */

[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/**
 * 1. Correct the inability to style clickable types in iOS and Safari.
 * 2. Change font properties to `inherit` in Safari.
 */

::-webkit-file-upload-button {
  -webkit-appearance: button; /* 1 */
  font: inherit; /* 2 */
}

/* Interactive
   ========================================================================== */

/*
 * Add the correct display in Edge, IE 10+, and Firefox.
 */

details {
  display: block;
}

/*
 * Add the correct display in all browsers.
 */

summary {
  display: list-item;
}

/* Misc
   ========================================================================== */

/**
 * Add the correct display in IE 10+.
 */

template {
  display: none;
}

/**
 * Add the correct display in IE 10.
 */

[hidden] {
  display: none;
}
```



## 3.3.去除默认样式表.css

```css
/* v2.0 | 20110126
  http://meyerweb.com/eric/tools/css/reset/ 
  License: none (public domain)
*/
html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed, 
figure, figcaption, footer, header, hgroup, 
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
	margin: 0;
	padding: 0;
	border: 0;
	font-size: 100%;
	font: inherit;
	vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure, 
footer, header, hgroup, menu, nav, section {
	display: block;
}
body {
	line-height: 1;
}
ol, ul {
	list-style: none;
}
blockquote, q {
	quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
	content: '';
	content: none;
}
table {
	border-collapse: collapse;
	border-spacing: 0;
}
```

