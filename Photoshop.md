## 1.PS基本操作

Ctrl+N:新建画布

Ctrl+O:新建画布并打开图片

 更改PS背景颜色：在菜单栏编辑下，打开首选项（Ctrl+K），点击左侧的界面选项，选择右侧颜色即可。

### 1.1.缩放工具

使用缩放工具的三种方式：（缩小或放大）

+ 按**Z键**（或点击缩放工具![1636636921871](F:\MyNote\images\1636636921871.png)），即可切换缩放工具
+ Ctrl+加号->放大物体，Ctrl+减号->缩小物体。
+ 按住Alt键并滑动滚轮(或使用鼠标左键左右拖拽)来放大/缩小物体。
+ 按住Alt键+空格键，即可切换缩放工具。

### 1.2.抓手工具

使用抓手工具的两种方式：（当物体超出视图栏或多张图层时，抓手工具才会起作用，背景与物体同时移动）

+ 按住空格键，光标会切换抓手工具。
+ 按**H键**（或点击抓手工具![1636637029994](F:\MyNote\images\1636637029994.png)）可以切换抓手工具。

### 1.3.移动工具

使用移动工具的三种方式：（在背景上移动物体）

+ 按**V键**即可切换移动工具
+ 使用移动工具时，按住Alt键可以通过拖拽物体来复制一个新物体，同时按住Shift键可以使目标保持平移状态
+ 通过移动工具可以将一个页面物体拖拽到另一个页面的物体中
+ 按Ctrl键+J键可以将物体在原来位置上复制一张
+ 按Ctrl键+Shift键+J键可以将物体从原来位置上提取出来，放入新建的图层
+ 使用移动工具时，按住Ctrl键可以通过鼠标左键点击图层选中某个图层，或者在移动工具的菜单栏勾选自动选择，在点击某物体时会自动选择对应物体所在图层，方便移动物体
+ 按住Shift键并选择多个图层，可以在工具菜单栏使用多种对齐方式（前六个控制水平或垂直对齐，后六个是控制平均分布）![1636720385413](F:\MyNote\images\1636720385413.png)。

### 1.4.自由变换

自由变换：

+ 按**Ctrl键+T键**，图层进入自由变换形态，图层周围出现边界框可以自由向四周拉伸。
+ 进入自由变换形态后，按住Alt键是以中心去放大缩小。
+ 进入自由变换形态后，按住Shift键可等比例放大。
+ 进入自由变换形态后，按住Alt键+Shift键可以以中心等比例放大。
+ 进入自由变换形态后，如果需要围绕某个中心旋转可以按住Alt键点击中心点，然后就可以围绕中心点旋转了
+ 进入自由变换形态后，右键可以选择缩放、旋转、斜切、扭曲、透视、变形等操作。
+ 自由变换完成之前，无法做其他操作。可以通过工具菜单栏最右侧的对勾确认自由变换已完成，也可以通过使用移动工具来确认，还有Ctrl键+Enter键确认。

### 1.5.选区工具

#### 1.5.1.选区工具使用方式

+ 按**M键**可以使用选取工具（圆形或方形）。按住Shift键，然后按M键可以切换圆形或方形选区工具。
+ 使用选取工具时，按Shift键会将选定区域变为正圆或正方形。
+ 使用选取工具时，同时按Shift键+Alt键会从中心绘制正圆或正方形。
+ 使用选取工具时，按住空格键，通过移动光标可以移动选区位置。
+ 使用选取工具完毕后，如需修改选区大小可右键点击变换选区，变换选区大小。
+ 使用选取工具完毕后，可通过点击空白处或Ctrl键+D键取消选区。
+ 确定选区后，先新建图层（快捷键Ctrl键+Shift键+N键或Ctrl键+Shift键+Alt键+N键），然后选色，按Alt键+Delete键是填充前景色，按Ctrl键+Delete键是填充背景色。
+ 新建一个和上一个选区同样大小的选区方法：按住Ctrl键，点击上一个选区所在图层，然后选择选区工具，新建图层，之后用鼠标移动上一个图层即可在新图层建立一个和上一个选区同样大小得到选区。
+ 填充颜色，确定选区后，再次填充颜色，如果放大图层会看到图层边缘还是有少许上一次填充颜色的痕迹，此时可以在填充颜色时，通过按住Shift键锁定透明元素，使得上一次填充颜色的痕迹彻底变为本次的填充颜色。

#### 1.5.2.选区修改方式

+ 平滑：进⾏选区圆⻆的改变
+ 扩展：将选区向外扩⼤指定的像素⼤⼩ （不易过⼤）
+ 收缩：将选区向内缩⼩指定的像素⼤⼩ （不易过⼤）
+ 羽化：将选区边缘变模糊效果，快捷键：SHIFT+F6 

羽化：![1636770047900](F:\MyNote\images\1636770047900.png)               收缩：![1636770080436](F:\MyNote\images\1636770080436.png)

扩展：![1636770119229](F:\MyNote\images\1636770119229.png)           平滑：![1636770225083](F:\MyNote\images\1636770225083.png)

#### 1.5.3.选区布尔运算

+ 确定第一个选区后，按住Alt键并选择一个与第一个选区相交的区域，结果会是减法，将第一次、第二次选区重叠部分删除。
+ 确定第一个选区后，按住Shift键并选择一个与第一个选区相交的区域，结果会是加法，将第一次、第二次选区非重叠部分联系到一起。
+ 确定第一个选区后，按住Shift键+Alt键并选择一个与第一个选区相交的区域，结果会是将第一次、第二次选区非重叠部分删除，留下重叠部分。
+ 按住Ctrl键点击图层可以直接载⼊选区（选择某个图层可以删除选区内的⾊块）。
+ 选择需要编组的图层，然后按Ctrl键+J键即可，取消编组是Ctrl键+Shift键+J键。
+ 按Ctrl键点击图层载入选区，按Ctrl键+Shift键+I键可以反向选择，将图层外面部分选区与里面部分选区进行反转，然后删除外面的选区，保留里面的。

