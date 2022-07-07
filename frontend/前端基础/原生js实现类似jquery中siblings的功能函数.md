### 原生js实现类似jquery中siblings()功能函数

以前在使用jquery的时候，想查找一下兄弟元素，使用siblings()方法特别方便，特别省事。今天在react中想实现一个类似的查找兄弟元素的功能，想起来原生的js中并没有提供这个功能，需要自己实现一下这个功能。

```ts
  // 查找同级别元素
  function siblings(ele:HTMLElement){
    let sibs = ele.parentNode!.children;
    let newArr = [];
    for(let i = 0; i < sibs.length; i++){
        if(sibs[i] !== ele){
          newArr.push(sibs[i]);
        }
    }
    return newArr;
  }
```
