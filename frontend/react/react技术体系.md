<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [一、项目构建工具 create-react-app](#一项目构建工具-create-react-app)
- [二、关于React](#二关于react)
  - [2.1 React的起源和发展](#21-react的起源和发展)
  - [2.2 React与传统MVC的关系](#22-react与传统mvc的关系)
- [三、编写第一个React应用](#三编写第一个react应用)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 一、项目构建工具 create-react-app

两种创建项目方式

```bash
# 先安装脚手架
npm install create-react-app -g

# 通过脚手架创建项目
create-react-app proname
```

另外一种安装方式：

```bash
npx create-react-app proname
```

npx是node内置的一个工具，它首先会去全局环境去寻找create-react-app，看有没有这个包，如果有，则使用全局的工具包去安装，如果没有，则先下载一个工具包，之后再安装，安装create-react-app后再创建项目。不过在项目创建完成之后，create-react-app就会被自动的移出了，不会污染环境。

> 以后类似需要全局安装的工具，都可以使用npx工具。

在前端领域，如果使用到node、npm、yarn的时候，可以设置镜像。

## 二、关于React

### 2.1 React的起源和发展

react在2013年5月开源的，源于Instagram项目；

国内大厂在2015年逐渐开始使用React项目；

React在国内流行于2015年底、2016年初的时候：写简历的时候，不要写在2015年或者之前就已经开始大量做react项目了，除非在阿里或者facebook。

### 2.2 React与传统MVC的关系

react是一个library，是一个用于构建用户界面的库，不是一个frame，不是框架，更不是一个完整的MVVM框架，它只是MVVM中的View部分。

Vue也不是纯粹的MVVM框架，但是vue有单文件组件系统、指令，从这个角度上来说，比React完整一些，React是没有单文件组件系统和指令集的。

React本身也不一定就是非常认可MVC模式，React将页面拆分成了众多的小模块，每个模块就是一个组件，然后这些组件之间组合、嵌套，形成了一个个功能完善、丰富的页面。

### 2.3 React高性能的体现：虚拟DOM

React两个优势：

1. 组件

   组件思想，让开发效率提升、降低了管理成本

2. 虚拟DOM

   虚拟DOM让用户对产品的体验更好

项目好坏的评价，或者一个工具库、框架的好坏，通常有两个评价因素：

1. 老板，管理者，也可以说是资本方

   关注的是做事情的效率有没有提升，是不是可以投入更少的资源做更多的事情，且质量上还很有保证

2. 用户

   用户的使用体验是不是友好，是不是能够解决用户的问题、痛点。

复杂、繁琐的DOM操作，通常是web项目性能瓶颈的原因。

> Vue的很多优秀的思想是参考了React的，所以说Vue的开发，是站了巨人的肩膀上的。

### 2.4 React的特点和优势

1. 虚拟DOM

2. 组件系统

3. 单向数据流

   react的核心就是数据绑定，所谓的数据绑定，就是指将服务端的数据和前端页面绑定好，开负责只关注实现业务就可以了。

4. jsx语法

   vue中，我们使用render函数构建组件的DOM结构性能较高，因为省区了查找和编译模板的过程。但是在render中利用createElement创建结构的时候代码可读性较低，较为复杂，此时可以利用jsx语法在render中创建DOM，解决这个问题，但前提是需要使用工具来编译jsx。

## 三、编写第一个React应用

通过脚手架搭建的项目，先把src下面的文件全部删除掉。

1. src下新建入口文件：index.js  必须是这个文件名，不可改

   react可以做两件事：

   1. 基于浏览器的web项目
   2. 开发原生的app：native

   入口文件中，先把需要使用到的react核心的文件导入

   ```javascript
   // React变量名按照规范，首字母要大写，但不是技术上一定要这样
   import React from "react";
   /**
    * react可以做基于浏览器的web项目，也可以做native，也就是app
    * 如果是做基于浏览器的web项目，则需要导入react-dom
    * 如果是做native，则需要导入react-native
    */
   import ReactDOM from "react-dom";
   ```

2. 简单的做一个小小的封装

   ```javascript
   // index.js 入口文件，必须是这个文件名
   // React变量名按照规范，首字母要大写，但不是技术上一定要这样
   // import React from "react";
   /**
    * react可以做基于浏览器的web项目，也可以做native，也就是app
    * 如果是做基于浏览器的web项目，则需要导入react-dom
    * 如果是做native，则需要导入react-native
    */
   import ReactDOM from "react-dom";
   import App from "./app";
   
   /**
    * render函数渲染一个模板，也就是段DOM结构
    * 但要注意这段DOM结构外面不要使用引号包裹，这段代码，就是jsx
    * react实现的核心：告诉render函数要渲染什么，以及渲染到哪里，就完成了react的使命了
    */
   ReactDOM.render(
     //   App, // 这里直接App，是不可以的，因为App本身是一个class，而render需要的是一个组件，直接将App按照组件的方式写就可以了，按照组件的方式写，本质上就是一个类实例化的过程
     <App />,
     // document.getElementById("root")
     document.querySelector("#root")
   );
   
   // app.js 定义了一个class类组件
   import React from "react";
   
   class App extends React.Component {
     render() {
       return <div>Hello,经过封装后的jsx组件</div>;
     }
   }
   
   export default App;
   ```

## 四、元素与组件

### 4.1 函数式组件

jsx语法中显示变量，使用一对大括号包裹变量，Vue中使用两对大括号包裹变量

```javascript
import React from "react";
import ReactDOM from "react-dom";

// ReactDOM.render(
//   /**
//    * 这种方式可以让render函数将组件渲染到指定的元素上
//    * 但是假如我想给组件传递参数的时候怎么办呢？现在的jsx是做不到的
//    * 可以把jsx抽离出去，抽离成一个函数，然后函数返回jsx，然后render函数中通过执行抽离出去的函数，这个函数就叫做组件函数
//    * 看下面的代码案例
//    */
//   <div>Hello, React</div>, // jsx
//   document.getElementById("root")
// );

const app = (props) => {
  return <div>Hello,新世界{props}</div>; // jsx中使用一对大括号包裹变量
};

ReactDOM.render(app("!!!"), document.getElementById("root"));
```

React中：

HTML元素，也称为React元素，React元素使用小驼峰的命名方式(camel-case)，即首字母小写

React组件，使用大驼峰的命名方式(pascal-case)，即首字母大写

```javascript
const App = (props) => {
  let title = props.title;
  let name = props.name;
  return (
    <div>
      Hello,{name}
      {title}
    </div>
  );
};

// ReactDOM.render(app("!!!"), document.getElementById("root")); // 组件app()方式，还可以通过<app></app>方式编码

ReactDOM.render(
  <App title="." name="Nicholas" />,
  document.getElementById("root")
);
```

### 4.2 class组件

函数式组件，可以通过给函数传参的方式传递props，那么类组件呢，怎么传递props？

类组件，是把props直接绑定到了class上面，可以通过this.props拿到当前class上的props。

```javascript
/**
 * props默认可以绑定到class上，然后通过this.props获取到当前class上关联的props
 */
class App extends React.Component {
  render() {
    return <div>Hello,Cookie{this.props.title}</div>;
  }
}

ReactDOM.render(<App title="..." />, document.getElementById("root"));
```

### 4.3 更老的一种方法

### 4.4 组件的组合、嵌套