---
title: CSS3-BFC规范
date: 2022-3-13 19:54:55
summary: 
categories: 
  - Frond End

tags:
  - CSS
---

# CSS-BFC规范

## BFC到底是什么东西

`BFC` 全称：`Block Formatting Context`， 名为 "块级格式化上下文"。

`W3C`官方解释为：`BFC`它决定了元素如何对其内容进行定位，以及与其它元素的关系和相互作用，当涉及到可视化布局时，`Block Formatting Context`提供了一个环境，`HTML`在这个环境中按照一定的规则进行布局。

简单来说就是，`BFC`是一个完全独立的空间（布局环境），让空间里的子元素不会影响到外面的布局。那么怎么使用`BFC`呢，`BFC`可以看做是一个`CSS`元素属性

## 怎样触发BFC

满足下列条件之一就可触发BFC

- display: inline-block/table-cell/table-caption/flex
- position: absolute/fixed
- float的值不为none（默认）
- overflow的值不为visible（默认）

## BFC特性

- 内部的盒子会在垂直方向上一个接一个地放置
- 对于同一个BFC的两个相邻的盒子的margin会发生重叠
- 每个元素的左外边距与包含块的左边界相接触
- BFC的区域不会与float的元素区域重叠
- 计算BFC的高度时，浮动子元素也参与计算
- BFC就是页面上的一个隔离的独立容器，不会影响外面的元素

## BFC应用场景

- 解决浮动子元素导致父元素高度坍塌的问题
- 解决文字环绕在float四周的情况
- 解决边距重叠的问题