---
title: JS自增(++)
date: 2022-03-04 18:29:37
summary: 
categories: 
  - Frond End

tags:
  - JS
---



## 自增 (++)

自增运算符 (**++**) 将其操作数递增（加1）并返回一个值。

```js
let x = 3;
const y = x++;

console.log(`x:${x}, y:${y}`);
// expected output: "x:4, y:3"

let a = 3;
const b = ++a;

console.log(`a:${a}, b:${b}`);
// expected output: "a:4, b:4"
```

### 描述

如使用`后置（Postfix）自增`，操作符在操作数后（例如 x++）， `操作数将在自增前返回`。

如使用`前置（Prefix）自增`，操作符在操作数前（例如 ++x）， `操作数将先自增后返回`。

### 示例

[后置自增(Postfix increment)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Increment#后置自增postfix_increment)

```js
let x = 3;
y = x++;

// y = 3
// x = 4


```



[前置自增(Prefix increment)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Increment#前置自增prefix_increment)

```js
let a = 2;
b = ++a;

// a = 3
// b = 3

i = 1;
console.log(++i);
// 2
```