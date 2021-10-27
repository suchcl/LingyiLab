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

   对象字面量的属性，可以是字符串，也可以是数字。<font color="#f20">当属性是数字时，会自动转化为字符串。</font>

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
   >
   > 在使用对象字面量方式创建函数时，并不会实际调用Object构造函数

   对象字面量的属性，可以加引号，也可以不加引号；

**属性的读取**

js中，对象读取属性有两种方式：

1. 点语法

   点语法读取对象属性，是大多数面向对象语言都遵循的惯例

   ```javascript
   let person = new Object();
   person.name = "Nicholas Zakas";
   person.age = 22;
   console.log(person.name); // 通过点语法读取属性
   ```

   点语法，面向对象语言都遵循这样的规则，更容易理解。

2. 中括号

   中括号语法读取对象属性，好像只有js有这个能力，但是<font color="#f20">在使用中括号语法的时候，属性名要使用字符串形式。</font>

   ```javascript
   let person2 = {
       name: "Nicholas Zakas",
       age: 28,
       66: "Hanmeimei"
   };
   console.log(person2["66"]); // Hanmeimei
   ```

   使用中括号语法读取对象属性，属性要使用字符串形式，简单理解下，就是属性要使用引号引起来。

   从实现属性访问本身的功能来说，点语法和中括号语法都没有什么本质的区别，但是通过中括号语法可以实现通过变量访问属性。

   属性中可能会有语法错误的字符，如属性中出现空格、关键字、保留字时，也可以使用中括号语法读取属性

   ```javascript
           let person = {
               name: "Nicholas Zakas",
               age: 18
           };
           let propertyName = "name";
           console.log(person[propertyName]);
           // 关键字属性
           person["const"] = "关键字属性";
           console.log(person["const"]);
   
           // 属性中出现了空格
           person["first name"] = "Nicholas";
           console.log(person["first name"]);
   ```

   像关键字属性、具有空格的属性，在点语法中都是不允许的，但是通过中括号语法可以实现。

**对象的两个基本的认知**

函数对象的原型是对象（原型链为：实例，通过new构造函数->函数对象->对象->null）

只有函数有prototype，对象没有

**使用构造函数创建对象和使用字面量方式创建对象的区别？**

两种创建对象的方法都可以创建对象，但在实践中，更加倾向于使用对象字面量的方式。





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