#### 1.5.4.图层层次修改方法

撤销的使用方法：按Ctrl键+Z键可以撤回上一步操作（单次），按Ctrl键+Alt键+Z键可以连续撤回上一步操作（多次）。

图层层次顺序修改方法：

+ 通过拖拽图层来修改选区层次顺序；
+ 选择图层，按Ctrl键+】键，可以将图层向上调整一层；
+ 选择图层，按Ctrl键+【键，可以将图层向下调整一层；
+ 选择图层，按Ctrl键+Shift键+】键，可以将图层调整到顶层；
+ 选择图层，按Ctrl键+Shift键+【键，可以将图层调整到底层；

图层合并：Ctrl键+E键，将不同图层合到一个图层中。**注意**：利用形状绘制的图形合并时会将所有区域颜色都变为顶层图层的颜色，利用选区绘制的图形合并时则不会。

### 1.6.套索工具组

#### 1.6.1.套索工具

+ 套索工具用于创建不规则的选区。用法是选择套索工具（或按**L键**），然后按住鼠标左键不放并通过移动在图层上绘制选区即可，最后需要形成一个闭合的选区。

#### 1.6.2.多边形套索工具

+ 多边形套索工具用于绘制直⻆或尖⻆的选区。用法是选择多边形套索工具（按L），然后选择选区起点，单击⿏标左键松开，之后反复对图片的直角或尖角进行同⼀步操作，直⾄完成（形成闭合区域-标志是鼠标右下角出现小圆圈）。如果出现误操作时可以按退格键或删除键来删除“点”。

#### 1.6.3.磁性套索工具

+ 磁性套索工具可以⾃动识别背景与前景的边缘部分，适⽤于背景⾊单⼀或者边缘清晰对⽐较强的图像。用法是选择磁性套索工具（按L），单击⿏标左键松开⿏标顺应所选的对象边缘，直⾄完成形成闭合区域-标志是鼠标右下角出现小圆圈），如果出现误操作时可以按退格键或删除键来删除“点，需要边删除边鼠标后退。
+ 多边形套索工具、磁性套索工具选区完毕后可以选套索工具并按住Shift键添加选区或按住Alt键减少选区。
+ 确认选区完毕可以按Ctrl键+J键来提取选区。

### 1.7.快速选择工具组

#### 1.7.1.快速选择工具

+ 按**W键**可以切换快速选择工具,使⽤场景：对⽐强烈，颜⾊接近，可以快速选择需要载⼊选区的部分
+ 单击⿏标左键拖动，向外拉扩展选区，在使⽤过程中根据需要不断调整笔触大小 ，笔触大小调整⽅法：“按住Alt键并鼠标右键向左移动”变小；“按住Alt键并鼠标右键向右移动”变大。笔触硬度调整方法：“按住Alt键并鼠标右键向上移动”变小；“按住Alt键并鼠标右键向下移动”变大
+ 绘制过程中，默认为添加选区，按住Alt可以切换为减去选区，不需要自己去点击切换

#### 1.7.2.魔棒工具

![1637329218953](F:\MyNote\images\1637329218953.png)

+ 按W键可以切换快速选择工具,使⽤场景：对⽐强烈，颜⾊接近，可以快速选择需要载⼊选区的部分
+ 功能：可以快速选择背景单⼀的⾊彩区域。
+ 容差：选择的颜⾊范围 
+ 连续：如果选择连续，那么不连续的颜⾊将不会被选中

### 1.8.橡皮擦工具组

#### 1.8.1.橡皮擦工具

+ 按**E键**即可切换橡皮擦工具，按住鼠标左键可擦除当前图层内容

  ![1637332103394](F:\MyNote\images\1637332103394.png)

+ 模式可选橡皮擦的形状：画笔（圆形）、铅笔（圆形）、块（方形）
+ 不透明度大小可以影响擦除后的效果，将图层不完全擦除，留有一些影子或者说是变模糊的程度
+ 笔触⼤⼩调整⽅法：“按住Alt键并鼠标右键向左移动”变⼩；“按住Alt键并鼠标右键向右移动”变⼤。笔触硬度调整⽅法：“按住Alt键并鼠标右键向上移动”变⼩；“按住Alt键并鼠标右键向下移动”变⼤

#### 1.8.2.背景橡皮擦工具

![1637332579927](F:\MyNote\images\1637332579927.png)

+ 第一个是连续取样，基本不用
+ 第二个是单次取样，点击图层某处，获取此处颜色，之后橡皮擦只擦除此种颜色。
+ 第二个是背景色板取样，点击图层某处背景获取此处颜色或设置背景颜色，之后橡皮擦只擦除背景色中的此种颜色。
+ 使⽤场景：对⽐强烈，背景⾊单⼀

#### 1.8.3.魔术橡皮擦工具

+ 使⽤场景：对⽐强烈，背景⾊单⼀

+ 设置颜色，点击图层，直接将图层中所有对应颜色删除

#### 1.8.4.选择主体/天空

+ 在移动工具下或橡皮擦工具下，在工具菜单栏的**选择主体/天空**或菜单栏**选择**-**主体/天空**里进行选择主体/天空操作。
+ 可在对⽐强烈，背景⾊单⼀的场景里使用，用于一键抠图。
+ 只有PS2018版本以上才会有这个功能
+ **注意**：当背景⾊对⽐不强烈时，容易出现误差。

### 1.9.渐变色工具组

+ 按**G键**可切换渐变色工具，为图层添加渐变色

![1637335004263](F:\MyNote\images\1637335004263.png)

+ 在左侧颜色区域鼠标左键点击，可在新面板里的色条上直接调节颜色或在渐变色中多添加几种渐变色

![1637334734387](F:\MyNote\images\1637334734387.png)

+ 在色条中间添加的渐变色，可通过鼠标左键点击色条下侧的小方块并按Delete键进行删除
+ 按住Alt键，然后通过拖拽左侧色条下侧的小方块进行复制，调整渐变色

