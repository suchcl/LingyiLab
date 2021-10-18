### var声明的全局变量，默认会被绑定到window上，let、const声明的变量，默认不会被绑定到window上

```javascript
// a,b分别是使用let、const声明的，所以a、b两个变量不会被绑定到window上
let a = 10;
const b = 20;
function foo() {
  console.log(this.a);
  console.log(this.b);
}
// foo函数，是在全局作用域执行的，所以函数foo的this指向的是window
foo(); //undefined,undefined
console.log(window.a); // undefined
```

### var是函数作用域，找变量时需要注意注意this的指向

```javascript
var a = 1;
function foo() {
  var a = 2;
  console.log(this); // window
  console.log(this.a); // 1,需要注意下限定词this,this是window
  console.log(a); // 2
}
foo();
```

案例中，函数foo的this指向的是window，函数外通过var声明的a，默认绑定到了window上，函数内通过var声明的变量a，具有函数的作用域，如果在函数内部找a，找的是函数内部声明的a=2，但是如果在函数内部通过this找a，则找的是window上的a。

### 闭包中的this指向window

闭包中的this指向window，如果期望闭包可以访问其包裹函数的this，将其包裹函数的作用域传给闭包即可。

```javascript
var num = 1;
var obj = {
  num: 2,
  getNum: function () {
    return (function () {
      return this.num;
    })();
  },
};
console.log(obj.getNum()); // 1
```

闭包中的this指向window，所以闭包中的this.num,最终找的是绑定在window上的num。

那如果这个案例中，如果闭包想访问内部的num怎么获取呢？传入一下作用域就可以了。

```javascript
var num = 1;
var obj = {
  num: 2,
  getNum: function () {
    return (function (self) {
      return self.num;
    })(this); // 传入当前的函数作用域，就可以取当前函数中的数据了
  },
};
console.log(obj.getNum()); // 2
```

### 隐式绑定

隐式绑定，就是被隐式绑定的函数在特定的情况下会丢失绑定对象。

有两种情况会发生隐式丢失问题：

1. 使用另一个变量为函数取别名；

2. 将函数作为参数传递时会被隐式赋值，回调函数丢失this绑定；

this永远指向最后调用它的那个对象，谁最后调用的函数，函数内部的this指向的就是谁（剪头函数除外）。

```javascript
function foo() {
  console.log(this.a);
}
var obj = { a: 1, foo };
var a = 2;
obj.foo(); // 1  谁最后调用的函数，函数中的this就指向谁，案例中obj最后调用的foo，那么函数foo中this指向的就是foo
```

```javascript
function foo() {
  console.log(this.a);
}
var obj = { a: 1, foo };
var a = 2;
var foo2 = foo;
obj.foo(); // 1 obj最后调用的foo，所以foo内部this指向的是obj
foo2(); // 2 foo2 = foo,是将foo函数的内存地址赋值给了foo2,且调用foo2的是window（缺省了），所以this指向的还是window
```

```javascript
function foo() {
  console.log(this.a);
}
function doFoo(fn) {
  console.log(this); // window
  fn();
}
var obj = { a: 1, foo };
var a = 2;
doFoo(obj.foo); // window 2,注意obj.foo没有小括号，就说明这个函数并没有执行，所以obj.foo是没有打印输出的，只是一个参数而已
```

```javascript
function foo() {
  console.log(this.a);
}

function doFoo(fn) {
  console.log(this);
  fn();
}

var obj = { a: 1, foo };
var a = 2;
var obj2 = { a: 3, doFoo };
obj2.doFoo(obj.foo); //obj2,2
```

> 非严格模式下，会把一些全局的this指向到window；在严格模式下，全局的this会指向到undefined

```javascript
"use strict";
function foo() {
  console.log(this.a);
}
function doFoo(fn) {
  console.log(this);
  fn();
}
var obj = { a: 1, foo };
var a = 2;
var obj2 = { a: 3, doFoo };
obj2.doFoo(obj.foo); // obj2,异常提示，因为在严格模式下，全局的this指向了undefined，undefined是没有a属性的，所以就给出来异常信息提示
```

### 显示绑定

显示绑定this，就是通过一些方法，显示的改变函数的this指向，主要通过的方法有call()、apply()、bind()直接指定this的绑定对象。

**注意：**

1. 使用.call()或者.apply()的函数是会直接执行的；

2. bind()是创建一个新的函数，需要手动调用才会执行；

3. .call()和.apply()用法基本类似，只是.call()接收多个参数，.apply()接收一个数组参数，就是一个参数的集合。

```javascript
function foo() {
  console.log(this.a);
}
var obj = { a: 1 };
var a = 2;
foo(); //2
foo.call(obj); // 1
foo.apply(obj); // 1
foo.bind(obj); // 什么都没有输出，bind会创建一个新的函数，需要手动调用才可以执行，否则不会执行
foo.bind(obj)(); // 1 新建一个函数，并执行，重新指定了this
```

**bind()**
bind()会创建一个新的函数，当这个函数被执行时，它的this就指向传递给bind的第一个参数

```javascript
var num = 9;
var mymodule = {
  num: 81,
  getNum: function () {
    console.log(this.num);
  },
};
mymodule.getNum(); // 81

var getNum = mymodule.getNum;
getNum(); // 9

getNum.bind(mymodule)(); // 创建一个新的函数，this指向创建新函数时的第一个参数，该行代码，也可以这么组织：

var boundGetNum = getNum.bind(mymodule);
boundGetNum(); // 81
```

> 如果call()、apply()、bind()接收的第一个参数是空或者null、undefined的话，则会忽略这个参数

```javascript
function foo() {
  console.log(this.a);
}
var a = 2;
foo.call(); // 2
foo.call(null); // 2
foo.call(undefined); // 2 虽然这3个调用都调用了call，但是给call传入了空、null或undefined，传入这些值，这些参数会被直接忽略
```

```javascript
var obj1 = {
  a: 1,
};
var obj2 = {
  a: 2,
  foo1: function () {
    console.log(this.a);
  },
  foo2: function () {
    setTimeout(function () { // 注意这里发生了隐式绑定的隐式丢失
      console.log(this);
      console.log(this.a);
    }, 0);
  },
};
var a = 3;
obj2.foo1(); // 2
obj2.foo2(); // window 3
```

call()改变this指向

```javascript
var obj1 = {
  a: 1,
};
var obj2 = {
  a: 2,
  foo1: function () {
    console.log(this.a);
  },
  foo2: function () {
    setTimeout(
      function () {
        console.log(this);
        console.log(this.a);
      }.call(obj1),
      0
    );
  },
};
var a = 3;
obj2.foo1(); //2
obj2.foo2(); //obj1,1
```

内部函数，如果是window调用的，其this也是指向window

```javascript
var obj1 = { a: 1 };
var obj2 = {
  a: 2,
  foo1: function () {
    console.log(this.a);
  },
  foo2: function () {
    function inner() {
      console.log(this);
      console.log(this.a);
    }
    inner(); // 注意：谁调用的函数，this就指向谁，这里是window调用的，所以this指向的window
  },
};
var a = 3;
obj2.foo1(); // 2
obj2.foo2(); //window, 3
```

```javascript
function foo() {
  console.log(this.a);
}
var obj = {
  a: 1,
};
var a = 2;
foo(); //2
foo.call(obj); //1
foo().call(obj); // 2 类型错误，因为foo()执行后就是一个数值了，该数值没有方法call(),所以就报错了
```