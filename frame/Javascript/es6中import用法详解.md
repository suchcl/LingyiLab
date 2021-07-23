### 简单认识ES6中的模块

在ES6之前，javascript中一直都没有模块的概念，那么在没有原生的js模块之前，在开发者社区制定了一些模块化方案，最具有代表性的有CommonJs和AMD两种方案。CommonJs方案用于服务器，AMD用于浏览器端。

CommonJs是为在浏览器环境之外构建Javascript应用而构建的一套规范，主要是为了解决Javascript的作用域问题而定义的模块形式，可以使每个模块在它自己的命名空间中执行，该规范的主要内容是模块之间必须通过module.exports导出对外的变量或者接口，通过require()来导入其他模块的输出到当前模块的作用域中。当前Nodejs遵循的是Commonjs规范。

CommonJs对模块的加载是同步执行的。

AMD是在ES6标准之前为浏览器端项目js的表现制定的一套规范，AMD是Asynchronous Module Definition的缩写，就是异步模块定义，采用的是异步的方式进行模块的加载，在加载模块的时候不影响后续模块语句的运行。

ES6标准，子啊语言标准的层面上，实现了模块功能，且实现的相对简单，可以替代CommonJs和AMD规范，成为浏览器和服务器端通用的模块化方案。

ES6标准的模块化，其设计思想是尽量的静态化，期望在代码编译时就能确定模块之间的依赖关系，以及输入和输出的变量。CommonJs和AMD的模块化思想是动态的，模块之间的依赖关系只有在代码运行的时候才能确定。

<font color="#f00">ES6标准模块自动采用严格模式，无论文件是否声明"use strict";</font>Js的严格模式有以下一些特点：

1. 变量必须先声明后使用；
2. 函数的参数不能有同名属性，否则报错；
3. 不能使用with语句；
4. 不能对只读属性赋值，否则报错；
5. 不能使用前缀0表示八进制数，否则报错；
6. 不能删除不可删除的属性，否则报错；
7. 不能删除变量delete props，会报错，只能删除属性 delete global[prop];
8. eval不会在它的外层作用域引入变量；
9. eval和arguments不能被重新赋值；
10. arguments不会自动反映函数参数的变化；
11. 不能使用arguments.callee；
12. 不能使用arguments.caller；
13. 禁止使用this指向全局对象；
14. 不能使用fn.caller和fn.arguments获取函数调用的堆栈；
15. 增加了保留字，如static、interface、protected等；

<b>简单总结下模块化</b>

1. CommonJS模块化思想，主要用在服务端，也可以用在浏览器端，同步执行；
2. AMD模块化思想，主要用在浏览器端，模块异步加载；
3. ES6标准的模块化思想，涵盖了CommonJs和AMD的所有优势，可以同时用在服务器端和浏览器端；其模块化思想是尽可能静态化；自动采用严格模式；

### import {} 和 import variable