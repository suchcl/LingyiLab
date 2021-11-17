### 1. 给定一个整数数组 nums 和一个目标值 target,请你在该数组中找出和为目标值 target 的那 2 个整数,并返回它们的下标.

```js
// 双层遍历
function twoSum(arr, target) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = i + 1; j < arr.length; j++) {
      if (target - arr[i] == arr[j]) {
        return [i, j];
      }
    }
  }
}
var arr = [3, 8, 7, 9, 12];
console.log(twoSum(arr, 16)); // [2,3]

// 借助map实现
function findNum(nums, target) {
  let map = new Map();
  for (let i = 0; i < nums.length; i++) {
    let rst = target - nums[i];
    if (map.has(rst)) {
      return [map.get(rst), i];
    }
    map.set(nums[i], i);
  }
}
```

### 2. 给定一个整数，翻转

如给 123，输出 321，如输入-456，则输出-654

```js
function reverse(num) {
  let resultArr = [];
  let numToStr = num.toString();
  for (let i = numToStr.length - 1; i > 0; i--) {
    resultArr.push(numToStr[i]);
  }

  if (numToStr[0] == "-") {
    resultArr.unshift("-");
  }
  resultArr.push(numToStr[0]);
  let resultNum = parseInt(resultArr.join(""));
  if (resultNum < Math.pow(-2, 31) || resultNum > Math.pow(2, 31) - 1) {
    return 0;
  }
  return resultNum;
}
```

### 3. 判断回文数,是回文数返回 true，否则返回 false

回文数：指正序（从左到右）和倒序（从右到左）读，都是一样的整数。

如 121 是回文数，1221 是回文数，-121 不是回文数。

关于回文数的一些特殊情况：

1. 0-9 的数字，都是回文数

2. 负数都不是回文数；

3. 不等于 0，但尾数是 0 的数字，都不是回文数

```js
// 实现1
function isPalindrome(num) {
  if (num < 0 || (num !== 0 && num % 10 === 0)) {
    return false;
  } else if (num >= 0 && num <= 9) {
    return true;
  }
  num = num.toString();
  for (let i = 0; i <= num.length / 2; i++) {
    // 注意这里不能使用num[i] === num[num.length - i - 1]，因为只要有false就要退出循环，而不是只要有1个true就可以
    if (num[i] !== num[num.length - i - 1]) {
      return false;
    }
  }
  return true;
}

// 实现2  通过高阶函数实现
function isPalindrome(num) {
  if (num < 0) {
    return false;
  }
  let numStr = num.toString();
  // return parseInt(Array.from(numStr).reverse().join("")) === num;
  return Array.from(numStr).reverse().join("") === numStr;
}

// 实现3  把原数字转换为字符串后反转，然后将反转后的字符串和原字符串做相等性判断
function isPalindrome(num) {
  let numToStr = num.toString();
  let newStr = "";
  let len = numToStr.length - 1;
  if (num >= 0 && num <= 9) {
    return true;
  } else if (num < 0 || (num !== 0 && num % 10 === 0)) {
    return false;
  }

  for (let i = len; i >= 0; i--) {
    newStr += numToStr[i];
  }
  return newStr === numToStr;
}
```
