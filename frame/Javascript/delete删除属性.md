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

#### 2.3 Object.create()函数创建对象