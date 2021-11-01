### js实现sleep函数

sleep函数，就是睡眠的意思，顾名思义，就是等待一会才去执行。

其他编程语言有类似sleep的方法、函数，而js中没有类似的原生的方法，所以sleep函数才会在js中被问到的频率高升。

因为sleep，就是等待，我们很容易就可以想到setTimeout。

没错，setTimeout确实可以实现。

```javascript
function sleep(callback,time){
    setTimeout(callback,time);
}
```

实现sleep函数，就是这么简单，这就已经实现了sleep函数的基本功能。

还有另外的一种实现方法，就是借助Promise，可以让代码实现的更优雅一些：

````javascript
function sleep(time){
    return new Promise((resolve) => {
        setTimeout(resolve,time);
    });
}

// 调用
sleep(3000).then(function(){
    console.log(6666);
});
````

这种方式，无论是实现，还是调用，从外观上来看，都更优雅一些。

不过这都是异步的执行方式，还可以设置同步的执行方式：

```javascript
(async function(){
    console.log("start");
    await sleep(1500);
    console.log("sleep");
    console.log("end");
})();
```

