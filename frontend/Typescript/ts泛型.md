参考链接:https://juejin.cn/post/7212622837063385125?

泛型有什么用？

### 1. 泛型处理函数参数

定义函数的时候不决定参数的类型，而是让调用者使用尖括号<>的方式传入对应的类型。

比如我们要实现一个函数，输入一个参数并返回它，要求保证参数和函数返回值类型一致。

```ts
function fn<Type>(args: Type): Type {
    return args;
}

console.log(fn<'hello'>("hello"));
```

泛型的语法是<>里面写类型参数，一般可使用T来表示。

> 类型参数经常会使用T、E、K、V、O，这些都是自定义的，可以任意修改，只是这几个使用的比较多，默认代码表了一些意义。

T: Type，类型

K: key

V: value

E: element，元素

O: Object,对象

<font color="#f20">这几个占位符只是使用的多一些而已，可以自定义，自己在编码的时候可以自定义。</font>

```ts
function print<T>(args: T): T {
    return args;
}
```
demo定义了一个函数，T是一个占位的类型变量，args是T类型，函数的返回值类型也是T类型。那么T究竟是一个什么类型呢？在函数定义阶段，我们并不知道T究竟是什么类型，而是在调用的时候，由调用者确定T到底是什么类型.

```ts
function print<T>(args: T): T {
    return args;
}
print<string>("hello"); // 函数调用方决定了函数定义时的T是string。
print<12>(12); // 调用时决定了T是一个数字字面量类型12
```

**泛型传入多个类型参数**

函数定义的时候，也可以传递多个类型参数 --- 我习惯把占位的<>里面的参数称为类型参数。

```ts
function fn2<T,E>(t:T,e:E):void{
    console.log(t,e);
}
fn2<string,number>("hello", 12); // hello, 12
```

### 2. 泛型接口

### 3. 泛型类

### 4. 泛型约束