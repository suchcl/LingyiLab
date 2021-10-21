### require和import的区别

**requrie/exports输出的是一个值的拷贝，import/export模块输出的是值的引用；**

require/exports输出的是一个值的拷贝，也就是说，一旦输出一个值，模块内部的变化就影响不到这个值；

import/export模块输出的是值的引用：js引擎对脚本静态分析的时候，遇到模块加载命令import会生成一个只读的引用。等到脚本真正执行时，再根据这个只读引用，到具体的模块中去取值。

**import/export只能在模块顶层使用，不能在函数、判断语句等代码块中应用；require和exports则可以**

import/export是在代码编译时加载，所以必须放在文件开头的地方；require/exprts在代码运行时被加载，在理论上可以放在任何地方；所以<font color="#f20">在性能上，import更优</font>；

**import/export导出的模块默认采用严格模式；require/exports导出默认不使用严格模式**


https://cloud.tencent.com/developer/article/1611197