+ 左侧第二组的五个灰色小色块是调整渐变方向，第一个是线性渐变。以直线或⻆度线的形式表达渐变效果

  <img src="F:\MyNote\images\1637335399591.png" alt="1637335399591" style="zoom: 25%;" />

  第二个是径向渐变，以起点到终点为半径，绘制中⼼向四周扩散或放射的形式表达渐变

  <img src="F:\MyNote\images\1637335436464.png" alt="1637335436464" style="zoom:25%;" />

  第三个是角度渐变，以直线为起点，顺时针的形式呈现渐变效果

  <img src="F:\MyNote\images\1637335489090.png" alt="1637335489090" style="zoom:25%;" />

  第四个是对称渐变，以中⼼为轴，向两边延伸出相同渐变

<img src="F:\MyNote\images\1637335604408.png" alt="1637335604408" style="zoom:25%;" />

​		第五个菱形渐变，以起点为中⼼向四周延伸菱形渐变效果

<img src="F:\MyNote\images\1637335805305.png" alt="1637335805305" style="zoom:25%;" />

+ 设置不透明度：选择需要设置的不透明度⾊标，在下⾯不透明度框中输⼊数据即可，删除是向下拉，添加是 

  点击空⽩处

### 1.10.钢笔工具

![1637883166020](F:\MyNote\images\1637883166020.png)



+ 上图中的点称为锚点，点与点之间的线称为路径，空心锚点是未被选中的锚点，不可操作，实心锚点是被选中的锚点，可操作（用鼠标悬浮在锚点上，不同锚点光标显示图案不一样）。选中的锚点两侧有两条线，称为控制手柄，用于弯曲当前路径。
+ 在工具菜单栏的设置中可以设置橡皮筋

+ 按**P键**即可切换钢笔工具，通过鼠标左键的不断点击与拖拽，即可用钢笔工具画出路径与锚点
+ 画直线，可以通过鼠标左键点击即可，或者按住Alt键然后鼠标左键点击也可以
+ 画曲线。可以通过鼠标左键点击然后按住鼠标进行拖拽，直到路径符合要求即可。
+ 画路径时，按住Alt键并点击锚点可以删除一条控制手柄，按住Shift键可以添加手柄。手柄至多2条。
+ 在使用钢笔工具构图时，按**A键**切换钢笔工具为路径选择工具，然后按住Ctrl键点击任意锚点，可以选中所有锚点，将锚点进行整体拖拽；在使用钢笔工具构图时，一般为直接选择 工具，可以按住Ctrl键点击任一锚点，只会选择当前点击锚点，同时按住Shift键可同时选择多个锚点。单个锚点被选中后，如果没有出现控制手柄则可以按住Alt键，并在锚点处拖拽即可把控制手柄弄出来。 
+ 添加锚点可以在路径时直接点击即可，删除锚点可以直接点击锚点。添加/删除锚点需先勾选工具菜单栏的自动添加/删除选择框，然后选中对应路径才可以在路径上添加/删除锚点
+ 按住Alt键，点击锚点可将锚点在平滑锚点与转折锚点间进行转换
+ 按住Alt  键并点击控制手柄可以操作一条控制手柄
+ 按住Ctrl键并点击控制手柄可以操作两条控制手柄
+ 路径选择完毕后，可以按Ctrl键+Enter键即可将路径转化为选区；也可以是在图层那里选中路径-》下方的虚线圆圈按钮![1637991456404](F:\MyNote\images\1637991456404.png)；还可以右击点击建立选区
+ 路径的存储：勾完路径后直接对图⽚进⾏存储即可将路径保存到这张图⽚，后续打开可以继续使⽤
+ 如果确定选区时，出现选择了图层外的部分，可以在工具菜单栏中点击![1638024259189](F:\MyNote\images\1638024259189.png)路径操作-》合并形状

### 1.11.画笔工具

+ 按**B键**即可切换画笔工具，用于在图层上进行涂抹、绘画
+ 画笔颜色有前景色决定；画笔大小调整⽅法：“按住Alt键并鼠标右键向左移动”变小；“按住Alt键并鼠标右键向右移动”变大。画笔硬度调整方法：“按住Alt键并鼠标右键向上移动”变小；“按住Alt键并鼠标右键向下移动”变大，或者按住Shift键+【键画笔硬度变小，按住Shift键+【键画笔硬度变大；鼠标右击在面板上也可以改变画笔大小、画笔硬度
+ 点击画笔面板![1638077174920](F:\MyNote\images\1638077174920.png)，经常使用的是画笔设置，常用的设置有画笔比较形状中大小、硬度，形状动态，散布，传递。

![1638077580802](F:\MyNote\images\1638077580802.png)



#### 1.11.1.定义画笔

+ 首先新建画布(50*50像素，不能太大)，然后在画布中填充颜色。其中⿊⾊：不透明，灰⾊：半透明，⽩⾊：透明（不要⽤这个颜⾊定义画笔），彩⾊：半透明。最后在编辑—定义画笔预设中，将当前画布设置为新画笔并定义画笔名称。

#### 1.11.2.路径描边

+ 第一种方法是先用钢笔画路径，随后新建图层，切换画笔工具设置画笔与前景色，按Enter键即可完成路径描边
+ 第二种方法是先用钢笔画路径，随后新建图层，在路径锚点处鼠标右键选择路径描边也可完成路径描边。此方法除钢笔工具还可以用于形状工具（需要将工具菜单栏的形状改为路径）

#### 1.11.3.定义图案

+ 首先新建画布(20*20像素，不能太大)，然后在画布中画出图案，然后在编辑—定义图案中，将当前画布设置为新图案。

#### 1.14.颜色替换

