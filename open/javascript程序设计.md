### 1. Javascript基础

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
<script src="" /><!--不能通过这种方式使用，<script>不是自闭合标签-->
```

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