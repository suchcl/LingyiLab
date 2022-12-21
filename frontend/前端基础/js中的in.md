### 1. js中的in

> 系统中全局安装ts:npm install typescript -g, 否则没有办法使用tsc指令

js中in关键字使用的场景很多，但是总的来说，是有2种类型：

1. for……in：对数组或对象的循环、迭代操作，格式：for(let 变量 in 对象/数组)，如果是数组则迭代变量是数组索引，如果是对象则迭代变量的是对象的属性；

2. 判断对象是否是数组的索引、对象的属性名，格式：(变量 in 对象)：数组时是索引，对象时是属性；

### 2. js中in的各种使用案例

1. for……in

```ts
let names = ['Tom', 'Herry'];
for(let i in names){
    console.log(i); // 0 1,变量i是数组names的索引
}

let userInfo = {
    id: 12,
    name: "Nicholas Zakas",
    age: 16
};

for(let item in userInfo){
    console.log(item);// id name age,变量item是对象userInfo的属性
}
```

在for……in循环中，循环变量是数组的索引，或者对象的属性，借此，我们也可以通过这个索引或者对象的属性来获得数组元素或者对象的属性值

```ts
let names = ['Tom', 'Herry'];
for(let i in names){
    console.log(names[i]); // Tom, Herry
}

let userInfo = {
    id: 12,
    name: "Nicholas Zakas",
    age: 16
};

for(let item in userInfo){
    console.log(`${item}: ${userInfo[item]}`); // 这里是通过[]方式读取对象属性值
}
```