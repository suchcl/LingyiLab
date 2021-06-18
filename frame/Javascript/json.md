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

#### JSON中的对象值

JSON中的对象于Javascript中的对象字面量很像，相像程度几乎就一模一样了。我们先看下Javascript中的对象字面量：

```javascript
let person = {
    name: "LiLei",
    age: 16
};
```
 
这是一个javascript的对象字面量，它首先声明了一个变量，然后语句的结尾部分使用了分号（虽然分号可有课无，但是建议还是加上）；再就是对象中最后一个属性的后面没有了逗号；这个对象的属性名没有引号，无论是单引号，还是双引号（javascript中的标准，属性名是可以加引号的，无论单引号还是双引号）。这是这个对象字面量的一些特点。

我们再来看一个标准JSON对象的实例：

```json
{
    "name": "Nicholas",
    "age": 16
}
```

这个标准JSON的特点，是没有声明变量，最后没有分号，两个属性名都加了引号。在JSON中，是没有变量、函数的概念的，而且JSON是一种数据格式，不是一门编程语言，所以这不是语句的结束，也不需要分号来结束了。另外，json中最后一个字段结束后不需要添加逗号；属性值也可以是一个对象，如：

```json
{
    "name": "Nicholas",
    "age": 16,
    "job":{
        "title": "Teacher",
        "salary": 2315
    }
}
```

#### json中的数组值


还是用两个案例来表示吧，先来看js中的数组：

```javascript
let arr = [16,"apple",true];
```

这是一个合法的js数组，再来看下json中的数组表现：

```json
[16,"apple",false]
```

这是合法的json数组，它们两个的区别，还是变量的声明，以及结束部分的分号，原因和对象部分相同。

数组的数据结构使用的频率最高，可以表示非常复杂的数据结构。

```json
[
  {
    "resourceData": {
      "code": "0103000",
      "data": {
        "blockName": "PC狐首飘红大皮肤",
        "content": [
          {
            "startTime": "2021/03/03 09:00:00",
            "endTime": "2021/03/12 11:00:00",
            "bg": "//5b0988e595225.cdn.sohucs.com/images/20210302/b994e3c0d4cc474282e50bb4c7724620.png"
          }
        ],
        "createTime": 0,
        "id": 819886343755857900,
        "isValid": 0,
        "resourceName": "",
        "sceneId": 758676716649644000,
        "targetResourceId": 758678068196999200,
        "updateTime": 0
      },
      "message": "请求成功",
      "scm": "",
      "spm": "",
      "status": 0,
      "timestamp": "2021-06-17 23:27:56"
    },
    "resourceType": 4
  }
]
```

### JSON和Javascript的区别

1. 字符串的区别

Javascript的字符串可以是单引号，也可以是双引号；

JSON中的字符串必须是双引号，如果是单引号会报语法错误。

2. 对象值的区别

javascript对象，需要声明一个变量，用来存放这个对象；而声明字面量对象的代码，是一个语句，语句的结束需要加上分号（可以加上，不是强制，加上好可读性更高）；对象的属性可以加分号，也可以不加分号，都是符合要求规范的；

JSON对象，不需要声明变量；代码不是语句，就是一种数据格式，一段代码的结束不需要分号；属性名必须要使用双引号（使用单引号会报语法错误）

3. 数组值的区别

JSON中的数组型数据，不需要声明变量，结束不需要分号。


### JSON解析器

JSON有2个方法：stringify()和parse()。

stringify()将js序列化为json对象，parse()将json解析为js值。

