### ts中函数声明和实现分离的写法

ts中函数的声明和实现是分离的，这一点是和js有区别的地方。

ts中可以通过type和interface来声明函数

**利用type声明函数**

```ts
type addFun = (a:number,b:number) => number;
```

这是使用type声明了一个函数的定义，定义了一些规则，然后就可以谁用这个规则约束去实现函数了.

```ts
// 根据上面定义的函数来实现函数
let add:addFun = function(x,y){
    return x + y;
}

// 调用函数
add(3,4);
```

**利用interface声明函数**

```ts
// 定义函数
interface IIncrease {
    (a: number, b: number): number;
}
```

下面来看interface定义的函数的实现

```ts
let increase: IIncrease = function (x, y) {
    return x + y;
}

let inc: IIncrease = (x, y) => x + y;
```

两种实现方式都可以，都可以满足函数声明的约束规则。

无论是使用type还是interface声明函数，都是作为一种类型来实际存在的，这种类型约束对于变量是最为友好的，所以在函数实现的时候，最简单的就是使用箭头函数或者函数表达式的方式。