+ 选择颜色替换工具后，有三种取色模式，一是连续取样，不常用；二是一次取样，常用，三是取样背景色板，常用
+ 一次取样是选择一次取样，然后设置前景色并确定画笔大小，之后用鼠标左键点击一次完成取样并按住，之后不断在需要替换颜色的地方划动即可替换取样的颜色；每次松开鼠标后，需要再次重复取样并划动来替换颜色
+ 取样背景色板是选择取样背景色板，然后设置背景色与前景色并确定画笔大小，之后用鼠标左键点击并按住，之后不断在需要替换颜色的地方划动即可替换背景的颜色；每次松开鼠标后，需要再次重复取样并划动来替换颜色

### 1.12.文字工具

+ 按**T键**即可切换文字工具，点击画布，即可进入编辑状态写字，写完按Ctrl键+Enter键就可以退出编辑状态。
+ 二次编辑文字时，需要选择图层，切换到文字工具，才可以更改文字字体、大小等内容
+ 字体对齐是相对于多行文字的
+ 字符面板：控制字体大小快捷键是按住Ctrl键+Shift键，并通过<键和>键调整行间距大小（需要先选中文字），控制行间距![1638890843770](F:\MyNote\images\1638890843770.png)快捷键是按住Alt键，并通过鼠标左键上下拖拽调整行间距大小（需要先选中文字）。控制字间距![1638890898169](F:\MyNote\images\1638890898169.png)快捷键是按住Alt键，并通过鼠标左键左右拖拽调整字间距大小（需要先选中文字）。字体高度控制![1638891061631](F:\MyNote\images\1638891061631.png)，字体宽度![1638891093165](F:\MyNote\images\1638891093165.png)，基线的偏移![1638891263660](F:\MyNote\images\1638891263660.png)

+ 段落面板：对齐方式是需要用于区域文字，即横排文字或竖排文字。对齐方式有左对齐，居中对齐，右对齐，最后一行左对齐，最后一行居中对齐，最后一行右对齐，全部对齐（两端对齐）。还有缩进，有左缩进、右缩进、首行缩进、段前空格、段后空格，都是可以选择缩进多少个像素。最后是避头尾法则设置可以选择宽松或严格，使得标点符号不会出现在每一行的开头，会自动向前或向后缩进，这项设置主要用于文字较多的时候。

### 1.13.形状工具

+ 位图与矢量图的案例：选区工具绘制的图是位图，放大后边缘模糊；形状工具绘制的图是矢量图，边缘清晰不失真。区别方法是矢量图层的右下角有路径的小图标，位图图层什么也没有。
+ 形状工具有矩形、圆角矩形、椭圆、多边形、直线、自定义形状这几种工具
+ 绘制形状工具以外的矢量图可以通过钢笔工具的形状模式来绘制
+ 首先矩形形状工具，选择矩形，绘制图形，按住Shift键可以绘制正方形，同时按住Alt键的话，可以以鼠标为中心绘制正方形。
+ 绘制完毕后可以在工具菜单栏或属性面板调整它的参数，如宽高，起始点位置、内部填充、描边、旋转角度、圆角半径（点击锁链后修改一个的同时也会修改其他几个角）,详情看形状填色部分
+ 在属性面板的蒙版中还可以修改其边缘羽化程度、浓度
+ 绘制的时候可以用路径选择工具拖拽路径上的锚点，但是拖拽后属性面板中圆角属性就不可用了
+ 绘制的时候，可以按住空格键，这样就可以将形状移动了
+ 多边形绘制可以在工具菜单栏或属性面板修改几条边，五边形时可以通过控制缩进边依据50%将其变为五角星
+ 直线时可以控制其粗细，在工具菜单栏或属性面板勾选起点或终点来为其在对应位置添加箭头
+ 自定义形状可以在工具菜单栏中选择预设的写一些形状

#### 1.13.1.形状填色

+ **填充属性：**形状填充属性就是形状的内部颜⾊
+ 修改方式有两种：1.直接双击形状图层就可以打开拾⾊器，直接修改颜⾊即可；2.在属性⾯板中修改
+ 内部填充分为⽆、纯⾊、渐变、图案。![1639223102941](F:\MyNote\images\1639223102941.png)

#### 1.13.2.形状描边

​		描边相关设置说明：![1639275920777](F:\MyNote\images\1639275920777.png) ![1639277010923](F:\MyNote\images\1639277010923.png)，第一个是形状填充属性，第二个是描边,同样可以填充⽆、纯⾊、渐变、图案，第三个是调整描边的粗细，

+ 第四个是描边线条的连续，实线、虚线。![1639277635677](F:\MyNote\images\1639277635677.png)

 第五个是设置描边对齐类型,

+ 路径在描边外部![1639277757067](F:\MyNote\images\1639277757067.png)
+ 路径在描边中间![1639277777780](F:\MyNote\images\1639277777780.png)
+ 路径在描边内部![1639277800163](F:\MyNote\images\1639277800163.png)

第六个是设置描边的线段端点，端点在方角路径上、端点在圆角路径内、端点在方角路径内；第七个是设置描边的线段合并类型，

+ 描边四角是方角![1639277891500](F:\MyNote\images\1639277891500.png)
+ 圆角![1639278169297](F:\MyNote\images\1639278169297.png)
+ 斜角![1639278187740](F:\MyNote\images\1639278187740.png)

#### 1.13.3.连续复制

​		首先绘制一个形状，然后填色，之后Ctrl键+J键原位复制一个，Ctrl键+T键进入自由变换形态，将复制的形状移动到一侧，最后按Ctrl键+Shift键+Alt键+T键即可重复上面动作，连续在一侧复制这个形状

​		上面连续复制是每次复制到一个新图层。如果在复制完第一个后，按A键选择路径选择工具，再按Ctrl键+Shift键+Alt键+T键会将之后所有复制的形状都放在第一个复制形状所在图层

#### 1.13.4.布尔运算

