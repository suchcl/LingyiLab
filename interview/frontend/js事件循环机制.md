### 常见问题

1. 浏览器和node的事件循环区别是什么？

2. 什么是宏任务和微任务，为什么要有这两种任务？其执行顺序是什么？

### 常见的事件循环

**Js是单线程、非阻塞的**

**浏览器的事件循环**

1. 执行栈和事件队列

2. 宏任务和微任务

**node环境下的事件循环:和浏览器环境有所不同**

1. 事件循环模型

2. 宏任务和微任务

**经典面试题分析**

### Js单线程和非阻塞

**单线程**

Js的一个非常主要的任务是与用户互动、操作DOM。如果Js是多线程，那么会出现很多复杂的问题要处理，比如有多个线程同时操作了DOM，那么以哪个线程为准呢？为了避免这种问题的出现，Js设计成了单线程。H5提出的web worker标准，虽然实现了多线程，但是也有很多的限制，web worker也只是主线程的子线程，受主线程的控制。

**非阻塞**

通过event loop实现，具体可参考[js非阻塞](./js非阻塞.md)。

### 浏览器的事件循环

**执行栈和事件队列**

浏览器中的事件循环，我们可以看一张图：

![浏览器事件循环](../../public/images/i108.png)

执行栈：同步代码的执行，按照执行顺序依次添加到执行栈中

**事件队列**

当一个脚本第一次执行的时候，js引擎会分析这段代码，并将其中的同步代码按照执行顺序加入执行栈中，然后从头开始执行。如果当前执行的是一个方法，那么js就会向执行栈中添加这个方法的执行环境，然后再进入到这个执行环境中去执行其中的代码。如果这个方法中又调用了其他的方法，那么js引起会继续进入这个方法继续执行。直到执行环境中的代码都执行完成了返回结果后，js引擎才会退出这个执行环境并销毁，回到上一个方法的执行环境。这样的过程反复循环，直到执行栈中的代码全部执行完成。

这是同步代码的执行过程。

**那么异步代码的执行过程呢？**

js引擎遇到一个异步事件后，并不会一直等待其返回结果，因为js非阻塞的特点，而是会将这个事件挂起（pending），继续执行执行栈中的其他任务。当一个异步事件返回结果后，js引擎会将这个事件加入到与当前执行栈不同的另外一个队列，一般称为事件队列。被放入事件队列的事件不会被立即执行，而是会<font color="#f20">等待当前执行栈中的所有任务都执行完成后、主线程处于闲置状态时，主线程会去查找事件队列中是否有任务在排队等待执行。如果有，那么主线程就会从事件队列中抽取出排位第一顺序的事件对应的回调函数放入到执行栈中，然后执行其中的同步代码</font>。按照这个规律反复循环。这个过程就是事件循环（Event loop）。

```javascript
var btn = document.getElementById("btn");
btn.addEventListener("click", function timer() {
  setTimeout(function () {
    console.log("点击了按钮");
  }, 2000);
});

console.log("Hi");

setTimeout(function timeout() {
  console.log("来点击按钮");
}, 5000);
console.log("欢迎你!");
// 执行结果
// Hi 、 欢迎你、来点击按钮    如果点击了按钮，则会打印“点击了按钮”，没有点击按钮，则不打印
```

**宏任务和微任务**

在事件循环过程中有很多不同的异步任务，这些异步任务也有区别，实际上也需要不同的异步任务有不同的执行优先级，然后异步任务又被分为了两类：宏任务、微任务。

**宏任务、微任务，都指的是异步任务。**

宏任务：

1. script
2. setTimeout()  定时器
3. setInterval()  定时调用
4. postMessage()
5. I/O
6. UI交互事件

微任务

1. new Promise().then(回调)  注意只有then部分才是微任务，new Promise()是同步的
2. MutationObserver():

**宏任务和微任务的执行顺序**

当当前执行栈执行完毕时，会立刻处理所有微任务队列中的事件，然后再去处理执行宏任务队列中的事件。

同一次事件循环中，微任务永远在宏任务之前执行。

### node环境下的事件循环机制

**node中的事件循环机制和浏览器中的区别**

node中的事件循环机制和浏览器中的基本相同，只是node有自己的事件模型，node中的事件循环的实现依赖libuv引擎。

node选择chrome v8引擎作为js的解释器，v8引擎将js代码解析后去调用对应的node api，这些node api最后由libuv引擎驱动，执行对应的任务，并把不同的事件放在不同的队列中等待主线程执行。

所以说node中的事件循环存在于libuv引擎中。

**node的事件模型**

 ┌───────────────────────┐
┌─>│        timers         │
│  └──────────┬────────────┘
│  ┌──────────┴────────────┐
│  │     I/O callbacks     │
│  └──────────┬────────────┘
│  ┌──────────┴────────────┐
│  │     idle, prepare     │
│  └──────────┬────────────┘      ┌───────────────┐
│  ┌──────────┴────────────┐      │   incoming:   │
│  │         poll          │<──connections───     │
│  └──────────┬────────────┘      │   data, etc.  │
│  ┌──────────┴────────────┐      └───────────────┘
│  │        check          │
│  └──────────┬────────────┘
│  ┌──────────┴────────────┐
└──┤    close callbacks    │
   └───────────────────────┘

