### var、let、const

var，是之前ES标准的变量声明关键词，现在不建议继续使用了。

var：有变量提升、初始化的提升，值可以在使用中改变，它声明的是变量；它只是声明的提升，赋值没有提升；

let：没有变量声明的提升，在哪里声明的就是在那个节点之后才可以使用，值可以在代码逻辑中改变，它声明的也是变量；

const：没有变量声明的提升，同let，只有在声明的地方之后才可以使用，在代码的一个执行周期中，其值不可以变，所以它声明的是一个常量。

> var和let、const的非常明显的一个区别，就是var可以在一个作用域内重复声明多次，最终的结果是以最后的一次声明为准，最后的一次声明会覆盖前面的声明；而let、const在同一个作用域内对同一个变量只能声明一次，否则会报异常。

> 暂时性死区：javascript在ES6之后，有了2个新的声明变量的关键词let和const，这两个关键词声明的变量在声明之前是禁止使用的，如果硬要使用会报错。这个现象被称为暂时性死区。

```javascript
var userName = "Nicholas";

function fn(){
    console.log(userName);  // 异常了，Uncaught ReferenceError: Cannot access 'userName' before initialization，暂时性死区了
    let userName="LiKaifu";
}

fn();
```

#### 块级作用域

在ES6之前，Javascript只有全局作用域和函数作用域，从ES6标准开始，引入了一个新的作用域概念：块级作用域，以大括号{}标识。

