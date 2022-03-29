---
title: HTML about Forms
date: 2021-12-05 20:20:47
summary: 
categories: 
  - Frond End

tags:
  - HTML
---
# HTML5表单验证

## 第一章 基本表单验证特征

### 一、HTML5中有那些类型

[HTML5的表单所有type类型 ](https://www.cnblogs.com/dadayang/p/5749068.html)

### 二、需要特殊记忆的特性

1、autocomplete：文本框中，输入一次下一次会自动提示；

2、autofocus：初始化页面之后，让input自动获得焦点；

3、list和datalist：

​	datalist与select类似，标签定义选项列表，通常与input元素配合使用该元素，datalist元素的内容不会直接显示在网页上，只是会在用户输入时作为候选项。

```html
        <input type='text' name='capital' list='address' />
        <datalist id="address">
            <option value="beijing">北京</option>
            <option value="shanghai">上海</option>
            <option value="shenzhen">深圳</option>
        </datalist>
```

​	datalist与select的区别：

|  异同点  | select | datalist |
| :------: | :----: | :------: |
|   多选   |  可以  |  不可以  |
|  缺失值  |  可以  |  不可以  |
|   查找   | 不可以 |   可以   |
| 增添选项 | 不可以 |   可以   |

4、required：设置表单元素为必填项；

5、pattern：表单验证使用正则表达式；比如要求邮箱的格式，==不符合规范不会提交==，并提示用户所输内容不符合规范

6、novalidate 和 formnovalidate：在设置表单元素必填的情况下，提交表单但不验证；

​	区别：novalidate 应用于表单，并防止验证；

​			   formnovalidate 应用于提交按钮，并覆盖 novalidate 选项（如果存在）；

​			   这意味着 ‘提交此表单而不验证，无论一般表单设置如何’。

代码展示：

```html
    <!-- <form action="post" novalidate> -->
    <form action="post">
        <table border="1px">
            <tr>
                <td> <label>邮箱:</label></td>
                <td><input type="email" placeholder="请输入注册邮箱！" name="email" required></td>
            </tr>
            <tr>
                <td><label>用户名:</label></td>
                <td><input type="text" placeholder="请输入用户名！" name="username" required autocomplete="on"></td>
            </tr>
            <tr>
                <td><label>密 码:</label></td>
                <td><input type="text" placeholder="请输入密码！" name="password" required pattern="^\d{5}[abcd]$"></td>
            </tr>
            <tr>
                <td>
                    <label for="">地址：</label>
                </td>
                <td>
                    <input type='text' name='capital' list='address' />
                    <datalist id="address">
                        <option value="beijing">北京</option>
                        <option value="shanghai">上海</option>
                        <option value="shenzhen">深圳</option>
                    </datalist>
                </td>
            </tr>
        </table>

        <!--<input type="submit" formnovalidate>-->
        <input type="submit">
    </form>
```

最终效果：

![最终效果](https://gitee.com/mr_tolie/pics/raw/master/images/202203271613948.png)

### 三、HTML约束验证的API

```H5中document.getElementById(" ") === id ，但这是H5的新特性，不推荐这样写```

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>validity</title>
</head>

<body>
    <form action="">
        <input type="text" id="username">
        <input type="submit">
    </form>

    <script>
        console.log(document.getElementById("username") === username)
    </script>
</body>
</html>
<!--
此页面，控制台输出结果为true；
证明H5中 document.getElementById(" ") === id是正确的
-->
```

#### 主要的HTML约束验证的API

1. willValidate属性：代表元素约束有没有被符合，没有被符合则返回false；
2. validity属性 *：表示元素当前所处的验证状态，表示验证是否成功；
3. validationMessage属性：用于描述与元素相关约束的失败信息；
4. checkValidity()方法 *：用的也很多，主要是看元素有没有满足他的任意约束，不满足返回false，满足返回true；
5. setCustomValidity()方法 *：设置自定义的验证信息。当表项设置成了required时候，可以用此方法设置/预定义弹出的提示信息；

#### validity属性的介绍及演示

* 属性介绍：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>validity</title>
</head>

<body>
    <form action="">
        <input type="text" id="username">
        <input type="submit">
    </form>

    <script>
        console.log(document.getElementById("username").validity)
    </script>
</body>
</html>
```

* 在此页面控制台上可以得到如下图所示的属性

![属性](https://gitee.com/mr_tolie/pics/raw/master/images/202203271613828.png)

* 代码演示：

```html
<!-- valueMissing属性值改成true-->
<input type="text" id="username" required>

<!-- patternMismatch属性值改成true-->
<input type="text" id="username" value="adfafea" pattern="^\d[5]">

<!-- typeMismatch属性值改成true，以type为email为例-->
<input type="email" id="email" value="adfafea">

<!-- rangeOverflow属性值改成true-->
<input type="number" id="number" max="5" min="3" value="6">
	
<!-- rangeUnderflow属性值改成true-->
<input type="number" id="number" max="5" min="3" value="1">

<!-- tooShort和tooLong 与 minlength和maxlength是对应的，但即使设置了这两个属性·，tooShort和tooLong依然会是false-->
```

#### checkValidity()方法的介绍及演示

* 方法介绍

checkValidity()方法 *：主要是看元素有没有满足他的任意约束，不满足返回false，满足返回true；

* 代码演示

```html
    <form action="" method="GET">
        <input type="text" id="username" name="username" value="12345" required pattern="^\d{5}">
        <input type="email" id="email" name="email" value="kfajihfioua@163.com">
        <input type="submit">
    </form>

    <script>
        if (username.checkValidity()) {
            alert("符合正则表达式")
        } else {
            alert("不符合")
        }
        if (email.checkValidity()) {
            alert("符合")
        } else {
            alert("不符合")
        }
```

#### setCust0mValidity()方法的介绍及演示

* 方法介绍

设置自定义的验证信息。当表项设置成了required时候，可以用此方法设置/预定义弹出的提示信息；

* 代码演示

```html
<body>
    <form action="" method="GET">
        <table>
            <tr>
                <td><label>密 码:</label></td>
                <td><input type="text" placeholder="请输入密码！" name="password" oninput="checkPaw(this)" required
                        pattern="^\d{5}$"></td>
            </tr>
        </table>

        <input type="submit">
    </form>

    <script type="text/javascript">
        function checkPaw(obj) {
            var password = obj.validity;
            if (true === password.valueMissing) {
                obj.setCustomValidity("密码不能为空！");
            } else if (true === password.patternMismatch) {
                obj.setCustomValidity("密码必须是5位数字！");
            }
        }
    </script>
</body>
```

### 四、HTML自带验证美化

要做出不一样的表单验证，需要==了解一些伪类和css选择器==

1. :required 和 :optional：前者必填，后者是选填
2. :in-range 和 :out-of-range：前者在范围之内，后者在范围之外
3. :valid 和 :invalid：前者不符合验证，后者符合验证
4. :read-only 和 :read-write： 前者为只读不能写，后者为可以写（在input或者div中匹配）

* 代码演示

==学完css回来补充==

(1). 默认气泡修改

* 思路：阻止默认气泡，后创建新的气泡

* 代码实现

==学完js再看一遍==
