<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. 交叉类型](#1-%E4%BA%A4%E5%8F%89%E7%B1%BB%E5%9E%8B)
- [2. 联合类型](#2-%E8%81%94%E5%90%88%E7%B1%BB%E5%9E%8B)

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