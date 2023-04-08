### 1. Javascript基础

#### 1.1 简介

**Javascript的发展历史**

1992年，Nombas公司Cenvi项目中的ScriptEase

1995年Netscape Navigator 2.0开发了LiveScript

Netscape Navigator 3.0将LiveScript命名为Javascript

随后微软开发出了JScript

> Javascript不是由微软开发的

**简单认识Javascript**

Javascript是一门解释型脚本语言，不是编译型语言，开发的js代码不需要经过编译器的编译可以直接运行。

Javascript是一种基于对象的语言，同时也可以理解为面向对象的语言。js编程中，可以使用自己已经创建好的对象。

javascript是一门弱类型语言，具有足够的安全型，因为js不允许访问本地磁盘。

**Javascript的特点**

是一门脚本语言

基于对象

简单性

安全性

动态的

跨平台的

**script代码的引用**

javascript代码在网页中放在<script></script>标记中，<script>标记不是自闭合标签，不能通过下面方式使用。

```html
<script src="" /><!-- 不能通过这种方式使用，<script>不是自闭合标签 -->
```

**js代码的引用方式有如下几种方式**

1. 放在html中的<script>标记中

```html
<script>
    function hello(){
        alert("hello!");
    }

    hello();
</script>
```

2. html中通过script标记的src属性导入外部的js文件

```html
<script src="../js/util.js"></script>
```

3. 嵌入到html标记中

```html
<body onload="alert('hello world!');"></body>
<input type="text" onblur="alert(this.value)" /> <!--表示在input失去焦点的时候弹出当前输入框的值-->
```

4. 可以在a标记中的href属性中通过javascript:的方式使用嵌入js代码

```html
<a href="javascript:alert('hello world,a标记');">弹出</a>
```

#### 1.2 js程序调试

1. alert调试

```html
<script>
    x = 10;
    alert(1);
    document.write("", +x);
    alert(2);
</script>
```
可以通过两个提示框的方式判断x的操作是否成功

alert会中断程序的执行，在当前的alert执行完成后才会继续执行后续语句

2. console调试

console.log不会中断程序的执行，它只是在控制台打印信息，不影响程序的执行。

console.assert():会判断一个表达式的真假，如果为假，则输出异常信息，并抛出异常

```html
<script>
    var result = 1;
    console.assert(result);
    var year = 2022;
    console.assert(year === 2028);
</script>
```

效果如下:

![console.assert调试抛出异常](./images/i1.png)

3. 断点调试

![chrome浏览器调试面板的功能按钮](./images/i2.png)

4. 在代码中添加debugger语句实现断点

在代码中添加debugger调试，注意在调试完成之后需要把该语句debugger删除掉

#### 1.3 语法基础

**标识符**

js中，为各种变量、函数、类等起的名字，就是标识符

**标识符的规则**

字母、数字、下划线、$组合而成

标识符不能以数字开头

大小写敏感，长度无限制

不能使用系统预留字、关键字

**注释**

注释有两种

// ：单行注释

/* */：多行注释

#### 1.4 数据类型

javascript中的数据类型主要包括三大类：

**基本类型**

数值、字符串、布尔类型

**引用类型**

也称为对象类型，如数组、Object

**特殊类型**

undefined、null

**typeof检测变量的数据类型**

未定义：undefined --- name除外，name在部分浏览器中是window的全局属性

布尔值：boolean

字符串：string

NaN、数值：number

数组、对象或null：object

function定义的函数、函数表达式、箭头函数等各种方式定义的函数：function

```html
<script>
    function sum(a, b) {
        return a + b;
    }
    const arr = [];
    const add = (a, b) => {
        return a + b;
    }
    const increase = function (a, b) {
        return a + b;
    }
    console.log("typeof 未定义的变量username:", typeof username); // undefined
    console.log("typeof 函数:", typeof sum); // function
    console.log("typeof 箭头函数:", typeof add); // function
    console.log("typeof 变量函数:", typeof increase); // function
    console.log("typeof undefined:", typeof undefined); // undefined
    console.log("typeof null:", typeof null); // object
    console.log("typeof 数组:", typeof arr); // object
    console.log("typeof NaN:", typeof NaN); // number
</script>
```

> 这里可以关注下window的属性，window的属性都不能直接作为普通的标识符使用，window下的全局变量很多，可以通过打印window属性来查看下。

数值型就是表示实数，即整数和浮点数
##### 1.4.1 整数的表示形式

**十进制整数**

0-9的10个阿拉伯数字表示，如0，10，15，-12

**八进制整数**

以0开头、由0-7的8个阿拉伯数字表示，如022，031

**十六进制整数**

以0x或者0X开头，由a-f6个字母以及0-9的10个数字表示，如0x12，0x26

##### 1.4.2 浮点数的表示形式

**十进制浮点数**

由数字和小数点组成: 12.3,123.5

**科学计数法**

较大的数会使用到科学计数法，如1.235e3表示1.235x10<sup>3</sup>

**八进制浮点数**


**十六进制浮点数**

#### 小结
**数据类型**

Javascript中的数据类型分为三大类:基本类型(数值型、字符串和布尔型)、引用类型(也称为对象类型)、特殊类型(undefined和null)

变量的作用域指变量的可见性。javascript中的变量作用域分为全局变量和局部变量。

一个完整的javascript程序由3部分组成:核心(ECMAScript)、浏览器对象模型(BOM)和文档对象模型(DOM)。

**以下变量具有全局的作用域**

所有定义在最外层的变量 --- 非函数体内部

未定义而直接赋值的变量

所有window对象的属性

**在函数体内通过var、let、const关键字定义的变量是局部作用域变量，只在函数内部生效**

### 2. 流程控制与异常处理

### 3. javascript对象

### 4. 文档对象模型

### 5. 浏览器对象模型

### 6. Nodejs与ajax

### 7. jquery应用

### 8. 综合应用案例