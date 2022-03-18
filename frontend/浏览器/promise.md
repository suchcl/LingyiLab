### 1. Promise

我们应该已经简单的知道，现代浏览器产生微任务的方式主要有两种方式：

1. 使用MutationObserver监控DOM节点的变化，当通过js来修改DOM节点的时候，就会产生DOM变化的记录的微任务；

2. 另外一种方式就是使用Promise

> Promise本身并不是异步的，也不是微任务，而是当调用Promise的resolve或者reject方法的回调时，会产生微任务。

> 另外可能也会有人认为process.nextTick和Object.observe也会产生异步的微任务，这里需要说明一下：

- process.nextTick不是浏览器的标准；

- Object.observe可以用来异步地监听一个对象的修改。但是这个方法已经从标准中废除了，它已经不再是标准。当有需要监听对象的变化时，更加推荐的是使用Proxy对象。

现在的Web标准中，DOM/BOM API中新加入的API大多数都是建立在Promise基础之上的，一些新生的前端框架也是用了大量的Promise。学习、掌握好Promise对于前端技术方向来说非常重要。

### 2. Promise的使命

Promise，主要是用来解决异步编程代码风格问题的。在Promise之前，可能会出现大量的异步回调，回调中可能还会嵌套回调，层层嵌套，也就成了回调地狱。Promise主要就是用来解决回调地狱的编码风格问题的。

Promise产生的原因或者叫背景，大概有两点原因：

1. 嵌套调用：内部的任务依赖上个任务的执行结果，根据上个回调的结果执行自己的业务逻辑。当嵌套层级深了之后，代码的可读性就非常差了。

2. 嵌套任务的不确定性：执行每个任务都有两种可能的结果(成功或者失败),所以在代码中每层嵌套的每个任务的执行结果都需要做两次的结果判断，这种对每个任务都要进行一次额外的错误处理的方式，增加了代码的混乱程度。

分析出了问题，那么解决问题的就好说了，主要解决2个问题：

1. 消灭嵌套调用；

2. 合并多个任务的错误处理；

**那么Promise具体怎么解决嵌套问题呢？**

Promise主要通过2个步骤解决嵌套回调的问题。

1. Promise实现了回调函数的延时绑定

看案例：

```js
// 创建promise对象p1，在executor函数中执行promise对象内的业务逻辑
function executor(resolve, reject) {
    resolve(200);
}
let p1 = new Promise(executor);

// p1的延时绑定回调函数
function onResolve(value) {
    console.log(value);
}

p1.then(onResolve);
```

先创建一个Promise对象p1，promise对象的业务逻辑在executor函数中执行，创建好了promise对象p1之后，再使用p1.then来设置回调函数。

2. 将回调函数onResolve的返回值穿透到最外层。

```js
// 创建promise对象p1，在executor函数中执行promise对象内的业务逻辑
function executor(resolve, reject) {
    resolve(200);
}
let p1 = new Promise(executor);

// p1的延时绑定回调函数
function onResolve(value) {
    console.log(value);
}

// 将promise执行结果的返回值穿透返回到最外层
let p2 = p1.then(onResolve);
console.log(p2);
```