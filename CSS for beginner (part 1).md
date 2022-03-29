---
title: CSS for beginner (part 1)
date: 2021-12-03 18:20:47
summary: 
categories: 
  - Frond End

tags:
  - CSS
---
# CSS学习

* 好看的颜色

|   颜色   |                      |
| :------: | -------------------- |
| 波尔多红 | **rgb(76,0,9)**      |
| 勃艮第红 | **rgb(128,0,32)**    |
|  提香红  | **rgb(176,89,35)**   |
|  苋菜紫  | **rgb(142,41,97)**   |
| 木乃伊棕 | **rgb(143,75,40)**   |
| 普鲁士蓝 | **rgb(0,49,83)**     |
|  邦迪蓝  | **rgb(0,149,182)**   |
| 卡布里蓝 | **rgb(26,85,153)**   |
| 蒂芙尼蓝 | **rgb(129,216,208)** |

### 一、CSS初识

CSS也称为层叠样式表，主要用于设置HTML页面的各种外观显示样式；

CSS以HTML为基础，提供了丰富的功能，如字体、颜色、背景的控制等，而且还可以根据不同的浏览器设置不同的样式；

CSS效果优先于HTML效果，即CSS效果可以覆盖HTML效果。

### 二、CSS的样式规则

> 选择器 + { 属性:值;属性:值;属性:值 }

1. 选择器用于指定CSS样式作用的HTML标签，花括号内是对该对象设置的具体样式；
2. 属性和属性值以“键值对”的形式出现；
3. 属性是对指定对象设置样式的属性，例如字体大小，文本颜色等；
4. 属性和属性值之间用英文的冒号“ : ”连接；
5. 多个键值对之间用英文的分号“ ; ”分割；

### 三、CSS的字体样式属性

#### font-size	字号大小

（相对长度单位使用较多，故没写绝对长度单位

| 相对长度单位 |              说明              |
| :----------: | :----------------------------: |
|      em      | 相对于当前对象内文本的字体尺寸 |
|    px **     |         像素，最为常用         |

#### font-family   字体

* 注意： 

可以指定多个字体，中间用英文逗号隔开；

表示如果浏览器不支持第一个字体，会自动尝试下一个，直到找到合适的字体。

* 小技巧：

1. 现今网页中普遍使用的字号为14px，普遍使用的字体为宋体和微软雅黑；
2. 尽量使用偶数的字号，一些老浏览器支持奇数会出现bug；
3. 各种字体之间必须用英文逗号隔开；
4. ==中文字体需要加英文状态下的引号==，比如 font-family:"宋体"；英文字体一般不需要加引号。
5. ==当需要设置英文字体时，英文字体名必须位于中文字体名之前==；
6. 如果字体名中包含空格，#，$等符号，则该字体必须加上英文状态下的单引号或双引号，如font-family:"Times New Roman";
7. 尽量使用系统字体，保证任何用户的浏览器都可以正常显示；

#### CSS Unicode字体

在CSS中设置字体名称，直接写中文是可以的，但在文件编码不匹配的时候会产生乱码的错误，比如xp系统就不支持微软雅黑的中文字体

* 解决方案：

一、使用英文字体来代替，比如font-family:"Microsoft Yahei";

二、在CSS中直接使用Unicode编码来写字体名称。使用Unicode编码写中文字体名称，浏览器是可以正确解析的，比如font-family:"\5FAE\8F6F\96C5\9ED1";表示设置字体为微软雅黑；

#### font-weight   字号加粗

提倡使用数字来表示字体粗细；

|     属性值      | 说明                                                         |
| :-------------: | ------------------------------------------------------------ |
|     normal      | 正常的字体，==相当于数字的400==                              |
|      bold       | 粗体，==相当于数字的700==                                    |
|     bolder      | 定义比继承值更重的值                                         |
|     lighter     | 定义比继承值更轻的值                                         |
| &lt;integer&gt; | 用数字表示文本字体的粗细，取值范围：100\|200\|300\|……\|800\|900 |

#### font-style    字体风格

可以使用HTML中的&lt; i &gt;和&lt; em &gt;标签，CSS中使用font-style；

| 属性值  | 说明             |
| :-----: | ---------------- |
| normal  | 正常的字体       |
| italic  | 设置为倾斜的字体 |
| oblique | ==不经常使用==   |

#### font  综合设置字体样式 *

* 基本语法格式

>选择器 + { font: font-style font-weight font-size/line-weight font-family; }

==使用font属性时，必须按照上面的语法格式中的顺序书写，不能更换顺序，各属性之间用空格隔开；==

* 注意：

其中不需要设置的属性可以忽略（取默认值），但必须保留font-size和font-family属性，否则font属性不起作用。

### 四、类选择器 **

#### 标签选择器

可以快速为页面中的同一标签设置样式，但也是他的缺点，即不能设计差异化的样式。

```css
/*格式：标签名  +  {属性:属性值;属性:属性值;属性:属性值;}*/
p {
    font: italic 600 20px "宋体";
}
```

```html
<!-- a标签 + ”# + id“实现页面内跳转-->
<a href="#wushi">武师时期</a>
<br>
<a href="#jiahe">嘉禾时期</a>
<br>
<a href="#luowei">罗威时期</a>
```

#### 类选择器

* 类命名小技巧

1. 长名称或词组可以使用短横线来为选择器命名；
2. 不建议使用下划线“_”来命名css选择器；（避免兼容性问题，输入更加方便
3. 不要使用纯数字或者中文命名，最好使用英文字母表示；

```css
<!-- 格式：.类名  +  {属性:属性值;属性:属性值;属性:属性值;} -->
span {
    font-size: 100px;
}
.blue {
    color: blue;
}
.orange {
    color: orange;
}
.yellow {
    color: yellow;
}
.green {
    color: green;
}
```

