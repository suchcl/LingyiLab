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

