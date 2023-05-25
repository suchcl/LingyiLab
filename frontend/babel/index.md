<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. babel是什么？](#1-babel%E6%98%AF%E4%BB%80%E4%B9%88)
- [2. babel能做什么？](#2-babel%E8%83%BD%E5%81%9A%E4%BB%80%E4%B9%88)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

参考链接：https://www.babeljs.cn/

### 1. babel是什么？

现在的前端项目中，无论是基于vue的开发，还是基于react的开发，都会有一些babel的配置，但是对于它的配置又没有那么重，就导致了很多开发者都知道有这么一个东西存在，但是它到底是干什么的，却很少有几个人能够说的清楚。最近几年在面试时，在和候选人聊的时候，候选人呢都会提到在项目中使用到了babel，做过babel的相关配置，那么具体做了什么配置呢，是为了解决什么问题呢，然后是怎么配置的呢？等等，几乎都说不上来，其中不乏一些5，6年以上工作经验的开发者。

一个简单的理解，说的直接一点，babel就是一个javascript编译器，可以将高版本的js代码编译成低版本的js代码，可以让代码在低版本的浏览器中去执行。

### 2. babel能做什么？

1. 语法转换
2. 通过Polyfill方式在目标环境中添加缺失的特性：通过引入第三方polyfill模块，如core-js
3. 源码转换：codemods

#### 2.1 babel支持新版本语法

Babel通过语法转换器来支持新版本的javascript语法。

> 新版本，一般是指ES2015及更新的版本。

Babel通过一些插件的支持，具备了使用新语法的能力，而不需要等待浏览器的支持。常用的一些插件如下：

#### 2.2 jsx与React

Babel同样也能够转换JSX语法，babel还可以通过和一些编辑器的插件一起使用对JSX的语法提供更加友好的支持，如babel-sublime.