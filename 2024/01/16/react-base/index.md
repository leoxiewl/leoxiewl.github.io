# React 基础


## React 基础

React由Meta公司开发，是一个用于 构建Web和原生交互界面的库

> The library for web and native user interfaces

## React 优势

**虚拟DOM（Virtual DOM）**

使用虚拟DOM，通过比较前后两个状态的差异，最小化DOM操作，提高性能。

**组件化**

强调组件化开发，将用户界面划分为独立的、可复用的组件。

**生态系统**

拥有庞大的生态系统，许多公司和项目使用 React，有丰富的社区支持。

**社区支持**

拥有庞大的社区，得到了来自Facebook等大公司的支持。

**适用场景**

更适用于大型应用和需要高度定制化的项目。

## React 开发环境搭建

### create-react-app

```bash
npx create-react-app react-project-name

// 启动项目
npm start
```

### Next.js

Next.js 是生产级的 React 框架

https://zh-hans.react.dev/learn/start-a-new-react-project



## 组件: 组合页面

React 应用程序是由 **组件** 组成的。一个组件是 UI（用户界面）的一部分，它拥有自己的逻辑和外观。组件可以小到一个按钮，也可以大到整个页面。经过组合，形成一整个页面。

![](https://pic.imgdb.cn/item/65a7c0df871b83018acd2a95.jpg)

![image-20240117194613170](react-base.assets/image-20240117194613170.png)

**React 组件是一个 JavaScript 函数**

```js
function MyButton() {
  return (
    <button>I'm a button</button>
  );
}
```

上述是 MyButton 组件的声明

现在把它嵌套到另一个组件中

```js
export default function MyApp() {
  return (
    <div>
      <h1>Welcome to my app</h1>
      <MyButton />
    </div>
  );
}
```

`export default` 关键字指定了文件中的主要组件。

**React 组件必须以大写字母开头，而 HTML 标签则必须是小写字母**。



## JSX: 构建 UI

JSX 是 React 中用来构建 UI 的方式。

> JSX并不是标准的JS语法，它是 JS的语法扩展，浏览器本身不能识别，需要通过解析工具做解析之后才能在浏览器中使用

### JSX 语法限制

- 必须闭合标签，如 `<br />`
- 组件不能返回多个 JSX 标签，必须将它们包裹到一个共享的父级中，比如 `<div>...</div>` 或使用空的 `<>...</>` 包裹

```js
function AboutPage() {
  return (
    <>
      <h1>About</h1>
      <p>Hello there.<br />How do you do?</p>
    </>
  );
}
```



### JSX 渲染数据

- 在JSX中可以通过 `大括号语法{}` 识别JavaScript中的表达式，比如常见的变量、函数调用、方法调用等等

注意：if语句、switch语句、变量声明不属于表达式，不能出现在{}中

```js

const message = 'this is message'

function getAge(){
    return 18
}

function App(){
    return (
        <div>
            <h1>this is title</h1>
            
            {/* 字符串识别 */}
            {'this is str'}
            
            {/* 变量识别 */}
            {message}
            
            {/* 函数调用 渲染为函数的返回值 */}
            {getAge()}
        </div>
    )
}
export default App;

```

### map 方法实现列表渲染

```js
const list = [
    {id:1001, name:'Vue'},
    {id:1002, name: 'React'},
    {id:1003, name: 'Angular'}
]

function App(){
    return (
        <div>
            <ul>
                {list.map(item => <li key={item.id}>{item.name}</li>)}
            </ul>
        </div>
    )
}

export default App;

```

对于列表中的每一个元素，你都应该传递一个字符串或者数字给 `key`，用于在其**兄弟节点中唯一标识该元素**。

通常 key 来自你的数据，比如数据库中的 ID。如果你在后续插入、删除或重新排序这些项目，React 将依靠你提供的 key 来思考发生了什么。

### 逻辑符号实现条件渲染

**逻辑与运算符 `&&`**

```js
const flag = false
function App(){
    return (
        <div>
            {flag && <span>测试条件渲染</span>}
        </div>
    )
}

export default App;
```

**三元表达式 (?:)**

```js
const flag = false
function App(){
    return (
        <div>
            {flag ? <span>flag</span> : <span>测试</span>}
        </div>
    )
}

export default App;

```

### 复杂条件渲染

解决方案：自定义函数 + 判断语句

```js
const type = 1  // 0|1|3

function getArticleJSX(){
  if(type === 0){
    return <div>无图模式模版</div>
  }else if(type === 1){
    return <div>单图模式模版</div>
  }else(type === 3){
    return <div>三图模式模版</div>
  }
}

function App(){
  return (
    <>
      { getArticleJSX() }
    </>
  )
}
```

## 组件样式 CSS

在 React 中，可以使用 `className` 来指定一个 CSS 的 class。与 HTML 的 [`class`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Global_attributes/class) 属性的工作方式相同：

```js
<img className="avatar" />
```

可以在一个单独的 CSS 文件中为它编写 CSS 规则

```css
/* In your CSS */
.avatar {
  border-radius: 50%;
}
```

> React 并没有规定你如何添加 CSS 文件，言外之意，如何添加由你自己决定

**行内样式**

```html
<div style={{ color:'red'}}>this is div</div>
```

**变量抽取出来定义**

```js
const style = {
    color: 'red',
    fontSize: '100px'
}
function App() {
  return (
    <div>
        <span style={style}>Hello</span>!
    </div>
  );
}

export default App;
```

## 组件属性传参 props

**props可以传递任意的合法数据**，比如数字、字符串、布尔值、数组、对象、函数、JSX

```js
const user = {
  name: 'Hedy Lamarr',
  imageUrl: 'https://i.imgur.com/yXOvdOSs.jpg',
  imageSize: 90,
};

export default function Profile() {
  return (
    <>
      <h1>{user.name}</h1>
      <img
        className="avatar"
        src={user.imageUrl}
        alt={'Photo of ' + user.name}
        style={{
          width: user.imageSize,
          height: user.imageSize
        }}
      />
    </>
  );
}
```







## React 事件绑定

**React中的事件绑定，通过语法 `on + 事件名称 = { 事件处理程序 }`，整体上遵循驼峰命名法**

```js
function App(){
  const clickHandler = ()=>{
    console.log('button按钮点击了')
  }
  return (
    <button onClick={clickHandler}>click me</button>
  )
}
```

> 注意，`onClick={handleClick}` 的结尾没有小括号！不要 **调用** 事件处理函数：你只需 **把函数传递给事件** 即可。当用户点击按钮时 React 会调用你传递的事件处理函数。

### 事件参数

```js
function App(){
  const clickHandler = (e)=>{
    console.log('button按钮点击了', e)
  }
  return (
    <button onClick={clickHandler}>click me</button>
  )
}
```

### 传递自定义参数

```js
function App(){
  const clickHandler = (name)=>{
    console.log('button按钮点击了', name)
  }
  return (
    <button onClick={()=>clickHandler('jack')}>click me</button>
  )
}
```

### 同时传递事件对象和自定义参数

在事件绑定的位置传递事件实参e和自定义参数，clickHandler中声明形参，注意顺序对应

```js
function App(){
  const clickHandler = (name,e)=>{
    console.log('button按钮点击了', name,e)
  }
  return (
    <button onClick={(e)=>clickHandler('jack',e)}>click me</button>
  )
}
```

## 更新界面(状态管理)-useState

useState 是一个 React Hook（函数），它允许我们向组件添加一个`状态变量`, 从而控制影响组件的渲染结果
和普通JS变量不同的是，状态变量一旦发生变化组件的视图UI也会跟着变化（数据驱动视图）

**其中的数据改变，渲染出的视图 UI 就会跟着发生变化**

### 基础使用

```js
function App(){
  const [ count, setCount ] = React.useState(0)
  return (
    <div>
      <button onClick={()=>setCount(count+1)}>{ count }</button>
    </div>
  )
}
```

⚠**注意**

- **useState 参数可以用来初始化，传什么样的类型，操作的就是什么样的类型**

- **状态修改只能用 `set...`方法**

### 修改对象状态

对于对象类型的状态变量，应该始终给set方法一个`全新的对象` 来进行修改

```js
import {useState} from "react";

function App(){
    const [Object, setObject] = useState({name:'leo'})
    const handleChangeName = () => {
        setObject({
            ...Object,
            name:'jack'
        })
    }
    return (
        <div>
            {Object.name}
            <button onClick={handleChangeName}>button</button>
        </div>
    )
}

export default App;

```

## Hook 函数

以 `use` 开头的函数被称为 **Hook**。`useState` 是 React 提供的一个内置 Hook

Hook 函数只能在你的组件（或其他 Hook）的 **顶层** 调用 Hook。如果你想在一个条件或循环中使用 `useState`，请提取一个新的组件并在组件内部使用它。

更多 Hook 函数 [React API 参考](https://zh-hans.react.dev/reference/react) 

### 自定义 Hook 函数

```js
// 封装自定义Hook

// 问题: 布尔切换的逻辑 当前组件耦合在一起的 不方便复用

// 解决思路: 自定义hook

import { useState } from "react"

function useToggle () {
  // 可复用的逻辑代码
  const [value, setValue] = useState(true)

  const toggle = () => setValue(!value)

  // 哪些状态和回调函数需要在其他组件中使用 return
  return {
    value,
    toggle
  }
}

// 封装自定义hook通用思路

// 1. 声明一个以use打头的函数
// 2. 在函数体内封装可复用的逻辑（只要是可复用的逻辑）
// 3. 把组件中用到的状态或者回调return出去（以对象或者数组）
// 4. 在哪个组件中要用到这个逻辑，就执行这个函数，解构出来状态和回调进行使用


function App () {
  const { value, toggle } = useToggle()
  return (
    <div>
      {value && <div>this is div</div>}
      <button onClick={toggle}>toggle</button>
    </div>
  )
}

export default App
```

### React Hooks使用规则

1. 只能在组件中或者其他自定义Hook函数中调用
2. 只能在组件的顶层调用，不能嵌套在if、for、其它的函数中





## 组件间共享数据

控制两个 Button 同时发生改变

```js
import { useState } from 'react';

export default function MyApp() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return (
    <div>
      <h1>Counters that update together</h1>
      <MyButton count={count} onClick={handleClick} />
      <MyButton count={count} onClick={handleClick} />
    </div>
  );
}

function MyButton({ count, onClick }) {
  return (
    <button onClick={onClick}>
      Clicked {count} times
    </button>
  );
}

```

## React副作用管理-useEffect

useEffect是一个React Hook函数，用于在React组件中创建不是由事件引起而是由渲染本身引起的操作（副作用）, 比**如发送AJAX请求，更改DOM**等等 

**组件渲染完毕之后就需要和服务器要数据，整个过程属于“只由渲染引起的操作”**

### 基础使用

需求：在组件渲染完毕之后，立刻从服务端获取平道列表数据并显示到页面中

```js
useEffect(() => {}, [])
```

1. 参数1是一个函数，可以把它叫做副作用函数，在函数内部可以放置要执行的操作 
2. 参数2是一个数组（可选参），在数组里放置依赖项，不同依赖项会影响第一个参数函数的执行，当是一个空数组的时候，副作用函数只会在组件渲染完毕之后执行一次 



| **依赖项**     | **副作用功函数的执行时机**      |
| -------------- | ------------------------------- |
| 没有依赖项     | 组件初始渲染 + 组件更新时执行   |
| 空数组依赖     | 只在初始渲染时执行一次          |
| 添加特定依赖项 | 组件初始渲染 + 依赖项变化时执行 |

### 清除副作用

概念：在useEffect中编写的由渲染本身引起的对接组件外部的操作，社区也经常把它叫做副作用操作

比如在useEffect中开启了一个定时器，我们想在组件卸载时把这个定时器再清理掉，这个过程就是清理副作用

![image-20240117210617500](react-base.assets/image-20240117210617500.png)

清除副作用的函数最常见的执行时机是在组件卸载时自动执行

```js
import { useEffect, useState } from "react"

function Son () {
  // 1. 渲染时开启一个定时器
  useEffect(() => {
    const timer = setInterval(() => {
      console.log('定时器执行中...')
    }, 1000)

    return () => {
      // 清除副作用(组件卸载时)
      clearInterval(timer)
    }
  }, [])
  return <div>this is son</div>
}

function App () {
  // 通过条件渲染模拟组件卸载
  const [show, setShow] = useState(true)
  return (
    <div>
      {show && <Son />}
      <button onClick={() => setShow(false)}>卸载Son组件</button>
    </div>
  )
}

export default App
```

## ReactRouter

一个路径 path 对应一个组件 component 。

当我们在浏览器中访问一个 path 的时候，path 对应的组件会在页面中进行渲染



### 路由引入

```bash
# 安装最新的ReactRouter包
npm i react-router-dom
```



### 基本使用

```js
import React from 'react'
import ReactDOM from 'react-dom/client'

const router = createBrowserRouter([
  {
    path:'/login',
    element: <div>登录</div>
  },
  {
    path:'/article',
    element: <div>文章</div>
  }
])

ReactDOM.createRoot(document.getElementById('root')).render(
  <RouterProvider router={router}/>
)
```



### 路由抽取

**router.js**

```js
import {createBrowserRouter} from "react-router-dom";
import Login from "../page/Login";
import Article from "../page/Article";

const router = createBrowserRouter([
    {
        path:'/login',
        element: <Login/>
    },
    {
        path:'/article',
        element: <Article/>
    }
])

export default router
```



**index.js**

```js
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import reportWebVitals from './reportWebVitals';
import router from "./router";
import {RouterProvider} from "react-router-dom";


ReactDOM.createRoot(document.getElementById('root')).render(
    <RouterProvider router={router}/>
)

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();

```



**页面(也可以用 jsx)**

```js
const Article = () => {
    return <div>我是文章页</div>
}

export default Article
```



### 路由导航

路由系统中的多个路由之间需要进行**路由跳转**，并且在跳转的同时有可能需要**传递参数进行通信**

#### 声明式导航

声明式导航是指通过在模版中通过 `<Link/> ` 组件描述出要跳转到哪里去，比如后台管理系统的左侧菜单通常使用这种方式进行

```js
<Link to={"/article"}>文章页</Link>
```

语法说明：通过给组件的to属性指定要跳转到路由path，组件会被渲染为浏览器支持的a链接，如果需要传参直接通过字符串拼接的方式拼接参数即可

#### 编程式导航

编程式导航是指通过 `useNavigate` 钩子得到导航方法，然后通过调用方法以命令式的形式进行路由跳转，比如想在登录请求完毕之后跳转就可以选择这种方式，更加灵活

**只需要调用 navigate 方法就能跳转**

语法说明：通过调用navigate方法传入地址path实现跳转

```js
import {Link, useNavigate} from "react-router-dom";

const Login = () => {
    const navicate = useNavigate()
    return (
        <div>
            我是登录页
            <Link to={"/article"}>文章页</Link>

        {/*  命令式*/}
            <button onClick={()=>navicate('/article')}>跳转到文章页</button>
        </div>
    )
}

export default Login
```

### 导航传参

**searchParam 传参**

1. 导航跳转-路由拼接传参

```js
import {Link, useNavigate} from "react-router-dom";

const Login = () => {
    const navicate = useNavigate()
    return (
        <div>
            我是登录页
            <Link to={"/article"}>文章页</Link>

            {/* 命令式 */}
            <button onClick={() => navicate('/article')}>跳转到文章页</button>

            {/* 导航 search 传参 */}
            <button onClick={() => navicate('/article?id=1001&name=jack')}>导航 search 传参</button>
        </div>
    )
}

export default Login
```

2. 接收参数-useSearchParams

```js
import {useSearchParams} from "react-router-dom";

const Article = () => {
    const [params] = useSearchParams()
    const name = params.get('name')
    return <div>我是文章页 获取到的参数-{name}</div>
}

export default Article
```



**params 传参**

步骤

1. 路径添加参数
2. 路由占位符
3. 获取参数-useParams

> 可以加多个，只需要添加占位符即可



1. 路径添加参数

```js
import {Link, useNavigate} from "react-router-dom";

const Login = () => {
    const navicate = useNavigate()
    return (
        <div>
            {/* 导航 params 传参 */}
            <button onClick={() => navicate('/article/jack')}>导航 params 传参</button>
        </div>
    )
}

export default Login
```

2. 路由占位符

```js
import {createBrowserRouter} from "react-router-dom";
import Login from "../page/Login";
import Article from "../page/Article";

const router = createBrowserRouter([
    {
        path:'/login',
        element: <Login/>
    },
    {
        path:'/article/:name',
        element: <Article/>
    }
])

export default router
```

3. 获取参数

```js
import {useParams, useSearchParams} from "react-router-dom";

const Article = () => {
    const params1= useParams()
    let nameParams = params1.name

    return <div>---- params 传参 {nameParams} </div>
}

export default Article
```

### 嵌套路由

在一级路由中又内嵌了其他路由，这种关系就叫做嵌套路由

#### 嵌套路由配置

实现步骤

    1. 使用 `children`属性配置路由嵌套关系  
    2. 使用 `<Outlet/>` 组件配置二级路由渲染位置



1. 嵌套路由配置

```js
{
        path: '/',
        element: <Layout/>,
        children: [
            {
                path: 'board',
                element: <Board/>
            },
            {
                path: 'about',
                element: <About/>
            }
        ]
    }
```

2. 使用 `<Outlet/>` 组件配置二级路由渲染位置

Layout

```js
import {Link, Outlet} from "react-router-dom";

const Layout = () => {
    return (
        <div>
            我是一级路由组件 Layout
            {/* 用来跳转的按钮*/}
            <Link to={'/board'}>面板</Link>
            <Link to={'/about'}>关于</Link>

            {/* 配置二级路由出口，页面就在这个地方渲染 */}
            <Outlet/>
        </div>
    )

}

export default Layout
```

#### 默认二级路由配置

当访问的是一级路由时，默认的二级路由组件可以得到渲染，只需要在二级路由的位置去掉path，设置index属性为true

```js
 {
        path: '/',
        element: <Layout/>,
        children: [
            {
                index: true,
                element: <Board/>
            },
            {
                path: 'about',
                element: <About/>
            }
        ]
    }
```

### 404 路由配置

场景：当浏览器输入url的路径在整个路由配置中都找不到对应的 path，为了用户体验，可以使用 404 兜底组件进行渲染

实现步骤：

1. 准备一个NotFound组件
2. 在路由表数组的末尾，以*号作为路由path配置路由

```js
 {
        path:'*',
        element: <NotFound/>
    }
```

### 两种路由模式

各个主流框架的路由常用的路由模式有俩种，history模式和hash模式, ReactRouter分别由 createBrowerRouter 和 createHashRouter 函数负责创建

| 路由模式 | url表现     | 底层原理                    | 是否需要后端支持 |
| -------- | ----------- | --------------------------- | ---------------- |
| history  | url/login   | history对象 + pushState事件 | 需要             |
| hash     | url/#/login | 监听hashChange事件          | 不需要           |











## 参考

[React 官方文档](https://react.dev/learn)

[React 官方中文文档](https://zh-hans.react.dev/learn)

[黑马前端 React 18 文档](https://www.bilibili.com/video/BV1ZB4y1Z7o8)


