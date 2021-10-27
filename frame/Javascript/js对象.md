### js对象：Object类型

大多数引用值的类型都是Object类型。

Object是js中最常用的类型之一，Object本身没有多少功能，但是比较适合存储在和应用之间的交换数据。

**创建对象有两种方式：**

1. 使用new操作符和Object的构造函数。

   ```javascript
   let person = new Object();
   person.name = "Nicholas Zakas";
   person.age = 22;
   ```

2. 使用对象字面量

   对象字面量创建对象，是对象定义的一种简写形式，尤其是包含了大量属性的对象的创建。

   ```javascript
   let person2 = {
       name: "Nicholas Zakas",
       age: 28
   };
   ```

   对象字面量中，最后一个属性的逗号，案例中省略了。这个逗号，在现代新标准的浏览器中，可有可无，但是在一些老旧的传统浏览器中，如果在对象的最后一个属性后面加了逗号，可能会报错。所以我们就干脆记住一点：<font color="#f20">对象字面量最后一个属性后面，不要加逗号</font>

   对象字面量的属性，可以是字符串，也可以是数字。当属性是数字是，会自动转化为字符串。

   ```javascript
   let person2 = {
       name: "Nicholas Zakas",
       age: 28,
       66: "Hanmeimei"
   };
   ```

   当字面量的属性是数字时，访问该属性时，就只能通过中括号的方式来读取该属性了

   ```javascript
   let person2 = {
       name: "Nicholas Zakas",
       age: 28,
       66: "Hanmeimei"
   };
   console.log(person2["66"]); // Hanmeimei
   ```

   > 注意，当是数字属性是，不是说可以使用中括号的方式读取属性，而是只能是通过中括号的方式读取属性，不能通过点语法去读取属性。

   对象字面量的属性，可以加引号，也可以不加引号；

   

**上下文**

表达式上下文：ECMAScript中，表达式上下文指的是期待返回值的上下文。如赋值操作符表示后面要跟一个值，因此赋值操作符后表示一个表达式的开始：如

```javascript
let person2 = {
    name: "Nicholas Zakas",
    age: 28
};
```

左大括号表示一个表达式上下文的开始

语句上下文：一个语句块的环境，如if语句后面跟的{}里面，就是一个语句上下文。

```javascript
if (true) {
    // 逻辑代码
}
```

这里面就是一个语句上下文。



**使用构造函数创建对象和使用字面量方式创建对象的区别？**

