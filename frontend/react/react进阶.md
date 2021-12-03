### 1. React全家桶

React基础

React-router

PubSub 消息管理

Redux 集中式状态管理

Ant-Design UI库

#### 1.1 React是什么？

用户构建用户界面的Js库

React只关注视图、只关注页面

React是一个将数据渲染为HTML视图的开源Javascript库

#### 1.2 起源

facebook公司推出的。

facebook2011年部署在newsfeed

2012年部署了Instgram

2013年5月开源了

React被国际上广大互联网一线大厂使用。

#### 1.3 价值

* 原生js开发，效率低，DOM操作繁琐
  * React、Vue等UI库、框架之前的前端开发，是通过DOM API操作UI
* 使用js操作DOM，浏览器会进行大量的重绘重排，严重影响性能；
* 原生js没有组件化解决方案，代码复用率低；

#### 1.4 React特点

* 采用组件式模式、声明式编码，提高开发效率和组件复用率；
* React Native中可以使用React语法进行移动端开发；
* 使用虚拟DOM+优秀的Diff算法，尽量减少与真实DOM的交互；

#### 1.5 学习React的需要准备的JS基础知识

判断this的指向

class（类）

ES6语法规范

npm包管理器

原型、原型链

数组常用方法

模块化

### 2.React基础

#### 2.1 基本介绍

##### 2.1.1 官网

https://reactjs.org/

https://react.docschina.org/

React CDN：https://unpkg.com/

##### 2.1.2 介绍

用于动态构建用户界面的javascript库，只关注视图

由facebook在2013年5月开源

##### 2.1.3 React特点

* 声明式编码
* 组件化编码
* 开用React Native编写原生应用
* 高效：优秀的diff算法和虚拟DOM

##### 2.1.4 React高效的原因

* 使用虚拟DOM，不总是直接操作页面的真实DOM
* DOM的diff算法，最小化的页面重绘

#### 2.2 React基本使用

##### 2.2.1 效果

JSX：开源像写js一样写jsx。jsx本身就是js的一写扩展，多了一些规则而已，可以像写js一样写jsx。

```html
    <!--容器-->
    <div id="app"></div>

    <!--
        引入react库时，注意引入的顺序：
        1. 引入react和辛库
        2. 引入react的扩展库：react-dom,让react具有操作DOM的能力
        3. 再引入扩展工具：babel.min.js
    -->
    <!--引入React核心库-->
    <script src="./js/react.development.js"></script>
    <!--引入react扩展库react-dom,支持react操作DOM-->
    <script src="./js/react-dom.development.js"></script>
    <!--引入babel，将jsx转为js-->
    <script src="./js/babel.min.js"></script>
    <!--
        type写成text/babel，表示这是jsx类型的代码，且使用babel进行转换
        type属性一定要写，默认为js
    -->
    <script type="text/babel">
      // 1. 创建虚拟DOM
      const VDOM = (
        <h1>Hello React</h1>
      ); /* 这里是jsx，不是js中的字符串，不要使用引号 */
      // 2. 渲染虚拟DOM到页面
      ReactDOM.render(VDOM, document.querySelector("#app"));
    </script>
```

效果：

<img src="./images/i3.png" alt="react初" style="zoom:50%;" />

##### 2.2.2 相关js库

react.development.js  react核心库

react-dom.development.js react扩展库，让react具备操作DOM的能力

babel.min.js react的转换工具，可以从https://www.babeljs.cn/setup这里获取

##### 2.2.3 创建虚拟DOM的两种方式

