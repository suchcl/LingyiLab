<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. 简单了解react-router](#1-%E7%AE%80%E5%8D%95%E4%BA%86%E8%A7%A3react-router)
- [2. 基本使用](#2-%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8)
  - [2.1 BrowserRouter](#21-browserrouter)
  - [2.2 NavLink组件](#22-navlink%E7%BB%84%E4%BB%B6)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 1. 简单了解react-router

react项目中使用react-router，主要会使用到2个方面的内容：react-router和react-router-dom.

react-router：为React应用提供了路由的核心功能；

react-router-dom：基于react-router,加入了在浏览器环境下的一些功能

> react不光能开发基于浏览器的web项目，也可以开发小程序、app等其他形式的应用。

### 2. 基本使用

#### 2.1 BrowserRouter

想要在React应用中使用react-router，那么就需要先在React应用中导入react-router，并包裹应用的根组件。

```tsx
import React, { StrictMode } from 'react';
import ReactDOM from 'react-dom/client';
import { BrowserRouter } from 'react-router-dom';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';

const root = ReactDOM.createRoot(
  document.getElementById('root') as HTMLElement
);
root.render(
  <StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </StrictMode>
);

reportWebVitals();
```

在这个入口文件中，我们从react-router-dom中导入了BrowserRouter组件，并使用BrowserRouter组件包裹了React应用的根组件App，这样，来自react-router-dom的其他组件和hooks已经可以正常使用了。

BrowserRouter(浏览器路由)是react-router中使用最频繁的路由方式。react-router中除了BrowserRouter，还包含了以下几种路由方式：

1. HashRouter:在路径前加1个#成为一个哈希值，hash路由模式的好处是不会因为刷新页面找不到对应的路径；

2. MemoryRouter:不存储history，路由过程存储在内存中，适用于React Native这种非浏览器环境；

3. NativeRouter:配合React Native使用，多应用于移动端；

4. StaticRouter:主要用于服务端渲染；

#### 2.2 Link组件

在react应用中，可以通过<Link />组件来创建常规链接，功能和效果类似html中的a标签。

1. <Link />组件通过属性to来传递需要跳转的链接。

```tsx
        <header className={styles.header}>
            <ul className={styles.menu}>
                <li>
                    <Link to="/home">首页</Link>
                </li>
                <li>
                    <Link to="/newsList">列表</Link>
                </li>
            </ul>
        </header>
```

2. to属性可以设置和传递一些参数，如通过search关键字设置查询字符串，pathname设置跳转路由，hash传递hash值

```ts
  <Link to={{
      pathname: '/newsList',
      search: '?sort=date',
      hash: '#hash'
  }}>列表</Link>
```

跳转后参数会体现在url上，如下:

![Link的to可以传递和设置多个属性](./images/i64.png)

#### 2.3 NavLink组件

NavLink是在Link组件的基础上做了一个功能的封装，其常规功能和Link组件一致，就是在Link跳转功能的基础上，加上了active状态的能力，然后在实际应用中根据active状态可以为当前导航添加高亮样式。

在使用<NavLink />组件时，当点击当前导航时，当前导航会自动添加active这个class，如：

![NavLink自动添加active这个class](./images/i65.png)

代码如下：

```tsx
<NavLink to="/docs">帮助</NavLink>
```

1. 如果没有模块化代码，样式中设置了active这个class的样式，则会直接生效；

2. 如果使用了模块化的样式，那么需要做些处理:

```tsx
<NavLink
    to="/docs"
    className={({ isActive }) => isActive ? `${styles['link']} ${styles['nav-active']}` : `${styles['link']}`}
>帮助</NavLink>
```

也可以通过isActive来设置style:

```tsx
<NavLink
    to="/feedback"
    style={({isActive}) => isActive ? ({color: '#6BE61A', fontSize: '16px'}) : ({})}
>反馈</NavLink>
```

className中，isActive是一个内置的属性，直接解构就可以了，固定的不能改为其他变量名。

在设置style的时候，需要注意下箭头函数的使用细节，其他的，就没有什么需要注意的了，就是很常规的设置方式。

