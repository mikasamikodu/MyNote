# 2． HTML

## 2.1. Idea快捷键

### 2.1.1. div*3(按tab生效)

- 效果：

```html
<div></div>
<div></div>
<div></div>
```

### 2.1.2. shift+Enter

- 作用：在当前行下方生成新的一行，并且光标下移到新的这一行。

### 2.1.3. ul>li{我是第$个li}*10

- 效果：

  ```javas
  <ul>
      <li>我是第1个li</li>
      <li>我是第2个li</li>
      <li>我是第3个li</li>
      <li>我是第4个li</li>
      <li>我是第5个li</li>
      <li>我是第6个li</li>
      <li>我是第7个li</li>
      <li>我是第8个li</li>
      <li>我是第9个li</li>
      <li>我是第10个li</li>
  </ul>
  ```

### 2.1.4. ctrl+d

- 作用：向下复制当前行内容

### 2.1.5. ctrl+shift+/

- 作用：注释被选中部分。

### 2.1.6. ctrl+/

- 作用：分别注释被选中的每一行。

## 2.2. 无序序列ul

> *a*   :如何让无序序列的序号消失？

```css
<style type='text/css'>
li{
    list-style:none;
}
</style>
```

## 2.3. 音频audio

> 定义

定义声音，比如音乐或其他音频流。

> 示例

```html
<audio src="mp3/1.mp3" controls></audio>
```

> 属性

| 属性     | 值             | 描述                                                         |
| -------- | -------------- | ------------------------------------------------------------ |
| autoplay | autoplay       | 如果出现该属性，则音频在就绪后马上播放。                     |
| controls | controls       | 如果出现该属性，则向用户显示控件，比如播放按钮。             |
| preload  | auto,meta,none | 如果出现该属性，则音频在页面加载时进行加载，并预备播放。如果使用 "autoplay"，则忽略该属性。 |
| loop     | loop           | 如果出现该属性，则每当音频结束时重新开始播放。               |
| src      | url            | 要播放的音频的 URL。                                         |
| muted    | muted          | 加了muted属性，**音频即使在播放的时候，也是没有声音**，除非用户手动调整控制面板的音量。 |

> 提示

可以在开始标签和结束标签之间放置文本内容，这样老的浏览器就可以显示出不支持该标签的信息。

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

## 2.5. 表格table

> 示例

```html
<table border="1">
  <tr>
    <th>Month</th>
    <th>Savings</th>
  </tr>
  <tr>
    <td>January</td>
    <td>$100</td>
  </tr>
</table>
```

> 效果

![1551236855439](E:\typora-document\MyNote\images\1551236855439.png)

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