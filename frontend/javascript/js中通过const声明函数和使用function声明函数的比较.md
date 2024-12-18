### js中通过const声明函数和直接使用function声明函数，哪个更好?

js中，常用两种方式去声明函数：使用function关键字和const常量的方式去声明一个函数。

#### 1. 函数声明方式

- 语法特点

使用function关键字声明函数如function add(a,b){return a + b;}这种方式，可以在代码执行之前进行函数声明提升，意味着可以在函数声明之前被调用；

```js
console.log('%c [ add(2,3) ]-75', 'font-size:13px; background:pink; color:#bf2c9f;', add(2,3)); // 正常打印出来了5
function add(a,b){
    return a + b;
}
```

上述代码是可以被正常执行的，因为js引擎在执行代码时会先扫描函数声明，将函数声明提升到当前作用域的顶部。

- 适用场景

    - 需要在代码的不同位置去调用函数，并且希望函数声明在整个作用域内都可见时，这种方案合适。如在一个包含多个函数的模块中，一些函数可能会存在相互调用，使用function来声明函数可以保证它们在合适的作用域内被正确的调用，而不需要担心函数的定义顺序的问题

    - 对于传统的js编程风格，尤其是在一些老的代码库中或者简单的脚本中，函数的声明方式更为常见

> function关键字声明函数的方式，虽然可以提升函数的定义，但是也会引起代码的混乱。js虽然提供了这种能力，但是个人不怎么推荐，更合理的是根据引入、定义顺序去按需引用，便于管理，更加安全。

#### 2. 常量(const)声明方式

- 语法特点

适用const关键字声明函数时，相当于定义了一个常量引用，该引用指向了一个函数表达式，如const add = function(a,b){return a + b;}。这种方式不存在函数声明的提升，函数必须要在函数定义之后才能调用。否则会报异常，提示不能在函数声明之前调用.

```js
console.log('%c [ subtraction(5,2) ]-80', 'font-size:13px; background:pink; color:#bf2c9f;', subtraction(5,2));
const subtraction = function(a,b){
    return a - b;
}
```

如期的抱了异常：

```bash
ReferenceError: Cannot access 'subtraction' before initialization
    at file:///react/src/pages/test/test.js:80:94
    at ModuleJob.run (node:internal/modules/esm/module_job:194:25)
```

- 适用场景

    - 在现代的js编程中，特别是在使用模块(如ES6模块)时，const方式声明函数，更为常用。因为莫块具有自己的作用域，并且代码的执行顺序有严格的限制，函数声明提升的优势不那么必要

    - 当希望确保函数引用不被意外修改时，const声明函数是很好的选择。如在一个函数式的编程场景中，函数作为参数传递或者返回时，使用const可以保证函数的稳定性和可预测性

总体来说，function和const没有绝对的说哪种声明方式更好。在传统的js代码中或者需要提升函数声明时，使用function更能够满足需求；在现代的js编程、模块系统以及注重函数稳定性的场景中，使用const来声明函数更加具有优势。