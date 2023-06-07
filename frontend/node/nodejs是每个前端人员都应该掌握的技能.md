参考链接:https://juejin.cn/post/7241526172165423163

作为一名web开发人员，如果正在因为网站的响应速度慢而烦恼，那么请了解下Nodej.js。

Node.js是一个基于Chrome V8引擎的Javascript运行时环境，作为一个快速、高效、易于使用的服务端运行环境，已经成为Web开发的不二选择。Node.js可以帮助我们在编写应用程序时轻松实现高效的I/O操作和数据传输，同时还能让我们在运行时处理海量数据而不会出现阻塞。

### 模块系统

Node.js使用基于CommonJs规范的模块系统来将代组织为可重用的、独立的组件，在Node.js中，每个文件都是一个独立的模块，每个文件都被视为一个模块，如果想在一个文件中使用其他模块，可以使用requrie()函数将其他模块导入。

```js
// 导入node内置模块
const http = require("http");

// 导入自定义模块,并调用自定义模块中的方法
var util = require("../utils/util.js");
const token = util.encryptStringWithSalt(str, salt);
```

### HTTP模块