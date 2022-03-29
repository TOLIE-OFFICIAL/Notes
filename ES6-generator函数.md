---
title: ES6-Generator
date: 2022-02-13 15:49:47
summary: 
categories: 
  - Frond End

tags:
  - JavaScript
---





#### 一次搞懂 Generator 函数

##### 1、什么是 Generator 函数

在Javascript中，一个函数一旦开始执行，就会运行到最后或遇到return时结束，运行期间不会有其它代码能够打断它，也不能从外部再传入值到函数体内，而Generator函数（生成器）的出现使得打破函数的完整运行成为了可能，其语法行为与传统函数完全不同。

Generator函数是ES6提供的一种异步编程解决方案，形式上也是一个普通函数，但有几个显著的特征：

* function关键字与函数名之间有一个星号 "*" （推荐紧挨着function关键字）
* 函数体内使用 `yield 表达式，定义不同的内部状态` （可以有多个yield）
*  直接调用 Generator函数并不会执行，也不会返回运行结果，而是返回一个遍历器对象（Iterator Object）
* 依次调用遍历器对象的next方法，遍历 Generator函数内部的每一个状态

```js
{
  // 传统函数
  function foo() {
    return 'hello world'
  }

  foo()   // 'hello world'，一旦调用立即执行

  // Generator函数
  function* generator() {
    yield 'status one'         // yield 表达式是暂停执行的标记  
    return 'hello world'
  }

  let iterator = generator()   
  // 调用 Generator函数，函数并没有执行，返回的是一个Iterator对象
  iterator.next()             
  // {value: "status one", done: false}，value 表示返回值，done 表示遍历还没有结束
  iterator.next()              
  // {value: "hello world", done: true}，value 表示返回值，done 表示遍历结束
}
```

上面的代码中可以看到传统函数和Generator函数的运行是完全不同的，传统函数调用后立即执行并输出了返回值；Generator函数则没有执行而是返回一个Iterator对象，并通过调用Iterator对象的next方法来遍历，函数体内的执行看起来更像是“被人踢一脚才动一下”的感觉

```js
{
  function* gen() {
    yield 'hello'
    yield 'world'
    return 'ending'
  }

  let it = gen()

  it.next()   // {value: "hello", done: false}
  it.next()   // {value: "world", done: false}
  it.next()   // {value: "ending", done: true}
  it.next()   // {value: undefined, done: true}
}
```

上面代码中定义了一个 Generator函数，其中包含两个 yield 表达式和一个 return 语句（即产生了三个状态）

每次调用Iterator对象的next方法时，内部的指针就会从函数的头部或上一次停下来的地方开始执行，直到遇到下一个 yield 表达式或return语句暂停。换句话说，`Generator 函数是分段执行的，yield表达式是暂停执行的标记，而 next方法可以恢复执行`。

**执行过程如下**：

第一次调用next方法时，内部指针从函数头部开始执行，遇到第一个 yield 表达式暂停，并返回当前状态的值 'hello'

第二次调用next方法时，内部指针从上一个（即第一个） yield 表达式开始，遇到第二个 yield 表达式暂停，返回当前状态的值 'world'

第三次调用next方法时，内部指针从第二个 yield 表达式开始，遇到return语句暂停，返回当前状态的值 'end'，同时所有状态遍历完毕，done 属性的值变为true

第四次调用next方法时，由于函数已经遍历运行完毕，不再有其它状态，因此返回 {value: undefined, done: true}。如果继续调用next方法，返回的也都是这个值

##### 2、yield 表达式

###### （1）、yield 表达式只能用在 Generator 函数里面，用在其它地方都会报错

```js
{
  (function (){
    yield 1;
  })()

  // SyntaxError: Unexpected number
  // 在一个普通函数中使用yield表达式，结果产生一个句法错误
}
```

###### （2）、yield 表达式如果用在另一个表达式中，必须放在圆括号里面

```js
{
  function* demo() {
    console.log('Hello' + yield); // SyntaxError
    console.log('Hello' + yield 123); // SyntaxError

    console.log('Hello' + (yield)); // OK
    console.log('Hello' + (yield 123)); // OK

  }
}
```

