### Promise和async/await的区别

#### Promise和async中的立即执行

我们应该知道，Promise中的异步，是体现在then和catch中，所以在Promise对象被实例化中的代码都是被当做同步任务被立即执行的。而在async/await中，在出现await之前的代码也是被同步、立即执行的。那么出现了await之后呢？

简单的理解，await就是等待，就是在等待await后面的代码执行完成，然后再进行下一步。但是实际上并不是这样，<font color="#f20">实际上await是一个让出线程的标志</font>。

await后面的表达式会先执行一遍，将await后面的代码加入到微任务中，然后跳出整个async函数来执行后面的代码。

因为async/await本身是promise+generator的语法糖，所以await后面的代码是微任务。

简单理解：

```javascript
async function async1() {
  console.log("async1 start");
  await async2();
  console.log("async1 end");
}
```

这几行代码，可以拆解为下面的代码，其是等价的：

```javascript
async function async1() {
  console.log("async1 start");
  Promise.resolve(async2()).then(function () {
    console.log("async1 end");
  });
}
```

**await的使用**

1. await必须使用在异步函数中，即声明位async的函数中

2. await不许出现在箭头函数中；

3. await不许出现在同步函数中；

4. await不许出现在同步函数表达式中；

如果出现了以上几种情况，就会抛出：SyntaxError

#### promise、async/await的区别

**promise**

Promise本身是同步的立即执行函数，只有在响应执行resolve或者reject的时候才是异步操作，才会执行then\catch，当主线程执行栈中任务都完成后，才会去执行resolve、reject的响应函数。

直接一点，就是Promise中，实例化对象的代码是同步的，then和catch是异步的，且是微任务。

**async/await**

async函数返回一个promise对象，当async函数执行的时候，一遇到await让出主线程，后面的代码加入到微任务队列；

async函数，在遇到await之前的代码，也是同步的；

async函数，遇到await后，让出主线程，跳出async函数体；

await只能在async函数中使用；

**牵强一点的说法**

async/await是建立在promise之上的

async/await写法更优雅；

async/await和promise一样，不阻塞

async/await看起来像同步代码，但本质上是异步；


#### promise和async/await的异常捕获方式