1. 纯js的方式：一般不会用

   ```html
   <!--创建react应用的容器-->
   <div id="app"></div>
   
   <!--引入react库，注意先后顺序：核心库、扩展库-->
   <script src="../js/react.development.js"></script>
   <script src="../js/react-dom.development.js"></script>
   <!--不需要引入转换工具了，因为babel的目标是把jsx转换成js，而现在我们直接使用js，所以不需要转换了-->
   <!-- <script src="../js/babel.min.js"></script> -->
   
   <!--type可以省略了，或者显示设置成text/javascript-->
   <script type="text/javascript">
       // 1. 以js的方式创建虚拟DOM
   
       /**
          * React.createElement()接收3各参数，分别为：
          * 标签名  string
          * 标签属性 object
          * 标签内容 any
          */
       const vd = React.createElement("h1",{id: "js"},"以js的方式创建虚拟DOM");
       // 2. 渲染虚拟DOM到页面
       ReactDOM.render(vd,document.querySelector("#app"));
   </script>
   ```

   <img src="./images/i4.png" alt="以js的方式创建虚拟DOM不建议使用" style="zoom:50%;" />

2. JSX方式，推荐使用

   ```html
   <!--创建react应用的容器-->
   <div id="app"></div>
   
   <!--引入react库，注意引入顺序：核心库、扩展库、转换工具-->
   <script src="../js/react.development.js"></script>
   <script src="../js/react-dom.development.js"></script>
   <script src="../js/babel.min.js"></script>
   <script type="text/babel">
         const vd = <h1 id="jsx">使用JSX方式创建虚拟DOM</h1>;
         ReactDOM.render(vd, document.querySelector("#app"));
   </script>
   ```

   <img src="./images/i5.png" alt="以jsx的方式创建虚拟DOM，推荐使用" style="zoom:50%;" />

实际代码中，推荐jsx的方式，因为如果有多层标签嵌套的时候，jsx可以直接按照真实的结构去写代码，简单；而js创建虚拟DOM就不一样了，需要多层都通过React.createElement()方法去创建标签。

JSX的主要作用，就是为了创建虚拟DOM，让我们开发代码更简单。

jsx在写的代码片段较长时，可以像写HTML一样进行折行书写，只是这个时候需要把jsx使用()包裹起来.

```html
<!--创建react应用的容器-->
<div id="app"></div>

<!--引入react库，注意引入顺序：核心库、扩展库、转换工具-->
<script src="../js/react.development.js"></script>
<script src="../js/react-dom.development.js"></script>
<script src="../js/babel.min.js"></script>
<script type="text/babel">
      const vd = (
        <h1 id="jsx">
          <span className="text">使用JSX方式创建虚拟DOM</span>
    </h1>
      );
      ReactDOM.render(vd, document.querySelector("#app"));
</script>
```

<img src="./images/i6.png" alt="jsx较长时使用()包裹换行书写" style="zoom:50%;" />

**关于虚拟DOM**

1. 本质是一般的Object对象；
2. 虚拟DOM本身比较轻量，真实DOM相对较重。因为虚拟DOM主要是为了供react内部使用，够React使用就可以了；但是真实DOM需要考虑兼容很多种场景，有了较多的冗余属性，导致了较多的属性，显得较重；
3. 虚拟DOM最终会被React渲染成真实DOM，呈现在页面上； --- 虚拟DOM是保存在内存中

#### 2.3 React JSX

1. 全称：Javascript XML
2. 是react定义的一种类似xml的js扩展语法：Js + XML
3. 本质是React.createElement(component,props,...children)方法的语法糖
4. 作用：用来简化创建虚拟DOM
   1. 写法：var element = <h1>Hello React JSX</h1>
   2. 注意：
      1. 它不是字符串，也不是HTML、XML标签
      2. 它最终产生的就是一个普通的Object对象
5. 标签名任意：可以是HTML标签或者其他标签

##### 2.3.1 效果

##### 2.3.2 JSX

jsx语法规则

1. 定义jsx时不要使用引号，因为它不是字符串

2. jsx如果需要混用js变量，那么js变量需要使用{}包裹起来，{}内也可以使用js表达式

   1. 标签中混入js表达式时使用{}包裹

3. 通过类来指定样式时，使用className，不要使用class，且属性值不需要使用{}包裹，正常使用引号即可

