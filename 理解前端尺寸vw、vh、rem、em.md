---
title: 理解前端尺寸vw、vh、rem、em
date: 2022-3-11 10:19:58
summary: 
categories: 
  - Frond End

tags:
  - CSS
---

## em

em 是一个相对长度单位。`其相对于当前对象内文本的字体尺寸`，如当前对行内文本的字体尺寸未被人为设置，则相对于浏览器的默认字体尺寸。

- em的值并不是固定的
- em会继承父级元素的字体大小

[例子：](https://jsbin.com/pafifiz/5/edit?html,css,js,output)



![img](http://pic.tolie.biz/images/202203091601805.jpeg)



其中，浏览器默认尺寸是16px，故body中的font-size: 16 * 62.5%=10px,而#app继承与父级元素10px * 1.2 = 12px，#footer继承与body 10px*2=20px;而#app p继承与#app，此时1em=12px，故#app p中的font-size为12px*1.2=14.4px

运行js

```js
document.body.style.fontSize='20px';
```



![img](http://pic.tolie.biz/images/202203091601457.jpeg)



我们可以看到，网页中所有采用em单位，由于body font-size设置为20px，其他均等比例的扩大

由此**得出结论**

- 我们可以通过设置一个父级元素如html、body font-size,作为整体默认尺寸，通过运行js脚本动态修改font-size实现适配
- 其适配方案依旧是依据像素点来适配
- 需要通过注入脚本实现
- 所有子元素的宽度、高度、font-size等尺寸，均继承与父元素，故增加了我们的计算成本

## rem

rem全名root em，简写rem，故其也是一个相对长度单位，但`只相对于根元素`，可以简单的通过更改根元素大小，从而调整所有字体大小。

- 只相对于根元素（html）
- 通过修改根元素可成比例的调整页面字体大小
- 其适配方案通过js脚本设置像素点来实现

其与em的基本用法是一致的，唯独不一致的是，所有元素都是相对于根元素，而不是父级元素，减少了我们的计算成本

[例子](https://jsbin.com/wugigap/1/edit?html,css,output)



![img](http://pic.tolie.biz/images/202203091601464.jpeg)



通过注入js

```js
document.documentElement.style.fontSize='20px'
```



![img](http://pic.tolie.biz/images/202203091600515.jpeg)



**总结**：

- 用rem，不用em，尺寸清晰，易于维护
- 由于rem是root em，故其与em兼容性是一致的
- 均是基于像素点适配

### 移动端使用方案

在移动端适配方案中，使用rem时，通常与scss、less、postcss等预编译器相结合，通过定义一些函数，或者使用一些插件、使我们在开发时，依旧使用px，即设计师给我们的设计稿像素点，通过预编译期将其编译成rem单位。从而实现适配

## vw、vh

vw（Viewport Width）、vh(Viewport Height)是基于视图窗口的单位，是css3的一部分，基于视图窗口的单位，除了vw、vh还有vmin、vmax。

- vw:1vw 等于视口宽度的1%
- Vh:1vh 等于视口高度的1%
- vmin: 选取 vw 和 vh 中最小的那个,即在手机竖屏时，1vmin=1vw
- vmax:选取 vw 和 vh 中最大的那个 ,即在手机竖屏时，1vmax=1vh

> Note: IE9 uses `vm` instead of `vmin`. It does not support `vmax`.

由于使用vw、vh依赖于视图窗口，故当屏幕分辨率变大或者缩小，尺寸会进行相应的放大或者缩小，当页面足够大，或者足够小时，尺寸会变得很大或者很小，从而导致用户体验差，当然谁会用那么大或者那么小的设备呢？大多数情况下，其实可以忽略不计的，如果你是一个最求完美用户体验的人，可通过rem，对根元素设置最大最小值，配合body加上最大宽度和最小宽度。