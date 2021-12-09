split(separator):将一个字符串从指定的位置分割成字符串数组

```js
function reverse(num) {
  let arr = [];
  let numArr = num.toString();
  arr = numArr.split(".");
  console.log(arr);
}
let num = 456.89; // ['456', '89']
```

join(separator):将数组转换成字符串，并以 separator 为分隔符，可选参数，默认为逗号

unshift():向数组的开头添加一个或多个元素
