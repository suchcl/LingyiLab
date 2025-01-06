1. 下面代码的输出内容是什么？

```js
let array = [,1,,2,,3,];
array = array.map(i => ++i)
console.log(array); // [,2,,3,,4]
```

输出结果:[,2,,3,,4]

js遍历中，forEach、filter、reduce、every和some都会跳过空位

map()也会跳过空位，但是会保留这个位置

2. 