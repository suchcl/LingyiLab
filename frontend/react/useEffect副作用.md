### useEffect副作用介绍

useEffect可以让函数组件也可以进行副作用操作。那么什么是副作用呢？

函数的副作用就是函数除了返回值外对外界环境造成的其他影响。例如我们在执行一个函数的时候，该函数都会影响到一个全局的变量，那么这个对全局变量的影响就是这个函数的副作用。我们期望的是函数可以处理一些逻辑，我传递给函数一些参数，函数给我返回一些数据，把影响范围控制在函数内部就行。但是实际情况是函数的执行影响到了全局的变量,所以这个函数就产生了除了本身以外返回值外的函数外界的值的作用，就是副作用了。

**在React中的副作用大体上可以分为两类：**

1. 一类是调用浏览器的API

这一类如使用addEventListender来添加事件的监听函数、使用clientWidth等浏览器API获取DOM元素的尺寸等；

2. 一类是发起的获取服务器数据的异步网络请求

这一类的副作用，如组件挂载后去异步获取数据。

**函数式组件中的useEffect和类组件中的生命周期的关系？**

useEffect，是一个钩子函数，有一些地方对这个钩子函数的称呼上，称其为side-effect。如果我们了解过类组件，那么useEffect，大致上相当于componentDidMount、componentDidUpdate、componentWillUnmount这3个周期的组合。

componentDidMount: 组件挂载

componentDidUpdate: 组件更新

componentWillUnmount: 组件即将卸载