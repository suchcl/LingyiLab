<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1.再学ts](#1%E5%86%8D%E5%AD%A6ts)
  - [1.1 简单认识Typescript](#11-%E7%AE%80%E5%8D%95%E8%AE%A4%E8%AF%86typescript)
  - [1.2 为什么要使用Typescript](#12-%E4%B8%BA%E4%BB%80%E4%B9%88%E8%A6%81%E4%BD%BF%E7%94%A8typescript)
  - [1.3 应该怎么去学习typescript？](#13-%E5%BA%94%E8%AF%A5%E6%80%8E%E4%B9%88%E5%8E%BB%E5%AD%A6%E4%B9%A0typescript)
- [2. Typescript基础](#2-typescript%E5%9F%BA%E7%A1%80)
  - [2.1 强类型与弱类型](#21-%E5%BC%BA%E7%B1%BB%E5%9E%8B%E4%B8%8E%E5%BC%B1%E7%B1%BB%E5%9E%8B)
  - [2.2 静态类型语言和动态类型语言](#22-%E9%9D%99%E6%80%81%E7%B1%BB%E5%9E%8B%E8%AF%AD%E8%A8%80%E5%92%8C%E5%8A%A8%E6%80%81%E7%B1%BB%E5%9E%8B%E8%AF%AD%E8%A8%80)
  - [2.3 ts基础](#23-ts%E5%9F%BA%E7%A1%80)
  - [2.4 ts的数据类型](#24-ts%E7%9A%84%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B)
  - [2.5 类型注解](#25-%E7%B1%BB%E5%9E%8B%E6%B3%A8%E8%A7%A3)
  - [2.6 接口](#26-%E6%8E%A5%E5%8F%A3)
  - [2.7 函数](#27-%E5%87%BD%E6%95%B0)
  - [2.8 函数重载](#28-%E5%87%BD%E6%95%B0%E9%87%8D%E8%BD%BD)
  - [2.9 接口定义函数](#29-%E6%8E%A5%E5%8F%A3%E5%AE%9A%E4%B9%89%E5%87%BD%E6%95%B0)
  - [2.10 混合类型接口](#210-%E6%B7%B7%E5%90%88%E7%B1%BB%E5%9E%8B%E6%8E%A5%E5%8F%A3)
  - [2.11](#211)
- [3. 泛型](#3-%E6%B3%9B%E5%9E%8B)
  - [3.1 泛型函数](#31-%E6%B3%9B%E5%9E%8B%E5%87%BD%E6%95%B0)
  - [3.2 泛型接口](#32-%E6%B3%9B%E5%9E%8B%E6%8E%A5%E5%8F%A3)
  - [3.3 泛型类与泛型约束](#33-%E6%B3%9B%E5%9E%8B%E7%B1%BB%E4%B8%8E%E6%B3%9B%E5%9E%8B%E7%BA%A6%E6%9D%9F)
- [4. 类](#4-%E7%B1%BB)
  - [4.1 类的继承和成员修饰符](#41-%E7%B1%BB%E7%9A%84%E7%BB%A7%E6%89%BF%E5%92%8C%E6%88%90%E5%91%98%E4%BF%AE%E9%A5%B0%E7%AC%A6)
  - [4.2 类的继承](#42-%E7%B1%BB%E7%9A%84%E7%BB%A7%E6%89%BF)
  - [4.3 类的修饰符](#43-%E7%B1%BB%E7%9A%84%E4%BF%AE%E9%A5%B0%E7%AC%A6)
  - [4.4 抽象类](#44-%E6%8A%BD%E8%B1%A1%E7%B1%BB)
  - [4.5 类与接口的关系](#45-%E7%B1%BB%E4%B8%8E%E6%8E%A5%E5%8F%A3%E7%9A%84%E5%85%B3%E7%B3%BB)
  - [4.6 接口的继承](#46-%E6%8E%A5%E5%8F%A3%E7%9A%84%E7%BB%A7%E6%89%BF)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 1.再学ts

#### 1.1 简单认识Typescript

js是一门动态的弱类型语言，没有类型的约束。

Ts可以完全的被编译为javascript，学习ts的时候，需要注意3个要点：

1. 类型检查

ts会在编译时进行类型检查，这就意味着可以在编译阶段排除掉语法错误。

2. 语言扩展

ts会包括来自ES6以及未来提案中的特性如异步操作和装饰器，也会从其他语言借鉴某些特性，如接口和抽象类。

3. 工具属性

ts可以编译成标准的javascript，可以在任何浏览器、操作系统上运行，无需任何运行时的额外开销。从这个角度上来讲，ts更像是一个工具，而不是一门编程语言。

#### 1.2 为什么要使用Typescript

1. vscode编辑器的强大自动补全、导航和重构功能，使得接口定义可以代替文档；

2. 同时可以提高开发效率；降低维护成本；

3. 可以帮助团队重塑“类型思维”，接口的提供方将被迫去思考API的边界，他们将从代码的编写者蜕变成代码的设计者。

如果javascript是一匹野马，那么typescript就是束缚这匹野马的缰绳；

#### 1.3 应该怎么去学习typescript？

循序渐进，基础（语法基础） -> 工程（做项目） -> 实战（还是做项目）

### 2. Typescript基础

#### 2.1 强类型与弱类型

什么是强类型语言呢？其实在很早之前，有一些计算机方面的科学家给出了一些解释：

> 在强类型语言中，当一个对象从调用函数传递到被调用函数时，其类型必须与被调用函数中声明的类型兼容。

```javascript
function a(){
    b(x);
}

function b(y){
    // ……
}
```

如案例中，函数a中调用了函数b，那么被调用的函数b中的参数x的类型，要和b函数定义时的参数y的类型保持一致，且程序应该运行良好。

后来关于强类型的定义又做了一些完善和具体：

> 强类型语言，不允许改变变量的数据类型，除非进行强制的类型转换。

以java为例，参考一下：

```java
import java.io.*;
class test  
{
	public static void main (String[] args) throws java.lang.Exception
	{
		int x = 1;
		boolean y = true;
		x = y;
		System.out.println(x);
	}
}
```

代码在运行时会报错，提示boolean型不能被转换为整型。

```java
import java.io.*;
class test  
{
	public static void main (String[] args) throws java.lang.Exception
	{
		int x = 1;
		boolean y = true;
// 		x = y;
        char z = 'a';
        x = z; // 这里没有报错，正常的输出了97，因为java进行了强制的类型转换
		System.out.println(x);
	}
}
```

> 弱类型语言：变量可以被赋值给、赋予不同的数据类型。

如js就是弱类型的编程语言，同一个变量可以被赋值不同类型的值。

强类型语言，有严格的限制，不同的数据类型之间不能进行赋值，除非进行了强制的数据类型的转换。

强类型语言，有一个好处，就是避免了很多不必要的错误。

#### 2.2 静态类型语言和动态类型语言

静态类型语言：在编译阶段确定所有变量的类型；

动态类型语言：在执行阶段确定所有变量的类型。

看案例：

```javascript
class C{
    constructor(x,y){
        this.x = x;
        this.y = y;
    }
}

function add(a,b){
    return a.x + a.y + b.x + b.y;
}
```

当js编译器看到这段代码的时候，它是不会知道类C和函数add中的参数的数据类型的，只有在实例化了类C和调用了add函数的时候，给类C的构造函数和add函数传递进来参数了，编译器才会知道函数的参数的具体的数据类型。

在来看一段C++的具有同样功能的代码：

```c
class C{
    public:
        int x;
        int y;
}

int add(C a,C b){
    return a.x + a.y + b.x + b.y;
}
```

C++的编译器在编译时，就已经知道了add函数参数的数据类型了，肯定是整型。

下面看一下在内存存储上的区别：

![动态类型语言和静态类型语言在内存存储上的区别](./images/i15.png)

| 静态类型语言       | 动态类型语言                    |
| ------------------ | ------------------------------- |
| 对类型要求极度严格 | 对类型要求非常宽松              |
| 可以立即发现错误   | Bug可能隐藏很长时间，不易被发现 |
| 运行时性能良好     | 运行时性能差                    |
| 自文档化           | 可读性差                        |

动态类型语言的支持者认为：

1. 性能是可以改善的，如V8引擎，而语言的灵活性更重要；
2. 隐藏的错误，可以通过一些技术手段去发现如单元测试；
3. 文档可以通过工具生成；

动态类型语言和静态类型语言的争论一直在争论中，但是没有一个明确的结论。每种语言都有自己的可取之处，同时也可能会存在一些不足。

**其他的一些争议，或者叫讨论吧**

一些学者，把强类型语言定义为：不允许程序发生错误后继续执行

那么按照这个标准，C/C++是就应该是弱类型语言了，它没有对数组的越界进行检查？那么这两门语言到底是强类型还是弱类型语言呢？

下面来补一张常识图：

![强类型和弱类型语言象限图](./images/i16.png)

#### 2.3 ts基础

刚开始学习ts的时候，不要安装太多工程化的东西，只需要有简单的编辑器和node环境支持即可。

**环境搭建**

全局安装typescript，以便可以全局使用tsc指令

```bash
npm install typescript -g
```

初始化一个ts项目

```bash
mkdir welcome
cd welcome
npm init -y # 直接忽略各种选择项吧
```

之后就可以通过执行tsc指令来查看ts的可以进行的各种配置了

可以通过tsc --init创建包含一些默认配置项的ts的配置文件：tsconfig.json

```bash
PS D:\welcome> tsc --init

Created a new tsconfig.json with:
                                                                                                                     TS
  target: es2016
  module: commonjs
  strict: true
  esModuleInterop: true
  skipLibCheck: true
  forceConsistentCasingInFileNames: true


You can learn more at https://aka.ms/tsconfig.json
```

**配置构建工具**

配置构建工具，会使用webpack

```bash
npm install webpack webpack-cli webpack-dev-server --save-dev
npm install ts-loader typescript --save-dev
```

#### 2.4 ts的数据类型

| ES6的数据类型 | TS的数据类型 |          |
| ------------- | ------------ | -------- |
| Boolean       | Boolean      | void     |
| Number        | Number       | any      |
| String        | String       | never    |
| Array         | Array        | 元祖     |
| Function      | Function     | 枚举     |
| Object        | Object       | 高级类型 |
| Symbol        | Symbol       |          |
| undefined     | undefined    |          |
| null          | null         |          |

ES6有6中基本的数据类型，Boolean、Number、String、null、undefined、Symbol

引用类型：Array、Object、Function

TS的数据类型，在ES6的基础上新增了void、any、never、元祖、枚举以及其他一些高级类型

#### 2.5 类型注解

作用：相当于强类型语言中的类型声明

语法：(变量/函数):type

对变量和函数发生约束作用。

```ts
// 原始类型
let bool:boolean = true;
let num:number = 12;
let str:string = "Hello String";

// 数组
let arr:number[] = [1,2,3];
let arr2:Array<number> = [4,5,6]; // 泛型

// 元祖
let tuple:[number,string] = [12,"Nicholas Zakas"];

// 函数
let add = (x:number,y:number):number => {
    return x + y;
}

// 对象
let obj:object = {
    x:1,
    y:2
};

// symbol
let s1:symbol = Symbol();
let s2 = Symbol();

// 多种数据类型，可以为变量dt声明了多种数据类型，可以为string类型值也可以为number类型值
let dt:string | number = 2;
dt = "hello";
```

ts中，也可以为一个变量同时声明多种类型，只需要在类型注解中用|分割多个数据类型即可，如

```ts
let dt:string | number = 10; // 变量dt可以为string类型或者number类型
```

元祖，是ts中区别于js的一种数据类型，元祖是一种特殊的数组，它限定了数组项的个数和类型。

```ts
let tuple:[number,string] = [12,"Nicholas Zakas"];
let t:[string,number,Array<number>] = ["Nicholas",18,[4,5]];
let t2:[string,number,string[]]=["Hanmeimei",16,["apple","banana"]];
let t3:[string,number,number[]] = ["LiLei",12,[3,4]];
```

这几种都是合法的元祖，需要注意的是元祖的数据类型限定中，如果是数组类型的限定，和定义数组相同，可以使用基本的数据类型加[]的方式声明，也可以通过范式的方式声明。

**元祖越界**

元祖是一种特殊的数组，它可以使用数组的方法，如遍历、插入、弹出元素等操作。

```ts
let t:[string,number,Array<number>] = ["Nicholas",18,[4,5]];
t.forEach((item) => {
    console.log(item);
});
```

元祖使用了数组的forEach方法遍历元素。

下面使用push向元祖插入元素

```ts
let t:[string,number,Array<number>] = ["Nicholas",18,[4,5]];
t.push(99);
console.log(t); // [ 'Nicholas', 18, [ 4, 5 ], 99 ]
```

从执行结果上看，成功的向元祖插入了元素。

但是这个时候需要注意，新插入的元素是访问不到的，这就是元祖的越界问题。

实际的开发中，不要越界插入元祖元素。

![越界的元祖元素不能访问](./images/i17.png)

> 可以通过数组的push等方法向元祖添加越界元素，但是越界元素不能被访问，ts编译是编译不过去的。

ts中函数声明的时候，函数可以省略类型的注解，这是利用了ts的类型推断功能。

个人的习惯中，还是不省略，养成一个良好的习惯，就是只要使用了ts写代码，就处处添加类型注解。

```ts
// 函数
let add = (x:number,y:number):number => x + y;

let increment = (x:number,y:number) => x + y;

function decrement(x:number,y:number):number{
    return x - y;
}
```

无论是箭头函数还是通过function声明的普通函数，函数的返回值类型可以省略。

```ts
// 声明了一个函数类型的变量，返回值为string，没有做实现
let compute:(x:number,y:number) => string;
// 做变量的函数的实现,做函数类型的实现的时候，形参可以不加类型注解，如a、b都没有加类型注解
compute = (a,b) => {
    return (a + b).toString();
}
console.log(compute(2,3)); // 5
```

**对象类型的限定**

ts中对象类型的注解，有点特殊，需要记一下

```ts
// 对象
let obj:object = {
    x:1,
    y:2
};
```

这样的对象类型的变量声明，在语法上按说是没有什么问题的，但是没有实际意义。

我们不能通过obj访问对象属性x或者y，因为变量obj是object类型的，但是object身上并没有x或者y这2个成员变量。所以正确的声明对象类型的变量的方式需要明确具体的成员变量及类型：

```ts
// ts中声明对象类型变量，需要明确对象的成员属性，并明确数据类型
let obj:{x:number,y:number} = {
    x: 12,
    y: 10
};
console.log(obj.x); // 12
```

**symbol**

symbol表示唯一值。

```ts
// symbol
let s1:symbol = Symbol();
let s2 = Symbol();
console.log("s1:", s1);
console.log(s1 === s2); // false
```

任何的Symbol类型的变量都是不相等的。

**undefined**

如果一个变量被声明了一个undefined类型，那么这个变量就只能被赋值undefined类型的唯一值undefined

```ts
let ud:undefined = 23; // 这里的赋值是有问题的，不能将23赋值给一个undefined类型变量
let udf:undefined = undefined;
```

![不能将其他的类型赋值给一个undefined类型变量](./images/i18.png)

**null**

null和undefined相同，如果一个变量被声明为了null类型，那么这个变量就只能被赋值null类型的唯一值null，而不能将其他的类型值赋值给null类型的变量。

> 既然其他的类型值都不能赋值给undefined、null这两个类型的变量，那么null和undefined可以赋值给其他的数据类型变量吗？

![undefined和null赋值给其他类型变量](./images/i19.png)

简单从代码上看是不行的，但是ts文档告诉我们了，undefined和null是其他类型的子类型，那么也就是说undefined和null是可以赋值给其他类型的变量的，这个时候需要在tsconfig.json配置文件进行一下简单配置：

```json
"strictNullChecks": false,  // 将strictNullChecks设置成false即可，默认是true
```

![undefined和null可以赋值给其他类型变量了](./images/i20.png)

**void类型**

在js中，void是一个操作符，它可以让任何表达式返回undefined。

void 0可以返回一个undefined。

js中的undefined不是一个保留字，我们可以自定义一个undefined代替全局的undefined

```js
console.log(void 0); // undefined
```

**any**

尽量不要是用any类型，否则就和js没有什么区别了，失去了ts的意义了。

**never**

永远不会有返回值的类型，或者死循环的语句，会返回一个never类型

```ts
let error = () => {
    throw new Error("error");
}

let endless = () => {
    while(1){} // 永远不会有返回值
}
```

**枚举类型**

来看一段代码：

```js
function initByRole(role){
    if(role === 1 || role === 2){
        // do sth
    }else if(role === 3 || role === 4) {
        // do sth
    }else if(role === 5){
        // do sth
    }else {
        // do sth
    }
}
```

这是一段角色判断的代码，这段代码，有一些问题：

1. 可读性差，除非对着文档，否则谁也不会知道各种role的码值具体是表示什么意思
2. 可维护性差：硬编码，牵一发动全身

枚举，就是一组具有名字的常量的集合。

枚举，是js中没有的数据类型。

枚举，分为数字枚举和字符串枚举。

数字枚举

```ts
// 数字枚举
enum Role{
    Reporter = 200,
    developer = 206,
    Maintainer = 300,
    Owner,
    Guest
}
```

数字枚举，值从0开始，也可以自定义值，后面的常量会在指定的值基础上自增加1

数字枚举，利用了反向映射的道理，但是字符串枚举没有反向映射。

**常量枚举**

常量枚举，不会显示在编译后的代码中。就是说常量枚举，在代码被编译成js后，什么都不会留下。

那么常量枚举有什么意义呢？就是为了给其他需要用的地方提供值。

```ts
// 字符串、常量枚举
const enum Message{
    Success = "恭喜您,您中大奖了!",
    Fail = "很遗憾,本次没哟中奖"
}
console.log(Message.Success);
```

从代码中我知道有什么样的提示信息，但是编译为js后不会留下任何信息，可读性高，好维护。

**异构枚举**

字符串枚举和数字枚举，构成了异构枚举，不建议使用。

> 将程序中不易维护的硬编码，都可以使用枚举

####  2.6 接口

接口，可以用来约束对象、函数以及类的结构和类型，这是一种代码协作的契约，开发者必须要遵守且不能改变。

**定义对象类型接口**

定义对象类型接口，并渲染到页面的案例

```ts
interface List {
    // 定义一个只读属性id
    readonly id:number;
    name:string;
}

interface Result{
    data:List[]
}
// 渲染函数
function render(result:Result){
    result.data.forEach((item) => {
        console.log(item.id,item.name);
    });
}

// 假如从api获取到的数据
const result = {
    data: [
        {
            id:1,
            name: "Nicholas Zakas",
            gender: "male"
        },
        {
            id: 2,
            name: "Hameimei"
        }
    ]
};

render(result);
```

这种情况下，api下发的数据字段和我们interface中定义的字段完全相同，非常理想化。当然了，这段代码是可以正常执行没有任何问题的。

但是实际上，很多时候api下发的字段总是会有一些冗余字段，比如案例中给我们多下发了gender和age字段，那ts代码编译，就有问题了：

1. 如果api下发的数据赋值给了一个变量，那么代码在执行的过程中不会有什么问题，可以通过ts的编译，只是冗余的字段不会被做处理

   ```ts
   // 假如从api获取到的数据
   const result = {
       data: [
           {
               id:1,
               name: "Nicholas Zakas",
               gender: "male" // 下发的冗余字段gender
           },
           {
               id: 2,
               name: "Hameimei"
           }
       ]
   };
   ```

2. 如果api下发的数据是通过字面量的形式直接传递给使用函数的，那会报错，通不过ts的编译

   ```ts
   render({
       data:[
           {
               id:1,
               name: "Nicholas Zakas ddd",
               age: 16 // 下发了冗余的age字段,会报异常
           },
           {
               id: 2,
               name: "Hameimei"
           }
       ]
   });
   ```

   <img src="./images/i21.png" alt="接口下发冗余字段，直接赋值给执行函数，会报异常" style="zoom:67%;" />

那么出现这种情况怎么处理呢？一般情况下常用的有3种方式解决：

- 使用类型断言，告诉编译器这就是某个指定的类型

  ```ts
  render({
      data:[
          {
              id:1,
              name: "Nicholas Zakas ddd",
              age: 16 // 下发了冗余的age字段
          },
          {
              id: 2,
              name: "Hameimei"
          }
      ]
  } as Result);
  ```

- 将api下发的数据赋值给一个变量，然后通过使用变量的方式实现对数据的调用 ---- 就是前面正常的那个情况

```ts
const result = {
    data: [
        {
            id:1,
            name: "Nicholas Zakas",
            gender: "male"
        },
        {
            id: 2,
            name: "Hameimei"
        }
    ]
};
render(result);
```

- 使用泛型

```ts
render(<Result>{ // 泛型
    data: [
        {
            id:1,
            name: "Nicholas Zakas",
            gender: "female"
        },
        {
            id: 2,
            name: "Hameimei"
        }
    ]
})
```

但一般不建议使用这种方式，因为在react中有歧义

**对象类型接口**

就是用接口定义对象，包括Object和数组

**函数类型接口**

函数类型接口，就是用接口定义函数。

前面在学习ts数据类型的时候，我们知道可以通过下面的方式来定义一个函数类型：

```ts
let Sum:(x:number,y:number) => number;
```

表示声明了一个变量，该变量是一个函数类型，这个函数类型接收2个number类型参数，并且返回一个number类型的函数。这个函数类型的名称可以使用Sum来表示，说的直白一点：声明Sum为一个接收2个数字类型参数并返回一个number类型的函数。

使用接口可以实现同样的功能，即通过接口类声明一个函数类型：

```ts
interface Adds{
    (x:number,y:number):number
}
```
  
通过接口声明的函数类型需要接收2个number类型参数，且返回number的类型值，使用Adds表示这个类型。

来看下这个函数类型的实现案例：

```ts
let ads:Adds = (a,b) => a + b;
```

在使用接口可以实现这个功能，使用别名的方式，也可以实现：

```ts
// 函数类型定义,通过别名方式
type Add = (x:number,y:number) => number;
// 函数的实现
let ad:Add = (a,b) => a - b;
// 执行出了正确的结果
console.log("add：",ad(5,2)); // 3
```

**混合类型接口**

```ts
// 定义混合类型接口
interface Lib {
    // void返回值
    ():void;
    // string类型版本号
    version: string;
    // 定义一个方法
    doSth():void;
}
// 实现这个混合类型接口
let lib:Lib = (() => {}) as Lib;
lib.version = "1.0.0";
lib.doSth = () => {};
```

实际应用：

```ts
// 可以尝试封装这个单例模式的获取库版本号的方法
function getLib(){
    let lib:Lib = (() => {}) as Lib;
    lib.version = '1.2.0';
    lib.doSth = () => {
        console.log('来干活了');
    };
    return lib;
}

let l1 = getLib(); // 实例化一个对象
console.log(l1.version); // 1.2.0
l1.doSth(); // 来干活了
```
#### 2.7 函数

js中的函数参数，可以任意，没有强制要求

ts中的函数参数，需要按照定义给定固定数量和固定类型的参数，也可以根据需要定义可选参数，这个时候也可以不用传递这些可选的参数。

```ts
// 可选参数y
function add2(x:number,y?:number){
    // 如果y存在，则返回x + y，否则返回x
    return y? x + y : x;
}

console.log(add2(3,4)); // 7
console.log(add2(9)); // 9
```

**如果有可选参数的话，那么可选参数的位置必须在必选参数的后面**。

为参数设置默认值，方式和js中的方式相同。

```ts
function add3(x:number, y = 2, z:number,q = 3){
    return x + y + z + q;
}
console.log(add3(1,2,3,4)); // 10
```

在设置参数默认值的时候，需要注意，必选参数前的默认值是不能省略的，需要传递undefined来获取参数的默认值；必选参数后面的默认值，可以省略

```ts
function add3(x:number, y = 2, z:number,q = 3){
    return x + y + z + q;
}
console.log(add3(3,undefined,2,9)); // 16,通过传递undefined获取到了y的默认值
```

如果函数参数个数不固定的时候，可以使用剩余参数，剩余参数的类型是以数组的形式存在的：

```ts
function add4(x:number,...rest:number[]){
    return x + rest.reduce((pre,cur) => pre + cur);
}
console.log(add4(2,3,4)); // 9
```

必选参数之前的默认参数是不可以省略的， 如果需要使用必选参数前面的参数的默认值，那么在调用的时候就必须要明确的传入一个undefined。

```ts
function inc2(x: number, y = 2, z: number, q = 1) {
    return x + y + z + q;
}

console.log(inc2(3, undefined, 4)); // 10
```

#### 2.8 函数重载

ts中，函数的重载和java以及C++有所不同。

ts中的函数重载，要求我们先定义一些列的相同函数名的函数声明，但是函数参数会有所不同，同时函数没有实现，只声明、定义。然后只在最后一个函数声明中去实现。

```ts
function inc4(...rest: number[]): number;
function inc4(...rest: string[]): string;
function inc4(...rest: any[]): any {
    let first = rest[0];
    if (typeof first === "string") {
        return rest.join(" ");
    }
    if (typeof first === "number") {
        return rest.reduce((prev, cur) => prev + cur);
    }
}
console.log(inc4(3, 4, 5)); // 12
console.log(inc4("x", "y", "z")); // x y z
```

#### 2.9 接口定义函数

语法：

```ts
interface 函数类型名{
    (参数名1:参数类型, 参数名2:参数类型):函数返回值类型
}
```

用接口定义函数，不需要定义函数名，只需要定义函数的结构，对函数的参数及返回值类型进行约束.如：

```ts
interface Add {
    (x: number, y: number): number
}
```

如这个接口定义了一个函数的接口类型Add，这个类型的函数需要有2个参数x和y，且参数类型都是number类型，函数也需要是number类型。

> 我一个简单的理解，ts定义函数类型常用的可能是3种方法：接口定义函数类型、变量定义函数类型、类型别名定义函数类型，其语法分别为：

**接口定义函数类型**

```ts
interface 函数名{
    (参数名称: 参数类型, 参数名称: 参数类型): 返回值类型
}
```

接口定义函数类型，不需要定义函数名称，只需要定义函数的参数名称、参数的数据类型和函数的返回值即可。

```ts
interface Add {
    (x:number, y: number):number
}
```

**变量定义函数类型**

```ts
let 变量名称:(参数名称:参数类型,参数名称:参数类型) => 返回值类型;
```

**类型别名定义函数类型**

```ts
type 类型名称 = (参数名称:参数类型,参数名称:参数类型) => 返回值类型;
```

#### 2.10 混合类型接口

混合类型接口，既可以有方法，也可以像对象类型接口一样定义属性。如

```ts
// 定一个一个混合类型接口
interface Lib {
    (): void;
    version: string;
    play(): void;
}

// 下的代码定义好了一个混合类型，但是有个弊端,这是一个单例，lib对象的属性和方法只能调用一次，调用次数多了没有意义
let lib: Lib = (() => { }) as Lib;
lib.version = "1.1.0";
lib.play = () => {
    console.log("Let's go playing football!");
}

console.log(lib.version);// 1.1.0

// 我们可以对上述案例进行优化，封装到一个方法中，然后返回实例
function getLib(version: string) {
    let lib: Lib = (() => { }) as Lib;
    lib.version = version;
    lib.play = () => {
        console.log("Let's go playing football!");
    }
    return lib;
}

let lib1 = getLib("1.2.0");
console.log(lib1.version);

let lib2 = getLib("1.4.0");
console.log(lib2.version);
```

js中对函数的参数是没有限制的，但是在ts中，函数的形参和实参必须要一一对应。

如果函数的形参有默认参数，那么在调用的时候如果想使用默认参数，那么就必须要传入一个undefined，而不能省略，否则就形参和实参酒对应不上了。

#### 2.11 

### 3. 泛型

泛型，就是不预先确定具体的数据类型，具体的、明确的数据类型在使用的时候才能确定。

很经典的案例，就是一个输出函数，一些场景可能要输出数字类型，一些场景可能要输出字符串类型等，那么按照常规的实现思路，可能就是要定义多个输出函数，做的好一些是做一个函数重载，反正无论怎么实现，终究都是要定义多个函数，或者那么干脆就定义一个参数都为any类型的函数吧。这样是是可以实现的，但是就失去了ts类型约束的初衷了。

```ts
function log(value: any): any {
    console.log(value);
    return value;
}

log(12);
log("hello world!");
```

其实定义了any类型，和没有定义类型没有什么太大的区别了，这不是我们的目的。

这个时候，就可以使用泛型，在函数定义的时候不预先设定参数的类型，只有在使用的时候才能具体的确定函数的类型。

```ts
function log<T>(value: T): T {
    console.log(value);
    return value;
}

// 明确指定函数参数类型的方式调用泛型函数
log<string[]>(['a', 'b']);
log(['1', '2', '3']); // 以类型推导的方式调用泛型函数，建议使用这种方式
```

#### 3.1 泛型函数

ts中，可以通过类型别名来定义泛型。

```ts
// 声明一个泛型类型函数类型
type Log = <T>(value: T) => T;
// 定义一个泛型类型函数的实现
// let myLog:Log = log;
let myLog: Log = <T>(value: T): T => {
    console.log(value);
    return value;
}
myLog(12); // 12
```
#### 3.2 泛型接口

泛型也可以用来定义接口。

```ts
interface Log {
    <T>(value: T): T
}

let myLog: Log = <T>(value: T): T => {
    console.log(value);
    return value;
}

myLog(15); // 15
myLog("Hello"); // Hello
```

如demo中，定义了一个接口，接口中定义了一个函数类型,但是有可能一个接口中不光只约束一个函数类型，还有可能会有其他的成员参数，如果需要对所有的成员参数都进行类型约束，那么就可以给接口添加泛型，如

```ts
interface Log<T> {
    (value: T): T
}
```
这样就会对接口中的所有成员参数进行约束，只是这样在调用的时候，需要指定下接口的类型：

```ts
// 使用接口的时候，需要显示指定接口的类型<string>
let myLog: Log<string> = <T>(value: T): T => {
    console.log(value);
    return value;
}
myLog(15); // 这里会报错，因为类型声明中声明了是string类型，所以这里会报错
myLog("Hello"); // 这里是符合要求的，没有任何问题
```

也可以通过给接口泛型默认值，就不需要在实现接口的时候都指定类型了，当然了，如果和指定的默认类型不同的时候，还是要指定类型的。

```ts
interface Log<T = number> {
    // <T>(value: T): T
    (value: T): T
}

let myLog: Log = <T>(value: T): T => {
    console.log(value);
    return value;
}
myLog(15); // 15，正常输出
myLog("Hello"); // 报异常，因为默认的number类型，这里给的是string类型
```

案例中，接口指定了默认的类型为number类型，而自定义函数myLog在实现Log接口的时候没有指定具体的类型，那么默认就是number类型，

#### 3.3 泛型类与泛型约束

泛型类

```ts
class Log<T>{
    run(value: T) {
        console.log(value);
    }
}

// 实例化的时候，可以指定类型，如果指定了类型，那么就只能穿入指定类型的数据，如果没有指定类型，那么就可以穿入任意类型的数据
let log = new Log<string>();
log.run("hello world!");

let log2 = new Log<number>();
log2.run(2);
```

> 泛型不能约束类的静态成员。

看代码：

```ts
function log<T>(value: T): T {
    console.log(value, value.length);
    return value;
}
```

案例定义了一个函数log，函数不光打印了其参数value，还打印出了其参数value的属性，这个时候编译器给我们提示：类型“T”上不存在属性“length”

![类型“T”上不存在属性“length”](./images/i29.png)


这个时候，我们可以预定义一个接口，让这个预定义的接口具有length属性，然后让类型变量T去继承我们预定义的接口：

```ts
// 预定义一个包含length属性的接口
interface Length {
    length: number;
}

// 让类型变量T实现含有length属性的接口Length
function log<T extends Length>(value: T): T {
    console.log(value, value.length);
    return value;
}
log("12"); // 12 2
```

这样在类型变量T实现了具有length属性的接口后，那么T就不能是任意的类型了，它必须是一个具有length属性的数据，如string、array等。这叫做**泛型约束**。

**泛型的好处**

1. 函数和类可以轻松的实现支持多种类型，增强程序的可扩展性；

2. 不必写多条函数重载，冗长的联合类型声明，增强代码的可读性；

3. 灵活控制类型之间的约束；
### 4. 类

ES6中引入了类的概念，Ts中也有类的概念，ts中的类覆盖了ES6中的类，同时还有一些自己独有的特性。

#### 4.1 类的继承和成员修饰符

无论在ES中还是TS中，类的成员属性都是实例属性,而不是原型属性；类的成员方法都是原型方法。

> js中，方法也被认为是一种特殊的属性。

```ts
class Cat {
    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
    name: string;
    age: number;
    run() { }
}

console.log(Cat.prototype); // {run: ƒ, constructor: ƒ} Cat类的原型上只有方法，定义的构造函数和成员函数

const cat = new Cat("Miaoxingren", 12);
console.log(cat); // Cat {name: 'Miaoxingren', age: 12} 只有Cat类的成员属性name和age
```

ts中的类和es有一点不同，就是成员属性在实例化的时候，必须要有初始值。

```ts
class Cat {
    constructor(name: string) {
        this.name = name;
    }

    name: string;
    run() { }
}
```

如在Cat类中，成员属性name在构造函数中被赋值了，初始化了一个值。

那么如果没有构造函数怎么办呢？那么就在声明成员属性的时候给初始化一个值，或者将成员属性声明为可选属性

```ts
class Cat {
    name: string = "Miaomiao";
    age?: number;
    run() { }
}
```
demo中，没有了构造函数中为成员属性初始化值，那么就给成员属性name赋了一个固定值，将成员属性age声明为了可选属性，这样也是不报错的。

#### 4.2 类的继承

TS中类的继承通过extends关键字实现。

在继承中，派生类中一定要包含super调用， 派生类的构造函数一定要包含父类的构造函数。

```ts
class MiaoMiao extends Cat {
    constructor(name: string, age: number, color: string) {
        super(name, age);
        // 派生类中成员属性初始化的时候，一定要在super之后，如this.color在super之后
        this.color = color;
    }
    // 为派生类添加自己的属性color，在
    color: string;
}
```

#### 4.3 类的修饰符

public: ts类中，默认是public的，即可被所有对象访问。

private：只能被类本身调用，不能被类的实例和类的字类调用；

protected：受保护的，受保护的成员变量，只能在字类中访问，不能在实例中访问

readonly：只读属性，只读属性的值不能被修改，声明时必须要初始化。

static：静态属性，通过static修饰的成员变量只能通过类名来调用； static成员变量可以被继承；

```ts
class Cat {
    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
    name: string;
    age: number;
    run() { }
    private play() {
        console.log("playing");
    }
}


const cat = new Cat("Miaoxingren", 12);
cat.play(); // 这里是报错的，会提示：属性“play”为私有属性，只能在类“Cat”中访问。
```

![属性“play”为私有属性，只能在类“Cat”中访问](./images/i25.png)

类的构造函数也可以被声明为private的，表明当前的这个类既不能被实例化，也不能被继承。

![声明为private的构造函数的类，既不能被继承，也不能被实例化](./images/i26.png)

如果一个类中的构造函数被声明成了protected的，那么这个类就只能被继承，不能被实例化。

除了正常的成员属性可以添加成员修饰符外，构造函数的参数也可以使用修饰符，构造函数的参数使用了成员呢修饰符后就自动变成了当前类的成员属性，就不需要在重新声明成员属性了。

```ts
class People {
    constructor(public name: string, public age: number) {
        this.name = name;
        this.age = age;
    }
}

const pl = new People("Nicholas Zakas", 16);
console.log(pl); // People {name: 'Nicholas Zakas', age: 16}
```

demo中，构造函数的参数使用了成员修饰符，就不需要重新这些参数的成员属性了。

```ts
class People {
    constructor(public name: string, public age: number) {
        this.name = name;
        this.age = age;
    }
    static color: string = "yello";
}

const pl = new People("Nicholas Zakas", 16);
console.log(People.color); // yello 只能通过类名People来访问
```

static修饰的成员变量可以被字类访问

```ts
class People {
    constructor(public name: string, public age: number) {
        this.name = name;
        this.age = age;
    }
    static color: string = "yello";
}

const pl = new People("Nicholas Zakas", 16);
console.log(People.color); // yello

console.log(pl); // People {name: 'Nicholas Zakas', age: 16}

class WhitePeople extends People {
    constructor(name: string, age: number) {
        super(name, age);
    }
}
console.log(WhitePeople.color); // 派生类访问了父类中定义的static成员变量
```

#### 4.4 抽象类

ES中没有引入抽象类的概念，抽象类是TS中具备而ES中不具备的东西，是对Es的扩展。

抽象类，就是只能被继承而不能被实例化的类。

抽象类使用abstract关键字声明。

```ts
abstract class Animal {

}
const animal = new Animal(); // 无法创建抽象类的实例
```

如demo，声明了一个抽象类Animal，然后我们通过new关键字实例化这个类，然而编译器给我们报错了，提示：无法创建抽象类的实例

![无法创建抽象类的实例](./images/i27.png)

> 在继承一个类的时候，无论父类有没有参数，都要调用super方法，且super的调用要在派生类其他成员属性赋值语句之前。

```ts
abstract class Animal {

}
// const animal = new Animal(); // 无法创建抽象类的实例

class Tiger extends Animal {
    constructor(public color: string, public age: number) {
        super(); // 如果这里不调用super，会提示异常：派生类的构造函数必须包含 "super" 调用，哪怕父类没有参数
    }
    introduce() {
        console.log("我的颜色是" + this.color + ",今年" + this.age + "岁了。");
    }
}
```

抽象类中看可以定义方法，以及具体的实现，那么派生类的实例就可以直接调用父类的方法而不需要重新声明了(直接调用即可，不需要在派生类中做任何操作).

```ts
abstract class Animal {
    constructor(name: string) {
        this.name = name;
    }
    name: string;
    play() {
        console.log(`${this.name}在玩皮球！`);
    }
}
// const animal = new Animal(); // 无法创建抽象类的实例

class Tiger extends Animal {
    constructor(name: string, public color: string, public age: number) {
        super(name); // 如果这里不调用super，会提示异常：派生类的构造函数必须包含 "super" 调用，哪怕父类没有参数
    }
    introduce() {
        console.log(`大家好，我是${this.name},今年${this.age}岁了，我是${this.color}颜色的！`);
    }
}

const tiger = new Tiger("小虎牙", "yello", 3);
tiger.introduce(); // 大家好，我是小虎牙,今年3岁了，我是yello颜色的！
// 调用从父类继承的play方法
tiger.play(); // 小虎牙在玩皮球！
```

抽象类中也可以声明抽象方法，抽象方法即通过abstract关键字声明，只声明了方法的结构即参数和函数返回值类型但是没有具体实现的方法。
抽象类中声明的抽象方法，在继承它的派生类中必须要实现这些抽象方法，否则会报错：非抽象类不会实现继承自“Animal”类的抽象成员“studying”

```ts
abstract class Animal {
    constructor(name: string) {
        this.name = name;
    }
    name: string;
    play() {
        console.log(`${this.name}在玩皮球！`);
    }
    // 定义的抽象类，在它的字类中必须要实现这个抽象方法，否则报错
    abstract studying(): void;
}
// const animal = new Animal(); // 无法创建抽象类的实例

class Tiger extends Animal {
    constructor(name: string, public color: string, public age: number) {
        super(name); // 如果这里不调用super，会提示异常：派生类的构造函数必须包含 "super" 调用，哪怕父类没有参数
    }
    introduce() {
        console.log(`大家好，我是${this.name},今年${this.age}岁了，我是${this.color}颜色的！`);
    }
    // 实现父类中定义的抽象方法
    studying(): void {
        console.log(`${this.name}非常爱学习！`);
    }
}

const tiger = new Tiger("小虎牙", "yello", 3);
tiger.introduce(); // 大家好，我是小虎牙,今年3岁了，我是yello颜色的！
// 调用从父类继承的play方法
tiger.play(); // 小虎牙在玩皮球！
tiger.studying(); // 小虎牙非常爱学习！
```

抽象类中的抽象方法，可以抽离出来类中的一些共性，以及实现多态，即在不同的字类中有不同的实现，实现了运行时的绑定。

```ts
abstract class Student {
    constructor(public stage: string) {
        this.stage = stage;
    }
    abstract study(): void;
    abstract play(): void;
}

class Pupil extends Student {
    constructor(stage: string, course: string, public sports: string) {
        super(stage);
        this.course = course;
    }
    course: string;
    study(): void {
        console.log(`${this.stage}学习${this.course}.`);
    }
    play(): void {
        console.log(`${this.stage}喜欢玩${this.sports}.`);
    }
}

const pupil = new Pupil("小学生", "语文和数学", "沙包");
pupil.study(); // 小学生学习语文和数学.
pupil.play(); // 小学生喜欢玩沙包.

class MiddleSchoolStudent extends Student {
    constructor(stage: string, public reading: string, public sports: string) {
        super(stage);
        this.reading = reading;
        this.sports = sports;
    }
    study(): void {
        console.log(`${this.stage}喜欢${this.reading}.`);
    }

    play(): void {
        console.log(`${this.stage}喜欢玩${this.sports}`);

    }
}
const middle = new MiddleSchoolStudent("中学生", "阅读", "足球");
middle.study(); // 中学生喜欢阅读.
middle.play(); // 中学生喜欢玩足球
```

ts中的类，也可以作为类型使用。

```ts
abstract class Student {
    constructor(public stage: string) {
        this.stage = stage;
    }
    abstract study(): void;
    abstract play(): void;
}

class Pupil extends Student {
    constructor(stage: string, course: string, public sports: string) {
        super(stage);
        this.course = course;
    }
    course: string;
    study(): void {
        console.log(`${this.stage}学习${this.course}.`);
    }
    play(): void {
        console.log(`${this.stage}喜欢玩${this.sports}.`);
    }
}

class MiddleSchoolStudent extends Student {
    constructor(stage: string, public reading: string, public sports: string) {
        super(stage);
        this.reading = reading;
        this.sports = sports;
    }
    study(): void {
        console.log(`${this.stage}喜欢${this.reading}.`);
    }

    play(): void {
        console.log(`${this.stage}喜欢玩${this.sports}`);

    }
}
const pupil = new Pupil("小学生", "语文和数学", "沙包");
const middle = new MiddleSchoolStudent("中学生", "阅读", "足球");

// 使用抽象类Student作为类型声明了一个Student类型的数组，其数组项为其字类的实例对象
const student: Student[] = [pupil, middle];
student.forEach(item => {
    item.study(); // 小学生学习语文和数学.、中学生喜欢阅读.
});
```

#### 4.5 类与接口的关系

**类类型接口**

一个接口可以约束类成员有哪些属性，以及它们的类型。

类实现接口的时候，必须要实现接口中定义的所有的属性，即包括接口中定义的方法。

实现接口的类，除了实现接口中所有的属性，也可以定义自己的属性。

```ts
interface Human {
    name: string;
    eat(): void;
}

class Asian implements Human {
    constructor(name: string) {
        this.name = name;
    }
    name: string;;
    eat(): void {
        console.log("我喜欢吃大米饭!");
    }

    // 除了实现所有的接口中定义的属性之外，类也可以定义自己的成员属性
    play() {
        console.log("play football!");
    }
}
```

接口只能约束类的公有成员，即定义为public的成员属性，在类中声明为非public类型的成员属性，是不能在接口中进行约束的

```ts
interface Human {
    // 接口中不能约束类的构造函数，下面一行代码即是一个构造函数
    // new(name: string): void;
    name: string;
    age: number;
    eat(): void;
}

// 这里会提示类错误的实现接口
class Asian implements Human {
    // 注意构造函数中声明了private的成员属性age，接口中也声明了age属性的约束，所以这里会报错
    constructor(name: string, private age: number) {
        this.name = name;
    }
    name: string;
    eat(): void {
        console.log("我喜欢吃大米饭!");
    }

    play() {
        console.log("play football!");
    }
}
```

![接口不能约束类中非public类型的成员变量](./images/i28.png)

接口不能约束类的构造函数，即接口中不能定义构造函数。

```ts
interface Human {
    // 接口中不能约束类的构造函数，下面一行代码即是一个构造函数
    // new(name: string): void;
    name: string;
    eat(): void;
}
```

#### 4.6 接口的继承

接口和类一样，也可以实现接口的相互继承，且接口可以继承多个接口。

接口的继承，通过extends实现。

> 继承，通过extends关键字实现；实现接口，通过implements关键字实现；

> 英语中，extends：延伸的意思，编程中可理解为延伸某个接口或类，就是在某个接口、类的基础上功能再次扩展；implements：执行、履行的意思，在编程中可以理解为实现、执行某个接口

**接口继承类**

接口除了可以继承接口以外还看可以继承类。

接口继承类，就是接口对类的成员变量做了一次抽象,接口可以抽象类的公有成员、受保护成员和私有成员。

```ts
class Auto {
    state = 1;
}

interface AutoInterface extends Auto {

}
```
如demo，AutoInterface接口继承了Auto类，其实就是AutoInterface接口抽象了类Auto的成员变量state。如果有类要实现AutoInterface接口时，只需要实现state变量就可以了。

```ts
class Auto {
    state = 1;
}

interface AutoInterface extends Auto {

}

class C implements AutoInterface {
    state: number = 2;
}
```

如类C实现了AutoInterface接口，只需要在类C种实现state变量即可。

```ts
let car = new C();
console.log(car.state); // 2
```

### 5. 类型检查机制

类型检查机制，就是Typescript编译器在做类型检查时，所秉承的一些原则，以及表现出来的一些行为。

作用：辅助开发，提升开发效率，

主要从以下3个方面来进行开发辅助：

1. 类型推断；

2. 类型兼容性；

3. 类型保护；

#### 5.1 类型推断

类型推断，就是不需要指定变量的类型(以及函数的返回值类型)，Typescript可以根据某些规则自动为其推断出一个类型。

1. 基础类型推断

2. 最佳通用类型推断

3. 上下文类型推断

##### 5.1.1 基础类型推断

基础类型推断，如在变量声明的时候、定义函数时的参数的时候，不指定变量和参数的具体类型，有ts编译器根据一些规则去推断出一个类型。

函数返回值也会被类型推断；

```ts
let a; // 只声明不赋值，推断为了一个any类型

let num = 12; // 根据变量值推断为了一个number类型

let arr = [1, 2, 3]; // 根据变量值推断为了number类型的数组

let fun = (x, y = 2) => x + y; // 函数参数x没有默认值，就被推断为了any类型，参数为默认值为2，被推断为了number类型
```

上面的几种类型推断，是从右到左边的类型推断，即根据右侧值的类型，来推断左侧变量的类型；

还有一种类型推断是从左到右的类型推断，即上下文的类型推断；

##### 5.1.2 上下文的类型推断

来看下面的案例：

```ts
window.onclick = event => {
    console.log(event.button);
}

window.onkeydown = e => {
    console.log(e.altKey);
}
```

案例定义了两个事件，分别为鼠标点击事件和键盘的键按下时的事件，鼠标点击事件参数event，根据左边的事件window.onclick被推断为了MouseEvent类型事件；而键盘的键按下事件，则被推断为了KeyboardEvent事件。

这就是典型的根据上下文的类型推断。

#### 5.2 类型断言

类型推断，是编译器可以帮我们推断出一个数据类型。但是有的时候，我们已经非常明确某个变量的类型了，这个时候，我们就可以使用类型断言，直接指定类型了。

```ts
let foo = {};
foo.bar = 1;
```

比如我们声明了一个空对象foo，然后给foo对象的bar属性赋值为1.但是实际上，foo对象并没有这个属性bar，那么编译器就会报错。

![类型断言](./images/i30.png)

这个时候，我们可以声明一个接口Foo，接口定义一个bar的属性，然后将foo对象指定为Foo类型：

```ts
interface Foo {
    bar: number
}

let foo = {} as Foo;
foo.bar = 1;
```

这样，就不会报错了。

但是这样有一个弊端，假如说这个时候我没有给foo对象实现bar属性，那么其实对象foo就没有实现接口Foo，没有遵循接口Foo的类型约束，是不友好的。因为这个时候编译器不会提示。
最好的办法就是直接将对象foo声明为Foo类型的，

```ts
interface Foo {
    bar: number
}

let foo: Foo = {};
```

这样的话，如果我们不实现bar属性，编译器就会提示：

![类型断言](./images/i31.png)

类型断言，不能滥用，一定要注意，否则会带来代码的安全隐患。

