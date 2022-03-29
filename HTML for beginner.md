---
title: HTML for beginner
date: 2021-11-27 20:20:47
summary: 
categories: 
  - Frond End

tags:
  - HTML
---
# HTML for beginner

## 第一章  HTML概述

### 一、什么是HTML

HTML是一种超文本标记语言，由大量的标记组成，每一个标签都有开始标签和结束标签，标签也可以设置各自的属性。

超文本包括流媒体，图片、视频等。

### 二、HTML是谁制定的

W3C ：世界万维网联盟

W3C 制定HTML的规范，每个浏览器厂家遵守这一规范。

HTML规范最新的是HTML 5.0，简称H5。

## 第二章 HTML基础

### 第一个HTML页面

```html
<!--
在HTML文件第一行加上这一行代码
就表示用的是HTML 5.0版本
去掉就表示HTML 4.0版本
-->
<!DOCTYPE html>
<html>
    <head>
        <!--
		指定浏览器的解码方式，为"utf-8"
		并不是设置当前页面的字符编码方式
		-->
        <meta charset="utf-8">
        <title>第一个HTML页面</title>
    </head>
    <body>
        TOLIE你的未来有无限可能！
    </body>
</html>
```

### HTML基本标签 *

1、段落

```html
<p>   </p>
```

2、标题字

从h1-h6代表标题字，序号越小字体越大。

```html
<h1> H1</h1>
<h2> H2</h2>
<h3> H3</h3>
<h4> H4</h4>
<h5> H5</h5>
<h6> H6</h6>
```

3、换行

是一个独目标记

```html
<br>
```

4、水平线

是一个独目标记

```html
<hr>
```

5、预留格式

两个标签之间是什么格式，就在网页上展示什么格式，不做改变。

```html
    <pre>
金樽清酒斗十千，玉盘珍羞直万钱。
停杯投箸不能食，拔剑四顾心茫然。
欲渡黄河冰塞川，将登太行雪满山。
闲来垂钓碧溪上，忽复乘舟梦日边。
行路难，行路难，多歧路，今安在？
长风破浪会有时，直挂云帆济沧海。
    </pre>
```

6、粗体字、斜体字、插入字、删除字

```html
    <!--粗体字--->
	<b>TOLIE你的未来有无限可能！</b>
    <!--插入字--->
    <ins>插入字</ins>
    <!--斜体字--->
    <i>斜体字</i>
    <!--删除字--->
    <del>删除字</del>
```

7、右上角加字、右下角加字

```html
    <!--显示为10的2次方--->
	10<sup>2</sup>

    <!--显示为X的下标n--->
    X<sub>n</sub>
```

8、font标签

一个字体标签

```html
     <!--size和color是字体的属性，表示字号和颜色--->   
	<font size = "10" color = "blue">NEUQ</font>
```

### HTML实体符号

