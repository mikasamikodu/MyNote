# 1．Jquery

## 1.1. js不好的地方

| 序号 | 缺点                                  |
| ---- | ------------------------------------- |
| 1    | 代码冗余，需要遍历，可能还需要嵌套    |
| 2    | 找对象麻烦，方法少，使用麻烦          |
| 3    | 有兼容性问题                          |
| 4    | 实现简单的动画时，需要使用animate对象 |
| 5    | 注册事件会被覆盖(后面的会覆盖前面的)  |

## 1.2  jquery初体验

首先引入jquery.js文件:

<script type="text/javascript" src="jquery-1.12.4.js"></script>

然后建立jquery入口，并在内部建立：

```javascript
$(document).ready();//代表HTML文档准备好，是jquery入口的标准写法

$(document).ready(function() {
   console.log('hello jquery');
});
```

//function写在ready中

Jquery对Microsoft和Google很支持，如果不想引入本地的jquery文件，可以通过Google或Microsoft引入jquery文件。

Google:

<script type=’text/javascript’ src=’http://ajax.googleapis.com/ajax/libs/jquery/1.4.0/jquery.min.js’></script>

Microsoft:

<script type=’text/javascript’ src=’http://ajax.microsoft.com/ajax/jquery/jquery-1.4.min.js’></script>

## 1.3. 元素选择器

> Jquery元素选择器和属性选择器允许使用标签名、属性、内容对HTML元素进行选择。