模型中的每个方块都代表事件循环的一个阶段。

<font color="#f20">这个不太好理解，还没有梳理好</font>

### 题目分析

```javascript
setTimeout(function () {
  console.log(1);
});

new Promise(function (resolve, reject) {
  console.log(2);
  resolve(3);
}).then(function (val) {
  console.log(val);
});
// 执行结果：2,3,1
```

```javascript
console.log(1);
setTimeout(function () {
  console.log(2);
}, 0);

const intervarId = setInterval(function () {
  console.log(3);
}, 0);

setTimeout(function () {
  console.log(10);
  new Promise(function (resolve) {
    console.log(11);
    resolve();
  })
    .then(function () {
      console.log(12);
    })
    .then(function () {
      console.log(13);
      clearInterval(intervarId);
    });
}, 0);

Promise.resolve()
  .then(function () {
    console.log(7);
  })
  .then(function () {
    console.log(8);
  });
console.log(9);
//1  9 7  8  2  3  10  11  12   13
```

```javascript
async function async1() {
  console.log("async1 start");
  await async2();
  console.log("async1 end");
}

async function async2() {
  console.log("async2");
}

async1();

new Promise(function (resolve) {
  console.log("promise1");
  resolve();
}).then(function () {
  console.log("promise2");
});
console.log("script end");
//async1 start、async2、promise1、script end、async1 end、promise2
```

```javascript
const s = new Date().getSeconds();

setTimeout(function () {
  console.log("Ran after " + (new Date().getSeconds() - s) + "seconds");
}, 500);

while (true) {
  if (new Date().getSeconds() - s >= 2) {
    console.log("Good,looped for 2 seconds");
    break;
  }
}
// Good,looped for 2 seconds、Ran after 2seconds
// 先同步执行栈，再异步
```

```javascript
setTimeout(() => {
  console.log(1);
}, 20);

setTimeout(() => {
  console.log(2);
}, 0);

setTimeout(() => {
  console.log(3);
}, 10);

setTimeout(() => {
  console.log(5);
}, 10);

console.log(4);

// 4  2  3   5  1
```

```javascript
setTimeout(() => {
  console.log(1);
}, 20);
setTimeout(() => {
  console.log(2);
}, 0);
setTimeout(() => {
  console.log(3);
}, 30);
console.log(4);
// 4  2  1  3
```

```javascript
console.log(1);
new Promise((resolve, reject) => {
  console.log(2);
  resolve();
}).then((res) => {
  console.log(3);
});
console.log(4);
// 1  2  4  3
```

```javascript
setTimeout(function () {
  console.log(1);
}, 0);

new Promise(function (resolve, reject) {
  console.log(2);
  resolve();
})
  .then(function () {
    console.log(3);
  })
  .then(function () {
    console.log(4);
  });
console.log(6);
// 2 6 3 4 1
```

```javascript
setTimeout(function () {
  console.log(1);
}, 0);
new Promise(function (resolve, reject) {
  console.log(2);
  for (var i = 0; i < 10000; i++) {
    if (i === 10) {
      console.log(10);
    }
    i == 9999 && resolve();
  }
  console.log(3);
}).then(function () {
  console.log(4);
});
console.log(5);
//2  10  3  5  4  1
```

```javascript
console.log("start");
setTimeout(() => {
  console.log("children2");
  Promise.resolve().then(() => {
    console.log("children3");
  });
}, 0);

new Promise(function (resolve, reject) {
  console.log("children4");
  setTimeout(function () {
    console.log("children5");
    resolve("children6");
  }, 0);
}).then((res) => {
  console.log("children7");
  setTimeout(() => {
    console.log(res);
  }, 0);
});
//start、children4、children2、children3、children5、children7、children6
// 需要注意当前执行栈中的所有任务都执行完成后才去执行下一个任务
```

```javascript
async function async1() {
  console.log("async1 start");
  await async2();
  console.log("async1 end");
}

async function async2() {
  console.log("async2");
}
console.log("script start");
setTimeout(function () {
  console.log("setTimeout");
}, 0);
async1();
new Promise((resolve) => {
  console.log("promise1");
  resolve();
}).then(function () {
  console.log("promise2");
});
console.log("script end");
//script start、async1 start、async2、promise1、script end、async1 end、promise2、setTimeout
```

```javascript
async function async1() {
  console.log("async1 start");
  await async2();
  console.log("async1 end");
}
async function async2() {
  new Promise(function (resolve) {
    console.log("promise1");
    resolve();
  }).then(function () {
    console.log("promise2");
  });
}
console.log("script start");
setTimeout(function () {
  console.log("setTimeout");
}, 0);
async1();
new Promise(function (resolve) {
  console.log("promise3");
  resolve();
}).then(function () {
  console.log("promise4");
});
console.log("script end");
// script start、async1 start、promise1、promise3、script end、promise2、async1 end、promise4、setTimeout
```