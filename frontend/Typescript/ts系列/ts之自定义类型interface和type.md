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

#### 2.2 调用签名

#### 2.3 构造签名

#### 2.4 this

### 3. 联合类型、交叉类型、函数重载

#### 3.1 联合类型和重载

### 4. 类型、非空、常量断言

### 5. 字面量类型

### 6. 字面量推理

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
```