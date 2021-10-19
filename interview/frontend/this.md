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
foo().call(obj); // 2 类型错误，因为foo()执行后正常打印了数值2，最后对foo函数的返回值执行call，foo函数的返回值是undefined，所以就报错了
```

函数内部的函数执行，如果没有指定调用方，那么就是window调用的

```javascript
function foo() {
  console.log(this.a);
  return function () {
    console.log(this.a);
  };
}
var obj = {
  a: 1,
};
var a = 2;
foo(); //2
foo.call(obj); // 1
foo().call(obj); // 2, 1 // foo()的返回值是一个函数，该函数的调用方是window，但是通过call将this指向了obj
```

```javascript
function foo() {
  console.log(this.a);
  return function () {
    console.log(this.a);
  };
}
var obj = {
  a: 1,
};
var a = 2;
foo(); //2
foo.bind(obj); // 无输出  函数没有执行foo.bind(obj)()才是执行了
foo().bind(obj); // 2，无输出   函数返回值只是重新绑定了this的指向，但是新函数没有执行，所以无输出
```

```javascript
function foo() {
  console.log(this.a);
  return function () {
    console.log(this.a);
  };
}
var obj = {
  a: 1,
};
var a = 2;
foo.call(obj)(); // 1,2返回值是一个函数，执行内部函数，其调用方是window，所以window.a是2
```

面试题，就是各种绕你，但是只要抓住了其中不变的地方以及核心的几个知识点，是绕不开的。

```javascript
var obj = {
  a: "obj",
  foo: function () {
    console.log(
      "%c [ foo ]",
      "font-size:13px; background:pink; color:#bf2c9f;",
      this.a
    );
    return function () {
      console.log("inner", this.a);
    };
  },
};

var a = "window";
var obj2 = {
  a: "obj2",
};
obj.foo()(); // obj,window
obj.foo.call(obj2)(); // obj2, window
obj.foo().call(obj2); //obj, obj2
```

```javascript
var obj = {
  a: 1,
  foo: function (b) {
    b = b || this.a;
    return function (c) {
      // console.log(this); // window
      console.log(this.a + b + c);
    };
  },
};
var a = 2;
var obj2 = {
  a: 3,
};

obj.foo(a).call(obj2, 1); // 6
/**
 * 解释上面一行代码
 * obj.foo(a) foo的this为obj，b得到赋值为2
 * 返回值内部函数再次执行：内部函数的this指向window，但是通过call改变了this指向，所以内部函数中的this.a = 3;
 * c为传入的参数：1
 * 所以最终结果位：this.a + b + c = 3 + 2 + 1 = 6
 */
obj.foo.call(obj2)(1); // 6
/**
 * 解释上面一行代码
 * obj.foo.call(obj2)：obj中foo原本的this为obj，但是通过call改变了this的指向，指向到了obj2
 * 因此得到b = this.a也就是obj2中的a，即3
 * 接下来返回值函数执行：返回值函数的this指向window，所以this.a = 2; c为传入的参数1
 * 所以最终结果为this.a + b + c = 2 + 3 + 1 = 6
 */
```

### 显示绑定的其他一些用法

可以在一个函数内部使用call来显示绑定某个对象，这样无论怎么样调用，其内部的this总是指向这个对象。

```javascript
function foo1() {
  console.log(this.a);
}
var a = 1;
var obj = {
  a: 2,
};
var foo2 = function () {
  foo1.call(obj); // 无论外部怎么调用，怎么绑定其他的迷惑人的对象，其内部的foo1的obj始终指向obj
};
foo2(); // 2
foo2.call(window); // 2
/**
 * 解释上一行代码
 * 虽然foo2.call(window)绑定了window，但是foo2的函数体内执行的是foo1，foo1绑定了obj
 * 无论foo2怎么绑定，但是内部执行的代码已经有所绑定的对象了，都不会变
 */
```

还是考察定力

```javascript
function foo1(b) {
  console.log(`${this.a} + ${b}`);
  return this.a + b;
}
var a = 1;
var obj = {
  a: 2,
};

var foo2 = function () {
  return foo1.call(obj, ...arguments);
};
var num = foo2(3);
console.log(num); // 2 + 3, 5
/**
 * 本题并不难，但是需要注意别被乱七八糟的东西给迷惑了
 */
