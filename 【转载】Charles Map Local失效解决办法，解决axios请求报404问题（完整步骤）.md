---
title: 【转载】Charles Map Local失效解决办法，解决axios请求报404问题（完整步骤）
date: 2022-02-19 18:39:55
summary: 
categories: 
  - Error

tags:
  - solution
---

[转载CSDN自喷气式水母](https://blog.csdn.net/weixin_43735348/article/details/100824002)

#### 问题提出

最近学习React过程中，写axios请求时，需要使用Charles重定向，反复报404错误。通过查阅Charles文档、StackOverflow相似情况回答，完整解决。有同样问题的朋友，可以跟着本文一步步操作，如果依然有问题，欢迎在下方评论区交流！

axios请求代码块：

componentDidMount() {
        axios.get('/api/todolist').then((res) => {
            alert('success');
        }).catch((err) => {
            alert('error');
        });
}
使用Charles Map Loacl重定向：

![img](http://pic.tolie.biz/images/202202121737852.png)

 

todolist.json文件内容如下，随意写的，很普通：

![img](http://pic.tolie.biz/images/202202121735360.png)

 

刷新浏览器后报错：

![img](http://pic.tolie.biz/images/202202121735060.png)

 

查看控制台Network，todolist请求报404错误：

![img](http://pic.tolie.biz/images/202202121735954.png)

 

查看Charles，没有抓取本地请求，空空如也：

![img](http://pic.tolie.biz/images/202202121736254.png)

 

#### 问题分析

Charles文档中找到了对Localhost的相关说明，附上链接：https://www.charlesproxy.com/documentation/faqs/localhost-traffic-doesnt-appear-in-charles/

![img](http://pic.tolie.biz/images/202202121736837.png)

Charles原理是把自身变为一个中间代理服务器，便于抓包。文档大意是某些系统会采用硬编码方式使本地的数据访问不使用代理，导致无法使用Charles重定向。官方给出的解决方案是使用http://localhost.charlesproxy.com/替代localhost。

再来看看StackOverflow上相关回答，附上链接：https://stackoverflow.com/questions/15183108/view-127-0-0-18080-traffic-in-charles-proxy

![img](http://pic.tolie.biz/images/202202121737658.png)

解决方案与官方给出的相同，使用localhost.charlesproxy.com替代localhost。

 

#### 解决问题

下面根据分析解决此问题。

首先，修改axios代码块中get的url（为什么http://localhost.charlesproxy.com后面要加:3000呢？因为我们使用的是3000端口）：

```js
componentDidMount() {
        axios.get('http://localhost.charlesproxy.com:3000/api/todolist').then((res) => {
            alert('success');
        }).catch((err) => {
            alert('error');
        });
}
```


随后，修改Charles中Map Local设置（只需要把Host栏改成localhost.charlesproxy.com即可）：

![img](http://pic.tolie.biz/images/202202121736207.png)

 

然后刷新浏览器（嗯？还是报错）：

![img](http://pic.tolie.biz/images/202202121736166.png)



我们来看网页地址：地址还是localhost，需要手动输入新地址localhost.charlesproxy.com:3000

![img](http://pic.tolie.biz/images/202202121736457.png)

![img](http://pic.tolie.biz/images/202202121737984.png)

问题解决！