+ 绘制完第一个形状后，绘制第二个时，按Alt键，两者相交，会减去相交部分；按Shift键会将两者所有部分合并在一起；按Alt键+Shift键会只保留两者相交部分。按键在绘制第二个形状时按一次就可以激活，不需持续按，注意观察此时鼠标右下角图标。
+ 绘制完毕两者的路径还是分开的，可以通过工具菜单栏的路径操作的下拉按钮（倒数第四个，不包含勾选框）中合并形状组件将路径合并。
+ 排除重叠形状：绘制好两个以上相交的形状后，选择最后一个（最顶层）绘制的形状或者选择所有形状路径，选择工具菜单栏的路径操作的下拉按钮（倒数第四个，不包含勾选框）中排除重叠形状将重叠部分删除 。
+ 布尔运算除在单图层进行，还可以在多图层进行。绘制两个形状，然后移动其中一个至两个形状相交，选择两个图层，按Ctrl键+E键合并图层（合并图层会导致图层颜色变为顶层图层颜色），此时可以通过工具菜单栏的路径操作的下拉按钮（倒数第四个，不包含勾选框）中的功能进行布尔运算。选中顶层形状，可以进行各种布尔运算

#### 1.13.5.剪切蒙版

​		剪切蒙版作用与两个或更多个图层间的功能，在上层放图片，下层放一个圆的形状，两者叠加，按住Alt键点击两个图层中间的分割线，就可以为两个图层建立剪切蒙版，可以使得下层形状限制上次图片的显示，只能在圆形内部显示。当图层多于两个时，选中需要建立剪切蒙版的所有图层，按Ctrl键+Alt键+G键即可将选中的图层放入这些图层下面的那个图层中，也可以通过这个快捷键解除剪切蒙版。**注意**：当需要建立剪切蒙版的图层间夹杂着其它的图层，两者是不可以建立剪切蒙版的。

### 1.14.图像调色

​		色彩是什么？ ⾊彩是可⻅光导致的视觉现象，光是⼀种电磁波，不同的波⻓可⻅光投射到 物体上⼀部分被吸收，⼀部分被反射到⼈眼，⼤脑把这种刺激反映成⾊彩信 息，所以说没有光就没有⾊彩可⾔。在⼤⾃然界中有256256256=16777216种颜⾊。

#### 1.14.1.色彩三要素

+ ps中颜色模式分为位图、灰度、RGB颜色（最常用）、CMYK颜色（常用）、Lab颜色

+ RGB颜色：红、绿、蓝，是⽬前运⽤最⼴的颜⾊模式之⼀。由红绿蓝三种原⾊组成，出现在电⼦屏幕上的 

  图像均采⽤RGB颜⾊模式，例如⼿机上的图⽚、电脑上的图⽚

+ CMYK颜色：青、洋红、黄、黑（简称红黄蓝），是油墨的混合模式（通常用于印刷或打印），各个颜色参数在1-100之间调整
+ 可以在图像-》模式-》RGB颜色中调整颜色模式
+ 色彩三要素是指的H、S、B。H（色相）是赤、橙、黄、绿、青、蓝、紫；S（纯度）是饱和度，是颜色的浓度或颜色鲜艳程度（深浅，如深红、浅红）；B（明度）是明暗程度
+ 颜色分为三类，原色、间色、复色。原色是指红黄蓝，两种原色混合可以得到间色，而原色与间色混合或两种间色混合到一起可以得到复色

#### 1.14.2.颜色通道

​		通道在右下角

![1639747780678](F:\MyNote\images\1639747780678.png)

+ ⼀个图⽚中包含：复（综）合通道、红⾊通道、绿⾊通道、蓝⾊通道

+ 通道的作⽤: 通道⽤来存储颜⾊信息、可以调整颜⾊、或者载⼊选区

+ 当点击红、绿、蓝的通道时，画面会变为纯白色、纯黑色或灰色。其中

  纯⽩⾊：表示存储的颜⾊的⾊值⾼为255，例如：点击红色通道，当前图层所有⽩⾊部分的颜色接近红色或者该部分颜色就是白色

  纯⿊⾊：表示存储当前通道的颜⾊的⾊值为0 ，例如：点击红色通道，当前图层所有黑⾊部分颜色中三原色红色部分几乎没有或者该部分颜色就是黑色

  灰⾊：表示存储当前通道的颜⾊的⾊值为0-255 ，例如：点击红色通道，当前图层灰色部分的颜色中三原色红色部分数值位于0-255

+ **亮度/对比度**：调整图像中的亮度与对⽐度，使图像中亮的更亮，暗的部分更暗，也可以单独调整亮度，不调整对⽐度;而对比度是将明亮对比变得更强烈，亮的更亮，暗的更暗

  位置是菜单栏中图像-》调整-》亮度/对比度，或者是在图层下方第四个小图标![1639749712177](F:\MyNote\images\1639749712177.png) 这里也有亮度/对比度的功能

  ![1639749753889](F:\MyNote\images\1639749753889.png)

+ **直方图**是⽤来查看图像彩⾊信息是否正常，位置是菜单栏窗口-》直方图，直方图顶部右侧的小菜单栏可以选择展示所有直方图，所有颜色、红、绿、蓝。调色时，某个直方图山峰从左到右分布比较平均，说明调色比较均衡，比较好。例如：红色直方图竖轴代表红色数值，横轴代表白色数值，调色好的直方图应是左侧、右侧有山峰，中间有M型山峰，从左到右都有一定的山峰（不一定要平均分布），这样比较好。调色就是白色少调亮度，红绿蓝少调RGB数值

  ![1639750091229](F:\MyNote\images\1639750091229.png)

#### 1.14.3.图像调整

以下通过快捷键或菜单栏调整的色彩都会直接反映在图像上，而可以通过图层下边第四个小图标调整图层操作的调色会以图层的形式出现，会影响在这个图层下的所有图层，可以以蒙版的形式将其作用在某一个图层。

