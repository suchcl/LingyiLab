<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. interface和type](#1-interface%E5%92%8Ctype)
  - [1.1 基本是用](#11-%E5%9F%BA%E6%9C%AC%E6%98%AF%E7%94%A8)
  - [1.2 interface和type的区别](#12-interface%E5%92%8Ctype%E7%9A%84%E5%8C%BA%E5%88%AB)
  - [1.3 索引签名](#13-%E7%B4%A2%E5%BC%95%E7%AD%BE%E5%90%8D)
  - [1.4 接口继承](#14-%E6%8E%A5%E5%8F%A3%E7%BB%A7%E6%89%BF)
  - [1.5 接口实现](#15-%E6%8E%A5%E5%8F%A3%E5%AE%9E%E7%8E%B0)
- [2. 函数](#2-%E5%87%BD%E6%95%B0)
  - [2.1 基本使用](#21-%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8)
  - [2.2 调用签名](#22-%E8%B0%83%E7%94%A8%E7%AD%BE%E5%90%8D)
  - [2.3 构造签名](#23-%E6%9E%84%E9%80%A0%E7%AD%BE%E5%90%8D)
  - [2.4 this](#24-this)
- [3. 联合类型、交叉类型、函数重载](#3-%E8%81%94%E5%90%88%E7%B1%BB%E5%9E%8B%E4%BA%A4%E5%8F%89%E7%B1%BB%E5%9E%8B%E5%87%BD%E6%95%B0%E9%87%8D%E8%BD%BD)
  - [3.1 联合类型和重载](#31-%E8%81%94%E5%90%88%E7%B1%BB%E5%9E%8B%E5%92%8C%E9%87%8D%E8%BD%BD)
- [4. 类型、非空、常量断言](#4-%E7%B1%BB%E5%9E%8B%E9%9D%9E%E7%A9%BA%E5%B8%B8%E9%87%8F%E6%96%AD%E8%A8%80)
- [5. 字面量类型](#5-%E5%AD%97%E9%9D%A2%E9%87%8F%E7%B1%BB%E5%9E%8B)
- [6. 字面量推理](#6-%E5%AD%97%E9%9D%A2%E9%87%8F%E6%8E%A8%E7%90%86)
- [7. 类型收窄(Type Narrowing)](#7-%E7%B1%BB%E5%9E%8B%E6%94%B6%E7%AA%84type-narrowing)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

参考链接:https://juejin.cn/post/7210369671664582711
### 1. interface和type

#### 1.1 基本是用

interface定义新的接口类型，使用type定义已经存在的类型的别名

都可以约束对象类型的结构

因为type是对已经存在的类型定义别名，所以在使用type的时候需要使用=进行赋值，而interface不需要

```ts
interface IPoint {
    x: number;
    y: number;
    z?: number; // ?代表可选
}

type TPoint = {
    x: number;
    y: number;
    readonly z?: number;
}
```

#### 1.2 interface和type的区别

| interface                  | type                                                     |
| -------------------------- | -------------------------------------------------------- |
| 只描述对象                 | 可以描述所有数据，基础类型和对象都可以                   |
| 使用extends来实现继承      | 通过&来实现交叉类型                                      |
| 创建新的类型名             | 只是给一个已经存在的类型起一个新的名字，不会创建新的类型 |
| 可以重复声明同一个类型名称 | 别名不能重复                                             |

总的来说，就是type可约束的范围比interface要更广，但是在实践中，能使用interface的地方就尽量使用interface，否则再去使用type。

#### 1.3 索引签名

```ts
// 表示对象中满足key为number、值为string即可，k可被替换为任意单词
interface IP {
    [k: number]: string;
}
```

type也可以实现同样的能力

```ts
type TP = Record<number, string>;
```

Demo:

```ts
const ic: IP = {
    0: "javascript",
    1: "php"
};
const tp: TP = {
    0: "javascript",
    1: "php"
};
```

#### 1.4 接口继承

接口和类相同，都是用extends关键词实现继承

接口的继承是多继承，类是单继承

```ts
interface Animal {
    running: () => void;
}

interface Person {
    name: string;
    age: number;
}

// 声明已经存在的类型，直接扩充原类型的属性
interface Person {
    gender: string;
}

// 通过extends继承类型
interface IStudent extends Person, Animal {
    id: number;
}

const stu: IStudent = {
    name: "Have Herman",
    age: 12,
    gender: "male",
    id: 123,
    running: () => {
        
    },
};
```

#### 1.5 接口实现

定义的接口可以被类实现

之后如果有需要传入接口的地方，同样也可以将类实例传入

这就是所谓的面向接口开发

```ts
interface IRun {
    running: () => void;
}

interface IEating {
    eating: () => void;
}

class Person implements IRun, IEating {
    running() {
        console.log("running");
    };
    eating() {
        console.log("eating");
    };
}

function run(runner: IRun) {
    runner.running();
}

const p = new Person();
run(p);
p.eating();
```

### 2. 函数

#### 2.1 基本使用

ts中函数声明和实现分离写法

**利用type声明函数**

```ts
type F1 = (a: number, b: number) => number;
```

**利用interface声明函数**

```ts
interface F1 {
    (a: number, b: number): number
}
```

函数实现

无论是使用type声明函数，还是通过interface声明函数，都可以通过箭头函数和函数表达式的方式实现函数，但是不能使用函数声明的方式实现函数。

```ts
// 箭头函数方式实现函数
const f1: F1 = (a, b) => a + b;

// 函数表达式的方式实现函数
const f2: F1 = function (a, b) {
    return a + b;
}
```

#### 2.2 调用签名

在通过interface声明函数的时候，也可以为函数声明自己的属性

```ts
interface FunctionWithAttrs {
    username: string;
    (msg: string): void
}

const fn4: FunctionWithAttrs = msg => {
    console.log(msg);
}
fn4.username = "Nicholas Zakas";
```

#### 2.3 构造签名

#### 2.4 this

### 3. 联合类型、交叉类型、函数重载

#### 3.1 联合类型和重载



### 4. 类型、非空、常量断言

断言，就是ts不知道一些必要信息，然后在编码过程中通过一些技术手段告诉编译器它想或者应该知道的一些信息。

**类型断言**

类型断言，就是当ts不知道或者没有办法获取到具体的类型时，就使用类型断言，告诉ts当前时什么具体的类型。

类型断言，有两种方式：尖括号方式和as语法方式。

尖括号方式：

```ts
let str:any = "hello";
let strLength = <string>str.length;
```
> 尖括号方式不能应用在jsx、tsx中

as语法

```ts
let str:any = "hello";
let strLen = (str as string).length
```

由于两种方式都可以实现类型断言，但是尖括号方式不能应用在jsx、tsx中，as语法的方式更灵活，也不需要记什么场景，可以简单只记住as语法就可以了。

**非空断言**

非空断言操作符：!。ts中特有的，js中没有该操作符。

!操作符，可以用于断言当前操作数不是null和undefined。

```ts
function getMessage(msg: string | undefined){
    let newMsg:string = msg;
    console.log(newMsg);
}
```

直接这么看这个代码，从视觉上是看不出有什么问题的，看截图：

![赋值类型错误](./images/i1.png)

提示是不能将undefined类型值赋值给一个string类型的变量。回到代码中，getMessage函数参数msg是一个联合联合类型，可能是string类型也可能是undefined，但newMsg是在函数内定义的变量，且类型是确定的string类型，所以在赋值的时候将一个不确定的类型值赋值给一个确定类型的变量，ts编译器就报错了。那么怎么解决呢？

```ts
// 通过类型收窄的方式
function getMessage(msg: string | undefined){
    let newMsg:string;

    // 下面两种收窄方式都可以，目的都是排除掉undefined值
    if(typeof msg === "string"){
        newMsg = msg;
    }

    // if(msg){
    //     newMsg = msg;
    // }
    console.log(newMsg);
}
```

也可以直接通过非空断言的方式解决:

```ts
function getMessage(msg: string | undefined){
    let newMsg:string = msg!;
    console.log(newMsg);
}
```

[非空断言操作符也可参考](../%E9%9D%9E%E7%A9%BA%E6%96%AD%E8%A8%80%E6%93%8D%E4%BD%9C%E7%AC%A6.md)

**常量断言**

通过as coust将一个基本数据类型收窄到一个字面量类型，或者也可以理解将当前变量变成了常量；

```ts
let uname = "Nicholas Zakas" as const;  // 通过as const，uname已经是一个字面量类型了，其类型值为Nicholas Zakas，也只能有这么一个确认的值，不能再为变量uname赋其他的值
uname = "Dave Herman"; // 报错，不能为一个Nicholas Zakas类型值赋一个Dave Herman类型
```

![常量断言基本数据类型](./images/i2.png)

如果as const断言一个数组，那么数组会被收窄为一个只读属性的数组，不能再对该数组添加、移除元素

```ts
const userArr = ["Nicholas Zakas", "Dave Herman"] as const;
userArr.push("");
```

![常量断言数组，数组变为readonly](./images/i3.png)

如果as const断言一个对象，那么会对对象的每个属性都添加上readonly，变为只读属性

```ts
const userObj = {
    name: "Dave Herman",
    age: 12
} as const;

userObj.name = "";
```

![常量断言对象，为对象的每个属性都添加reasonly属性](./images/i4.png)

![常量断言对象后就不能再对对象属性重新赋值](./images/i5.png)

### 5. 字面量类型

字面量类型，可以参考: [ts中的字面量类型](../ts%E4%B8%AD%E7%9A%84%E5%AD%97%E9%9D%A2%E9%87%8F%E7%B1%BB%E5%9E%8B.md)

简单来说，就是一些常量用来做ts的类型。字面量类型，大多场景是用来联合类型

```ts
let msg: 'hello' = 'hello';
type Direction = 'left' | 'right';
const d:Direction = 'left'; // Direction类型的d的值，只有2个合法的值，left和right
```

### 6. 字面量推理

这个没有搞懂

### 7. 类型收窄(Type Narrowing)

由1个宽泛的类型变为更小的类型，缩小声明时的类型路径(Type Narrowing)，如number | string -> number.

实践中可以通过类型保护(Type Guards)来收窄类型

常见的类型保护有：
    typeof
    switch或者一些相等运算符(===、!==)来表达相等性
    instanceof
    in

```ts
// typeof收窄
function unionType(id: string | number){
    if(typeof id === 'string'){
        console.log("字符串类型的ID:", id);
    }else {
        console.log("数值型的id:", id);
    }
}
 
// 布尔值收窄
function getMsg(msg?: string) {
    if (msg) {
        console.log("可以获取到该msg:", msg);
    }
}

// 相等性收窄
function equal(x: string | number, y: string | number) {
    if (x === y) {
        console.log("相等性收窄");
    }
}

// in收窄
type Fish = {
    swim: () => {}
}

type Bird = {
    fly: () => {}
}

function fn(ani: Fish | Bird) {
    if ('swim' in ani) {
        return ani.swim();
    }
    return ani.fly();
}

function isFish(animal: Fish | Bird): animal is Fish {
    return 'swim' in animal;
}

function fn2(animal: Fish | Bird){
    if(isFish(animal)){
        return animal.swim();
    }
    animal.fly();
}

// instanceof 收窄
function fn3(args: Date | string) {
    if (args instanceof Date) {
        return args.getDate();
    }
    return "args是一个字符串";
}
```

看了这些案例，其实类型收窄的概念说的云里雾里的，说什么将大范围的类型变成更小范围的类型，其实简单的理解就是通过类型守卫，将数据的类型范围缩小，然后有针对性的操作、管理这些数据。