### promise

**promise是什么呢？**

<font color="#f20">promise是异步编程的一种解决方案。</font>

**什么时候会处理异步事件呢？**

一般情况下，有类似网络请求等异步操作的时候会用到promise，对异步操作进行封装。

**Promise有三种状态**

pending:等待状态

fulfill：满足状态，成功状态

reject：拒绝状态，

promise机制

将异步操作包裹一层Promise

```html
    <script>
        new Promise((resolve, reject) => {
            setTimeout(() => {
                resolve("Hello Vue");
            }, 4000);
        }).then(data => { // data是从resolve传递过来的数据，只要resolve执行力，就一定会执行then
            console.log(data);
        }, err => {
            console.log(err);
        });
    </script>
```

promise的链式调用

