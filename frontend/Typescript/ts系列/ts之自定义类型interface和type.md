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
