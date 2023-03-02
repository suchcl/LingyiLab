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



### class

### declare