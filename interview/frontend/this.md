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