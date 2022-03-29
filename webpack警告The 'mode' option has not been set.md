---
title: webpack警告The 'mode' option has not been set
date: 2022-3-3 18:41:49
summary: 
categories: 
  - Error

tags:
  - solution
---

### webpack警告The 'mode' option has not been set



![报错](http://pic.tolie.biz/images/202203031842913.jpeg)



> WARNING in configuration
> The 'mode' option has not been set, webpack will fallback to 'production' for this value. Set 'mode' option to 'development' or 'production' to enable defaults for each environment.
> You can also set it to 'none' to disable any default behavior. Learn more: https://webpack.js.org/configuration/mode/

提示这个的时候，需要在webpack配置文件webpack.config.js中，设置mode，如设置为开发环境

```js
module.exports = {
  mode: 'development'
};
```