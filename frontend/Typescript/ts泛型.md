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

泛型接口是一种具有泛型类型参数的接口，它可以在接口的定义中使用这些参数，从而使得接口的属性和方法能够适用于多种类型。

1. 接口定义的时候使用泛型

```ts
interface IPerson<T> {
    name: T;
    friends: T[];
    sayHi: (msg: T) => void;
}

const p: IPerson<string> = {
    name: "Nicholas Zakas",
    friends: ["Dave Herman"],
    sayHi: (msg) => {
        console.log(msg);
    }
};
```

demo中定义了一个接口IPerson，并为接口指定了一个类型参数T,在接口内声明的属性都使用到了这个类型参数。这个类型参数究竟是什么类型，在接口定义的时候不确定，在接口被调用的时候由调用者指定。案例中调用时指定了类型参数为string。

2. 指定类型的默认值

在定义泛型接口时，也可以像定义函数一样，参数也可以有默认值，那么定义泛型接口时参数类型也可以有默认值

```ts
interface IPerson<T = string> {
    name: T;
    friends: T[];
    sayHi: (msg: T) => void;
}

const p: IPerson<number> = {
    name: 12,
    friends: [1, 2, 3],
    sayHi: (msg) => {
        console.log(msg);
    }
};

const p2: IPerson = {
    name: "Nicholas Zakas",
    friends: ["Dave Herman"],
    sayHi: (msg) => {
        console.log();
    }
};
```
案例在定义泛型接口的时候，指定了一个默认的类型，但是在实际使用到这个接口进行类型约束的时候，如果没有显示指定类型，则使用默认的类型参数string，如p2；如果使用泛型接口时显示指定了类型参数，则使用指定的类型参数，如p。

### 3. 泛型类

泛型类，是一种具有泛型类型约束的类，泛型类可以在类定义的时候使用这些类型参数，从而使得类的属性和方法能够适用于多种类型。

```ts
class Point<T>{
    x: T;
    y: T;
    constructor(x: T, y: T) {
        this.x = x;
        this.y = y;
    }
}

const p0 = new Point(3, 4);
const p1 = new Point<number>(2, 3);
const p4:Point<number> = new Point(2,5);
```

### 4. 泛型约束

#### 4.1 泛型中使用extends 

extends和泛型结合，可解决固定参数类型传递的需求

```ts
interface Person {
    name: string;
}

// 这里类型参数T继承了Person类型，那么T就继承了Person的所有属性，且参数person是T类型，那么函数参数person的类型只要有name属性就可以了，其他属性也可以自定义
function getName<T extends Person>(person: T) {
    return person.name;
}

// 调用中，函数getName()的参数实现了继承自Person的属性name，且也实现了自定义属性age
// name是必须的，age是可选的
getName({
    name: "Dave Herman",
    age: 12
});
```

在实际业务代码中，我们经常需要使用一个属性，但是编译器老提示我们没有这个属性，但是实际上呢是有的，比如我们获取某个数据的length属性的时候，如果参数是数组、字符串或者具有length属性的对象的时候。这个时候我们可以通过泛型继承的方式来规避表编译器对我们代码的异常信息提示.

```ts
interface ILength {
    length: number;
}

function getLength<T extends ILength>(args: T) {
    return args.length;
}

getLength<string>("hello");
getLength({
    name: "Dave Herman",
    age: 12,
    length: 3
});

getLength(['hello', 123]);

interface IUser {
    name: string;
    age: number;
}
getLength<IUser[]>([
    {
        name: "Nicholas Zakas",
        age: 18
    },
    {
        name: "Dave Herman",
        age: 21
    }
]);
```

#### 4.2 泛型中使用keyof



#### 4.3 泛型中使用extends和keyof