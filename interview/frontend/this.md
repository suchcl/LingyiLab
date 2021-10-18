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