| 表现形式   | 作用                     |
| ---------- | ------------------------ |
| $(“p”)     | 查找标签元素<p>          |
| $(“.demo”) | 查找`class=”demo”`的元素 |
| $(“#demo”) | 查找`id=”demo”`的元素    |

## 1.4. 注册事件

`$("#color").click(function() {
​    $("div").show();
});`

为`id=”color”`的元素注册点击事件(click),function内部是事件具体内容。

在事件这一部分，与js不同的是只需要去除on即可。Js与jquery在事件这一部分只差一个on。

## 1.5. 关于循环

> Jquery会自动迭代，不需要自己迭代。

## 1.6. 入口函数

Jquery入口函数有2种，分别是:

```javascript
$(function(){
    console.log("jquery的第二种入口");
});

$(document).ready(function() {
    console.log("jquery第一种入口");
});
```

> Jquery的入口函数与js的入口函数`window.onload()`,都会等待文档加载完成才执行，但是jquery的入口函数不会等待图片的加载。

## 1.7. 动画

### 1.7.1. 显示、隐藏

```javascript
$("p").show();//显示，显示已被隐藏的元素
$("p").hide();//隐藏，隐藏正在显示的元素
```

> 定义与语法

语法：`$(selector).show(speed,callback)`

| 参数     | 描述                                                         |
| -------- | ------------------------------------------------------------ |
| speed    | <p>可选。规定元素从隐藏到完全可见的速度。默认为 "0"。</p>    |
|          | 可能的值：                                                   |
|          | 毫秒 （比如 1500）, "slow" ,"normal", "fast"                 |
|          | 在设置速度的情况下，元素从隐藏到完全可见的过程中，会逐渐地改变其高度、宽度、外边距、内边距和透明度。 |
| callback | 可选。show 函数执行完之后，要执行的函数。                    |
|          | 如需学习更多有关 callback 的内容，请访问我们的 jQuery Callback 这一章。 |
|          | 除非设置了 speed 参数，否则不能设置该参数。                  |

> *提示*：如果元素已经是完全可见，则该效果不产生任何变化，除非规定了 callback 函数。

*注释*：该效果适用于通过 jQuery 隐藏的元素，或在 CSS 中声明 display:none 的元素（但不适用于 visibility:hidden 的元素）。

### 1.7.2. 滑入、滑出、切换

```javascript
$("div").slideUp(1000);//滑入，从下向上收缩元素
$("div").slideDown(1000);//划出，从上向下伸展元素
$("div").slideToggle(1000);//切换，元素每点击一次，便会在滑入与滑出状态间切换一次
```

> 定义与语法与显示隐藏相同

### 1.7.3. 淡入、淡出、切换

```javascript
$("div").fadeIn(1000);//淡入，元素透明度从0到1
$("div").fadeOut(1000);//淡出，元素透明度从1到0
$("div").fadeToggle(1000);//切换，元素每点击一次，便会在淡入或淡出状态间切换一次
```

> 定义与语法与显示隐藏相同

### 1.7.4. 自定义动画animate

```javascript
$("div").animate({left:800}, 2000, "linear", function(){
                console.log("yooo, jquery!");
            });
```

> 定义与语法

| 位置 | 含义                   | 作用                                           |
| ---- | ---------------------- | ---------------------------------------------- |
| 1    | 元素的样式，是一个数组 | 代表元素从现在的样式将会变化为被定义的样式     |
| 2    | 变化的速度             | 代表元素从开始到结束的时间                     |
| 3    | 变化的快慢             | 可选参数："swing"(秋千/摇摆)、"linear"(匀加速) |
| 4    | 回调函数callback       | 完成动画后执行函数                             |

### 1.7.5. 停止动画stop

```javascript
$div.stop(false, true);
```

> 定义与语法

| 参数位置 | 选项       | 效果                           |
| -------- | ---------- | ------------------------------ |
| 1        | true/false | 是否停止当前动画并清除动画队列 |
| 2        | true/false | 是否显示当前动画的最终动画效果 |

### 1.7.6. delay

> 效果：延迟动画的播放

```javascript
$("div").fadeIn(1000).delay(1000).fadeOut(1000);
//效果是div将会在1s内以淡入的动画出现，然后维持2s，最后在1s内以淡出的动画隐藏
```



## 1.8. text和html

### 1.8.1. text()

> 实例

```javascript
$("div").text("<p>我是文本2。</p>")//设置p元素的内容,将div元素设置为‘<p>我是文本2。</p>’ 
$("div").text()//获取div元素的内容，不包含div元素内的标签元素

```

> 定义

设置和获取被选元素的文本内容，文本内容不会识别标签元素，一律视为字符串。

### 1.8.2. html()

> 示例

```javascript
$("div").html()//获取div元素的内容，包含div元素内部的标签元素
$("div").html("<p>我是文本。</p>")
//设置div元素的内容，将div元素的内容设置为一个值为‘我是文本。’的p标签
```

## 1.9. jquery与dom对象

*a*  : dom对象是一个对象(dom对象即js对象)，jquery对象是一个伪数组，里面是js对象；

*b*  :dom对象与jquery对象不能使用对方的方法，例如：

```javascript
var btn = document.getElementById('btn');
btn.onclick = function(){};
var $btn = $('#btn');//btn是专门用于js对象，$btn是用于jquery对象
$btn.onclick = function(){};//$btn.onclick无法生效
$btn[0].onclick = function(){};//$btn[0].onclick可以生效
//jquery转dom对象方法是$btn[0]，即取出一个js对象即可，类似的方法还有$btn.get(0)
//dom对象转jquery对象方法是$(btn)，即将dom对象置于$()中即可
```

## 1.10. 操作样式

### 1.10.1. 修改单个css样式

```javascript
//css(name, value);name指需要修改的css的名字，value是对应的值
$("#btn").css("backgroundColor","red");
```

### 1.10.2. 修改多个css样式

```javascript
$("li").css({
    "backgroundColor": "lightblue",
    "border": "1px solid black"
});
```

### 1.10.3. 获取css样式

```javascript
$("li").css("backgroundColor")
```

## 1.11. 鼠标悬浮事件

| 方法                      | 区别                                                 |
| ------------------------- | ---------------------------------------------------- |
| mouseover()-mouseout()    | 鼠标指针先经过事件元素然后事件元素的子元素算经过两次 |
| mouseenter()-mouseleave() | 鼠标指针先经过事件元素然后事件元素的子元素只算一次   |

## 1.12. 层级选择器

| 选择器     | 表现形式   | 作用                       |
| ---------- | ---------- | -------------------------- |
| 并集选择器 | $("s1,s2") | 查找元素内有s1或s2的元素   |
| 后代选择器 | $("s1 s2") | 查找位于元素s1内部的s2元素 |
| 子代选择器 | $("s1>s2") | 查找与元素s1挨着的s2元素   |
| 交集选择器 | $("s1s2")  | 查找元素有s1且有s2的元素   |

## 1.13. 过滤选择器

```javascript
 $(function () {
        //下标从0开始
        $("li:even").css("backgroundColor", "red");//下标是偶数的
        $("li:odd").css("backgroundColor", "lightblue");//下标是奇数的
        $("li:first").css("fontSize", "30px");//下标是第一个的
        $("li:last").css("width", "100px");//下标是最后一个的
        $("li:eq(8)").css("width", "200px");//下标等于8的
        $("li:gt(5)").css("color", "white");//下标大于5的
        $("li:lt(5)").css("color", "pink");//下标小于5的
  });

```

## 1.14. 表单选择器

| 表现形式 | 作用                       |
| -------- | -------------------------- |
| input    | 选择输入框元素             |
| password | 选择密码输入框元素         |
| text     | 选择文本输入框元素         |
| radio    | 选择单选框元素             |
| checkbox | 选择复选框元素             |
| submit   | 选择提交按钮元素           |
| image    | 选择图片元素               |
| reset    | 选择重置按钮元素           |
| button   | 选择按钮元素               |
| file     | 选择文件元素               |
| hidden   | 选择隐藏元素               |
| enabled  | 选择禁用元素               |
| disabled | 选择可用元素               |
| checked  | 选择被选中的单选框或复选框 |
| selected | 选择被选中的下拉框         |

## 1.15. 筛选选择器

| 选择器     | 作用                                                         | demo                    |
| ---------- | ------------------------------------------------------------ | ----------------------- |
| children() | 查找某元素的子元素                                           | $(this).children("ul")  |
| siblings() | 查找某元素的兄弟元素（不包含自已）                           | $(this).siblings("li")  |
| find("li") | 在某元素的子元素中查找指定的元素                             | $(this).find("li")      |
| next()     | 查找某元素的下一个元素（是否必须是同级元素）                 | $(this).next("div")     |
| parent()   | 查找某元素的父级元素                                         | $(this).parent("li")    |
| prevAll()  | 查找某元素前面的所有元素                                     | $(this).prevAll()       |
| nextAll()  | 查找某元素后面的元素                                         | $(this).nextAll()       |
| end()      | 结束上一个查找元素方法prevAll()的效果，让上上一个查找元素的方法$(this)再次生效 | $(this).prevAll().end() |

## 1.16. 操作class（类）

### 1.16.1 . 添加类

```javascript
$("li").addClass("basic");
```

### 1.16.2. 删除类

```javascript
$("li").removeClass("basic");
```

### 1.16.3. 切换类的有无

> 当元素中有某个类时，将会删除这个类；当元素没有这个类时，将会添加这个类；

```javascript
 $("li").toggleClass("basic");
```

### 1.16.4. 判断类的有无

```javascript
$("li").hasClass("basic");
```

## 1.17. 操作属性

### 1.17.1. 修改单个属性

```javascript
$("img").attr("alt", "灵梦1号");
```

### 1.17.2. 修改多个属性

```javascript
$("img").attr({
            "alt": "灵梦2号",
            "title": "东方幻想乡",
    		"aaa": "bbb"
        });
```

### 1.17.3. 获取属性

```javascript
$("img").attr("alt");
```

> 注意：在。jquery1.6之后，对于checkbox的input的checked属性，attr将会出现问题，需要使用其他的方法(prop方法)进行替代。原因是attr对布尔类型的属性无法操作。

```javascript
$("input").prop("checked", true);
$("input").prop("checked");
```

### 1.17.4. 移除单个属性

```javascript
$("img").removeAttr("title");//移除图片的标题属性
```

## 1.18. 操作音频

> 方法 

| 方法         | 作用                                                         | 演示           |
| ------------ | ------------------------------------------------------------ | -------------- |
| load()       | 控制加载                                                     | m.load()       |
| play()       | 控制播放                                                     | m.play()       |
| pause()      | 控制暂停                                                     | m.pause()      |
| fastSeek(20) | 指定播放时间，这样的话，音频会定位到20秒的播放位置。不过目前只有Firefox浏览器支持，你可以通过currentTime属性来实现。 | m.fastSeek(20) |

> 属性 

| 属性        | 作用                                                         | 演示              |
| ----------- | ------------------------------------------------------------ | ----------------- |
| currentTime | 获取和设置已播放的时间，返回的数字以( s )秒为单位            | m.currentTime=10  |
| autoplay    | 是否自动播放                                                 | m.autoplay = true |
| loop        | 是否循环播放                                                 | m.loop = true     |
| controls    | 是否显示控制面板                                             | m.controls = true |
| muted       | 是否静音                                                     | m.muted = true    |
| paused      | 是否暂停，判断音频当前是否暂停，返回true代表暂停，返回false代表正在播放；**默认是true；该值只能读取，不能修改**。 | m.paused          |
| volume      | 调节音量，音量的取值范围在：**0（无声）~1（最大声）之间**。可以对volume属性赋合理的值或者做一些运算，来改变音频的音量。 | m.volume = 0.1    |

## 1.19. 添加节点

> 方法

| 方法       | 演示               | 结果                                 |
| ---------- | ------------------ | ------------------------------------ |
| append()   | $div.append($p)    | 将p元素加在div元素的元素内部的最后面 |
| prepend()  | $div.prepend($p)   | 将p元素加在div元素的元素内部的最前面 |
| appendTo() | $div.appendTo($p)  | 将div元素加在p元素的元素内部的最后面 |
| after()    | $p.after($div)     | 将div元素加在p元素的元素外部后面     |
| before()   | $div.before($p)    | 将div元素加在p元素的元素外部前面     |
| $()        | $("<span></span>") | 创建一个span元素                     |

## 1.20. 节点的删除克隆

> 方法

| 方法     | 演示                      | 作用                                                         | 范围                 |
| -------- | ------------------------- | ------------------------------------------------------------ | -------------------- |
| html()   | $div.html("")             | 可以清空节点，会造成内存泄漏（只清空div内部节点并将其置为空，未清除内部节点相关事件） | 用于从父节点清空元素 |
| empty()  | $div.empty()              | 可以清空节点，不会造成内存泄漏（清空div内部节点并清除内部节点相关事件） | 用于从父节点清空元素 |
| remove() | $div.remove()             | 删除自己这个节点与相关事件                                   | 用于移除自身元素     |
| clone()  | $p.clone().appendTo($div) | 克隆自身节点                                                 | 用于克隆自身元素     |

> 注意

clone()可以传入参数true/false，默认参数是false。传入true时，会进行深度复制，而且会复制元素相关事件；传入false时，只会进行深度复制，不会复制元素相关事件。

## 1.21. val

> 用于获取和设置text、textarea等可输入内容的元素的值。

```javascript
$txt.val("洋酒");//设置元素内容
$txt.val();//获取元素内容

```

## 1.22. width和height

### 1.22.1. 设置元素的宽度

| 方法         | 演示                   | 效果                                                |
| ------------ | ---------------------- | --------------------------------------------------- |
| width()      | $div.width()           | 获取div元素的width                                  |
|              | $div.width(400)        | 设置div元素的width为400px                           |
| innerWidth() | $div.innerWidth()      | 获取div元素的width与padding的和                     |
| outerWidth() | $div.outerWidth(false) | 获取div元素的width、padding、border三者之和         |
|              | $div.outerWidth(true)  | 获取div元素的width、padding、border、margin四者之和 |

### 1.22.2. 设置元素高度

| 方法          | 演示                    | 效果                                                 |
| ------------- | ----------------------- | ---------------------------------------------------- |
| height()      | $div.height()           | 获取div元素的height                                  |
|               | $div.height(400)        | 设置div元素的height为400px                           |
| innerHeight() | $div.innerHeight()      | 获取div元素的height与padding的和                     |
| outerHeight() | $div.outerHeight(false) | 获取div元素的height、padding、border三者之和         |
|               | $div.outerHeight(true)  | 获取div元素的height、padding、border、margin四者之和 |

### 1.22.3. 获取屏幕宽高

```javascript
$(window).width();//宽度
$(window).height();//高度
```

## 1.23. scrollTop和scrollLeft

> 例子

```javascript
$window.scroll(function(){						//注册滚动条滚动事件
            console.log($window.scrollTop());	//打印竖向滚动条的位置
            console.log($window.scrollLeft());	//打印横向滚动条的位置
 });
//屏幕向下滑动时在控制台打印坐标，向右滑动时同样打印。
```

> 兼容性

```javascript
$("html,body").animate({scrollTop: 0}, 2000);
//注册动画，当浏览器为ie6，7，8时，用html；火狐谷歌用body
```

## 1.24. offset与position

```javascript
console.log($(".son").offset().top);	//打印自身相对于document的位置
console.log($(".son").position().left); //打印自身相对于有定位的父元素的位置
```

## 1.25. 事件委托机制

简单事件绑定>bind事件绑定>delegate事件绑定>on事件绑定（推荐）

### 1.25.1. click和onclick

```javascript
$("p").click(function(){ 
    alert("111");
});
```

> 缺点：一次注册一个事件

### 1.25.2. bind

```javascript
$("p").click(function(){
     alert("111");
});
//一次注册一个事件
 $("p").bind("click mouseenter", function(){
     alert("222");
 });
//一次为不同的动作注册同一的事件
$("p").bind({"click":function(){
    alert("333");
},"mouseenter":function(){
    alert("444");
}});
//一次为不同动作注册不同的事件
```

> 注意：上述两种事件注册方式共有的缺点就是只能为已有元素注册事件，注册完事件后新增的元素并不会被注册事件。只能为自己这个元素注册事件的事件机制称为简单事件机制。

### 1.25.3 delegate

```javascript
$("div").delegate("p", "click", function(){
    alert("555");
});
```

可以为内部子元素注册事件。

> 参数含义

| 位置   | 作用                                |
| ------ | ----------------------------------- |
| 第一个 | 填写选择器                          |
| 第二个 | 填写事件类型（ 如click,mouseenter） |
| 第三个 | 非必填项                            |
| 第四个 | 事件发生时需要执行的函数            |

> 委托机制原理

​	首先向父元素注册事件，然后当元素被触发事件时，会向上传递给父元素，父元素将会为其注册事件，最后该事件引动函数。类似的例子有快递员给人发货，会先发给快递之家，然后有快递之家发送给具体的人。

### 1.25.4. on

```javascript
$("button").on("click", function(){ //为自身元素注册事件
    $("<p>我是新的p元素。</p>").appendTo("div");
});
$("div").on("click", "p", function(){//为内部子元素注册事件
    alert("222");
});
```

> 参数含义

| 位置   | 作用                                     |
| ------ | ---------------------------------------- |
| 第一个 | 填写事件类型（ 如click,mouseenter）      |
| 第二个 | 填写选择器（必须是注册事件元素的子元素） |
| 第三个 | 非必填项                                 |
| 第四个 | 事件发生时需要执行的函数                 |

委托机制原理与delegate相似。

### 1.25.5. off

```javascript
$("p").on("mouseenter click", function(){//为p元素注册点击与鼠标经过事件
    alert("1111");
});
$("p").off("mouseenter");//将p元素的鼠标经过事件移除
```

> 效果：p元素只剩点击事件

### 1.25.6. trigger

```javascript
$("p").on("mouseenter click", function(){//为p元素注册点击与鼠标经过事件
    alert("1111");
});
$("#btn").on("click", function(){//为button元素注册点击事件
    // $("p").click();		//按钮被点击时，触发p元素的点击事件
    $("p").trigger("click");//按钮被点击时，触发p元素的点击事件
});
```

## 1.26. 阻止事件冒泡与默认行为

```javascript
$("a").on("click", function(){
    alert("111");
    e.preventDefault();//阻止元素的默认行为
    e.stopPropagation();//阻止元素的冒泡行为
    //return false; //同时阻止元素的默认行为和冒泡行为
});

```

## 1.27. each

```javascript
for(var i=0;i<$("li").length;i++){
    $("li").eq(i).css("opacity", (i+1)/10);
}
$("li").each(function(index, element){
    $(element).css("opacity", (index+1)/10);
});
//上下效果相同，将10个li依次排开，并且透明度逐渐增加，从0到1

```

## 1.28. noConflict

> $的冲突

当引入2个不同的js文件时，如果二者都需要使用$,则必然会产生冲突。为解决冲突可通过noConflict()方法释放$的控制权，改为jQuery获得控制权，或者通过noConflict()方法换一个变量控制jquery。

```javascript
<script src='new.js'></script>//引入另一个使用$的js文件
<script src='jquery-1.12.4.js'></script>//引入jquery.js文件
<script>
	 var c = $.no.noConflict();//1.释放$的控制权，改为由c控制jquery
jQuery(function(){//2.用jQuery代替$控制jquery
    
});
</script>
```

## 1.29. 引入插件color

```javascript
<script src="jquery-1.12.4.js"></script>
<script src="jquery-2.1.2.color.js"></script>
<script>
    $(function(){
        $("div").animate({backgroundColor: "green"}, 3000, function(){
            alert("hello");
        });
    });
</script>
//插件只需引入就可以起作用
```

## 1.30. 引入插件lazyload

```javascript
<body>
<img class="lazy" data-original="images/a.jpg" alt="">//2.将图片src改为data-original

<script src="jquery-1.12.4.js"></script>
<script src="jquery.lazyload.js"></script>//1.引入js文件
<script>
    $(function(){
        $("img.lazy").lazyload();//3.调用lazyload方法
    });
</script>
//作用：当页面图片过多时，可以使图片可以暂时不加载，等到需要时再加载。
```

## 1.31.引入插件ui

> 增加了js对css的操作部分

```javascript
script src="jquery-1.12.4.js"></script>
<script src="jquery-ui.js"></script>
<script>
    $(function(){
        $(".container").draggable({//整个div可拖动
            handle: ".top"		   //限制为只有顶部导航栏可拖动这个div
        });
        $("ul").sortable({			//ul内部的li可通过拖动进行排序
            opacity: 0.3			//拖动li时，将其透明度变为0.3
        });
        $(".resize").resizable({	//div可扩展大小
            minHeight: 160,			//限制最小高度为160px
            handles: "s"			//限制只有div下面可拖动
        });
    });
```

## 1.32. 制作插件

```javascript
$.fn.bgColor = function(color){
    this.css("backgroundColor", color); //this代表使用这个方法的元素
    return this;	//返回this是为了链式编程可以进行下去
};
//bgColor为方法名称,function为其内容，可传参数
//使用时需先引入jquery，再引入自己做的插件
```

