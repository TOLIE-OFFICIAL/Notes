---
title: JS for beginner (part 1)
date: 2021-12-24 18:20:47
summary: 
categories: 
  - Frond End

tags:
  - JavaScript

---

## JavaScript学习

### 第一部分 JavaScript基础

#### 第一章 绪论

##### 1.1JavaScript是什么

* JavaScript 是世界上最流行的语言之一, 是`一种运行在客户端的脚本语言` ( Script是脚本的意思)
* 脚本语言：不需要编译,运行过程中由js解释器(js引擎)逐行来进行解释并执行
* 现在也可以`基于 Node.js技术进行服务器端编程`

##### 1.2  JavaScript的作用

1. 表单动态校验(密码强度检测) （JS 产生最初的目的）
2. 网页特效
3. 服务端开发(Node.js)
4. 桌面程序(Electron)
5. App(Cordova)
6. 控制硬件-物联网(Ruff)
7. 游戏开发(cocos2d-js)

##### 1.3  HTML/CSS/JS的关系

1. HTML/CSS标记语言-描述类语言
   * HTML决定网页结构和内容(决定看到什么) ,相当于人的身体
   * CSS决定网页呈现给用户的模样(决定好不好看) ,相当于给人穿衣服、化妆

2. JS脚本语言--编程类语言
   * 实现业务逻辑和页面控制(决定功能) ,相当于人的各种动作的

##### 1.4 浏览器执行JS简介

* 浏览器分成两部分渲染引擎和JS引擎

  * 渲染引擎：用来解析HTML与CSS ,俗称内核,比如chrome浏览器的blink ,老版本的webkit
  * JS 引擎：也称为JS解释器。用来读取网页中的JavaScript代码 。对其处理后运行，比如chrome浏览器的V8引擎

  > 浏览器本身并不会执行JS代码,而是通过内置JavaScript引擎(解释器)来执行JS代码。JS 引擎执行代码时逐行解释每一句源码(转换为机器语言) , 然后由计算机去执行,所以JavaScript语言归为`脚本语言, 会逐行解释执行`。

##### 1.5 JS的组成

