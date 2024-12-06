### set

Set是ES6中新引入的一种数据结构，它是一种类数组结构，也就是说，它的数据结构类似于数组，但是成员是唯一的，不会重复。Set允许存储任何类型的唯一值，无论是引用类型还是原始类型。

**创建Set**

可以通过new操作符来创建一个新的Set。

```js
// 创建一个空的set
const set = new Set();

// 通过一个已存在的数组初始化一个Set
const setWithArr = new Set([1, 2, 3, 4, 5]);
```

### API、常用方法

1. add(value): 添加元素，如果元素已经存在，则不会重复添加

```js
set.add("12);
set.add({
    name: "Nicholas Zakas"
});
```

2. delete(value):删除元素

```js
setWithArr.delete(2);
```

3. has(value): 检查set中是否含有某个值

```js
if(set.has(4)){
    console.log('%c [  ]-12', 'font-size:13px; background:pink; color:#bf2c9f;', "1111")
}else {
    console.log('%c [  ]-14', 'font-size:13px; background:pink; color:#bf2c9f;', "22222")
}
```

4. clear(): 清空

```js
set.clear();
```

5. size(): 获取元素数量

```js
set.size()
```

### Set的使用场景

Set作为一种高效的数据结构，具有很多可用的场景。

1. 确保唯一性

当我们明确需要一个集合来存储唯一值时，Set就是理想的选择。

```js
const set = new Set([1, 2, 2, 3, 4, 4, 5]);
console.log('%c [ set ]-66', 'font-size:13px; background:pink; color:#bf2c9f;', set)
```

2. 数组去重

当需要对一个数组进行去重的时候，可以将数组转换为set，然后再将set转换为数组。通过两次的数据结构转换，可以完成数组的去重。

```js
const set = new Set([1, 2, 2, 3, 4, 4, 5]);
const uniqueArr = [...new Set(set)];
```

3. 高效查找

Set可以用来高效查找某个数据是否存在。

```js
const fruits = new Set(['apple', 'banana', 'orange']);
console.log('%c [  ]-85', 'font-size:13px; background:pink; color:#bf2c9f;', set.has("orange"))
```

4. 集合操作

并集

```js
function union(setA,setB){
    return new Set([...setA, ...setB]);
}
const setA = new Set([1, 2, 3]);
const setB = new Set([3, 4, 5]);
console.log('%c [  ]-98', 'font-size:13px; background:pink; color:#bf2c9f;', union(setA, setB));
```

交集

```js

```

差集

```js

```

5. 临时数据结构

6. 事件监听管理器

7. 缓存机制

8. 过滤重复的api请求

Set的唯一性的独特提醒，使它成为处理唯一值、高效查找以及集合操作等问题的理想选择。通过合理利用Set，可以简化代码逻辑，提高程序性能，更好的管理数据。Set的这个特性使得我们在日常开发和解决特定问题时，都是一个强大而灵活的工具。