---
title: react-Loadable实现异步加载
date: 2022-3-2 15:53:24
summary: 
categories: 
  - Frond End

tags:
  - React
---



#### react-Loadable实现异步加载

##### 一、引入react-Loadable模块

> npm install react-Loadable
>
> yarn add react-Loadable



##### 二、使用react-Loadable

###### a.创建loadable.js文件

```js
import Loadable from 'react-loadable';
import * as components from './components'

const LoadableComponent = Loadable({
    //指明异步加载的路径
    loader: () => import('./index'),
    //加载过程中展示的组件
    loading: components.Loading
});
//通过回调函数返回定义好的<LoadableComponent/>
export default () => {
    return <LoadableComponent/>
}
```

###### b.修改路由

```js
import React from "react";
import {Route, Routes} from 'react-router-dom';
import Home from "./pages/home";
import Detail from "./pages/detail/loadable";
import SignIn from './pages/signIn';
import SignUp from './pages/signUp';

function App() {
    return (
        <Routes>
            <Route path='/' element={<Home/>} exact/>
            <Route path='/detail/:id' element={<Detail/>} exact/>
            <Route path='/sign_in' element={<SignIn/>} exact/>
            <Route path='/sign_up' element={<SignUp/>} exact/>
        </Routes>
    );
}

export default App;
```

