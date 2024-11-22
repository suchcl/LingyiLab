### ReactHooks原理

参考链接:[https://www.netlify.com/blog/2019/03/11/deep-dive-how-do-react-hooks-really-work/](https://www.netlify.com/blog/2019/03/11/deep-dive-how-do-react-hooks-really-work/)、[https://juejin.cn/post/6844904128326434823](https://juejin.cn/post/6844904128326434823)


作为一种改变组件状态、处理组件副作用的方式,Hooks这个概念最早由React提出,而后被其他框架如vue、Svelte甚至原生js库所应用.对闭包的很好的了解,可以对使用hooks有很大的帮助.

#### 问题

1. 闭包怎么在Hooks内使用;

2. 怎么实现一个迷你的React Hooks

#### 闭包是什么?

Hooks的优势:可以避免复杂的class组件的和高阶组件,不用担心class组件的this指向问题

弊端:需要留心闭包的使用;