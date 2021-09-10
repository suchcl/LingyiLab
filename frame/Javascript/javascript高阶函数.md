### Js高阶函数

常用的编程范式：

1. 命令式编程：

2. 声明式编程：

3. 面向对象编程：

4. 函数式编程：


Js中，数组操作的几个高阶函数：

1. map：返回一个新的数组，原数组不变   映射操作

```javascript
let num = [1, 4, 9];
let newNum = num.map(function (item) {
    return item * 2;
});
console.log(newNum); // 返回一个经过处理后的数据组成的新数组[2, 8, 18]
console.log(num); // [1, 4, 9],原数组不变
```

2. reduce：归并，返回最后一次归并的值

```javascript
let num = [1,4,6];
/**
    * prev: 前一次归并（计算）的结果，默认为reduce方法的第2个参数
    * item：当前次遍历的当前值
    * return：最后归并（计算）的结果，一个新的值
    * remark: 原数组不变
    */
let total = num.reduce(function(prev,item){
    return prev + item;
},0);
console.log(total); // 11，数组各项计算的最终结果
console.log(num); // [1, 4, 6]，原数组不变
```

3. filter：返回一个过滤后的符合要求的数据组成的新数组，原数组不变

```javascript
let nums = [56, 120, 87, 19, 109, 210, 47];
let newNum = nums.filter(function (n) {
    return n < 100;
});
console.log(newNum); // 返回了由符合条件的数据组成的新数组[56, 87, 19, 47]
console.log(nums); // 原数组不变 [56, 120, 87, 19, 109, 210, 47]
```

4. some：