---
title: 【转载】浅谈JavaScript函数重载
date: 2022-3-5 13:57:01
summary: 
categories: 
  - Frond End

tags:
  - JavaScript
---

[转载自渔歌](https://www.cnblogs.com/yugege/p/5539020.html)

## 【转载】浅谈JavaScript函数重载

我们现在有这样的一个需求，有一个people对象，里面存着一些人名，如下：

```js
var people = {
  values: ["Dean Edwards", "Sam Stephenson", "Alex Russell", "Dean Tom"]
};
```

我们希望people对象拥有一个find方法，当不传任何参数时，就会把people.values里面的所有元素返回来；当传一个参数时,就把first-name跟这个参数匹配的元素返回来；当传两个参数时，则把first-name和last-name都匹配的才返回来。因为find方法是根据参数的个数不同而执行不同的操作的，所以，我们希望有一个addMethod方法，能够如下的为people添加find的重载：

```js
addMethod(people, "find", function() {}); /*不传参*/
addMethod(people, "find", function(a) {}); /*传一个*/
addMethod(people, "find", function(a, b) {}); /*传两个*/
```

这时候问题来了，这个全局的addMethod方法该怎么实现呢？John Resig的实现方法如下，代码不长，但是非常的巧妙：

```js
function addMethod(object, name, fn) {
　　var old = object[name]; //把前一次添加的方法存在一个临时变量old里面
　　object[name] = function() { // 重写了object[name]的方法
　　　　// 如果调用object[name]方法时，传入的参数个数跟预期的一致，则直接调用
　　　　if(fn.length === arguments.length) {
　　　　　　return fn.apply(this, arguments);
　　　　// 否则，判断old是否是函数，如果是，就调用old
　　　　} else if(typeof old === "function") {
　　　　　　return old.apply(this, arguments);
　　　　}
　　}
}
```

现在，我们一起来分析一个这个addMethod函数，它接收3个参数，第一个为要绑定方法的对象，第二个为绑定的方法名称，第三个为需要绑定的方法（一个匿名函数）。函数体的的分析已经在注释里面了。

OK，现在这个addMethod方法已经实现了，我们接下来就实现people.find的重载啦！全部代码如下：

```js
//addMethod
function addMethod(object, name, fn) {
　　var old = object[name];
　　object[name] = function() {
　　　　if(fn.length === arguments.length) {
　　　　　　return fn.apply(this, arguments);
　　　　} else if(typeof old === "function") {
　　　　　　return old.apply(this, arguments);
　　　　}
　　}
}
 
 
var people = {
　　values: ["Dean Edwards", "Alex Russell", "Dean Tom"]
};
 
/* 下面开始通过addMethod来实现对people.find方法的重载 */
 
// 不传参数时，返回peopld.values里面的所有元素
addMethod(people, "find", function() {
　　return this.values;
});
 
// 传一个参数时，按first-name的匹配进行返回
addMethod(people, "find", function(firstName) {
　　var ret = [];
　　for(var i = 0; i < this.values.length; i++) {
　　　　if(this.values[i].indexOf(firstName) === 0) {
　　　　　　ret.push(this.values[i]);
　　　　}
　　}
　　return ret;
});
 
// 传两个参数时，返回first-name和last-name都匹配的元素
addMethod(people, "find", function(firstName, lastName) {
　　var ret = [];
　　for(var i = 0; i < this.values.length; i++) {
　　　　if(this.values[i] === (firstName + " " + lastName)) {
　　　　　　ret.push(this.values[i]);
　　　　}
　　}
　　return ret;
});
 
// 测试：
console.log(people.find()); //["Dean Edwards", "Alex Russell", "Dean Tom"]
console.log(people.find("Dean")); //["Dean Edwards", "Dean Tom"]
console.log(people.find("Dean Edwards")); //["Dean Edwards"]
```