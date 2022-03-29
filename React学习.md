---
title: React for beginner (part 1)
date: 2022-02-15 13:05:42
summary: 
categories: 
  - Frond End

tags:
  - React
---

`react最高兼容到ie 8`

#### 虚拟DOM

##### 1). 原理

![虚拟DOM原理](http://pic.tolie.biz/images/202202101437897.png)



##### 2). 虚拟DOM的diff算法

**关键**：同级比对

![虚拟DOM的diff算法](http://pic.tolie.biz/images/202202101458972.png)



#####  列表循环中key的必要性

底层是对key相同的DOM进行比对，如果key值发生变换，则key就失去了本来的意义

> **注意**：不要用index作为key值

![列表循环中key的必要性](http://pic.tolie.biz/images/202202101505969.png)



#### react中的生命周期函数                                              

* 生命周期函数指的是在某一时刻会自动调用执行的函数；
* 生命周期函数是针对组件来说的，父组件、子组件都有生命周期函数；

##### React组件的生命周期                                           

![React组件的生命周期](http://pic.tolie.biz/images/202202111736972.png)

###### Mounting

*componentWillMount* 和 *componentDidMount* 只在页面挂载的时候执行

###### Updation

*shouleComponentUpdate* 函数要求返回的是一个bealoon类型的值。如果返回为true则执行后续函数对页面进行更新，反之则不进行更新。

*componentWillReceiveProps* 当一个组件从父组件接受参数，如果这个组件第一次存在于负组件中不会执行；如果这个组件`之前已经存在于父组件中`才会执行。

###### Unmounting

*componentWillUnmount* 当组件即将从页面中移除的时候，才会被执行

 

##### 生命周期函数的使用场景

```js
//用于提升性能，如果接下来的props与之前的相等就不执行render函数
// shouldComponentUpdate(nextProps, nextState, nextContext) 接受这些参数
shouldComponentUpdate(nextProps, nextState, nextContext) {
    if (nextProps.item !== this.props.item) {
        return true;
    } else {
        return false;
    }
}
```



#### React中使用AJAX（axiso模块

要通过第三方模块才可以发送Ajax请求

* `一般放在componentDidMount()中`，此函数只在页面挂载时执行一次
* 一般不放在componentWillMount()中，

```js
componentDidMount() {
    axios.get('http://localhost.charlesproxy.com:3000/api/TodoList')
        .then((res) => {
        this.setState(() => ({
            finished_list: [...res.data],
        }));
    })
        .catch(() => {
        alert('error')
    })
}
```



#### React中使用动画效果（react-transition-group模块

[官方文档](https://reactcommunity.org/react-transition-group/)

```js
// in ={this.state.show}属性用来指出根据哪个值判断
// timeout = {1000}属性指出动画执行时间
// classNames="fade"指出类名前缀
// unmountOnExit 退出时移除元素
// appear={true} 挂载时也有动画

<CSSTransition
    timeout={1000}
    classNames='fade'
    appear={true}
    key={index}
>
    <div>{item}</div>
</CSSTransition>
```



#### React Redux

##### Redux概念简述

> Redux = Reducer + Flux

把`数据集中存储`，尽量不在组件中保存数据。各个组件都从store中获取数据。解决了react中传值的困难。

![React Redux](http://pic.tolie.biz/images/202202122142491.png)

##### redux的工作流程

![redux的工作流程](http://pic.tolie.biz/images/202202122153536.png)



##### redux-devtools-extension的使用

[redux-devtools-extension的使用](https://github.com/zalmoxisus/redux-devtools-extension)



##### store

```js
constructor(props) {
    super(props);
    this.state = store.getState();
    this.searchFocus = this.searchFocus.bind(this);
    this.searchBlur = this.searchBlur.bind(this);
    this.handleStoreChange = this.handleStoreChange.bind(this);
}

componentDidMount() {
    store.subscribe(this.handleStoreChange);
}    
reder(){
    .................
}

handleStoreChange() {
    this.setState(store.getState());
}
```



###### subscribe

Store 允许使用 `store.subscribe` 方法设置监听函数，一旦 State 发生变化，就自动执行这个函数。

```js
import { createStore } from 'redux';
const store = createStore(reducer);

store.subscribe(listener);
```

显然，只要把 View 的更新函数（对于 React 项目，就是组件的render方法或setState方法）放入listen，就会实现 View 的自动渲染。

store.subscribe方法返回一个函数，调用这个函数就可以解除监听。

```js
let unsubscribe = store.subscribe(() =>
  console.log(store.getState())
);

unsubscribe();
```



##### 利用redux下的combineReducers，对reducer进行拆分

根目录下的store/index

```js
import {combineReducers} from "redux";
import headerReducer from '../common/header/store/reducer'

//导出整合之后的reducer
export default combineReducers({
    header: headerReducer,
})
```

组件目录下的store/index

```js
const defaultState = {
    focus: false,
};
const reducer = (state = defaultState, action) => {
    if (action.type === 'search-focus') {
        return {
            focus: true,
        }
    }
    if (action.type === 'search-blur') {
        return {
            focus: false,
        }
    }
    return state;
};
export default reducer;

```



##### 总结

![redux要点](http://pic.tolie.biz/images/202202132057652.png)

![redux的重要api](http://pic.tolie.biz/images/202202132057078.png)



#### React中管理css（styled-components模块

styled-components是一个针对React的 css in js 类库（[官方文档](https://styled-components.com/docs)、[基本使用](https://www.cnblogs.com/wswm/p/10692168.html)）

它的优点在于：

- 贯彻React的 *everything in JS*理念，降低js对css文件的依赖
- 组件的样式和其他组件完全解耦，`有效避免了组件之间的样式污染`

**index.js中**

```js
//index.js中
import React, {Fragment} from 'react';
import ReactDOM from 'react-dom';
import {Globalstyle} from "./style";
import App from './App';

ReactDOM.render(
    <Fragment>
        <Globalstyle/>
        <App/>
    </Fragment>,
    document.getElementById('root')
);
```



##### styled-components模块导入iconfont

2. 接下来就要在项目的statics文件夹下把这四个文件加进font文件夹，并创建iconfont.js文件，文件结构如下图：

![img](http://pic.tolie.biz/images/202202172043046.png)

3. 针对新创建iconfont.js中内容进行编写：

```js
import { createGlobalStyle } from 'styled-components';

export const IconStyle = createGlobalStyle`
&.iconfont {
  font-family: "iconfont" !important;
 
 &.iconfont {
  font-family: "iconfont" !important;
  font-size: 16px;
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

&.icon-icon-pencil:before {
  content: "\\e670";
}
&.icon-zhinanzhen:before {
  content: "\\e60c";
}
&.icon-Aa:before {
  content: "\\e636";
}
`
```

4. 最后在需要用到的组件中引用一下：

```js
<Button className='wr'>
     <IconStyle />
     <i className='iconfont icon-icon-pencil'></i>
       写文章
</Button>
```



#### UI组件与容器组件的拆分

> ui组件负责页面的渲染，容器组件负责页面的逻辑



#### 无状态组件

一个组件如果只有reader函数的话，我们可以将其修改为一个`无状态组件`

> 无状态组件只是一个函数，如果是一般的组件，其本质是一个js的类，还包含其他的一些内容，比如生命周期函数等，所以无状态组件性能更好。

```js
const TodoListUI = (props) => {
    return (
        <Fragment>
            <header>
                <div className="header_con w">
                    <a href="../public/index.html" className='logo fl'>TodoList</a>
                    <div className="fr">
                        <Input
                            value={props.inputValue}
                            placeholder="todo Info"
                            onChange={props.inputChange}
                        />
                        <Button
                            type="primary"
                            onClick={props.btnClick}
                        >添加</Button>
                    </div>
                </div>
            </header>

            {/*通过renderItem向后续组件传递参数index*/}
            <article>
                <div className='contain w'>
                    <div className='doing w'>
                        <h4>正在进行</h4>
                        <i>0</i>
                        <List
                            itemLayout="horizontal"
                            dataSource={props.list}
                            renderItem={(item, index) => (
                                //下面这个onClick的回调函数要注意
                                <List.Item>
                                    <Radio onClick={(index) => props.delete_item(index)}>
                                        {<div/>}
                                    </Radio>

                                    <List.Item.Meta
                                        title={<a href="https://ant.design">{item.title}</a>}
                                        description="Ant Design, a design language for background applications, is refined by Ant UED Team"
                                    />
                                </List.Item>
                            )}
                        />
                    </div>
                </div>
            </article>
        </Fragment>
    )
}
//UI组件只负责页面显示
// class TodoListUI extends Component {
//     render() {
//         return (
//             // Fragment占位符，不适用有含义的标签；
//
//         )
//     }
// }
```



#### redux中间件

中间件主要影响的是dispatch的过程

​	如果dispatch方法收到的是一个对象，dispatch就会直接将这个对象传递给store；

​	但是如果收到的是一个函数，dispatch就不会直接提交，先将收到的函数执行。 

![redux流程-plus中间件](http://pic.tolie.biz/images/202202142258138.png)



##### 使用Redux-thunk中间件异步操作（ajax请求为例

[官方文档](https://github.com/reduxjs/redux-thunk)

redux-thunk可以将复杂的逻辑或者异步的请求放到action里进行处理。

```js
//redux-thunk使得可以创造一个函数性质的action
export const getInneList = () => {
    return (dispatch) => {
        axios.get('/api/TodoList')
            .then((res) => {
                    // console.log(res.data);
                    const action = getList(res.data);
                    dispatch(action);
                }
            )
    }
};
```



##### 使用Redux-saga中间件进行异步操作（ajax请求为例





#### React-redux的使用

##### 核心API

###### 1.Provider 

Provider将组件与store进行连接,

```js
<//允许TodoList组件访问store
    Provider store={store}>
        <TodoList/>
    </Provider>;
```

###### 2.connect	

connect表示什么和什么做链接，通过mapStatetoProps方法，返回一个对象，指明怎么做链接，将store中的数据转化为组件的props

```js
export default connect(mapStateToProps, mapDispatchToProps)(TodoList);
```





#### immutable. js的使用

- [immutable-js](https://github.com/facebook/immutable-js)它是一个完全独立的库，无论基于什么框架都可以用它，它可以维持javascript不可变数据。
- 意义在于它弥补了Javascript没有不可变数据结构的问题。不可变数据结构是函数式编程中必备的。

```js
import * as actionTypes from "./actionTypes";
import {fromJS} from "immutable";
//d导入formJS方法，将state转化为immutable对象
const defaultState = fromJS({
    focus: false,
});
//对immutable对象调用set方法，返回一个新的修改过的immutable对象
const reducer = (state = defaultState, action) => {
    if (action.type === actionTypes.searchFocus) {
        return state.set('focus',true);
    }
    if (action.type === actionTypes.searchBlur) {
        return state.set('focus',false);
    }
    return state;
};
export default reducer;
```

##### 主要API

###### 1.get()

getimmutable对象的get方法可以获取immutable对象的某一个属性值；

###### 2.getIn()

另一种获取属性值的方法，参数为一个数组

```js
//数组第一项是immutable对象的一个属性名，其属性值也是一个immutable对象
//数组第二项是子immutable对象的子属性名
//state > header > focus immutable对象state下的immutable对象header的focus属性的属性值
state.getIn(['header','focus'])
```

###### 3.set()

immutable对象的set方法，会结合之前immutable对象的值和设置的值，返回一个全新的对象；

###### 4.merge()

同时改变多个immutable对象的属性值

```js
return state.merge({
    searchList: action.searchList,
    pageNum: action.pageNum
})
```

###### 5.toJS()

将immutable对象转变为普通的js对象

###### 6.fromJS()

将普通js对象转变为immutable对象

```js
import {fromJS} from "immutable";
//d导入formJS方法，将state转化为immutable对象
const defaultState = fromJS({
    focus: false,
    mouseIn: false,
    searchList: [],
    page: 1,
    pageNum: 1,
    angle:0
});
```



##### redux-immutable规范数据格式

**思路**：immutable. js + redux-immutable



#### React路由

react-router-dom @ > 6.0

```js
//App.js

import React, {Fragment} from "react";
import {BrowserRouter as Router, Route, Routes} from 'react-router-dom';
import Header from "./common/header";
import Footer from "./common/footer";
import Home from "./pages/home";
import Detail from "./pages/detail";

function App() {
    return (
 			<Router>
            <Header/>
                <Routes>
                    <Route path='/' element={<Home/>} exact/>
                    <Route path='/detail' element={<Detail/>} exact/>
                </Routes>
            <Footer/>
         </Router>
    );
}

export default App;
```





#####  React Router中的Link和NavLink组件有什么区别？

[转载于简书-潇湘轮回](https://www.jianshu.com/u/0fd9438d0145)

###### Link

我们开发网页应用需要在各个页面间切换，如果使用锚点元素实现，在每次点击时，页面被重新加载，React Router提供了&lt;Link&gt;组件用来避免这种状况发生。当你点击&lt;Link&gt;时，url会更新，组件会被重新渲染，但是页面不会重新加载。

举例说明

```csharp
// to为string
<Link to="/about">关于</Link>
 
// to为obj
<Link to={{
  pathname: '/courses',
  search: '?sort=name',
  hash: '#the-hash',
  state: { fromDashboard: true }
}}/>
 
// replace 
<Link to="/courses" replace />
```

&lt;Link&gt;使用to参数来描述需要定位的页面。它的值既可是字符串，也可以是location对象（包含pathname、search、hash、与state属性）如果其值为字符串，将会被转换为location对象。

replace(bool)：为 true 时，点击链接后将使用新地址替换掉访问历史记录里面的原地址；为 false 时，点击链接后将在原有访问历史记录的基础上添加一个新的纪录，默认为 false。



###### 点击Link组件后，React Router路由发生了什么?

&lt;Link&gt;组件最终会渲染为 HTML 标签 &lt;a&gt;，它的 to、query、hash 属性会被组合在一起并渲染为 href 属性。虽然 Link 被渲染为超链接，但在内部实现上使用脚本拦截了浏览器的默认行为，然后调用了history.pushState 方法（注意，文中出现的 history 指的是通过 history 包里面的 create*History 方法创建的对象，window.history 则指定浏览器原生的 history 对象，由于有些 API 相同，不要弄混）。history 包中底层的 pushState 方法支持传入两个参数 state 和 path，在函数体内有将这两个参数传输到 createLocation 方法中，返回 location 的结构如下：



```cpp
location = {
  pathname, // 当前路径，即 Link 中的 to 属性
  search, // search
  hash, // hash
  state, // state 对象
  action, // location 类型，在点击 Link 时为 PUSH，浏览器前进后退时为 POP，调用 replaceState 方法时为 REPLACE
  key, // 用于操作 sessionStorage 存取 state 对象
}
```

系统会将上述 location 对象作为参数传入到 TransitionTo 方法中，然后调用 window.location.hash 或者window.history.pushState() 修改了应用的 url，这取决于你创建 history 对象的方式，同时会触发history.listen中注册的事件监听器。

###### NavLink

&lt;NavLink&gt;是&lt;Link&gt;的一个特定版本，会在匹配上当前的url的时候给已经渲染的元素添加参数，组件的属性有：

- activeClassName(string)：设置选中样式，默认值为active
- activeStyle(object)：当元素被选中时，为此元素添加样式
- exact(bool)：为true时，只有当导致和完全匹配class和style才会应用
- strict(bool)：为true时，在确定为位置是否与当前URL匹配时，将考虑位置pathname后的斜线
- isActive(func)判断链接是否激活的额外逻辑的功能

举例说明

```kotlin
// activeClassName选中时样式为selected
<NavLink
  to="/faq"
  activeClassName="selected"
>FAQs</NavLink>
 
// 选中时样式为activeStyle的样式设置
<NavLink
  to="/faq"
  activeStyle={{
    fontWeight: 'bold',
    color: 'red'
   }}
>FAQs</NavLink>
 
// 当event id为奇数的时候，激活链接
const oddEvent = (match, location) => {
  if (!match) {
    return false
  }
  const eventID = parseInt(match.params.eventID)
  return !isNaN(eventID) && eventID % 2 === 1
}
 
<NavLink
  to="/events/123"
  isActive={oddEvent}
>Event 123</NavLink>
```



























