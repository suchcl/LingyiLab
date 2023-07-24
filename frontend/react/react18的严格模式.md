### React18默认采用了严格模式

React18默认开启了严格模式，且在react18正式版本发布了后，官方没有提供正式的接口来关闭严格模式。

在18正式版发布之前，可以通过unstable_disableDevMode接口来关闭严格模式，但是18正式发布后，就关闭了该接口。

在18的正式版本前，可以通过如下方式关闭严格模式：

```tsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.tsx'
import './index.css'
// 导入unstable_disableDevMode函数
import { unstable_disableDevMode } from "react";

// 禁用严格模式
unstable_disableDevMode();

ReactDOM.createRoot(document.getElementById('root')!).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
)
```

> 在18正式版后就规规矩矩的使用严格模式吧。

### 使用了严格模式后有什么影响呢？

在严格模式下，在开发环境/阶段会执行一些额外的检查，并在发现问题时发出警告信息，这些检查主要包括：

- 禁止使用已经废弃的生命周期方法

- 检查组件的回调函数是否已经正确的绑定了this

- 检查组件是否正确的使用了状态和属性

通过启用严格模式，可以帮助开发人员在开发过程中尽早的发现和解决问题，从而提高应用程序的质量并减少后期维护的成本。

> 需要注意的是，严格模式只在开发模式下启用，在生产环境下不会执行额外的检查，这样可以确保应用程序在生产环境具有最佳的性能和效率。

开发环境，在React18点严格模式下，组件初始化的useEffect会执行两次，也就是组件初始化的useEffect里面的操作会被执行两次。在生产环境不会执行两次，还是正常的执行一次。

#### 怎么关闭严格模式

在<font color="#f20">React18正式版发布前</font>，可以通过unstable_disableDevMode函数来关闭,方式如下：

```tsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.tsx'
import './index.css'
// 导入unstable_disableDevMode函数
import { unstable_disableDevMode } from "react";

// 禁用严格模式
unstable_disableDevMode();

ReactDOM.createRoot(document.getElementById('root')!).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
)
```

但是在React18正式版发布之后，官方就不再提供正式的接口来关闭严格模式了。

### 在React18严格模式下的一些实践推荐

1. 避免使用已经过期的生命周期方法

2. 推荐使用函数式组件和hooks

3. 使用typescript或者proptypes进行类型检查

4. 使用React DevTools进行调试

5. 升级依赖项