<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. 逻辑空赋值(??=)](#1-%E9%80%BB%E8%BE%91%E7%A9%BA%E8%B5%8B%E5%80%BC)
- [2. 空值合并运算符(??)](#2-%E7%A9%BA%E5%80%BC%E5%90%88%E5%B9%B6%E8%BF%90%E7%AE%97%E7%AC%A6)
  - [2.1 为变量赋默认值](#21-%E4%B8%BA%E5%8F%98%E9%87%8F%E8%B5%8B%E9%BB%98%E8%AE%A4%E5%80%BC)
  - [2.2 短路](#22-%E7%9F%AD%E8%B7%AF)
  - [2.3 不能直接与逻辑运算符and和or操作符共用](#23-%E4%B8%8D%E8%83%BD%E7%9B%B4%E6%8E%A5%E4%B8%8E%E9%80%BB%E8%BE%91%E8%BF%90%E7%AE%97%E7%AC%A6and%E5%92%8Cor%E6%93%8D%E4%BD%9C%E7%AC%A6%E5%85%B1%E7%94%A8)
  - [2.4 可选链式操作符?.](#24-%E5%8F%AF%E9%80%89%E9%93%BE%E5%BC%8F%E6%93%8D%E4%BD%9C%E7%AC%A6)
- [3. 逻辑空赋值和空值合并运算符的区别](#3-%E9%80%BB%E8%BE%91%E7%A9%BA%E8%B5%8B%E5%80%BC%E5%92%8C%E7%A9%BA%E5%80%BC%E5%90%88%E5%B9%B6%E8%BF%90%E7%AE%97%E7%AC%A6%E7%9A%84%E5%8C%BA%E5%88%AB)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 1. 逻辑空赋值(??=)

逻辑空赋值，是在左侧操作数是nullish(null和undefined)时对其赋值。

语法：

expr1 ??= expr2;

表示只有在expr1为null和undefine的时候，才会将expre2的值赋给expr1。它等价于下面的表达式：

```ts
x ?? (x = y)
```

### 2. 空值合并运算符(??)

空值合并运算符(??)，是一个逻辑运算符，当操作符左侧的操作数为null或者undefined的时候，然后返回操作符右侧的操作数，否则返回操作符左侧的操作数。

与逻辑或操作符(||)不同，逻辑或操操符会在操作数为假值时返回右侧的操作数。也就是说，如果使用落激活(||)来为某些变量设置默认值，可能会遇到意料之外的行为。因为空字符串和0都会被认为是假值。

```ts
const foo = null ?? "default value";
console.log(foo); // default value

const foor = undefined ?? "not default value";
console.log(foor); // not default value

const baz = 0 || 100;
console.log(baz); // 100

const bar = '' || "Hello";
console.log(bar); // "Hello"

const cnt = 0 ?? "Hello world!";
console.log(cnt); // 0
```

空值合并运算符(??)，只有在操作数为null和undefined的时候，才会返回右侧的操作数；逻辑或操作符(||)，只要左侧操作数是假值，就会返回右侧的操作数。

实用空值合并运算符，通常都是为了给常量提供默认值，以此保证常量不是null或者undefined。

#### 2.1 为变量赋默认值

通常情况下，如果想给一个变量赋默认值，都是实用逻辑或操作符(||)，如：

```ts
let foo;
let newFoo = foo || "hello";
console.log(newFoo); // hello

let count = 0;
let text = "";
let qty = count || 100;
let message = text || 'hi';
console.log(qty); // 100
console.log(message); // hi
```

由于逻辑或(||)是一个布尔逻辑运算符，左侧的操作数会被强制转换成布尔值用于求值。任何假值(0、空字符串、NaN、null、undefined)都不会能够被返回，加入这个时候使用0、空字符串、NaN作为有效值的时候，就不能得到有效、预期的值。

```ts
let count = 0;
let text = "";
let qty = count || 100;
let message = text || 'hi';
console.log(qty); // 100
console.log(message); // hi
```

在这种场景中，可以使用空值合并运算符(??)，空值合并运算符只有在左侧操作数是null和undefined的时候，才会返回右侧的操作数。

```ts
let foo;
let newFoo = foo || "hello";
console.log(newFoo); // hello，foo声明后没有赋值，所以其值是一个undefined

let count = 0;
let text = "";
let qty = count ?? 100;
let message = text ?? 'hi';
console.log(qty); // 0
console.log(message); // "" 空的字符串
```

> 注意，空值合并运算符(??),是一个逻辑运算符，不是一个布尔逻辑运算符，不会对左侧操作数做强制的值转换，不会被强制转换成布尔值求值去做判断，只判断左侧的操作数是不是null和undefined。

#### 2.2 短路

空值合并运算符(??)和逻辑运算符(逻辑或||、逻辑与and &&)相似，当左侧表达式不为null或者undefined的时候，不会对右侧的操作数、表达式求值。

#### 2.3 不能直接与逻辑运算符and和or操作符共用

空值合并运算符不能直接和逻辑运算符and与or直接使用，大概是因为它们之间的优先级没有定义吧。如果直接使用了，现在会抛出语法错误。

但是如果通过小括号显示的指定了优先级，则可以正常使用。

```ts
(null || undefined) ?? "Hello"
```

这样显示的指定了运算优先级，逻辑运算符and和or就可以和空值合并运算符一起使用了。

#### 2.4 可选链式操作符?.

空值合并运算符针对的是null和undefined，可选链式操作符?.也是针对这两个值。在访问对象的属性值可能是null或undefined时非常有用。

```ts
let obj = {
    msg: "hello world!"
};
console.log(obj.msg?.toUpperCase());
```
先判断obj.msg是否存在，是否为null或者undefined，如果是，则不能正常执行后面的toUpperCase()，否则可以正常执行。

### 3. 逻辑空赋值和空值合并运算符的区别

在一些场景下，使用两种运算符的结果在视觉上感觉是相同的，但是底层的逻辑不通。

```ts
const a = {
    duration: 50,
    speed: 10
};
a.duration ??= 10;
console.log(a.duration); // 50
a.speed ?? 20;
console.log(a.speed); // 10
```
比如这样一个案例，a.duration ??= 10最终的值是50，a.speed的最终的值是10.

先来看a.duration ??= 10,该表达式是当a.duration为null或者undefined的时候，将操作符右侧的值10赋值给a.duration,然后a.duration的值会变成10.而a.speed ?? 20的意思是如果a.speed的值为null或者undefined的时候，就将a.speed的值返回，否则返回操作符右侧的操作数20.

所以空值合并运算符和逻辑空赋值的本质区别是，一个是返回值，一个是赋值。