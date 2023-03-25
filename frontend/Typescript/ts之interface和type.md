参考连接:https://juejin.cn/post/7210369671664582711
### 1. interface和type

#### 1.1 基本使用

1. 使用interface定义新的自定义结构类型

2. 使用type重新命名一个已经存在的类型

```ts
// interface定义一个新的结构
interface IPerson {
    name: string;
    age?: number; // ?表示当前属性可选
    readonly code: string; // readonly只读
}

// 使用type重新命名一个已经存在的类型
type Point = {
    x: number;
    y: number;
};
```

使用type定义的结构{x:number;y:number;}是一个已经存在的类型，然后通过type重新为该类型起了个新的名字Point。

interface和类型之间没有=，type和类型之间通过=连接。

#### 1.2 区别

#### 1.3 索引签名

#### 1.4 接口继承

#### 1.5 接口实现

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