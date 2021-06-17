### 认识json

2006年，Web开发领域的权威Douglas Crockford在国际互联网工程任务组确定了Javascript对象简谱标准，即JSON标准。但实际上，json在2001年就已经开始被使用了。

JSON是Javascript的严格子集，理解JSON最关键的一点，是把它当成一种数据格式，而不是一门编程语言，虽然它和Javascript很像，但是它不是Javascript，只是它们有相近的语法而已。

### 语法

JSON虽然不是一门编程语言，但是也有一些简单的语法。

JSON语法支持表示3种类型的值：

1. 简单值：字符串、数值、布尔值和null都可以在JSON中出现

<font color="#f20">undefind是一个特殊值，不可以在JSON中出现。</font>

2. 对象：JSON中的一种复杂数据类型，表示有序的键值对。每个值都可以是简单的值，也可以是复杂的类型值。

3. 数组：另外一种复杂的数据类型，数组表示可以通过数值索引来访问值的有序列表。数组的值可以是任意类型，包括简单值、对象以及数组。

> JSON中没有变量、函数或对象实例的概念，JSON中的所有记号仅仅是为了表示结构化的数据，虽然它和借用了Javascript语法，但是它不是Javascript，不要和Javascript混淆。

### 简单值

简单值，就是Javascript中简单的数据类型值，如数值、字符串、布尔值、null，注意，没有undefined。如下面的都是合法的JSON值:

23,"Hello world"这些都是合法的JSON值。

布尔值true、false和null本身是有效的JSON值，但是一般的情况下很少直接使用这些值来直接作用JSON值来出现，因为JSON通常用来表示复杂的数据结构。

#### Javascript字符和JSON字符串的区别

Javascript字符串可以是单引号，也可以是双引号，JSON字符串必须是双引号（如果JSON中使用了单引号，会报语法错误）。

