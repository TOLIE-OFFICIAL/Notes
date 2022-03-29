---
title: JS for beginner (part 2)
date: 2022-3-23 09:22:10
summary: 
categories: 
  - Frond End

tags:
  - JavaScript
---

# JS for beginner (part 2)

## Symbol

Symbol是JS的第七种数据类型，代表的是独一无二的一个数据值；

### 声明Symbol类型数据的方法

#### 一、利用Symbol()

Symbol可以理解为一个构造函数，但又不是一个构造函数，因为它`不需要使用new关键字`。

Symbol()可以传入一个字符串 (description)，作为这个Symbol变量的一个标识符，但不能通过这个description 调用这个Symbol变量；

**注意**：此种声明新的Symbol类型变量的方法下，即使两个Symbol变量的标识符相同，两个变量也是不相同的。

```js
let a = Symbol();

let b = Symbol('num');
let c = Symbol('num');
b == c    //false
```

#### 二、利用Symbol.for()

Symbol.for()是Symbol类型的一个方法，会根据括号中传入的字符串，在全局Symbol注册表中检查有无相同description的记录，如果有就不再创建新的symbol，直接返回上次存储的那个否则，它会再新建一个。

```js
let a = Symbol.for('tolie');

let b = Symbol.for('num');
let c = Symbol.for('num');
b == c  //true
```

#### 三、两种声明方式的区别

和 Symbol() 不同的是，用 Symbol.for()方法创建的的 symbol 会被放入一个全局 symbol 注册表中，而symbol()不会创建记录。`Symbol.for()并不是每次都会创建一个新的 symbol`，它会首先检查给定的 description是否已经在注册表中了。假如是，则会直接返回上次存储的那个。否则，它会再新建一个。



### 对象中的Symbol属性

[Object.getOwnPropertySymbols()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertySymbols) 方法让你在查找一个给定对象的符号属性时返回一个symbol类型的数组。

**注意**：每个初始化的对象都是没有自己的symbol属性的，因此这个数组可能为空，除非你已经在对象上设置了symbol属性。

```js
var obj = {
    name: 'tolie',
    sex: 1,
    [Symbol('say')]: function () {
        console.log(12138);
    },
    [Symbol('zibao')]: function () {
        console.log(113302);
    }
}
	Object.getOwnPropertySymbols(obj);	// [Symbol(say), Symbol(zibao)]
	
 	Object.getOwnPropertyNames(obj);	// ['name', 'sex']

    Reflect.ownKeys(obj);	// ['name', 'sex', Symbol(say), Symbol(zibao)]  

	//执行对象中的symbol方法
	obj[Object.getOwnPropertySymbols(obj)[0]]();//	12138
	obj[Reflect.ownKeys(obj)[3]]();	//	113302
```

## 迭代器 iterator

遍历器（Iterator）就是这样一种机制。它是一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署 Iterator 接口，就可以完成遍历操作（即依次处理该数据结构的所有成员）。

### 迭代器的作用

Iterator 的作用有三个：

一、为各种数据结构，提供一个统一的、简便的访问接口；

二、使得数据结构的成员能够按某种次序排列；

三、 ES6 创造了一种新的遍历命令for...of循环，**Iterator 接口主要供for...of消费**。

### 迭代器的遍历过程

Iterator 的遍历过程是这样的。

（1）创建一个指针对象，指向当前数据结构的起始位置。也就是说，遍历器对象本质上，就是一个指针对象。

（2）第一次调用指针对象的next方法，可以将指针指向数据结构的第一个成员。

（3）第二次调用指针对象的next方法，指针就指向数据结构的第二个成员。

（4）不断调用指针对象的next方法，直到它指向数据结构的结束位置。

### 实现迭代器

指针对象的next方法，用来移动指针。开始时，指针指向数组的开始位置。然后，每次调用next方法，指针就会指向数组的下一个成员。第一次调用，指向a；第二次调用，指向b。

next方法返回一个对象，表示当前数据成员的信息。这个对象具有value和done两个属性，`value`属性返回当前位置的成员，done属性是一个布尔值，表示遍历是否结束，即是否还有必要再一次调用`next`方法。

```js
//需求：使用for of进行遍历，每次返回对象一个数组的每一项内容
const stuClass = {
    name: '信息管理与信息系统',
    stus: [
        '张三',
        '李四',
        '王五',
        '赵六'
    ],
    [Symbol.iterator]() {
        let index = 0;
        return {
            next: () => {
                if (index < this.stus.length) {
                    const result = this.stus[index]
                    index++;
                    return {
                        value: result,
                        done: false
                    }
                } else {
                    return {
                        value: undefined,
                        done: true
                    }
                }
            }
        }
    }
}

for (let v of stuClass) {
    console.log(v);
}
```

