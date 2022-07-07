### ts类型断言

类型断言，就是我知道这个变量的类型是什么，我来告诉你这个变量的类型，而不用编译器自己去推断，类型断言对运行时没有影响，只是在编译阶段起作用。也就是说如果没有进行类型断言，编辑器中可能会显示一个红色的提示，但是对代码的运行结果可能没有影响。

**类型断言有两种形式**

1. 尖括号的方式

```ts
let nvalue:string = "这是一个字符串";
let strLength:number = (<string>nvalue).length;
```

2. as操作符

```ts
let nvalue:string = "这是一个字符串";
let strLength2:number = (nvalue as string).length;
```

这是ts中使用的两种类型断言的方式，一般的情况下，两种断言方式是等价的。但是在react中，只能使用as语法，因为尖括号和react语法有冲突。所以，为了记忆方便，我们也可以只记忆as语法。

无论是两种哪种断言方式，都有一个需要注意的地方，就是进行类型断言的变量，需要使用小括号括起来，让编译器知道这是一个整体，而不能分散开，否则就成了最后的那个类型去使用变量的方法了。

```ts
// 两种断言方式，进行类型断言的变量nvalue都是用小括号括了起来(<string>nvalue)、(nvalue as string)，表示它们是一个整体
let strLength:number = (<string>nvalue).length;
let strLength2:number = (nvalue as string).length;
```

### 非空断言

