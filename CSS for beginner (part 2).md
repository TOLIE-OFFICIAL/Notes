---
title: CSS for beginner (part 2)
date: 2022-01-10 22:00:58
summary: 
categories: 
  - Frond End

tags:
  - CSS
---

### 十三、CSS浮动

#### 传统网页布局的方式

网页布局的本质——用CSS来摆放盒子。把盒子摆放到相应位置
CSS提供了三种传统布局方式(简单说，就是盒子如何进行排列顺序) 

> *注意*：实际开发中，一个页面基本都包含了这三种布局方式。（后面移动端学习新的布局方式）

##### 普通流(标准流/文档流)

所谓的标准流：就是标签按照规定好默认方式排列。

1. 块级元素会独占一行,从上向下顺序排列。
   * 常用元素：div、 hr. p、h1~h6、 ul、 ol、 dl、 form、 table
2. 行内元素会按照顺序,从左到右顺序排列,碰到父元边缘则自动换行。
   * 常用元素：span、a、i、em等

##### 浮动

*提问*：我们用标准流能很方便的实现如下效果吗?

* 如何让多个块级盒子(div)水平排列成一 行?

![问题一](http://pic.tolie.biz/images/image-20220111125531686.png)

* 比较难，虽然转换为行内块元素可实现一行显示，但是`他们之间会有大的空白缝隙`，`且大小很难控制`。

> *总结*：有很多的布局效果，标准流没有办法完成，此时就可以利用浮动完成布局。因为`浮动可以改变元素标签默认的排列方式`。浮动最典型的应用就是可以让多个块级元素在一行内排列显示。

**网页布局第一准则**：<span style="color:red;">多个块级元素纵向排列找标准流，多个块级元素横向排列找浮动。</span>

###### 什么是浮动

**float**属性用于创建浮动框，将其移动到一边，直到左边缘或右边缘触及包含块或另一个浮动框的边缘。

**语法**

> 选择器 {
>
> ​	float:属性值;
>
> }

| 属性值  | 描述                                                     |
| :------ | :------------------------------------------------------- |
| left    | 元素向左浮动。                                           |
| right   | 元素向右浮动。                                           |
| none    | **默认值**。元素不浮动，并会显示在其在文本中出现的位置。 |
| inherit | 规定应该从父元素继承 float 属性的值。                    |

###### 浮动的特性*

1. **浮动元素会脱离标准流(脱标)**

   > 脱离标准普通流的控制（浮）移动到指定位置（动），（俗称`脱标`）；
   >
   > `浮动的盒子不再保留原先的位置`；

   ![浮动特性一](http://pic.tolie.biz/images/image-20220111131436272.png)

2. **浮动的元素会一行内显示并且元素顶部对齐**

![浮动特性二](http://pic.tolie.biz/images/image-20220111131800742.png)

> **注意**：浮动的元素是互相贴靠在一起的(不会有缝隙) , 如果父级宽度装不下这些浮动的盒子，多出的盒子会另起一行对齐。

3. **任何元素都可以浮动。不管原先是什么模式的元素，添加浮动之后具有行内块元素相似的特性。**

> 如果行内元素有了浮动，则不需要转换块级\行内块元素就可以直接给高度和宽度。
>
> * 如果块级盒子没有设置宽度，`默认宽度和父级一样宽`，但是添加浮动后，它的大小根据内容来决定；
> * 浮动的盒子中间是`没有缝隙的`，是紧换着-起的；
> * 行内元素同理；

<span style="color:red;font-size:17px">为了约束浮动元素位置我们网页布局一般采取的策略是</span>：

> 1. 先用标准流的父元素排列上下位置，
> 2. 它的内部子元素采取浮动排列左右位置。

**网页布局第二准则**：<span style="color:red;">:先设置盒子大小,之后设置盒子的位置.</span>

###### 常见的网页布局

![常见的网页布局-1、2、3](http://pic.tolie.biz/images/image-20220111203252211.png)

###### 浮动的注意点

1. **浮动和标准流的父盒子搭配。**

   先用标准流的父元素排列上下位置，之后内部子元素采取浮动排列左右位置

2. **一个元素浮动了，理论上其余的兄弟元素也要浮动。**

   一个盒子里面有多个子盒子，如果其中一个盒子浮动了，那么其他兄弟也应该浮动,以防止引起问题。浮动的盒子只会影响浮动盒子后面的标准流不会影响前面的标准流.

##### 清除浮动

###### 清除浮动的原因

`不是所有的父盒子都能设定具体高度`。![清除浮动的原因](http://pic.tolie.biz/images/image-20220111210230154.png)

所以我们理想中的状态是让子盒子撑开父亲，有多少孩子，我父盒子就有多高。但是子盒子浮动又不占有位置，最后父级盒子高度为0时，就会影响下面的标准流盒子。

![父盒子高度为0的影响](http://pic.tolie.biz/images/image-20220111210740022.png)

###### 清除浮动的本质

`清除浮动的本质是清除浮动元素造成的影响`；

如果父盒子本身有高度，则不需要清除浮动；

`清除浮动之后，父级就会根据浮动的子盒子自动检测高度`。父级有了高度，就不会影响下面的标准流了。

**语法**

> 选择器 {
>
> ​	clear:属性值;
>
> }

| 属性值  | 描述                                  |
| :------ | :------------------------------------ |
| left    | 在左侧不允许浮动元素。                |
| right   | 在右侧不允许浮动元素。                |
| both    | 在左右两侧均不允许浮动元素。          |
| none    | **默认值**。允许浮动元素出现在两侧。  |
| inherit | 规定应该从父元素继承 clear 属性的值。 |

我们实际工作中，几乎只用 <span style="color:red;">clear: both;</span>

清除浮动的策略是：<span style="color:red;">闭合浮动</span>。只让浮动在父盒子内部影响，不影响父盒子外面的其他盒子。

###### 清除浮动的方法

1. **额外标签法也称为隔墙法，是W3C推荐的做法。**

**额外标签法**又叫隔墙法，会在`浮动元素末尾添加一个空的标签`。 例如&lt;div style=" clear:both" &gt; &lt;/div&gt;， 或者其他标签		（如&lt;br/&gt;等）。

<span style="color:red;">注意：要求这个新的空标签必须是块级元素。</span>

> **优点**：通俗易懂,书写方便
>
> **缺点**：添加许多无意义的标签,结构化较差

2. **父级添加overflow属性**

可以给`父级元素`添加overflow属性，将其属性值设置为hidden、auto 或scroll。

> 优点：代码简洁
>
> 缺点：无法显示溢出的部分

3. **父级添加after伪元素**

**语法**

```css
.clearfix:after {
    /*伪元素必须写的属性*/
	content:"";
    /*转换为块级元素*/
	display: block;
    /* 使元素不可见 */
	height: 0;
    /* 通过额外标签法清除 */
	clear: both;
    /* 使元素不可见 */
	visibility: hidden;
}

.clearfix { /* IE6、7专有 */
	*zoom: 1;
}
```

本质是在浮动元素的后面加了一个新的元素**（伪元素本身是行内元素，需要转换成块级元素）**

使用时，复制上方代码，并将 clearfix 类名赋给浮动的子元素的父级元素

> **优点**：没有增加标签,结构更简单
>
> **缺点**： 照顾低版本浏览器

4. **父级添加双伪元素**

**语法**

```css
.clearfix :before, 
.clearfix:after {
	content: "";
	display:table;
}
.clearfix:after {
    clear:both;
}
.clearfix {
	*zoom: 1;
}
```

本质是在浮动元素的前后都加了一个新的元素（此元素本身是行内元素，需要认为转换成块级元素）

> **优点**：代码更简洁
>
> **缺点**：照顾低版本浏览器

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        /* 清除浮动之 after伪元素 */
        /* .clearfix:after {
            content: "";
            display: block;
            height: 0;
            clear: both;
            visibility: hidden;
        } */

        /* .clearfix {
            IE6、7专有 
            *zoom: 1;
        }*/
        .clearfix :before,
        .clearfix:after {
            content: "";
            display: table;
        }

        .clearfix:after {
            clear: both;
        }

        .clearfix {
            *zoom: 1;
        }

        .head {
            height: 40px;
            width: 1226px;
            background-color: #a09e9e;
            margin: 10px auto;
            text-align: center;
        }

        .banner {
            height: 200px;
            width: 1226px;
            background-color: pink;
            margin: 10px auto;
        }

        .body {
            /*  height: 400px; */
            width: 1226px;
            background-color: skyblue;
            margin: 5px auto;
            /* 清除浮动之父级元素添加overflow属性 
            overflow: hidden;*/
        }

        /* .body ul {
            清除浮动之父级元素添加overflow属性  
            overflow: hidden;
        }*/

        .body ul li {
            height: 195px;
            width: 296.5px;
            background-color: purple;
            list-style: none;
            float: left;
            margin-left: 10px;
            margin-bottom: 10px;
        }

        /* .clear {
             清除浮动之额外标签法 
            clear: both;
        }*/


        .footer {
            height: 300px;
            width: 1226px;
            background-color: gray;
            margin: 10px auto 0;
        }
    </style>
</head>

<body>
    <div class="head">head</div>
    <div class="banner">banner</div>
    <div class="body">
        <ul class="clearfix">
            <li>1</li>
            <li>2</li>
            <li>3</li>
            <li>4</li>
            <li>5</li>
            <li>6</li>
            <li>7</li>
            <li>8</li>
            <!-- 清除浮动之额外标签法 -->
            <!--  <div class="clear"></div> -->
        </ul>
    </div>
    <div class="footer">footer</div>
</body>

</html>
```

##### PS基本操作

因为网页美工大部分效果图都是利用PS ( Photoshop )来做的，所以以后我们大部分切图工作都是在PS里面完成。

* 文件→打开:可以打开我们要测量的图片；
* Ctrl+R：可以打开标尺,或者视图----&gt;标尺；
* 右击标尺 ，把里面的单位改为像素；
* Ctrl+加号(+)可以放大视图， Ctrl+减号(-)可以缩小视图；
* 按住空格键，鼠标可以变成小手，拖动PS视图；
* 用选区拖动可以测量大小；
* Ctrl+ D可以取消选区，或者在旁边空白处点击一下也可以取消选区。

![PS的基本切图操作](http://pic.tolie.biz/images/image-20220110185733754.png)

###### 常见的图片格式

1. **jpg图像格式**: JPEG ( JPG )对色彩的信息保留较好，高清，颜色较多，`产品类的图片经常用jpg格式的`；
2. **gif图像格式**: GIF格式最多只能储存256色，所以通常用来显示简单图形级字体，但是可以保存透明背景和动画效果，`实际经常用于一些图片小动画效果`；
3. **png图像格式**：是一种新兴的网络图形格式，结合了GIF和PEG的优点，具有存储形式丰富的特点，能够保持透明背景。`如果想要切成背景透明的图片，请选择png格式`；
4. **PSD图像格式**：PSD格式是Photoshop的专用格式，里面可以存放图层、通道、遮罩等多种设计稿。`对我们前端人员来说最大的优点我们可以直接从上面复制文字，获得图片，还可以测量大小和距离`。
4. **webp图像格式**：谷歌在2010年推出的图片格式，压缩率只有jpg的2/3，大小比png小了45%。缺点是压缩的时间更久了，兼容性不好，目前谷歌和opera支持。

###### PS切图

1. **图层切图**

图层切图：右击图层→快速导出为PNG。

但是很多情况下，我们需要合并图层再导出: 

1. 选中需要的图层:图层菜单→合并图层(ctrl+e)
2. 右击→快速导出为PNG



2. **切片切图**

1. 利用切片选中图片

   利用切片工具手动划出；

2. 导出选中的图片

   文件菜单 → 导出 > 存储为web设备所用格式→ 选择我们要的图片格式 → 存储。



3. **PS插件切图**

Cutterman是一款运行在Photoshop中的插件，能够自动将你需要的图层进行输出，以替代传统的手工"导出web所用格式"以及使用切片工具进行挨个切图的繁琐流程。[Cutterman下载](http://www.cutterman.cn/zh/cutterman)

**注意**：Cutterman插件要求你的PS必须是完整版，不能是绿色版，所以大家需要安装完整版本。

### 十四、项目大作业

##### CSS属性书写顺序*

> 1. 布局定位属性：display / position/ float / clear / visibility / overflow （建议display第一个写,毕竟关系到模式）；
>
> 2. 自身属性： width/ height / margin/ padding / border / background；
>
> 3. 文本属性：color/ font / text-decoration/ text-align/ vertical- align/ white- space/ break-word；
>
> 4. 其他属性（CSS3）：content / cursor / border. -radius/ box shadow / 
>
>    text- shadow/background:liear-gradient...

```css
/* CSS书写顺序示例 */
.jdc {
    /* 1 */
    display: block;
    position: relative;
    float: left;
    /* 2 */
    width: 100px;
    height: 100px;
    margin: 0 10px;
    padding: 20px 0;
    /* 3 */
    font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif;
    color: #333;
    /* 4 */
    background: rgba(0,0,0, .5) ;
    border-radius: 10px;
}
```

##### 页面布局整体思路

为了提高网页制作的效率,布局时通常有以下的整体思路:

1. 必须确定页面的版心(可视区) ，我们测量可得知。
2. 分析页面中的行模块,以及每个行模块中的列模块。（页面布局第一准则）
3. 一行中的列模块经常浮动布局，先确定每个列的大小，之后确定列的位置（页面布局第二准则）
4. 制作HTML结构。我们还是遵循,先有结构，后有样式的则。结构永远最重要
5. 所以， 先理清楚布局结构，再写代码尤为重要这需要我们多写多积累。







### 十五、定位

![定位的学习目标](http://pic.tolie.biz/images/image-20220114134629817.png)

#### 为什么需要定位

1. 浮动可以让多个块级盒子一行没有缝隙排列显示，经常用于横向排列盒子。

2. 定位则是可以让盒子自由的在某个盒子内移动位置或者固定屏幕中某个位置，并且可以压住其他盒子。

#### 定位

**定位**：将盒子定在某一个位置，所以定位也是在摆放盒子，按照定位的方式移动盒子。

> 定位 = 定位模式 + 边偏移

**定位模式**用于指定一个元素在文档中的定位方式。 **边偏移**则决定了该元素的最终位置。



##### 定位模式

定位模式决定元素的定位方式，它通过CSS的`position`属性来设置,其值可以分为四个：

| 可能的值 | 描述                                                         | 语义     |
| :------- | :----------------------------------------------------------- | -------- |
| absolute | 生成绝对定位的元素，`相对于 static 定位以外的第一个父元素进行定位`。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。 | 绝对定位 |
| fixed    | 生成绝对定位的元素，`相对于浏览器窗口进行定位`。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。 | 固定定位 |
| relative | 生成相对定位的元素，`相对于其正常位置进行定位`。因此，"left:20px" 会向元素的 LEFT 位置添加 20 像素。 | 相对定位 |
| static   | 默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声明）。 | 静态定位 |
| inherit  | 规定应该从父元素继承 position 属性的值。                     | /        |



##### 边偏移

**边偏移**就是定位的盒子移动到最终位置。有top、bottom、 left 和right 4个属性。

| 边偏移属性 | 描述                                               |
| ---------- | -------------------------------------------------- |
| top        | `顶端`偏移量，定义元素相对于其父元素上边线的距离。 |
| bottom     | `底部`偏移量，定义元素相对于其父元素下边线的距离。 |
| left       | `左侧`偏移量，定义元素相对于其父元素左边线的距离。 |
| right      | `右侧`偏移量，定义元素相对于其父元素右边线的距离   |



##### 静态定位static (了解)

静态定位是元素的默认定位方式，无定位的意思。

**语法**

```css
选择器 {
	position: static;
}
```

**静态定位的特点**: 

* 静态定位按照标准流特性摆放位置，它没有边偏移；
* 静态定位在布局时很少用到。



##### 相对定位relative (重要)

`相对定位`是元素在移动位置的时候，是`相对于它原来的位置`来说的（*自恋型*）。

```css
选择器 {
	position: relative;
}
```

( 务必记住)

1. 它是**相对于自己原来的位置来移动**的（移动位置的时候参照点是自己原来的位置）。
2. **原来在标准流的位置继续占有**，后面的盒子仍然以标准流的方式对待它。( `不脱标`，继续保留原来位置）



##### 绝对定位absolute (重要)

`绝对定位`是元素在移动位置的时候，是相对于它祖先元素来说的（*拼爹型*）。

```css
选择器 {
	position: absolute;
}
```

**绝对定位的特点**: ( 务必记住)

1. 如果`没有祖先元素`或者`祖先元素没有定位`，则以`浏览器为准定位`。（Document文档）
2. 如果祖先元素有定位（相对、绝对、固定定位） ，则以`最近一级`的`有定位祖先元素`为参考点移动位置。
3. `绝对定位不再占有原先的位置`。（`脱标`）



######  子绝父相的原因

1. 子级绝对定位，不会占有位置，可以放到父盒子里面的任何一个地方，不会影响其他的兄弟盒子。
2. 父盒子需要加定位限制子盒子在父盒子内显示。
3. 父盒子布局时，需要占有位置，因此父亲只能是相对定位。

**总结**：因为父级需要占有位置，因此是相对定位，子盒子不需要占有位置，则是绝对定位。



##### 固定定位fixed (重要)

**固定定位**是元素固定于浏览器可视区的位置。

主要使用场景：`可以在浏览器页面滚动时元素的位置不会改变`。

```css
选择器 {
	position: absolute;
}
```

**固定定位的特点**: (务必记任)

1. 以浏览器的`可视窗口为参照点`移动元素。
   * 跟父元素没有任何关系；
   * 不随滚动条滚动。；

2. 固定定位`不再占有原先的位置`。
   * 固定定位也是`脱标`的，其实固定定位也可以看做是一种特殊的绝对定位。

**固定定位fixed** ( 重要)

<span style="color:red;">固定定位小技巧：固定在版心右侧位置。</span>

小算法:

1. 让固定定位的盒子left: 50%.走到浏览器可视区(也可以看做版心)的一半位置。
2. 让固定定位的盒子margin-left : 版心宽度的一半距离。多走版心宽度的一半位置。

```css
fixed {
    position: fixed; 
    /* 1.走浏览器宽度的一半*/
    left: 50%;
    /* 2.利用margin走版心盒子宽度的一半*/
    margin-left: 400px;
    width: 50px;
    height: 150px;
    background-color: skyblue;
}
```



##### 粘性定位sticky(了解)

**粘性定位**可以被认为是`相对定位和固定定位的混合`。Sticky 粘性的

**语法**:

```css
选择器{
    position: sticky; 
    top:10px;
}
```

粘性定位的特点:

1. 以浏览器的可视窗口为参照点移动元素（固定定位特点）
2. 粘性定位`占有原先的位置`（相对定位特点）
3. `必须添加`top、left、 right、 bottom 其`中一个才有效`。
4. 跟`页面滚动搭配`使用。兼容性较差, IE不支持。

![定位总结](http://pic.tolie.biz/images/image-20220114154935922.png)



#### 定位叠放次序z-index

在使用定位布局时，可能会出现盒子重叠的情况。此时，可以`使用z-index来控制盒子的前后次序`（z轴）

```css
选择器 {
	z-index: 1;
    /* 没有单位*/
}
```

* 数值可以是正整数、负整数或0，默认是auto，数值越大，盒子越靠上；
* `如果属性值相同`，则按照书写顺序，`后来居上`；
* 数字后面`不能加单位`；
* `只有定位的盒子才有z-index属性`;



#### 定位的拓展

##### 绝对定位的盒子居中

加了绝对定位的盒子不能通过margin:0 auto水平居中，但是可以通过以下计算方法实现水平和垂直居中。

1. **水平居中**

* left: 50%; :让盒子的左侧移动到父级元素的水平中心位置。
* margin-left: -100px; :让子左移动自身宽度的一半。

2. **垂直居中**

* top: 50%; :让盒子的左侧移动到父级元素的垂直中心位置。
* margin-top: -100px; :让子左移动自身高度的一半。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box {
            position: fixed;
            width: 100px;
            height: 200px;
            /* 水平居中 */
            left: 50%;
            margin-left: -50px;
            /* 垂直居中 */
            top: 50%;
            margin-top: -100px;

            background-color: pink;
        }
    </style>
</head>

<body>
    <div class="box"></div>
</body>

</html>
```

##### 定位特殊特性

1. 行内元素添加绝对或者固定定位，`可以直接设置高度和宽度`。

2. 块级元素添加绝对或者固定定位，如果不给宽度或者高度，默认大小是内容的大小。

3. 浮动元素、绝对定位（固定定位）元索的都`不会触发外边距合并`的问题。

4. 浮动元素不同，只会压住它下面标准流的盒子，但是不会压住下面标准流盒子里面的文字（图片）；但是绝对定位/固定定位会压住下面标准流所有的内容。

   > 浮动之所以不会压住文字，因为浮动产生的目的最初是为了做文字环绕效果的。文字会围绕浮动元素

###  十六、网页布局总结

一个完整的网页，是标准流、浮动、定位一起完成布局的,每个都有自己的专门用法。

1. **标准流**

* 可以让盒子上下排列或者左右排列，`垂直的块级盒子显示就用标准流布局`。

2. **浮动**

* 可以让多个块级元素一行显示或者左右对齐盒子，`多个块级盒子水平显示就用浮动布局`。

3. **定位**

* 定位最大的特点是有层叠的概念，就是可以让多个盒子前后叠压来显示。`如果元素自由在某个盒子内移动就用定位布局`。

### 十七、元素的显示和隐藏

#### display显示隐藏元素

> display：none ;	隐藏对象
>
> display：block ;	 除了转换为块级元素之外，同时还有显示元索的意思

<span style="color:red;">display隐藏元素后，不再占有原来的位置。</span>

#### visibility显示隐藏元素

**visibility属性用于指定一个元素应可见还是隐藏**。

> visibility : visible;	元素可视
>
> visibility : hidden;	元素隐藏

<span style="color:red;">visibility隐藏元素后，继续占有原来的位置。</span>

#### overflow溢出显示隐藏

overflow属性指定了如果内容溢出一个元素的框（超过其指定高度及宽度）时，会发生什么，只对溢出的部分处理。

| 可能的值 | 描述                                                     |
| :------- | :------------------------------------------------------- |
| visible  | 默认值。内容不会被修剪，会呈现在元素框之外。             |
| hidden   | 内容会被修剪，并且其余内容是不可见的。                   |
| scroll   | 内容会被修剪，但是浏览器会显示滚动条以便查看其余的内容。 |
| auto     | 如果内容被修剪，则浏览器会显示滚动条以便查看其余的内容。 |
| inherit  | 规定应该从父元素继承 overflow 属性的值。                 |

一般情况下，我们都不想让溢出的内容显示出来，因为溢出的部分会影响布局。但是如果有定位的盒子认为设置的超出部分，请慎用overflow:hidden 因为它会隐藏多余的部分。

### 十八、CSS高级技巧

#### 精灵图

**目的**：降低服务器压力，减少请求次数。

**使用**

1. 精灵技术主要针对于背景图片使用。就是把多个小背景图片整合到一张大图片中。
2. 这个大图片也称为sprites、精灵图或者雪碧图。
3. 移动背景图片位置,此时可以使用`background-position`。
4. 移动的距离就是这个目标图片的x和y坐标。`注意网页中的坐标有所不同`。
5. 因为一般情况下都是`往上往左移动`，所以`数值负值`。。

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>精灵图</title>
  <style>
    .box {
      width: 60px;
      height: 60px;
      margin: 100px auto;
      /* 主要是使用背景以及背景的background-posion属性 */
      background: url(img/sprites.png) no-repeat -182px 0px;
    }
  </style>
</head>

<body>
  <div class="box"></div>
</body>

</html>
```

#### 字体图标

精灵图是有诸多优点的,但是缺点很明显。

1. 图片文件还是比较大的。
2. 图片本身放大和缩小会失真。
3. 一旦图片制作完毕想要更换非常复杂。

此时，有一种技术的出现很好的解决了以上问题，就是字体图标 iconfont。

字体图标可以为前端工程师提供一种方便高效的图标使用方式，`展示的是图标`，`本质属于字体`。



##### 字体图标的优点

1. 轻量级：一个图标字体要比一系列的图像要小。一旦字体加载了,图标就会马上渲染出来，减少了服务器请求；
2. 灵活性：本质其实是文字,可以很随意的改变颜色、产生阴影、透明效果、旋转等；
3. 兼容性：`几乎支持所有的浏览器`，请放心使用；

**注意**：字体图标不能替代精灵技术，只是对工作中图标部分技术的提升和优化。



**总结**:

1. 如果遇到-些结构和样式比较简单的小图标，就用字体图标。
2. 如果遇到一 些结构和样式复杂一 点的小图片，就用精灵图。



##### 字体图标的使用

1. 下载字体图标

*  [icomoon字库](http://icomoon.io)  
  * IcoMoon成立于2011年,推出了第-一个自定义图标字体生成器,允许用户选择所需要的图标,使它们成
    一字型。 该字库内容种类繁多，非常全面，唯一的遗憾是国外服务器，打开网速较慢。<span style="color:red;">免费</span>
* [阿里iconfont字库](http://www.iconfont.cn)
  * 这个是阿里妈妈M2UX的一个iconfont字体图标字库,包含了淘宝图标库和阿里妈妈图标库。可以使用Al制作图标上传生成。<span style="color:red;">免费</span>

2. 字体图标的引入（引入到html页面中）

* 将下载下来的fonts文件夹放在合适的路径下；

* 在CSS样式中全局声明字体（可以理解为把这些字体文件通过CSS引入到页面中）

  要注意字体文件的路径问题。

* [iconmoon字体图标使用](https://www.bilibili.com/video/BV14J4114768?p=257)
* [阿里矢量图库字体图标使用](https://www.iconfont.cn/help/detail?spm=a313x.7781069.1998910419.d8cf4382a&helptype=code)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>字体图标的使用</title>
  <style>
    /* 字体声明 */
    @font-face {
      font-family: 'iconfont';
      /* Project id 2986248 */
      src: url('//at.alicdn.com/t/font_2986248_p7pfwmnao7.woff2?t=1642240730393') format('woff2'),
        url('//at.alicdn.com/t/font_2986248_p7pfwmnao7.woff?t=1642240730393') format('woff'),
        url('//at.alicdn.com/t/font_2986248_p7pfwmnao7.ttf?t=1642240730393') format('truetype');
    }

    .iconfont {
      font-family: "iconfont" !important;
      font-size: 20px;
      font-style: normal;
      /* -webkit-font-smoothing: antialiased;
      -webkit-text-stroke-width: 0.2px;
      -moz-osx-font-smoothing: grayscale; */
    }
  </style>
</head>

<body>
  <span class="iconfont">&#xe60d;</span>
  <span class="iconfont">&#xe6b4;</span>
  <span class="iconfont">&#xe646;</span>
</body>

</html>
```



##### 字体图标的追加

如果工作中,原来的字体图标不够用了, 我们需要添加新的字体图标到原来的字体文件中。

1. iconmoon字体图标追加

* 把压缩包里面的selection.json从新上传，然后选中自己想要新的图标，重新下载压缩包，并替换原来的文件即可。

2. 阿里矢量字体图标追加

* 暂时没有



#### CSS三角形的做法

[CSS实现带小三角形的边框](https://blog.csdn.net/qq_21108311/article/details/104038590)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>CSS三角形</title>
  <style>
    .box {
      width: 0;
      height: 0;
      /* 兼容性代码 */
      font-size: 0;
      line-height: 0;

      border-bottom: 50px solid pink;
      border-top: 50px solid black;
      border-left: 50px solid blueviolet;
      border-right: 50px solid purple;
    }

    .box1 {
      margin: 100px auto;
      width: 0;
      height: 0;
      font-size: 0;
      line-height: 0;
      /* 指向上方 */
      border: 50px solid transparent;
      border-bottom-color: pink;
    }

    .box2 {
      margin: 100px auto;
      width: 0;
      height: 0;
      font-size: 0;
      line-height: 0;
      /* 指向左侧 */
      border: 50px solid transparent;
      border-right-color: blue;
    }
  </style>
</head>

<body>
  <div class="box"></div>
  <div class="box1"></div>
  <div class="box2"></div>
</body>

</html>
```

#### CSS用户界面样式

所谓的界面样式，就是更改一些用户操作样式，以便提高更好的用户体验。

##### 鼠标样式cursor

设置或检索在对象上移动的鼠标指针采用何种系统预定义的光标形状。

| 可能的值  | 描述                                                         |
| :-------- | :----------------------------------------------------------- |
| *url*     | 需使用的自定义光标的 URL。<br>注释：请在此列表的末端始终定义一种普通的光标，以防没有由 URL 定义的可用光标。 |
| default   | 默认光标（通常是一个箭头）                                   |
| auto      | 默认。浏览器设置的光标。                                     |
| crosshair | 光标呈现为十字线。                                           |
| pointer   | 光标呈现为指示链接的指针（一只手）                           |
| move      | 此光标指示某对象可被移动。                                   |
| e-resize  | 此光标指示矩形框的边缘可被向右（东）移动。                   |
| ne-resize | 此光标指示矩形框的边缘可被向上及向右移动（北/东）。          |
| nw-resize | 此光标指示矩形框的边缘可被向上及向左移动（北/西）。          |
| n-resize  | 此光标指示矩形框的边缘可被向上（北）移动。                   |
| se-resize | 此光标指示矩形框的边缘可被向下及向右移动（南/东）。          |
| sw-resize | 此光标指示矩形框的边缘可被向下及向左移动（南/西）。          |
| s-resize  | 此光标指示矩形框的边缘可被向下移动（南）。                   |
| w-resize  | 此光标指示矩形框的边缘可被向左移动（西）。                   |
| text      | 此光标指示文本。                                             |
| wait      | 此光标指示程序正忙（通常是一只表或沙漏）。                   |
| help      | 此光标指示可用的帮助（通常是一个问号或一个气球）。           |

##### 表单轮廓线outline

outline（轮廓）是绘制于元素周围的一条线，位于边框边缘的外围，可起到突出元素的作用。

outline简写属性在一个声明中设置所有的轮廓属性。可以设置的属性分别是（按顺序）：outline-color, outline-style, outline-width。如果不设置其中的某个值也是允许的。

```css
选择器 {
	/* 取消轮廓线 */
	outline:none;
}
```

##### 防止文本域拖拽resize

```css
textarea {
	resize:none; 
}
```

#### vertical-align属性应用

##### 用于设置图片或者表单（行内块元素）文字垂直对齐。

**官方解释**：用于设置一个元素的垂直对齐方式，但是它只针对于行内元素或者行内块元素有效。

**语法**

```css
vertical-align : baseline|top| middle|bottom；
```

| 可能的值    | 描述                                                         |
| :---------- | :----------------------------------------------------------- |
| baseline    | 默认。元素放置在父元素的基线上。                             |
| sub         | 垂直对齐文本的下标。                                         |
| super       | 垂直对齐文本的上标                                           |
| top         | 把元素的顶端与行中最高元素的顶端对齐                         |
| text-top    | 把元素的顶端与父元素字体的顶端对齐                           |
| middle      | 把此元素放置在父元素的中部。                                 |
| bottom      | 使元素及其后代元素的底部与整行的底部对齐。                   |
| text-bottom | 把元素的底端与父元素字体的底端对齐。                         |
| length      | 将元素升高或降低指定的高度，可以是负数。                     |
| %           | 使用 "line-height" 属性的百分比值来排列此元素。允许使用负值。 |
| inherit     | 规定应该从父元素继承 vertical-align 属性的值。               |

![基线、中线……](http://pic.tolie.biz/images/image-20220115205502200.png)

```html
<style>
    .account a{
      float: left;
      height: 42px;
      margin-right: 30px;
      line-height: 42px;
      color: #050505;
    }
    .account a img{
      /* 中线对齐 */
      vertical-align: middle;
</style> 

<div class="account clearfix">
      <a href="#"><img src="images/头像.png" alt="">
        qq-leishui</a>
    </div>
```

##### 去除图片底侧的空白缝隙

**bug**：图片和文字在一行时，图片的底侧会有一个空白缝隙；

**原因**：是因为行内块元素会和文字的基线对齐。

![图片底侧的空白缝隙](http://pic.tolie.biz/images/image-20220116113953843.png)

* 主要解决方法有两种:
  1. 给图片添加vertical-align: middle | top | bottom等。(`提倡使用的`）

让图片和文字不再以基线对齐；

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>去除图片底侧的空白缝隙</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        .box {
            margin: 100px auto;
            background-color: pink;
        }

        .box img {
            /* vertical-align: middle; */
            vertical-align: bottom;
        }
    </style>
</head>

<body>
    <div class="box">
        <img src="img/bg1.jpg" alt="">我是你的爸爸
    </div>
</body>

</html>
```

![去除图片底侧的空白缝隙-1](http://pic.tolie.biz/images/image-20220116114105451.png)



2. 把图片转换为块级元素display. block;（`不提倡`，可能会导致排版错误）

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>去除图片底侧的空白缝隙</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        .box {
            margin: 100px auto;
            background-color: pink;
        }

        .box img {
            display: block;
        }
    </style>
</head>

<body>
    <div class="box">
        <img src="img/bg1.jpg" alt="">
    </div>
</body>

</html>
```



#### 溢出的文字省略号显示

##### 单行文本溢出显示省略号

固定写法：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        .box {
            margin: 100px auto;
            width: 100px;
            height: 80px;
            background-color: pink;

            /*1.先强制一行内显示文本，超出部分也在一行显示*/
            white-space: nowrap;
            /*(默认normal自动换行)*/

            /*2.超出的部分隐藏*/
            overflow: hidden;
            /*3.文字用省略号昔代超出的部分*/
            text-overflow: ellipsis;

        }
    </style>
</head>

<body>
    <div class="box">
        1
    </div>
</body>

</html>
```



##### 多行文本溢出显示省略号

`多行文本溢出显示省略号`，`有较大兼容性问题`，适合于webKit浏览器或移动端（移动端大部分是webkit内核）

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        .box {
            margin: 100px auto;
            /* 
            要控制好盒子的大小，因为只会在第二行加入省略号
            后续行如果还有文字，仍然会显示出来
            */
            width: 100px;
            height: 45px;
            background-color: pink;

            overflow: hidden;
            text-overflow: ellipsis;
            /*弹性伸缩盒子模型显示*/
            display: -webkit-box;
            /*限制在一个块元素显示的文本的行数*/
            -webkit-line-clamp: 2;
            /*设置或检索伸缩盒对象的子元素的排列方式*/
            -webkit-box-orient: vertical;


        }
    </style>
</head>

<body>
    <div class="box">
        马古法金GIA健康码国家安康咖喱块结构看阿加几个为哦啊接哦为阿技工为爱护公监理机构
    </div>
</body>

</html>
```

<span style="color:red;">更推荐让后台人员来做这个效果,因为后台人员可以设置显示多少个字，操作更简单。</span>

#### margin负值的巧妙使用

![浮动的盒子边框会因为相邻而变宽](http://pic.tolie.biz/images/image-20220116121537256.png)

1. 让每个盒子margin往左侧移动`负一个边框的距离`正好压住相邻盒子边框
2. 鼠标经过某个盒子的时候，提高当前盒子的层级即可
   * 如果没有定位，则加相对定位(保留位置) ；
   * 如果有定位，则加z-index。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        .clearfix :before,
        .clearfix:after {
            content: "";
            display: table;
        }

        .clearfix:after {
            clear: both;
        }

        .clearfix {
            *zoom: 1;
        }

        a {
            text-decoration: none;
        }

        ul {
            list-style: none;
            margin: 100px auto;
            width: 1200px;
        }

        .box_con {
            float: left;
            position: relative;
            width: 228px;
            height: 270px;
            margin-left: -1px;
            border: 1px solid white;
            background-color: pink;
        }

        .box_con:hover {

            border: 1px solid black;
            /* 
            
            避免边框被兄弟节点遮盖，保证四个边框全部漏出
            兄弟节点全都有定位，所以可以设置z-index属性使其显现
             */
            z-index: 1;
        }

        .box_con:nth-child(5n) {
            margin-right: 0;
        }

        .box_con .box_con_bg {
            width: 100%;
        }

        .box_con h4 {
            padding: 25px 20px 20px;
            font-size: 14px;
            font-weight: normal;
            color: #050505;
        }

        .box_con .info {
            padding: 0 20px;
            font-size: 12px;
            color: #999;
        }

        .box_con .hot {
            position: absolute;
            top: 4px;
            right: -4px;
        }

        .box_con .info span {
            color: #ff7c2d;
        }
    </style>
</head>

<body>
    <ul class="clearfix">
        <li class="box_con">
            <a href="#">
                <img src="img/图层137.png" alt="" class="box_con_bg">
                <h4>Think PHP 5.0 博客系统实战项目演练</h4>
                <div class="info"><span>高级</span> • 1125人在学习</div>
                <img src="img/形状24.png" alt="" class="hot">
            </a>
        </li>
        <li class="box_con">
            <a href="#">
                <img src="img/图层137.png" alt="" class="box_con_bg">
                <h4>Think PHP 5.0 博客系统实战项目演练</h4>
                <div class="info"><span>高级</span> • 1125人在学习</div>
                <img src="img/形状24.png" alt="" class="hot">
            </a>
        </li>
        <li class="box_con">
            <a href="#">
                <img src="img/图层137.png" alt="" class="box_con_bg">
                <h4>Think PHP 5.0 博客系统实战项目演练</h4>
                <div class="info"><span>高级</span> • 1125人在学习</div>
                <img src="img/形状24.png" alt="" class="hot">
            </a>
        </li>
        <li class="box_con">
            <a href="#">
                <img src="img/图层137.png" alt="" class="box_con_bg">
                <h4>Think PHP 5.0 博客系统实战项目演练</h4>
                <div class="info"><span>高级</span> • 1125人在学习</div>
                <img src="img/形状24.png" alt="" class="hot">
            </a>
        </li>
        <li class="box_con">
            <a href="#">
                <img src="img/图层137.png" alt="" class="box_con_bg">
                <h4>Think PHP 5.0 博客系统实战项目演练</h4>
                <div class="info"><span>高级</span> • 1125人在学习</div>
                <img src="img/形状24.png" alt="" class="hot">
            </a>
        </li>
    </ul>

</body>

</html>
```

#### 文字围绕浮动元素巧妙运用

浮动本身就是为了设置图片的环绕文字效果；

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>图片的环绕文字效果</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        a {
            display: block;
            margin: 100px auto;
            width: 420px;
            height: 150px;
            background-color: pink;
        }

        a img {
            float: left;
            width: 300px;
            height: 150px;
            margin-right: 5px;

        }
    </style>
</head>

<body>
    <a href="#">
        <img src="img/环绕文字.jpg" alt="">
        梅西巴黎和C罗曼联，不是欧冠大热门的原因梅西巴黎和C罗曼联，罗曼联，不是欧冠大热门的原因
    </a>
</body>

</html>
```

#### 行内块的巧妙使用

行内块元素不用再利用margin就可以居中(text-align:cernter)，且之间有缝隙。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JD下方换页部件</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        .box {
            /*  width: 1200px;
            margin: 100px auto; */
            /* 行内块元素不用再利用margin就可以居中 */
            text-align: center;
        }

        .box a {
            display: inline-block;
            width: 36px;
            height: 36px;
            background-color: #f7f7f7;
            border: 1px solid #ccc;
            text-decoration: none;
            text-align: center;
            line-height: 38px;
            font-size: 14px;
            color: #333;
        }

        .box a span {
            color: #b1b4c5;
            margin: 0 4px;
        }

        .box .pre,
        .box .next {
            width: 84px;
        }

        .box .current {
            background-color: #fff;
            border: none;
            color: #e4393c;
        }

        .box .etc {
            background-color: #fff;
            border: none;
        }

        /* 有一个小bug input上方有个缝隙 ？？ */
        .box input {
            width: 36px;
            height: 36px;
            border: 1px solid #ccc;
        }
    </style>
</head>

<body>
    <div class="box">
        <a href="" class="pre"><span>&lt;</span>上一页</a>
        <a href="#">1</a>
        <a href="#" class="current">2</a>
        <a href="#">3</a>
        <a href="#">4</a>
        <a href="#">5</a>
        <a href="#">6</a>
        <a href="#">7</a>
        <a href="#">8</a>
        <a href="#" class="etc">...</a>
        <a href="#" class="next">下一页<span>&gt;</span></a>
        到第
        <input type="text">
        页
        <a href="#">确定</a>
    </div>

</body>

</html>
```

#### CSS三角形的巧妙使用

![CSS三角](http://pic.tolie.biz/images/image-20220116131014373.png)

* 实现直角三角形

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box {
            width: 0;
            height: 0;

            /* 直角三角形 */

            /*  border-bottom: 0 solid blue;
            border-top: 100px solid transparent;
            border-right: 50px solid red;
            border-left: 0 solid pink; */

            border-color: transparent red transparent transparent;
            border-style: solid;
            border-width: 100px 50px 0 0;
        }
    </style>
</head>

<body>
    <div class="box"></div>
</body>

</html>
```

* 实现上图效果

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;

        }

        .clearfix :before,
        .clearfix:after {
            content: "";
            display: table;
        }

        .clearfix:after {
            clear: both;
        }

        .clearfix {
            *zoom: 1;
        }

        .box {
            position: relative;
            margin: 100px auto;
            width: 800px;
            height: 48px;
            border: 1px solid red;
        }

        .box p {
            float: left;
            width: 400px;
            line-height: 48px;
            text-align: center;

        }

        .box p:first-child {
            background-color: red;
            color: #fff;
            font-weight: bold;
        }

        .box p:nth-child(2) {
            color: #999;
            font-weight: lighter;
        }

        .box i {
            position: absolute;
            left: 50%;
            margin-left: -25px;
            width: 0;
            height: 0;

            /* 直角三角形 */
            border-color: transparent pink transparent transparent;
            border-style: solid;
            border-width: 48px 25px 0 0;

        }
    </style>
</head>

<body>
    <div class="box clearfix">
        <p>￥2099.00</p>
        <p><del>￥2649.00</del></p>
        <i></i>
    </div>
</body>

</html>
```

![CSS直角三角形](http://pic.tolie.biz/images/202203141109417.png)

#### CSS的初始化

不同浏览器对有些标签的默认值是不同的，为了消除不同浏览器对HTML文本呈现的差异，照顾浏览器的兼容，我们需要对CSS初始化

> *简单理解*： CSS初始化是指重设浏览器的样式。(也称为CSS reset )

**Unicode编码字体**:
把中文字体的名称用相应的Unicode编码来代替，这样就可以有效的避免浏览器解释CSS代码时候出现乱码的问题。比如:

| 字体名称 | Unicode编码          |
| -------- | -------------------- |
| 黑体     | \9ED1\4F53           |
| 宋体     | \5B8B\4F53           |
| 微软雅黑 | \5FAE\8F6F\96C5\9ED1 |

```css
/* 把我们所有标签的内外边距清零 */
* {
    margin: 0;
    padding: 0
}
/* em 和 i 斜体的文字不倾斜 */
em,
i {
    font-style: normal
}
/* 去掉li 的小圆点 */
li {
    list-style: none
}

img {
    /* border 0 照顾低版本浏览器 如果 图片外面包含了链接会有边框的问题 */
    border: 0;
    /* 取消图片底侧有空白缝隙的问题 */
    vertical-align: middle
}

button {
    /* 当我们鼠标经过button 按钮的时候，鼠标变成小手 */
    cursor: pointer
}

a {
    color: #666;
    text-decoration: none
}

a:hover {
    color: #c81623
}

button,
input {
    /* "\5B8B\4F53" 是Unicode的编码字体
    就是宋体的意思 这样浏览器兼容性比较好 */
    font-family: Microsoft YaHei, Heiti SC, tahoma, arial, Hiragino Sans GB, "\5B8B\4F53", sans-serif
}

body {
    /* CSS3 抗锯齿形 让文字显示的更加清晰 */
    -webkit-font-smoothing: antialiased;
    background-color: #fff;
    font: 12px/1.5 Microsoft YaHei, Heiti SC, tahoma, arial, Hiragino Sans GB, "\5B8B\4F53", sans-serif;
    color: #666
}

.hide,
.none {
    display: none
}
/* 清除浮动 */
.clearfix:after {
    visibility: hidden;
    clear: both;
    display: block;
    content: ".";
    height: 0
}

.clearfix {
    *zoom: 1
}
```

### 十九、HTML5和CSS3提高

#### HTML5的新特性

HTML5的新增特性主要是针对于以前的不足，增加了一些新的标签、新的表单和新的表单属性等。

这些新特性都有兼容性问题，基本是IE9+以上版本的浏览器才支持，如果不考虑兼容性问题，可以大量使用这些新特性。

##### HTML5新增的语义化标签

###### 为什么需要语义化

- 易修改、易维护。
- 无障碍阅读支持。
- 搜索引擎友好，利于 SEO。
- 面向未来的 HTML，浏览器在未来可能提供更丰富的支持。



以前布局，我们基本用div来做。`div 对于搜索引擎来说是没有语义的`。

> &lt;header&gt; :头部标签
> &lt;nav&gt; :导航标签
> &lt;article&gt; : 内容标签
> &lt;section&gt; :定义文档某个区域
> &lt;aside&gt; : 侧边栏标签
> &lt;footer&gt; :尾部标签

![典型的HTML文档结构](http://pic.tolie.biz/images/202203131903668.png)

**注意**:

1. 这种`语义化标准主要是针对搜索引擎`的；
2. 这些新标签页面中`可以使用多次`；
3. 在`IE9`中，`需要把这些元素转换为块级元素`；
4. 移动端更喜欢使用这些标签；
5. HTML5还增加了很多其他标签；



##### HTML5新增的多媒体标签

使用它们可以很方便的在页面中嵌入音频和视频，而不再使用flash和其他浏览器插件。

###### 音频: &lt;audio&gt;

音频格式及浏览器支持	`尽量使用mp3格式`

| 浏览器               | MP3  | Wav  | Ogg  |
| :------------------- | :--- | :--- | :--- |
| Internet Explorer 9+ | YES  | NO   | NO   |
| Chrome 6+            | YES  | YES  | YES  |
| Firefox 3.6+         | YES  | YES  | YES  |
| Safari 5+            | YES  | YES  | NO   |
| Opera 10+            | YES  | YES  | YES  |

**语法**

```html
<audio controls>
  <source src="horse.ogg" type="audio/ogg">
  <source src="horse.mp3" type="audio/mpeg">
  <!-- 当用户浏览器不支持H5时，此处的文字会展示在页面内 -->
   您的浏览器不支持 audio 元素。
</audio>
```

**可能的属性值**

| 属性     | 值       | 描述                                                         |
| :------- | :------- | :----------------------------------------------------------- |
| autoplay | autoplay | 如果出现该属性，则音频在就绪后马上播放。(`Chrome禁用了自动播放，暂无好的解决办法`) |
| controls | controls | 如果出现该属性，则向用户显示控件，比如播放按钮。             |
| loop     | loop     | 如果出现该属性，则每当音频结束时重新开始播放。               |
| muted    | muted    | 规定视频输出应该被静音。                                     |
| preload  | preload  | 如果出现该属性，则音频在页面加载时进行加载，并预备播放。如果使用 "autoplay"，则忽略该属性。 |
| src      | *url*    | 要播放的音频的 URL。                                         |



###### 视频: &lt;video&gt;

视频格式与浏览器的支持		`尽量使用mp4格式`

| 浏览器            | MP4                  | WebM | Ogg  |
| :---------------- | :------------------- | :--- | :--- |
| Internet Explorer | YES                  | NO   | NO   |
| Chrome            | YES                  | YES  | YES  |
| Firefox           | YES                  | YES  | YES  |
| Safari            | YES                  | NO   | NO   |
| Opera             | YES (从 Opera 25 起) | YES  | YES  |

**语法**

```html
<video width="320" height="240" controls>
    <source src="movie.mp4" type="video/mp4">
    <source src="movie.ogg" type="video/ogg">
    <!-- 当用户浏览器不支持H5时，此处的文字会展示在页面内 -->
    您的浏览器不支持 video 标签。
</video>

```

**可能的属性值**

| 属性     | 值                      | 描述                                                         |
| :------- | :---------------------- | :----------------------------------------------------------- |
| autoplay | autoplay                | 如果出现该属性，则视频在就绪后马上播放。(`Chrome需要添加muted来解决自动播放问题`) |
| controls | controls                | 如果出现该属性，则向用户显示控件，比如播放按钮。             |
| height   | pixels<br>(像素)        | 设置视频播放器的高度。                                       |
| loop     | loop                    | 如果出现该属性，则`当媒介文件完成播放后再次开始播放`。       |
| muted    | muted                   | 如果出现该属性，视频的音频输出为静音。                       |
| poster   | *URL*                   | 规定视频正在下载时显示的图像，直到用户点击播放按钮。         |
| preload  | auto <br/>metadata none | 如果出现该属性，则视频在页面加载时进行加载，并预备播放。如果使用 "autoplay"，则忽略该属性。 |
| src      | *URL*                   | 要播放的视频的 URL。                                         |
| width    | pixels<br/>(像素)       | 设置视频播放器的宽度。                                       |



##### HTML5新增的input类型

[H5-input类型](https://www.runoob.com/tags/tag-input.html)

![HTML5新增的input类型](http://pic.tolie.biz/images/image-20220116184041691.png)



##### HTML5新增的表单属性

![HTML5新增的表单属性](http://pic.tolie.biz/images/image-20220116201719589.png)

**修改placeholder样式**

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>修改placeholder样式</title>
    <style>
        input::placeholder {
            /* 伪元素 修改placeholder样式 */
            color: pink;
        }
    </style>
</head>

<body>
    <form action="#">
        <input type="search" placeholder="TOLIE">
        <button type="submit">提交</button>
    </form>
</body>

</html>
```



#### CSS3的新特性

##### 新增选择器

<span style='color:red'> 见 part 1</span>



##### CSS3盒子模型

CSS3中可以通过`box-sizing`来指定盒模型，有2个值：即可指定为`content- box`、`border-box`，这样我们计算盒子大小的方式就发生了改变。

可以分成两种情况:
1. box-sizing：content-box：盒子大小为width + padding + border (`默认`)
2. box-sizing：border-box：盒子大小为width；

> 如果盒子模型我们改为了box-sizing: border- box，那padding和border就不会撑大盒子了 (`前提padding和border不会超过width宽度`)



##### CSS3其他特性

###### CSS3滤镜filter

filter CSS属性将模糊或颜色偏移等图形效果应用于元素。

CSS 语法

```css
filter: blur();
/*  none | blur() | brightness() | contrast() | drop-shadow() 
	等其他的Filter函数*/
```



| Filter函数        | 描述                                                         |
| :---------------- | :----------------------------------------------------------- |
| none              | `默认值`，没有效果。                                         |
| blur(*px*)        | 给图像设置`高斯模糊`。"radius"一值设定高斯函数的标准差，或者是屏幕上以多少像素融在一起， 所以`值越大越模糊`，同时`注意数值要加px单位`；<br>如果没有设定值，则默认是0；这个参数可设置css长度值，但不接受百分比值。 |
| brightness(*%*)   | 给图片应用一种线性乘法，使其看起来更亮或更暗。如果值是0%，图像会全黑。值是100%，则图像无变化。其他的值对应线性乘数效果。值超过100%也是可以的，图像会比原来更亮。如果没有设定值，默认是1。 |
| contrast(*%*)     | 调整图像的对比度。值是0%的话，图像会全黑。值是100%，图像不变。值可以超过100%，意味着会运用更低的对比。若没有设置值，默认是1。 |
| grayscale(*%*)    | 将图像转换为灰度图像。值定义转换的比例。值为100%则完全转为灰度图像，值为0%图像无变化。值在0%到100%之间，则是效果的线性乘子。若未设置，值默认是0； |
| hue-rotate(*deg*) | 给图像应用色相旋转。"angle"一值设定图像会被调整的色环角度值。值为0deg，则图像无变化。若值未设置，默认值是0deg。该值虽然没有最大值，超过360deg的值相当于又绕一圈。 |
| invert(*%*)       | 反转输入图像。值定义转换的比例。100%的价值是完全反转。值为0%则图像无变化。值在0%和100%之间，则是效果的线性乘子。 若值未设置，值默认是0。 |
| opacity(*%*)      | 转化图像的透明程度。值定义转换的比例。值为0%则是完全透明，值为100%则图像无变化。值在0%和100%之间，则是效果的线性乘子，也相当于图像样本乘以数量。 若值未设置，值默认是1。该函数与已有的opacity属性很相似，不同之处在于通过filter，一些浏览器为了提升性能会提供硬件加速。 |
| saturate(*%*)     | 转换图像饱和度。值定义转换的比例。值为0%则是完全不饱和，值为100%则图像无变化。其他值，则是效果的线性乘子。超过100%的值是允许的，则有更高的饱和度。 若值未设置，值默认是1。 |
| sepia(*%*)        | 将图像转换为深褐色。值定义转换的比例。值为100%则完全是深褐色的，值为0%图像无变化。值在0%到100%之间，则是效果的线性乘子。若未设置，值默认是0； |
| url()             | URL函数接受一个XML文件，该文件设置了 一个SVG滤镜，且可以包含一个锚点来指定一个具体的滤镜元素。例如： |

###### 媒体查询









##### CSS3 calc函数

calc()此CSS函数让你在声明CSS属性值时执行一些计算。

- 需要注意的是，运算符前后都需要保留一个空格，<br>例如：`width: calc(100% - 10px)`；
- 任何长度值都可以使用calc()函数进行计算；
- calc()函数支持 "+", "-", "*", "/" 运算；
- calc()函数使用标准的数学运算优先级规则；

**CSS 语法**

```css
width:calc(expression);
/* expression必须是一个数学表达式，结果将采用运算后的返回值。 */

/* 这里表示此盒子的宽度永远比其父盒子小30px */
width: calc(100% - 30px);
```



#### CSS3动画**

##### CSS3过渡

过渡( transition)是CSS3中具有颠覆性的特征之一，我们可以在不使用 Flash 动画或
JavaScript的情况下，当元素从一种样式变换为另一种样式时为元素添加效果。

> 过渡动画：是从一个状态渐渐的过渡到另外一个状态

可以让我们页面更好看，更动感十足，`虽然低版本浏览器不支持( ie9以下版本)但是不会影响页面布局`。
我们现在经常和:hover 一起搭配使用。

<span style='color:red'>过渡的使用口诀：谁做过渡给谁加</span>

**语法**

```css
transition: property duration timing-function delay;
		/* 要过渡的属性、花费时间、运动曲线、何时开始; */
```

| 值                         | 描述                                                         |
| :------------------------- | :----------------------------------------------------------- |
| transition-property        | 规定设置过渡效果的 CSS 属性的名称。如果想要所有的属性都变化过渡，写一个all就可以。 |
| transition-duration        | 规定完成过渡效果需要多少秒或毫秒，`必须写单位`。             |
| transition-timing-function | 规定速度效果的速度曲线。                                     |
| transition-delay           | 定义过渡效果何时开始。                                       |

> *注意*：请始终设置 transition-duration 属性，否则时长为 0，就不会产生过渡效果。



**transition-timing-function**

| 可能的值                      | 描述                                                         |
| :---------------------------- | :----------------------------------------------------------- |
| linear                        | 规定以相同速度开始至结束的过渡效果<br/>（等于 cubic-bezier(0,0,1,1)）。 |
| ease                          | `默认`，规定慢速开始，然后变快，然后慢速结束的过渡效果（cubic-bezier(0.25,0.1,0.25,1)）。 |
| ease-in                       | 规定以慢速开始的过渡效果<br>（等于 cubic-bezier(0.42,0,1,1)）。 |
| ease-out                      | 规定以慢速结束的过渡效果<br/>（等于 cubic-bezier(0,0,0.58,1)）。 |
| ease-in-out                   | 规定以慢速开始和结束的过渡效果<br/>（等于 cubic-bezier(0.42,0,0.58,1)）。 |
| cubic-bezier(*n*,*n*,*n*,*n*) | 在 cubic-bezier 函数中定义自己的值。可能的值是 0 至 1 之间的数值。 |

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>CSS过渡效果</title>
  <style>
    div {
      width: 100px;
      height: 200px;
      background-color: pink;
      /* 
        谁过渡，给谁加transition属性
        与:hover配合使用
      */

      /* 过渡属性 变换时间 运动曲线 何时开始 */
      /* transition: height 0.5s ease 1s; */

      /* 同时变换多个属性可以采用以下的方式 */
      /* transition: height 0.5s, width 0.5s; */

      /* 如果想要所有的属性都变化过渡，写一个all就可以。 */
      transition: all 0.5s;
    }

    div:hover {
      width: 200px;
      height: 400px;
      background-color: #115154;
    }
  </style>
</head>

<body>
  <div>

  </div>
</body>

</html>
```



##### CSS3 2D转换

`转换( transform )`是CSS3中具有颠覆性的特征之一, 可以实现元素的位移、旋转、缩放等效果。

2D转换是改变标签在二维平面上的位置和形状的一种技术。



###### 移动translate

2D移动是2D转换里面的一种功能，可以改变元素在页面中的位置，类似`定位`。

```css
div{
transform: translate(x,y);	/* x y 都2D移动 */
transform: translateX(n) ;	/* x 2D移动 */
transform: translateY(n) ;	/* y 2D移动 */
}
```

**重点**

* 定义2D转换中的移动，沿着X和Y轴移动元素
* `translate最大的优点：不会影响到其他元素的位曾`
* translate中的百分比单位是`相对于自身元素`的translate:(50%,50%);
* `对行内标签没有效果`。

定位加移动实现盒子的水平、垂直居中

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>定位加移动实现水平垂直居中</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        .box {
            position: relative;
            margin: 100px auto;
            width: 200px;
            height: 200px;
            background-color: pink;
        }

        p {
            position: absolute;
            width: 50px;
            height: 50px;
            /* 水平居中 垂直居中 */
            left: 50%;
            top: 50%;
            transform: translate(-50%, -50%);

            background-color: blue;

        }
    </style>
</head>

<body>
    <div class="box">
        <p></p>
    </div>
</body>

</html>
```





###### 旋转rotate

2D旋转指的是让元素在2维平面内顺时针旋转或者逆时针旋转。

**语法**

> transform: rotate (度数)

**重点**

* rotate里面跟`度数`，`单位是deg`，比如rotate(45 deg)；
* 角度为正时，顺时针旋转；为负时，为逆时针；
* `默认旋转的中心点是元素的中心点`。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>旋转</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        img {
            display: block;
            margin: 100px auto;
            width: 200px;
            transition: all 2s ease;
        }

        img:hover {
            transform: rotate(360deg);
        }
    </style>
</head>

<body>
    <img src="img/成功-绿.png" alt="">
</body>

</html>
```



**CSS3的展开三角**

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>旋转</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        p {
            width: 10px;
            height: 10px;
            margin: 200px auto;
            border-right: 2px solid black;
            border-bottom: 2px solid black;
            /* 顺时针旋转45度 */
            transform: rotate(45deg);
        }
    </style>
</head>

<body>
    <p></p>
</body>

</html>
```



###### 缩放scale

缩放，顾名思义，可以放大和缩小。只要给元素添加上了这个属性就能控制它放大还是缩小。
**语法**

> transform:scale(x,y) ;

**注意**

* 其中的x和y用`逗号`分隔
* transform:scale(1,1) : 宽和高都放大一倍，相对于没有放大；
* transform:scale(2,2) : 宽和高都放大了2倍；
* transform:scale(2) : `只写一个参数，第二个参数则和第一个参数一样`，相当于scale(2,2)；
* transform:scale(0.5,0.5) :缩小；
* sacle缩放最大的优势：可以设置转换中心点缩放，`默认以中心点缩放的，而且不影响其他盒子`。

```css
.box {
            margin: 200px auto;
            height: 200px;
            width: 200px;
            background-color: pink;
            /* 水平、垂直都放大为2倍 */
            /* 
    			transform: scale(2, 2); 
    			transform: scale(2); 
    		*/
    
            /* 水平、垂直都缩小为原来的二分之一倍 */
            /* 
                transform: scale(.5, .5);
                transform: scale(.5); 
            */

            /*  
                transform: scaleX(2);
                transform: scaleY(2);
                不能同时出现
            */

            /* 水平都放大为2倍 */
            /* transform: scaleX(2); */
            /* 垂直都放大为2倍 */
            /*transform: scaleY(2);*/
        }
```



###### 2D转换中心点设置

**语法**

> transform-origin: x y;

**重点**

* 注意后面的参数x和y用`空格`隔开；
* `x y默认转换的中心点是元素的中心点(50% 50%);`
* 还可以给 x y 设置`像素`或者`方位名词`( top bottom left right center )

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>旋转</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        /* 
            思路：
            大盒子包着一个小盒子，小盒子设置超出部分隐藏；
            小盒子有一个子元素，与小盒子宽高都一样；
            并进行旋转，因为小盒子设置了超出隐藏
            所以这个子元素看不见
            鼠标经过小盒子，子元素旋转角度归零
         */
        .box {
            position: relative;
            margin: 100px auto;
            width: 400px;
            height: 400px;
            background-color: blue;
        }

        .con {
            position: absolute;
            top: 50%;
            left: 50%;
            width: 100px;
            height: 100px;
            overflow: hidden;
            transform: translate(-50%, -50%);
            background-color: pink;
        }

        .con::after {
            content: '你好';
            display: block;
            width: 100%;
            height: 100%;
            transition: all ease .6s;
            transform-origin: bottom left;
            transform: rotate(90deg);
            background-color: black;
            text-align: center;
            line-height: 100px;
            font-size: 20px;
            color: white;
        }

        .con:hover::after {
            transform: rotate(0deg);
        }
    </style>
</head>

<body>
    <div class="box">
        <div class="con">
        </div>
    </div>
</body>

</html>
```

<img src="http://pic.tolie.biz/images/%E6%97%8B%E8%BD%AC%E6%95%88%E6%9E%9C%E5%9B%BE.gif" alt="旋转效果图" style="zoom:50%;" />



###### 2D转换综合写法

**注意**:

1. 同时使用多个转换，其格式为: transform: translate() rotate() scale()……等等,
2. 其*顺序会影响转换的效果*。( 先旋转会改变坐标轴方向)
3. `当我们同时有位移和其他属性的时候，记得要将位移放到最前`



##### CSS3动画

动画( animation )是CSS3中具有颠覆性的特征之一, 可`通过设置多个节点来精确控制一个或一组动画`
`常用来实现复杂的动画效果`。

> 相比较过渡，动画可以实现更多变化，更多控制，连续自动播放等效果。

###### 动画的基本使用

制作动画分为两步:

1. 定义动画

  用keyframes定义动画(类似定义类选择器)

  ```css
  @keyframes动画名称{
      0% {
          width: 100px;
      }
      100% {
          width: 200px;
  	}
  }
  ```

  >动画序列
  >
  >* 0% 是动画的开始, 100%是动画的完成。这样的规则就是动画序列。
  >* 在 @keyframes中规定某项CSS样式,就能创建由当前样式逐渐改为新样式的动画效果。
  >* 动画是使元素从一 种样式逐渐变化为另一种样式的效果。您可以改变任意多的样式任意多的次数。
  >* 请用百分比来规定变化发生的时间 ,或用关键词"from"和"to" ,等同于0%和100%。

2. 元素使用动画

```css
div {
    width: 200px; 
    height: 200px;
    background-color: aqua;
    margin: 100px auto;
    	/*调用动画
    	animation-name:动画名称;*/
    animation-name:move;
    	/*持续时间
    	animation-duration:持续时间;*/
    animation-duration:10s;
}

```



###### 动画序列

* 0% 是动画的开始，100%是动画的完成。这样的规则就是动画序列，里面的百分比代表时间的划分。
* 在 @keyframes中规定某项CSS样式，就能创建由当前样式逐渐改为新样式的动画效果。
* 动画是使元素从一种样式逐渐变化为另一种样式的效果。您可以改变`任意多的样式任意多的次数`。
* 请用百分比来规定变化发生的时间，或用关键词"from"和"to"，等同于0%和100%。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS3动画</title>
    <style>
        /* 定义动画 */
        @keyframes move {

            /* 开始状态 */
            0% {
                transform: translate(0, 0);
            }

            25% {
                transform: translate(500px, 0);
            }

            50% {
                transform: translate(500px, 500px);
            }

            75% {
                transform: translate(0, 500px);
            }

            /* 结束状态 */
            100% {
                transform: translate(0, 0);
            }
        }

        div {
            width: 100px;
            height: 100px;
            /* margin: 100px auto; */
            background-color: pink;
            /* 动画名称 */
            animation-name: move;
            /* 动画执行时间 */
            animation-duration: 10s;
        }
    </style>
</head>

<body>
    <div></div>
</body>

</html>
```



###### 动画的属性

| 属性                      | 描述                                                         |
| ------------------------- | ------------------------------------------------------------ |
| @keyframes                | 规定动画                                                     |
| animation                 | 所有动画属性的简写属性，除了animation-play-state属性。       |
| animation-name            | 规定@keyframes动画的名称。( `必须的`)                        |
| animation-duration        | 规定动画完成一个周期所花费的秒或毫秒 ，默认是0。( `必须的`)  |
| animation-timing-function | 规定动画的速度曲线，默认是"ease" 。                          |
| animation-delay           | 规定动画何时开始，默认是0。负值也是允许的。如果使用负值，则动画将开始播放，如同已播放 N 秒。 |
| animation-iteration-count | 规定动画被播放的次数，默认是1， 还有infinite                 |
| animation-direction       | 规定动画是否在下一周期逆向播放，默认"normal "，alternate是逆播放 |
| animation-play-state      | 规定动画是否正在运行或暂停。默认是"running"，还有"pause"。   |
| animation-fill-mode       | 规定动画结束后状态，保持forwards，回到起始backwards          |

```html
    <style>
        /* 定义动画 */
        @keyframes move {

            /* 开始状态 */
            0% {
                transform: translate(0, 0);
            }

            25% {
                transform: translate(500px, 0);
            }

            50% {
                transform: translate(500px, 500px);
            }

            75% {
                transform: translate(0, 500px);
            }

            /* 结束状态 */
            100% {
                transform: translate(0, 0);
            }
        }

        div {
            width: 100px;
            height: 100px;
            /* margin: 100px auto; */
            background-color: pink;
            /* 动画名称 */
            animation-name: move;
            /* 动画执行时间 */
            animation-duration: 8s;
            /*运动曲线*/
            animation-timing-function: ease;
            /*何时开始*/
            animation-delay: 1s;
            /* 重复次数  infinite无限循环*/
            animation-iteration-count: 1;
            /* 是否反方向播放 */
            animation-direction: alternate;
            /*动画结束后的状态默认的是backwards回到起始状态我们可以让他停留在结束状态backwards*/
            animation-fill-mode: backwards;
        }

        div:hover {
            /*鼠标经过div让这个div停止动画，鼠标离开就继续动画*/
            animation-play-state: paused;
        }
    </style>
```



动画的速度曲线

> animation-timing-function 属性可接受以下值：
>
> - ease - 指定从慢速开始，然后加快，然后缓慢结束的动画（`默认`）
> - linear - 规定从开始到结束的速度相同的动画;
> - ease-in - 规定慢速开始的动画;
> - ease-out - 规定慢速结束的动画;
> - ease-in-out - 指定开始和结束较慢的动画;
> - cubic-bezier(n,n,n,n) - 运行您在三次贝塞尔函数中定义自己的值;
> - steps(n) - 指定了时间函数中的间隔数量(步长)，分n步完成动画

```html
<style>
        /* 定义动画 */
        @keyframes move {
            /* 开始状态 */
            0% {
      
            }

            /* 结束状态 */
            100% {
                width: 1000px;
            }
        }

        div {
            width: 0px;
            height: 100px;
            /* margin: 100px auto; */
            background-color: pink;
            /* 动画名称 */
            animation-name: move;
            /* 动画执行时间 */
            animation-duration: 8s;
            /*运动曲线 steps(n) 分n步完成动画*/
            animation-timing-function: steps(10);

        }

        div:hover {
            /*鼠标经过div让这个div停止动画，鼠标离开就继续动画*/
            animation-play-state: paused;
        }
    </style>
```



###### 动画属性简写

> animation :动画名称持续时间运动曲线何时开始播放次数是否反方向动画起始或者结束的状态;

```css
/*animation: name duration timing-function delay iteration-count direction fill-mode;*/
animation: move 2s linear 0s 1 alternate forwards;
```

**注意**

* 简写属性里面不包含animation-play-state；
* 暂停动画: animation-play-state: puased; 经常和鼠标经过等其他配合使用；
* 想要动画走回来，而不是直接跳回来: animation-direction : alternate；
* 盒子动画结束后，停在结束位置: animation-fill-mode : forwards；



##### CSS3 3D转换

###### 三维坐标系

三维坐标系其实就是指立体空间,立体空间是由3个轴共同组成的。

* x轴:水平向右；注意: x右边是正值，左边是负值。
* y轴: 垂直向下；注意: y下面是正值，上面是负值。
* z轴:垂直屏幕；注意:往外面是正值，往里面是负值。



###### 3D位移: translate3d(x,y,z)

> * translform:translateX(100px) :仅仅在x轴上移动;
> * translform:translateY(100px) :仅仅在Y轴上移动;
> * translform:translateZ(100px) :仅仅在Z轴上移动(`注意:translateZ一般用px单位`需借助透视 );
> * transform:translate3d(x,y,z) :中x、y、z分别指要移动的轴的方向的距离;



###### 透视: perspective

> * 在2D平面产生近大远小视觉立体，但是只是效果二维的;
> * `如果想要在网页产生3D效果需要透视`(理解成3D物体投影在2D平面内)。
> * 模拟人类的视觉位置，可认为安排一只眼睛去看;
> * 透视我们也称为`视距`: 视距就是人的眼睛到屏幕的距离;
> * 距离视觉点越近的在电脑平面成像越大，越远成像越小;
> * `透视的单位是像素`;

**注意**

* `透视写在被观察元素的父盒子上面`。
* d：就是视距，视距就是一个距离人的眼睛到屏幕的距离。视距越小，元素的大小越大。
* z：就是z轴，物体距离屏幕的距离，轴越大(正值)我们看到的物体就越大。

<span style="color:red;">所以translateZ越大(正值)物体越大，透视越小物体越大。</span>

![透视](http://pic.tolie.biz/images/image-20220125231218852.png)



###### 3D旋转 rotate3d(x,y,z)

3D旋转指可以让元素在三维平面内沿着x轴， y轴，z轴或者`自定义轴`进行旋转。

**语法**

> * transform:rotateX(45deg) :沿着x轴正方向旋转45 deg
> * transform:rotateY(45deg) : 沿着y轴正方向旋转45 deg
> * transform:rotateZ(45deg) :沿着Z轴正方向旋转45 deg
> * transform:rotate3d(x,y,z,deg) :沿着自定义轴旋转deg为角度(了解即可)。xyz是表示旋转轴的矢量，标示你是否希望沿着该轴旋转，最后一个标示旋转的角度。

transform:rotate3d(1,0,0,45deg)就是沿着x轴旋转45 deg

transform:rotate3d(1,1,0,45deg)就是沿着对角线旋转45 deg

###### 确定元素旋转的方向

**左手准则**

* 左手的手拇指指向x轴的正方向；
* 其余手指的弯曲方向就是该元素沿着`轴旋转的正方向`；

![左手准则](http://pic.tolie.biz/images/202201261250698.png)



###### 3D呈现 transfrom-style**

用来控制子元素是否开启三维立体环境。`代码写给父级，但是影响的是子盒子`	

> transform-style: flat；子元素不开启3d立体空间（`默认的`）
> transform-style: preserve-3d; 子元素开启立体空间



#### 广义的HTML5

1. 广义的HTML5是HTML5本身+ CSS3 + JavaScript。
2. 这个集合有时称为HTML5和朋友，通常缩写为HTML5。
3. 虽然HTML5的一些特性仍然不被某些浏览器支持，但是它是一种发展趋势。



### 二十、网站制作流程

![网站制作流程](http://pic.tolie.biz/images/image-20220117180703240.png)



### 二十一、模块化开发

#### 模块化

所谓的模块化：将一个项目按照功能划分，一个功能一个模块，互不影响。模块化开发具有重复使用、更换方便等优点



#### 模块化开发

* 有些样式和结构在很多页面都会出现，比如页面头部和底部，大部分页面都有。此时，可以把这些结构和样式单独作为一个模块，然后重复使用，
* 这里最典型的应用就是`common.css`公共样式。写好一个样式 ，其余的页面用到这些相同的样式。

![模块化开发](http://pic.tolie.biz/images/image-20220117195438296.png)

> common.css公共样式里面包含版心宽度、清除浮动、页面文字颜色等公共样式。



### 二十二、网站favicon图标

favicon.ico 一般用于作为缩略的网站标志，它显示在浏览器的地址栏或者标签上。
目前主要的浏览器都支持favicon.ico图标。

1. 制作favicon图标

* 把图标切成png图片。
* 把png图片转换为ico图标，这需要借助于第三方转换网站，例如[比特虫]( http://www.bitbug.net/)

2. favicon图标放到网站根目录下

3. HTML页面引入favicon图标

* 在html 页面里面的&lt;head&lt;/head&gt;元素之间引入代码。

```html
<link rel="shortcut icon" href="favicon.ico" type="image/x-icon"/>
```



### 二十三、网站TDK三大标签SEO优化

**SEO** ( Search Engine Optimization )汉译为搜索引擎优化，是-种利用搜索引擎的规则提高网站在有关搜索引擎内自然排名的方式。

`SEO的目的是对网站进行深度的优化`，从而帮助网站获取免费的流量，进而在搜索引擎上提升网站的排名，提高网站的知名度。



页面必须有三个标签用来符合SEO优化

![TDK三大标签](http://pic.tolie.biz/images/image-20220117205739013.png)

#### title网站标题

title具有不可替代性，是我们内页的第一个重要标签，是搜索引嘴了解网页的入口和对网页主题归属的最佳判断点。

**建议**：`网站名(产品名) -网站的介绍( 尽量不要超过30个汉字)`

> *例如*:
>
> * 京东(JD.COM)- 综合网购首选正品低价、品质保障、配送及时、轻松购物!
> * 小米商城-小米5s、红米Note4、小米MIX. 小米笔记本官方网站



#### description网站说明

简要说明我们网站主要是做什么的。

我们提倡，description作为网站的总体业务和主题概括，多采用“我们.."、“我们提供.." 、"xxx网作为..”、“电话 :010.."之类语句。
**例如**:

> &lt;meta name= "description" content=“京东JD.COM-专业的综合网上购物商城，销售家电、数码通讯、电脑、
> 家居百货、服装服饰、母婴、图书、食品等数万个品牌优质商品.便捷、诚信的服务,为您提供愉悦的网上购物
> 体验!" /&gt;



#### keywords关键字

`keywords是页面关键词，是搜索引拿的关注点之一.`
keywords最好限制为6~ 8个关键词，关键词之间用英文逗号隔开，采用关键词1，关键词2的形式，而且关键词越靠前，权重越高。
**例如**:

> &lt;meta name= "keywords" content="网上购物,网上商城手机笔记本,电脑MP3,CD,VCD,DV,相机,数码配件,手表存储卡，京东" /&gt;



### 二十四、浏览器私有前缀

* -moz- :代表firefox浏览器私有属性
* -ms- :代表ie浏览器私有属性
* -webkit- :代表safari、chrome 私有属性
* -0- :代表Opera私有属性

#### 提倡的写法

> -moz-border-radius: 10px;
> -webkit-border-radius: 10px;
> -o-border-radius: 10px;
> border-radius: 10px;
