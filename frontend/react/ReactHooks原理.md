### ReactHooks原理

参考链接:[https://www.netlify.com/blog/2019/03/11/deep-dive-how-do-react-hooks-really-work/](https://www.netlify.com/blog/2019/03/11/deep-dive-how-do-react-hooks-really-work/)、[https://juejin.cn/post/6844904128326434823](https://juejin.cn/post/6844904128326434823)


作为一种改变组件状态、处理组件副作用的方式,Hooks这个概念最早由React提出,而后被其他框架如vue、Svelte甚至原生js库所应用.对闭包的很好的了解,可以对使用hooks有很大的帮助.

#### 问题

1. 闭包怎么在Hooks内使用;

2. 怎么实现一个迷你的React Hooks

#### 闭包是什么?

Hooks的优势:可以避免复杂的class组件的和高阶组件,不用担心class组件的this指向问题

弊端:需要留心闭包的使用;

闭包是js中的一个基础的概念,但是很多开发者还是对这个概念似懂非懂,懵懵懂懂.Kyle Simpson在他的《你不知道的javascript》一书中这么定义闭包:

> 当代码已经执行到一个函数的词法作用域之外,但是这个函数仍然可以记住并访问它的词法作用域,那么就形成了闭包.

这个解释还是有点绕,生涩难懂.具体关于闭包解释,可以参考:[闭包](../javascript/闭包.md)

