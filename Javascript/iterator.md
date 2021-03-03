## 迭代器 Iterator

迭代的意思就是重复、再来。在软件开发领域，就是按照顺序反复执行同一段代码的行为，一般情况下都会有明确的终止条件。ECMAScript6开始，新增了2个高级特性：迭代器和生成器。使用这2个特性，能够更清晰、方便、高效的实现迭代。

循环，是迭代机制的基础，这是因为循环可以指定迭代的次数，以及每次迭代需要执行什么样的操作。每次循环都是在下一次迭代之前弯沉，每次迭代的顺序都是提前预定好的。

由上面的介绍可以得知，迭代会在一个有序的集合上进行，有序，我们可以理解为集合中所有的项都可以按照既定的顺序被遍历到，特别是开始和结束都有明确的定义。数组是这类数据结构最典型的案例：

```javascript
let fruits = ["apple", "peach", "pear"];
for (let i = 0; i < fruits.length; i++) {
    console.log(fruits[i]);
}
```

由于部分的原因，通过这种方式的循环并不是理想的执行过程

1. 迭代之前需要先知道数据结构的相关知识，要知道数据结构是如何遍历的，如在遍历数组的时候，要了解数组需要通过索引来遍历

2. 遍历顺序并不是数据结构所固有的：一般情况下只能通过索引的递增或者递减这种方式只适合使用数组这样的数据结构，并不适合那些具有隐式顺序的数据结构

虽然ES中增加了Array.prototype.forEach()方法，这个方法虽然相较于循环遍历数据结构有了进步，但是这个方法不能标识什么时候终止迭代，所以这个方法也是有些缺憾。

虽然正常的流程不能终止foreach循环，但是可以通过曲线、迂回的方式终止掉，可以参考：[终止foreach循环](foreach.md)

在ECMAScript实现的语言中，虽然可以通过一些方式实现迭代虽然通过一些辅助的技术手段可以实现，但是随着代码量的增加，代码就会变的越来越臃肿且不易维护。在其他的语言中如java、python等通过语言结构从原生上解决了这个问题，开发者事先不用先了解数据结构的迭代模式就可以实现迭代的操作，这就是迭代器模式。Javascript从ECMAScript6版本开始也支持了迭代器模式。

### 迭代器模式

**迭代器模式**描述了一个方案，即可以把有些结构成为可迭代对象(iterable)，因为他们实现了正式的Iterable接口，而且可以通过迭代器Iterator消费(sonsume)。

可迭代对象，是一种抽象的说法。基本上可以把数组或者集合这样的类似集合类型的对象，它们包含的元素的个数都是有限的，而且具有无歧义的遍历顺序。

**可迭代对象**

1. 可迭代对象元素的个数是有限的；

### 可迭代对象和集合的关系

1. 可迭代对象不一定是集合对象：也可以是仅仅有类似数组行为的其他类型的数据结构，如下面的计数循环

```javascript
for (let i = 0; i < 10; i++) {
    console.log(i);
}
```

循环中产生的值是临时性的，但是循环本身就是在进行迭代；

> 计数循环和数组、集合都具有可迭代对象的行为

> 计数循环(临时性可迭代对象)可实现为生成器：Generator

任何实现Iterable接口的数据结构都可以被实现Iterator接口的结构“消费”(consume)。**迭代器(iterator)** 是按需创建的一次性对象。每个迭代器都会关联一个**可迭代对象**，而迭代器会暴露迭代其关联的可迭代对象的API。迭代器无需了解其关联的可迭代对象的结构，只需要知道如何取得连续的值。这种概念上的分离是Iterable和Iterator的强大之处。


### 可迭代协议

实现iterable接口(可迭代协议)要求同时具备两种能力：支持迭代的自我识别能力和创建实现Iterator接口对象的能力。在ECMAScript中，这意味着必须要暴露一个属性作为“默认迭代器”,而且这个属性必须使用特殊的Symbol.iterator作为键。这个默认迭代器属性必须引用一个迭代器工厂函数，调用这个工厂函数必须返回一个新迭代器。

很多内置类型都实现了Iterable接口：

* 字符串

* 数组

* 映射

* 集合

* NodeList等Dom集合类型

* arguments对象

检查一些数据类型是否存在默认的迭代器，可暴露这个工厂函数：

```javascript
let num = 0;
let obj = {};

let arr = ['a','b','c'];
let str = "Hello";
let map = new Map().set("a",1).set("b",2);
let set = new Set().add("a").add("b");
let div = document.querySelectorAll("div");

// 下面几个数据类型和结构没有实现迭代器工厂函数
console.log(num[Symbol.iterator]); // undefined
console.log(obj[Symbol.iterator]); // undefined

// 下面几个数据类型和结构实现了迭代器工厂函数
console.log(arr[Symbol.iterator]);  // ƒ values() { [native code] }
console.log(str[Symbol.iterator]);  // ƒ [Symbol.iterator]() { [native code] }
console.log(map[Symbol.iterator]);  // ƒ entries() { [native code] }
console.log(set[Symbol.iterator]);  // ƒ values() { [native code] }
console.log(elements[Symbol.iterator]);  // ƒ values() { [native code] }


// 调用这个工厂函数会生成一个迭代器
console.log(str[Symbol.iterator]()); //  StringIterator {}
console.log(num[Symbol.iterator]()); //   Uncaught TypeError: num[Symbol.iterator] is not a function 报错了
```

