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

#### 1.2 合并的新类型中有重名属性时的处理逻辑


### 2. 联合类型