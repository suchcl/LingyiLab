<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Ts中的类型关键字：type](#ts%E4%B8%AD%E7%9A%84%E7%B1%BB%E5%9E%8B%E5%85%B3%E9%94%AE%E5%AD%97type)
- [接口(interface)和类型别名(type)的相同点](#%E6%8E%A5%E5%8F%A3interface%E5%92%8C%E7%B1%BB%E5%9E%8B%E5%88%AB%E5%90%8Dtype%E7%9A%84%E7%9B%B8%E5%90%8C%E7%82%B9)
- [接口(interface)和类型别名(type)的不同点](#%E6%8E%A5%E5%8F%A3interface%E5%92%8C%E7%B1%BB%E5%9E%8B%E5%88%AB%E5%90%8Dtype%E7%9A%84%E4%B8%8D%E5%90%8C%E7%82%B9)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

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

```ts
type Name = string;
type Person = {
    name: Name
};
type Student = Person & { grade: number };
type Teacher = Person & { major: string };
type StudentAndTeacherList = [Student, Teacher];
const list: StudentAndTeacherList = [
    {
        name: "Nicholas Zakas",
        grade: 2
    },
    {
        name: "谭浩强",
        major: "Computer Science"
    }
];
```

### 接口(interface)和类型别名(type)的相同点

1. 接口和类型别名，都可以用来描述对象的约束和函数签名

```ts
// 描述对象类型
interface Points {
    x: number;
    y: number;
}

// 描述函数
interface SetPoints {
    (x: number, y: number): void;
}

// 类型别名来描述对象类型
type Points2 = {
    x: number;
    y: number
}
// 类型别名描述函数约束
type SetPoints2 = (x: number, y: number) => void;
```

2. 扩展和实现(extends & implements)

接口可以通过extends继承另外一个接口，类型别名没有继承的概念，但是可以通过联合类型、交叉类型来达到同样的效果。

### 接口(interface)和类型别名(type)的不同点

1. 接口可以被声明多次，虽然声明多次，但是被视为单个接口——接口合并了；类型别名不可以；

2.type可以使用in关键字生成映射类型，interface不行

```ts
type Keys = "name" | "sex"

type DulKey = {
    [key in Keys]: string    // 类似for...in
}

let stu: DulKey = {
    name: "wang",
    sex: "man"
}
```