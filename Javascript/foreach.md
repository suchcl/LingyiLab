在通过forEach()进行数据遍历的时候，有的时候期望在某个场景中终止遍历，因为并不是所有的数据都需要遍历，或者遍历的时候没有实际的意义。那么按照正常的逻辑，可能我们会在遍历某个值的时候，return 一下，或者return false，这是我们的常规做法。但是在forEach遍历中，使用return或者return false只能退出当前遍历而进行到下一次遍历。

```javascript
let fruits = ["apple", "peach", "pear"];
fruits.forEach((item) => {
    if (item == "peach") {
        return;
    }
    console.log(item);
});
```
输出结果如下
```bash
apple
pear
```