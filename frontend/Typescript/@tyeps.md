<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [@types介绍](#types%E4%BB%8B%E7%BB%8D)
  - [1. 概述](#1-%E6%A6%82%E8%BF%B0)
  - [2. 工作原理](#2-%E5%B7%A5%E4%BD%9C%E5%8E%9F%E7%90%86)
  - [3. 安装和使用](#3-%E5%AE%89%E8%A3%85%E5%92%8C%E4%BD%BF%E7%94%A8)
  - [4. 来源和维护](#4-%E6%9D%A5%E6%BA%90%E5%92%8C%E7%BB%B4%E6%8A%A4)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### @types介绍

#### 1. 概述

- @tyeps是一个在typescript项目中常用到的工具。它用于管理第三方javascript库的类型声明文件.d.ts文件

- 在Typescript中，类型声明文件提供了一种机制，让Typescript编译器能够理解Javascript库的结构和类型。这对于在Typescript项目中使用javascript库非常重要

#### 2. 工作原理

- 当我们在一个typescript项目中使用一个没有类型声明的第三方的javascript库时，可以通过安装对应的@types包来获取该库的类型定义

- 例如当我们在一个typescript项目中使用jquery时，而jquery库本身并没有提供typescript的类型定义，那么我们这个时候就可以安装@types/jquery包。这个包中包含了jquery库的类型声明文件

- 这个类型声明文件描述了库中的函数、对象、类等的参数类型和返回值类型等信息，使得typescript编译器可以进行类型检查

#### 3. 安装和使用

- 一般情况下，可以直接使用npm或者yarn等包管理器来安装@types包，如安装@tyeps/jquery包，可如下指令：

```bash
npn install @types/jquery --save-dev
```

- 安装完成以后，在我们的typescript项目中就可以直接导入和使用jquery了，typescript编译器会根据@types/jquery中的类型声明进行检查

#### 4. 来源和维护

- @types通常由社区来维护。在DefinitelyTyped这个github仓库中，有大量的@types包被创建和维护。社区成员会根据第三方库的版本更新和API变化来更新对应的@types包，以确保类型声明的准确性。