4. 内联样式，要用style={{key:value}}的形式去写：外层的{}表示要使用js表达式了，内层的{}表示js对象，css的属性本身是key：value的形式

5. 虚拟DOM必须只能有1个根标签

6. 标签必须闭合

7. 标签首字母：

   1. 如果首字母是小写字母，则将标签转换为HTML中的同名元素；如果HTML没有对应的同名元素，则浏览器会报错

      1. 也就是说，jsx中，如果首字母是小写，那么只能使用html中有的元素，html中没有的标签元素，jsx中不要随便使用

   2. 如果大写字母开头，就去渲染对应的组件

      1. 如果组件没有定义，则报错

         ```react
             <style>
               .title {
                 color: #f20;
                 font-size: 32px;
               }
             </style>
           </head>
           <body>
             <!--react应用容器-->
             <div id="app"></div>
         
             <!--导入react库-->
             <script src="../js/react.development.js"></script>
             <script src="../js/react-dom.development.js"></script>
             <script src="../js/babel.min.js"></script>
         
             <script type="text/babel">
               const propId = "msg";
               const data = "Hello React!";
               // 创建虚拟DOM
               const VDOM = (
                 // 只能有1个根元素
                 <div>
                   {/*使用js变量时，要使用{}包裹*/}
                   <h2 id={msg}>
                     {/*
                         内联属性，使用双层的{},外层的{}表示要使用js表达式了，内层的{}表示这是一个对象
                         内联属性如果是多个单词组成，则使用小驼峰的命名规则
                         如果希望通过类（class）来控制样式，需要使用className作为属性名，而不能直接使用class
                     */}
                     <span style={{ padding: "10px", fontStyle: "italic" }}>{data}</span>
                   </h2>
                   {/*标签要闭合，可以自闭和，也可以使用闭合标签*/}
                   <input type="text" />
                   {/*
                         jsx中标签
                             如果首字母小写，则只能使用HTML中有的标签，然后react会将这些jsx标签转换为同名的HTML标签
                             如果首字母大写，react会去渲染对应的组件：如果组件不存在则会报错
                     */}
                   <Card></Card>
                 </div>
               );
         
               // 渲染VDOM到页面
               ReactDOM.render(VDOM, document.querySelector("#app"));
             </script>
         ```

##### 2.3.3 渲染虚拟DOM（元素）

##### 2.3.4 JSX demo

在写jsx时，需要明确js中表达式和语句的概念。

表达式：可以被求值的并产生一个值的js短语，如：a、a+b、fn(2)、arr.map()、function fn(){}等，从案例中可以看到，一个变量、算术运算、函数调用、数组访问、函数定义等，都是表达式；

语句：控制程序走向的语句，如if、for、switch等，都是js语句

<font color="#f20">jsx中，只能使用表达式，不能使用语句。</font>

```react
    <!--react应用容器-->
    <div id="app"></div>

    <!--导入react库-->
    <script src="../js/react.development.js"></script>
    <script src="../js/react-dom.development.js"></script>
    <script src="../js/babel.min.js"></script>

    <script type="text/babel">
      const data = ["Angular", "React", "Vue"];

      const VDOM = (
        <div>
          <h2>前端框架</h2>
          <ul>
            {data.map((item,index) => {
            {/*实际项目中，不要使用index和随机数作为key值，这里仅仅是小的demo演示，可以先不细究这个问题*/}
              return <li key={index}>{item}</li>;
            })}
          </ul>
        </div>
      );

      // 渲染DOM
      ReactDOM.render(VDOM, document.querySelector("#app"));
    </script>
```

#### 2.4 模块与组件和模块化与组件化的理解

##### 2.4.1 模块

前端领域中的模块，指的是js的模块。

1. 理解：向外提供特定功能的js程序，一般情况下就是一个文件就是一个模块
2. 为什么要拆成模块：随着业务逻辑的增加，代码越来越多且越来越复杂
3. 作用：复用js、简化js的编写，提高js的运行效率

