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

instanceof是另外一种判断对象的方式：

```js
    const a: any = undefined;
    console.log('%c [ a ]-27', 'font-size:13px; background:pink; color:#bf2c9f;', a instanceof Object); // false
    const b: any = "abcd";
    console.log('%c [ b ]-29', 'font-size:13px; background:pink; color:#bf2c9f;', b instanceof Object);  // false
    const c: any = 1;
    console.log('%c [ c ]-31', 'font-size:13px; background:pink; color:#bf2c9f;', c instanceof Object);  // false
    const d = [1, 2];
    console.log('%c [ d ]-33', 'font-size:13px; background:pink; color:#bf2c9f;', d instanceof Object);  // true
    const e = { a: 12 };
    console.log('%c [ e ]-35', 'font-size:13px; background:pink; color:#bf2c9f;', e instanceof Object);  // true
    const f: any = null;
    console.log('%c [ f ]-37', 'font-size:13px; background:pink; color:#bf2c9f;', f instanceof Object);  // false
    const g = function () { };
    console.log('%c [ g ]-39', 'font-size:13px; background:pink; color:#bf2c9f;', g instanceof Object); // true
```

从案例中可以看到：

使用instanceof关键字的时候，数组、普通对象和数组会被判定为Object。null不会被判定为Object，它是一个独立的类型。

3. Array.isArray()

Array.isArray()可以判断数组，比较精准。这是ES6中新增的api,返回值是一个布尔值。


```js
const arr = [2, 3];
console.log('%c [  ]-47', 'font-size:13px; background:pink; color:#bf2c9f;', Array.isArray(arr)); // true
const obj = {};
console.log('%c [  ]-49', 'font-size:13px; background:pink; color:#bf2c9f;', Array.isArray(obj)); // false
```

只有在数组的时候，才会返回true。

4. Object.prototype.toString方法

```ts
const a: any = undefined;
console.log('%c [ a ]-54', 'font-size:13px; background:pink; color:#bf2c9f;', Object.prototype.toString.call(a)); // [object Undefined]
const b: any = "abcd";
console.log('%c [ b ]-56', 'font-size:13px; background:pink; color:#bf2c9f;', Object.prototype.toString.call(b)); // [object String]
const c: any = 1;
console.log('%c [ c ]-58', 'font-size:13px; background:pink; color:#bf2c9f;', Object.prototype.toString.call(c)); // [object Number]
const d = [1, 2];
console.log('%c [ d ]-60', 'font-size:13px; background:pink; color:#bf2c9f;', Object.prototype.toString.call(d)); // [object Array]
const e = { a: 12 };
console.log('%c [ e ]-62', 'font-size:13px; background:pink; color:#bf2c9f;', Object.prototype.toString.call(e)); // [object Object]
const f: any = null;
console.log('%c [ f ]-64', 'font-size:13px; background:pink; color:#bf2c9f;', Object.prototype.toString.call(f)); // [object Null]
const g = function () { };
console.log('%c [ g ]-66', 'font-size:13px; background:pink; color:#bf2c9f;', Object.prototype.toString.call(g)); // [object Function]
```

当且仅当是普通对象的时候，返回了字符串[object Object],所以如果需要判断对象类型的时候，可以通过如下方式：

```js
if(Object.prototype.toString.call(obj) === "[Object Object]"){
    return true;
}
```

5. 使用第三方库如lodash提供的方法

lodash库提供了很多功能强大的工具库函数，可以根据需要使用。

**总结**

判断一个变量是不是对象，有多种判断方法，通常情况下，使用Object.prototype.toString方法可以准确的判断一个变量的类型。