1. for……in：遍历对象

常用于遍历对象，用来遍历对象的属性

也可以用来遍历数组，只不过获取的是数组的索引，而不是数组的值

```js
const obj1 = {
    name: "Nicholas Zakas",
    age: 16
};
for (const key in obj1) {
    console.log(key);
} // name,age

const arr = ["Nicholas Zakas", 16];
for(const key in arr){
    console.log(key);
} // 0,1
```

可以总结来说，for...in获取的是可枚举对象的key，即键，返回值是一个字符串。

> 有另外一个原生的API可以直接获取可枚举属性:Object.keys(obj:Object)，该方法返回指定对象的可枚举属性的属性，返回的数据类型是一个数组。

```js
const obj1 = {
    name: "Nicholas Zakas",
    age: 16
};
console.log(Object.keys(obj1)); // ["name", "age"]
```

2. for……of：遍历数组

用来返回可枚举对象的值,可以遍历数组、Set、Map、String等几种常用的可枚举数据类型数据。

```js
const arr = ["Nicholas Zakas", 16];
for (const item of arr) {
    console.log(item); // Nicholas Zakas, 16
}
```

for...of不能遍历常规类型的对象，因为普通的对象不是可迭代的，而for...of就是用来遍历可迭代数据类型的。