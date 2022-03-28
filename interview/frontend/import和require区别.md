<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. 简单了解模块](#1-%E7%AE%80%E5%8D%95%E4%BA%86%E8%A7%A3%E6%A8%A1%E5%9D%97)
- [2. commonjs模块](#2-commonjs%E6%A8%A1%E5%9D%97)
- [. require和import的区别](#-require%E5%92%8Cimport%E7%9A%84%E5%8C%BA%E5%88%AB)
- [import的优势](#import%E7%9A%84%E4%BC%98%E5%8A%BF)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 1. 简单了解模块

说到require和import的区别，其实更应该关注的是commonjs和es6模块机制的区别，而require和import只是commonjs和es6两种模块机制的具体的表现。

### 2. commonjs模块

Commonjs模块规范规定，每个模块内部，module变量代表当前模块。这个变量是1个对象，它的exports属性(即module.exports)是对外的接口，加载某个模块，其实就是加载该模块的exports属性(module.exports)。

```js
// m1.js
const x = 5;
const addX = (value) => {
    return value + x;
}
const y = 12;
const del = (value) => {
    return value - y;
}
```

如上述代码在m1.js文件中，那么m1.js文件本身就是一个js模块，这个模块中有一些变量和函数。那么在commonjs模块规范下，可以通过module.exports暴露接口(暴露接口，就是指暴露变量、方法名等，让模块外部可以访问某个模块内部的这些属性和方法)。如我想暴露m1.js这个模块中的变量和方法，通过module.exports关键字。

```js
const x = 5;
const addX = (value) => {
    return value + x;
}
const y = 12;
const del = (value) => {
    return value - y;
}
// 通过module.exports暴露了变量x和函数addX
module.exports.x = x;
module.exports.addX = addX;
```

上面案例中，暴露接口的时候，是各个数据逐一暴露的，也可以统一暴露，如：

```js
// 统一、集中暴露接口
module.exports = {x,addX,y,del};
```

假如在common.js文件中调用m1模块：

```js
// common.js
const baseModule = require("./m1"); // 定义一个变量来接收m1模块
console.log("baseModule.x:", baseModule.x); // 通过模块变量来调用m1模块中的数据，包括变量和方法
console.log("baseModule.addX:", baseModule.addX(12));
console.log("baseModule.y", baseModule.y);
console.log("baseModule.del:", baseModule.del(20));
```

> 上面模块导出，我们应该注意到导出的模块名称和模块中定义的变量名和函数名是相同的，其实这里面隐藏了一个知识点。就是导出的模块名称不是必须和模块内定义的变量和函数同名，只是在大多数的实践中是相同的。这里隐藏的知识点是ES6中，属性值可以是一个变量。当属性和属性值变量同名的时候，那么可以省略属性值变量，如:

```js
const name = "Nicholas Zakas";
const person = {
    name
};
```

person对象有一个属性name，并且属性值是name，具体为“Nicholas Zakas”，这行的代码等价于：

```js
const person = {
    name: name
};
```

回到正题，commonjs模块规范中，导出的模块内的接口名称可以不用和定义的接口同名，如

```js
const x = 5;
const addX = (value) => {
    return value + x;
}
const y = 12;
const del = (value) => {
    return value - y;
}
module.exports = {
    a: x,
    b: y,
    jian: del,
    jia: addX
};
```

那么在调用的时候，也是以定义的导出的模块接口为准，如

```js
const baseModule = require("./base");
console.log("baseModule.a: ", baseModule.a);
console.log("baseModule.b: ", baseModule.b);
console.log("baseModule.jia: ", baseModule.jia(12));
console.log("baseModule.jian: ", baseModule.jian(30));
```

**CommonJs模块规范，有以下的一些特点**

- 所有代码都在当前作用域下有效，不会污染全局作用域；

- 模块可以被多次加载，但是只是在第一次加载时运行一次，之后运行结果被缓存，以后再次加载的时候，直接读取缓存；如果希望模块再次运行，则需要清空缓存再次执行；

- 模块的加载顺序，按照其在代码中出现的先后顺序；

### . require和import的区别

**requrie/exports输出的是一个值的拷贝，import/export模块输出的是值的引用；**

require/exports输出的是一个值的拷贝，也就是说，一旦输出一个值，模块内部的变化就影响不到这个值；

import/export模块输出的是值的引用：js引擎对脚本静态分析的时候，遇到模块加载命令import会生成一个只读的引用。等到脚本真正执行时，再根据这个只读引用，到具体的模块中去取值。

**import/export只能在模块顶层使用，不能在函数、判断语句等代码块中应用；require和exports则可以**

import/export是在代码编译时加载，所以必须放在文件开头的地方；require/exprts在代码运行时被加载，在理论上可以放在任何地方；所以<font color="#f20">在性能上，import更优</font>；

**import引入的对象被修改时，源对象也会被修改，相当于浅拷贝；require引入的对象被修改时，源对象不会被修改，可以称为值拷贝，也可以理解为深拷贝**

**配合webpack，import会触发代码分割，把代码分离、编译到不同的bundle中，以实现按需加载或者并行加载；require不会实现代码分割：import在性能上的操作更优**

**import/export导出的模块默认采用严格模式；require/exports导出默认不使用严格模式**

### import的优势

1. 可以实现代码分割（配合webpack），将代码打包到不同的bundle中，可以实现文件、代码的按需加载；require不行；

2. import静态引入，代码编译时就已经已经确定了代码、文件之间的相互关系，require动态编译，只有在代码运行时才会确认代码、文件之间的彼此关系；性能上import更优；
