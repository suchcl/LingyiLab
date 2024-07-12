### 1. 简介

装饰器,是一种特殊类型的声明,它能够被作用到类(class)、方法、属性和参数上.

> 装饰器,不能被作用到函数上.

> 函数和方法,是不同的.一般的情况下,可以简单理解为函数为面向过程定义的,一个函数就是一个独立的功能,或者说函数是某个算法的实现.而方法是为面向对象设计的,其要依附于类,方法可以理解为其是某个类中的某个业务逻辑的实现.

装饰器,当前在ECMAScript标准中还仅仅是一个提议,目前已进入到stage3阶段,在javascript语言中还没有实现这个标准.但是Ts将它作为一个实验性特性做了实现.所以,javascript里面,目前还不支持装饰器,typescript里是支持的.也就是说,在js里面不能使用装饰器,在ts里面可以使用.

- 语法:装饰器使用@expression形式,expression求值后必须为一个函数,它会在运行时被调用,被装饰的声明信息作为参数传入

- 若要在ts项目中启用装饰器这个实验性特性,需要手动配置下experimentalDecorators为true

tsconfig.json

```json
{
    "compilerOptions": {
        // ……
        "experimentalDecorators": true,
        // ……
    },
}
```

不过现在大部分的脚手架搭箭项目,该属性都是自动配置为true的.

- 常用的装饰器类型:类装饰器、属性装饰器、方法装饰器、参数装饰器

- 装饰器的写法:

    * 普通装饰器:无法传参

    * 装饰器工厂:可以传参

### 2. 装饰器的写法

#### 2.1 普通装饰器

```ts
interface Person {
    name: string;
    age: string;
}

function enhancerDecorator(target: any) {
    target.prototype.name = "Nicholas Zakas";
    target.prototype.age = "16";
}

@enhancerDecorator
class Person {
    
}

function HomeController(req: any, res: any) {
    const p = new Person();
    const obj = {
        name: p.name,
        age: p.age
    };
    res.send(obj);
}
```

<img src="./images/i66.png" width="300" />

从代码和执行结果中可以看出,装饰器函数enhancerDecorator通过修改原型的方式成功的给类Person新增了2个属性name和age.

#### 2.2 装饰器工厂

```ts
interface Person {
    name: string;
    age: string;
}

// 利用函数柯里化解决传参问题,向装饰器传递一些参数,也叫做参数注解
function enhancerDecorator(name: string) {
    // name为装饰器的元数据,外界传递进来的参数
    return function enhancerDecorator(target: any){
        target.prototype.name = name;
        target.prototype.age = 21;
    }
}

@enhancerDecorator("Rusira Jayatilake")
class Person {
    
}

function HomeController(req: any, res: any) {
    const p = new Person();
    const obj = {
        name: p.name,
        age: p.age
    };
    res.send(obj);
}
```

### 3.装饰器分类

#### 3.1 类装饰器

类装饰器在类声明之前声明,即紧靠着类声明,用来监听、修改或者替换类定义

- 类装饰器不能用在声明文件中(.d.ts),也不能用在任何外部上下文中如declare的类

- 类装饰器表达式会在运行时当作函数调用,类的构造函数作为其唯一的参数

- 如果类装饰器返回一个值,它会使用提供的构造函数来替换类的声明

#### 3.2 属性装饰器

#### 3.3 方法装饰器

#### 3.4 参数装饰器

#### 3.5 装饰器执行顺序

### 4. 装饰器原理

#### 4.1 执行步骤