+ **色阶**：快捷键Ctrl键+L键，或者是菜单栏图像-》调整-》色阶，还可以通过图层下边第四个小图标调整图层中选择色阶。调整输入色阶与输出色阶，首先选择通道，然后调整输入色阶的图像，通过调整图像下方三个小三角滑块对图像进行微调，调整得左右的白色、黑色部分分布更均匀。输入色阶左侧滑块向右调是黑暗部分变强,将直方图山峰左侧向左拉；右侧滑块向左调是光亮部分变强，将直方图山峰右侧向右拉。输出色阶色条下左侧滑块向右是整体变亮，将直方图山峰左侧向右拉；右侧滑块向左是整体变暗，，将直方图山峰右侧向左拉

![1640009222630](F:\MyNote\images\1640009222630.png)

​		**注意事项**：如果需要使⽤⾊阶来矫正图像颜⾊，那么这张图像⼀定要是原⽚。否则该⽅法将不能调整，并 不		是所有照⽚都需要对其所有通道进⾏调整

+ **色彩平衡**：快捷键是Ctrl键+B键或菜单栏图像-》调整-》色彩平衡，还可以通过图层下边第四个小图标调整图层中选择色彩平衡。色彩平衡打开面板后可以通过调整三种色条来调整图像整体颜色，下面的阴影是用来调整有阴影的地方的颜色，高光同样如此。

  ![1640094631189](F:\MyNote\images\1640094631189.png)

+ **色相/饱和度**：快捷键是Ctrl键+U键或菜单栏图像-》调整-》色相/饱和度，还可以通过图层下边第四个小图标调整图层中选择色相/饱和度。勾选右下角**着色**可以直接对整体调整色相、饱和度、明度 ，添加滤镜；可以在不勾选**着色**的情况下，对左上角的下拉框中的全图选择单个颜色，调整这个颜色的色相、饱和度、明度。

  ![1640095289753](F:\MyNote\images\1640095289753.png)

+ **去色**：快捷键是Ctrl键+Shift键+U键或菜单栏图像-》调整-》去色，作用是将所有颜色都去除，只留黑色、白色、灰色。

+ **黑白**：快捷键是Ctrl键+Shift键+Alt键+B键或菜单栏图像-》调整-》黑白，还可以通过图层下边第四个小图标调整图层中选择黑白。作用是将所有颜色都去除，只留黑色、白色、灰色，然后可以对图像中某一种颜色的黑白灰颜色进行精细地调整。

  ![1640131767048](F:\MyNote\images\16401315903211.png)

+ **曲线**：快捷键是Ctrl键+M键或菜单栏图像-》调整-》曲线，还可以通过图层下边第四个小图标调整图层中选择曲线。作用是通过曲线的形式调整色彩。在曲线上直接点击可以在曲线中间增加点，可通过拖拽到X轴或右侧Y轴的方法删除点。曲线向左上角拖拽是图像变亮，向右下角拖拽是图像变暗。常用的曲线是S型的。

  ![1640179141423](F:\MyNote\images\1640179141423.png)

+ **可选颜色**：菜单栏图像-》调整-》可选颜色，还可以通过图层下边第四个小图标调整图层中选择可选颜色。作用与色相/饱和度类似，可以更精细的对某一种颜色进行调整。

  ![1640179706171](F:\MyNote\images\1640179706171.png)

### 1.15.图层混合模式

#### 1.15.1.模糊工具

+ 模糊工具![1640265950025](F:\MyNote\images\1640265950025.png)需要在左侧工具栏中选择，作用是对图像局部进行模糊化处理，根据模糊程度的需要调整画笔硬度及强度。
+ 锐化工具![1640266171992](F:\MyNote\images\1640266171992.png)从属于模糊工具，作用是对图像局部进行清晰化处理，根据清晰程度的需要调整画笔硬度及强度。
+ 涂抹工具![1640266192524](F:\MyNote\images\1640266192524.png)从属于模糊工具，作用是对图像局部进行扭曲处理（扭曲的是前景色的部分），根据扭曲程度的需要调整画笔硬度及强度。

#### 1.15.2.加深减淡工具

+ 加深减淡工具快捷键是O键
+ 加深工具就是加深颜色，减淡工具就是减少颜色，两者调整范围与色彩平衡相似，也是中间调、阴影、高光，还可以调整曝光度。可根据加深减淡程度需要调整画笔硬度与曝光度
+ 海绵工具有两种模式，去色与加色，去色是去除颜色，减少颜色直至黑色；加色是添加颜色，添加颜色直至白色。可根据去色与加色程度需要调整画笔硬度与流量

#### 1.15.3.蒙版应用

+ 用于控制图层的显示与隐藏
+ 方法是选择需要添加蒙版的图层，点击图层下第三个小图标![1640351862752](F:\MyNote\images\1640351862752.png)，即可在图层上添加蒙版，需要删除的时候将图层中蒙版部分拖拽到图层右下角的删除图标处即可，也可以在蒙版部分右击删除或停用蒙版(按住Shift键点击蒙版)。这里的应用蒙版是将蒙版与图层结合，蒙版修改部分将无法删除
+ 直接添加蒙版时，默认是添加白色蒙版，图像全部显示，切换画笔，在图层上涂抹是不起作用的，需要切换前景色为黑色；也可以按住Alt键然后添加蒙版，此时添加的是黑色蒙版，图像全部隐藏，切换画笔即可在图层涂抹，随着涂抹图像会从涂抹之处逐渐显示出来。这里黑色代表隐藏，白色代表显示，这里是与橡皮擦不一样的地方
+ **载入蒙版**--按住Alt键，点击蒙版可以查看蒙版的内容，也可以做一些其他操作。比如在蒙版内添加其他图片，然后点击普通图层，就可以在普通图层看到蒙版里的图片（半透明状态）
+ **注意事项**：添加蒙版后，如果擦除图像时，擦除不彻底，查看前景色是否是纯黑色

#### 1.15.4.混合模式

