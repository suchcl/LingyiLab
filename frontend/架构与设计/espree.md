### espree解析器

参考文档:https://github.com/eslint/espree

espree是eslint使用的默认的解析器。

espree最初是EsprimV1.2.2的一个分支，这是在ES6发布之前Esprima发布的最后一个稳定版本。espree现在建立在Acorn之上，acorn也是一个解析器，具有模块化架构，允许扩展核心功能。espree的目标是通过类似API产生类似基于esprima的输出，以便可以代替esprima使用。