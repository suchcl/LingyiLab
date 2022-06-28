### Ts中的类型关键字：type

type是ts中的一个关键字，它的作用是给一个类型起一个新的名字。

type不会创建一个新的类型，它只是会给一个已经存在的类型起一个新的名字，也叫别名。

比如我国的一名非常有名的主持人尼格买提·热合曼，他的主持风格幽默，赢得了很多人的喜爱。我也很喜欢他的主持风格，但是他的名字，我念起来很绕口，不好记，那我就给他重新起个名字吧(有点起外号的感觉，哈哈)---小尼。好，以后，在我的世界里，小尼就是尼格买提·热合曼了。

ts中的type，就是起到了一个这样的作用，就是专门起别名的(起外号的)，有了类型别名，可以使代码书写起来更加简洁、易懂。

给如number、string、boolean等基本类型起别名在实际中是没有什么用处的，别名适合用于联合类型。

```ts
// 为string类型起个别名：Name
type Name = string;

// 为函数类型类型() => string起个别名NameResolve，定义一个返回string类型值的函数
type NameResolve = () => string;

// 定义个string或者返回string类型值的函数类型的联合类型
type NameOrResolver = Name | NameResolve;

// 定义1个返回Name类型值、形参为Name或者返回string类型值的函数
function getName(n: NameOrResolver): Name {
    if (typeof n === "string") {
        return n;
    } else {
        return n();
    }
}
```

demo中，最终定义的getName函数，可能接收1个Name(string)类型的参数，也可能接收一个返回string类型的函数。

但是如果传递给getName()函数一个其他类型的参数，ts编译器就会报错。

```ts
getName(12); // 这是ts编译器会给异常提示
```

![类型“number”的参数不能赋给类型“NameOrResolver”的参数](./images/i37.png)

> 类型别名，是给类型起一个新的名字。类型别名，有的时候和接口很像，但是可以用于原始值，联合类型、元祖以及其他任何自定义的类型。

