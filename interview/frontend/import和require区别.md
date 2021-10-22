### require和import的区别

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
