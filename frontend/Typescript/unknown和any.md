### unknown和any

unknown和any都是ts的数据类型。

unknown表示一种不确定的类型，即编译器没有办法确定该变量的类型，也因此没有办法对该变量执行任何操作。所以通常情况下，unknown类型的变量需要在进行类型检查或者断言后才能使用；

any可以简单的理解为对ts不熟悉，而仅仅的简单使用any做为一种类型约束的随意版。

也就是说，声明的unknown类型的变量，在对变量进行操作时，需要先对变量进行类型检查或者类型断言后才能去操作

```ts
let input1: unknown;
let username: unknown;
input1 = 3;
// input1 = "hello";
console.log("input1:", input1);

// 直接操作unknown类型报错
console.log("pos:", input1.indexOf('lo'));

// 或者使用类型断言的方式
console.log("pos:", (<string>input1).indexOf("lo"));
console.log("pos:", (input1 as string).indexOf("ll"));

// 或者使用下面的类型检查的方式
if (typeof input1 === "string") {
    username = input1;
}
console.log("username:", username);
```

any，可以简单的理解为ts的最顶层类型，也可以理解为ts的最底层类型，本质上给一个变量声明了any类型，就会关闭ts对该变量的类型检查，也就是和js一样了，没有类型约束了，也就是说代码中可能会出现一些问题不能提前发现了。所以呢，在使用any类型时要特别谨慎。