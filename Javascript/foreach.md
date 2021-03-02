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

**那我们还是想再某种场景下终止循环，怎么处理呢？**

办法还是有的，只不过是一种曲折、迂回的办法