###### （3）、yield 表达式用作参数或放在赋值表达式的右边，可以不加括号

```js
{
  function* demo() {
    foo(yield 'a', yield 'b'); // OK
    let input = yield; // OK
  }
}
```

###### （4）、yield 表达式和return语句的区别

**相似**：都能返回紧跟在语句后面的那个表达式的值
**区别**：

* 每次遇到 yield，函数就暂停执行，下一次再从该位置继续向后执行；而 return 语句不具备记忆位置的功能
* 一个函数只能执行一次 return 语句，而在 Generator 函数中可以有任意多个 yield

##### 3、yield* 表达式

如果在 Generator 函数里面调用另一个 Generator 函数，`默认情况下是没有效果的`

```js
{
  function* foo() {
    yield 'aaa'
    yield 'bbb'
  }

  function* bar() {
    foo()
    yield 'ccc'
    yield 'ddd'
  }

  let iterator = bar()

  for(let value of iterator) {
    console.log(value)
  }

  // ccc
  // ddd
}
```


上例中，使用 for...of 来遍历函数bar的生成的遍历器对象时，只返回了bar自身的两个状态值。此时，如果想要正确的在bar 里调用foo，就需要用到 yield* 表达式

yield* 表达式用来在一个 Generator 函数里面 执行 另一个 Generator 函数

```js
{
  function* foo() {
    yield 'aaa'
    yield 'bbb'
  }

  function* bar() {
    yield* foo()      // 在bar函数中 **执行** foo函数
    yield 'ccc'
    yield 'ddd'
  }

  let iterator = bar()

  for(let value of iterator) {
    console.log(value)
  }

  // aaa
  // bbb
  // ccc
  // ddd
}
```

#####  4、next() 方法的参数

yield表达式本身没有返回值，或者说总是返回undefined。next方法可以带一个参数，该参数就会被当作上一个yield表达式的返回值

> [rv] = yield [expression]

  expression：定义通过遍历器从生成器函数返回的值，如果省略，则返回 undefined
  rv：接收从下一个 next() 方法传递来的参数

先看一个简单的小栗子，并尝试解析遍历生成器函数的执行过程

```js
{
  function* gen() {
    let result = yield 3 + 5 + 6
    console.log(result)
    yield result
  }

  let it = gen()
  console.log(it.next())      // {value: 14, done: false}
  console.log(it.next())      // undefined    {value: undefined, done: false}
}
```


（此处分析过程纯属个人理解，有误之处，欢迎批评指正！）
第一次调用遍历器对象的next方法，函数从头部开始执行，遇到第一个 yield 暂停，在这个过程中其实是分了三步：

（1）、声明了一个变量result，并将声明提前，默认值为 undefined
（2）、由于 Generator函数是 “惰性求值”，执行到第一个 yield 时才会计算求和，并加计算结果返回给遍历器对象 {value: 14, done: false}，函数暂停运行
（3）、理论上应该要把等号右边的 [yield 3 + 5 + 6] 赋值给变量result，但是，由于函数执行到 yield 时暂定了，这一步就被挂起了

第二次调用next方法，函数从上一次 yield 停下的地方开始执行，也就是给result赋值的地方开始，由于next()并没有传参，就相当于传参为undefined


基于以上分析，就不难理解为什么说 yield表达式本身的返回值（特指 [rv]）总是undefined了。现在把上面的代码稍作修改，第二次调用 next() 方法传一个参数3，按照上图分析可以很快得出输出结果

```js
{
  function* gen() {
    let result = yield 3 + 5 + 6
    console.log(result)
    yield result
  }

  let it = gen()
  console.log(it.next())      // {value: 14, done: false}
  console.log(it.next(3))      // 3    {value: 3, done: false}
}
```


如果第一次调用next()的时候也传了一个参数呢？这个当然是无效的，next方法的参数表示上一个yield表达式的返回值，所以在第一次使用next方法时，传递参数是无效的。

