---
title: HTTP协议详解
date: 2021-11-27 22:20:47
summary: 
categories: 
  - Net

tags:
  - HTTP
---
# HTTP协议详解
## 学习内容：
一、原理
1.	形象理解Http协议
2.	动手试试Http协议
3.	Http协议三部分介绍

二、实战
1.	PHP + socket编程发送http请求
2.	PHP批量发帖
3.	Http协议的防盗链

三、优化
1.	Http协议与缓存控制
2.	Http协议与Cookie
3.	持久链接


## 学习内容：
### 一、原理
#### A.	形象理解Http协议
#####  1） Http协议的定义：
> 
> 计算机协议和现实的协议是一样的，双方多方都遵循这一个共同的规范，这就是协议。计算机可以全世界共通，这些协议功不可没。
> 
> HTTP协议就是按照一定的规则，向服务器索要数据/发送数据。服务器安照一定的规则进行回应。

#####  2） Http协议的工作流程

> 1、原始状态下客户端与服务器没有连接；（连接就是虚拟电路）
>    
> 2、建立链接发送请求到服务器；
> 
> 3、服务器沿着建立的连接，返回响应信息。客户端收到响应，并进行解析；
> 
> 4、断开连接。


#####  3） Http请求信息和响应信息的格式

###### 1、请求信息


> ​	请求行；
> ​	请求头信息；
> ​	（换行）
> ​	请求主体信息（可无）

**！！换行用来分开请求/响应头信息和请求/响应主体信息虽主体信息可有可无，但此空行一定要有。**

请求行分为三部分：

请求方法、请求路径(URL)、所用的协议。

> 请求方法包括：GET POST HEAD PUT DELETE TRACE OPTIONS
>
> 请求路径就是URL的一部分

请求头信息格式：

> KEY：VALUE
> KEY：VALUE
> ………………
> Contente-length:接下来的主体长度
> Contente-type:接下来的主体类型

---------------------------------------------------

######  2、响应信息

				响应行
				响应头信息
				（换行）
				响应主体信息

**！！换行用来分开请求/响应头信息和请求/响应主体信息虽主体信息可有可无，但此空行一定要有。**

响应主体信息可以是HTML或者其他内容

响应行分为三部分：

>  协议 状态码 状态文字信息
> 状态文字信息是像‘ok’这样

响应头信息格式： 

>  KEY：VALUE
> KEY：VALUE
> ………………
> 例如：HTTP/1.1 200 OK
> 	 Contente-type:text/html
> 	 Contente-length:5


#####  4） 请求方法
  ``GET POST HEAD PUT DELETE TRACE OPTIONS``

> （注意要大写
> 
> （注意：这些请求方法虽然Http协议里规定了，但可能有Web Service不支持这些方法。）

###### 1、HEAD与GET方法基本一致，只是不返回内容

###### 2、POST的请求方法
```
	因为POST比GET多了主体信息
	
	所以要在请求头信息里表明主体信息的长度content－length
	
	还要标明主体信息的类型content-type:application/x-www-form-urlencoded
```



###### 3、POST和GET请求区别的常见误区

<span style="color:orange">请求参数长度限制：GET请求长度最多1024kb，POST对请求数据没有限制</span>

1、首先即使有长度限制，也是限制的是**整个 URI 长度**，**而不仅仅是你的参数值数据长度**。

2、`HTTP 协议从未规定 GET/POST 的请求长度限制是多少`。

3、所谓的请求长度限制是由**浏览器**和 **web 服务器**决定和设置的，各种浏览器和 web 服务器的设定均不一样，这依赖于各个浏览器厂家的规定或者可以根据 web 服务器的处理能力来设定。



<span style="color:orange">GET请求一定不能用request body传输数据</span>

`GET可以带request body，但不能保证一定能被接收到`。如果你用GET服务，在request body偷偷藏了数据，不同服务器的处理方式也是不同的，有些服务器会帮你读出数据，有些服务器直接忽略。



<span style="color:orange">POST比GET安全性要高</span>

这里的安全是相对性，通过GET提交的数据都将显示到URL上，`页面会被浏览器缓存`，其他人查看历史记录会看到提交的数据，而POST不会。另外GET提交数据还可能会造成CSRF攻击。



<span style="color:orange">GET产生一个TCP数据包，POST产生两个TCP数据包</span>

对于GET方式的请求，浏览器会把http header和data一并发送出去，服务器响应200 OK(返回数据);
而对于POST，浏览器先发送header，服务器响应100 continue，浏览器再发送data，服务器响应200 OK(返回数据)。注意，`尽管POST请求会分两次，但body 是紧随在 header 后面发送的，根本不存在『等待服务器响应』一说`。



###### 4 POST和GET请求的区别小结

`请求参数`：GET请求参数是通过URL传递的，多个参数以&连接，POST请求放在request body中。
`请求缓存`：GET请求会被缓存，而POST请求不会，除非手动设置。
`收藏为书签`：GET请求支持，POST请求不支持。
`安全性`：POST比GET安全，GET请求在浏览器回退时是无害的，而POST会再次请求。
`历史记录`：GET请求参数会被完整保留在浏览历史记录里，而POST中的参数不会被保留。
`编码方式`：GET请求只能进行url编码，而POST支持多种编码方式。
`对参数的数据类型`：GET只接受ASCII字符，而POST没有限制。

> 这里还想补充说明一点，就是通过浏览器地址栏输入URL访问资源的方式都是**GET**请求。



###### 5、TRACE应用情况：

比如用了代理上网，想查看代理有没有修改Http请求，这种情况就可以用到TRACE，服务器回把最后收到的请求返回给客户端。

###### 6、OPTIONS：
返回服务器可用的请求方法。




#####  5） 状态码和状态文字
> 状态码用来反映服务器的响应情况
> 
> 状态文字用来描述状态码的
> 
###### 常见的状态码
	200 OK：服务器正常返回网页
	301/2：永久/临时重定向 （可能会在重定向过程中丢失数据，比如POST可能会变成GET导致数据丢失）
	304 Not Modified：未修改（请求的内容未修改，告诉客户端到缓存里取
	307 Temporay Redirect：在重定向中保持原有数据 
###### 失败的状态码－
 	404 NOT FOUND：请求的网页不存在
 	500：服务器内部错误
 	503：服务器暂时不可用


###### 状态码	定义	说明
	1XX	信息	收到请求，继续处理
	2XX	成功	操作成功收到、理解、接受
	3XX	重定向	为了完成请求，必需采取进一步措施
	4XX	客户端错误	请求的语法有明显错误或不能完全被满足
	5XX	服务端错误	服务器无法完成明显有效的请求



B.	动手试试Http协议
C.	Http协议三部分介绍

二、实战
A.	PHP + socket编程发送http请求
B.	PHP批量发帖
C.	Http协议的防盗链

三、优化
A.	Http协议与缓存控制
B.	Http协议与Cookie
C.	持久链接

