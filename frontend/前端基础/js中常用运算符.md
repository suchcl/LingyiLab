<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. 逻辑空赋值(??=)](#1-%E9%80%BB%E8%BE%91%E7%A9%BA%E8%B5%8B%E5%80%BC)
- [2. 空值合并运算符(??)](#2-%E7%A9%BA%E5%80%BC%E5%90%88%E5%B9%B6%E8%BF%90%E7%AE%97%E7%AC%A6)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 1. 逻辑空赋值(??=)



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
```

空值合并运算符(??)，只有在操作数为null和undefined的时候，才会返回右侧的操作数；逻辑或操作符(||)，只要左侧操作数是假值，就会返回右侧的操作数。