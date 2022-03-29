---
title: CSS3-Flex布局
date: 2021-02-03 18:20:47
summary: 
categories: 
  - Frond End

tags:
  - CSS
---

### Flex 布局

[Flex 布局](https://www.runoob.com/w3cnote/flex-grammar.html)

网页布局（layout）是CSS的一个重点应用。布局的传统解决方案，基于盒状模型，依赖 display属性 + position属性 + float属性。它对于那些特殊布局非常不方便，比如，[垂直居中](https://css-tricks.com/centering-css-complete-guide/)就不容易实现。

2009年，W3C提出了一种新的方案——Flex布局，可以简便、完整、响应式地实现各种页面布局。目前，它已经得到了所有浏览器的支持，这意味着，现在就能很安全地使用这项功能。

![Flex 布局支持情况](http://pic.tolie.biz/images/202202251459749.jpeg)



#### 基本概念

Flex是Flexible Box的缩写，意为”弹性布局”，用来为盒状模型提供最大的灵活性。

`任何一个容器都可以指定为Flex布局，行内元素也可以使用Flex布局。`

> 注意：设为Flex布局以后，子元素的float、clear和vertical-align属性将失效。



`采用Flex布局的元素，称为Flex容器（flex container）`，简称”容器”。`它的所有子元素`自动成为容器成员，称为Flex项目（flex item），简称”项目”。

![基本概念](http://pic.tolie.biz/images/202201301422200.png)

容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。主轴的开始位置（与边框的交叉点）叫做main start，结束位置叫做main end；交叉轴的开始位置叫做cross start，结束位置叫做cross end。项目默认沿主轴排列。单个项目占据的主轴空间叫做main size，占据的交叉轴空间叫做cross size。



#### Flex布局元素的属性

##### 1、flex-direction属性

flex-direction属性决定主轴的方向（即项目的排列方向）。

**语法**

```css
.box {
  flex-direction: row | row-reverse | column | column-reverse;
}
```

**属性值**

| 属性值          | 说明                         |
| --------------- | ---------------------------- |
| row（`默认值`） | 主轴为水平方向，起点在左端。 |
| row-reverse     | 主轴为水平方向，起点在右端。 |
| column          | 主轴为垂直方向，起点在上沿。 |
| column-reverse  | 主轴为垂直方向，起点在下沿   |

![flex-direction属性](http://pic.tolie.biz/images/202202251459717.png)



##### 2、flex-wrap属性

默认情况下，项目都排在一条线（又称”轴线”）上。flex-wrap属性定义，如果一条轴线排不下，如何换行。

![img](http://pic.tolie.biz/images/202201301428726.png)

**语法**

```css
.box{
  flex-wrap: nowrap | wrap | wrap-reverse;
}
```

**属性值**

（1）nowrap（默认）：不换行。

![img](http://pic.tolie.biz/images/202202251459524.png)

（2）wrap：换行，第一行在上方。

![img](http://pic.tolie.biz/images/202201301428735.jpeg)

（3）wrap-reverse：换行，第一行在下方。

![img](http://pic.tolie.biz/images/202202251459558.jpeg)



##### 3、flex-flow属性

flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。

```css
.box {
  flex-flow: <flex-direction> <flex-wrap>;
}
```



##### 4、justify-content属性

justify-content属性定义了项目在主轴上的对齐方式。

```css
.box {
  justify-content: flex-start | flex-end | center | space-between | space-around;
}
```

![img](http://pic.tolie.biz/images/202201301430136.png)

它可能取5个值，`具体对齐方式与轴的方向有关`。下面`假设主轴为从左到右`。

> - flex-start（`默认值`）：左对齐
> - flex-end：右对齐
> - center： 居中
> - space-between：两端对齐，项目之间的间隔都相等。
> - space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。



##### 5、align-items属性

align-items属性定义项目在交叉轴上如何对齐。

```css
.box {
  align-items: flex-start | flex-end | center | baseline | stretch;
}
```

![img](https://www.runoob.com/wp-content/uploads/2015/07/2b0c39c7e7a80d5a784c8c2ca63cde17.png)

它可能取5个值。`具体的对齐方式与交叉轴的方向有关，下面假设交叉轴从上到下。`

> - flex-start：交叉轴的起点对齐。
> - flex-end：交叉轴的终点对齐。
> - center：交叉轴的中点对齐。
> - baseline: 项目的第一行文字的基线对齐。
> - stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。



##### 6、align-content属性

align-content属性`定义了多根轴线的对齐方式`。如果项目只有一根轴线，该属性不起作用。

**语法**

```css
.box {
  align-content: flex-start | flex-end | center | space-between | space-around | stretch;
}
```

![img](http://pic.tolie.biz/images/202201301434126.png)

**属性值**

> - flex-start：与交叉轴的起点对齐。
> - flex-end：与交叉轴的终点对齐。
> - center：与交叉轴的中点对齐。
> - space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
> - space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
> - stretch（默认值）：轴线占满整个交叉轴。