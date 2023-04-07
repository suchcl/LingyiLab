参考链接:https://juejin.cn/post/7210369671664582711
### interface和type

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

### interface和type的区别

| interface                  | type                                                     |
| -------------------------- | -------------------------------------------------------- |
| 只描述对象                 | 可以描述所有数据，基础类型和对象都可以                   |
| 使用extends来实现继承      | 通过&来实现交叉类型                                      |
| 创建新的类型名             | 只是给一个已经存在的类型起一个新的名字，不会创建新的类型 |
| 可以重复声明同一个类型名称 | 别名不能重复                                             |

总的来说，就是type可约束的范围比interface要更广，但是在实践中，能使用interface的地方就尽量使用interface，否则再去使用type。

### 索引签名

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

### 接口继承

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

### 接口实现

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