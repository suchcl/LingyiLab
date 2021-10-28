<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [作用域的理解](#作用域的理解)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 作用域的理解

作用域，我一般就是简单的理解为变量的可被访问的、有效的范围。

### 1. 作用域的分类

#### 1.1 全局作用域

全局，就是字面意思，如果是一个文件，那么这个变量就是在整个文件中都可被访问，如果是一个项目，那么这个变量就是在整个项目都是可见的，都是可以被访问的。这个全局作用域的生成时间，在文件被打开、被引用，或者项目被打开、被运行时作用域生效，文件关闭、结束引用，或者项目关闭了、停止运行了，作用域自动消失。

一般情况下，在函数外部定义的变量就是全局的变量，拥有全局的作用域；

window是浏览器项目的最顶级的全局对象，也就是说它是浏览器项目中js的最顶级的作用域，也就是说具有着全局的作用域；

```javascript
// 全局作用域
// 定义在了函数外面，是一个全局变量，具有全局的作用域
var username = "Hanmeimei";
function getUserName() {
    return username;
}
console.log(getUserName());
```

#### 1.2 函数作用域

函数作用域，属于这个函数的变量，可以在整个函数内使用及复用，而在函数外则不可以访问、调用；

外部无法访问封装在函数内部的变量；

```javascript
// 函数作用域
function fn() {
    var a = "12";
}
console.log(a); // Uncaught ReferenceError: a is not defined,a是在函数fn内部的，函数外部不可以调用
```

关于函数作用域，有2个小的知识点，需要记住:

1. 外部作用域无法访问封装在函数内部作用域中的变量；

2. 嵌套作用域，内部的作用域可以访问外部作用域中的内容

   ```javascript
   // 嵌套作用域，内部可以访问外部作用域中的变量
   function fn() {
       var a = 1;
       function inner() {
           var b = 2;
           // 内部作用域访问到了外部作用域中的变量a
           console.log(a);
       }
       inner();
       console.log(b); // object.js:104 Uncaught ReferenceError: b is not defined  虽然这是一个嵌套作用域，但是b是封装在函数内部的变量
   }
   fn();
   ```

#### 1.3 块级作用域

语句块，就是通过{}包裹起来的代码，就是一个块级作用域

块级作用域是在ES6标准新增的概念。

使用let、const声明的变量，都是块级作用域的。

```javascript
function fn() {
    var a = 1;
    if (true) {
        console.log(b);
        let b = 2; // Uncaught ReferenceError: Cannot access 'b' before initialization  变量b是通过let声明的，那么这个变量就直接绑定到这个区域，不再受外部的影响；如果b是通过var声明的，则会打印undefiend
    }
}
fn();
```

关于块级作用域、 通过let、const声明变量，有几点需要注意：

1. 同一个作用域内，只能声明一个变量；
2. const声明变量的同时要初始化值；
3. const声明的对象不可以修改，但是对象的属性可以修改值；
4. 没有变量提升，但是会发生暂时性死区现象；
