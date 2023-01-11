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

#### 2.2 NavLink组件

