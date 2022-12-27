<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. 交叉类型](#1-%E4%BA%A4%E5%8F%89%E7%B1%BB%E5%9E%8B)
  - [1.1 不是所有的类型都要通过&合并新的类型](#11-%E4%B8%8D%E6%98%AF%E6%89%80%E6%9C%89%E7%9A%84%E7%B1%BB%E5%9E%8B%E9%83%BD%E8%A6%81%E9%80%9A%E8%BF%87%E5%90%88%E5%B9%B6%E6%96%B0%E7%9A%84%E7%B1%BB%E5%9E%8B)
  - [1.2 合并的新类型中有重名属性时的处理逻辑](#12-%E5%90%88%E5%B9%B6%E7%9A%84%E6%96%B0%E7%B1%BB%E5%9E%8B%E4%B8%AD%E6%9C%89%E9%87%8D%E5%90%8D%E5%B1%9E%E6%80%A7%E6%97%B6%E7%9A%84%E5%A4%84%E7%90%86%E9%80%BB%E8%BE%91)
- [2. 联合类型](#2-%E8%81%94%E5%90%88%E7%B1%BB%E5%9E%8B)
- [3. 交叉类型和联合类型的关系](#3-%E4%BA%A4%E5%8F%89%E7%B1%BB%E5%9E%8B%E5%92%8C%E8%81%94%E5%90%88%E7%B1%BB%E5%9E%8B%E7%9A%84%E5%85%B3%E7%B3%BB)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 1. 交叉类型

交叉类型，就是通过&符号将多个类型联合到一起，合并成一个新的类型，然后使用type来声明新生成的类型。

```ts
interface classA {
    name: string;
    age: number;
}

interface classB {
    name: string;
    mobile: number;
}

type NewClass = classA & classB;

let info: NewClass = {
    name: "Nicholas Zakas",
    age: 16,
    mobile: 13209099876
}
```

有两个类型classA和classB，然后这两个类型通过&合并了，最后通过type关键字将合并的类型生成为一个新的类型，该新的类型包括了原来两个类型的所有属性。重合的类型只算一次。

#### 1.1 不是所有的类型都要通过&合并新的类型

不是说所有类型都能通过&合并成新的类型，因为这样合并后没有现实意义。比如两个类型A和B都有属性name，其中A中的name属性为string类型，B中的name为number类型，但是如果A & B合并了，那么这个新合成的新的类型就成了never类型了，就已经失去了类型合并的意义了。

```ts
interface A {
    name: string;
}

interface B {
    name: number;
}

type T = A & B;

let t:T = {
    name: 12 // 这里会报异常，A和B合并后形成的是never类型，不能将类型“number”分配给类型“never”
};
```

#### 1.2 合并的新类型中有重名属性时的处理逻辑

合并的接口类型中如果有重名属性，可以分为两种情况去处理：

1. 同名属性的类型相同，合并后还是原来类型

```ts
interface M {
    name: string;
    age: number;
}

interface N {
    name: string;
    gender: number;
}

type MN = M & N;
let nm: MN = {
    name: "Nicholas Zakas",
    age: 16,
    gender: 1
};
```

原类型M和N，有同名的属性name，也有不同名的其他属性，在M和N合并后，同名的name还是原来的string类型，其他不同名的属性保持原来的类型不变。

2. 同名属性的类型不同，合并后为never，合并操作没有现实意义

如果原来类型中有同名的属性，但是类型不同，这个时候合并后的新类型就是never。

```ts
interface X {
    q: number;
    w: string;
}

interface Y {
    q: boolean;
    r: string;
}

type Z = X & Y; // Z是never
```

原类型X和Y中都有一个q属性，在X中q属性是nunber类型，Y中q是boolean类型，所以两个类型合并后就是never了。因为一个值，不可能同时即时nunber类型，又是boolean类型，那么结果就只能是never，永远不可能。

### 2. 联合类型

联合类型和交叉类型类似，只是联合类型是通过｜符合合并链接多个类型而成的新类型。联合类型取多个类型的交集，即多个类型都有的类型才是新类型的最终类型。

### 3. 交叉类型和联合类型的关系

交叉类型和联合类型类似，都是通过对原来的多个类型进行一些操作，形成一个新的类型。

区别：

1. 交叉类型，通过&合并原类型，新类型的最终类型是原类型的且的关系，即原类型中每个类型都要实现；

```ts
interface M {
    name: string;
    age: number;
}

interface N {
    name: string;
    gender: number;
}

type MN = M & N;
let nm: MN = {
    name: "Nicholas Zakas",
    age: 16,
    gender: 1
};
```

新类型MN必须要全部实现原类型的所有属性，如name、age和gender。

2. 联合类型，通过｜合并原类型，新类型的最终结果是原类型的或的关系，即新的类型可以只实现原类型中的部分属性，也可以全部实现；

```ts
let n:string | number; // n的值可以是string类型，也可以是number类型
```

**多个接口类型的联合**

```ts
interface X {
    q: number;
    w: string;
    r: string;
    z: string;
}

let n:string | number;

interface Y {
    q: number;
    r: string;
}

type XY = X | Y;
let xy: XY = {
    q: 2,
    r: "Hello",
    w: '12',
    z: 'world'
};
```

变量xy可以实现X和Y的部分类型，也可以实现X和Y的全部属性，即xy这个对象的属性，可以只有X和Y、X或Y的部分属性，而不必全部都包含进来。

> ts中通过function关键字声明的函数，如果定义的返回值类型如果不是void或者any，那么这个函数就必须要有返回值。

```ts
function contactName(oldName:string):string{
    let newName:string = oldName;
    return newName;
}
```

案例函数声明为string类型，那么就必须要有一个返回值，返回了newName。

<font color='#f20'>ts中，如果函数需要继承或实现某个接口，那么可以尝试优先使用函数表达式的方式声明函数，可以规避一些ts类型校验的一些问题。</font>