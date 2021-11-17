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
