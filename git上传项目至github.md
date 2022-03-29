---
title: update project
date: 2021-12-23 14:20:47
summary: 
categories: 
  - project-manage

tags:
  - project
---

### 一、打开终端

* cd 直接将项目文件夹拖进来；

### 二、输入

1. cd 直接将项目文件夹拖进来；

2. git init

3. git config --global user.name “你的账户名”

4. git config --global user.email "你的账户邮箱"

5. git add 直接将项目文件夹拖进来

6. git commit -m "对项目文件进行注释"

   > 这时候点击回车键，会生成一些描述，就是将项目中的各种文件都进行了创建，并创建相关的描述文件，我们可以对README.md文件进行编辑（下面会提到在哪里进行项目说明）

7. git remote add origin https://URL

   > 这时候如果中断中提示：fatal: remote origin already exists.，已经存在了，不用管，执行下一步

8. git push -u origin maste



原文链接：https://blog.csdn.net/m0_37625794/article/details/73549997