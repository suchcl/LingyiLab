### js的内存管理

js与许多其他现代的编程语言一样，使用自动内存管理，即js会自动完成垃圾回收。这也就意味着，我们在程序运行的时候不需要手动分配内存和释放内存。

自动内存管理(垃圾回收)主要通过标记-清除法完成，主要分为2个阶段：

1. 标记阶段：垃圾收集器从根对象开始，标记所有可到达或可访问的对象；

2. 清除阶段：任何未标记(即无法访问)的对象都被视为“垃圾”，并且其内存将被释放；

但是自动的内存管理无法管理所有场景下的内存问题，所以在一些特殊场景下就会导致出现**内存泄漏**的问题。

### 关于内存泄漏

垃圾回收经常伴随着内存泄漏的概念。这里我们需要理清一个概念：就是内存泄漏和内存溢出是不同的。

> 内存溢出，指的是程序运行过程中需要使用的内存大于系统能够提供的内存。即系统内存不足。

一般所谓的内存泄漏指的是：当一块内存(通常是变量)未被释放(垃圾回收)，同时我们也无法访问到它时。我们也可以简单的理解为：一个变量，我们访问不到它了，但是它占用的内存还没有被回收。那么这个时候，就会出现内存泄漏的问题：

1. 未清理的定时器或者回调

- 场景：使用setInterval或setTimeout，但在组件清理或者不再需要时没有清理

- 结果：定时器还在，引用被保留，导致无法释放内存

```js
function startTimer(){
    setInterval(() => {
        console.log("定时器");
    }, 1000);
}
```

如果调用函数后不清理定时器，那么就会造成内存泄漏。

可按照如下方式进行优化：

```js
const timer = setInterval(() => {
    console.log("定时器");
}, 1000);
clearInterval(timer); // 使用完成后，要及时清理
```

2. DOM引用未释放

- 场景：保留对已经移除的DOM元素的引用

- 结果：虽然DOM节点从页面上被移除，但是js中仍有对它的引用，导致内存泄漏

```js
const ele = document.getElementById("leak");
document.body.removeChild(ele); // 因为id为leak的元素已经被删除，但是js中仍然存在对其的引用，导致了内存没有办法被释放
```

可以通过下面的方式进行优化:

```js
ele = null;
```

显示的将其置空，内存得到释放。

3. 闭包中多余的引用

- 场景：闭包中的变量保留了对外部对象的引用，导致对象无法被垃圾机制回收

- 结果：长时间的引用链阻止了内存释放

```js
function createClosure(){
    const largeObject = new Array(1000).fill("leak");
    return function(){
        console.log('%c [ largeObject ]-20', 'font-size:13px; background:pink; color:#bf2c9f;', largeObject);
    }
}

const closure = createClosure(); // 这里有个漏洞，就是closure使用完了以后，不再被继续使用了，largeObject也依然存在
```

可以优化一下，在使用完成后主动释放内存：

```js
function createClosure(){
    const largeObject = new Array(1000).fill("leak");
    return function(){
        console.log('%c [ largeObject ]-20', 'font-size:13px; background:pink; color:#bf2c9f;', largeObject);
        largeObject = null; // 这样，显示的释放了内存
    }
}

const closure = createClosure();
```

4. 全局变量或未声明变量

- 场景：未使用var、let、const定义变量，导致变量挂载到全局作用域；

- 结果：全局变量生命周期与页面一致，无法被垃圾机制回收

```js
function leak(){
    leakedVariable = "I am a leak"; // leakedVariable是一个隐式的全局变量，其声明周期不随函数，而随页面的声明周期一起变动
}
leak();
```

可以使用var、let或者const关键字来约束变量的作用域

```js
function leak2(){
    const leakedVariable = "I am a leak"; // leakedVariable被限定在了leak2的函数作用域
}
leak2();
```

5. 事件监听器未清理

- 场景：在DOM元素上绑定了事件监听器，但是没有在元素销毁时移除

- 结果：监听器仍然存在，阻止DOM元素被回收

```js
const button = document.getElementById("btn");
button.addEventListener("click", () => {
    console.log('%c [ clickhandle ]-42', 'font-size:13px; background:pink; color:#bf2c9f;', "点击事件click");
});
document.body.removeChild(button); // 这段代码存在一个内存泄漏风险：button已经被移除了，但是button和监听器仍然在被引用
```

可以显示的移除事件监听器

```js
const btn = document.getElementById("btn");
const handler = () => {
    console.log('%c [ handler ]-48', 'font-size:13px; background:pink; color:#bf2c9f;', "点击事件");
};
btn.addEventListener("click", handler);
btn.removeEventListener("click", handler); // 事件完成之后，要及时销毁事件监听器
document.body.removeChild(btn);
```

6. 忘记清理Set/Map中的键或值

7. 闭环引用

- 两个对象互相引用，导致垃圾回收机制无法判断它们是否可以释放

- 结果：循环引用导致内存泄漏

```js
function CircularReference(){
    const obj1 = {};
    const obj2 = {};
    obj1.ref = obj2;
    obj2.ref = obj1;
}
```

如果可以的话，可以使用WeakMap/WeakSet来避免相互引用

```js
function CircularReference(){
    const obj1 = {};
    const obj2 = {};
    obj1.ref = obj2;
    obj2.ref = obj1;
}
```