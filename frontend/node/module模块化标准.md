### 前端模块化四大规范

在js发展的早期,一直都没有自己的模块化方案,没有办法将一个大的程序、文件拆分成若干个小文件,然后再用简单的方法拼接.其他众多开发语言都有类似功能,如Ruby有require机制,Python有import机制,css也有@import.但是js没有类似的支持,在一些大型、复杂的项目中形成了很大的障碍.

在ES6之前,社区制定、推出了一些模块化方案,也得到了很大范围的推广和应用,如应用于服务端的CommonJS(CJS),以及应用于浏览器端的AMD.ES6在语言标准的层面上,实现了模块功能,而且实现的相对简单,完全可以取代社区推出的且已经应用很广泛的CommonJS和AMD规范,称为浏览器端和服务端通用的模块化解决方案.

在前端领域的模块化规范常用的有4个,分别为:CommonJs、AMD、CMD、ES6模块,除此之外用的相对较多的还有UMD和SystemJS.

#### CommonJS

CommonJS和AMD都是社区推出的模块化方案,并不是语言上的标准.

#### AMD

#### CMD

#### ES6模块

ES6模块的设计思想是尽量的静态化,在代码编译阶段就能确定模块之间的依赖关系,以及模块的输入、输出变量.这点和CommonJS以及AMD的模块化标准,有很大的区别,CommonJS和AMD都只能在运行时才能确定模块之间的依赖关系,如CommonJS模块就是对象

##### 概述

ES的模块化分为导出(export)和导入(import)两个模块

ES6中,一个模块就是一个独立的文件,该文件内部所有的变量,包括函数、方法、变量、常量,外部都无法获取.如果希望外部文件使用该文件内的变量,就必须使用export关键字导出该变量.

export在导出变量的时候,通常情况下导出的就是变量本来的、原来的名字,但是也可以为export通过as关键字起别名导出.

**export**

export导出模块的要求:

1. 先声明后导出;

2. 要和模块内的变量一一对应;

3. 不能直接导出值;

```js
// 导出变量
export const firstName = "Nicholas";
export const lastName = "Zakas";
export const year = 2012;

// 导出函数
export function add(a, b) {
  return a + b;
}

// 导出类
export class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  setName(name){
    this.name = name;
  }
  getName(){
    return this.name;
  }
}

/**
 * as别名
 * 通过as为变量起别名的方式导出、输出
 */
function multiply(a, b) {
  return a * b;
}
export { multiply as multiplyTwo }
```
上面的案例,使用export直接导出类变量,也可以使用大括号指定一组要输出变量.这两种导出变量的作用是等效的,但是使用大括号集中输出变量的方式可以更加直观的看出该模块中输出了哪些变量,个人推荐使用大括号集中输出变量的写法.但是不反对使用export直接导出变量的方式.

```js
// 默认导出
const firstName = "Nicholas";
const lastName = "Zakas";
const year = 2012;

// 导出函数
function add(a, b) {
  return a + b;
}

// 导出类
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  setName(name) {
    this.name = name;
  }

  getName() {
    return this.name;
  }
}

// 使用as为变量别名导出后,通过import导入的是就需要使用别名导入,不能使用变量原来的名了
export { firstName as xing, lastName as ming, year, add as jia, Person };
```

> export指令必须与模块内的变量是一一对应的关系,不能通过export直接导出模块内的值.

```js
/**
 * export需要与模块内的变量一一对应,不能直接导出值
 */
export 1; // 直接导出值,报错
const m = 1;
export m; // 还是直接导出值,报错
```

<img src="./images/i16.png" alt="export直接导出值,报错" width="500" />

默认导出  export default

```js
// 1. 先声明,后导出
function add(a,b){
  return a + b;
}
export default add;

// 先声明后导出,也可以是厦下面的这种写法
export default function add(a,b){
  return a + b;
}

// 2. 导出的函数可以匿名
export default function(a,b){
  return a + b;
}

// 3. export default 后不能直接导出const|let|var 声明变量的,变量声明和导出需要分开两个步骤
export default const age = 12; // 这样是不可以的,会报错,可按照如下方式修改

const age = 12;
export default age;
```

1. 一个模块只能有一个默认导出,即一个文件中只能使用一次export default

2. 一个文件可以导出包含expert default在内的多个成员变量

3. export default后不能直接导出const|let|var 声明变量,变量声明和导出需要分开为2个步骤;如果需要导出多个变量,可以封装到一个对象中

```js
const userAge = 16;
export default userAge;
```

**import**

1. 通过export导出的,需要时import {}的方式导入

```js
import {userAge} from "./md.js"
```

2. 通过export default方式导出的模块,导入的名字可以任意

```js
// 导出
const age = 16;
export default age;

// 导入
import aa from "./md.js"
console.log(aa)
```

3. import * as 的方式导入整个模块导出的变量

导入导出文件内所有的导出变量,然后可以通过点(.)的方式访问导出变量

```js
// 导出文件 ma.js
// 导出变量
export const firstName = "Nicholas";
export const lastName = "Zakas";
export const year = 2012;

// 导出函数
export function add(a, b) {
  return a + b;
}

// 导出类
export class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  setName(name){
    this.name = name;
  }
  getName(){
    return this.name;
  }
}

// as别名
function multiply(a, b) {
  return a * b;
}
export { multiply as multiplyTwo }

// 导入&使用
import * as info from "./ma.js"
info.multiply(3,4);
```

<img src="./images/i17.png" width="500" />

4. 别名导入

es6模块可以通过export as的语法导出模块别名,import也可以通过import 变量名 as 新变量名 的方式为导入的模块重命名

```js
import {add as addtion } from "./ma.js";
addtion(3,5);
```

##### 特点

- ES6的模块化自动开启严格模式,无论模块顶部是否加入了"use strict"声明;

- 模块中可以导出和导入各种类型的变量,如函数、对象、字符串、数字、布尔值、类等;

- 每个模块都有自己的上下文,每个模块内部声明的变量都是局部变量,不会污染全局作用域;

- 每个模块只加载一次(单例模式),如果再次加载同一个目录下的同一个文件,那么会直接从内存中读取;

**ES6模块与CommonJS模块有什么不同?**

当CommonJS模块化中使用require(path)导入一个模块时,CommonJS会将path模块运行一遍,并返回一个对象,然后将这个对象缓存起来,这个对象包含path模块的所有API.以后无论多少次加载这个path模块但是取的值都是缓存起来的值,也就是第一次运行时的结果,除非手动清除.

ES6使用import导入path模块时,只会加载path模块中的3个方法,其他的方法不会加载,这就是编译时加载.ES6可以在编译时就完成模块的加载,当ES6遇到import时,不会像CommonJS去完整的执行一遍这个被引入的模块,然后把这个模块去缓存下来,而是生成一个动态的只读引用,当真正需要的时候再去模块里去取相应的值.

ES6中每个文件是一个模块,或者说一个模块就是一个独立的文件,但是该文件不可被直接引用,因为ex6中通过export导出的并不是模块本身,而是模块中的变量.该变量包括函数、方法、类、定义的变量、常量等.

### UMD和SystemJS

