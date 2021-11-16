### 1. 给定一个整数数组nums和一个目标值target,请你在该数组中找出和为目标值target的那2个整数,并返回它们的下标.

```js
// 双层遍历
function twoSum(arr,target){
    for(let i = 0; i < arr.length;i++){
        for(let j = i + 1; j < arr.length; j++){
            if(target - arr[i] == arr[j]){
                return [i,j];
            }
        }
    }
}
var arr = [3,8,7,9,12];
console.log(twoSum(arr,16)); // [2,3]


// 借助map实现
function findNum(nums,target){
    let map = new Map();
    for(let i = 0; i < nums.length;i++){
        let rst = target - nums[i];
        if(map.has(rst)){
            return [map.get(rst),i];
        }
        map.set(nums[i],i);
    }
}
```