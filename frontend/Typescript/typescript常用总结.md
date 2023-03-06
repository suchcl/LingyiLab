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

```ts
interface IUser {
    name: string;
    age: number;
    salary?: number;
}

type User = {
    name: string;
    age: number;
    salary?: number;
};
```

2. 区别

interface是声明一个新的类型，但是如果使用interface声明了同名的类型会自动合并。如：

```ts
interface IUser {
    name: string;
    age: number;
    salary?: number;
}

interface IUser {
    gender: string;
}

const uesr:IUser = {
    name: 'Nicholas Zakas',
    age: 12,
    gender: '男'
}
```

声明了两个IUser接口，

> 熟悉java的朋友一定要注意，ts中的接口和java中的接口意义不同，java中的接口定义了一系列方法，是一系列方法特征的集合，但是并没有去实现。ts中的接口，可以理解为定义了一个新的数据类型。如ts中的内置的数据类型number、string、boolean等数据类型一样，interface定义了新的数据类型。

从上面1可以看出，type是对一个已经存在的类型重新起了个名字而已。如本来就有一个类型:

```ts
{
    name: string;
    age: number;
    salary?: number;
};
```

只是这个类型呢，没有名字，使用的时候如果直接使用这个类型不方便，那么type就给这个已经存在的类型重新起了个名字叫User，那么再使用这个类型的时候就可以直接使用User，有了变量使用就会方便了很多。

这就是type的作用。

#### 1.3 数组类型

可以说数组类型是客户端开发中使用的最为广泛的数据类型。

数组类型，有两种类型声明方式：

1. 在基础数据类型后面添加[]表示该类型的数组

```ts
const numArry: number[] = [1, 2, 3];
```

2. 使用数组泛型的方式声明数组

```ts
const numList: Array<number> = [4, 5, 6];
```

案例都是使用语言内置的数据类型创建的数组，在日常的开发中也可以使用自定义的类型定义数组。

```ts
interface INewUser {
    name: string;
    age: number;
}

const userList: INewUser[] = [
    {
        name: "Nicholas Zakas",
        age: 16
    },
    {
        name: "HcySunYang",
        age: 22
    }
];
```

通过自定义的数据类型INewUser，以及在类型后面添加[]的方式创建了一个数组。

自定义的数据类型，也可以通过数组泛型的方式定义数组:

```ts
interface INewUser {
    name: string;
    age: number;
}

const userList: Array<INewUser> = [
    {
        name: "Nicholas Zakas",
        age: 16
    },
    {
        name: "HcySunYang",
        age: 22
    }
];
```

可以发现，使用自定义类型创建数组，和使用内置类型创建数组的方式完全一致，可以使用数组泛型，也可以使用在类型后面添加[]d的方式。

### class

### declare