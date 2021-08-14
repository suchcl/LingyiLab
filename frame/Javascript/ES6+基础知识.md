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

#### 默认参数作用域与暂时性死区

ES5.1及以前的版本中，给函数定义默认参数的方式就是检测某个参数是否为undefined，如果是undefined，则意味着没有这个参数，那么给它传递一个默认值。

```javascript
function defaultParam(uname) {
    var uname = (typeof uname != "undefined") ? uname : "Nicholas";
    console.log(uname);
}

defaultParam(); // 输出Nicholas，因为没有给defaultParam()函数传递有效的参数
defaultParam("Lalala"); // 输出Lalala，因为给函数defaultParam()传递了一个有效的参数值“Lalala”
```

在ES5.1及之前版本中，我们可以按照上面的方式，但是到了ES6标准后，就不需要上面的方式了，有更简单的方式。

```javascript
function setDefaultParam(uname="Nicholas"){
    console.log(uname);
}

setDefaultParam(); // 输出Nicholas，没有给函数传递参数值，形参uname就取用了默认值Nicholas
setDefaultParam("Nigula"); // 输出Nigula，给函数传递了一个参数值Nigula
```

ES6标准中，在函数参数列表中设置默认参数和在函数体中使用let声明变量的效果是一样的，只不过默认值除了声明了变量外，还初始化了值。默认参数会按照它们的顺序依次被初始化。

```javascript
// 下面两个函数是等价的，形参在函数的参数列表中
function setDefaultParam(uname = "Nicholas") {
    return uname;
}

// 函数的带有参数默认值的形参，和在函数体中声明变量的效果等价
function setDefaultParam() {
    let uname = "Nicholas";
    return uname;
}
```

因为在ES6以后的标准中，已经不再推荐使用var了，所以我们也就不要再使用了。但是在使用let声明变量的时候，要注意看函数的形参列表中是否已经有了同名的变量，如果有同名的变量，会报异常：Uncaught SyntaxError: Identifier 'uname' has already been declared，所以又一个不成文的良好的编程实践是在一个作用域内，不要声明同名变量，无论是使用var、let、const的任何一个关键词，也无论是在函数的参数列表或者函数体中。

```javascript
// 这种方式在Es6标准中国是会报异常的，因为函数参数列表中的参数名和函数体中的变量名同名了
function setDefault(uname, age) {
    let uname = uname;
    let age = age;
    return [uname, age];
}
```

但是如果把代码中声明变量的方式有let改为var就可以了，但是在实践中不建议这么改。let不能声明同名变量，var可以，只是后面的覆盖前面的。

```javascript
function setDefault(uname, age) {
    var uname = uname;
    var age = age;
    return [uname, age];
}
```

一定注意下面的代码是一定不行的，前辈们不小心的时候可能会有这样的习惯，入行新人应该不会有这样的习惯了。在ES6之前的版本中，在没有let的时候，这是一种很常见的设置默认值的方法。现在尤其是要注意的是声明变量的关键词let。

```javascript
function fn(name, age) {
    let name = name || "Nicholas";
    let age = age || 12;
    return [name, age];
}
```

### 扩展运算符

ES5.1及以前，我们在合并数组的时候，常用的方法可能是使用concat、或者遍历数组，将要合并的数组项依次添加到目标数组中：

```javascript
// 使用concat合并数组
function mergeArray() {
    let arr = [1, 2];
    let arr2 = [3, 4];
    let arr3 = [5, 6];
    let newArr = arr.concat(arr2).concat(arr3);
    return newArr;
}

// 通过遍历数组的方式，将一个数组的数组项依次添加到另一个数组中
function eachMergeArr() {
    let arr = [1, 2];
    let arr2 = [3, 4];
    for (let i in arr2) {
        arr.push(arr2[i]);
    }
    return arr;
}
```

ES6标准引入了扩展运算符(...)的概念，我们可以通过扩展运算符来快速合并数组。

```javascript
function extendMerge(){
    let arr = ["a","b"];
    let arr2 = ["c","d"];
    let newArr = [...arr,...arr2];
    return newArr;
}
console.log(extendMerge()); // ["a", "b", "c", "d"]
```

#### 对象合并

对象合并和数组合并有着同样的方式，直接看案例吧：

```javascript
// 原来通过assign的方式合并对象
function asObj() {
    let obj1 = { a: 1 };
    let obj2 = { b: 2 };
    let obj3 = { c: 3 };
    let newObj = { es: "demo" };
    let targetObj = Object.assign({}, obj1, obj2, obj3);
    return targetObj;
}

console.log(asObj()); // {a: 1, b: 2, c: 3}


// 通过扩展运算符来合并对象，和合并数组的方式相同
function restObj() {
    let obj = { a: 1 };
    let obj2 = { b: 2 };
    let newObj = {...obj,...obj2};
    return newObj
}
console.log(restObj()); // {a: 1, b: 2}
```

### 剩余参数

剩余参数符号和扩展运算符相同，都是...。在编码中可能会遇到向一个函数传入的参数个数不固定，这个时候我们可以使用剩余参数统一表示。

