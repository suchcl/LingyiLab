<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. js中字符串常用方法](#1-js%E4%B8%AD%E5%AD%97%E7%AC%A6%E4%B8%B2%E5%B8%B8%E7%94%A8%E6%96%B9%E6%B3%95)
- [2. js中数组常用方法](#2-js%E4%B8%AD%E6%95%B0%E7%BB%84%E5%B8%B8%E7%94%A8%E6%96%B9%E6%B3%95)
- [3. js中对象常用方法](#3-js%E4%B8%AD%E5%AF%B9%E8%B1%A1%E5%B8%B8%E7%94%A8%E6%96%B9%E6%B3%95)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 1. js中字符串常用方法

1. split(separator):将一个字符串从指定的位置分割成字符串数组

```js
function reverse(num) {
  let arr = [];
  let numArr = num.toString();
  arr = numArr.split(".");
  console.log(arr);
}
let num = 456.89; // ['456', '89']
```

2. includes(searchString,[position]):从当前字符串中指定的位置开始查询是否存在某字符串。position可选，默认从0开始。

如果查找到了字符串，返回true，否则返回false

```js
const str = "hello world!";
console.log(str.includes("lo")); // true
console.log(str.includes("Nic")); // false
```

3. indexOf(searchString[,fromIndex]):获取从指定的位置开始查找查询字符串第一次出现的索引，如果不存在返回-1

索引从0开始

```js
const str2 = "He is seeking a divorce, and was granted a temporary restraining order by the courts, the Post reported";
console.log(str2.indexOf("Nicho")); // -1
console.log(str2.indexOf("ing")); // 10
```


### 2. js中数组常用方法

1. join(separator):将数组转换成字符串，并以 separator 为分隔符，可选参数，默认为逗号

2. unshift():向数组的开头添加一个或多个元素

### 3. js中对象常用方法

1. Object.entries()

返回给定对象自身可枚举属性的键值对数组。或者可以这么简单的理解，只要是我们自己编码设置的属性，就可以通过Object.entries()遍历返回，返回的数据类型为数组。

```js
const obj1 = {
    name: "Nicholas Zakas",
    age: 16
};
console.log(Object.entries(obj1));
```

返回结果为：

```js
[
  [
    "name", "Nicholas Zakas"
  ],
  [
    "age": 16
  ]
]
```

2. Object.keys()

3. Object.values()

