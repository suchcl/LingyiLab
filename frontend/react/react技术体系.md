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

## 四、元素与组件

### 4.1 函数式组件

### 4.2 class组件

### 4.3 更老的一种方法

### 4.4 组件的组合、嵌套