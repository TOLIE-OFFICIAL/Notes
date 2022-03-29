---
title: Ajax for beginner
date: 2021-10-27 20:20:47
summary: 
categories: 
  - Ajax

tags:
  - Ajax
---
### 第一章：原生AJAX

#### 1.1  AJAX简介

> 全称为Asynchronous Javascript And XML（异步JavaScript和XML）
>
> 不刷新页面的条件下，向服务端发送请求，即```无刷新获取数据``` 也是AJAX最大的优势！
>
> AJAX不是一门编程语言，而是一种将现有标准组合在一起使用的新方式。

##### AJAX优点

* 可以不刷新页面与服务器进行通信
* 允许根据用户事件来更新部分页面内容
* AJAX获得的数据被JS动态创建之后，这部分可以展示在网页，但信息不能被爬虫爬取

##### AJAX缺点 

* 没有浏览历史，不能回退
* 存在跨域问题（同源）

#### 1.2 XML简介

> XML：可扩展标记语言，被设计用来传输和存储数据，而HTML被设计用来呈现数据。
>
> 开始时AJAX就是使用XML格式进行数据交换，但```现已被JSON替换```

#### 1.3 node.js的安装

​		[2020 node.js的安装教程](https://blog.csdn.net/Small_Yogurt/article/details/104968169)

#### 1.4 AJAX发送GET请求

##### 1、AJAX的使用步骤：

1. 创建异步对象，即XMLHttpRequest对象；
2. 初始化，指定请求方法和请求url；
3. 发送请求；
4. 绑定onreadystatechange事件；
5. 确定服务器返回了所有对象后，处理返回结果；

##### 2、jsp页面代码

> 这里需要注意js文件的引入方式 src="${pageContext.request.contextPath}/js/weather.js" 
>
> 防止出现路径问题

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%--src="${pageContext.request.contextPath}/js/weather.js"--%>
<script type="text/javascript" src="${pageContext.request.contextPath}/js/weather.js"></script>
<link rel="stylesheet" href="css/index.css">
<html>
<head>
    <title>AJAX GET请求</title>
</head>
<body>
<input type="text" id="search" name="search" placeholder="请输入要查询的内容">
<input type="button" id="btn" value="查询" onclick="Check()">
<br>
<div  id="result" ></div>
</body>
</html>
```

##### 3、js内容

> 请求URL的填写：
>
> “ / + 项目发布名 + / servlet映射名称 ”
>
> 
>
> GET请求参数设置：
>
> 在URL后用？分割然后加上要提交的变量和变量值



```js
function Check() {
    // alert("hello")
    const result = document.getElementById("result");
    //1.创建XHR对象
    const xhr = new XMLHttpRequest();
    //2.初始化，设定请求方法和请求url
    xhr.open("GET", "/test/server?search=hh");
    //3.发送
    xhr.send();
    //4.绑定事件，处理返回的结果
    xhr.onreadystatechange = function () {
        // 判断服务端返回了所有数据
        if (xhr.readyState === 4) {
            // 判断返回响应是否成功
            if (xhr.status === 200) {
                // 结果处理
                result.innerHTML = xhr.response;
            }
        }
    }
}
```

##### 4、servlet的配置

（这里制定了路径，所以不用配置xml配置文件

```java
@WebServlet("/server")
public class searchServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String search = request.getParameter("search");
        System.out.println(search + ":发来一条get请求");
        response.setContentType("text/html;charset=utf-8");
        response.getWriter().write("get请求已收到");
    }
}
```

###### 		@WebServlet的属性列表

![@WebServlet的属性列表](https://gitee.com/mr_tolie/pics/raw/master/images/202203271609782.png)

#### 1.5 AJAX发送POST请求

##### 1、js内容

> 参数设置：
>
> 语法上参数设置比较的随意，只需要服务器端可以解析，就可以；
>
> send("a=100&b=100&c=100&d=100")或者send("hquwuifahfhoihqi")都可以传入服务器端
>
> 甚至可以自定义请求头的key和value（需要后端进行适配，否则会报错

```js
function post() {
    // alert("hello")
    const result = document.getElementById("result")
    //1.创建XHR对象
    const xhr = new XMLHttpRequest();
    //2.初始化，设定请求方法
    xhr.open("POST", "/test/server");
    //3.发送
    xhr.send();
    //xhr.send("a=100&b=100&c=100&d=100");
    //xhr.send("hquwuifahfhoihqi");
    
    //4.绑定事件，处理返回的结果
    xhr.onreadystatechange = function () {
        // 判断服务端返回了所有数据
        if (xhr.readyState === 4) {
            // 判断返回响应是否成功
            if (xhr.status === 200) {
                // 结果处理
                result.innerHTML = xhr.response;
            }
        }
    }
}
```

##### 2、servlet的配置（这里制定了路径，所以不用配置xml配置文件

```java
@WebServlet("/server")
public class searchServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("发来一条POST请求");
        response.setContentType("text/html;charset=utf-8");
        response.getWriter().write("POST请求已收到");
    }
}
```

#### 1.6  AJAX设置请求头信息

##### 1、HTTP请求头信息格式

```KEY：VALUE
KEY：VALUE
```

比如：
Contente-length:接下来的主体长度
Contente-type:接下来的主体类型

```js
// 设置请求头
xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded")
//这样就可解析 "a=100&b=100&c=100&d=100" 的格式数据
```

#### 1.7 Servlet返回json类型的数据

```java
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //指定返回的格式为JSON格式
        response.setCharacterEncoding("utf-8");
        request.setCharacterEncoding("utf-8");
        response.setContentType("application/json; charset=utf-8");
        //拼接json数据
        String jsonStr = "{\"name\":\""+"TOLIE"+"\",\"age\":\"20\"}";
        //将数据写入流中
        response.getWriter().write(jsonStr);
    }
}
```

#### 1.8 AJAX处理接收到的json类型返回结果

##### 1、手动对json数据转化

```js
function get() {
    // 建立div对象
    const result = document.getElementById("result")
    //1.创建XHR对象
    const xhr = new XMLHttpRequest();
    //2.初始化，设定请求方法
    xhr.open("GET", "/test/server");
    //3.发送
    xhr.send();
    //4.绑定事件，处理返回的结果
    xhr.onreadystatechange = function () {
        // 判断服务端返回了所有数据
        if (xhr.readyState === 4) {
            // 判断返回响应是否成功
            if (xhr.status === 200) {
                // 5.结果处理
                //手动对json数据转化
                let data = JSON.parse(xhr.response);
                console.log(xhr.response);
                result.innerHTML = data.name;                
            }
        }
    }
}
```

##### 2、自动对json数据转化

```js
function get() {
    // alert("hello")
    const result = document.getElementById("result")
    //1.创建XHR对象
    const xhr = new XMLHttpRequest();
    
    // 设定响应体数据的一个类型
    xhr.responseType = "json";
    
    //2.初始化，设定请求方法
    xhr.open("GET", "/test/server");
    //3.发送
    xhr.send();
    //4.绑定事件，处理返回的结果
    xhr.onreadystatechange = function () {
        // 判断服务端返回了所有数据
        if (xhr.readyState === 4) {
            // 判断返回响应是否成功
            if (xhr.status === 200) {
                // 结果处理
                
                //自动对json数据转化
                result.innerHTML = xhr.response.age;
            }
        }
    }
}
```

#### 1.9 AJAX的IE缓存问题

##### 1、IE缓存

在ajax的应用中，当用户访问一次后，再进行访问当XMLHttpRequest请求不变的时，在ie中获取数据不会到服务器端取，而是直接从ie的缓存中取，这会就是ie的缓存问题。==IE缓存可能会导致一些时效性很强的请求不能正常获取最新数据==。

##### 2、解决方案：添加时间戳

```js
	//2.初始化，设定请求方法
    xhr.open("GET", "/test/server?t="+Date.now());