![JS的组成](https://gitee.com/mr_tolie/pics/raw/master/images/image-20211223195620639.png)

1. **ECMAScript**是由ECMA国际(原欧洲计算机制造商协会)进行标准化的一]编程语言, 这种语言在万维网上应用广
   泛,它往往被称为JavaScript或JScript ,但实际上后两者是ECMAScript语言的实现和扩展。

   ![ECMAScript](https://gitee.com/mr_tolie/pics/raw/master/images/image-20211223195729359.png)

   > ECMAScript ：ECMAScript规定了JS的编程语法和基础核心知识，所有浏览器厂商共同遵守的一套S语法工业标准。

2. **文档对象模型**( Document Object Model ,简称DOM) , 是W3C组织推荐的处理可扩展标记语言的标准编程接口。通过DOM提供的接口可以对页面上的各种元素进行操作(大小位置、颜色等)。

3. **浏览器对象模型**(Browser Object Model ,简称BOM)是指浏览器对象模型,它提供了独立于内容的、可以与浏览器窗口进行互动的对象结构。通过BOM可以操作浏览器窗口,比如弹出框、控制浏览器跳转、获取分辨率等。

#### 第二章 开始JavaScript

##### 2.1 JavaScript的三种类型

1. 行内式

   * 可以将单行或少量JS代码写在HTML标签的事件属性中(以on开头的属性)，如 : onclick
   * 注意单双引号的使用：在HTML中我们推荐使用双引号，JS中我们推荐使用`单引号`
   * 可读性差,在html中编写JS大量代码时,不方便阅读;
   * 引号易错,引多层嵌套匹配时,非常容易弄混;
   * 特殊情况下使用

2. 内嵌式 

   * 可以将多行IS代码写到"script"标签中

   * 内嵌JS是学习时常用的方式

   * **Javascript的加载和执行的特点：** 
     （1）载入后马上执行； 

     （2）执行时会阻塞页面后续的内容（包括页面的渲染、其它资源的下载）。原因：因为浏览器需要一个稳定的DOM树结构，而JS中很有可能有代码直接改变了DOM树结构，比如使用 document.write 或  appendChild,甚至是直接使用的location.href进行跳转，浏览器为了防止出现JS修改DOM树，需要重新构建DOM树的情况，所以就会阻塞其他的下载和呈现。

     （3）`推荐script标签写在body结束标签之前，而不是head结束标签之前`。

3. 外部

   * 利于HTML页面代码结构化,把大段JS代码独立到HTML页面之外,既美观,也方便文件级别的复用
   * 引用外部JS文件的script标签中间不可以写代码
   * 适合于JS代码量比较大的情况

##### 2.2 JavaScript输入输出语句

|       方法       | 说明                           |  归属  |
| :--------------: | ------------------------------ | :----: |
|    alert(msg)    | 浏览器弹出警示框               | 浏览器 |
| console.log(msg) | 浏览器控制台打印输出信息       | 浏览器 |
|   prompt(info)   | 浏览器弹出输入框，用户可以输入 | 浏览器 |

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <!-- 外部JS文件 -->
    <script src="js/Demo1.js"></script>
    <!-- 内嵌式 -->
    <script>
        /* 这是一个输入框 */
        prompt("请输入用户名！")
        /* 控制台输出 */
        console.log("wzhhhhhhhhhhh!")
    </script>
</head>

<body>
    <!-- 内嵌式 -->
    <!-- 弹窗输出 -->
    <input type="button" value="加油！" onclick="alert('好耶！')">
</body>

</html>
```

##### 2.3 JS变量

变量是程序在内存中申请的一块用来存放数据的空间。
`在javascript中有三种声明变量的方式：var、let、const`。

1. **var**
   var定义的变量`可以修改`，`如果不初始化会输出undefined，不会报错`。

```js
var a = 1;
// var a;//不会报错
console.log('函数外var定义a：' + a);//可以输出a=1
function change(){
a = 4;
console.log('函数内var定义a：' + a);//可以输出a=4
} 
change();
console.log('函数调用后var定义a为函数内部修改值：' + a);//可以输出a=4
```

var 声明全局变量，换句话理解就是，声明在for循环中的变量，跳出for循环同样可以使用。

声明在for循环内部的sum，跳出for循环一样可以使用，不会报错正常弹出结果

```js
for(var i=0;i<=1000;i++){ 
var sum=0; 
sum+=i; 
} 
alert(sum);
```

2. **let**
   同一个变量，不可在声明之前调用，必须先定义再使用，否则会报错，循环体中可以用let

   `let是块级作用域`，函数内部使用let定义后，对函数外部无影响。并且let不能定义同名变量，否则会报错。

```js
let c = 3;
console.log('函数外let定义c：' + c);//输出c=3
function change(){
let c = 6;
console.log('函数内let定义c：' + c);//输出c=6
} 
change();
console.log('函数调用后let定义c不受函数内部定义影响：' + c);//输出c=3
```

`注意：必须声明'use strict'；后才能使用let声明变量否则浏览并不能显示结果,`

3. **const**
   const：用于声明常量，也具有块级作用域 ，也可声明块级。`const定义的变量不可以修改，而且必须初始化`。

```js
const b = 2;//正确
// const b;//错误，必须初始化 
console.log('函数外const定义b：' + b);//有输出值
// b = 5;
// console.log('函数外修改const定义b：' + b);//无法输出
const PI=3.14;
```

> const和let一样，也不能重复定义同一个变量，const一旦定义，无法修改；
>
> let和const属于局部变量，不会出现变量提升的情况，全局定义的let和const变量，不属于顶层变量，不属于window的属性；

##### 2.4 JS函数的两种声明方式

```js
/* 1.利用函数关键字声明函数 */
function sum() {
    console.log('我是关键字声明的函数！');
}
sum();
/* 2.函数表达式声明的函数 （也叫匿名函数）*/
var add = function () {
    console.log('我是函数表达式声明的函数');
}
add();
//(1) fun是变量名不是函数名
//(2) 函数表达式声明方式跟声明变量差不多，只不过变量里面存的是值而函数表达式里面存的是函数
//(3) 函数表达式也是可以传递参数的
```

##### 2.5 JavaScript的作用域

1. **作用域概述**
   通常来说，一段程序代码中所用到的名字并不总是有效和可用的，而`限定这个名字的可用性的代码范围就是这个名字的作用域`。

   > 作用域的使用提高了程序逻辑的局部性，增强了程序的可靠性，减少了名字冲突。

2. **JavaScript的两种作用域**（es6之前）

   * 全局作用域：即整个script标签或者一个单独的js文件内起效果；
   * 局部作用域：局部作用域(函数作用域)在函数内部就是局部作用域`这个代码的名字只在函数内部起效果和作用；`；

3. **变量的分类**

   根据作用域的不同我们变量分为全局变量和局部变量

   * 全局变量：在全局作用域下的变量，在整个script标签或者一个单独的js文件起效果；
   * 局部变量：在局部作用域下的变量，后者在函数内部的变量就是局部变量；

   > **注意**：如果在函数内部没有声明直接赋值的变量也属于全局变量；函数的形参也可以看做一种局部变量。

   从执行效率来看全局变量和局部变量

   * (1)全局变量`只有浏览器关闭的时候才会销毁`，比较占内存资源
   * (2) 局部变量当我们程序执行完毕就会销毁，比较节约内存资源

4. ES6之前，JS中作用域有：全局作用域、函数作用域，并没有块作用域的概念。

   `ECMAScript 6`(简称ES6)中`新增了块级作用域`。块作用域由 { } 包括，if语句和for语句里面的{ }也属于块作用域。

   ```js
   if (7 > 5) {
               var num = 10;
               console.log(num);
           }
           console.log('num=' + num);
   		/* 输出结果 10；num=10*/
   ```

5. **作用域链**

   * 只要是代码,就至少有一个作用域；
   * 写在函数内部的局部作用域，如果函数中还有函数 ,那么在这个作用域中就又可以诞生一个作用域；
   * 内部函数访问外部函数的变量，采取的是`链式查找`的方式来决定取那个值这种结构我们称为作用域链，并遵循`就近原则`；

   ```js
   function f1() {
               var num = 123;
               function f2() {
                   console.log(num);
               }
               f2();
           }
           var num = 456;
           f1();
   //輸出結果為 123
   ```

   ![作用域链](https://gitee.com/mr_tolie/pics/raw/master/images/image-20211224132422879.png)

#### 第三章 JS的预解析

> JavaScript代码是由浏览器中的JavaScript解析器来执行的。JavaScript 解析器在运行JavaScript代码的时候分为两步:`预解析和代码执行`。

预解析：js引擎会把js里面所有的var 还有function 提开到当前作用域的最前面；

代码执行：按照代码书写的顺序从上往下执行

##### 3.1 预解析

预解析分为`变量预解析`(变量提升) 和`函数预解析`(函数提升) 

1. ###### 变量预解析

   变量提升就是把所有的变量声明提升到当前的作用域最前面，但`不提升赋值操作`

   ```js
   var add = function () {
               console.log('我是函数表达式声明的函数');
           }
           add();
   //上方代码等价于
   var add;
   add = function () {
       console.log('我是函数表达式声明的函数');
   }
   add();
   /*故下方代码会报错
   fun(); 
   var fun = function（）{
   console.1og(22); 
   }*/
   ```

2. ###### 函数提升

   函数提升就是把所有的函数声明提升到当前作用域的最前面，但`不调用函数`。

   ```js
   function fn(){
   	console. log(11);
   }
   fn();
   //与下方代码执行效果相同
   fn();
   function fn(){
   	console. log(11);
   }
   ```

   

#### 第四章 JS的对象

> JavaScript中的对象分为3种：定义对象、内置对象、浏览器对象
>
> **内置对象**就是指JS语言自带的一些对象，这些对象供开发者使用，并提供了一些常用的或是最 基本而必要的功能(属性和方法)

**学习对象中的方法：**

[MDN开发文档地址](https://developer.mozilla.org/zh-CN/)

1. 查阅该方法的功能
2. 查看里面参数的意义和类型
3. 查看返回值的意义和型
4. 通过demo进行测试

**重写Math中的PI属性和最大值最小值方法**

```js
var myMath = {
    PI: 3.1415926,
    max: function () {
        let max = arguments[0];
        for (i = 1; i < arguments.length; i++) {
            if (max < arguments[i]) {
                max = arguments[i];
            }
        }
        return max;
    },
    min: function () {
        let min = arguments[0];
        for (i = 1; i < arguments.length; i++) {
            if (min > arguments[i]) {
                min = arguments[i];
            }
        }
        return min;
    }
}
console.log(myMath.PI);  // 3.1415926
console.log(myMath.max(1, 3, 10));  // 10
console.log(myMath.min(1, 3, 10));  // 1
```

**猜数字小游戏**

```js
//得到一个两数之间的随机整数，不包含这两个数
function getRandomInt(min, max) {
    //Math.ceil()向上取整
    min = Math.ceil(min);
    //Math.floor()向下取整
    max = Math.floor(max);
    return Math.floor(Math.random() * (max - min)) + min; //不含最大值，含最小值
}
//得到一个两数之间的随机整数，包含这两个数
function getRandomIntInclusive(min, max) {
    min = Math.ceil(min);
    max = Math.floor(max);
    return Math.floor(Math.random() * (max - min + 1)) + min; //含最大值，含最小值 
}

var numGame = function () {
    let number = getRandomInt(1, 10);
    console.log(number);
    while (true) {
        let num = prompt('我是谁？ 1~10');
        if (num > number) {
            alert('你太高看我了!');
            // continue;
        } else if (num < number) {
            alert('你太小瞧我了！');
            //continue;
        } else {
            alert('你猜对了！！')
            break;
        }
    }
}
```



##### 4.1 对象object

在JavaScript中，`对象是一组无序的相关属性和方法的集合` ,所有的事物都是对象，例如字符串、数值、数组、函数等。

* **属性**：事物的`特征`，在对象中用属性来表示（常用名词）
* **方法**：事物的`行为`，在对象中用方法来表示（常用动词）

![JS的对象](https://gitee.com/mr_tolie/pics/raw/master/images/image-20211226134520090.png)

保存一个值时，可以使用变量，保存多个值(一组值)时,可以使用数组。而JS中的对象表达结构更清晰，更强大。

##### 4.2 创建对象的三种方式

1. ###### 利用字面量创建对象

```js
/* 1.利用字面量创建对象 */
var obj = {
    uname: 'TOLIE',
    age: 18,
    sex: 1,
    sayHi: function () {
        console.log('你好，我是TOLIE！');
    }
}
//调用对象的属性
console.log(obj.uname);
console.log(obj['age']);
//调用对象的方法
obj.sayHi();
```

* **注意**：

  **创建对象**

  1. 里面的属性或者方法我们采取键值对的形式，键  属性名:值 属性值
  2. 多个属性或者方法中间用`英文逗号`隔开的
  3. 方法冒号后面跟的是一个`匿名函数`

  **使用对象**

  1. 调用对象的属性我们采取：`对象名.属性名`
  2. 调用属性还有一种方法：`对象名['属性名']`
  3. 调用对象的方法：`对象名.方法名()`

> *变量、属性的区别*：
>
> * 相同点
>
>   变量和属性的相同的他们都是用来存储数据的
>
> * 不同点
>
>   变量：单独声明并赋值，使用的时候直接写变量名，是`单独存在`的
>   属性：在`对象里面`的不需要声明的，使用的时候必须是：对象.属性
>
> *函数、方法的区别*：
>
> * 相同点
>
>   都是实现某种功能/做某件事
>
> * 不同点
>   函数：单独存在的,通过“ 函数名()”的方式就可以调用
>   方法：对象里面的函数称为方法，方法不需要声明,使用“对象方法名()”的方式就可以调用,方法用来描述该对象的行为和功能。

2. ###### 利用new object 创建对象

```js
/* 2.利用new object创建对象 */
var obj2 = new Object();
obj2.name = 'James';
obj2.age = 18;
obj2.school = 'NEUQ';
obj2.sayHello = function () {
    console.log('你好~~~');
}
console.log(obj2.name);
console.log(obj2['school']);
obj2.sayHello();
```

* **注意**：
  1. 我们是利用等号 = 赋值的方法添加对象的属性和方法；
  2. 每个属性和方法之间用`分号`结束；

3. ###### 利用构造函数创建对象

* 因为我们一次创建个对象，里面很多的属性和方法是大量相同的我们只能复制。因此我们可以利用函数的方法重复这些相同的代码我们就把这个函数成为构造函数；
* 构造函数: 是一种特殊的函数。主要用来初始化对象,即为对象成员变量赋初始值，它总与new运算符一起使用。我们可以把对象中一些公共的属性和方法抽取出来，然后封装到这个函数里面。

```js
/* 3.利用构造函数创建对象 */
function Singers(name, age, sex) {
    this.name = name;
    this.age = age;
    this.sex = sex;
    this.sing = function (sang) {
        console.log(sang);
    }
}
var X = new Singers('薛之谦', 38, '男');
console.log(X.name);
console.log(X['sex']);
X.sing('认真的雪');
console.log(typeof X);
```

* **注意**：
  1. 构造函数名字`首字母要大写`；
  2. 构造函数`不需要return就可以返回结果`；
  3. 属性和方法前面必须添加`this关键字`；
  4. 我们调用构造函数必须使用`new关键字`。

构造函数：如Stars( )，抽象了对象的公共部分，封装到了函数里面，它泛指某一大类( class )；
创建对象：如new Stars() ，特指某一个，通过new关键字创建对象的过程我们也称为对象实例化。

> **new关键字执行过程**
>
> 1. 在内存中创建了一个空的对象
> 2. this 指向刚才创建的空对象
> 3. 执行构造函数里面的代码，给这个空对象添加属性和方法
> 4. 返回这个对象，(所以构造函数里面不需要return )。

##### 4.3.1 遍历对象的属性 *

`for..in语句`用于对数组或者`对象的属性`进行循环操作。

```js
function Hero(name, type, blood) {
    this.name = name;
    this.type = type;
    this.blood = blood;
    this.attack = function (attack) {
        console.log(attack);
    }
}
var lp = new Hero('廉颇', '力量型', 500);
/* lp.attack('近战'); */
for (var k in lp) {
    //输出属性名
    console.log(k);
    //输出属性值，注意：k不加引號
    console.log(lp[k]);
}
```

##### 4.3.2 判断对象中是否有某个属性

```js
//有一个对象来判断是否有该属性对象[ '属性名']
var obj = {
    age: 18,
    sex: 0
}
if (obj['age']) {
    //obj['age']为18,18!=0,故为true
    //obj['sex']为0,故为false
    console.log('里面有该属性');
} else {
    console.log('没有该属性');
}
```

##### 4.4.1 Date()对象

###### 1). 日期对象的使用

* Date()日期对象是一个构造函数，`必须使用new关键字来创建日期对象`；

```js
//实例化一个日期对象
var date = new Date();
//1.如果没有参数，则返回的是实例化时候的系统时间
var date1 = new Date();
console.log('date1=' + date1);
//2.如果使用参数，参数的常用写法有：
//数字型2019,02,01；会比输入的时间晚一个月
var date2 = new Date(2019, 02, 01);
console.log('date2=' + date2);
//字符串型‘2019-2-1 14:14:14’
var date3 = new Date('2019-2-1 14:14:14');
console.log('date3=' + date3);
```

###### 2). 日期的格式化

* 需要获取日期的指定部分，可以手动得到

| 方法名        | 說明                        | 代碼               |
| ------------- | --------------------------- | ------------------ |
| getFullYear() | 获取当年                    | Obj.getFullYear()) |
| getMonth()    | 获取当月（0-11）            | Obj.getMonth()     |
| getDate()     | 获取当天日期（从1--31）     | Obj.getDate()      |
| getDay()      | 获取星期几(`周日0 到周六6`) | Obj.getDay()       |
| getHours()    | 获取当前小时                | Obj.getHours()     |
| getMinutes()  | 获取当前分钟                | Obj.getMinutes()   |
| getSeconds()  | 获取当前秒钟                | Obj.getSeconds()   |

```js
//以getFullyear为例
var date3 = new Date('2019-2-1 14:14:14');
console.log(date3.getFullYear());
//输出结果为2019

//日期的格式化方法
function getMyDate() {
    let date = new Date();
    let year = date.getFullYear();
    let month = date.getMonth() + 1;
    let dates = date.getDate();
    let arr = ['星期日', '星期一', '星期二', '星期三', '星期四', 
               '星期五', '星期六']
    let weekDays = date.getDay();
    let hour = date.getHours();
    //判断，含义是如果hour小于10则在前面加上‘0’，反之不做更改，最终返回hour
    hour = hour < 10 ? '0' + hour : hour;
    let min = date.getMinutes();
    min = min < 10 ? '0' + min : min;
    let sec = date.getSeconds();
    sec = sec < 10 ? '0' + sec : sec;
    let now = year + '年' + month + '月' + dates + '日 ' + arr[weekDays] + 				' ' + hour + ':' + min + ':' + sec;
    return now;
}
getMyDate();
```

###### 3). 获取日期的总的毫秒/时间戳

> 获得Date总的毫秒数，不是当前时间的毫秒数，而是**距离1970年1月1号过了多少毫秒数**

```js
//获取当前时间距离1970年1月1号过了多少毫秒数
//方法一：
var date = new Date();
console.log(date.getTime());
console.log(date.valueOf());
//方法二：（最常用的方法）
var date1 = +new Date();
console.log(date1);
//方法三：（新增的方法）
console.log(Date.now());
```

* **倒计时函数**

```js
//倒计时
function count(time) {
    let dateNow = +new Date();
    let date = +new Date(time);
    let times = (date - dateNow) / 1000;
    //parseInt()将参数解析为整数并返回：
    //Number.parseInt('237.21') 输出结果为237
    let day = parseInt(times / 60 / 60 / 24);
    day = day < 10 ? '0' + day : day;
    let hour = parseInt(times / 60 / 60 % 24);
    hour = hour < 10 ? '0' + hour : hour;
    let min = parseInt(times / 60 % 60);
    min = min < 10 ? '0' + min : min;
    let sec = parseInt(times % 60);
    sec = sec < 10 ? '0' + sec : sec;
    return day + '天' + hour + '时' + min + '分' + sec + '秒';
}
console.log(count('2021-12-28 17:0:0'));
```

##### 4.5 数组对象

###### 1). 创建数组的两种方式

```js
//利用字面量创建了一个数组
var arr1 = ['apple', 'banana']
//利用new关键字创建了一个空数组
var arr2 = new Array();
////利用new关键字创建了一个长度为3的空数组，里面有三个空的数组元素
var arr3 = new Array(3);
```

###### 2). 检测一个对象是不是数组

1. ###### instanceof

   是数组则返回true，反之返回false；

   ```js
   function reverse(arr) {
       //如果不是数组
       if (!(arr instanceof Array)) {
           alert('您输入的不是一个数组！')
       } else {
           let arrCopy = [];
           let i = arr.length - 1;
           for (; i >= 0; i--) {
               arrCopy.push(arr[i]);
           }
           return arrCopy;
       }
   }
   /* arr = [1, 2, 3, 4] */
   arr = 123;
   console.log(reverse(arr));
   //结果是弹窗输出“您输入的不是一个数组！”
   ```

2. ###### Array.isArray（）

   是数组则返回true，反之返回false；`H5新增的方法ie9以 上版本支持`

   ```js
   //翻转数组
   function reverse(arr) {
       //if (!(arr instanceof Array)) {
       if (Array.isArray(arr)) {
           let arrCopy = [];
           let i = arr.length - 1;
           for (; i >= 0; i--) {
               arrCopy.push(arr[i]);
           }
           return arrCopy;
       } else {
           alert('您输入的不是一个数组！')
       }
   }
   /* arr = [1, 2, 3, 4] */
   arr = 123;
   console.log(reverse(arr));
   ```

###### 3). 修改数组元素

* ***添加数组元素***

1. **push()**
   * push()在我们数组的`末尾`添加`一个或者多个数组元素`；
   * push()的参数是要添加的数组元素；
   * push完毕之后，`返回的结果是新数组的长度`，原数组也会被更改。
2. **unshift()**
   * unshift()在我们数组的`头部`添加`一个或者多个数组元素`；
   * unshift()的参数是要添加的数组元素；
   * unshift完毕之后，`返回的结果是新数组的长度`，原数组也会被更改。

```js
//输出pop()的返回值
console.log(arr.push(111));
//输出处理后的数组
console.log(arr); 

//输出pop()的返回值
console.log(arr.unshift(222));
//输出处理后的数组
console.log(arr);
```

* ***删除数组元素***

1. **pop()**

   * pop()从数组中`删除最后一个`元素；
   * pop()方法`不需要参数`；
   * pop完毕之后，`返回的结果是被删去的元素`，`原数组也会被更改`。

2. **shift()**

   * shift()从数组中`删除第一个`元素；
   * shift()方法`不需要参数`；
   * shift完毕之后，`返回的结果是被删去的元素`，`原数组也会被更改`。

3. splice()

   * `删除或替换`指定位置的元素

   * splice完毕之后，`返回的结果是被删去的元素`，`原数组也会被更改`。

   * ```
     array.splice(start[, deleteCount[, item1[, item2[, ...]]]])
     ```

     - `start`

       指定修改的开始位置（从0计数）。如果超出了数组的长度，则从数组末尾开始添加内容；如果是负值，则表示从数组末位开始的第几位（从-1计数，这意味着-n是倒数第n个元素并且等价于`array.length-n`）；如果负数的绝对值大于数组的长度，则表示开始位置为第0位。

     - `deleteCount` 可选

       整数，表示要移除的数组元素的个数。

       如果 `deleteCount` 大于 `start` 之后的元素的总数，则从 `start` 后面的元素都将被删除（含第 `start` 位）。

       如果 `deleteCount` 被省略了，或者它的值大于等于`array.length - start`(也就是说，如果它大于或者等于`start`之后的所有元素的数量)，那么`start`之后数组的所有元素都会被删除。

       如果 `deleteCount` 是 0 或者负数，则不移除元素。这种情况下，至少应添加一个新元素。

     - `item1, item2, *...*` 可选

       要添加进数组的元素,从`start` 位置开始。如果不指定，则 `splice()` 将只删除数组元素。

   

```js
//输出pop()的返回值
console.log(arr.pop());
//输出处理后的数组
console.log(arr);

//输出shift()的返回值
console.log(arr.shift());
//输出处理后的数组
console.log(arr);
```

* ***对数组元素排序***

1. **原生sort()**

   sort()方法用[原地算法](https://en.wikipedia.org/wiki/In-place_algorithm)对数组的元素进行排序，并`返回数组`。`默认排序顺序是在将元素转换为字符串，然后比较它们的UTF-16代码单元值序列时构建的`。由于它取决于具体实现，因此无法保证排序的时间和空间复杂性。；

   ```js
   const months = ['March', 'Jan', 'Feb', 'Dec'];
   months.sort();
   console.log(months);
   // expected output: Array ["Dec", "Feb", "Jan", "March"]
   
   const array1 = [1, 30, 4, 21, 10, 7, 66];
   array1.sort();
   console.log(array1);
   //输出的结果：[ 1, 10, 21, 30, 4, 66, 7 ]
   ```

2. **改进后的sort()**

   > arr.sort（[compareFunction]）

   如果没有指明 `compareFunction` ，`那么元素会按照转换为的字符串的诸个字符的Unicode位点进行排序`。例如 "Banana" 会被排列到 "cherry" 之前。当数字按由小到大排序时，9 出现在 80 之前，但因为（没有指明 `compareFunction`），比较的数字会先被转换为字符串，所以在Unicode顺序上 "80" 要比 "9" 要靠前。

   如果指明了 `compareFunction` ，那么数组会按照调用该函数的返回值排序。即 a 和 b 是两个将要被比较的元素：

   - 如果 `compareFunction(a, b)` 小于 0 ，那么 a 会被排列到 b 之前；

   - 如果 `compareFunction(a, b)` 等于 0 ， a 和 b 的相对位置不变。备注：ECMAScript 标准并不保证这一行为，而且也不是所有浏览器都会遵守（例如 Mozilla 在 2003 年之前的版本）；

   - 如果 `compareFunction(a, b)` 大于 0 ， b 会被排列到 a 之前。
   - `compareFunction(a, b)` 必须总是对相同的输入返回相同的比较结果，否则排序的结果将是不确定的。

* `要比较数字而非字符串`，比较函数可以简单的以 a 减 b，如下的函数将会将数组升/降序排列

  ```js
  /*function compareNumbers(a, b) {
    //return a - b;升序排列
    return b - a;//降序排列
  }*/
  
  var arr1 = [13, 4, 77, 1, 7];
  arr1. sort(function(a, b) {
  // return a - b;升序的顺序排列
  return b - a; //降序的顺序排列
  };
  console . log(arr1);
  ```

* `对象可以按照某个属性排序`：

  ```js
  var items = [
    { name: 'Edward', value: 21 },
    { name: 'Sharpe', value: 37 },
    { name: 'And', value: 45 },
    { name: 'The', value: -12 },
    { name: 'Magnetic' },
    { name: 'Zeros', value: 37 }
  ];
  
  // sort by value
  items.sort(function (a, b) {
    return (a.value - b.value)
  });
  
  // sort by name
  items.sort(function(a, b) {
    var nameA = a.name.toUpperCase(); // 忽略大小写
    var nameB = b.name.toUpperCase(); // 忽略大小写
    if (nameA < nameB) {
      return -1;
    }
    if (nameA > nameB) {
      return 1;
    }
  
    // name必须完全一样
    return 0;
  });
  ```

###### 4). 获取数组元素的索引

1. **indexof()**

   数组中查找给定元素的`第一个`索引，如果存在返回索引号如果`不存在`，`则返回-1`。

   ```js
   var arr = [1, 'TOLIE', 'James', 'wang', 'TOLIE', 'TOLIE', 'wang']
   console.log(arr.indexOf('TOLIE'));//结果是 1
   //indexOf( '要查找的元素'，[起始的位置])
   console.log(arr.indexOf('TOLIE',2));//结果是 4
   ```

2. **lastIndexof()**

   数组中查找给定元素的`最后一个`索引，如果存在返回索引号如果`不存在`，`则返回-1`。

   ```js
   var arr = [1, 'TOLIE', 'James', 'wang', 'TOLIE', 'TOLIE', 'wang']
   console.log(arr.indexOf('TOLIE'));//结果是 1
   console.log(arr.lastIndexOf('TOLIE'));//结果是 5
   ```

###### 5). 数组元素去重

1. **自己的方法**

```js
var arr = [1, 'TOLIE', 1, 1, 'James', 1, 1, 'wang', 'TOLIE', 'TOLIE', 'wang']
function removeSame(array) {
    let arrCopy = [];
    for (let i = 0; i < array.length; i++) {
        if (i === array.lastIndexOf(array[i])) {
            arrCopy.push(array[i])
        }
    }
    return arrCopy;
}
console.log(removeSame(arr));
//[ "James", 1, "TOLIE", "wang" ]
```

2. **利用indexOf()**

   利用新数组.indexOf(数组元素)，如果返回时-1就说明新数组里面没有该元素；

```js
function unique(array) {
    let arrNew = [];
    for (let i = 0; i < array.length; i++) {
        //如果数组里没有该元素，则返回-1
        if (arrNew.indexOf(array[i]) === -1) {
            arrNew.push(array[i]);
        }
    }
    return arrNew;
}
```

3. ***不能实现去重？？？？***

```js
var arr = [1, 'TOLIE', 1, 1, 'James', 1, 1, 'wang', 'TOLIE', 'TOLIE', 'wang']
 /*不能实现去重????????????????????*/
function removeSame(array) {
    for (let i = 0; i < array.length; i++) {
        if (!(i === array.lastIndexOf(array[i]))) {
            //从索引 i 的位置开始删除 1 个元素
            array.splice(i, 1);
        } 
    }
    return arrCopy;
}
console.log(removeSame(arr));
```

###### 6). 数组转化为字符串

1. **toString()**

   `toString()` 返回一个字符串,逗号分隔每一项，表示指定的数组及其元素。

   ```js
   var arr = [1, 'TOLIE', 1, 1, 'James', 1, 1, 'wang', 'TOLIE', 'TOLIE', 'wang']
   console.log(arr.toString());
   //1,TOLIE,1,1,James,1,1,wang,TOLIE,TOLIE,wang
   ```

2. join('分隔符')

   `join()` 方法将一个数组（或一个[类数组对象](https://developer.mozilla.org/zh-CN_docs/Web/JavaScript/Guide/Indexed_collections#working_with_array-like_objects)）的所有元素连接成一个字符串并返回这个字符串。如果数组只有一个项目，那么将返回该项目而不使用分隔符。

   ```js
   const elements = ['Fire', 'Air', 'Water'];
   console.log(elements.join());
   // expected output: "Fire,Air,Water"
   
   console.log(elements.join(''));
   // expected output: "FireAirWater"
   
   console.log(elements.join('-'));
   // expected output: "Fire-Air-Water"
   ```


##### 4.6.1 字符串对象

###### 1).基本包装类型

* 基本包装类型：就是把简单数据类型包装成为了复杂数据类型
* JavaScript中有三种基本包装类型：`String、Number和Boolean`。

**步骤**：

1. 把简单数据类型包装为复杂数据类型；
2. 把临时变量的值给str；
3. 销毁这个临时变量。

```js
var str = 'tolie';
console.log(str.length);//5
/*对象才有属性和方法 复杂数据类型才有属性和方法
简单数据类型为什么会有lenght属性呢?*/

//以上步骤的本质是
var temp = new String('tolie');
var str = temp;
temp = null;
console.log(str.length);//5
```

###### 2).字符串的不可变

`字符串的不可变指的是里面的值不可变`，虽然看上去可以改变内容，但`其实是地址变了，内存中新开辟了一个内存空间`。

```js
var str = 'abc';
str = 'hello';
//当重新给str赋值的时候，常量'abc'不会被修改，依然在内存中
//重新给字符串赋值，会重新在内存中开辟空间，这个特点就是字符串的不可变
//由于字符串的不可变，在大量拼接字符串的时候会有效率问题
var str = '';
for (var i = 0; i < 100000; i++) {
    str += i;
}
console.log(str); //这个结果需要花费大量时间来显示，因为需要不断的开辟新的空间=
```

###### 3).根据字符返回位置

> `字符串所有的方法`，`都不会修改字符串本身`（字符串是不可变的)），操作完成会`返回一个新的字符串`。

* 查找字符串中某个字符出现的次数

  [JavaScript中return返回多个值的三个方法](https://blog.csdn.net/loongkingwhat/article/details/83350504)

  ```js
  function selectStr(str, letter) {
      let arr = [];
      let m = 0;
      var i = str.indexOf(letter);
      //
      while (i !== -1) {
          //console.log(i);
          arr.push(i);
          m++;
          i = str.indexOf(letter, i + 1);
      }
      return {
          loc: arr.toString(),
          num: arr.length
      };
  }
  var obj = selectStr('jafigiuoauhju', 'u');
  console.log(obj.loc);// 7,9,12
  console.log(obj.num);// 3
  ```

###### 4).根据位置返回字符 *

1. charAt(index)

   返回指定索引号位置的字符（index 字符串的索引号）

   ```js
   var str = 'jafigiuoauhju'
   for (let i = 0; i < str.length; i++) {
       console.log(str.charAt(i));
   }
   ```

2. charCodeAt(index)

   获取指定位置处字符的`ASCII码` （index索引号）

   用来判断用户按了哪个键；

   ```js
   console.log(str.charCodeAt(0));
   ```

3. str[index]

   获取指定位置处字符 `HTML5， IE8+支持` ，和charAt()等效

   ```js
   var str = 'jafihju'
   for (let i = 0; i < str.length; i++) {
       console.log(str[i]);
   }
   ```

4. **判断一个字符串'abcoefoxyozzopp' 中出现次数最多的字符，并统计其次数**。

   * *方案一*

   ```js
   function countMost(str) {
       let arr = [];
       let n = 0;
       let letter = '';
       for (let i = 0; i < str.length; i++) {
           if (arr.indexOf(str.charAt(i)) == -1) {
               arr.push(str.charAt(i));
           }
       } //return arr;
       for (let i = 0; i < arr.length; i++) {
           if (selectStr(str, arr[i]).num > n) {
               n = selectStr(str, arr[i]).num;
               letter = arr[i];
           }
       } //return n;
       console.log('出现次数最多的字符是' + letter + '，出现了' + n + '次');
   }
   countMost('abcoefoxyozzopp')
   //出现次数最多的字符是o，出现了4次
   ```

   * *方案二*

   ```js
   function countMost2(str) {
       //1、创建对象
       let obj = {};
       let max = 0;
       let letter = '';
       for (let i = 0; i < str.length; i++) {
           let chars = str.charAt(i);
           //判断是否有chars属性
           //没有，新建chars属性，并赋值为1
           //有，让chars属性属性值加一
           if (obj[chars]) {
               obj[chars]++;
           } else {
               obj[chars] = 1;
           }
       }
       //2、遍历对象
       for (let k in obj) {
           if (max < obj[k]) {
               max = obj[k];
               letter = k;
           }
       } 
       return {
           mostLetter: letter,
           times: max
       }
   }
   console.log('出现次数最多的字符是' + countMost2('abcoefoxyozzopp').mostLetter + '，出现了' + countMost2('abcoefoxyozzopp').times + '次');
   ```

###### 5).拼接和截取字符串

1. *concat(str1 ,str2,tr3...)*
   concat()方法用于连接两个或多个字符串。拼接字符串，`等效于+`，+更常用

2. *substr(start,length)*
   从start位置开始（索引号），`length 是取的个数，省略就默认取到最后一个`。重点记住这个

3. *slice(start, end)*
   从start位置开始，截取到end位置,，`end取不到`（他们俩都是索引号）

4. *substring(start, end)*

   从start位置开始，截取到end位置， end取不到；基本和slice 相同，但是不`接受负值`、

   ```js
   var str = 'to be better';
   
   //在字符串后面添加一段内容
   console.log(str.concat('12138'));
   
   //3是从1开始数，2是想要取的字符个数
   console.log(str.substr(3, 2));
   ```

###### 6).替换字符和字符转换为数组

1. *replace(' 被替换的字符'，' 替换为的字符')*

   > 它只会替换第一个字符；

   ```js
   var str = 'to be better';
   console.log(str.replace('b', 'B'));
   //to Be better，只替换了第一个b
   
   //将字符串中某一个字符全部替换为另一个字符
   function replaceLetter(str, letter1, letter2) {
       while (str.indexOf(letter1) !== -1) {
           str = str.replace(letter1, letter2);
       }
       return str;
   }
   console.log(replaceLetter('kangopaolkgqoppo', 'o', '*'));
   //kang*pa*lkgq*pp*
   ```

2. *split( '分隔符')* 

   `字符转换为数组`；与之相对的是前面我们学过join('分隔符')把数组转换为字符串

   ```js
   var Str = 'red,blue,pink';
   console.log(Str.split(','));
   //[ "red", "blue", "pink" ]
   ```

###### 7).字符串大小写转换

1. toUpperCase()
   字符串的英文字符全部转换为大写；

   ```js
   var Str = 'red,blue,Pink';
   console.log(Str.toUpperCase());
   //RED,BLUE,PINK
   ```

   tolowerCase(
   字符串的英文字符全部转换为小写；

   ```js
   var Str = 'red,blue,Pink';
   console.log(Str.toLowerCase());
   //red,blue,pink
   ```

#### 第五章 JS的简单数据类型和复杂数据类型

###### 1).简单数据类型和复杂数据类型及其内存分配

简单数据类型又叫做基本数据类型或者`值类型`，复杂数据类型又叫做`引用类型`

1. **值类型**：简单数据类型/基本数据类型，在`存储时变量中存储的是值本身`，所以叫做值类型。

   * 包括：string、number、boolean、undefined、`null`
   * `null返回的是一个空的对象` object，如果有一个变量以后打算存储为对象，就可以赋值为null

   ```js
   var timer = null;
   console.log(typeof timer);
   //object
   ```

2. **引用类型**：复杂数据类型，在`存储时变量中存储的只是地址（引用）`，因此叫做引用数据类型；

   * 通过`new关键字`创建的对象（系统对象，自定义对象），如Object、Array、Date等

3. **存储的“堆和栈”**

   > **注意**：`JavaScript中没有堆栈的概念`，这里只是通过堆栈的方式进行理解

   * **栈**（操作系统）：由操作系统自动分配存放函数的参数值、局部变量的值等。其操作方式类似于数据结构中的“栈”。`简单数据类型存放在栈里面`。
   * **堆**（操作系统）：存储复杂类型（对象），一般由程序员分配释放，如果程序员不释放，则由垃圾回收机制回收。`复杂数据类型存放在堆里面`，栈里存放存储的是复杂数据类型的地址。

   ![数据的存储](https://gitee.com/mr_tolie/pics/raw/master/images/33BDEC12E9AB0D0975F3DB44D276A368.jpg)

###### 2).简单数据类型传参

```js
function fn(a) {
    a++;
    console.log(a);
}
var x = 10;
fn(x);
console.log(x);
//  11  10
```

函数的形参也可以看做是一个变量，当我们把`一个值类型变量作为参数传给函数的形参`时，`其实是把变量在栈空问里的值复制了一份给形参`，那么在方法内部对形参做任何修改，都`不会影响到的外部变量`。

![简单数据类型传参](https://gitee.com/mr_tolie/pics/raw/master/images/87a7d82-6f88bf53-113-0.png)

###### 3).复杂数据类型传参

函数的形参也可以看做是一个变量，当我们把引用类型变量传给形参时， `实际上是把变量在栈空间里保存的堆地址复制给了形参`，形参和实参其实保存的是同一一个堆地址，所以操作的是同一一个对象。

```js
function f1(x) { //x= p
    console.log(x.name); // 2.这个输出什么?  刘德华
    x.name = "张学友";
    console.1ogl(x.name); // 3.这个输出什么?  张学友
    }
var p = new Person ("刘德华");
console.log(p.name); // 1.这个输出什么?  刘德华

f1(p);
console.log(p.name); // 4. 这个输出什么?  张学友
```

### 第二部分 Web APIs

**JS基础和Web APIs的关系**

![JS基础和Web APIS的关系](https://gitee.com/mr_tolie/pics/raw/master/images/image-20220102151923793.png)

JS基础学习ECMAScript 基础语法为后面作铺垫，Web APIs是JS的应用,大量使用JS基础语法做交互效果![两部分的要求](https://gitee.com/mr_tolie/pics/raw/master/images/image-20220102152136255.png)

**API和Web API**

* **API** ( Application Programming Interface，应用程序编程接口)是一些预先定义的函数，目的是提供应用程序与开发人员基于某软件或硬件得以访问一组例程的能力，而又无需访问源码，或理解内部工作机制的细节。`简单理解为API是给程序员提供的一种工具,以便能更轻松的实现想要完成的功能。`
* **Web API**是`浏览器`提供的一套操作`浏览器功能和页面元素`的API（ BOM和DOM）。

#### 第六章 DOM

##### 6.1 什么是DOM

`文档对象模型`( Document Object Model ,简称DOM) ,，是W3C组织推荐的处理可扩展标记语言( HTML或者XML )的标准编程`接口`。

W3C已经定义了一系列的DOM接口，通过这些DOM接口可以改变网页的内容、结构和样式。

##### 6.2 DOM树

* 文档：一个页面就是一个文档，*DOM中使用document表示*；
* 元素：页面中的所有标签都是元素， *DOM中使用element表示*；
* 节点：网页中的所有内容都是节点(标签、属性、文本、注释等) ， *DOM中使用node表示*；
* DOM把以上的内容都看做是`对象`；

![DOM树](https://gitee.com/mr_tolie/pics/raw/master/images/image-20211224140057312.png)



##### 6.3 动态创建元素方法

> 1. document.write()
> 2. element.innerHTML
> 3. document.createElement ()

**区别**

* document .write是直接将内容写入页面的内容，但是`如果文档流执行完毕，再执行这句话就会导致页面全部重绘；即重新创建一个新的HTML页面`。

```js
window.onload = function(){
	document.write('<div>123</div>');
}
```

* innerHTML是将内容写入某个DOM节点，`不会导致页面全部重绘`；
* innerHTML 创建多个元素效率更高(`不要拼接字符串，采取数组形式拼接`) , 结构稍微复杂；
* createElement() 创建多个元素效率稍低一点点，但是结构更清晰；



##### 6.4 获取元素

###### 1).通过ID获取元素

```js
//获取到id为date的元素
var div = document.getElementById('date');
```

###### 2).通过标签名获取元素

​	document . getElementsByTagName ('标签' )，其返回的是`获取过来元素对象的集合`以`伪数组`的形式存储的。

```js
//获取到页面中第一个div标签
var div = document.getElementsByTagName('div')[0];
```

###### 2).通过类名获取元素

​	document . getElementsByClassName('类名' ) ，其返回的是`获取过来元素对象的集合`也是以`伪数组`的形式存储的。（`HTML5新增`）

```js
//获取到页面中第一个classname为date的标签
var div = document.getElementsByClassName('date')[0];
```

###### 4).根据指定选择器获取元素

​	document . querySelector (选择器') ，其`返回第一个元素对象`。（`HTML5新增`）

​	**注意**：切记里面的选择器需要加符号.box   #name

```js
//获取到页面中第一个id为date的标签
var div = document.querySelector('#date');
```

###### 5).根据指定选择器获取元素

​	document . querySelectorAll(选择器')，其返回的是`获取过来元素对象的集合`也是以`伪数组`的形式存储的。（`HTML5新增`）

```js
//获取到页面中所有id为date的标签，并在返回的数组中选择了第一个
var div = document.querySelectorAll('#date')[0];
```

###### 6).获取body和html元素

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="date">你好，JS</div>

	<!-- 推荐的<script>标签书写位置 -->
    <script>
        // 1.获取body元素
        var bodyEle = document.body;
       
        console.log(bodyEle);
        console.dir(bodyEle);

        // 2.获取html元素
        // var htmlEle = document.html;不能获取页面的HTML元素
        var htmlEle = document.documentElement;
       
        console.log(htmlEle);
    </script>
</body>
</html>
```



##### 6.5 事件基础

JavaScript使我们有能力创建动态页面，而事件是可以被JavaScript侦测到的行为。可以简单理解为`触发——响应机制`。
网页中的每个元素都可以产生某些可以触发JavaScript的事件，例如,我们可以在用户点击某按钮时产生一个事件，然后去执行某些操作。

###### 1).事件三要素

事件是有三部分组成：包括事件源、事件类型、事件处理程序，我们也称为事件三要素。

1. 事件源

   即事件被触发的对象；

2. 事件类型

   即通过什么情况下才可以触发事件：比如鼠标点击（onclick）；

3. 事件处理程序
   一般是通过一个函数赋值的方式指明触发事件后的下一步处理。

```js
//1.获取事件源
var btn = document.getElementsByTagName('button')[0];
//2.指明事件类型
btn.onclick = function () {//3.定义事件处理程序（方法）
alert('你好，我是一个按钮！')
}
```

###### 2).事件类型

[HTML 事件参考手册](https://www.w3school.com.cn/tags/html_ref_eventattributes.asp)

| 事件        | 事件发生时间                         |
| :---------- | :----------------------------------- |
| onclick     | 用户点击 HTML 元素发生               |
| onmouseover | 鼠标指针移动到指定的元素上时发生     |
| onmouseout  | 用户从一个 HTML 元素上移开鼠标时发生 |
| onblur      | 失去鼠标焦点时触发                   |
| onfocus     | 获得鼠标焦点时触发                   |
| onkeydown   | 用户按下键盘按键触发                 |
| onload      | 浏览器已完成页面的加载时触发         |
| onchange    | HTML 元素改变时触发                  |

###### 3).事件流

？？？？

##### 6.6 操作元素

![操作元素](https://gitee.com/mr_tolie/pics/raw/master/images/image-20220105171433240.png)

###### 1).改变元素内容

1. ###### element. innerText

   从起始位置到终止位置的内容，但`它去除html标签，同时空格和换行也会去掉`；***不识别html标签，非标准***

```js
//1.获取元素
var div = document.getElementById('date');
//2.绑定事件
div.onclick = function () {//3.事件
    let date = new Date();
    //div.innerText = getMyDate();
    div.innerText = date.toString();
}

//也可以不绑定事件
var div = document.getElementById('date');
div.innerText = Date().toString();
```

1. ###### element. innerHTML

   `起始位置到终止位置的全部内容，包括html标签，同时保留空格和换行`；***识别html标签，W3C标准***

```js
var div = document.querySelectorAll('#date')[0];
div.innerText = '<b>今天是</b>周日';
//页面显示<b>今天是</b>周日

var div = document.querySelectorAll('#date')[0];
div.innerHtml = '<b>今天是</b>周日';
```

![是否识别HTML标签](https://gitee.com/mr_tolie/pics/raw/master/images/image-20220102174446957.png)

```js
/*    <div id="text" class="date">
        你好
        <span>12345</span>
    </div>*/
var div2 = document.querySelectorAll('.date')[1];
console.log(div2.innerText);
console.log(div2.innerHTML);
/*输出结果
    你好 12345 
            你好
           <span>12345</span>*/
```

![是否保留空格和换行](https://gitee.com/mr_tolie/pics/raw/master/images/image-20220102174345703.png)

###### 2).改变元素属性（以img标签为例

```js
//<button>背景图</button>
//<button>蛋糕</button>
//<div><img src="img/cake-1.jpg" alt="图片" title="蛋糕一号"></div>

var img = document.querySelector('img')
var button1 = document.querySelectorAll('button')[0];
var button2 = document.querySelectorAll('button')[1];
button1.onclick = function () {
    img.src = 'img/indexbg.jpg';
    img.title = '背景图';
}
button2.onclick = function () {
    img.src = 'img/cake-2.jpg';
    img.title = '蛋糕二号';
}
```

###### 3).改变表单属性

```js
 //<input type="text" value="!!!">
    //<button id="btn">登录</button>

var btn = document.querySelector('button');
var input = document.querySelector('input');
btn.onclick = function () {

    input.value = '13333！';
    //btn.disabled = true;
    this.disabled = true;
    //this指向事件函数的调用者，这里是btn
}
```

***仿京东登录界面***

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>仿JD密码明文展示</title>
    <style>
        div {
            position: relative;
            /* 子绝父相 */
            width: 343px;
            height: 60px;
            margin: 1.5em;

        }

        #tittle {
            text-align: center;
            letter-spacing: 0.25em;
        }


        #tittle b {
            font-weight: normal;
            /* 取消加粗 */
            font-size: 23px;
        }

        input {
            padding: 0;
            width: 343px;
            height: 38px;
            border: 0;
            border-bottom: 1px solid #ccc;
            /* 下方边框的宽度，solid，颜色 */
            outline: none;
            /* 取消选中时的边框效果 */
        }

        label {
            font-weight: lighter;
            display: inline-block;
        }

        label img {
            position: absolute;
            /* 子绝父相 */
            top: 26px;
            right: 10px;
            width: 24px;
            cursor: pointer;
        }

        #password {
            padding: 0;
            display: inline-block;
            /* 转换为行内块元素 */
        }

        #login {
            width: 343px;
            height: 38px;
            background-color: #a41619;
            font-size: 18px;
            letter-spacing: 1.5em;
            /* 字符间距 */
            color: white;
            border: none;
            /* 边框 */
            margin-top: 1em;
            cursor: pointer;
            /* 鼠标移动至上方变成小手 */
        }
    </style>
</head>

<body>
    <div id="all">
        <form action="" method="POST">
            <div id="tittle"><b>京东登录</b></div>

            <div><label for="name">用户名</label><input type="text" id="name"></div>

            <div>
                <label for="password">密&nbsp;码</label>
                <input type="password" id="password" flag=0>
                <label><img src="img/眼睛_隐藏_o.png" alt=""></label>
            </div>

            <div><button id="login"><b>登录</b></button></div>
        </form>
    </div>

    <script>
        var img = document.getElementsByTagName('img')[0];
        var pwd = document.getElementById('password')
        img.onclick = function () {

            if (pwd.flag == 1) {
                img.src = 'img/眼睛_隐藏_o.png';
                pwd.type = 'password';
                pwd.flag = 0;
            } else {
                img.src = 'img/眼睛_显示_o.png';
                pwd.type = 'text';
                pwd.flag = 1;
            }
        }
    </script>
</body>

</html>
```

###### 4). 样式属性操作

* element. style**行内样式操作**

使用element.style 主要在`样式比较少或者功能简单`的情况下。

`其本质不是修改样式值，而是在行内添加新的样式，因为行内样式要优先于内嵌或外部样式，所以实现了样式改变`

```js
const box = document.querySelector('.box');
const x = document.querySelector('.box i');
x.onclick = function () {
//设定box的display属性为none，将其隐藏；
//box的display属性为block，将其显示出来；
box.style.display = 'none';
}
```

* element. className**类名样式操作**

使用element. className更改元素的样式适合于`样式较多或者功能复杂的情况`。

`其本质是在标签内添加/修改类名的方式，使标签应用写好的样式`

`如果想要保留之前的样式，就应用多类名选择器 class =’first second‘`

***密码验证提示信息***

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>密码验证提示信息</title>
    <style>
        div {
            width: 400px;
            margin: 100px auto;
        }

        .message {
            display: inline-block;
            /* 让背景不与文字重复 */
            padding-left: 18px;
            /* 字体颜色 */
            color: #999;
            /* 字体大小 */
            font-size: 8px;
            /* background的图片，是否重复，背景图片的位置 */
            background: url("img/提示.png") no-repeat left center;
            background-size: 16px;
        }

        .msg_wor {
            color: #fd6b6d;
            background: url("img/错误-红.png") no-repeat left center;
            background-size: 16px;
        }

        .msg_rig {
            color: #52c41a;
            background: url("img/成功-绿.png") no-repeat left center;
            background-size: 16px;
        }

    </style>
</head>
<body>
<div>
    <input type="password">
    <p class="message">请输入8-16位密码</p>
</div>
<script>
    const pwd = document.querySelector('input');
    const msg = document.querySelector('.message');
    pwd.onblur = function () {
        if (pwd.value.length < 8 || pwd.value.length > 16) {
            //给p标签添加多类名样式
            msg.className = 'message msg_wor';
            //修改p标签里的内容
            msg.innerHTML = '请输入正确位数的密码！';

        } else {
            //给p标签添加多类名样式
            msg.className = 'message msg_rig';
            //修改p标签里的内容
            msg.innerHTML = '密码位数正确！';
        }
    }
</script>
</body>
</html>
```

###### 5).排他思想

如果有同一组元素，我们想要某一个元素实现某种样式，需要用到循环的排他思想算法:

1. 所有元素全部清除样式（**干掉其他人**）

2. 给当前元素设置样式（**留下我自己**）

> `注意顺序不能颠倒`，首先干掉其他人，再设置自己

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>排他思想</title>
</head>

<body>
    <button>按钮1</button>
    <button>按钮2</button>
    <button>按钮3</button>
    <button>按钮4</button>
    <button>按钮5</button>
    <script>
        //获取所有的button对象，得到的是一个伪数组
        const btns = document.getElementsByTagName('button');
        for (i = 0; i < btns.length; i++) {
            btns[i].onclick = function () {
                //利用循环，清除其他的所有样式
                for (i = 0; i < btns.length; i++) {
                    btns[i].style.backgroundColor = '';
                }
                this.style.backgroundColor = 'pink';
                //this指向每一个调用function方法的对象
            }
        }
    </script>
</body>
</html>
```

##### 6.7 自定义属性

`自定义属性目的：是为了保存并使用数据。有些数据可以保存到页面中而不用保存到数据库中。`

H5给我们新增了自定义属性:

1. **设置H5自定义属性**

> H5规定自定义属性`data-`开头做为`属性名并且赋值`。比如&lt;div data-index="1"&gt;&lt;/div&gt;”

###### 1).获取自定义属性值

程序员自己添加的属性我们称为`自定义属性`。

1. element.属性名

```js
var box = document.getElementById('box');
console.log(box.id);
```

2. element.getAttribute('属性名')

```js
var box = document.getElementById('box');
console.log(box.id);
console.log(box.getAttribute('id'));
```

3. 两者区别

* **element.属性**：`获取内置属性值`（元素本身自带的属性）
* **element.getAttribute( '属性')**：`主要获得自定义的属性 （标准）我们程序员自定义的属性`。也可以获取内置属性

4. **H5新增**elerment.dataset. *index *或者 element.dataset[ '*index*' ] 

   `ie 11才开始支持`

```JS
// h5新增的获取自定义属性的方法
var box = document.getElementById('box');
console.log(box.dataset.index); //这里的dataset是一个集合里面存放了所有以data开头的自定义属性。
console.log(box.dataset['index']);


//如果自定义属性里面有多个 '-' 链接的单词，我们获取的时候采取驼峰命名法
console.log(div.dataset.listName)
```

###### 2).设置自定义属性

1. 设置内置属性值

   > element.属性='值’

2. 设置自定义属性值

   > element.setAttribute('属性'，'值') ;

3. `setAttribute也可以用来修改内置属性值`

###### 2).移除自定义属性

> element.removeAttribute ('属性') ;

```js
// 2.设置元素属性值
// (1) element.属性= '值'
div.id = 'test' ;
div.className = 'navs' ;

// (2) element. setAttribute('属性'，'值');主要针对于自定义属性
div.setAttribute('index', 2);
div.setAttribute( 'class', 'footer'); 
//一个是class 一个是classname 注意区分

div.removeAttribute('index')
```

##### 6.8 节点操作

###### 1). 节点获取

![节点操作](https://gitee.com/mr_tolie/pics/raw/master/images/image-20220108113431959.png)

HTML `DOM树中的所有节点均可通过JavaScript进行访问`，所有HTML元素(节点)均可被修改，也可以创建或删除。

###### 2). 节点属性

一般地 ,节点至少拥有`nodeType (节点类型)`、`nodeName (节点名称)`和`nodeValue (节点值)`这三个基本属性。

> 元素节点的 nodeType 为 1
>
> 属性节点的 nodeType 为 2
>
> 文本节点的 nodeType  为 3 (文本节点包含文字、空格、换行等)

###### 3). 节点层级

利用DOM树可以把节点划分为不同的层级关系，`常见的父子兄层级关系`。

1. ###### 父级节点

```js
//const box = document.querySelector('.box');
        const x = document.querySelector('.box i');
        /* x.onclick = function () {
            //设定box的display属性为none，将其隐藏；
            //box的display属性为block，将其显示出来；
            box.style.display = 'none';
        } */

        //x.parentNode即上方获取的box节点
        //element.parent获取的是离此节点最近的父级节点
        //如果找不到父节点，则返回 null
        x.onclick = function () {
            x.parentNode.style.display = 'none';
        }
```

2. ###### 子级节点

> parentNode.chilaNodes (标准)
>
> //获取所有子节点，包含：元素节点、文本节点等等

parentNode. childNodes返回`包含指定节点的子节点的集合，包含：元素节点、文本节点等等`，该集合为`即时更新`的集合。

如果只想要获得里面的元素节点,则需要专[处理。所以我们一 般不提倡使用childNodes方法。

> parentNode. children (非标准)
>
> //获取所有的子级元素节点

parentNode. children是一个只读属性，`返回所有的子元素节点的集合`。它只返回子元素节点，其他节点不返回**(这个是我们重点掌握的)**。

虽然children是一个非标准 ，但是得到了各个浏览器的支持，可以放心使用，**兼容性良好**。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="box" index="1">
        <ul>
            <li>1</li>
            <li>2</li>
            <li>3</li>
            <li>4</li>
        </ul>
        <ol>
            <li>5</li>
            <li>6</li>
            <li>7</li>
            <li>8</li>
        </ol>
    </div>
    <script>
        var ul = document.querySelector('ul');
        //childNodes 获得的是所有的子节点，包含：元素节点、文本节点等等
        console.log(ul.childNodes);
        //获取所有的子级元素节点
        console.log(ul.children);
    </script>
</body>

</html>
```

![获取子级节点](https://gitee.com/mr_tolie/pics/raw/master/images/image-20220108121041889.png)





> parentNode.firstChild

parentNode . firstChild返回`第一个子节点`，找不到则返回 null 。`同样，也是包含所有的节点`。

> parentNode.lastChild

parentNode .lasttChild返回`最后一个子节点`，找不到则返回 null 。`同样，也是包含所有的节点`。



<span style='color:red; font-weight:bold;font-size:18px'>注意:以下这两个方法有兼容性问题，IE9以上才支持，可能存在兼容性问题。</span>

> parentNode.firstElementChild

parentNode . firstElementChild返回`第一个元素子节点`，找不到则返回 null 。

> parentNode.lastElementChild

parentNode . lastElementChild返回`最后一个元素子节点`，找不到则返回 null 。

```js
var ul = document.querySelector('ul');

// 1.firstChild第一个子节点,不管是文本节点还是元素节点
console.log(ul.firstChild);
// 2.lastChild第一个子节点,不管是文本节点还是元素节点
console.log(ul.lastChild);

//注意:以下这两个方法有兼容性问题，IE9以上才支持。
//3. firstElementChild 返回第一个子元素节点
console.log(ul.firstElementChild);
//4. lastElementChild 返回最后一个子元素节点
console.log(ul.lastElementChild);
```

![获取第一个或最后一个节点](https://gitee.com/mr_tolie/pics/raw/master/images/image-20220108124649993.png)

<span style='color:red; font-weight:bold;font-size:18px'>实际开发中，一般使用parentNode.children[parentNode.children.length-1]和parentNode.children[0] 获得最后一个 和 第一个子元素</span>



###### 4). 创建节点

> document.createElement ( 'tagName')

document. createElement()方法创建由tagName 指定的HTMI 元素。因为这些元素原先不存在，是根据我们的需求动态生成的，``所以我们也称为动态创建元素节点`。



###### 5). 添加节点

> node.appendChild (child)  /* node是父级，child是子级 */

`node.appendChild()方法将一个节点添加到指定父节点的子节点列表末尾。`类似于css里面的after伪元素。

> node.insertBefore (child,指定元素)

`node. insertBefore ()方法将一个节点添加到父节点的指定子节点前面`。类似于css里面的before伪元素。

```js
// 1.创建节点元素节点
var li = document.createElement('li');
// 2.添加节点node. appendChild(child) node 父级  child是子级
var ul = document.querySelector('ul');
u1.appendChild(li);/* 将元素添加到ul中，并且位于所有子元素的最后 */
u1.insertBefore(li,ul.children[0]);/* 将元素添加到ul中，并且位于所有子元素的最前面 */
```



###### 6). 删除节点

> node.removeChild (child)

node . removechild()方法从DOM中删除一个子节点，`返回删除的节点`。

> `阻止链接跳转`，可以将a标签的herf属性的值写为javascriptvoid();或者javascript:;



###### 7). 复制节点(克隆节点)

> node. cloneNode ()

node. cloneNode()方法`返回调用该方法的节点的一个副本`。也称为克隆节点/拷贝节点

注意

> 1. 如果括号参数为空或者为false ，则是`浅拷贝`，`即只克隆复制节点本身，不克隆里面的子节点`。
> 2. 括号为true，则为`深拷贝`，`即复制标签同时复制里面的内容`。



#### 第七章 高级事件

##### 7.1 注册/绑定事件

给元素添加事件，称为`注册事件或者绑定事件`。

> 注册事件有两种方式：传统方式和方法监听注册方式;



###### 传统注册方式

即利用on开头的事件onclick等

```js
<button  onclick="alert('hi~")” > </button>
/* 或者 */
btn.onclick = functio(){}
```

**特点**：`注册事件唯一性`。即同一个元素同一个事件只能设置一个处理函数，最后注册的处理函数将会覆盖前面注册的处理函数。



###### 方法监听注册方式

* w3c 标准推荐方式；
* addEventListen( ) 它是一个方法；
* IE9 之前的IE不支持此方法，可使用 attachEvent() 代替；

**特点**：`同一个元素同一个事件可以注册多个监听器，并按注册顺序依次执行`。



**addEventListen( ) 语法**

> eventTarget. addEventListener (type, listener[, useCapture])
>
> */\* 如果使用非匿名函数，则函数不需要加小括号进行调用 \*/*

eventTarget . addEventListener ()方法将指定的监听器注册到eventTarget (目标对象)上,当该对象触发指定的事件时,就会执行事件处理函数。

**该方法接收三个参数**：

1. type :`事件类型字符串`,比如click、mouseaver , `注意这里不要带on，并记得加上引号`
2. listener :事件处理函数,事件发生时，会调用该监听函数
3. useCapture :可选参数，是一个布尔值，默认是false。如果是false ，表示在事件冒泡阶段调用事件处理程序；第三个参数如果是true，表示在事件捕获阶段调用事件处理程序；

```js
// 2.事件侦听注册事件
btns[1].addEventListener('click', function() {
	alert(22);
})

btns[1].addEventListener('click', function() {
	alert(22);
})
/* 这里的两个点击事件都可以成功执行 */
```



<span style='color:red;'>注意: attachEvent()仅有IE8及早期版本支持</span>

**attachEvent()语法**

> eventTarget . attachEvent (eventNameWithon, callback)

eventTarget .attachEvent ()方法将指定的监听器注册到eventTarget(目标对象)上，当该对象触发指定的事件时,指定的回调函数就会被执行。

**该方法接收两个参数**:

1. eventNameWithOn : 事件类型字符串，比如onclick、onmouseover ，`这里要带on`；
2. callback : 事件处理函数，当目标触发事件时`回调函数`被调用

>回调函数原理：函数可以作为一个参数。将这个函数作为参数传到另一个函数里面，当那个函数执行完之后, 再执行传进去的这个函数，这个过程就叫做回调。



###### 注册事件兼容性解决方案

<span style='color:red;'>兼容性处理的原则：首先照顾大多数浏览器，再处理特殊浏览器</span>

```js
function addEventListener (element, eventName, fn) {
//判断当前浏览器是否支持addEventListener方法
    if (element.addEventListener) {
    element.addEventListener (eventName, fn); // 第三个参数默认是false :
    } else if (element.attachEvent) {
    element.attachEvent( 'on' + eventName, fn) ;
    } else {
    //相当于element.onclick = fn;
    element[ 'on' + eventName] = fn;
}
```



##### 7.2 删除/解绑事件

###### 传统注册方式删除事件

> eventTarget. onclick = null;

注意：此种方式不能移除匿名函数；



###### 方法监听注册方式删除事件

> eventTarget. remove EventListener (type,listener[, useCapture] );



<span style='color:red;'>注意: attachEvent() 和 detachEvent()仅有IE8及早期版本支持</span>

>eventTarget. detachEvent (eventNameWithon，callback) ;



```js
const divs = document.querySelectorAll('div');
        divs[0].onclick = function () {
            alert(1111);
            /* 实现事件解绑/删除事件*/
            divs[0].onclick = null;
        }
        divs[1].addEventListener('click', fn2); /* 里面的fn不需要调用加小括号 */

        function fn2() {
            alert(222);
            /* 在函数内实现移除事件 */
            divs[1].removeEventListener('click', fn);
        }
        divs[2].attachEvent('click', fn3); /* 里面的fn不需要调用加小括号 */

        function fn3() {
            alert(333);
            /* 在函数内实现移除事件 */
            divs[2].detachEvent('click', fn);
        }
```



###### 删除事件兼容性解决方案

```js
function removeEventListener (element, eventName, fn) {
    //判断当前浏览器是否支持removeEventlistener方法
    if (element. removeEventListener) {
    element . removeEventListener (eventName, fn); // 第三个参数默认是false
    } else if (element . detachEvent) {
    	element. deta chEvent( 'on' + eventName, fn) ;
    } else {
    element[ 'on' + eventName] = null;
}
```



##### 7.3 DOM事件流

>事件流描述的是从页面中接收事件的顺序。
>
>`事件发生时会在元素节点之间按照特定的顺序传播，这个传播过程即DOM事件流。`

DOM事件流分为3个阶段:

1. 捕获阶段
2. 当前目标阶段
3. 冒泡阶段

**比如我们给一个div 注册了点击事件**，则有

![DOM事件流](https://gitee.com/mr_tolie/pics/raw/master/images/202201271541853.png)

* 事件冒泡：IE最早提出，事件开始时由最具体的元素接收，然后逐级向上传播到到DOM最顶层节点的过程。
* 事件捕获：网景最早提出，由DOM最顶层节点开始，然后逐级向下传播到到最具体的元素接收的过程。



**注意**

1. JS代码中只能执行捕获或者冒泡其中的一个阶段。
2. onclick和attachEvent只能得到冒泡阶段。
3. addEventListener (type, listener [, useCapture])  <span style='color:pink'>第三个参数如果是true，表示在事件捕获阶段调用事件处理程序；如果是false (不写默认就是false ) ，表示在事件冒泡阶段调用事件处理程序。</span>

```js
const father = document.querySelector('.father');
const son = document.querySelector('.son');
/* addEventLister()第三个参数省略或者为 false，则在冒泡过程执行
	所以这里会先弹出 son；再弹出 father */
son.addEventListener('click', function () {
    alert('son');
})
father.addEventListener('click', function () {
    alert('father');
})

/* addEventLister()第三个参数省略为true，则在捕获过程执行
	所以这里会先弹出 father；再弹出 son */
son.addEventListener('click', function () {
    alert('son');
}, true)
father.addEventListener('click', function () {
    alert('father');
}, true)
```



> 实际开发中我们很少使用事件捕获，我们更关注事件冒泡；
>
> `有些事件是没有冒泡的，比如onblur、 onfocus, onmouseenter. onmouseleave`；
>
> 事件冒泡有时候会带来麻烦，有时候又会帮助很巧妙的做某些事件。



##### 7.4 事件对象

###### 1).什么是事件对象

```js
eventTarget.onclick = function (event) {}
eventTarget.addEventListener('click', function (event) {})
// 这个event就是事件对象，我们还喜欢的写成 e 或者 evt
```



1. 事件对象一般写到侦听函数的小括号里面，当形参来看；
2. `事件对象只有有了事件才会存在，`当我们注册事件时， event 对象就会被系统自动创建，并依次传递给事件监听器(事件处理函数)不需要我们传递参数；
3. `事件发生后，跟事件相关的一系列信息数据的集合都放到这个对象里面，这个对象就是事件对象event，它有很多属性和方法。`如果是鼠标点击事件就包含鼠标事件的相关信息；比如鼠标坐标等；如果是键盘事件里面就包含的键盘事件的信息，比如判断用户按下了那个键；
4. .这个事件对象我们可以自己命名比如event、evt、e；
5. 事件对象也有兼容性问题，`ie6 7 8 只能通过window. event获得事件对象`；
6. 兼容性的写法：e = e || window. event ;

```js
 const father = document.querySelector('.father');
        const son = document.querySelector('.son');
        /* son.onclick = function (e) {
            console.log(e);
        } */
        father.addEventListener('click', function (e) {
            /* console.log(e); */
            
            /* 兼容性写法 */
            e = e || window.event;
            console.log(e);
        })
```



###### 2). 事件对象的常见属性和方法

下面列出了 2 级 DOM 事件标准定义的属性。

| 属性                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [bubbles](https://www.w3school.com.cn/htmldom/event_bubbles.asp) | 返回布尔值，指示事件是否是起泡事件类型。                     |
| [cancelable](https://www.w3school.com.cn/htmldom/event_cancelable.asp) | 返回布尔值，指示事件是否可拥可取消的默认动作。               |
| [currentTarget](https://www.w3school.com.cn/htmldom/event_currenttarget.asp) | 返回其事件监听器触发该事件的元素。                           |
| [eventPhase](https://www.w3school.com.cn/htmldom/event_eventphase.asp) | 返回事件传播的当前阶段。                                     |
| [target](https://www.w3school.com.cn/htmldom/event_target.asp) | `返回触发此事件的元素`（事件的目标节点）。                   |
| [timeStamp](https://www.w3school.com.cn/htmldom/event_timestamp.asp) | 返回事件生成的日期和时间。                                   |
| [type](https://www.w3school.com.cn/htmldom/event_type.asp)   | 返回当前 Event 对象表示的事件的名称。比如click/mouseover 不带on |
| returnValue                                                  | 该属性阻止默认事件 (默认行为)`非标准`ie6-8使用，比如不让链接跳转 |

```js
a.addEventListener('click', function (e) {
    /* 阻止默认事件发生，这里阻止链接跳转 */
    e.preventDefault();

    /* 低版本浏览器 i6 7 8 */
    e.returnValue;

    //我们可以利用return false也能阻止默认行为没有兼容性问题
    //特点:return后面的代码不执行了，而且只限于传统的注册方式
   // return false;
})
```



###### e.target和this区别

<span style='color:pink;'>e. target返回的是触发事件的对象(元素) ；</span>

<span style='color:pink;'>this 返回的是绑定事件的对象(元素)</span>

```js
/* e.target返回的是触发事件的元素，*/
/* this返回的是绑定事件的元素，*/
father.addEventListener('click', function (e) {
    console.log(e.target);
    console.log(this);
})
```



###### 3). 事件对象的常见方法

下面列出了 2 级 DOM 事件标准定义的方法。IE 的事件模型不支持这些方法：

| 方法                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [initEvent()](https://www.w3school.com.cn/htmldom/event_initevent.asp) | 初始化新创建的 Event 对象的属性。                            |
| [preventDefault()](https://www.w3school.com.cn/htmldom/event_preventdefault.asp) | 通知浏览器`不要执行与事件关联的默认动作`。让链接不跳转或者提交按钮不提交 |
| [stopPropagation()](https://www.w3school.com.cn/htmldom/event_stoppropagation.asp) | 不再派发事件。`阻止冒泡`                                     |

```JS
const father = document.querySelector('.father');
const son = document.querySelector('.son');
/* addEventLister()第三个参数省略或者为 false，则在冒泡过程执行
	所以这里会先弹出 son；再弹出 father */
son.addEventListener('click', function () {
    alert('son');
    e.stopPropagation();	/* 阻止事件冒泡 stop 停止 Propagation传播 标准*/
    e. cancelBubble =true;	//非标准  cancel 取消bubble 泡泡

})
father.addEventListener('click', function () {
    alert('father');
})
```



**阻止事件冒泡的兼容性解决方案**

```js
if(e && e. stopPropagation) {
	e. stopPropagation();
}else{
	window.event.cancelBubble = true ;
```



##### 7.5 事件委托

事件委托也称为事件代理，在jQuery里面称为事件委派。

###### 1). 事件委托的原理

<span style='color:pink;'>不是每个子节点单独设置事件监听器，而是事件监听器设置在其父节点上，然后利用冒泡原理影响设置每个子节点。</span>
以上案例：给ul注册点击事件，然后利用事件对象的target来找到当前点击的Ii，因为点击li，事件会冒泡到ul上， ul有注册事件，就会触发事件监听器。

###### 2). 事件委托的作用

<span style='color:pink;'>我们只操作了一次DOM，提高了程序的性能</span>

```js
const ul = document.querySelector('ul');
ul.addEventListener('click', function (e) {

    /* 排他思想 */
    const brothers = e.target.parentNode.children;
    for (let n = 0; n < brothers.length; n++) {
        brothers[n].style.backgroundColor = '';
    }

    e.target.style.backgroundColor = 'pink';
})
```



##### 7.5 鼠标事件

| 事件类型    | 说明                                                         |
| ----------- | ------------------------------------------------------------ |
| click       | 单击鼠标左键时发生，如果右键也按下则不会发生。当用户的焦点在按钮上并按了 Enter 键时，同样会触发这个事件 |
| dblclick    | 双击鼠标左键时发生，如果右键也按下则不会发生                 |
| mousedown   | 单击任意一个鼠标按钮时发生                                   |
| mouseout    | 鼠标指针位于某个元素上且将要移出元素的边界时发生             |
| mouseover   | 鼠标指针移出某个元素到另一个元素上时发生                     |
| mouseup     | 松开任意一个鼠标按钮时发生                                   |
| mousemove   | 鼠标在某个元素上时持续发生                                   |
| focus       | 获得鼠标焦点触发                                             |
| blur        | 失去鼠标焦点触发                                             |
| contextmenu | 主要控制应该何时显示上下文菜单，主要用于程序员取消默认的上下文菜单 |
| selectstart | 禁止鼠标选中                                                 |

###### 1). mouseenter和mouseover的区别

mouseenter鼠标事件

* 当鼠标移动到元素上时就会触发mouseenter事件
* 类似mouseover，它们两者之间的差别是：`mouseover鼠标经过自身盒子会触发,经过子盒子还会触发。mouseenter 只会经过自身盒子触发。`
* 原因是因为**mouseenter不会冒泡**。



###### 2). 禁止鼠标右键菜单

contextmenu主要控制应该何时显示上下文菜单，主要用于程序员取消默认的上下文菜单

```js
document.addEventListener ('contextmenu', function(e) {
	e.preventDefault () ;
})
```



###### 3). 禁止鼠标选中

 selectstart开始选中

```js
document. addEventListener (' selectstart', function(e) {
	e.preventDefault () ;
}
```



###### 4). 鼠标事件对象属性

| 属性    | 说明                                                         | 兼容性                     |
| ------- | ------------------------------------------------------------ | -------------------------- |
| clientX | 以`浏览器可视区域`左上顶角为原点，定位 x 轴坐标              | 所有浏览器，不兼容 Safari  |
| clientY | 以`浏览器可视区域`左上顶角为原点，定位 y 轴坐标              | 所有浏览器，不兼容 Safari  |
| offsetX | 以`当前事件的目标`对象左上顶角为原点，定位 x 轴坐标          | 所有浏览器，不兼容 Mozilla |
| offsetY | 以`当前事件的目标`对象左上顶角为原点，定位 y 轴坐标          | 所有浏览器，不兼容 Mozilla |
| pageX   | 以 `document 对象`（即文档页面）左上顶角为原点，定位 x 轴坐标（IE9+支持） | 所有浏览器，不兼容 IE      |
| pageY   | 以 `document 对象`（即文档页面）左上顶角为原点，定位 y 轴坐标（IE9+支持） | 所有浏览器，不兼容 IE      |
| screenX | 以`计算机屏幕左上顶角`为原点，定位 x 轴坐标                  | 所有浏览器                 |
| screenY | 以`计算机屏幕左上顶角`为原点，定位 y 轴坐标                  | 所有浏览器                 |
| layerX  | 最近的绝对定位的父元素（如果没有，则为 document 对象）左上顶角为元素，定位 x 轴坐标 | Mozilla 和 Safari          |
| layerY  | 最近的绝对定位的父元素（如果没有，则为 document 对象）左上顶角为元素，定位 y 轴坐标 | Mozilla 和 Safari          |

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>跟随鼠标的图片</title>
    <style>
        img {
            position: absolute;
        }
    </style>
</head>

<body>
    <img src="images/dog.jpg" alt="">

    <script>
        const img = document.querySelector('img');
        document.addEventListener('mousemove', function (e) {
            /* 减去宽度高度的一般，使得鼠标位置位于图片中心 */
            img.style.top = e.clientY - 100 + 'px';
            img.style.left = e.clientX - 150 + 'px';
        })
    </script>
</body>

</html>
```



##### 7.5 键盘事件

| 属性     | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| keydown  | 在键盘上`按下某个键时触发`。`如果按住某个键，会不断触发该事件`，但是 Opera 浏览器不支持这种连续操作。该事件处理函数返回 false 时，会取消默认的动作（如输入的键盘字符，在 IE 和 Safari 浏览器下还会禁止keypress 事件响应）。 |
| keyup    | `释放某个键盘键时触发`。该事件`仅在松开键盘时触发一次，不是一个持续的响应状态`。 |
| keypress | `按下某个键盘键并释放时触发`。`如果按住某个键，会不断触发该事件`。该事件处理函数返回 false 时，会取消默认的动作（如输入的键盘字符）。<br><span style='color:pink;'>但是它不识别功能键，比如ctrl  shift  箭头等</span> |



###### 3). 键盘事件对象属性

| 属性       | 说明                                                         |
| ---------- | ------------------------------------------------------------ |
| keyCode    | 该属性包含键盘中`对应键位的ASCII键值`                        |
| charCode   | 该属性包含键盘中`对应键位的 Unicode 编码`，仅 DOM 支持       |
| target     | 发生事件的节点（包含元素），仅 DOM 支持                      |
| srcElement | 发生事件的元素，仅 IE 支持                                   |
| shiftKey   | 是否按下 Shift 键，如果按下返回 true，否则为false            |
| ctrlKey    | 是否按下 Ctrl 键，如果按下返回 true，否则为false             |
| altKey     | 是否按下 Alt 键，如果按下返回 true，否则为false              |
| metaKey    | 是否按下 Mtea 键，如果按下返回 true，否则为false，仅 DOM 支持 |

>* keyup和keydown事件的keyCode`不区分字母大小写`，按下a和A得到的都是65;
>* keypress事件的keyCode`区分字母大小写`，按下a和A得到的都是ASCII值不同。

































#### 第八章 BOM

##### 8.1 什么是BOM

BOM ( Browser Object Model )即`浏览器对象模型`，它提供了`独立于内容而与浏览器窗口进行交互的对象`，其`核心对象是window`。BOM由一系列相关的对象构成，并且每个对象都提供了很多方法与属性。

![BOM和DOM](https://gitee.com/mr_tolie/pics/raw/master/images/202201291352953.png)

##### 8.2 BOM的构成

BOM比DOM大，它包含DOM。

![BOM的构成](https://gitee.com/mr_tolie/pics/raw/master/images/202201291405596.png)

window对象是浏览器的顶级对象，它具有双重角色。

1. 它是JS访问浏览器窗口的一个接口。
2. `它是一个全局对象。定义在全局作用域中的变量、函数都会变成window对象的属性和方法`。在调用的时候可以省略window，前面学习的对话框都属于window对象方法，如alert()、prompt()等。

> *注意*: window下的一个特殊属性window.name。一般不要设定名为name的全局变量。

```js
var num=10;
console.log(num);
console.log(window. num) ;

function fn() {
	console.log(11);
}
fn();
window.fn();

alert(11);
window.alert(11)
```



##### 8.3 window对象的常见事件

###### 1). load事件

> window.onload = function() { }
> 或者
> window.addEventListener ("load", function() { }) ;

window.onload是（窗口页面）加载事件，`当文档内容完全加载完成会触发该事件(包括图像、脚本文件、CSS文件等)，就调用的处理函数`。

**注意**

1. 有了window.onload就可以把JS代码写到页面元素的上方，因为onload是等页面内容全部加载完毕，
   再去执行处理函数。
2. window.onload传统注册事件方式只能写一次，如果有多个，会以最后一个window.onload为准。
3. 如果使用addEventListener()则没有限制

> 下面三种情况都会刷新页面都会触发load事件。
> 1. a标签的超链接
>
> 2. F5或者刷新按钮 (强制刷新)
>
> 3. 前进后退安钮
>
>   
>
>   但是火狐中，有个“往返缓存”, 这个缓存中不仅保存着页面数据，还保存了DOM和JavaScript的
>   状态;实际上是将整个页面都保存在了内存里。`所以此时后退按钮不能刷新页面。`



###### 2).DOMContentLoaded事件

```js
document. addEventListener ( ' DOMContentLoaded' , function() { })
```

DOMContentLoaded事件触发时，`仅当DOM加载完成，不包括样式表，图片， flash等等。加载速度比load更快一些`。<span style="color:red;">Ie9以上支持</span>

如果页面的图片很多的话，从用户访问到onload触发可能需要较长的时间交互效果就不能实现，必然影响用户的体验，此时用DOMContentloaded事件比较合适。



###### 3). pageshow事件

pageshow事件在页面显示时触发，无论页面是否来自缓存。在重新加载页中，pageshow会`在load事件触发后触发`；根据事件对象中的persisted来判断是否是缓存中的页面触发的pageshow事件，`注意这个事件给window添加。`



###### 4). resize事件

```js
window. onresize = function() { }
window. addEventListener ("resize", function() {}) ;
```

window.onresize是调整窗口大小加载事件，当触发时就调用的处理函数。

**注意**:

1. 只要窗口大小发生像素变化，就会触发这个事件。
2. 我们经常利用这个事件完成响应式布局。window.innerWidth 当前屏幕的宽度

```js
const box = document.querySelector('.box');

window.addEventListener('resize', function () {
    /* window.innerWidth表示此时页面的宽度 */
    if (window.innerWidth <= 900) {
        box.style.display = 'none';
    } else {
        box.style.display = 'block';
    }
})
```



###### 3). 定时器

window对象给我们提供了2个非常好用的方法定时器。

1. setTimeout()

**语法**

> window. setTimeout (调用函数，[延迟的亳秒数]) ;

setTimeout() 方法用于`设置一个定时器`，`该定时器在定时器到期后执行调用函数`。

**注意**:

1. window可以省略。
2. 这个调用函数可以直接写函数，写函数名 或者 采取字符串 函数名() 三种形式。 `第三种不推荐`
3. `延迟的毫秒数省略默认是0`，如果写，必须是`毫秒`。
4. 因为定时器可能有很多，所以我们经常给定时器赋值一个标识符（名字）。

```js
function callback() {
	console.log('爆炸了');
}
setTimeout(callback, 3000);
/* 或者 */
setTimeout("callback()" 3000);// 不提倡

//给定时器加标识符 (名字)
var clock = setTimeout(callback, 3000);
```



2. **停止setTimeout()定时器**

> window. clearTimeout (timeout ID)

clearTimeout ()方法取消了先前通过调用setTimeout ()建立的定时器。
**注意**:

* window可以省略。
* 里面的参数就是定时器的 标识符 / 名称。



3. **setInterval()定时器**

> window . setInterval (回调函数，[间隔的亳秒数]);

setInterval()方法`重复`调用一个函数，`每隔这个时间，就去调用一次回调函数`。

**注意**:

* window可以省略。
* 这个调用函数可以直接写函数，或者写函数名 或者 采取字符串 '函数名0' 三种形式。 `第三种不推荐`
* 间隔的`毫秒数省略默认是0` ，如果写，必须是`毫秒`，表示每隔多少毫秒就自动调用这个函数。
* 因为定时器可能有很多，所以我们经常给定时器赋值一个 标识符/名字。

```html
<!--电商主页倒计时效果-->
<!DOCTYPE html>
<html lang="zh">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>倒计时模块</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        .w {
            width: 1200px;
        }

        i,
        em {
            font-style: normal;
        }

        .line {
            margin: 100px auto;
            background-color: pink;
        }

        .box {
            float: left;
            width: 190px;
            height: 260px;
            color: #E8E6E3;
            text-align: center;
            background-color: rgb(169, 22, 19);
            background: url(../images/JD倒计时.png) no-repeat 50%;
        }

        .box h4 {
            width: 100%;
            margin-top: 36px;
            margin-bottom: 90px;
            font-size: 30px;
        }

        .box i {
            display: block;
            width: 100%;
            font-size: 14px;
        }

        .box i strong {
            /* 与右侧汉字按 中线 对齐 */
            display: inline-block;
            margin-top: -3px;
            vertical-align: middle;

            margin-right: 2px;
            font-size: 18px;
        }

        .box>span {
            display: block;
            width: 130px;
            height: 30px;
            margin-top: 17px;
            margin-left: auto;
            margin-right: auto;
            font-size: 20px;
            font-weight: 700;
            line-height: 30px;
        }

        .box>span span {
            position: relative;
            float: left;
            width: 30px;
            height: 30px;
            margin-right: 20px;
            /* text-align: center; */
            background-color: #25282A;
        }

        .box>span span:last-child {
            margin-right: 0;
        }

        .box .hour::after {
            content: ':';
            position: absolute;
            display: block;
            right: -20px;
            top: 0;
            height: 100%;
            width: 20px;
            margin-top: -2px;
        }

        .box .min::after {
            content: ':';
            position: absolute;
            display: block;
            right: -20px;
            top: 0;
            height: 100%;
            width: 20px;
            margin-top: -2px;
            text-align: center;
        }
    </style>
</head>

<body>
    <div class="line w">
        <div class="box">
            <h4>京东秒杀</h4>
            <i><strong>18:00</strong>点场&nbsp;距结束</i>
            <span>
                <span class="hour"></span>
                <span class="min"></span>
                <span class="sec"></span>
            </span>
        </div>

        <div style="clear: both;"></div>
    </div>

    <script>
        const seckilling_hour = document.querySelector('.hour');
        const seckilling_min = document.querySelector('.min');
        const seckilling_sec = document.querySelector('.sec');

        function count(time) {
            let dateNow = +new Date();
            let date = +new Date(time);
            let times = (date - dateNow) / 1000;

            let hour = parseInt(times / 60 / 60 % 24);
            hour = hour < 10 ? '0' + hour : hour;
            seckilling_hour.innerHTML = hour;

            let min = parseInt(times / 60 % 60);
            min = min < 10 ? '0' + min : min;
            seckilling_min.innerHTML = min;

            let sec = parseInt(times % 60);
            sec = sec < 10 ? '0' + sec : sec;
            seckilling_sec.innerHTML = sec;
        }
        /* 先单独执行一次，避免防止刚开始刷新页面有空白问题 */
        count('2022-1-29 20:0:0');
        setInterval("count('2022-1-29 20:0:0')", 1000);
    </script>
</body>

</html>
```



4. **停止setInterval()定时器**

> window. clearInterval (intervalID) ;

clearInterval ()方法取消了先前通过调用setInterval ()建立的定时器。

**注意**:

1. window可以省略。
2. 里面的参数就是定时器的标识符 / 名字。

```html
<body>
    <button class="begin">开启定时器< /button>
    <button class="stop"> 停止定时器</ button>

    <script>
        var begin = document.querySelector('.begin');
        var stop = document.querySelector('.stop');
        //小技巧
        var timer = null; //全局变量 nul1是一个空对象
        
        begin.addEventListener( 'click', function() {
        timer = setInterval(function() {
          	  console.log('ni hao ma' );
        	}, 1000);
        })
        
        stop.addEventL istener( 'click', function() {
        	clearInterval(timer );
        })
    </script>
</body>
```



##### 8.4 window对象的常见属性

###### 1)、pageXOffset 和 pageYOffset 属性

pageXOffset 和 pageYOffset 属性返回文档在窗口左上角水平和垂直方向滚动的像素。

> `pageXOffset 设置或返回当前页面相对于窗口显示区左上角的 X 位置。`
>
> `pageYOffset 设置或返回当前页面相对于窗口显示区左上角的 Y 位置。`

pageXOffset 和 pageYOffset 属性`相等于 scrollX 和 scrollY 属性`。

这些属性是`只读`的。



##### 8.5 this的指向问题

**this 指向问题一般情况下this的最终指向的是那个调用它的对象；**

1. 全局作用域 或者 普通函数中this指向全局对象window（**注意**：定时器里面的this指向window）
2. 方法调用中谁调用this指向调用方法的人；
3. 构造函数中this指向构造函数的实例；
3. 箭头函数没有自己的this，看其外层的是否有函数，如果有，外层函数的this就是内部箭头函数的this；如果没有，则this是window。

```js
//1.全局作用域或者普通函数中this指向全局对象window(注意定时器里面的this指向window)
console.log(this);

function fn() {
	console.log(this);
}
fn();

// 定时器里面的this指向window
setTimeout(function() {
	console.log(this);
}, 1000);

// 2.方法调用中谁调用this指向谁
var O={
	sayHi: function() {
	console.log(this); // this指向的是。这个对象
    }
O.sayHi();
var btn = document.querySelector( 'button' );
btn. onclick = function() {
	console.log(this); // this指向的是btn这个按钮对象
 }
btn.addEventListener('click', function() {
	console.log(this); // this指向的是btn这个按钮对象
})

//3.构造函数中this指向构造函数的实例
function Fun() {
	console.log(this); // this指向的是fun实例对象
}
var fun = new Fun();

//4.箭头函数this指向:箭头函数没有自己的this，看其外层的是否有函数，如果有，外层函数的this就是内部箭头函数的this，如果没有，则this是window。
<button id="btn1">箭头函数this</button>
<script type="text/javascript">   
    let btn1 = document.getElementById('btn1');
    let obj = {
        name: 'kobe',
        age: 39,
        getName: function () {
            btn1.onclick = () => {
                console.log(this);//obj
            };
        }
    };
    obj.getName();
</script>

//5.call、apply和bind中：this 是指第一个参数
function add(c, d){
  return this.a + this.b + c + d;
}
var o = {a:1, b:3};
add.call(o, 5, 7); // 1 + 3 + 5 + 7 = 16
add.apply(o, [10, 20]); // 1 + 3 + 10 + 20 = 34
```



##### 8.6 JS执行机制

###### 1). JS是单线程

JavaScript语言的一大特点就是单线程，也就是说，同一个时间只能做一件事。这是因为Javascript这门脚本语言诞生的使命所致——JavaScript 是为处理页面中用户的交互，以及操作DOM而诞生的。比如我们对
某个DOM元素进行添加和删除操作，不能同时进行。应该先进行添加，之后再删除。

单线程就意味着，所有任务需要排队，前一个任务结束，才会执行后一个任务。 这样所导致的问题是：如果JS执行的时间过长,这样就会造成页面的渲染不连贯，导致页面渲染加载阻塞的感觉。

下面这段程序中，分析来看，1打印完，必须经过1s才能打印3，最后再打印2。

```js
console.log(1);

setTimeout( function() {
	console.log(3);
}, 1000);

console.log(2);
```



###### 2). 同步和异步

为了解决这个问题，利用多核CPU的计算能力，HTML5提出Web Worker标准，允许JavaScript脚本创建多个线程。于是，JS中出现了`同步`和`异步`。

**同步**

前一个任务结束后再执行后一个任务，程序的执行顺序与任务的排列顺序是一致的、 同步的。比如做饭的同步做法：我们要烧水煮饭，等水开了( 10分钟之后)，再去切菜，炒菜。

**异步**

你在做一件事情时，因为这件事情会花费很长时间，在做这件事的同时，你还可以去处理其他事情。比如做饭的异步做法，我们在烧水的同时，利用这10吩钟，去切菜，炒菜。

**本质区别**：这条流水线上各个流程的执行顺序不同。



###### 3). 同步任务和异步任务

同步任务
同步任务都在主线程上执行，形成一个执行栈。

异步任务
JS的异步是通过回调函数实现的。

一般而言，异步任务有以下三种类型:

> 1、普通事件，如click、resize等
>
> 2、资源加载，如load. error等
>
> 3、定时器，包括setInterval. setTimeout 等
>
> 异步任务相关`回调函数`添加到`任务队列`中(任务队列也称为消息队列)。

![任务队列](https://gitee.com/mr_tolie/pics/raw/master/images/202201292337730.png)



###### 4). JS执行机制

1. `先执行执行栈中的同步任务`；
2. 异步任务(回调函数)放入任务队列中；
3. 一旦执行栈中的所有同步任务执行完毕，系统就会`按次序读取任务队列中的异步任务`，于是被读取的异步任务结束等待状态，进入执行栈，开始执行。

![JS执行机制](https://gitee.com/mr_tolie/pics/raw/master/images/202201292353817.png)

由于主线程不断的重复获得任务、执行任务、再获取任务、再执行，所以这种机制被称为`事件循环`( event loop )。



##### 8.7 location对象



###### 1). 什么是location对象

`window对象`给我们提供了一个`location属性用于获取或设置窗体的URL`，并且可以用于解析URL。因为这个属性返回的是一个对象，所以我们将这个属性也称为location对象。



###### 2). 什么是URL

`统一资源定位符`(Uniform Resource Locator, URL)是互联网上标准资源的地址。互联网上的每个文件都有一个唯一的URL ,它包含的信息指出文件的位置以及浏览器应该怎么处理它。
URL的一般语法格式为:

> protocol: //host [:port]/path/ [?query]# fragment
>
> 比如：http: //www. tcast.cn/index.html?name=andy&age=18#link

| 组成     | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| protocol | 通信协议，常用的有http，ftp，maito等                         |
| host     | 主机(域名)  比如：www.itheima.com                            |
| port     | 端口号可选，省略时使用方案的默认端口如http的默认端口为80     |
| path     | 路径由零或多个"/"符号隔开的字符串，一般用来表示主机上的一个目录或文件地址 |
| query    | 参数以`键值对`的形式，通过`&`符号分隔开来                    |
| fragment | 片段#后面内容，常见于链接、锚点                              |



###### 3). location对象的属性

| 属性                                                         | 描述                                                    |
| :----------------------------------------------------------- | :------------------------------------------------------ |
| [hash](https://www.w3school.com.cn/jsref/prop_loc_hash.asp)  | 设置或返回从井号 (#) 开始的 URL（锚）。                 |
| [host](https://www.w3school.com.cn/jsref/prop_loc_host.asp)  | 设置或返回主机名和当前 URL 的端口号。                   |
| [hostname](https://www.w3school.com.cn/jsref/prop_loc_hostname.asp) | 设置或返回当前 URL 的主机名。                           |
| [href](https://www.w3school.com.cn/jsref/prop_loc_href.asp)  | 设置或返回完整的 URL。                                  |
| [pathname](https://www.w3school.com.cn/jsref/prop_loc_pathname.asp) | 设置或返回当前 URL 的路径部分。                         |
| [port](https://www.w3school.com.cn/jsref/prop_loc_port.asp)  | 设置或返回当前 URL 的端口号。                           |
| [protocol](https://www.w3school.com.cn/jsref/prop_loc_protocol.asp) | 设置或返回当前 URL 的协议。                             |
| [search](https://www.w3school.com.cn/jsref/prop_loc_search.asp) | 设置或返回从问号 (?) 开始的 URL（查询部分），包括问号。 |

```js
var time = 5;
setInterval(() => {
    if (time == 0) {
        location.href = 'https://www.baidu.com';
    } else {
        con.innerHTML = '将在' + time + '秒钟后跳转到百度';
        time--;
    }
}, 1000);
```



**search属性**

```html

<body>
    <span><i></i>，欢迎你</span>
    <script>
        const i = document.querySelector('i');

        /* console.log(location.search.substr(1).split('=')[1]); */
        /* 思路：
        通过location的search属性获得传递过来的参数
        再对参数进行处理，用substr()截取问号后面的内容
        然后用split('=')将字符串转换为数组
        最后从数组中取出想要的参数，通过innerHTML写入页面中 */
        
        i.innerHTML = location.search.substr(1).split('=')[1]
    </script>
</body>
```



###### 4). Location 对象方法

| 属性                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [assign()](https://www.w3school.com.cn/jsref/met_loc_assign.asp) | 跟href一样，可以跳转页面(也称为重定向页面)。`记录历史`，可以后退页面 |
| [reload()](https://www.w3school.com.cn/jsref/met_loc_reload.asp) | 重新加载页面，相当于刷新按钮或者f5；如果参数为true，强制刷新ctrl+f5 |
| [replace()](https://www.w3school.com.cn/jsref/met_loc_replace.asp) | 替换当前页面，因为`不记录历史`，所以不能后退页面             |



##### 8.8 navigator对象

navigator对象包含有关浏览器的信息，它有很多属性，`最常用的是userAgent`，该属性可以返回由客
户机发送服务器的user- agent头部的值。

下面前端代码可以判断用户那个终端打开页面，实现跳转

```js
if ( (navigator. userAgent. match (/ (phone I padI podl iPhone liPod | ios I iPad |Android | Mobile | BlackBe rry | IEMobile |MQQBrowser | JUC | Fennec |wOSBrowser | Browse rNG | Webos| Symbian |Windows Phone)/i))) {
	window.location.href = "";	//手机
} else {
	window.location.href = "";	//电脑
}
```



##### 8.9 history对象

window对象给我们提供了-个history对象，与浏览器历史记录进行交互。该对象包含用户(在浏览器窗口中)访问过的URL。

| history对象方法 | 作用                                                         |
| --------------- | ------------------------------------------------------------ |
| back()          | 可以后退功能                                                 |
| forward()       | 前进功能                                                     |
| go(参数)        | 前进后退功能参数，如果是1，前进1个页面；如果是-1，后退1个页面。参数为几就前进/后退几个页面。 |

```js
var btn = document . querySelector( ' button' );
btn. addEventListener( ' click', function( ) {
    //前进
    	history. go(1); 
	//history. forward(); 
    
    //后退
	history. go(-1); 
	history. back(); 
})
```



#### 第九章 PC端网页动效

##### 9.1 offset概述

offset翻译过来就是偏移量，我们使用offset系列相关属性可以`动态的`得到该元素的位置(偏移)、大小等。

* 获得元素距离带有定位父元素的位置
* 获得元素自身的大小(宽度高度)

> 注意:返回的数值都`不带单位`

**offset系列常用属性**

| offset系列属性       | 作用                                                         |
| -------------------- | ------------------------------------------------------------ |
| element.offsetParent | 返回作为该元素带有定位的父级元素，如果父级都没有定位，则返回body |
| element.offsetTop    | 返回元素相对带有定位父元素上方的偏移                         |
| element.offsetLeft   | 返回元素相对带有定位父元素左边框的偏移                       |
| element.offsetWidth  | `返回自身包括padding、边框、 内容区的宽度`，返回数值不带单位 |
| element.offsetHeight | `返回自身包括padding、边框、内容区的高度`，返回数值不带单位  |



###### 1). offset与style区别

![offset与style区别](https://gitee.com/mr_tolie/pics/raw/master/images/202201301452318.png)



###### 实现拖动效果

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>js拖动效果</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        a {
            text-decoration: none;
            color: #000;
        }

        input {
            outline: none;
        }

        li {
            list-style: none;
        }

        .hd {
            width: 100px;
            margin: 30px auto;
            text-align: center;
        }

        .con {
            display: none;
            width: 666px;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 2;
            /* margin: 0 auto; */
            /* padding-left: 150px; */
            background-color: #fff;
        }

        .box {
            width: 500px;
            margin: 0 auto;
        }

        .con li {
            margin-bottom: 36px;
        }

        .con h4 {
            position: relative;
            text-align: center;
            margin-bottom: 30px;
            margin-top: 10px;
            font-size: 24px;
            width: 100%;
            cursor: move;
        }

        .con h4 a {
            position: absolute;
            top: -36px;
            right: -26px;
            width: 50px;
            height: 50px;
            border-radius: 25px;
            background-color: #ccc;
            font-size: 16px;
            line-height: 50px;
            font-weight: normal;
        }

        .con label {
            display: inline-block;
            width: 60px;
            height: 30px;
            margin-right: 5px;
            line-height: 30px;
            text-align: right;
        }

        .con input {
            width: 420px;
            height: 40px;
        }

        .con input:nth-child(-n+2) {
            padding-left: 5px;
        }

        .con li:last-child input {
            margin-left: 50px;
            font-size: 22px;
            letter-spacing: 26px;
        }

        .bg {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            bottom: 0;
            right: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, .4);
        }
    </style>
</head>

<body>
    <div class="hd"><a href="javascript:;">点击登录</a></div>
    <!-- 内容 -->

    <div class="con">
        <h4>会员登录 <a href="javascript:;">关闭</a></h4>
        <div class="box">
            <form action="">

                <ul>
                    <li>
                        <label for="username">用户名:</label>
                        <input type="text" name="" placeholder="请输入用户名" id="username">
                    </li>
                    <li>
                        <label for="pwd">密码:</label>
                        <input type="password" name="" placeholder="请输入密码" id="pwd">

                    </li>
                    <li><input type="submit" value="登录"></li>
                </ul>

            </form>
        </div>

    </div>

    <!-- 遮罩层 -->
    <div class="bg"></div>

    <script>
        const hd_a = document.querySelector('.hd a');
        const bg = document.querySelector('.bg');
        const con = document.querySelector('.con');
        const title = document.querySelector('.con h4');
        const con_close = document.querySelector('.con h4 a ');

        hd_a.addEventListener('click', function () {
            bg.style.display = 'block';
            con.style.display = 'block';
        });
        con_close.addEventListener('click', function () {
            con.style.display = 'none';
            bg.style.display = 'none';
        })

        /* 鼠标的坐标减去鼠标在盒子内的坐标，才是模态框真正的位置。 */

        /* 鼠标按下，我们要得到鼠标在盒子的坐标。*/
        /*鼠标移动，就让模态框的坐标设置为:鼠标坐标减去盒子坐标即可，注意移动事件写到按下事件里面。 */
        title.addEventListener('mousedown', function (e) {
            var x = e.pageX - con.offsetLeft;
            var y = e.pageY - con.offsetTop;

            document.addEventListener('mousemove', move);

            function move(e) {
                con.style.top = e.pageY - y + 'px';/* 注意单位 */
                con.style.left = e.pageX - x + 'px';

                /* 取消mousemove 事件 */
                document.addEventListener('mouseup', function () {
                    document.removeEventListener('mousemove', move);
                })

            }
        })
    </script>
</body>

</html>
```



##### 9.2 元素可视区client系列

client翻译过来就是客户端，我们使用client系列的相关属性来获取元素可视区的相关信息。通过client系列
的相关属性可以动态的得到该元素的边框大小、元素大小等。

| client系列属性       | 作用                                                         |
| -------------------- | ------------------------------------------------------------ |
| element.clientTop    | 返回元素上边框的大小                                         |
| element.clientLeft   | 返回元素左边框的大小                                         |
| element.clientWidth  | 返回自身包括padding、内容区的宽度， `不含边框`，`返回数值不带单位` |
| element.clientHeight | 返回自身包括padding、内容区的高度， `不含边框`，`返回数值不带单位` |



###### 立即执行函数

`立即执行函数：不需要调用，立马能够自己执行的函数。`

**语法**

> (function() {}) () 或者 (function(){}())

主要作用：创建一个独立的作用域，`里面所有的变量都是局部变量不会有命名冲突的情况`。

```js
/* 立即执行函数 ，也可以不是匿名函数*/

//方法一
(function () {
    console.log(1);
})
();

/* 传参 */
(function (a, b) {
    console.log(a);
    console.log(b);
    console.log(a + b);
})
(1, 2);//第二个小括号可以看做是调用函数


//方法二
(function (a, b) {
    console.log(a);
    console.log(b);
    console.log(a + b);
}
 ("lo", "ve"))//第二个小括号可以看做是调用函数
```



##### 9.3 元素scroll系列属性

使用scroll系列的相关属性可以动态的得到该元素的大小、滚动距离等。

| scroll系列属性       | 作用                                                         |
| -------------------- | ------------------------------------------------------------ |
| element.scrollTop    | 返回被卷去的上侧距离，返回数值不带单位                       |
| element.scrollLleft  | 返回被卷去的左侧距离，返回数值不带单位                       |
| element.scrollWidth  | 返回自身`实际的`宽度，`包括超出部分的宽度`，`不含边框`，返回数值不带单位 |
| element.scrollHeight | 返回自身`实际的`高度，`包括超出部分的高度`，`不含边框`，返回数值不带单位 |

> *注意*:元素被卷去的头部是element.scrollTop ,如果是页面被卷去的头部则是window.pageYOffset

![element.scrollTop和element.scrollWidth](https://gitee.com/mr_tolie/pics/raw/master/images/202202041749951.png)



##### 9.4 三大系列总结

1. offset系列 `经常用于获得元素位置`offsetLeft offsetTop
2. client `经常用于获取元素大小`clientWidth clientHeight
3. scroll `经常用于获取滚动距离`scrollTop scrolLeft

4. 注意`页面滚动的距离通过window. pagexoffset获得`



##### 9.5 动画函数封装

###### 1). 动画实现原理

`核心原理`：通过定时器setInterval0不断移动盒子位置。

**实现步骤**:

1. 获得盒子当前位置
2. 让盒子在当前位置加上1个移动距离
3. 利用定时器不断重复这个操作
4. 加一个结束定时器的条件
5. 注意此元素需要添加定位,才能使用element.style.left

```js
function boxMove(obj, distence) {
    var box_moving = setInterval(function () {
        if (obj.offsetLeft <= distence) {
            obj.style.left = obj.offsetLeft + 1 + 'px';
        } else {
            clearInterval(box_moving);
        }
    }, 500);
}
```

###### 2). 动画函数给不同元素记录不同定时器

如果多个元素都使用上方的动画函数，每次都要var声明定时器。我们可以给不同的元素使用不同的定时器(自己专门用自己的定时器)。

**核心原理**：利用JS一门动态语言,可以很方便的给当前对象添加属性。

```js
  const box1 = document.querySelector('.box1');
        const box2 = document.querySelector('.box2');
        const btn = document.querySelector('button');

        boxMove(box2, 200);

        btn.addEventListener('click', function () {
            /* 不断点击，就会不断创建新的定时器，导致obj的运动加快
            所以必须保证只有一个定时器存在 */
            boxMove(box1, 100);
        })

        function boxMove(obj, distence) {
            /* 保证只有一个定时器存在 */
            clearInterval(obj.box_moving);

            /* 给不同元素指定了不同的定时器 */
            obj.box_moving = setInterval(function () {
                if (obj.offsetLeft <= distence) {
                    obj.style.left = obj.offsetLeft + 1 + 'px';
                } else {
                    clearInterval(obj.box_moving);
                }
            }, 30);
        }
```



###### 3). 缓动效果原理

缓动动画就是让元素运动速度有所变化，最常见的是让速度慢慢停下来。

思路:

1. 让盒子每次移动的距离慢慢变小， 速度就会慢慢落下来。
2. `核心算法: (目标值-现在的位置) / 10做为每次移动的距离步长`
3. 停止的条件是:让当前盒子位置等于目标位置就停止定时器。



###### 4). 动画函数添加回调函数

```js
//左右移动的缓动动画
function move(obj, distence, callback) {
    //保证只有一个定时器存在
    clearInterval(obj.box_moving);

    //给不同元素指定了不同的定时器
    obj.box_moving = setInterval(function () {
        let step = (distence - obj.offsetLeft) / 10;
        //应保证步长为整数，才能使得obj严格走到要求的位置
        //如果为正值，则向上取整
        //如果为负值，则向下取整
        step = step > 0 ? Math.ceil(step) : Math.floor(step);

        if (obj.offsetLeft == distence) {
            clearInterval(obj.box_moving);
            //回调函数放在定时器停止之后
            //如果存在回调函数，就调用回调函数执行。
            callback && callback();
            /*  if (callback) {
                 callback();
             } */
        }
        obj.style.left = obj.offsetLeft + step + 'px';
    }, 15);
}

//上下移动的缓动动画
function moveUp(obj, distence, callback) {
    //保证只有一个定时器存在
    clearInterval(obj.box_moveUp);
    //给不同元素指定不同的定时器
    obj.box_moveUp = setInterval(function () {
        let step = (distence - window.pageYOffset) / 10;
        //应保证步长为整数，才能使得obj严格走到要求的位置
        //如果为正值，则向上取整
        //如果为负值，则向下取整
        step = step > 0 ? Math.ceil(step) : Math.floor(step);

        if (window.pageYOffset == distence) {
            clearInterval(obj.box_moveUp);
            //回调函数放在定时器停止之后
            //如果存在回调函数，就调用回调函数执行。
            callback && callback();
            /*  上方 callback && callback();
           		等同于if (callback) {
                 callback();
             } */
        }
        window.scroll(0, window.pageYOffset + step)
    }, 15);
}
```





##### 第十章 ES6

![ES6思维导图](https://gitee.com/mr_tolie/pics/raw/master/images/202202232152093.jpeg)

