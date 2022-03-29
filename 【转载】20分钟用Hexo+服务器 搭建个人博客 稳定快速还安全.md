---
title: 【转载】浅谈JavaScript函数重载
date: 2022-3-2 09:23:01
summary: 
categories: 
  - blog

tags:
  - hexo
---

## 20分钟用Hexo+服务器 搭建个人博客 稳定快速还安全

先来看Hexo制作的制作的博客。可以看到，有良好的外观，对markdown语法的完美支持，并且可以支持一键部署，有350多个主题可以选择。好了废话不多说，我们来开始动手操作吧。

### 一、本地博客环境搭建

现在我们来到了电脑前，先来安装本地需要的搭建环境。本地只需要安装两个软件：一个是Node.js，另一个是Git.

Node.js的安装：先来安装Node.js ，直接到官方网站，下载后。像安装QQ一样。下一步、下一步、下一步。就安装完成了。安装完成，打开`PowerShell`，输入 `Node -v` ,如果出现版本号，说明你已经安装成功了。

Git的安装：我们再来看Git的安装，这个也非常简单，打开官网，然后下载，还是下一步，下一步。就可以安装成功。安装好后，还是打开`powerShell` 然后输入 `git —version`,出现版本号，说明安装成功。

这样本地环境就安装好了。我会把这个视频用到的所有链接都放在评论区的第一条，你自取就好。

### 二、**重点**-服务器端的环境搭建

有了本地环境，我们想要别人看到我们的博客，我们还需要云服务器。有人说用Github不好吗？我个人觉的Github现在的访问速度几乎没办法使用。个人博客不仅是自己的开发记录，还是对外名片，

说实话我认为程序员就应该有一台云服务器，没事自己捣鼓捣鼓，对个人的技术成长和作品展示都是有好处的，也是非常有意思的事情。

我们进入服务器的控制台，然后找到服务器，找到服务器的公网IP地址，我这里`180.76.183.66` 。可以使用任何的远程服务器链接软件。直接输入IP地址和密码，显示连接成功。

```PowerShell
yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel perl-devel
```

刷刷刷.........一会就全部安装完成了，我们在安装`git` 安装的命令如下

```PowerShell
yum install -y git
```

安装完成后用`git - -version`查看一下版本，能查到证明安装成功了。接下来创建git使用的用户。

```PowerShell
useradd jspang
passwd jspang // 设置密码
chmod 740 /etc/sudoers   // 设置权限
vim /etc/sudoers  // 修改root权限
```

使用`:set nu`打开vim的行数显示，按i直接进入编辑状态。输入下面的命令

```PowerShell
jspang ALL=(ALL)    ALL
```

直接`:wq!`，进行保存，保存后再次修改权限。因为 `sudoers`是只读文件，所有要使用 `!`进行保存，否则会失败。

修改完成后记得把这个文件的权限改回来，否则很容易被攻击。服务器一定要安全为主。

```PowerShell
chmod 600 /etc/sudoers   //改回权限
```

权限改好了，我们再来设置Nginx，当然你也可以用其他的服务器软件，不过我还是很喜欢Nginx的就使用了。

先创建网站跟目录，我这里放在`\home\hexo`下了。

```PowerShell
mkdir /home/hexo
chown jspang:jspang -R /home/hexo //授予权限
```

完成后正式开始安装Nigx软件

```PowerShell
yum install -y nginx  //安装nginx
systemctl start nginx.service  //启动Nginx服务
```

启动后修改`nginx.conf`配置文件。

```PowerShell
vim /etc/nginx/nginx.conf
```

修改项

```JSON
server {
        listen       80 default_server;
        listen       [::]:80 default_server;
        server_name  180.76.183.66;
        root         /home/hexo;
```

**保存退出后，重启服务器**

修改完配置以后，需要重启一下Nginx服务。

```PowerShell
systemctl start nginx.service  //重启启动Nginx服务
```

如果正常启动，没有任何报错，说明Nginx配置好了。

**建立git仓库**

