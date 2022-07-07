### Number.prototype.foFixed(digits)

一句四舍五入的计算规则，精确小数点后的位数，格式化数据。

参数：digits，number类型，小数点后数字的个数，范围：0-20(包括)之间，默认为0.

如果最后的一位数是0的话，不会省略

```ts
let num:number = 12.598374;
num.toFixed(); // 13
num.toFixed(2); // 12.60
num.toFixed(4); // 12.598
```