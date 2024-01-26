
### JSX

在了解React运行机制之前,先了解一下前置的、简单的基础知识:JSX.

**什么是JSX**

jsx是js语法的一种扩展.jsx在表面上看起来像html,但其本质上还是js,只是通过babel转换为js去执行.也有网友说,jsx就是js,只是写成了html的样子而已.我也这么认识jsx.当我们的代码在读取这段jsx的时候,jsx会被转换成为vnode返回给我们,供我们的代码调用.这里面做事情是通过react-script中内置的babel帮我们自动完成的,我们在调用的时候无需关心内部的转换过程.

如我们刚开始学习一门新的语言时都会从hello world开始的demo:

```jsx
return (
    <div>Hello world</div>
)

// 实际上React中是这么处理的:
return React.createElement(
    "div",
    null,
    "Hello world"
)
```

**实现一个简易版的react**