剩余参数，都会体现在一个数组里面.

```javascript
function params(param, ...params) {
    console.log(param);
    console.log(params);
}
params(1); // 1,[]
params(1, "苹果"); // 1,["苹果"]
params(1, "苹果", ["大众", "别克", "理想汽车"]); //1,["苹果",["大众", "别克", "理想汽车"]]
params("苹果", 1, 2, 3, 4); // "苹果",[1,2,3,4]
params(1, "苹果", ["大众", "别克", "理想汽车"], { uname: "Nicholas" }); // 1,["苹果",["大众", "别克", "理想汽车"],{uname: "Nicholas"}]
```
### 模板字符串

以前（ES6标准及以前）我们在拼接字符串的方式是使用+拼接，参考下面demo：

```javascript
function spliceString(){
    var name = "Nicholas";
    var age = 18;
    var job = "programmer";
    var userInfo = "我的名字叫" + name + ",今年" +　age + "岁，我的职业是" + job + "。";
    return userInfo;
}
console.log(spliceString()); // 打印出：我的名字叫Nicholas,今年18岁，我的职业是programmer。
```

从ES6标准开始，引入了模板字符串(template string)的概念，模板字符串是增强版的字符串，用反引号(数字键1前面的那个引号)标识。模板字符串可以当做普通字符串去使用，也可以定义多行字符串（可以定义多行字符串的意思就是定义的多行字符串在输出的时候原样输出），也可以在模板字符串中嵌入变量。

定义多行字符串demo：

```javascript
function tempString(){
    let desc = `这里开始
换行了, 
    又换了一下`;  // 这一行在输出的时候，前面会空出2个空格， 因为这前面的空格也会被当作是字符串的一部分；上面一行输出时顶头输出
    return　desc;
}
console.log(tempString());
```

> 上面的demo注释都放到字符串结束后的，因为在字符串没有结束的第二行是不可以注释的，这一细节，以前没有注意过

模板字符串嵌套变量demo：

```javascript
function variInTempString(){
    let uname = "Nicholas";
    let age = 26;
    let userInfo = `我的名字是${uname},我今年${age}岁。`;
    return userInfo;
}
console.log(variInTempString()); // 我的名字是Nicholas,我今年26岁。
```

在模板字符串中嵌入变量，使用$表示，然后将变量用{}包裹即可。

从demo可以看出来，使用模板字符串功能更加强大，代码更加优雅，在我们的代码中可以更多的实践。

### 获取对象属性 Object.keys()

以前在js中，也可以获取到对象的属性，使用方法Object.getOwnPropertyNames(obj),在ES6的标准里，新增了Object.keys(obj)方法来获取对象的属性，也叫key。

```javascript
function getKeys(){
    let obj = {
        name: "Nicholas",
        age: 16,
        gender: "Male"
    };
    let keys = Object.getOwnPropertyNames(obj);
    return keys;
}
console.log(getKeys()); // ["name", "age", "gender"]

function getKeys2(){
    let obj = {
        name:"Nicholas",
        age: 18,
        gender: "Male"
    };
    let keys = Object.keys(obj);
    return keys;
}
console.log(getKeys2()); // ["name", "age", "gender"]
```

两种方法都取到了对象的属性，也可以说是key。

> 明天去确认下Object.getOwnPropertyNames(obj)和Object.keys(obj)的区别，以及对象中属性和key的区别。

### 箭头函数

箭头函数是ES6标准中新增的一种函数类型，允许使用箭头(=>)来定义函数。如：

```javascript
var f = v => v;
// 上面的箭头函数等同于下面的方式
var f = function(v){
    return v;
}
```

箭头函数如果没有参数或者有多个参数，那么使用小括号来代表参数部分：

```javascript
// 没有参数demo
let fn = () => "Nicholas"; // 没有参数，等同于下面方式

let fn = function () {
    return "Nicholas"
}

// 有多个参数
let multipleParams = (num1, num2) => num1 + num2;
console.log(multipleParams(1, 2)); // 3
```

在箭头函数中，如果函数体有多条语句，那么函数体就要使用大括号包裹起来。

```javascript
let multipleParams = (num1, num2) => { return num1 + num2; }
```

由于大括号在ES6标准中被解释为代码块，如果箭头函数直接返回的是一个对象，那么就需要在对象的外面包裹一层小括号：

```javascript
let fn3 = (obj) => ({
    uname: "Nicholas",
    age: 20,
    gender: "Male"
});
console.log(fn3()); // {uname: "Nicholas", age: 20, gender: "Male"}
```

如果我们把直接返回的对象赋值给一个变量返回，则就不需要最外层的小括号包裹了：

```javascript
let fun2 = (obj) => {
    obj = {
        uname: "Nicholas",
        age: 18,
        gender: "Male"
    };
    return obj;
}
console.log(fun2()); // {uname: "Nicholas", age: 18, gender: "Male"}
```

箭头函数和普通函数的区别：

1. 箭头函数不可以作为构造函数，不能使用关键词new来实例化对象；
2. 箭头函数没有自己的this；
3. 箭头函数没有arguments对象；
4. 箭头函数没有原型对象；