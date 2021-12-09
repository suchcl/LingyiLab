<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [数组](#%E6%95%B0%E7%BB%84)
- [数组中另外5个常用的迭代(遍历)方法](#%E6%95%B0%E7%BB%84%E4%B8%AD%E5%8F%A6%E5%A4%965%E4%B8%AA%E5%B8%B8%E7%94%A8%E7%9A%84%E8%BF%AD%E4%BB%A3%E9%81%8D%E5%8E%86%E6%96%B9%E6%B3%95)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 数组

ECMAScript中数组常用的方法：

2个归并方法:reduce()、reduceRight():

这2个方法基本作用相同，只是起始位置不同，reduce()方法从数组的第一个项开始遍历，reduceRight()方法从数组的最后一项开始遍历，且都不影响原数组。其他的两个方法就没有什么区别了。

两个方法接收的参数也是相同的，一个必选的处理遍历项的回调函数，一个可选的归并的起始值。<font color="#f20">一般情况下在没有给定这个可选的第2个参数时，处理归并操作的函数将从第2项开始处理</font>。例如给下面的数组的每一项求和：

> 归并处理，可以简单理解为前一次遍历的处理结果会作为当前次处理的一个参数。

最简单的实现，我们可能会直接使用一个for循环遍历数组的每一项，然后求和,如下：

```javascript
var arr = [1, 2, 3, 4];
function getSum(arr) {
    var sum = 0;
    for (var i = 0; i < arr.length; i++) {
        sum += arr[i];
    }
    return sum;
}

console.log(getSum(arr)); // 10
```

这种逻辑设计非常简单，没有任何的难度，当然了计算结果是对的,这种解决方案用了7行代码，再来看另外一种解决方案：

```javascript
function getSumByReduce(arr){
    return arr.reduce(function(prev,cur,index,arr){
        return prev + cur
    },0); //这个参数0可有可无，如果没有就当默认是0了，因为加0后数字没变化
}

console.log(getSumByReduce(arr));  // 10
```

这种解决方案也得到了预期的计算结果，但是比第1种解决方案少了2行代码。还有一种更加精简的实现方式：

```javascript
const sum = (...num) => num.reduce((prev, cur) => prev + cur, 0);
console.log(sum(...arr));
```

只有1行，也实现了同样的目标。

可见，随着标准的升级，实现同一各效果的技术解决方案是越来越简单，对于刚入行的同学们来说还是挺好的，但是对于老人来说就需要时刻关注、学习技术标准的迭代了。这也算是对技术人的一个基本要求吧。想少干点活，总得在其他方面多付出点吧哈。

### 数组中另外5个常用的迭代(遍历)方法

下面的5个常用迭代方法，都需要传入1个必选参数回调函数，一个可选参数作为函数运行上下文的作用域对象（影响函数中this的值）。每个方法的回调函数可以接受3个参数：数组元素、元素索引、数组本身。不同的方法可能会影响到原数组的值，具体可参考如下：

every()：对数组的每一项都运行回调函数（传入的函数），如果数组的每一项都返回true，则这个方法返回true.

> 需要根据数组的一些特性来做一些真假值判定的时候，就可以使用该方法

```javascript
var arr = [0, 1, 2, false];
var flag = arr.every(function (item, index, arr) {
    if (item) {
        return false;
    }
});
console.log(flag); // false
```

filter()：

forEach()：

map()：

some()：

> 本文中学习到的<font color="#f60">所有这些方法，都可以通过常规的for循环来实现</font>，但那又为什么出了那么多的新的方法呢？技术发展了，标准也在做更新迭代，新的技术解决方案会比原来的方案代码量更少，实现更具有针对性，更加有利于我们项目性能的优化，这是内在的；还有一点是外在的，就是我们一直在使用新的技术、标准，这个时候可能还有很多人没有了解到这个技能，体现我们的代码更高大上、更具有逼格。

> 另外一个共性，就是所有的这些方法，都需要传入一个必选的回调函数，以及一个可选参数。