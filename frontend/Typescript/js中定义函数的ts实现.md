### JS中定义函数的TS实现方式

我们知道js中定义函数常用的有3种方式：

1. 通过function关键字声明函数

JS实现

```js
function setName(name){
    console.log(name);
}
```

ts实现

```ts
function setNameTs(name: string):void{
    console.log(name);
}
```

2. 函数表达式，也被称为匿名函数

```js
let setName2 = function(name){
    console.log(name);
}
```

TS实现

```ts
let setName2Ts = function(name:string):void {
    console.log(name);
}
```

3. 箭头函数

```js
let setName3 = (name) => {
    console.log(name);
}
```

TS实现

```ts
let setName3Ts = (name:string):void => {
    console.log(name);
}
```