从语义上讲，第一个next方法用来启动遍历器对象，所以不用带有参数。

```js
{
  function* gen() {
    let result = yield 3 + 5 + 6
    console.log(result)
    yield result
  }

  let it = gen()
  console.log(it.next(10))      // {value: 14, done: false}
  console.log(it.next(3))      // 3    {value: 3, done: false}
}
```


Generator 函数从暂停状态到恢复运行，它的上下文状态（context）是不变的。通过next方法的参数，就有办法在 Generator 函数开始运行之后，继续向函数体内部注入值。也就是说，可以在 Generator 函数运行的不同阶段，从外部向内部注入不同的值，从而调整函数行为。

```js
{
  function* gen(x) {
    let y = 2 * (yield (x + 1))   // 注意：yield 表达式如果用在另一个表达式中，必须放在圆括号里面
    let z = yield (y / 3)
    return x + y + z
  }

  let it = gen(5)
  /* 通过前面的介绍就知道这部分输出结果是错误的啦
    

    console.log(it.next())  // {value: 6, done: false}
    console.log(it.next())  // {value: 2, done: false}
    console.log(it.next())  // {value: 13, done: false}

  */

  /*** 正确的结果在这里 ***/
  console.log(it.next())  // 首次调用next，函数只会执行到 “yield(5+1)” 暂停，并返回 {value: 6, done: false}
  console.log(it.next())  // 第二次调用next，没有传递参数，所以 y的值是undefined，那么 y/3 当然是一个NaN，所以应该返回 {value: NaN, done: false}
  console.log(it.next())  // 同样的道理，z也是undefined，6 + undefined + undefined = NaN，返回 {value: NaN, done: true}
}
```


如果向next方法提供参数，返回结果就完全不一样了

```js
{
  function* gen(x) {
    let y = 2 * (yield (x + 1))   // 注意：yield 表达式如果用在另一个表达式中，必须放在圆括号里面
    let z = yield (y / 3)
    return x + y + z
  }

  let it = gen(5)

  console.log(it.next())  // 正常的运算应该是先执行圆括号内的计算，再去乘以2，由于圆括号内被 yield 返回 5 + 1 的结果并暂停，所以返回{value: 6, done: false}
  console.log(it.next(9))  // 上次是在圆括号内部暂停的，所以第二次调用 next方法应该从圆括号里面开始，就变成了 let y = 2 * (9)，y被赋值为18，所以第二次返回的应该是 18/3的结果 {value: 6, done: false}
  console.log(it.next(2))  // 参数2被赋值给了 z，最终 x + y + z = 5 + 18 + 2 = 25，返回 {value: 25, done: true}
}
```



```js
{
  function* gen(x) {
    let y = 2 * (yield (x + 1))   
    let z = yield (y / 3)
    z = 88    // 注意看这里
    return x + y + z
  }

  let it = gen(5)

  console.log(it.next())   // {value: 6, done: false}
  console.log(it.next(9))  // {value: 6, done: false}
  console.log(it.next(2))  // 这里其实也很容易理解，参数2被赋值给了 z，但是函数体内又给 z 重新赋值为88， 最终 x + y + z = 5 + 18 + 88 = 111，返回 {value: 111, done: true}
}

```

##### 5、与 Iterator 接口的关系

ES6 规定，默认的 Iterator 接口部署在数据结构的Symbol.iterator属性，或者说，一个数据结构只要具有Symbol.iterator属性，就可以认为是“可遍历的”（iterable）。

Symbol.iterator属性本身是一个函数，就是当前数据结构默认的遍历器生成函数。执行这个函数，就会返回一个遍历器。

由于执行 Generator 函数实际返回的是一个遍历器，因此可以把 Generator 赋值给对象的Symbol.iterator属性，从而使得该对象具有 Iterator 接口。

```js
{
  let obj = {}

  function* gen() {
    yield 4
    yield 5
    yield 6
  }

  obj[Symbol.iterator] = gen

  for(let value of obj) {
    console.log(value)
  }
  // 4
  // 5
  // 6

  console.log([...obj])    // [4, 5, 6]
}

```