前端工程中说的模块化，一般就是指js的模块化。

##### 2.4.2 组件

1. 理解：用来实现局部功能效果的代码和资源的集合
2. 为什么要用组件：页面的功能复杂
3. 作用：复用编码，简化项目编码，提高运行效率

组件和模块相比的区别：

1. 模块指的是js模块
2. 组件，指某个局部效果的所有资源的集合，包括js、html、css、image等所有的资源

##### 2.4.3 模块化

当应用的js都已模块的方式来编写的，这个应用就是一个模块化的应用

##### 2.4.4 组件化

当应用是以多组件的形式实现，这个应用就是一个组件化的应用

### 3. React面向组件编程

#### 3.1 基本理解和使用

react中有两种定义组件的方式：

1. 函数式组件

   就是通过function定义的组件

   定义函数式组件时，函数名的首字母一定要大写，且函数一定要有返回值

   另外在注册组件时，组件的首字母也使用大写，标签要闭合

   ```react
       <!--定义react应用容器-->
       <div id="app"></div>
   
       <!--引入react库-->
       <script src="../js/react.development.js"></script>
       <script src="../js/react-dom.development.js"></script>
       <script src="../js/babel.min.js"></script>
   
       <script type="text/babel">
         // 1. 创建函数式组件
         // 函数名要使用大写
         function Demo() {
           return <h2>Hello React</h2>;
         }
   
         // 2. 渲染组件到页面
         // 组件渲染时，首字母也要使用大写
         ReactDOM.render(<Demo />, document.querySelector("#app"));
       </script>
   ```

2. 类式组件

   通过class定义的组件
   
   React中，如果使用类式组件，需要满足几个条件：
   
   * 那么类需要继承React.Component
   * 必须要实现render函数
   * 必须要有返回值
   
   ```react
      <!--定义react应用的容器-->
       <div id="app"></div>
   
       <!--导入react库-->
       <script src="../js/react.development.js"></script>
       <script src="../js/react-dom.development.js"></script>
       <script src="../js/babel.min.js"></script>
   
       <script type="text/babel">
         // 类式组件必要是继承React.Component
         // 类名，也就是组件名，首字母需要大写
         // react中的组件明明，直接使用大驼峰的命名方式就可以了
         class MyComponent extends React.Component {
           // 必须要实现render函数
           render() {
               /**
                * render是放在哪里的？ ---- 类MyComponent的原型对象上，供实例使用
                * render中的this是谁？ ---- 类MyComponent的实例对象，MyComponent组件实例对象
                */
             // render函数必须要有返回值，返回值其实是jsx
             return <h2>Hello,React的类式组件</h2>;
           }
         }
   
         ReactDOM.render(<MyComponent />, document.querySelector("#app"));
         /**
          * 执行ReactDOM.render(<MyComponent />, document.querySelector("#app"));之后，发生了什么？
          *    1. React解析组件标签，找到了MyComponent组件；
          *    2. 发现组件是用类定义的，随后new出来该实例对象，并通过该实例调用原型上的render方法
          *    3. 将render返回的虚拟DOM转换为真实DOM，随后呈现在页面中
          */
       </script>
   ```

#### 3.2 组件实例的三大核心属性之一：state

**组件实例的三大属性，指的是类组件实例的三大属性：state、refs、props**

函数式组件，通过hooks也实现了state、refs和props。

react中组件又可以分为简单组件和复杂组件。

简单组件：无状态的组件称为简单组件；

复杂组件：带有状态的组件称为复杂组件；

**那么什么是状态呢？-state**



#### 3.3 组件实例的三大核心属性之二：props

#### 3.4 组件实例的三大核心属性之三：refs与事件处理

#### 3.5 收集表单数据

#### 3.6 组件声明周期

#### 3.7 虚拟DOM与DOM diff算法

### 4. React应用：基于React脚手架

### 5. React Ajax

### 6. react-router

### 7. React组件库

### 8. redux
