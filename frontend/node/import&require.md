### import & require

imoprt和require是现代前端模块化的模块导入方式。

import是ES6的语法，而require是CommonJS的语法。

**我们主要关注下这2种模块机制的一些区别:**

1. 加载实际的差异

- import在脚本的解析阶段(编译)进行静态分析，并且会被提升到模块的顶部。

    这种模块加载时机意味着在代码执行之前，javascript引擎就知道要加载哪些模块。这种静态分析特性使得模块之间的依赖关系更加易于分析，然后据此做一些优化，如tree-shaking就是利用这个特性来移除未使用的代码。

    ```ts
    console.log("11111");
    import { subtract } from "./math.js";
    console.log("222222");
    ```

    这种看起来import看起来在代码中间，但是在实际执行时，它会在代码执行之前就已经开始加载math.js模块了。

- requrie在脚本的执行阶段(运行)进行动态加载。
    
    这种模块加载时机意味着在代码执行到require这一行时，javascript引擎才会去加载模块。这种动态加载特性使得模块之间的依赖关系更加灵活，但是也可能导致一些性能问题，因为模块的加载是在代码执行时才进行的。
    
2. 模块作用域的差异

- import模块作用域

    import创建的模块是一个独立的作用域，模块内部的变量和函数不会自动添加到全局作用域中。每个模块都是一个独立的沙盒，模块内部的变量和函数默认都是私有的，只有通过export导出的模块才能被其他模块访问。

    ```js
    // module1.js
    let privateVariable = 10;
    export function getPrivateVariable() {
    return privateVariable;
    }
    ```

    另一个模块中:

    ```js
    // module2.js
    import { getPrivateVariable } from './module1.js';
    console.log(privateVariable); // 会报错，因为privateVariable没有被导出，不能在module2.js中访问
    console.log(getPrivateVariable()); // 输出10
    ```

    privateVariable不能在module2.js中访问，因为它没有被export导出，是1个独立的作用域。

- require模块作用域

    在Commonjs模块作用域内，如果模块内的变量和函数没有被正确的封装，那么就有可能被泄漏到全局作用域的风险。module.exports是向外暴露一个对象给外部，对象的属性可以在外部被修改。

3. 使用的环境差异

- import，主要针对ES Module模块，使用环境主要是浏览器

- require，主要针对CommonJS模块，使用环境主要是Node.js环境