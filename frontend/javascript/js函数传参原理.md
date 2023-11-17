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

奇怪，一个变量作为参数传递给一个函数，在函数中修改这个参数的值，那么最终会影响到这个变量的值吗？

从demo来看，有的可以改变变量原来的值，有的不会改变变量原来的值。这里面有什么规律吗？

### 函数的参数：形参和实参

js中函数传参常用的两种方式：形参和实参。

形参：所谓形参，就是函数定义的时候给函数定义的参数，例如demo中testP和testObj函数的param参数，这2个函数中的param都是形参。

实参：所谓实参，就是在函数调用的时候实际传递给函数的值，如demo中testP函数中调用时的p和testObj函数调用时传递的参数obj都是实参。

### js中函数中参数的传递方式：按值传递和按引用传递

#### 按值传递

按值传递，是一种比较容易理解，也使用最为广泛的一种传递方式，在使用这种方式传参的时候，首先在内存中复制一份实参的值，然后把复制的副本传递给

#### 按引用传递

<font color="#f20">首先可以明确一点，在js函数中，所有函数参数都是按值传递，而不是按引用传递。</font>

按引用传递，就是形参接收的是实参的引用，而不是实参的一份复制的副本，那么函数中对于形参的修改将会直接影响到实参本身的值。