+ **正片叠底**： 去⽩留⿊  过滤画⾯中的亮部区域，保留暗部区域
+ **滤色**： 去⿊留⽩  过滤画⾯中的暗部区域，保留亮部区域
+ 关闭所有窗口快捷键Ctrl键+W键
+ **叠加柔光**： 对于灯光类型作品，复制越多，亮度也会越亮；对于图像，复制越多，画⾯对⽐度会越强烈
+ **颜色**：可以将前景⾊在配合画笔⼯具，对图像上的颜⾊进⾏替换。先用画笔涂抹颜色，之后选择颜色即可将画笔涂抹的颜色印在图像原来的颜色上，对其进行一个覆盖

#### 1.15.5.图标分解

+ ![1640360752746](F:\MyNote\images\1640360752746.png)

+ **A组：基础混合模式**

  需要⽤图层的不透明度或填充来控制下⾯图层的效果进⾏混合，如果不改变透明度或填充更改“正常模式”或“溶解”  时将没有效果出现 

  **常⽤：正常模式** 

  **B组：降暗图像型混合模式（去亮留暗）** 

  滤除当前图层亮调部分的像素，从⽽达到图像变暗的⽬的 

  常⽤：正⽚叠底(过滤⽩⾊）、变暗 

  技巧：在⽹上找寻⼀些⿊⾊图案⽩⾊背景直接拿到设计稿中⽤变暗或正⽚叠底来去除⿊⾊。 

  **C组：提亮图像混合模式（去暗留亮）** 

  ⽤来滤除图像中较暗的部分像素。从⽽达到使图像提亮的效果。⼀般会利⽤这组来去除暗的部分留下亮的部分。 

  常⽤：滤⾊、颜⾊减淡（添加）

  **D组：融合图像型混合模式** 

  保留了⾊相的基础上，亮的区域更亮，暗的区域更暗（加强对⽐度） 

  常⽤：叠加、柔光 

  **E组：变异图像混合模式** 

  制作出各种变异的颜⾊效果 

  常⽤：本组⼏乎不⽤ 

  **F组：⾊彩叠加弄混合模式** 

  依据图像中的⾊相、饱和度等基本属性，将⾊彩的三要素应⽤到图像中 

  常⽤：明度

### 1.16.图层样式

​		图层样式是PS中⼀个⽤于制作各种效果的强⼤功能，利⽤图层样式的功能可以简单快捷制作 

出各种⽴体投影，各种质感及光影效果的图像特效。

​		图层样式具有速度快、效果明确，可编辑性强等⽆法⽐拟的效果。

+ 添加方法：1.点击图层下方第二个小图标![1640439892719](F:\MyNote\images\1640439892719.png)；2.双击需要添加图层样式的图层空白部分，不能是涂层的名字部分
+ 添加图层样式的图层右侧会有fx的字样，且图层下方会有图层名称为效果的图层
+ 需要修改图层样式时，可以双击图层右侧空白部分或双击下边效果图层
+ 删除图层样式需要先进入图层样式的面板，在左侧菜单栏选择需要删除的图层样式，然后在左侧菜单栏右下角点击删除按钮即可
+ 文字图层、形状图层、普通图层、组都可以添加图层样式
+ 2016版之后添加新功能，有的图层样式可以添加多次，如描边，点击描边菜单栏的右侧加号即可添加第二个描边

#### 1.16.1.混合选项

+ **混合颜色带**：将本图层的右侧滑块向左拖动会将本图层的亮度值的上限降低，高于此值的都隐藏，将左侧滑块向右拖动是将本图层的亮度值的下限提高，低于此值的都隐藏。

  这里本图层指正在处理的图层，下一图层是指本图层下面挨着的那个图层。

  下一图层的滑块滑动含义相反，不是隐藏而是显示。将下一图层的右侧滑块向左拖动会将本图层的亮度值的上限降低，高于此值的都显示，将左侧滑块向右拖动是将下一图层的亮度值的下限提高，低于此值的都显示。

  按住Alt键可以将一个滑块变成两个半个的滑块，滑块中间部分为半透明区域，即图像亮度在此区域的部分会处于半透明状态，其中 色调值越低，图像越透明 

+ 如果剪切蒙版失效，可以在混合选项中间部分勾选"将内部效果混合成组"，不勾选"将剪切图层混合成组"，这样就可以了。

#### 1.16.2.斜面浮雕

![1640509083236](F:\MyNote\images\1640509083236.png)

+ 样式分为外斜面、内斜面、浮雕效果、枕状浮雕、描边浮雕。

  演示文字：![1640509276622](F:\MyNote\images\1640509276622.png)

  外斜面是针对于背景进⾏浮雕凸起处理

  ![1640509197514](F:\MyNote\images\1640509197514.png)

  内斜面是针对于当前图层内部浮雕凸起处理（常用）

  ![1640509238776](F:\MyNote\images\1640509238776.png)

  浮雕效果是结合背景及当前图层共同浮雕凸起

  ![1640509309532](F:\MyNote\images\1640509309532.png)

  枕状浮雕是以当前图层为轮廓在背景中执⾏下陷内凹效果

  ![1640509397600](F:\MyNote\images\1640509397600.png)

  描边浮雕是图层中有描边样式时⽅可起作⽤

  ![1640509621226](F:\MyNote\images\1640509621226.png)

  ​										描边浮雕应用前

  ![1640509699283](F:\MyNote\images\1640509699283.png)

   									  描边浮雕应用后（深度调整到300%）

  浮雕方法有平滑（用的比较多）、雕刻清晰、雕刻柔和，深度是浮雕立体感的深度；方向是灯光从上打下来，还是从下向上打；大小是浮雕面积大小；软化是指浮雕边缘与侧面之间的角度是尖锐的还是平滑过渡的

+ **阴影**：角度和高度一般不需要调， 角度控制光线方向，高度控制阴影范围 ；光泽等高线的图像就是一个直方图，表示光的明暗关系；高光就是图层上的高光或光比较亮的地方，首先是模式，与混合模式类似，有正常、溶解之类的，建议用滤色，然后是高光的颜色可以调节，建议用比较亮的颜色；不透明度是浮雕高光相对于图层的，不透明度越高浮雕越明显；阴影模式与下面的不透明度是指图层上的阴影或光比较暗的地方与高光的类似，颜色建议用比较暗的，模式建议用正片叠底

#### 1.16.3.描边

+ 描边有大小、位置、混合模式、不透明度、填充类型	这几种选项。大小是图层外边缘向外扩展的大小。位置有外部、居中、内部，一般选外部。混合模式与不透明度与图层的一样，填充类型有颜色、渐变、图案三种。颜色只能选颜色，渐变可选渐变颜色、样式、渐变角度、缩放程度等，样式有线性、角度、径向、对称的、菱形、迸发状。图案可以选图案及图案的缩放程度等

## 2.PS小技巧

### 2.1.提取线稿

​		打开图片，首先复制一张，然后选择菜单栏中**图像**-》**去色**，之后再次进行复制，按Ctrl键+I键反向选择，选择图层-》颜色减淡

![1639236421365](F:\MyNote\images\1639236421365.png)
颜色减淡

选择**滤镜**-》**其它**-》**最小值**，最后只需导出或另存为即可

**注意**：批量提取线稿可以录制动作，先打开一张图片，然后点击窗口-》动作，![1639276240501](F:\MyNote\images\1639276240501.png) 创建新动作，创建后开始录制，然后从复制开始到导出结束，之后点击创建动作图标最左边的图标结束录制，最后点击文件-》自动-》批处理，在左侧源文件夹处选择图片所在文件夹，在右侧目标文件夹处选择线稿文件夹，勾选覆盖动作中的"存储为"命令，确定即可开始批量提取线稿。

### 2.2.撕纸效果

1. 首先，小编把照片导入到PS中，并点击图层面板新建图层按钮，如下图所示。

   ![怎样简单快速的做出撕纸效果](F:\MyNote\images\acfda02f47704618c40d6788b08602214e57766e.jpg)

2. 然后，我们需要重命名背景图层为图层0，这样就可以把图层0移到图层1上面。

   ![怎样简单快速的做出撕纸效果](F:\MyNote\images\3ac71c214f579356726c7b93effb960b3021706e.jpg)

   ![怎样简单快速的做出撕纸效果](F:\MyNote\images\52fae62064fb960b14f686d28fa355e982ae6c6e.jpg)

3. 接着，我们需要在菜单栏的图像处调节画布大小，并使画布比图片相对大一些，如下图所示。

   ![怎样简单快速的做出撕纸效果](F:\MyNote\images\05e24be983aee8d772fd605c6b781431deb6666e.jpg)

   ![怎样简单快速的做出撕纸效果](F:\MyNote\images\def72c6c576699cf3184acd0a885e036e3915e6e.jpg)

   ![怎样简单快速的做出撕纸效果](F:\MyNote\images\2e223d85e036e2917f3fb053b2723d03baea5b6e.jpg)

4. 填充画布颜色为白色。选择套索工具，选择图层0，在TOM and JERRY处套索，如下图。

   ![怎样简单快速的做出撕纸效果](F:\MyNote\images\baab2086304861439703cb828febf6a75e0f536e.jpg)

   ![怎样简单快速的做出撕纸效果](F:\MyNote\images\f7e6410f822b74ee5be5c8abda2c8cf1d9a74a6e.jpg)

5. 点击工具栏的快速蒙版工具（见黄色荧光笔），然后点击滤镜--像素化--晶格化，调节晶格化数值。再点击快速蒙版工具来退出快速蒙版。如下图，撕纸效果的纹理就比较清楚了。

   ![怎样简单快速的做出撕纸效果](F:\MyNote\images\d9e638334884cde304fbd55df07f860e7d75426e.jpg)

   ![怎样简单快速的做出撕纸效果](F:\MyNote\images\874f6275e5f4fcf5b8dab97d21d7726b0de2bd6e.jpg)

   ![怎样简单快速的做出撕纸效果](F:\MyNote\images\1562a0b9763e21c2d9016263e6e89a618725b16e.jpg)

   ![怎样简单快速的做出撕纸效果](F:\MyNote\images\304f0999e92abab83097e94d4814f1c594eea16e.jpg)

6. 接下来，按住ctrl+t，将套索的一部分照片移动，做撕开状。为了使撕开效果更逼真，我们可以选择图片所在图层面板下方第二个图标（fx的字样）设置图层样式效果，设置为投影，并调节投影的各项数值。

   ![怎样简单快速的做出撕纸效果](F:\MyNote\images\c255efc595ee41c1cff02fe08d88912ca4ca9b6e.jpg)

   ![怎样简单快速的做出撕纸效果](F:\MyNote\images\906dbbcadce890487f2bf444130e5f204271926e.jpg)

   ![怎样简单快速的做出撕纸效果](F:\MyNote\images\3761a73acd8920c5afd80b86568a59de4407886e.jpg)

7. 最后，看一下效果吧，撕纸效果还是很逼真的。还是那句话，大家不妨体验一下，真的是比较简单快速的。

   ![怎样简单快速的做出撕纸效果](F:\MyNote\images\89402670d5413a8c34df26bc1ffc508c9ace816e.jpg)

### 2.3.美女脱丝袜

首先选中需要脱掉的丝袜并提取出来，建议使用魔棒工具。选好之后建立色相/饱和度图层-**色相/饱和度**在通道下方第四个图标（半个圆月图标）中，然后按住Alt键，在色相/饱和度图层与提取出来的丝袜图层中间分界线处点击建立剪切蒙版，之后在色相/饱和度中勾选着色，然后将色相设为0，调整饱和度与明度至丝袜大致呈现肉色。之后再次在丝袜图层上建立曲线图层，移动曲线增加丝袜亮感与光泽，使之更像皮肤。到此基本完成，也可以再建立一个曲线图层，二次调整丝袜的整体感觉。