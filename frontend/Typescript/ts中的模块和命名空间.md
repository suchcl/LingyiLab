<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Typescript的模块和命名空间](#typescript%E7%9A%84%E6%A8%A1%E5%9D%97%E5%92%8C%E5%91%BD%E5%90%8D%E7%A9%BA%E9%97%B4)
  - [模块](#%E6%A8%A1%E5%9D%97)
  - [导出](#%E5%AF%BC%E5%87%BA)
- [命名空间](#%E5%91%BD%E5%90%8D%E7%A9%BA%E9%97%B4)
  - [命名空间语法](#%E5%91%BD%E5%90%8D%E7%A9%BA%E9%97%B4%E8%AF%AD%E6%B3%95)
  - [引入命名空间](#%E5%BC%95%E5%85%A5%E5%91%BD%E5%90%8D%E7%A9%BA%E9%97%B4)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### Typescript的模块和命名空间

#### 模块

javascript在2015年引入了模块的概念，从此js开始了标准的模块化开发阶段，ts沿用了这个概念。

ts中的模块，和js中的模块，从语法到概念、应用，和js基本是一致的。

#### 导出

在一个文件中，任何的声明都可以通过export关键字导出。导出，其实就是对外暴露该内容，让外部可以引用该模块的内容。

ts中声明模块并导出

```ts
// modA.ts
export const num = 100;
export const str = "Hello World!";

export function add(a: number, b: number) {
    return a + b;
}

export class People {
    
}

export interface IUser {
    name: string;
    age: number;
}
```

通过import导入通过expor导出的模块，并引用

```ts
// modB.ts
import { num, str, add, IUser } from "./modA";
console.log("🚀 ~ file: modB.ts:2 ~ str:", str)
console.log('%c [ num ]-2', 'font-size:13px; background:pink; color:#bf2c9f;', num)

console.log("🚀 ~ file: modB.ts:6 ~ add(2,4):", add(2, 4))

const User: IUser = {
    name: "Nicholas Zakas",
    age: 12
};
console.log("🚀 ~ file: modB.ts:11 ~ User:", User)
```

### 命名空间

早期的ts中是没有命名空间的概念的，和js一样，只有模块的概念。

但是ts中的模块区分为内部模块和外部模块

从ts1.5开始，内部模块被改名为命名空间，所以我们使用ts时常说的命名空间，其实就是指ts的内部模块

那么在实际应用中怎么区分内部模块(命名空间)和外部模块呢？应该还是从其封装的内容上来区分：

1. 命名空间(内部模块):主要用于组织代码，避免命名冲突

2. 外部模块(模块):侧重代码的封装复用，一个模块内可能包含了多个命名空间

在日常的项目开发中，如果一个ts文件没有书写模块化的语法，那么这个文件中所有定义的变量默认都是挂载到全局上的，那么两个文件内就不能出现两个同名的变量，否则编译器就会报错，给出异常提示.

> 但是如果一个ts文件中只要有一个模块使用了export关键字导出过模块那么上面的异常就会消失。

```ts
// modC.ts
const username:string = "Youyyyy";

// modD.ts
const username:string = "Hello";
```

如果modC.ts和modD.ts中都没有使用过export导出过模块，那么这两个文件中因为都定义了username变量，所以编译器就会报错

![声明重复变量异常提示](./images/i63.png)

但是只要modC.ts或者modD.ts中有一个文件中有使用过export导出过模块，这个重复声明的异常就会消失：

```ts
const username:string = "Hello";
export const flag:boolean = false;
```

异常提示消失

#### 命名空间语法

```markdown
namespace 命名{

}
```

- 命名空间可以直接导出

- 命名空间内可以定义变量，也可以将变量导出；

- 命名空间内通过export向外暴露内容，如变量、函数、类、接口等

当命名空间和命名空间内的变量都有导出的时候，就可以在其他文件中通过导入命名空间，然后通过命名空间.变量名的方式使用。

```ts
// modC.ts 声明并导出命名空间、导出命名空间中的一个变量
export namespace ModC {
    const username: string = "Youyyyy";
    export const age: number = 12; // 命名空间内的变量导出
}

// modD.ts 导入命名空间，并引用其内的变量
```

#### 引入命名空间

前面我们已经使用过export导出命名空间，然后在需要使用的文件中通过import关键字导入，和普通变量、方法、接口等变量的使用方式相同，但是也有介绍可以通过三斜杠(///)的方式导入命名空间

使用三斜杠的方式导入命名空间的时候,三斜杠指令必须在文件的最开始,且命名空间不需要使用export导出

```ts
// modC.ts
namespace ModC {
    const username: string = "Youyyyy";
    export const age: number = 12;
}

// modD.ts
///<reference path="./modC.ts" />
console.log("🚀 ~ file: modD.ts:8 ~ ModC.age:", ModC.age)
```

虽然有些文档曾这么介绍过，但我测试没有成功，各种方式都曾尝试过，都没有成功。

> 对于命名空间的引用，直接使用export、import即可，对于三斜杠(///)的使用方式，了解即可。

**模块和命名空间**

当一个项目规模变大以后，我们就可能会大范围的使用模块和命名空间，那么就意味着向外暴露的内容增多。为了文件数量和文件质量的合理规划，我们有可能会在一个命名空间中导出多个模块，也可能会在一个模块中导出多个命名空间，具体使用哪种方式，根据实际场景灵活应用即可。

命名空间，主要是为了解决变量的命名冲突；

模块，主要为了实现代码复用。

命名空间和模块的目标不同。