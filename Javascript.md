# 4． Javascript

## 4.1. 开头

```javasc
<script type="text/javascript">
    var btn1 = document.getElementById('color');
    var btn2 = document.getElementById('content');
    var div = document.getElementsByTagName('div');

    btn1.onclick = function() {
        for(var i=0;i<div.length;i++) {
            div[i].style.display = 'block';
        }
    };

    btn2.onclick = function() {
        for(var i=0;i<div.length;i++) {
            div[i].innerText = 'content';
        }
    };
</script>
```



*a*  : 注意拼写错误；

*b*  : innerText在火狐浏览器中有兼容性问题,低版本的火狐浏览器不支持innerText，指出textContent,textContent在ie6，7,,8中不支持；

*c*  : js改变css样式需要在元素后加style，在加具体样式（如display,color）

## 3.8.width

```css
#header{min-width:100px;}
```

:arrow_forward: min-width:设置元素最小宽度

## 3.9. img

```css
#img{background:url(images/bg.png) no-repeat top center}
```

:arrow_forward: no-repeat:图片不平铺展开，后面的top center产生效果是使图片随页面缩小而随之缩小，展示部分始终是中间部分。

## 3.10.box-shadow

> 作用：box-shadow 属性向框添加一个或多个阴影。

> 属性表

| 值         | 描述                                      |
| ---------- | ----------------------------------------- |
| *h-shadow* | 必需。水平阴影的位置。允许负值。          |
| *v-shadow* | 必需。垂直阴影的位置。允许负值。          |
| *blur*     | 可选。模糊距离。                          |
| *spread*   | 可选。阴影的尺寸。                        |
| *color*    | 可选。阴影的颜色。请参阅 CSS 颜色值。     |
| inset      | 可选。将外部阴影 (outset) 改为内部阴影。> |

示例1

```css
div{box-shadow: 10px 10px 5px #888888;}
```

效果：![1552380660631](D:\MyNote\images\1552380660631.png)

实例2

```css
div{box-shadow: 1px 10px 5px #888888;}
```

效果：![1552380763966](D:\MyNote\images\1552380763966.png)

实例3

```css
div{box-shadow: 10px 1px 5px #888888;}
```

效果：![1552380826847](D:\MyNote\images\1552380826847.png)

实例4

```css
div{box-shadow: 10px 1px 5px #ccc;}
```

效果：![1552380910043](D:\MyNote\images\1552380910043.png)