```JSON
su root
cd /home/jspang
git init --bare blog.git  //创建Git仓库
chown jspang:jspang -R blog.git  //授予Git仓库权限
```

同步网站根目录

```JSON
cd blog.git/hooks/

vim post-receive
// 把下面的内容拷贝进去
#!/bin/sh
git --work-tree=/home/hexo  --git-dir=/home/jspang/blog.git checkout -f
```

再次修改权限，

```JSON
chmod +x post-receive
```

这样就已经把服务器端的环境基本配置好了。

### 三、本地安装和配置Hexo

本地环境和云服务器全部都准备好后，我们就可以正式搭建博客了。安装Hexo只需要一条命令，全局安装hexo-cli，刷的瞬间就安装成功了。

```PowerShell
npm install -g hexo-cli
```

然后我们找到要写博客的项目文件夹，我这里就选择 `E:\Code\`文件夹了，这个路径你可以自行选择，什么都可以，然后输入下面的命令。

```text
$ hexo init <folder>
$ cd <folder>
$ npm install
```

可以看到在文件夹下生成了很多文件，有了这些文件就可以在本地编写博客了。

安装完这一部后，我们一般会个性化配置我们的网站信息，所以这时候我们使用`code .` 打开VSCode，来修改代码。

打开`_config.yml`对下面这些代码进行配置。

```PowerShell
title: '技术胖'
subtitle: '技术胖的博客'
description: '技术胖有15年开发经验，每年出100集免费视频教程'
keywords: '前端开发'
author: JSPang
language: en
timezone: ''
```

配置完成就可以编写文章了。

### 四、本地编写文章和预览

你可以执行下列命令来快速创建一篇新文章或者新的页面

```PowerShell
hexo new pinia
```

这样一键就创建好了文章编写页面。默认的位置是。

```PowerShell
\source\_posts\pinia.md
```

然后把你写的markdown文章直接复制进去，粘贴复制，保存。就完成了。接下来就需要查看一下自己的文章和网站的样子了。打开VSCode的终端，然后安装`hexo-server`，输入下面的命令。

```PowerShell
npm install hexo-server --save
```

刷的一瞬间，就完成了安装，然后启动服务。

```PowerShell
hexo server
```

在浏览器输入地址：`[http://localhost:4000/](http://localhost:4000/)`,就可以看到你写的博客了。

### 五、把博客上传到云服务器

有了文章我们就可以把博客上传到云服务器了。但是要想用Git把代码传到服务器，是需要密钥的。这就就直接创建一下密钥。在本地电脑打开`powerShell`，创建密钥。创建密钥的命令是 `ssh-keygen -t rsa`

如果你已经有了密钥就不用再次创建了，特别是公司已经有很多git管理的项目时，否则需要都进行重新配置。我这里是已经有密钥了。

到服务端创建一个存放密钥的文件夹。

```PowerShell
su jspang
mkdir ~/.ssh   //创建存放密钥的文件夹
vim ~/.ssh/authorized_keys  //写入密钥
```

来到自己的客户端，找到`C:\Users\Administrator\.ssh` 打开`id_rsa`文件，直接复制全部，就可以完成了。

这样我们就可以通过jspang这个用户向服务器提交代码了，我们要测试一下，看看是否配置的可以连接上

**本地测试**

打开本地主机的`powerShell`，然后用ssh进行连接。

```PowerShell
ssh -v jspang@180.76.183.66 //服务器ip
```

修改本地的hexo配置文件`_config.yml`,打开文件后，拖动到最后边，输入下面的配置

```JSON
deploy:
  type: git
  repository: jspang@180.76.183.66:/home/jspang/blog.git
  branch: master
npm install --save hexo-deployer-git
```

安装完成后，输入下面的命令

```text
hexo clean
hexo g -d
```

如果一切正常，就可以直接传到服务器上，然后输入网址`180.76.183.66`就可以完成博客的浏览了，我这里没有使用域名，如果你有域名，只要把域名解析到这个网址就可以了。