[html中特殊字符对应表](https://www.jb51.net/web/779702.html)

```html
    <!-- “&lt;” 是小于号--->
    a&lt;b
    <!-- “&gt;” 是大于号--->
    b&gt;c
    <!-- “&nbsp;” 是空格--->
    abc&nbsp;&nbsp;&nbsp;efg
```

### HTML的表格 *

#### 基本表格

1、table标签表示一个表格 
2、th标签也是一个单元格标签，一般用于表头，自带有加粗，居中效果
3、tr标签表示表格的一行
4、td标签表示表格中一个单元格

* border="1px"表示边框为1像素
* align="center"表示位置居中，也可以设置为居左居右
* width = "40%"表示内容占整个窗口的百分之几，==可以随着窗口的变化变化大小==

```html
    <!--
    1、table标签表示一个表格 
    2、th标签也是一个单元格标签，一般用于表头，自带有加粗，居中效果
    3、tr标签表示一行
	4、td标签表示一个单元格
    -->
	<!--一个3*3的表格 -->
    <table border="1" width = "40%">
        <tr align="center">
            <td>序号</td>
            <td>姓名</td>
            <td>班级</td>
        </tr>
        <tr align="center">
            <td>1</td>
            <td>TOLIE</td>
            <td>信管1901</td>
        </tr>
        <tr align="center">
            <td>2</td>
            <td>James</td>
            <td>信管1903</td>
        </tr>
    </table>
```

#### 单元格合并 *

==不能跨格合并==

row合并：一般把下侧单元格删掉，在上方单元格td标签中添加一个 rowspan 属性，属性值为几就合并几个单元格

```html
	<!--一个3*3的表格 -->
    <table border="1" width = "40%">
        <tr align="center">
            <td>序号</td>
            <td>姓名</td>
            <td>班级</td>
        </tr>
        <tr align="center">
            <td>1</td>
            <td>TOLIE</td>
            <td rowspan="2">信管1903</td>
        </tr>
        <tr align="center">
            <td>2</td>
            <td>James</td>
		<!-- <td>信管1903</td> -->
        </tr>
    </table>
</body>
```

col合并：删除左右的的单元格皆可，在单元格td标签中添加一个colspan 属性，属性值为几就合并几个单元格

```html
	<!--一个3*3的表格 -->
    <table border="1" width="40%">
        <tr align="center">
            <td>序号</td>
            <td>姓名</td>
            <td>班级</td>
        </tr>
        <tr align="center">
            <td>1</td>
            <!-- <td>TOLIE</td> -->
            <td colspan="2">信管1903</td>
        </tr>
        <tr align="center">
            <td>2</td>
            <td>James</td>
            <td>信管1903</td>
        </tr>
    </table>
```

#### thead. tbody. tfoot标签

将表格分为三个部分：头、身体和脚

不是必须的，但可以方便后期的JS代码编写。

==注意拆分之后可能会影响单元格的合并，导致单元格合并失败==

```html
	<!--一个3*3的表格 -->
    <table border="1" width="40%">
        <thead>
            <tr align="center">
                <td>序号</td>
                <td>姓名</td>
                <td>班级</td>
            </tr>
        </thead>

        <tbody>
            <tr align="center">
                <td>1</td>
                <!-- <td>TOLIE</td> -->
                <td colspan="2">信管1903</td>
            </tr>
            <tr align="center">
                <td>2</td>
                <td>James</td>
                <td>信管1903</td>
            </tr>
        </tbody>

        <tfoot>
        </tfoot>
    </table>
```

### HTML背景

```html
	<!--
	1.bgcolor 属性表示背景颜色，值为背景颜色的名称
	2.background 属性表示背景图片，值为背景图片的路径
	-->
	<body bgcolor="blue" background="web/img/cake-1.jpg"></body>
```

### HTML的图片

1. 设置图片高度和宽度的时候，只设置宽度，高度会等比例缩放；
2. img 标签就是图片标签；
3. src 属性的属性值是图片所在的路径；
4. tittle 属性值在==鼠标悬停==时显示的信息；
5. alt 属性设置在==图片找不到的时候==显示的内容；



#### Canvas位图

**描述**

- 通过Javascript来绘制2D图形。
- 是逐像素进行渲染的。
- 其位置发生改变，会重新进行绘制。

#### SVG矢量图

**描述**

- 一种使用XML描述的2D图形的语言
- SVG基于XML意味着，SVG DOM中的每个元素都是可用的，可以为某个元素附加Javascript事件处理器。
- 在 SVG 中，每个被绘制的图形均被视为对象。如果 SVG 对象的属性发生变化，那么浏览器能够自动重现图形。

#### 比较

**Canvas**

- 依赖分辨率
- 不支持事件处理器
- 弱的文本渲染能力
- 能够以 .png 或 .jpg 格式保存结果图像
- 最适合图像密集型的游戏，其中的许多对象会被频繁重绘

**SVG**

- 不依赖分辨率
- 支持事件处理器
- 最适合带有大型渲染区域的应用程序（比如谷歌地图）
- 复杂度高会减慢渲染速度（任何过度使用 DOM 的应用都不快）
- 不适合游戏应用

### HTML超链接

特点： 1. 超链接下面有下划线；

​			2.点击之后可以跳转页面；

​			3.鼠标放在上面会变成小手；

```html
//文本超链接
<a href="http://www.baidu.com">百度</a>
//图片超链接
<a href="http://www.baidu.com">
    <img src="web/img/cake-2.jpg">
</a>
//点击超链接之后在本页面实现跳转
<a href="http://www.baidu.com" target="_blank">百度</a>
//点击超链接之后在新页面实现跳转
<a href="http://www.baidu.com" target="_self">百度</a>
```

herf：是热引用，属性值一定是一个资源的地址，比如"https://www.bilibili.com"

a 标签的target属性的可取值有

1. _self ：在本窗口实现跳转
2. _blank：在新窗口实现跳转
3. _top：在顶级窗口实现跳转
4. _parent：在父窗口实现跳转

### 有序列表和无序列表

* 有序列表

​	标签：ol （ordered list）属性有个type用于指定序号的形式，可以是数字、大写英文、小写英文等；

​	表项：li

* 有序列表

​	标签：ul （unordered list）属性有个type用于指定序号的形式，可以是圆圈，方块或者点；

​	表项：li

```html
<!-- 有序列表 -->
<ol type="1">
    <li>水果
        <ol type="a">
            <li>苹果</li>
            <li>西瓜</li>
        </ol>
    </li>
    <li>蔬菜</li>
    <li>甜点</li>
</ol>

<!-- 无序列表 -->
<ul type="circle">
    <li>beijing
        <ul type="disc">
            <li>e</li>
            <li>w</li>
            <li>s</li>
            <li>n</li>
        </ul>
    </li>
</ul>
```

### HTML中的id和name

1. 在html文档中，任何元素/节点都有唯一的id，id是节点的唯一标识，在同一个html文档中id值不能重复
2. id可以帮助我们确定唯一的节点
3. html文档是一棵树（DOM树），树上有很多节点，每个节点都有着唯一的id。而js就是对这个树上的节点进行增删改查等操作的。

### HTML中的div和span

* div是块级元素，span是内联元素

* 是什么？什么div和span都可以称为“图层”；
  * 图层的作用是保证页面可以灵活布局，现在最流行的就是使用div进行布局；
  * 图层可以是一个一个的盒子，盒子套盒子就是div套div；
  * div和span的定位可以通过左上角的x轴，y轴坐标来确定；
* 作用：布局，方便布局；
* div和span的区别：默认情况下div会独占一行，而span不会；

## HTML的form表单 *

### 标签：form

作用：收集用户信息，用户填写好之后，提交服务器做后续处理；

1. action 属性值为提交表单的服务器路径/地址；
2. method 属性值为提交表单的方法；
3. id 属性值用于唯一标识表单，可以理解为 ；
4. class 属性值用于标识变量，但不能唯一标识，可以理解为民族；

```html
<form method="post" action="login.do" class="login" id="lg">
            <input type="text" placeholder="用户名" id="username1" name="username1" autocomplete="off">
            <input type="password" placeholder="密码" id="password1" name="password1">
            <input type="button" value="登 录" class="btn" id="login" onclick="Log()">
        </form>
```

### 标签：input  **

* readonly，只读，用户不能更改，==但可以提交到服务器==；
* disabled，只读，用户不能选中更不能此 input 标签的value，==且不能提交服务器==；
* maxlength，可以用来==控制输入的字符数量==，属性值为几就能输入几个字符
* type 属性值可以有多种，具体内容如下表所示！！[更多属性值](https://www.cnblogs.com/dadayang/p/5749068.html)

| 值         | 描述                                                         |
| :--------- | :----------------------------------------------------------- |
| button     | 定义可点击按钮（多数情况下，用于通过 JavaScript 启动脚本）。 |
| checkbox * | 定义复选框。                                                 |
| file *     | 定义输入字段和 "浏览"按钮，供文件上传。使用时要给form表单设置enctype属性，enctype ="multipart/form-data" |
| hidden **  | 定义隐藏的输入字段，这部分内容网页不展示，但可以正常提交。   |
| image      | 定义图像形式的提交按钮。                                     |
| password * | 定义密码字段。该字段中的字符被掩码。                         |
| radio *    | 定义单选按钮。                                               |
| reset      | 定义重置按钮。重置按钮会清除表单中的所有数据。               |
| submit *   | 定义提交按钮。提交按钮会把表单数据发送到服务器。             |
| text *     | 定义单行的输入字段，用户可在其中输入文本。默认宽度为 20 个字符 |
| number     | 定义输入的类型为数字，且==默认情况下会要求填一个整数==。此时定义maxlength不会发挥作用，如果需要限制用户输入的位数，就用js进行约束。 |

==填写了表单项 input 的name属性一律会提交给服务器，没有name属性就不会提交==

* placeholder 属性提供可描述输入字段预期值的==提示信息==（hint）；

  该提示会在输入字段为空时显示，并会在字段获得焦点时消失；

  适用于以下 text, search, url, telephone, email 以及 password 的  input 类型；

* name   input  没有name属性就不会提交  input  内的数据；

* 使得 number类型的 input 可以向服务器传小数

```html
<!-- 支持传送至多两位小数 -->
<input type="number" id="number" name="number" step="0.01">

<!-- 支持传送至多4位小数 -->
<input type="number" id="number" name="number" step="0.0001">
```

### 标签：label

一般用于和单选或多选使用，使得==点击label可以选择label对应的选项==

* label 中的 for 属性值是对应选项的id 值

```html
<label for="man">男</label>
<input type="radio" name="sex" id="man">
<label for="woman">女</label>
<input type="radio" name="sex" id="woman">
```

### 标签：select *

* `multiple用来设置允许多选`，设置多选之后可以按住ctrl进行多选；

* size 用来指示展示几项选项；

```html
	<select name="degree" multiple size="2">
        <!-- selected表示默认选择 -->
        <option value="dz" selected>大专</option>
        <option value="bk">本科</option>
        <option value="ss">硕士</option>
        <option value="bs">博士</option>
	</select>
```

### 第一个form表单 *

注意：

* 选择按钮的value必须手动指定；
* 文本域没有value属性，用户填写的内容就是value；
* 单选内容一般设置每个 input 的name相同，只提交一个内容，保证单选；
* 确认密码的时候记住不设置name属性值，阻止提交；
* 提交格式不管是什么方式都是 ==name=value&name=value&name=value&name=value==

```html
<form method="GET" action="login.do" class="regist" id="lg">
<!-- method属性是指定提交方式
	默认方式，也就是GET方式会把数据展示在地址栏上
	POST方式不会把数据展示在地址栏-->
    <table border="1px">
        <tr>
            <td align="center">用户名</td>
            <td><input type="text" placeholder="用户名" id="username1" name="username1" autocomplete="off"></td>
        </tr>
        <tr>
            <td align="center">密&nbsp;&nbsp;&nbsp;码</td>
            <td><input type="password" placeholder="密码" id="password" name="password"></td>
        </tr>
        <tr>
            <td align="center">确认密码</td>
            <td><input type="password" placeholder="确认密码"></td>
        </tr>
        <tr align="center">
            <!-- 选择按钮的value必须手动指定 -->
            <td align="center">性&nbsp;&nbsp;&nbsp;别</td>
            <td>
                <!-- checked表示默认选择 -->
                <input type="radio" name="sex" id="man" value="1" checked>
                <label for="man">男</label>
                <input type="radio" name="sex" id="woman" value="0">
                <label for="woman">女</label>
            </td>
        </tr>
        <tr align="center">
            <!-- 选择按钮的value必须手动指定 -->
            <td>爱&nbsp;&nbsp;&nbsp;好</td>
            <td>
                <!-- checked表示默认选择 -->
                <input type="checkbox" name="interest" value="0" checked>读书
                <input type="checkbox" name="interest" value="1">喝酒
                <input type="checkbox" name="interest" value="2">烫头
                <input type="checkbox" name="interest" value="3">保健
            </td>
        </tr>
        <tr align="center">
            <!-- 选择按钮的value必须手动指定 -->
            <td>学&nbsp;&nbsp;&nbsp;历</td>
            <td>
                <select name="degree">
                    <!-- selected表示默认选择 -->
                    <option value="dz" selected>大专</option>
                    <option value="bk">本科</option>
                    <option value="ss">硕士</option>
                    <option value="bs">博士</option>
                </select>
            </td>
        </tr>
        <tr align="center">
            <!-- 选择按钮的value必须手动指定 -->
            <td>个人介绍</td>
            <td>
                <!-- 文本域没有value属性，用户填写的内容就是value -->
                <textarea name="selfjs" role="20" rows="2"></textarea>
            </td>
        </tr>            
    </table>
</form>
<input type="reset" value="重 置">
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<input type="submit" value="登 录" class="btn" id="regist">
<!-- 提交结果：http://127.0.0.1:5500/login.do?username1=ww&password=qq&sex=1&interest=0&interest=1&interest=2&degree=dz&selfjs=1231-->
```

