<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Js中的对象](#js%E4%B8%AD%E7%9A%84%E5%AF%B9%E8%B1%A1)
- [创建对象](#%E5%88%9B%E5%BB%BA%E5%AF%B9%E8%B1%A1)
    - [对象字面量方式创建对象](#%E5%AF%B9%E8%B1%A1%E5%AD%97%E9%9D%A2%E9%87%8F%E6%96%B9%E5%BC%8F%E5%88%9B%E5%BB%BA%E5%AF%B9%E8%B1%A1)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 1. Js中的对象

Js对象是多个属性的无需集合,每个属性都有自己的名字和值.属性名通常是字符串,也可以是符号,因此,也有一个说法,就是对象把字符串映射为值.

js对象中的这种把字符串映射到值的这种映射关系,曾经有很多种叫法,包括散列、散列表、字典或关系数组等基本的数据结构.

Javascript对象是动态的,即可以动态的添加和删除属性.

对象是可以被修改的,对象是按照引用操作,而不是按值来操作的.

对象的属性,有一个名字和值.属性名,可以是任意的字符串,包括空字符串或任意符号,但是对象不能有两个同名的属性.值可以是任意的合法的javascript值,也可以是函数(函数也是js中合法的值).

很多时候,区分直接定义在对象上的属性和那些从原型继承的属性很重要.javascript使用术语“自有属性”指代非继承属性.

除了名字和值两个基本的属性之外,每个属性还有3个属性特性(property attribute):

1. writalbe:可写的,指定是否可以设置属性的值

2. enumerable: 可枚举的,指定是否可以在for/in循环中返回属性的名字.

3. configurable:可配置的,指定是否可以删除属性,以及是否可以修改其他属性特性

很多的javascript的内置对象拥有可读、不可枚举、不可配置的特性.

默认情况下,我们自己所创建对象的所有属性都是可写、可枚举和可配置的.

### 2. 创建对象

Js中创建对象有3种方式:

1. 对象字面量

2. new 关键字

3. Object.create()函数

#### 2.1 对象字面量方式创建对象

```js
// 对象字面亮的形式创建对象
const person = {
    fullname: "Nicholas Zakas",
    "age": 18,
    " ": "e2e",
    for: "Programmer",
    play: function(){
        console.log("play games");
    },
    name: {
        firstname: "Nicholas",
        lastname: "Zakas"
    }
};

console.log(person[" "]); // e2e
```

上面的代码,就是一个字面量对象.

兑现字面量对象:

1. 属性名可以使用引号包裹起来,也可以不包裹;
2. 属性名可以是任意的字符串:包括js语言的保留字、空字符串
3. 属性值可以是基本的数据类型、也可以是function、对象(包括对象字面量读写)和数组
4. 最后一个属性后的逗号可以省略,也可以不省略

> 对象字面量是一个表达式,每次求值都会创建并初始化一个新的、不一样的对象.
>
> 字面量每次求值的时候,它的每个属性也会被求值
>
> 这就意味着同一个对象字面量如果出现在循环体中,或出现在被重复调用的函数体内,则会创建多个新对象,且这些新对象的属性值可能不同.

#### 2.2 new关键字创建对象

new操作符后跟构造函数.

构造函数,有语言内置的,也可以是我们自定义创建的.

js内置的、使用较多的构造函数有:

```js
const o = new Object();
const arr = new Array();
const date = new Date();
const map = new Map();
```

也可以是自定义的构造函数

```js
function Person(name, age) {
    this.name = name;
    this.age = age;
}

const p = new Person("Nicholas Zakas", 16);
console.log(p.name); // Nicholas Zakas
console.log(p.age); // 16
```

> 构造函数和普通函数并没有什么区别.主要的区别就是使用的方式不同
>
> 就形式上来看,构造函数的函数名首字母大写,标识这是一个构造函数;普通函数的函数名,首字母一般小写 --- 但这种命名规则,不是绝对的,仅仅是我们的一些编码习惯,不具备的技术上的约束.

#### 2.3 Object.create()函数创建对象

##### 2.3.1 原型

js中,几乎每个js都有一个与之关联的对象,这个与之关联的对象,被称为原型(prototype).

通过对象字面量创建的对象,都有相同的原型对象:可以通过Object.prototype访问它的原型对象.

通过new关键字和构造函数调用创建的对象,那么可以使用构造函数的prototype属性访问它的原型对象.即通过new Object()创建的对象的原型对象是Object.prototype,通过new Date()创建的对象的原型对象是Date.prototype.

> 几乎所有的js对象都有原型,但是只有少数的对象有prototype属性. ---  没有太理解
>
> 但正是因为这些少数有prototype属性的对象,为所有的其他的对象定义了原型

Object.prototype没有原型,因为它不继承任何属性.

##### 2.3.2 使用Object.create()函数创建对象

js中还可以使用Object.create()函数来创建对象,使用该函数创建对象时,第一个参数为新建对象的原型.也可以有第二个可选的参数,用来描述新对象的属性.

```js
const book = Object.create({
    name: "Javascript高级程序设计",
    price: 79
});
console.log(book.name); // Javascript高级程序设计
```

Object.create()函数的一个用途是可以防止对象被某个第三方的函数意外(但非恶意)的修改.

这种情况下,不要直接将对象传递给库函数,而是将一个继承自该对象的对象.如果第三方的库函数要读取这个对象的属性,那么可以读取到继承来的属性值,如果要设置这个对象的属性,那么也只是修改新对象的属性,并不会修改、影响原始对象.

```js
// 原始对象
const obj = {
    name: "Nicholas Zakas",
    age: 18
};

lib.fn(Object.create(obj)); // 以这种方式,可以访问到原始对象obj的属性,也可以设置新的属性,但是设置的新属性只是修改继承自obj的新对象的属性,并不会修改obj本身
```

#### 2.4 读取、设置属性

#### 2.5 删除属性

js中通过delete操作符删除对象的属性

>  delete删除的是对象的属性本身,不是属性的值,delete不操作属性值.

delete操作符只能删除自有属性,不删除继承属性 --- 如果要删除继承属性,必须从定义属性的原型对象上删除.但是这样做会影响继承自该原型的所有对象.

如果delete删除成功,或者删除一个不存在的属性,或者对原对象没有影响的,操作结果都会返回true

delete删除一个非属性访问表达式,也返回true

```js
const book = {
    name: "Javascript高级程序设计",
    author: "Nicholas Zakas",
    price: 119
};
console.log(delete book.price); // true  删除了price属性
console.log(delete book.toString); // true 删除了一个继承的属性,它不能删除继承属性,无影响 true
console.log(delete book.priter); // true  删除了一个不存在的属性
console.log(delete 18); // true 删除了一个非属性访问表达式
```



delete不能删除configurable特性为false的属性

严格模式下,删除不可配置的属性,会报TypeError的异常

在非严格模式下,删除不可配置的属性,返回一个false

```js
const person = {
    name: "Nicholas Zakas",
    age: 18,
    height: 1.89
};
Object.defineProperty(person,"height",{
    configurable: false
});

console.log(delete person.height); // false  将height属性设置成了不可配置了
```

