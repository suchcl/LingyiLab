<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. 简单了解模块](#1-%E7%AE%80%E5%8D%95%E4%BA%86%E8%A7%A3%E6%A8%A1%E5%9D%97)
- [2. commonjs模块](#2-commonjs%E6%A8%A1%E5%9D%97)
  - [2.1 module对象](#21-module%E5%AF%B9%E8%B1%A1)
  - [2.2 模块缓存](#22-%E6%A8%A1%E5%9D%97%E7%BC%93%E5%AD%98)
- [3. es6模块](#3-es6%E6%A8%A1%E5%9D%97)
  - [3.1 export](#31-export)
  - [3.2 import指令](#32-import%E6%8C%87%E4%BB%A4)
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

> Nodejs是CommonJs模块规范的一个具体实现。

#### 2.1 module对象

Node内部提供一个Module构建函数，所有模块都是Module的实例。

```js
function Module(id,parent){
    this.id = id;
    this.exports = {};
    this.parent = parent;
}
// ……
```
在每个模块内部，都有一个module对象，代表当前模块，它具有以下属性：

- module.id 模块标识符，通常是带有绝对路径的模块文件名

- module.filename 模块的文件名，带有绝对路径

- module.loaded 表示该模块是否已经加载完成，是一个布尔值

- module.parent 返回一个数组，表示调用该模块的模块

- module.children 返回一个数组，表示该模块要用到的其他模块

- module.exports 表示该模块对外输出的值

**module.exports属性表示当前模块对外输出的接口，其他文件加载该模块，实际上就是读取module.exports的变量**

为了方便，Node为每个模块提供一个exports变量，指向module.exports.这样就等同于在每个模块的头部，有一行这样的指令：

```js
const exports = module.exports;
```

> 不能直接将exports指向一个具体的值，因为这样就切断了exports和module.exports的联系。

如下面的写法，都是无效的：

```js
exports.hello = function () {
    return "How do you do?";
}

exports = "Hello world!";
```

> module.exports和exports使用的时候，有的时候会感觉到迷惑，最简单的方式就是不使用exports，我们的代码中不使用exports，在commonjs模块规范中，统一使用module.exports。

#### 2.2 模块缓存

第一次加载一个模块时，Node会缓存该模块，当以后再次加载该模块时，node就会直接从缓存中取该模块的module.exports属性。

```js
// base.js
const message = "success";
function hello() {
    return "How do you do?";
}

module.exports = {
    hello, message
};

// commonjs.js
const mb = require("./base");
const message = require("./base").message = "Hello world!";
const msg = require("./base").message; // msg会使用上面缓存的message值，而不是重新加载base模块而使用message属性值

console.log(mb.hello());
console.log(message); // Hello world!
console.log(mb.message); // Hello world!
console.log(msg); // Hello world!
```

commonjs.js中，有3处模块导入的地方，其中后两处的模块导入，都是导入的message属性

```js
const message = require("./base").message = "Hello world!";
const msg = require("./base").message; 
```
代码在执行的时候，会将第一次导入的message属性进行缓存，缓存的过程中对message属性重新赋值了，为“Hello world！”，但是下面又重新导入了message：const msg = require("./base").message;。

但是后面的导入，并不会去从base.js重新导入模块，而是从缓存中获取message属性，所以msg的值是Hello world!,而不是模块中定义的“success”。

> 缓存是根据绝对路径识别模块的，如果同样的模块名，但是保存在不同的路径，require是会重新加载模块的。

### 3. es6模块

ES6模块的设计思想就是尽量静态化，能够在编译阶段就能确定模块之间的依赖关系，以及输入和输出变量。CommonJs和AMD模块，只能在运行时才能够确认模块之间的依赖关系。如CommonJS模块规范的应用：

```js
// 如CommonJS规范中的
let { stat, exits, readFile } = require("fs");
// 等价于
let _fs = require("fs");
let stat = _fs.stat;
let exits = _fs.exits;
let readFile = _fs.readFile;
```

这个demo的本质是正题加载fs模块，就是加载fs模块的所有方法以及属性，生成一个_fs对象，然后再从这个_fs对象读取3个方法。这种加载称为运行时加载，因为只有在运行的时候才能得到这个对象，导致没有办法在源码的编译阶段做静态优化。

而ES6的模块不是对象，而是通过export指令显示指定输出的代码，再通过import导入。

```js
// es6模块
import { stat, exits, readFile } from "fs";
```

这段es6模块的实质是从fs模块加载3个方法，其他的不加载(fs模块也许就只有这3个方法，也许还有很多方法和属性)，这种加载方式称为“编译时加载”或者静态加载，即ES6可以再编译阶段就完成了模块的加载，效率要比CommonJS模块的加载方式要高。当然这种高效率的背后也有一些弊端，就是没有办法引用ES6模块本身，因为它不是一个对象，我们没有办法使用。

#### 3.1 export

ES6的模块功能主要由2个指令构成：export和import。export指令用于规定模块的对外接口，import指令用于导入其他模块。

- ES6模块必须且只能使用export导出；

- export必须于模块内部的变量建立一一对应的关系；

1. 一个模块就是一个独立的文件。该文件内部的所有变量，外部无法获取。如果我们希望外部能够使用模块内部的变量，就必须且只能使用export导出。

```js
export const firstName = "Nicholas";

export function add(x, y) {
    return x + y;
}
```

> export指令指定的是对外的接口，必须于模块内部的变量建立一一对应的关系。如上面的代码，也可以使用下面的方式导出：

```js
const firstName = "Nicholas";

function add(x, y) {
    return x + y;
}

export {
    firstName, add
};
```

export导出的，需要是一个变量，而不能是一个具体的值。如下面的导出方式是错误的：

```js
export "hello";
const msg = "hello";
export msg;
```

第一个导出，直接导出了一个值，是不允许的；

第二个导出，虽然导出了一个变量，但是变量msg指向的是hello，所以还是一个具体的值，也是不被允许的。

对于上述案例，可以通过如下方式进行导出：

```js
export const msg = "hello";
// 或者
const msg = "hello";
export {
    msg
};
```

es6中还可以通过别名的方式导出：

```js
const msg = "hello";
export { msg as message };
// 导入时通过message变量导入
import { message } from "./es6base.js";
console.log(message);
```

#### 3.2 import指令

- import指令导入的变量都是只读的，不能被修改； 

- import指令具有变量提升的效果；

- import是静态执行，所以不能使用变量和表达式；

- import语句是单例模式；

1. import指令导入的变量是只读的，不能被修改：因为import的本质就是一个导入接口，不允许在加载模块内部改变变量值

```js
let msg = "hello";
export { msg as message };

// 导入
import { message } from "./es6base.js";
message = "How are you?"; // 是不被允许的
```

demo中在导入后修改了import进来的变量，这是不被允许的。因为import导入变量，本质上是声明了一个常量，常量，是不允许修改值的。

上面的demo，message是一个变量，但是如果message是一个对象，那么这样的情况下，message本身不允许被修改，但是message对象的属性是可以被修改的。

```js
// m1.js
const person = {
    name: "Nicholas Zakas",
    age: 18
};

// es6.js
export { person };
import { person } from "./m1.js";
console.log(person); // {name: 'Nicholas Zakas', age: 18}
person.age = 16; // 修改了对象的属性值
console.log(person.age); // 16
```

> 通过import导入的对象，其属性值可以被修改，其他模块可以读取到修改后的属性值，但是这种写法有一个问题，就是如果出问题了不好纠错，问题不好排查，所以最好的实践是凡是通过import导入的变量，都默认为只读，不要轻易修改对象的属性。

**import指令具有提升效果，import指令语句会提升到整个模块的头部执行** 这是因为import指令是在编译阶段执行的，是在代码执行之前。

```js
console.log(addX(2, 3));
import { addX } from "./es6base.js";
```
比如上面的案例，是完全没有问题的，代码可以正常的执行，实际上在编译的时候，先编译了import指令语句，然后再去执行。

**import是静态执行，被import的部分不能是表达式和变量**

```js
// 这里不能导入表达式
import {"a" + "b"} from "modules";

// 这里不能从一个变量中导入数据
const myModule = "modules";
import { foo } from myModule;
```

**如果多次重复从一个语句中导入变量，那么只会执行一次导入动作，而不是多次**

```js
import { foo } from "module";
import { bar } from "module";
```

这里的两行导入语句，等价于：

```js
import { foo, bar } from "module";
```

> 上面的两条导入语句，foo和bar，但是是从同一个模块module中导入的，也就是说，import指令语句是单例模式。


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
