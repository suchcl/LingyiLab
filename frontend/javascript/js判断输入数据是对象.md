javascript判断一个变量是不是一个对象，在数据处理的时候经常遇到。那么可以通过什么方式判断一个变量是不是一个对象呢？

1. typeof关键字

```js
    const a = undefined;
    console.log('%c [ a ]-3', 'font-size:13px; background:pink; color:#bf2c9f;', typeof a); // undefined
    const b = "abcd";
    console.log('%c [ b ]-5', 'font-size:13px; background:pink; color:#bf2c9f;', typeof b); // string
    const c = 1;
    console.log('%c [ c ]-7', 'font-size:13px; background:pink; color:#bf2c9f;', typeof c); // number
    const d = [1,2];
    console.log('%c [ d ]-9', 'font-size:13px; background:pink; color:#bf2c9f;', typeof d); // object
    const e = {a: 12};
    console.log('%c [ e ]-11', 'font-size:13px; background:pink; color:#bf2c9f;', typeof e); // object
    const f = null;
    console.log('%c [ f ]-13', 'font-size:13px; background:pink; color:#bf2c9f;', typeof f); // object
    const g = function(){
        console.log('%c [  ]-10', 'font-size:13px; background:pink; color:#bf2c9f;', "function"); // object
    };
    console.log('%c [ g ]-15', 'font-size:13px; background:pink; color:#bf2c9f;', typeof g); // function
```

通过案例我们可以得出结论，当使用typeof判断null、普通对象和数组的时候，其值都是object。

如果需要判断变量是数组或者普通对象的时候，可以通过如下的方式：

```js
if(obj !== null && typeof obj === "object"){
    return true;
}
return false;
```

不过这种判断，好像没有什么实际价值，更多的是需要判断当前变量究竟是一个数组，还是一个普通的对象，又或者是一个null。

2. instanceof关键字

3. Array.isArray()

4. Object.prototype.toString()方法

5. 使用第三方库如lodash提供的方法

**总结**

判断一个变量是不是对象，有多种判断方法，通常情况下，使用Object.prototype.toString方法可以准确的判断一个变量的类型。