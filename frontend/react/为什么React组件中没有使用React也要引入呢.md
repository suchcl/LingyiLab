### 为什么React组件中没有用到React也要导入呢?

在回答这个问题之前,先做一点关于React编译原理的铺垫,有了这个铺垫之后,再回过头来看这个问题就比较简单了.

在React的编译史上,曾有两代编译器,第一代是React自己团队开发的,叫做JSXTransformer.js.到了2015年的时候,React团队放弃了自研的JSXTransformer.js编译器,改用了babel,之后就一直在使用babel作为React的编译器.

babel有两种React Runtime,或者可以简单的理解为支持两种编译模式,分别为classic和automatic.

**classic模式**

classic模式本质上是使用React.createElement来进行代码编译成js代码.

```jsx
// 源代码
function App(){
	return (
    	<div>Hello World!</div>
    )
}
```

```js
// 转译之后的代码
function App() {
  return /*#__PURE__*/React.createElement("div", null, "Hello World!");
}
```

我们可以看到源文件是通过React.createElement()方法做了处理.

**automatic模式**

automatic模式,使用react/jsx-runtime做翻译工作.

```jsx
// 源代码
function App(){
	return (
    	<div>Hello World!</div>
    )
}
```

```js
// automatic模式转译后的目标代码
import { jsx as _jsx } from "react/jsx-runtime";
function App() {
  return /*#__PURE__*/_jsx("div", {
    children: "Hello World!"
  });
}
```

可以看到automatic模式,是通过react/jsx-runtime来进行的代码翻译工作,它没有显示的依赖React.

**为什么React组件中不需要React也要引入React呢?**

```jsx
import Reract from "react";
```

以前在做React项目开发的时候,即便组件内没有显示的使用到React,也要导入React呢?

根据上面我们对React编译模式的了解,就是原来React低版本的时候使用的是babel编译器的classic编译模式,该模式下对源代码的翻译需要依赖React的createElement方法,所以即便组件中没有显示的使用到React,也要导入进来,否则编译器会找不到React.

到了React的新版本(React17)的时候,React开始使用babel的automatic编译模式了,该模式下翻译源代码不依赖React,所以到了React17以后,就不再需要导入React了,如果组件内没有显示的调用React.