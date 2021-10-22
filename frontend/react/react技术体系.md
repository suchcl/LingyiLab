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

### 2.3 React高性能的体现：虚拟DOM

### 2.4 React的特点和优势

## 三、编写第一个React应用

## 四、元素与组件

### 4.1 函数式组件

### 4.2 class组件

### 4.3 更老的一种方法

### 4.4 组件的组合、嵌套