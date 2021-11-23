### js 和 ts 有什么区别？在做技术选型的时候会基于什么因素考虑使用这些语言？

typescript 是 javascript 的超级，其本质是在 javascript 的基础上添加了可选的静态类型和基于类的面向对象编程。

Typescript 有这样的一些能力、特点：

- 解决大型项目的代码复杂性；

- 可以在编译期间发现一些语法的阴性错误

- 支持强类型、接口、模块、泛型

我的一个项目中使用到了 typescript，当时有 2 个原因：

1. 就是想探索、尝试项目中引入 ts。当时了解了 ts 的优势，了解、调研的差不多了，就想找个项目实践一下。正好就有个新项目，就想让这个项目成为 ts 使用探索和使用的示范，推进技术升级的标杆；

2. ts 确实有一些 javascript 在技术上所不具备的优势：

   1. 强类型：规范项目中的变量声明、可控可预知，减少由于开发人员的疏忽以及语法的问题；

   2. 接口：接口，其实也就是定义了一些数据结构，有一定的规范数据结构的作用；

   3. 继承：避免实现一些重复的功能，减少开发成本，也可以提升代码的可维护性；