```

数组的filter、map、forEach也可以绑定this，改变this的指向

```javascript
function foo(item) {
  console.log(item, this.a);
}
var obj = {
  a: "obj",
};
var a = "window";
var arr = [1, 2, 3];
arr.filter(function (i) {
  console.log(i, this.a);
  /**
   * 1 obj
   * 2 obj
   * 3 obj
   */
  return i > 2;
}, obj);
```

#### 小结

1. this永远指向最后调用它的那个对象
2. 匿名函数的this指向window
3. 使用call()或者apply()的函数会立即执行
4. bind()会创建一个新的函数，不会自动立即执行，需手动调用才可执行
5. 如果call()、apply()、bind()接收到的第一个参数是null、undefined或者是空，则忽略这个参数
6. 数组的forEach、map、filter函数的第2个参数也可以动态的显示的绑定this，改变this的指向

### new绑定

不管是new绑定还是其他方式的绑定，以及call、apply、bind，还是数组的forEach、filter、map等，函数内部的this始终指向最后调用它的对象。

```javascript
function Person(name) {
  this.name = name;
}
var name = "window";
var person1 = new Person("Nicholas");
console.log(person1.name); // Nicholas
```

```javascript
function Person(name) {
  this.name = name;
  this.foo1 = function () {
    console.log(this.name);
  };
  this.foo2 = function () {
    return function () {
      console.log(this.name);
    };
  };
}
var person1 = new Person("p1");
person1.foo1(); // p1
person1.foo2()(); // 空值，没有输出
/**
 * 比较有意思的是，一开始给输出了一个window，原来是我之前代码中定义过name属性赋值为window，var name="window",代码删除了之后，浏览器也不会回收
 * 当前的浏览器标签页关掉了才可以回收之前window上的属性
 */
```

```javascript
var name = "Nicholas";
function Person(name) {
  this.name = name;
  this.foo = function () {
    console.log(this.name);
    return function () {
      console.log(this.name);
    };
  };
}
var person2 = {
  name: "person2",
  foo: function () {
    console.log(this.name);
    return function () {
      console.log(this.name);
    };
  },
};

var person1 = new Person("person1");
person1.foo()(); //person1,Nicholas
person2.foo()(); //person2,Nicholas
```
无论是函数，还是对象，其内部匿名函数的this，始终指向window

```javascript
var name = "window";
function Person(name) {
  this.name = name;
  this.foo = function () {
    console.log(this.name);
    return function () {
      console.log(this.name);
    };
  };
}

var person1 = new Person("person1");
var person2 = new Person("person2");
person1.foo.call(person2)(); // person2,widnow
person2.foo().call(person2); // person2,person2
```

百变不离其宗，只要抓住几个核心的点，谁调用的函数、bind、call、apply以及数组的几个方法：forEach、map、filter

### 箭头函数的this绑定

普通的函数，其this永远指向最后调用它的那个对象，但是箭头函数就不是了：

箭头函数中的this，是由外层作用域决定的，指向函数定义时的this，而不是执行时的this。

> 箭头函数中没有this绑定，必须通过查找作用域链来决定this的指向的值，如果剪头函数被非箭头函数包裹，则箭头函数中的this指向的是最近一层非箭头函数的this，否则，this值位undefined

```javascript
var obj = {
  name: "obj",
  foo1: () => {
    // foo1箭头函数，其作用域是外层作用域，外层作用域也就是window
    console.log(this.name);
  },
  foo2: function () {
    console.log(this.name);
    return () => {
      console.log(this.name);
    };
  },
};
var name = "window";
obj.foo1(); // window
obj.foo2()(); // obj, obj
```

```javascript
var name = "window";
var obj1 = {
  name: "obj1",
  foo: function () {
    console.log(this.name);
  },
};
var obj2 = {
  name: "obj2",
  foo: () => {
    console.log(this.name);
  },
};
obj1.foo(); // obj1
obj2.foo(); // window
```

下面这个题目比较绕，但是还是抓住核心的几个点：

1. 箭头函数的this指向定义时的作用域，即指向外部作用域，而不是执行时的作用域

2. 函数内部匿名函数的this指向window

3. 

```javascript
var name = "window";
var obj1 = {
  name: "obj1",
  foo: function () {
    console.log(this.name);
    return function () {
      console.log(this.name);
    };
  },
};

var obj2 = {
  name: "obj2",
  foo: function () {
    console.log(this.name);
    return () => {
      // this为定义箭头函数时的作用域，即obj2
      console.log(this.name);
    };
  },
};

var obj3 = {
  name: "obj3",
  foo: () => {
    // 箭头函数为定义时的外层作用域，即window
    console.log(this.name);
    return function () {
      // 匿名函数，this指向window
      console.log(this.name);
    };
  },
};

var obj4 = {
  name: "obj4",
  foo: () => {
    // 箭头函数的this指向定义时的外层作用域，即window
    console.log(this.name);
    return () => {
      // 箭头函数this指向定义时的作用域，该函数定义时的作用域为window
      console.log(this.name);
    };
  },
};

obj1.foo()(); // obj1, window
obj2.foo()(); //obj2, obj2
obj3.foo()(); // window,window
obj4.foo()(); // window,window
```

```javascript
var name = "window";
function Person(name) {
  this.name = name;
  this.foo1 = function () {
    console.log(this.name);
  };
  // 箭头函数的外部作用域为Person
  this.foo2 = () => {
    console.log(this.name);
  };
}
var person2 = {
  name: "person2",
  foo2: () => {
    console.log(this.name);
  },
};
var person1 = new Person("person1");
person1.foo1(); // person1
person1.foo2(); // person1
person2.foo2(); // window
```