<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. React渲染机制的理解](#1-react%E6%B8%B2%E6%9F%93%E6%9C%BA%E5%88%B6%E7%9A%84%E7%90%86%E8%A7%A3)
- [2. 虚拟化技术](#2-%E8%99%9A%E6%8B%9F%E5%8C%96%E6%8A%80%E6%9C%AF)
- [3. 懒加载与按需加载，减少初始时间](#3-%E6%87%92%E5%8A%A0%E8%BD%BD%E4%B8%8E%E6%8C%89%E9%9C%80%E5%8A%A0%E8%BD%BD%E5%87%8F%E5%B0%91%E5%88%9D%E5%A7%8B%E6%97%B6%E9%97%B4)
- [4. 减少重新渲染的其他技巧](#4-%E5%87%8F%E5%B0%91%E9%87%8D%E6%96%B0%E6%B8%B2%E6%9F%93%E7%9A%84%E5%85%B6%E4%BB%96%E6%8A%80%E5%B7%A7)
- [5. 构建优化：减小打包体积和提高构建速度](#5-%E6%9E%84%E5%BB%BA%E4%BC%98%E5%8C%96%E5%87%8F%E5%B0%8F%E6%89%93%E5%8C%85%E4%BD%93%E7%A7%AF%E5%92%8C%E6%8F%90%E9%AB%98%E6%9E%84%E5%BB%BA%E9%80%9F%E5%BA%A6)
- [6. 服务端渲染(SSR)和静态站点生成(SSG)](#6-%E6%9C%8D%E5%8A%A1%E7%AB%AF%E6%B8%B2%E6%9F%93ssr%E5%92%8C%E9%9D%99%E6%80%81%E7%AB%99%E7%82%B9%E7%94%9F%E6%88%90ssg)
- [7. 图片优化](#7-%E5%9B%BE%E7%89%87%E4%BC%98%E5%8C%96)
- [8. 总结](#8-%E6%80%BB%E7%BB%93)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 1. React渲染机制的理解

首先需要了解一下React的渲染机制。React使用虚拟DOM来提升UI的渲染效率，每当组件的props或者state更新的时候React就会重新渲染组件。并以此对比虚拟DOM的差异，实现真实DOM的更新。

React自身的渲染机制并不是一直都是最优的，会在一些不必要重新渲染的时候进行了重新渲染，所以有的时候需要开发人员加以控制，以达到最优的渲染效果。

为了达到最优的优化效果，需要了解React渲染过程中的几个概念：React.memo、PureComponent、useMemo、useCallback等。

- React.memo：函数式组件，React.memo可以避免不必要的重新渲染。当组件的props没有变化时，React会跳过该组件的重新渲染过程。

- PureComponent：类组件，内部通过shouldComponentUpdate来判断是否需要更新重新渲染

- userMemo和useCallback:这2个hooks用于函数式组件中缓存计算结果和函数，避免在每次创建函数时重新计算和重新创建函数

### 2. 虚拟化技术

在数据量较大的页面，渲染大量数据会影响页面的性能，虚拟化可以解决、优化这个问题。

所谓的虚拟化，就是只渲染当前屏幕视口内的元素，而不是一次性渲染所有的数据。这种方法可以减少不必要的DOM渲染，显著提升页面的渲染性能。

react-window、react-virtualized是React常用的虚拟化库。

### 3. 懒加载与按需加载，减少初始时间

应用随着开发的迭代，可能会越来越庞大。庞大的项目带来了代码量的积累，代码组织不好就可能会带来性能的问题。这种情况下，按需加载和懒加载的技术可以缓渲染时间的耗时。

1. 按需加载组件

```tsx
import React, { Suspense, memo } from "react";

const LazyComponent = React.lazy(() => import("./components/userInfo"));

const User = () => {
    return (
        <>
            <Suspense>
                <LazyComponent />
            </Suspense>
        </>
    )
}

export default memo(User);
```

上述案例中，LazyComponent组件并不会一开始就加载，而是在需要时才被加载，从而减少了初次加载的包体积。

2. 按需加载路由

```tsx
import React, { Suspense } from 'react';
import Layout from './layouts/layout';
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
const Home = React.lazy(() => import('./pages/home'));
const List = React.lazy(() => import('./pages/list'));
const Detail = React.lazy(() => import("./pages/detail"));
const About = React.lazy(() => import("./pages/about"));

function App() {
  return (
    <Router>
      <Routes>
        <Route path='/' element={<Layout />}>
          <Route path="/" element={<Home />} />
          <Route path="/list" element={<List />} />
          <Route path="/detail" element={<Detail />} />
          <Route path="/about" element={<About />} />
        </Route>
      </Routes>
    </Router>
  )
}

export default App
```

通过这种方式，相关的页面路由只有在路由能匹配时才会加载，也减少了项目的初次加载时间。

### 4. 减少重新渲染的其他技巧

### 5. 构建优化：减小打包体积和提高构建速度

### 6. 服务端渲染(SSR)和静态站点生成(SSG)

### 7. 图片优化

### 8. 总结

通过以上技术和优化方案，我们可以显著提升React的开发体验和性能表现。

1. 虚拟DOM和渲染优化：使用React.memo、PureComponent、useMemo、useCallback等方法，减少不必要的渲染；

2. 虚拟化技术：使用react-window、react-virtualized等库，优化长列表渲染；

3. 懒加载与按需加载：使用React.lazy和Suspense，减少初次加载时间；

4. 构建优化：通过webpack优化打包，启用tree shaking和代码分割，减小代码体积；

5. 服务端渲染和静态站点生成：利用Nex.tjs实现服务端渲染和静态站点生成，提高加载速度；

6. 图片优化：采用懒加载和优化图片大小和格式，提升页面的加载性能；