实际代码过程中个，我们不需要显示的调用工厂函数来生成迭代器。实现迭代协议的所有类型都会自动兼容接收可迭代对象的任何语言特性。接收可迭代对象的原生语言特性包括：

* for-of循环
* 数组解构
* 扩展运算符
* Array.from()
* 创建集合
* 创建映射
* Promise.all()接收由契约组成的可迭代对象
* Promise.race()接收由契约组成的可迭代对象
* yield*操作符，在生成器中使用

如果对象原型链上的父类实现了Iterable接口，那么这个对象也就实现了这个接口。

```javascript
class FooArray extends Array { }
let fooArray = new FooArray("apple", "peach", "pear");
for (let item of fooArray) {
    console.log(item);
}
```

### 迭代器协议

迭代器是一种一次性使用的对象，用于迭代与之关联的可迭代对象。迭代器API使用next()方法在可迭代对象中遍历数据。每次成功调用next(),都会返回一个IteratorResult对象，其中包含迭代器返回的下一个值。如果不调用next(),则没有办法知道当前在什么位置，也就没有办法对可迭代对象进行遍历、迭代。

next()方法返回的IteratorResult对象包含2个属性：value和done。done是一个布尔值，表示是否还可以继续调用next()取得下一个值；value包含可迭代对象的下一个值（done值为false时），或者是undefined（done值为true时）。

```javascript
let arr = ["apple", "peach", "pear"];
// //迭代器
let iter = arr[Symbol.iterator]();
console.log(iter.next()); // { value: 'apple', done: false }
console.log(iter.next()); // { value: 'peach', done: false }
console.log(iter.next()); // { value: 'pear', done: false }
console.log(iter.next()); // { value: undefined, done: true }
console.log(iter.next()); // { value: undefined, done: true }
console.log(iter.next()); // { value: undefined, done: true }
```

> 这里我们看到迭代器iter通过调用next()命名取得的是当前值，而文档中一直说的是下一个值呀，这是为什么呢？

> 这里需要明确几个知识点，就是迭代器的位置是动态的，它随着next()方法的调用而发生位置移动的。刚开始的时候，迭代器是在所有元素的最左侧的，调用next()时获取的是迭代器的下一个值，而不是显示表现出来的当前元素的下一个值。当完成了一次next()调用之后，迭代器就会向后移动一位，next()返回当前刚刚经过的元素，也就是迭代器上一个位置的下一个元素。

每个迭代器都表示对可迭代对象的一次性有序有序遍历。不同迭代器实例之间没有关系，都各自独立的遍历可迭代对象。

```javascript
let arr = ["apple", "peach", "pear"];
// //迭代器
let iter = arr[Symbol.iterator]();
let iter2 = arr[Symbol.iterator]();
console.log(iter.next()); // { value: 'apple', done: false }
console.log(iter.next()); // { value: 'peach', done: false }
console.log(iter2.next()); // { value: 'apple', done: false }
```

迭代器并不与可迭代对象某个时刻的快照相互绑定，而仅仅是使用游标来来记录遍历可迭代对象的历程。如果可迭代对象在迭代对象被修改了，那么迭代器也会发生相应的改变。

```javascript
let arr = ["apple", "peach", "pear"];
// //迭代器
let iter = arr[Symbol.iterator]();
console.log(iter.next()); // { value: 'apple', done: false }
arr.splice(1, 0, "banana"); 
console.log(iter.next()); // { value: 'banana', done: false }
console.log(iter.next()); // { value: 'peach', done: false }
console.log(arr); // [ 'apple', 'banana', 'peach', 'pear' ]
```

这里在第一次迭代后，数组中新插入了一个元素，那么在第二次迭代的时候，直接迭代出了新插入的元素，还是在可迭代对象的第二个位置，没有停留在原来的第二个元素前面位置。

```javascript
let arr = ["apple", "peach", "pear"];
// //迭代器
let iter = arr[Symbol.iterator]();
console.log(iter.next()); // { value: 'apple', done: false }
console.log(iter.next()); // { value: 'peach', done: false }
arr.splice(1, 0, "banana"); 
console.log(iter.next()); // { value: 'peach', done: false }
console.log(arr); // [ 'apple', 'banana', 'peach', 'pear' ]
```

这个案例中，在执行了2次迭代后，迭代器的位置在可迭代对象第2个元素的后面，这个时候在可迭代对象中第一个索引位置插入了一个新的元素。虽然插入了一个新的元素，但是迭代器需要迭代可迭代对象的第3个元素了，这个时候可迭代对象的第3个对象还是peach，那么就再一次把peach打印了出来。

这2个案例，都印证了上面的结论，就是迭代器并不与可迭代对象的快照相互绑定，而仅仅是用游标记录了遍历可迭代对象迭代历程，且迭代器游标和可迭代对象的索引信息绑定，而不是和可迭代对象的元素绑定。