传统对象没有原生部署 Iterator接口，不能使用 for...of 和 扩展运算符，现在通过给对象添加 Symbol.iterator 属性和对应的遍历器生成函数，就可以使用了

##### 6、for...of 循环

由于 Generator 函数运行时生成的是一个 Iterator 对象，因此，可以直接使用 for...of 循环遍历，且此时无需再调用 next() 方法

这里需要注意，一旦 next() 方法的返回对象的 done 属性为 true，for...of 循环就会终止，且不包含该返回对象

```js
{
  function* gen() {
    yield 1
    yield 2
    yield 3
    yield 4
    return 5
  }

  for(let item of gen()) {
    console.log(item)
  }

  // 1 2 3 4
}
```

##### 7.Generator.prototype.return()

Generator 函数返回的遍历器对象，还有一个 return 方法，可以返回给定的值(若没有提供参数，则返回值的value属性为 undefined)，并且**终结**遍历 Generator 函数

```js
{
  function* gen() {
    yield 1
    yield 2
    yield 3
  }

  let it = gen()

  it.next()             // {value: 1, done: false}
  it.return('ending')   // {value: "ending", done: true}
  it.next()             // {value: undefined, done: true}
}
```

#####  Generator 函数应用举例

###### 应用一

假定某公司的年会上有一个抽奖活动，总共6个人可以抽6次，每抽一次，抽奖机会就会递减

按照常规做法就需要声明一个全局的变量来保存剩余的可抽奖次数，而全局变量会造成全局污染，指不定什么时候就被重新赋值了，所以往往并不被大家推荐

```js
{
  let count = 6  // 声明一个全局变量

  // 具体抽奖逻辑的方法
  function draw() {
    // 执行一段抽奖逻辑
    // ...
    // 执行完毕
    console.log(`剩余${count}次`)
  }

  // 执行抽奖的方法
  function startDrawing(){
    if(count > 0) {
      count--
      draw(count)
    }
  }

  let btn = document.createElement('button')
  btn.id = 'start'
  btn.textContent = '开始抽奖'
  document.body.appendChild(btn)

  document.getElementById('start').addEventListener('click', function(){
    startDrawing()
  }, false)

}
```


事实上，抽奖通常是每个人自己来抽，每抽一次就调用一次抽奖方法，而不是点一次就一次性就全部运行完，是可暂停的，这个不就是 Generator 函数的意义所在吗？

```js
{
  // 具体抽奖逻辑的方法
  function draw(count) {
    // 执行一段抽奖逻辑
    // ...

    console.log(`剩余${count}次`)

  }

  // 执行抽奖的方法
  function* remain(count) {
    while(count > 0) {
      count--
      yield draw(count)
    }
  }

  let startDrawing = remain(6)

  let btn = document.createElement('button')
  btn.id = 'start'
  btn.textContent = '开始抽奖'
  document.body.appendChild(btn)

  document.getElementById('start').addEventListener('click', function(){
    startDrawing.next()
  }, false)
}

```

###### 应用二

由于HTTP是一种无状态协议，执行一次请求后服务器无法记住是从哪个客户端发起的请求，因此当需要实时把服务器数据更新到客户端时通常采用的方法是长轮询和Websocket。这里也可以用 Generator 函数来实现长轮询

```js
{
  // 请求的方法
  function* ajax() {
    yield new Promise((resolve, reject) => {
      // 此处用一个定时器来模拟请求数据的耗时，并约定当返回的json中code为0表示有新数据更新
      setTimeout(() => {
        resolve({code: 0})
      }, 200)
    })
  }

  // 长轮询的方法
  function update() {
    let promise = ajax().next().value    // 返回的对象的value属性是一个 Promise 实例对象
    promise.then(res => {
      if(res.code != 0) {
        setTimeout(() => {
          console.log('2秒后继续查询.....')
          update()
        }, 2000)
      } else{
        console.log(res)
      }
    })
  }

  update()
}
```