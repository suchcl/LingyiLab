在通过forEach()进行数据遍历的时候，有的时候期望在某个场景中终止遍历，因为并不是所有的数据都需要遍历，或者遍历的时候没有实际的意义。那么按照正常的逻辑，可能我们会在遍历某个值的时候，return 一下，或者return false，这是我们的常规做法。但是在forEach遍历中，使用return或者return false只能退出当次遍历而进行到下一次遍历。

```javascript
let fruits = ["apple", "peach", "pear"];
fruits.forEach((item) => {
    if (item == "peach") {
        return; // 使用return false是同样的效果，只是终止了档次循环，但是转而进入到了下次循环中
    }
    console.log(item);
});
```
输出结果如下
```bash
apple
pear
```

这个时候我想到了可以使用break来终止循环了，于是我就拿过来实践一下吧：

```javascript
let fruits = ["apple", "peach", "pear"];
fruits.forEach((item) => {
    if (item == "peach") {
        break;
    }
    console.log(item);
});
```
我们执行下代码，看下结果:

```bash
D:\Iterator\index.js:33
        break;
        ^^^^^

SyntaxError: Illegal break statement
    at wrapSafe (internal/modules/cjs/loader.js:979:16)
    at Module._compile (internal/modules/cjs/loader.js:1027:27)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:1092:10)
    at Module.load (internal/modules/cjs/loader.js:928:32)
    at Function.Module._load (internal/modules/cjs/loader.js:769:14)
    at Function.executeUserEntryPoint [as runMain] (internal/modules/run_main.js:72:12)
    at internal/main/run_main_module.js:17:47
```

结果报错了。

原来在forEach()中是不可以使用break的。

> 到这里为止，我们应该已经可以感知到了，就是不能通过正常的流程来终止foreach循环的。

**那我们还是想再某种场景下终止循环，怎么处理呢？**

办法还是有的，只不过是一种曲折、迂回的办法，就是通过抛出异常的办法，可以看下面的示例：

```javascript
try {
    let fruits = ["apple", "peach", "pear"];
    fruits.forEach((item) => {
        if (item == "peach") {
            throw new Error("End");
        }
        console.log(item);
    });
}catch(e){
    console.log(e.message);
}

console.log("遍历之后的代码");
```

看执行结果：

```bash
PS D:\Iterator> node .\index.js
apple
End
遍历之后的代码
```

到了指定的场景，确实是退出了循环，不光是本次循环，而是真个循环直接退出来后继续执行该代码块后续的代码了，没有影响代码的整体执行。话说回来，这也是一种曲线救国策略。
