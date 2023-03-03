参考链接:https://juejin.cn/post/6981728323051192357

### 1. 数据类型相关

学习任何一门编程语言，一般都会先从学习数据类型开始，ts也不例外。

#### 1.1 基础数据类型

常用的类型有: boolean、number、string、array、enum、any、void

不常用的类型: tuple、null、undefined、never

ts的优势就是类型约束，在ts中变量的声明都要使用类型约束，否则就和js一样了

> 当然了，现在浏览器还不能直接运行ts，ts最终也是被编译成js后在浏览器中执行的。但是如果没有类型约束那么就失去了ts的优势了。

```ts
const num:number = 12;
function getUserInfo(name:string,age:number):void{
    // 逻辑处理
}
```

变量的声明可以使用类型约束，函数的声明，也可以使用类型约束。函数如果没有使用类型约束，则默认为void。

#### 1.2 对象类型

对象类型，这里不介绍什么是对象、怎么声明对象，主要总结下ts中怎么声明自定义对象类型数据。

ts中，声明对象使用类型约束，一般不会使用、也没有现成的对象类型可用，如果有的话，那应该也是其他团队成员定义过了。一般请看下，都是需要我们自己定义对象类型的。ts可以通过interface和type声明、定义自定义的类型。

**interface和type的异同点**

1. 相同点

interface和type都可以声明自定义的类型

2. 区别

interface是声明一个新的类型，但是如果使用interface声明了同名的类型会自动合并。

### class

### declare