#### 多类名选择器

`一个对象可以有多个类名，中间用空格隔开，使得类名选择器使用更加灵活`；

* 注意

`如果上下样式显示效果有冲突，此时的显示效果跟HTML中元素的类名先后顺序没有关系`，受CSS样式的书写的上下顺序影响。

```html
<style> 
    .G {
        font-style: italic;
    }

    .blue {
        color: blue;
    }
</style>

<body>
    <span class="blue G">G</span>
</body>
```

#### id选择器

```css
<!-- 格式：#id名  +  {属性:属性值;属性:属性值;属性:属性值;} -->
#font-s {
    font-size: 100px;
}
```

* id选择器和类选择器的区别

1. 在一个文件中id名称不可以重复，类似于身份证号；
2. 在一个文件中类名可以重复，类似于姓名，比如张伟；
3. id选择器前面是“#”，类选择器前面是“.”

#### 通配符选择器

“ * ”代表页面中的所有元素

```css
<!-- 格式：*  +  {属性:属性值;属性:属性值;属性:属性值;} -->
* {
    color：red；    
}
```

#### 伪类选择器 *

##### 1. 链接伪类选择器

| 链接伪类选择器（主要针对a标签） | 含义                                 |
| :------------------------------ | :----------------------------------- |
| :link                           | 未访问的链接                         |
| :visited                        | 已访问的链接                         |
| :hover                          | 鼠标移动到链接上                     |
| :active                         | 选定的链接，即点击但还没有松开的状态 |

```css
/*未访问的链接*/
a:link {
    font-size:18px;
    color: black;
}
/*已访问的链接*/
a:visited {
    font-size:18px;
    color: gray;
}
/*鼠标放在链接上*/
a:hover {
    font-size:18px;
    color: blue;
}
/*点击了链接还没有松开*/
a:active {
    font-size:18px;
    color: red;
}
```

```顺序不能随便调整，必须按照如上的顺序，简记为LV好（LV hao），所以顺序是l-v-h-a```

* 简写链接伪类选择器

```css
a {
    font-size:18px;
}
/*未访问的链接*/
a:link {
    color: black;
}
/*已访问的链接*/
a:visited {
    color: gray;
}
/*鼠标放在链接上*/
a:hover {
    color: blue;
}
/*点击了链接还没有松开*/
a:active {
    color: red;
}
```

##### 2. 结构(位置)伪类选择器(CSS 3的新特性)

