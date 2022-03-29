---
title: 【转载】Hexo 博客无法搜索的终极解决方法
date: 2022-03-06 11:52:29
summary: 
categories: 
  - blog

tags:
  - hexo
---

[转载自国光大佬，自行添加了自己遇到的问题](https://www.sqlsec.com)



![img](https://image.3001.net/images/20171229/15145248387556.jpg)


以前在 Hexo 的 next 主题上遇到了搜索框无法加载出来的问题，已经一系列分析查找，终于完美的解决了 Hexo 博客的 next 主题的搜索问题，同理其他 Hexo 主题解决方法大致相同。

# 概览

本次是在`Hexo`博客下的`next`主题进行测试的。一般`Hexo`博客无法搜索主要有`2`种以下情况:

- `搜索插件没有配置好`
- `文章中包含特殊字符`

`Hexo` 的搜索出了问题，点击搜索会一直转圈圈，搜索无法加载出来，如下图所示:

![img](http://pic.tolie.biz/images/202203061139467.png)



下面分别对这`2`情况进行解决。

# 搜索插件的配置

## 问题分析

浏览器审查元素，转到网络模块，然后点击搜索，发现`search.xml`的状态为`404`的状态，这表明这个文件不存在。

![img](https://image.3001.net/images/20171229/15145231219074.png)



## 解决方法

编辑 `站点配置文件`，新增以下内容到任意位置：





r

```yml
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```

编辑 `主题配置文件`，启用本地搜索功能：





r

```yml
# Local search
local_search:
  enable: true
```

**安装搜索插件**





ru

```powershell
C:\Users\CTF\Documents\GG
λ npm install hexo-generator-searchdb --save

+ hexo-generator-searchdb@1.0.8
added 119 packages in 8.327s
```

然后再重新生成静态文件，会发现 `Hexo` 博客的搜索功能已经可以正常使用了。

# 文章中特殊字符

## 问题分析

确保了搜索插件配置没有问题的情况下，有时候我们还是会遇到无法搜索的问题，浏览器调试发现:



![img](https://image.3001.net/images/20171229/1514523841767.png)



此时的`search.xml`文件存在，但是点击搜索的时候去找`search.xml`资源的时候发现是`304`的状态码，说明这个`xml`文件解析异常。

浏览器直接访问`search.xml`文件看看:

![img](http://pic.tolie.biz/images/202203061139070.png)


果然 `search.xml` 文件无法正常的解析。



查看返回包，找到文件中特殊字符的所在位置:

![img](https://image.3001.net/images/20171229/15145241354418.png)



用`Sublime Text3`和 `Visual Studio Code` 分别打开文件对比看看，这两个编辑器都找到了特殊字符。

![img](https://image.3001.net/images/20171229/15145243584788.png)



## 解决方法

既然知道了文件中特殊字符所造成生成的`search.xml`文件无法正常解析的话，那么解决也好解决了，就是删掉这些特殊字符。如果特殊字符比较多的话，建议使用 `Visual Studio Code` 去批量删除。
首先`标记特殊字符`，然后`Ctrl`+`F`键，全部查找出来。`展开替换按钮`，全部替换为`空`就可以啦。

![img](http://pic.tolie.biz/images/202203061139697.png)



然后再重新生成静态文件，会发现 `Hexo` 博客的搜索功能已经可以正常使用了。

# XML文件标签的开始结束符号不匹配

## 问题分析

插件没有问题，也没有特殊字符的情况下，我还是出现了本地搜索失效的问题。浏览器调试发现此时的search.xml状态码为200，应该没有问题，但搜索还有问题。

参考上方国光的解决方案，访问http://localhost:4000/search.xml发现

>XML error message Opening and ending tag mismatch



## 解决方案

修改问题位置的标签，**重点注意左尖括号和右尖括号**。

排除一处之后再次访问http://localhost:4000/search.xml，根据问题描述进行排错，直至出现

> This XML file does not appear to have any style information associated with it. The document tree is shown below.

然后再重新生成静态文件，会发现 `Hexo` 博客的搜索功能已经可以正常使用了。

![ 博客的搜索功能恢复](http://pic.tolie.biz/images/202203061150463.png)

