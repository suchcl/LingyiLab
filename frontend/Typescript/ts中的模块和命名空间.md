参考链接：https://juejin.cn/post/7229193250904752188
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