```

Date.now()就是获取一个当前时间，让每一次请求都不相同，避免不能正常获取最新数据。

#### 1.10 AJAX的网略请求超时和网络异常处理

##### 1、主要目的

让用户在网络请求超时或者网络异常的时候可以收到提醒，避免长时间无响应，优化使用体验。

##### 2、处理方式

* 网络请求超时处理

```js
//设置超时2s，即超过两秒没有收到回应，就取消请求
xhr.timeout = 2000;

//设置超时事件之后的方法
xhr.ontimeout = funcation(){
    //比如可以是弹窗等等显示或操作
    alert("请求超时，请稍后重试！");
}
```

* 网络异常处理

```js
//设置网络异常事件之后的方法
xhr.error = funcation(){
	//比如可以是弹窗等等显示或操作
    alert("网络异常，请检查你的网络！");
}
```

#### 1.11 取消AJAX请求

##### 1、js的ES6规范中let和const

```let 声明的变量只在 let 命令所在的代码块 {} 内有效，在 {} 之外不能访问。```

```const 声明一个只读的常量，一旦声明，常量的值就不能改变。```

##### 2、 取消AJAX请求

调用XMLHttpRequest对象的abort()方法，即可完成请求的取消；

```js
    //获取所有的button对象
    const btns = document.querySelectorAll("button");	
    //通过let新建一个变量x
	let x = null;
	
	//给第一个button绑定事件
    btns[0].onclick = function () {
        x = new XMLHttpRequest();
        x.open("GET","/test/server")
        x.send();
    }
	//给第二个button绑定事件
    btns[1].onclick = function () {
        x = new XMLHttpRequest();
        //取消请求
        x.abort();
    }
```

#### 1.12 处理用户重复发送请求

###### 1、目的

防止服务器收到高频率的相同请求，导致服务器不能及时响应，影响服务器性能

###### 2、处理

选择在用户第二次触发事件的时候，将上一个相同请求取消掉

```js
//通过let新建一个变量x
let x = null;
//设置一个标识变量，帮助判断请求是否正在发送
let isSending = false;
//获取所有的button对象
const btns = document.querySelectorAll("button");
btns[0].onclick = function () {
    //如果请求正在发送，就取消请求
    if (isSending) {
        x.abort();
    }
    //如果没有请求正在发送，就取消请求
    x = new XMLHttpRequest();
    //c请求正在发送，更改标识变量
    isSending = true;
    x.open("GET", "/test/server")
    x.send();
    x.onreadystatechange = function () {
        if (x.readyState === 4) {
            //请求发送结束，更改标识变量
            isSending = false;
        }
    }
}
```