### 字符串的iterator接口

字符串是一个类似数组的对象，也原生具有 Iterator 接口。

```js
var someString = "hi";
typeof someString[Symbol.iterator]
// "function"

var iterator = someString[Symbol.iterator]();

iterator.next()  // { value: "h", done: false }
iterator.next()  // { value: "i", done: false }
iterator.next()  // { value: undefined, done: true }
```

同时也可以覆盖原生的Symbol.iterator方法，达到修改遍历器行为的目的。

```javascript
var str = new String("hi");

[...str] // ["h", "i"]

str[Symbol.iterator] = function() {
  return {
    next: function() {
      if (this._first) {
        this._first = false;
        return { value: "bye", done: false };
      } else {
        return { done: true };
      }
    },
    _first: true
  };
};

//这里才第一次执行next函数，所以第一次的this._first是true
//第二次是因为第一次执行next函数将_first赋值为了false，所以返回{ done: true }
[...str] // ["bye"]
str // "hi"
```

上面代码中，字符串 str 的`Symbol.iterator`方法被修改了，所以扩展运算符（...）返回的值变成了`bye`，而字符串本身还是hi。

## 生成器 generator



> yield* 表达式用于委托给另一个generator或可迭代对象。

* yield* 表达式迭代操作数，并产生它返回的每个值。

* yield* 表达式本身的值是当迭代器关闭时返回的值（即done为true时）。

### yield和yield*

#### 委托给其他生成器

以下代码中，g1() yield 出去的每个值都会在 g2() 的 `next()` 方法中返回，就像那些 `yield` 语句是写在 `g2()` 里一样。

```js
function* g1() {
  yield 2;
  yield 3;
  yield 4;
}

function* g2() {
  yield 1;
  yield* g1();
  yield 5;
}

var iterator = g2();

console.log(iterator.next()); // { value: 1, done: false }
console.log(iterator.next()); // { value: 2, done: false }
console.log(iterator.next()); // { value: 3, done: false }
console.log(iterator.next()); // { value: 4, done: false }
console.log(iterator.next()); // { value: 5, done: false }
console.log(iterator.next()); // { value: undefined, done: true }
```

#### 委托给其他可迭代对象

除了生成器对象这一种可迭代对象，`yield*` 还可以 `yield` 其它任意的可迭代对象，比如说数组、字符串、`arguments` 对象等等。

```js
function* g3() {
  yield* [1, 2];
  yield* "34";
  yield* arguments;
}

var iterator = g3(5, 6);

console.log(iterator.next()); // { value: 1, done: false }
console.log(iterator.next()); // { value: 2, done: false }
console.log(iterator.next()); // { value: "3", done: false }
console.log(iterator.next()); // { value: "4", done: false }
console.log(iterator.next()); // { value: 5, done: false }
console.log(iterator.next()); // { value: 6, done: false }
console.log(iterator.next()); // { value: undefined, done: true }
```

#### yield* 表达式的值

`yield*` 是一个表达式，不是语句，所以它会有自己的值。

```js
function* g4() {
  yield* [1, 2, 3];
  return "foo";
}

var result;

function* g5() {
  result = yield* g4();
}

var iterator = g5();

console.log(iterator.next()); // { value: 1, done: false }
console.log(iterator.next()); // { value: 2, done: false }
console.log(iterator.next()); // { value: 3, done: false }
console.log(iterator.next()); // { value: undefined, done: true },
                              // 此时 g4() 返回了 { value: "foo", done: true }

console.log(result);          // "foo"
```



## Promise

Promise是一个对象，通过构造函数Promise()创建promise对象，`是一种新的异步编程的方式`。

promise对象有三种状态，pending(初始化)、resolved(成功的)、rejected(失败的)

```js
var promise = new Promise((resolve, reject) => {})

console.log(promise, typeof promise) //Promise{<pending>}  'object'
```

### Promise的基本使用

promise接收两个参数，resolve和reject。同时promise有then方法，promise.then()接收两个函数，promise的状态为resolved就执行第一个函数，若为rejected就执行第二个函数。

```js
//使用promise封装原生 Ajax 请求
var promise = new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open('GET', './static/TodoList.json');
    xhr.send();
    xhr.onreadystatechange = function () {
        if (xhr.readyState === 4) {
            if (xhr.status >= 200 && xhr.status < 300) {
                resolve(xhr.response);
            } else {
                reject(xhr.status);
            }
        }
    }
})
//指定回调
promise.then((value) => {
    //promise状态为resolved，输出返回值
    //value就是上方resolve传入的参数
    console.log(value);
}, (reason) => {
    //promise状态为rejected，输出状态码
    //reason就是上方reject传入的参数
    console.log(reason);
});
```

### 手写Promise

```js

```









