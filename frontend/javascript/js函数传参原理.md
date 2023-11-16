### js中函数的传参原理

先来看一段代码，也是迷惑了我很久的一段代码了，网上也有类似的代码。

```js
var p = 1;
var obj = {};

function testP(param) {
  param = 2;
}

function testObj(param) {
  param.test = 3;
}
testP(p);
testObj(obj);

console.log('%c [ p ]-14', 'font-size:13px; background:pink; color:#bf2c9f;', p)
console.log('%c [ obj ]-16', 'font-size:13px; background:pink; color:#bf2c9f;', obj)
```

这段代码执行后的p和obj的最终结果是什么呢？

```js
p: 1;
obj: {test: 3}
```
p的值没有变，还是1，obj的值变了，obj新增了属性test，并赋值为3；