[CSS3 - :nth-child()选择前几个元素](https://blog.csdn.net/idomyway/article/details/93921248?spm=1001.2101.3001.6650.5&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7Edefault-5.no_search_link)

| 结构(位置)伪类选择器 | 含义                                                         |
| -------------------- | ------------------------------------------------------------ |
| :first-child         | 选取属于父元素的首个子元素的指定选择器                       |
| :last-child          | 选取属于父元素的最后一个子元素的指定选择器                   |
| **:nth-child(n)**    | 选取属于父元素的第n个子元素，`不论元素的类型`<br>n可以是`数字`，`关键字`和`公式`。<br>如果n是公式，则从0开始计算,但是第0个元素或者超出了元素的个数会被忽略 |
| :nth-last-child(n)   | 选取属于父元素的```倒数```第n个子元素，`不论元素的类型`      |
| :first-child         | 冒号前是选择器，选取与此选择器同一类的元素的第一个           |
| :last-child          | 冒号前是选择器，选取与此选择器同一类的元素的最后一个         |
| :nth-of-type()       | 冒号前是选择器，`选取与此选择器同一类的元素`；<br>n可以是`数字`，`关键字`和`公式`。<br/>如果n是公式，则从0开始计算,但是第0个元素或者超出了元素的个数会被忽略 |

```css
/* 选择第一个孩子 */
li:first-child {
    color: rgb(76, 0, 9);
}

/* 选择最后一个孩子 */
li:last-child {
    color: rgb(129, 216, 208);
}
```

```css
/* 选择偶数孩子 */
li:nth-child(even) {
    color: rgb(0, 49, 83);
}

li:nth-child(2n) {
    color: rgb(143, 75, 40);
}

/* 选择奇数孩子 */
li:nth-child(odd) {
    color: rgb(143, 75, 40);
}

li:nth-child(2n-1) {
    color: rgb(143, 75, 40);
}

/* 选择3的倍数孩子 */
li:nth-child(3n) {
    color: rgb(143, 75, 40);
}
```

```css
/* 选择倒数第3个孩子 */
li:nth-last-child(3) {
    color: rgb(0, 49, 83);
}

/* 选择倒数的奇数孩子，即正数的偶数孩子 */
li:nth-last-child(odd) {
    color: red;
}
/*其他同理*/
```

```css
div.message:nth-of-type(-n+2) {
border-bottom: 1px #999;
}
/*选取div.message 的前两个元素*/
```



```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<style type="text/css">
		li:first-child{
			color: green; /*第一个绿色*/
		}
		li:nth-child(2){
			color: blue; /*第二个蓝色*/
		}
		li:last-child{
			color: red; /*倒数第二个橙色*/
		}
		li:nth-last-child(2){
			color: orange; /*最后一个红色*/
		}
	</style>
</head>
<body>
	<ul>
		<li>第一个绿色</li>
		<li>第二个蓝色</li>
		<li>第三个默认色</li>
		<li>第四个默认色</li>
		<li>倒数第二个橙色</li>		
		<li>最后一个红色</li>		
	</ul>	
</body>
</html>
```

![网页效果](http://pic.tolie.biz/images/image-20220106140841616.png)

###### nth-child 和 nth-of-type 的区别

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        /* nth-child 会把所有的盒子都排列序号*/
        /*执行的时候首先看 :nth-child(1) 之后回去看前面div */
        /* 所以都不会添加红色背景效果 */
        section div:nth-child(1) {
            background-color: red;
        }

        /* nth-of-type 会把指定元素的盒f排列序号*/
        /*执行的时候首先看div指定的元素 之后回去看:nth-of-type(1) 第几个孩子*/
        /* 所以这里的熊大会添加蓝色背景颜色效果 */
        section div:nth-of-type(1) {
            background-color: blue;
        }
    </style>
</head>

<body>
    <ul>
    </ul>
    <!-- 区别-->
    <section>
        <p>光头强</p>
        <div> 熊大</div>
        <div>熊二</div>
    </section>

</body>

</html>
```



##### 3. 目标伪类选择器

:target 目标伪类选择器：用于选取当前活动的目标元素；

```css
:target {
    color: red;
    font-family: 'Courier New', Courier, monospace;
}
```

##### 4.focus伪类选择器

`:focus伪类选择器`用于选取获得焦点的表单元素。

焦点就是光标，一般情况&lt;input&gt;类表单元素才能获取，因此`这个选择器也主要针对于表单元素`来说。

```css
input:focus {
background-color: yellow;
}
```



### 五、CSS外观属性

#### color 	文本颜色

color属性用于定义文本颜色，取值方式主要有三种：

1. 预定义颜色值，如red，green等；
2. 十六进制，如#FF0000，#29D794等；```十六进制是最常用的定义颜色方式```
3. RGB代码，如rgb(143, 75, 40)，等。

* 注意：

若是使用RGB代码的百分比颜色，取值为0时也不能省略百分号，必须写为0%。

#### line-height	 行间距

line-height属性用于设置行间距，即行与行之间的距离，即字符的垂直距离；

常用的属性单位有三种，分别是像素px，相对值em和百分比%，使用最多的是像素；

一般情况下，行距比字号大7-8像素即可；

![行间距](http://pic.tolie.biz/images/image-20220108155423729.png)

#### text-align 	水平对齐方式

text-align用于设置文本的水平对齐方式，相当于html中的align属性

可用属性有三种：

1. left：左对齐，即默认对齐方式；
2. right：右对齐；
3. center：居中对齐；

#### line-height = height 单行文字垂直居中

CSS没有给我们提供文字垂直居中的代码.这里我们可以使用一个小技巧来实现。

> 解决方案：`让文字的行高等于盒子的高度就可以让文字在当前盒子内垂直居中`。

实现原理：行高的上空隙和下空隙把文字挤到中间了。是如果行高小于盒子高度文字会偏上，如果行高大于盒子高度，则文字偏下。

####  text-decoration  	装饰文本

text-decoration属性规定添加到文本的修饰。可以给文本添加下划线、删除线、上划线等。

| 可能的值     | 描述                                            |
| :----------- | :---------------------------------------------- |
| none         | 默认。定义标准的文本。                          |
| underline    | 定义文本下的一条线。                            |
| overline     | 定义文本上的一条线。                            |
| line-through | 定义穿过文本下的一条线。                        |
| blink        | 定义闪烁的文本。                                |
| inherit      | 规定应该从父元素继承 text-decoration 属性的值。 |

#### text-indent  	首行缩进

text-indent属性用于设置文本的首行缩进，允许使用负值，```建议使用em作为单位```；

1 em就是一个字的宽度，如果是汉字则1 em就是一个汉字的宽度；

```css
/*设置本页面中所有段落首行缩进两个字符*/
p{
    text-indent：2em；
}
```

#### letter-spacing 	字间距

letter-spacing用于设置字符与字符之间的距离，其属性值可以为不同单位的数值，```允许使用负值```，默认值为normal；

#### word-spacing 	单词间距

word-spacing用于设置英文单词之间的间距，```对中文字符无效```。其属性值可以为不同单位的数值，```允许使用负值```，默认值为normal；

* 注意

letter-spacing 和word-spacing均可以对英文字符进行设置；

不同的是，前者是英文字母之间的距离，后者是英文单词之间的距离；

#### word-break	自动换行

属性值有以下几种

1. normal：使用浏览器默认的换行规则；
2. break-all：允许在单词内换行；
3. keep-all：只能在半角空格或者连字短符的位置换行；

#### 颜色半透明(CSS 3)

格式：```color: rgba(r, g, b, a);```

a 代表透明度，取值范围为[0~1]，0为全透明，1为全不透明；

```css
/*给rgb(0, 49, 83)设置为0.1的半透明;*/
li:nth-last-child(3) {
    color: rgba(0, 49, 83, .1);
}
```

#### 文字阴影(CSS 3)

> /* 使 用 格 式 */
> 选择器 {
> text-shadow:水平位置 垂直位置 模糊距离 阴影颜色
> }

|  属性值  | 描述                                       |
| :------: | ------------------------------------------ |
| h-shadow | ```必需```；水平的阴影位置。```允许负值``` |
| v-shadow | ```必需```；垂直的阴影位置。```允许负值``` |
|   blur   | ```选填```；模糊的距离                     |
|  color   | ```选填```；阴影的颜色                     |

### 六、引入CSS样式表

#### 内部样式表

* 内嵌式是将CSS代码集中在HTML文档的head头部标签中，并用style标签包裹；

* 基本格式

```html
<!-- <style>
        选择器 {
            属性名: 属性值;
        }
    </style>-->
<style>
    label {
        font: italic, 400, 40px, "黑体";
    }
</style>
```

#### 行内样式表

* 行内样式又称内联样式。是通过HTML中标签的style属性来设置元素的样式；

* 基本格式

```html
 <!-- <标签名 style="属性名: 属性值;">内容</标签名>	-->
 <label style="color: chartreuse;">名称</label>
```

#### 外部样式表

* 外部样式是将CSS代码单独写在一个.css文件中，通过HTML头部中利用 link 标签引入； 
* 基本格式

```html
 <!-- <head>
  <link rel="stylesheet" type="text/CSS" href="css文件路径" />
</head>	-->
<head>
  <link rel="stylesheet" type="text/CSS" href="css/iconfont.css" />
</head>
```

* 注意

1. link是个单标签；
2. 必须指定link标签的三个属性
   1. herf：定义所连接外部文档的URL，可以是相对路径，也可以是绝对路径；
   2. type：定义所链接文档的类型，这里type="text/CSS"，表明链接的外部文件是CSS样式表；
   3. rel：定义当前文档和链接文档之间的关系，这里rel="stylesheet"，表明连接的文档是个样式表文件。

### 七、标签显示模式

#### 块级元素

* 每个块级元素通常都会独自占据一整行或多整行，可以对其设置宽度，高度，对齐等属性，常用于网页布局和结构的搭建；
* 常见的块级元素，div是最典型的块级元素。

```html
    <h1></h1>~~<h6></h6>		<div></div>
    <ul></ul>					<ol></ol>
    <li></li>
```

* 特点

1. 总是占据一整行；
2. `高度，行高，外边距等都可以控制`；
3. 宽度默认是容器的100%；
4. 可以容纳其他的内联元素和其他块级元素；

#### 行内元素

* 行内元素又叫内联元素，不占有独立的区域，仅仅依靠自身的字体大小和图像尺寸支撑结构。
* ```一般不能设置宽度、高度、对齐等属性```,默认宽度就是本身内容的宽度；
* 水平方向的padding和margin可以设置，垂直方向设置无效；
* 常用于控制页面中文本的样式；
* ```行内元素只能容纳文本或其他行内元素```；（a标签特殊）
* 常见的块级元素，span是典型的块级元素。

```html
    <a></a>					<span></span>
    <strong></strong>		<b></b>
    <em></em>				<i></i>
```

* 注意

1. 只有文字才能组成段落，因此```p标签中不能放块级元素，同理还有h1~h6等标签```；
2. 链接里不能在放链接；

#### 行内块元素

行内块元素有几个特殊的标签：&lt;img   /&gt;、&lt;input   /&gt;、&lt;td &gt;，对他们就可以设置宽高和对齐属性；

有些资料中会称他们为行内块元素。

> 行内块元素的特点：
>
> 1. 与相邻行内元素/行内块元素在一行上，但是之间会有空白间隙；
> 2. 默认宽度就是他本身内容的宽度；
> 3. `高度，行高，外边距及内边距都可以控制`。

#### 显示模式转换 *

| 转换类型                  | 代码                 |
| ------------------------- | -------------------- |
| 块级元素转行内元素        | display:inline;      |
| 行内元素转块级元素        | display:block;       |
| 块级/行内元素转行内块元素 | display:inline-block |

```css
div {
    color: #3c3c3c;
    background-color: chartreuse;
    font: italic 600 18px "宋体";
    display: inline;/*块级元素转为行内元素显示模式*/
}
span {
    color: #3c3c3c;
    background-color: chartreuse;
    font: italic 600 18px "宋体";
    display: block;/*行内元素转换为块级元素显示模式*/
}
a {
    height: 100px;
    width: 100px;
    background: red;
    display: inline-block;/*行内元素转换为行内块级元素显示模式*/
}
```

### 八、CSS复合选择器

#### 交集选择器

交集选择器由两个选择器构成，其中一个为标签选择器，第二个为class选择器，

```两个选择器之间不能有空格```，如p.red{};

```css
div {
    /*所有的div标签进行设置*/
    color: #3c3c3c;
    background-color: chartreuse;
    font: italic 600 18px "宋体";
    display: inline;
}
div.i {
    /*div标签中class为i的标签进行设置*/
    font-size: 40px;
}
```

#### 并集选择器

并集选择器是各个选择器通过“逗号”链接而成的，任何形式的选择器（包括标签选择器、class选择器、id选择器等）都可以作为并集选择器的一部分。

`如果某些选择器定义的样式完全相同或部分相同，就可以利用并集选择器为他们定义相同的样式`。

```css
a,
#love,
.i {
    color: #3c3c3c;
    background-color: chartreuse;
    font: italic 600 40px "宋体";
}
div {
    display: inline;
}
span {
    display: block;
}
a {
    display: block;
}
```

#### 后代选择器

后代选择器又叫包含选择器，`用来选择元素和元素组的所有后代`；

当标签发生嵌套时，内层标签就成为外层标签的后代；

其写法是```外层标签写在前面，内层标签写在后面，中间用空格分开```；

```html
<style>
    .mht p {
        color: yellowgreen;
    }
    p a {
        color: cyan;
    }
</style>
<body>
    <p>企鹅</p>
    <div class="mht">
        <P>王者荣耀<a href="#">华腾马</a></P>
    </div>
</body>
```



#### 子元素选择器

```子元素选择器只能选择作为某元素的最近一级子元素。```;

其写法是把父级元素写在前面，子级标签写在后面，中间用一个“&gt;”连接；

> 元素2必须是亲儿子，`其孙子、重孙之类都不归他管`，你也可以叫他儿子选择器。



#### 属性选择器

`属性选择器可以根据元素特定属性的来选择元素`。这样就可以不用借助于类或者id选择器。

| 选择器                                                  | 描述                                                         |
| :------------------------------------------------------ | :----------------------------------------------------------- |
| E[attribute]                                            | 用于选取带有指定属性的E元素。                                |
| E[*attribute*=value]<span style = 'color:red'>**</span> | 用于选取带有指定属性和值的E元素。                            |
| E[attribute~=value]                                     | 用于选取属性值中包含指定词汇的E元素。                        |
| E[attribute\|=value]                                    | 用于选取带有以指定值开头的属性值的E元素，该值必须是整个单词。 |
| E[attribute^=value]                                     | 匹配属性值以指定值开头的E元素。                              |
| E[*attribute*$=value]                                   | 匹配属性值以指定值结尾的E元素。                              |
| E[attribute*=value]                                     | 匹配属性值中包含指定值的E元素。                              |



#### 伪元素选择器(CSS 3)**

**伪元素选择器**可以帮助我们`利用CSS创建新标签元素`，而不需要HTML标签，从而简化HTML结构。

> /* CSS3语法 **/
> element::before {样式}
>
> /* (单冒号) CSS2过时语法(仅用来支持IE8) */
> element:before { 样式}
>
> /*在每一个p元索前插入内容**/
> p::before { content: "Hello world!"; }

| 伪元素         | 说明                                                         |
| -------------- | ------------------------------------------------------------ |
| ::first-line   | 可改变段落首行文字的样式。                                   |
| ::first-letter | 会选中`块级元素`第一行的第一个字母，并且文字所处的行之前没有其他内容（如图片和内联的表格） 。 |
| ::after        | 来创建一个伪元素，作为已选中元素的后面。                     |
| ::before       | 来创建一个伪元素，作为已选中元素的前面。                     |

**注意**:

* before 和after创建一个元素，但是属于`行内元素`；
* `img、input和其他的单标签是没有after和before伪元素的`，因为单标签本身不能有子元素，所以不能通过input::before来写一些图标之类的内容，即使写了样式也不会生效；
* 新创建的这个元素在文档树中是找不到的，所以我们称为伪元素；
* 语法：element::before { }；
* `before和after必须有content属性`；
* before 在`父元素`（`即此 element`）内容的前面创建元素，after 在父元素内容的后面插入元素，可以理解为为父元素创建了一个孩子；
* `伪元素选择器`和`标签选择器`一样，`权重为1`；



```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>伪元素选择器</title>
  <style>
    div {
      width: 200px;
      height: 200px;
      background-color: pink;
    }

    div::before {
      /*这个content是必须要写的*/
      content: '我';

      /* 这里新生成的伪元素是行内元素
      所以这里的宽高不起作用 */
      width: 100px;
      height: 20px;
      border: 1px solid black;
    }

    div::after {
      content: '小猪佩奇';
    }
  </style>
</head>

<body>
  <div>是</div>
</body>

</html>
```

![显示效果](http://pic.tolie.biz/images/image-20220116212500358.png)

### 九、Emment语法

#### 快速生成HTML结构语法

1. 生成标签直接输入标签名按tab键即可比如div 然后tab键，就可以生成&lt;div&gt; &lt;/div&gt;
2. 如果想要生成多个相同标签加上*就可以了比如 div * 3 就可以快速生成3个div
3. 如果有父子级关系的标金,可以用 > 比如 ul >  li 就可以了
4. 如果有兄弟关系的标签,用 + 就可以了比如div+p
5. 如果生成带有类名或者id名字的，直接写.demo或者#two 再按 tab 键就可以了
6. 如果生成的div 类名是有顺序的,可以用自增符号$
7. 如果想要在生成的标签内部写内容可以用 { } 表示

#### 快速生成CSS样式语法

* 简写，全部使用首字母，比如w200就是width：200px。

### 十、CSS的背景

通过CSS背景属性,可以给页面元素添加背景样式。背景属性可以设置背景颜色、背景图片、背景平铺、背景图片位置、背景图像固定等。

#### 背景颜色

**background-color**

#### 背景颜色半透明（CSS3）

> background: rgba(0, 0，0, 0.3) ;



#### 背景图片

**background-image**属性描述了元素的背景图像。实际开发常见于logo或者一些装饰性的小图片或者是超大的背景图片，`优点是非常便于控制位置`(精灵图也是一种运用场景)。

> background- image: none | url(ur1)

#### 背景平铺

如果需要在HTML页面上对背景图像进行平铺,可以使用**background-repeat**属性。

> background-repeat: repeat | no- repeat | repeat-xI repeat- y

可能的值：

* repeat : 背景图像在纵向和横向上平铺
* no-repeat:背景图像不平铺
* repeat-x:背景图像在横向上平铺
* repeat-y:背景图像在纵向平铺

#### 背景图片位置

利用**background- position**属性可以改变图片在背景中的位置。

> background- -position: x  y;

参数代表的意思是: x坐标和y坐标。可以使用`方位名词`或者`精确单位`

| 参数值   | 说明                                                   |
| -------- | ------------------------------------------------------ |
| length   | 百分数、由浮点数字和单位标识符组成的长度值             |
| position | top 、 center、 bottom、left、 center 、 right方位名词 |

1. 参数是方位名词

* 如果指定的两个值都是方位名词，则`两个值前后顺序无关`，比如left top和top left效果一致；
* 如果只指定了一个方位名词，另一个值省略，则第二个值默认居中对齐；

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>超大背景图片</title>
  <style>
    body {
      background: url(img/bg-wzry.jpg) no-repeat top center;
    }
  </style>
</head>

<body>

</body>

</html>
```

2.参数是精确单位

* 如果参数值是精确坐标，那么`第一个肯定是x坐标`， `第二个一定是y坐标`；
* `如果只指定一个数值，那该数值一定是x坐标`，另一个默认垂直居中；

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>背景图片位置</title>
  <style>
    div {
      width: 118px;
      height: 41px;
      background-image: url(img/title_sprite.png);
      background-position: -30px 5px;
      background-repeat: no-repeat;
      /* background-color: pink; */
    }

    h3 {
        /* 上下居中，左右位置，显出背景图 */
      padding: 12px 0px 7px 28px;
        /* 取消字体加粗 */
      font-weight: normal;
      font-size: 14px;
      /* 为什么h3的背景颜色会挡住自己的背景图片，而div的不会 */
      /* background-color: rgb(226, 223, 224); */
    }
  </style>
</head>

<body>
  <div>
    <h3>成长守护平台</h3>
  </div>
</body>

</html>
```

3.参数是混合单位

* 如果指定的两个值是精确单位和方位名词混合使用，则`第一个值是x 坐标`，`第二个值是y坐标`。

```css
background-posion：20px center；
```

#### 背景图像固定(背景附着)

**background-attachment **属性设置背景图像是否固定或者随着页面的其余部分滚动。

background-attachment后期可以`制作视差滚动的效果`。

| 可能的值  | 说明                                                         |
| --------- | ------------------------------------------------------------ |
| **fixed** | 此关键属性值表示`背景相对于视口固定`。即使一个元素拥有滚动机制，`背景也不会随着元素的内容滚动`。 |
| **local** | 此关键属性值表示`背景相对于元素的内容固定`。如果一个元素拥有滚动机制，背景将会随着元素的内容滚动， 并且背景的绘制区域和定位区域是相对于可滚动的区域而不是包含他们的边框。 |
| scroll    | **默认**，此关键属性值表示`背景相对于元素本身固定`， `而不是随着它的内容滚动`（对元素边框是有效的）。 |

#### 背景属性复合写法

**background**

### 十一、CSS的三大特性

#### 层叠性

`相同选择器给设置相同的样式`，此时`一个样式就会覆盖(层叠)另一个冲突的样式`。层叠性主要解决样式冲突的问题。

> **层叠性原则:**
>
> * 样式冲突遵循的原则是`就近原则`，哪个样式离结构近，就执行哪个样式
> * 样式不冲突，不会层叠

#### 继承性

CSS中的继承：子标签会继承父标签的`某些样式`，`如文本、颜色和字号`。简单的理解就是：`子承父业`。

恰当地使用继承可以简化代码，降低CSS样式的复杂性；

子元素可以继承父元素的样式（ text- , font- , line- 这些元素开头的可以继承，以及color属性）

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>超大背景图片</title>
  <style>
    body {
      background: url(img/bg-wzry.jpg) no-repeat top center;
      /* 背景固定效果 */
      /* background-attachment: scroll; */
      background-attachment: fixed;
      color: #fff;
      font-size: 20px;
    }

  </style>
</head>

<body>
  <div>
    <!-- p从body标签继承了字体颜色、字体大小的属性 -->
    <p>NEUQ</p>
    <p>NEUQ</p>
    <p>NEUQ</p>
    <p>NEUQ</p>
    <p>NEUQ</p>
  </div>
</body>

</html>
```

##### 行高的继承

`行高的设置可以跟单位也可以不跟单位`

```css
 body {
     font: 12px/1.5 'Microsoft YaHei';
}
```

* 如果子元素没有设置行高，则会继承父元素的行高为1.5
* 此时子元素的行高是：当前子元素的 文字大小 *  1.5 

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>小琉璃</title>
    <style>
        body {
            background: url(img/bg-wzry.jpg) no-repeat top center;
            /* 背景固定效果 */
            /* background-attachment: scroll; */
            background-attachment: fixed;
            color: #fff;
            font: 12px/1.5 'Microsoft YaHei';
        }

        p {
            /* p从body继承了行高为1.5 */
            /* 
            	如果子元素没有设置行高 ,则会继承父元素的行高为1.5
            	此时子元素的行高是:当前子元素的文字大小* 1.5 
            */
            font-size: 18px;
        }
    </style>
</head>

<body>
    <div>
        <!-- p从body标签继承了字体颜色、字体大小的属性 -->
        <p>NEUQ</p>
        <p>NEUQ</p>
        <p>NEUQ</p>
        <p>NEUQ</p>
        <p>NEUQ</p>
    </div>
</body>

</html>

```

#### 优先级

当同一个元索指定多个选择器，就会有优先级的产生。

> 优先级原则
>
> * 选择器相同，则执行层叠性；
> * 选择器不同,则根据选择器权盟执行；

| 选择器               | 权重    |
| -------------------- | ------- |
| 继承或者 *           | 0,0,0,0 |
| 元素选择器           | 0,0,0,1 |
| 类选择器，伪类选择器 | 0,0,1,0 |
| `ID`选择器           | 0,1,0,0 |
| 行内样式 style=""    | 1,0,0,0 |
| ! important 重要的   | 无穷大  |

![specifishity chart](https://specifishity.com/specifishity.png)

> 优先级注意点:
>
> 1. 权重是有4组数字组成,但是`不会有进位`。
> 2. 可以理解为类选择器永远大于元索选择器id选择器永远大于类选择器，以此类推..
> 3. `等级判断从左向右，如果某一位数值相同，则判断下一位数值`。
> 4. *可以简单记忆法：通配符和继承权重为0，标签选择器为1，类(伪类)选择器为10， id选择器100，行内样式表为1000， !important无穷大。*
> 5. `继承的权重是0`，如果该元素没有直接选中，`不管父元素权重多高，元素得到的权重都是0`。

```css
/*父亲的权重是100 */
#father {
	color: red!important;
}
/* p继承的权重为0 */
p{
	color: pink;
}
/* 最终的颜色仍然为粉色 */
```

##### 权重叠加

`如果是复合选择器，则会有权重叠加，需要计算权重。`

```css
/*复合选择器会有权重叠加的问题*/
	/*ul li权重
    0,0,0,1 + 0,0,0,1 = 0,0,0,2 */
ul li{
	color :green;
}
/* li的权重是0,0,0,1 */
li {
	color: red; 
}
/* 最终的显示为红色 */
```

### 十二、盒子模型

#### 盒子模型( Box Model )组成

所谓盒子模型：就是把HTML页面中的布元素看作是一个矩形的盒子，也就是一个盛装内容的容器。

CSS盒子模型本质上是一个盒子，,封装周围的HTML元素，它包括：边框、外边距、内边距、和实际内容。

![盒子模型](http://pic.tolie.biz/images/image-20220109114115792.png)

![盒子模型](http://pic.tolie.biz/images/image-20220109114205565.png)

##### 1.边框（border）

border可以设置元素的边框。`边框有三部分组成：边框宽度(粗细)、边框样式、边框颜色`；

`边框会额外增加盒子的实际大小`。因此我们有两种方案解决:

1. 测量盒子大小的时候，不边框；
2. 如果测量的时候包含了边框，则需要width/height减边框宽度。

###### border-width

 **border-width** 属性可以设置盒子模型的边框宽度。

```css
* 用法一：明确指定宽度值 */
/* 当给定一个宽度时，该宽度作用于选定元素的所有边框 */
border-width: 5px;
/* 当给定两个宽度时，该宽度分别依次作用于选定元素的横边与纵边 */
border-width: 2px 1.5em;
/* 当给定三个宽度时，该宽度分别依次作用于选定元素的上横边、纵边、下横边 */
border-width: 1px 2em 1.5cm;
/* 当给定四个宽度时，该宽度分别依次作用于选定元素的上横边、右纵边、下横边、左纵边 （即按顺时针依次作用） */
border-width: 1px 2em 0 4rem;

/* 用法二：使用全局关键字 */
/* 可以使用的全局关键字有：inherit(继承),initial（初始值）,unset（不设置） */
border-width: inherit;

/* 用法三：使用作用于 border-width 的关键字 */
border-width: thin;
border-width: medium;
border-width: thick;
```

###### border-style

**border-style** 是一个 CSS的简写属性，用来设定元素所有边框的样式。

> **注意：**`border-style` 默认值是 `none`，这意味着如果只修改 [`border-width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-width) 和 [`border-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-color) 是不会出现边框的。

```css
/* Apply to all four sides */
border-style: dashed;

/* horizontal | vertical */
border-style: dotted solid;

/* top | horizontal | bottom */
border-style: hidden double dashed;

/* top | right | bottom | left */
border-style: none solid dotted dashed;
```

|        |                                                              |
| ------ | ------------------------------------------------------------ |
| none   | 和关键字 `hidden` 类似，不显示边框。在这种情况下，如果没有设定背景图片，[`border-width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-width) 计算后的值将是 `0`，即使先前已经指定过它的值。在单元格边框重叠情况下，`none` 值优先级最低，意味着如果存在其他的重叠边框，则会显示为那个边框。 |
| hidden | 和关键字 `none` 类似，不显示边框。在这种情况下，如果没有设定背景图片，[`border-width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-width) 计算后的值将是 `0`，即使先前已经指定过它的值。在单元格边框重叠情况下，`hidden` 值优先级最高，意味着如果存在其他的重叠边框，边框不会显示。 |
| dotted | 显示为一系列圆点。标准中没有定义两点之间的间隔大小，视不同实现而定。圆点半径是 [`border-width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-width) 计算值的一半。 |
| dashed | 显示为一系列短的`方形虚线`。标准中没有定义线段的长度和大小，视不同实现而定。 |
| solid  | 显示为一条实线。                                             |
| double | 显示为一条双实线，宽度是 [`border-width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-width) 。 |
| groove | 显示为有雕刻效果的边框，样式与 `ridge` 相反。                |
| ridge  | 显示为有浮雕效果的边框，样式与 `groove` 相反。               |
| inset  | 显示为`有陷入效果的边框`，样式与 `outset` 相反。当它指定到 [`border-collapse`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-collapse) 为 `collapsed` 的单元格时，会显示为 `groove` 的样式。 |
| outset | 显示为`有突出效果的边框`，样式与 `inset` 相反。当它指定到 [`border-collapse`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-collapse) 为 `collapsed` 的单元格时，会显示为 `ridge` 的样式。 |

###### border-color

**border-color** 是一个用于设置元素四个边框颜色的快捷属性

###### border-collapse

**border-collapse **属性控制浏览器绘制表格边框的方式。`它控制相邻单元格的边框`。

> border-collapse: collapse 表示相邻边框合并在一起。

##### 2.内边距(padding）

一个元素的内边距区域指的是`其内容与其边框之间的空间`。

> **注意：**
>
> * 内边距控制的是`元素内部空出的空间`。相反，外边距margin操作元素*外部*空出的空间。
> * `padding也会影响盒子的大小`。也就是说，如果盒子已经有了宽度和高度，此时再指定内边框，会撑大盒子。
> * `如何盒子本身没有指定width / height属性，则此时padding不会撑开盒子的宽 / 高`。

```css
/* 应用于所有边 */
padding: 1em;

/* 上边下边 | 左边右边 */
padding: 5% 10%;

/* 上边 | 左边右边 | 下边 */
padding: 1em 2em 2em;

/* 上边 | 右边 | 下边 | 左边 */
padding: 5px 1em 0 2em;

/* 全局值 */
padding: inherit;
padding: initial;
padding: unset;
```

##### 3.外边距（margin）

margin属性用于设置外边距，即控制盒子和盒子之间的距离。

**语法**

```css
/* 应用于所有边 */
margin: 1em;
margin: -3px;

/* 上边下边 | 左边右边 */
margin: 5% auto;

/* 上边 | 左边右边 | 下边 */
margin: 1em auto 2em;

/* 上边 | 右边 | 下边 | 左边 */
margin: 2px 1em 0 auto;

/* 全局值 */
margin: inherit;
margin: initial;
margin: unset;
```

###### 外边距典型应用——块级盒子水平居中对齐

外边距可以让块级盒子水平居中，但是必须满足两个条件：

* `盒子必须指定了具体宽度(width)，百分号没有用`；

* `盒子左右的外边距都设置为auto`；

> 常见的写法,以下三种都可以:
>
> 1. margin-left: auto; margin-right auto;
> 2. margin: auto;
> 3. margin: 0 auto;

###### 外边距典型应用——行内元素或者行内块元素水平居中对齐

> 行内元素或者行内块元素水平居中给其父元素添加<span style="color:red;font-size:20px">text-align:center</span> 即可。

###### 外边距合并问题

使用margin定义块元素的`垂直外边距`时，可能会出现`外边距的合并`。

**1.相邻块元素垂直外边距的合并**

当上下相邻的两个块元素<span style="color:red;font-size:16px"> (兄弟关系)</span>相遇时，如果上面的元素有下外边距margin-bottom，下面的元素有上外边距margin-top ，`则他们之间的垂直间距不是margin-bottom与margin-top之和。取两个值中的较大者这种现象被称为相邻块元素垂直外边距的合并`。

**解决方案**： 尽量只给一个盒子添加margin值。

**2.嵌套块元素垂直外边距的塌陷**
对于两个嵌套关系<span style="color:red;font-size:16px">(父子关系)</span>的块元素，`元素有上外边距同时子元素也有上外边距，此时父元素会塌陷较大的外边距值`。

![嵌套块元素垂直外边距的塌陷](http://pic.tolie.biz/images/image-20220110183921855.png)

**解决方案**:

1. 可以为父元素定义上边框；`transparant 透明色`
2. 可以为父元素定义上内边距；
3. 可以为父元素添加 overflow:hidden 。
4. 其他方法，比如浮动、固定、绝对定位的盒子不会有塌陷问题，

###### 清除内外边距

网页元素很多都带有默认的内外边距，而且不同浏览器默认的也不一致。`因此我们在布局前，有必要先清除下网页元索的内外边距`。

```css
* {
    padding:0;		/*清除内边距*/
	margin:0;		/*清除外边距*/
}
```

> **注意**：行内元素为了照顾兼容性，`尽量只设置左右内外边距，不要设置上下内外边距`。但是转换为块级和行内块元素就可以了

##### 小总结

1. 布局为啥用不同盒子 ?

   标签都是有语义的，合理的地方用合理的标签。比如产品标题就用h，大量文字段落就用p。

2. 为啥每个盒子都有一个类名?

   类名就是给每个盒子起了一个名字，可以更好的找到这个盒子，选取盒子更容易，后期维护也方便。

3. 到底用margin还是padding ?

   大部分情况两个可以混用，两者各有优缺点，但是根据实际情况，总是有更简单的方法实现。

4. 自己做没有思路?

   布局有很多种实现方式，同学们可以开始先模仿写法，然后再做出自己的风格。

##### 5.圆角边框（CSS3）

**border- radius**属性用于设置元素的外边框圆角。当使用一个半径时确定一个圆形，当使用两个半径时确定一个椭圆。这个(椭)圆与边框的交集形成圆角效果。

**语法**

> border- radius : length;
>
> /* 定义圆形半径或椭圆的半长轴，半短轴。负值无效。 */
>
> border- radius : percentage;
>
> /* 使用百分数定义圆形半径或椭圆的半长轴，半短轴。水平半轴相对于盒模型的宽度；垂直半轴相对于盒模型的高度。负值无效。 */

![border-radius:一个值时;](http://pic.tolie.biz/images/image-20220110214130560.png)

```css
{
    border-radius: 1em/5em;
    /* 等价于： */
    border-top-left-radius: 1em 5em;
    border-top-right-radius: 1em 5em;
    border-bottom-right-radius: 1em 5em;
    border-bottom-left-radius:  1em 5em;
}

{
    border-radius: 4px 3px 6px / 2px 4px;
    /* 等价于： */
    border-top-left-radius:     4px 2px;
    border-top-right-radius:    3px 4px;
    border-bottom-right-radius: 6px 2px;
    border-bottom-left-radius:  3px 4px;
}
```

**圆形作法**

```css
.yuanxing {
    width: 200px;
    height: 200px;
    background-color:pink;
    /* border- radius: 100px; */
    border-radius: 50%; /* 更常用 */
}
```

**圆角矩形**

```css
.juxing {
    width: 300px ;
    height: 100px;
    background-color:pink;
    /*圆角矩形设置为高度的一半*/
    /*border-radils: 50px;*/
    border-radius: 50%; /* 更常用 */
}	
```

##### 6.盒子阴影（CSS3）

**box- shadow**属性为盒子添加阴影。

**语法**

> box-shadow: h-shadow v-shadow blur spread color inset ;

| 值         | 描述                                     |
| :--------- | :--------------------------------------- |
| *h-shadow* | 必需。水平阴影的位置。允许负值。         |
| *v-shadow* | 必需。垂直阴影的位置。允许负值。         |
| *blur*     | 可选。模糊距离。                         |
| *spread*   | 可选。阴影的尺寸。                       |
| *color*    | 可选。阴影的颜色。请参阅 CSS 颜色值。    |
| inset      | 可选。将外部阴影 (outset) 改为内部阴影。 |

**注意**：

1. 默认的是外阴影(outset)，`但是不可以写这个单词，否则导致阴影无效`；
2. `盒子阴影不占用空间`，不会影响其他盒子排列。

##### 7.文字阴影（CSS3）

**语法**

> text-shadow: h-shadow v-shadow blur color;

| 值         | 描述                                                         |
| :--------- | :----------------------------------------------------------- |
| *h-shadow* | 必需。水平阴影的位置。允许负值。                             |
| *v-shadow* | 必需。垂直阴影的位置。允许负值。                             |
| *blur*     | 可选。模糊的距离。                                           |
| *color*    | 可选。阴影的颜色。参阅 [CSS 颜色值](https://www.w3school.com.cn/cssref/css_colors_legal.asp)。 |

2022年1月10日22:02:45



