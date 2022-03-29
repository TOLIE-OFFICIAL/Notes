---
title: deploy project
date: 2021-12-04 22:20:47
summary: 
categories: 
  - project-manage

tags:
  - project
---

## 部署说明
### 一、部署本地服务器
>1. 现将users.sql导入MySQL数据库，数据库名为users
>2. 数据库root用户的用户名设置为root，密码为666666
>3. 将fight.war导入eclipse或者idea，选用编码集UTF-8
>4. 为项目部署tomcat
>5. 访问http://localhost:8080/+项目名

### 二、部署网络服务器
1. 阿里云服务器

> 操作系统：CentOS 7.45  X64,
>
> 服务器：apache-tomcat-8
>
> JDK：oracle jdk 12.0.1
>
> 工具：SecureCRT 8.3和SecureFX 8.3
>
> 未使用宝塔面板辅助部署


2. 部署步骤
> 1. 上传sql文件并设置大小写不敏感
>
>    vi /etc/my.cnf
>    在[mysqld]后添加
>    lower_case_table_names=1
>    重启mysql
>    systemctl restart mysqld.service
>
>    
>
> 2. 创建数据库并导入数据
>
>    mysql -uroot -p+密码
>    
> CREATE DATABASE 数据库名 DEFAULT CHARACTER SET utf8;
>    
> ctrl+c退出数据库
>    
> mysql -u root -p+密码 --default-character-set=utf8 数据库名 < sql文件路径
>
> 
>
> 3. 部署到tomcat
>
>    * 修改server.xml
>    * 在<host 添加
>      <Context path="/名称" docBase="web文件路径" debug="0" reloadable="false" 
>    * 重启tomcat
>    
>    

3. 已上传的web项目信息

> 个人服务器地址：http://47.95.194.205:8080/fight/（服务器已过期）

