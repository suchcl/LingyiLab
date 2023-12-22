<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. C语言概述](#1-c%E8%AF%AD%E8%A8%80%E6%A6%82%E8%BF%B0)
  - [1.1 C语言字符集](#11-c%E8%AF%AD%E8%A8%80%E5%AD%97%E7%AC%A6%E9%9B%86)
  - [1.2 C语言单词](#12-c%E8%AF%AD%E8%A8%80%E5%8D%95%E8%AF%8D)
  - [1.3 C语句分类](#13-c%E8%AF%AD%E5%8F%A5%E5%88%86%E7%B1%BB)
  - [1.4 函数分类与使用](#14-%E5%87%BD%E6%95%B0%E5%88%86%E7%B1%BB%E4%B8%8E%E4%BD%BF%E7%94%A8)
  - [1.5 C语言程序的层次结构](#15-c%E8%AF%AD%E8%A8%80%E7%A8%8B%E5%BA%8F%E7%9A%84%E5%B1%82%E6%AC%A1%E7%BB%93%E6%9E%84)
  - [1.6 标准输出函数printf()的使用](#16-%E6%A0%87%E5%87%86%E8%BE%93%E5%87%BA%E5%87%BD%E6%95%B0printf%E7%9A%84%E4%BD%BF%E7%94%A8)
  - [1.7 标准输入函数scanf()的使用](#17-%E6%A0%87%E5%87%86%E8%BE%93%E5%85%A5%E5%87%BD%E6%95%B0scanf%E7%9A%84%E4%BD%BF%E7%94%A8)
  - [1.8 c语言程序的上机操作过程](#18-c%E8%AF%AD%E8%A8%80%E7%A8%8B%E5%BA%8F%E7%9A%84%E4%B8%8A%E6%9C%BA%E6%93%8D%E4%BD%9C%E8%BF%87%E7%A8%8B)
- [2. 基本数据类型和表达式](#2-%E5%9F%BA%E6%9C%AC%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B%E5%92%8C%E8%A1%A8%E8%BE%BE%E5%BC%8F)
  - [2.1 数据类型](#21-%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B)
  - [2.2 常量](#22-%E5%B8%B8%E9%87%8F)
  - [2.3 变量](#23-%E5%8F%98%E9%87%8F)
  - [2.4 运算符和表达式](#24-%E8%BF%90%E7%AE%97%E7%AC%A6%E5%92%8C%E8%A1%A8%E8%BE%BE%E5%BC%8F)
  - [2.5 一些函数的使用](#25-%E4%B8%80%E4%BA%9B%E5%87%BD%E6%95%B0%E7%9A%84%E4%BD%BF%E7%94%A8)
- [3. 流程控制语句](#3-%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6%E8%AF%AD%E5%8F%A5)
  - [3.1 if条件语句](#31-if%E6%9D%A1%E4%BB%B6%E8%AF%AD%E5%8F%A5)
  - [3.2 switch开关语句](#32-switch%E5%BC%80%E5%85%B3%E8%AF%AD%E5%8F%A5)
  - [3.3 for循环语句](#33-for%E5%BE%AA%E7%8E%AF%E8%AF%AD%E5%8F%A5)
  - [3.4 while循环语句](#34-while%E5%BE%AA%E7%8E%AF%E8%AF%AD%E5%8F%A5)
  - [3.5 do循环语句](#35-do%E5%BE%AA%E7%8E%AF%E8%AF%AD%E5%8F%A5)
  - [3.6 跳转类语句](#36-%E8%B7%B3%E8%BD%AC%E7%B1%BB%E8%AF%AD%E5%8F%A5)
- [4. 数组的概念](#4-%E6%95%B0%E7%BB%84%E7%9A%84%E6%A6%82%E5%BF%B5)
  - [4.1 数组的概念](#41-%E6%95%B0%E7%BB%84%E7%9A%84%E6%A6%82%E5%BF%B5)
  - [4.2 一维数组的定义和使用](#42-%E4%B8%80%E7%BB%B4%E6%95%B0%E7%BB%84%E7%9A%84%E5%AE%9A%E4%B9%89%E5%92%8C%E4%BD%BF%E7%94%A8)
  - [4.3 二维数组的定义和使用](#43-%E4%BA%8C%E7%BB%B4%E6%95%B0%E7%BB%84%E7%9A%84%E5%AE%9A%E4%B9%89%E5%92%8C%E4%BD%BF%E7%94%A8)
  - [4.4 使用typedef语句定义数组类型](#44-%E4%BD%BF%E7%94%A8typedef%E8%AF%AD%E5%8F%A5%E5%AE%9A%E4%B9%89%E6%95%B0%E7%BB%84%E7%B1%BB%E5%9E%8B)
  - [4.5 数组的应用](#45-%E6%95%B0%E7%BB%84%E7%9A%84%E5%BA%94%E7%94%A8)
  - [4.6 字符串的定义与应用](#46-%E5%AD%97%E7%AC%A6%E4%B8%B2%E7%9A%84%E5%AE%9A%E4%B9%89%E4%B8%8E%E5%BA%94%E7%94%A8)
- [5. 指针的概念](#5-%E6%8C%87%E9%92%88%E7%9A%84%E6%A6%82%E5%BF%B5)
  - [5.1 指针的概念](#51-%E6%8C%87%E9%92%88%E7%9A%84%E6%A6%82%E5%BF%B5)
  - [5.2 指针变量的定义和使用](#52-%E6%8C%87%E9%92%88%E5%8F%98%E9%87%8F%E7%9A%84%E5%AE%9A%E4%B9%89%E5%92%8C%E4%BD%BF%E7%94%A8)
  - [5.3 指针运算](#53-%E6%8C%87%E9%92%88%E8%BF%90%E7%AE%97)
  - [5.4 指针与数组的关系](#54-%E6%8C%87%E9%92%88%E4%B8%8E%E6%95%B0%E7%BB%84%E7%9A%84%E5%85%B3%E7%B3%BB)
  - [5.5 变量存储空间的动态分配](#55-%E5%8F%98%E9%87%8F%E5%AD%98%E5%82%A8%E7%A9%BA%E9%97%B4%E7%9A%84%E5%8A%A8%E6%80%81%E5%88%86%E9%85%8D)
  - [5.6 使用指针和动态存储分配的程序举例](#56-%E4%BD%BF%E7%94%A8%E6%8C%87%E9%92%88%E5%92%8C%E5%8A%A8%E6%80%81%E5%AD%98%E5%82%A8%E5%88%86%E9%85%8D%E7%9A%84%E7%A8%8B%E5%BA%8F%E4%B8%BE%E4%BE%8B)
- [6. 函数的定义](#6-%E5%87%BD%E6%95%B0%E7%9A%84%E5%AE%9A%E4%B9%89)
  - [6.1 函数的定义](#61-%E5%87%BD%E6%95%B0%E7%9A%84%E5%AE%9A%E4%B9%89)
  - [6.2 函数的使用](#62-%E5%87%BD%E6%95%B0%E7%9A%84%E4%BD%BF%E7%94%A8)
  - [6.3 变量的作用域](#63-%E5%8F%98%E9%87%8F%E7%9A%84%E4%BD%9C%E7%94%A8%E5%9F%9F)
  - [6.4 分析变量作用域的程序举例](#64-%E5%88%86%E6%9E%90%E5%8F%98%E9%87%8F%E4%BD%9C%E7%94%A8%E5%9F%9F%E7%9A%84%E7%A8%8B%E5%BA%8F%E4%B8%BE%E4%BE%8B)
  - [6.5 递归函数和函数指针](#65-%E9%80%92%E5%BD%92%E5%87%BD%E6%95%B0%E5%92%8C%E5%87%BD%E6%95%B0%E6%8C%87%E9%92%88)
  - [6.6 利用函数编写应用程序举例](#66-%E5%88%A9%E7%94%A8%E5%87%BD%E6%95%B0%E7%BC%96%E5%86%99%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F%E4%B8%BE%E4%BE%8B)
- [7. 结构类型的定义](#7-%E7%BB%93%E6%9E%84%E7%B1%BB%E5%9E%8B%E7%9A%84%E5%AE%9A%E4%B9%89)
  - [7.1 结构类型的定义](#71-%E7%BB%93%E6%9E%84%E7%B1%BB%E5%9E%8B%E7%9A%84%E5%AE%9A%E4%B9%89)
  - [7.2 结构变量的定义和成员访问](#72-%E7%BB%93%E6%9E%84%E5%8F%98%E9%87%8F%E7%9A%84%E5%AE%9A%E4%B9%89%E5%92%8C%E6%88%90%E5%91%98%E8%AE%BF%E9%97%AE)
  - [7.3 结构成员的访问](#73-%E7%BB%93%E6%9E%84%E6%88%90%E5%91%98%E7%9A%84%E8%AE%BF%E9%97%AE)
  - [7.4 结构与链表](#74-%E7%BB%93%E6%9E%84%E4%B8%8E%E9%93%BE%E8%A1%A8)
  - [7.5 联合定义与使用](#75-%E8%81%94%E5%90%88%E5%AE%9A%E4%B9%89%E4%B8%8E%E4%BD%BF%E7%94%A8)
  - [7.6 使用结构的应用编程举例](#76-%E4%BD%BF%E7%94%A8%E7%BB%93%E6%9E%84%E7%9A%84%E5%BA%94%E7%94%A8%E7%BC%96%E7%A8%8B%E4%B8%BE%E4%BE%8B)
- [8. 文件的概念](#8-%E6%96%87%E4%BB%B6%E7%9A%84%E6%A6%82%E5%BF%B5)
  - [8.1 文件的概念](#81-%E6%96%87%E4%BB%B6%E7%9A%84%E6%A6%82%E5%BF%B5)
  - [8.2 文件的打开和关闭](#82-%E6%96%87%E4%BB%B6%E7%9A%84%E6%89%93%E5%BC%80%E5%92%8C%E5%85%B3%E9%97%AD)
  - [8.3 文本文件的输出和访问操作](#83-%E6%96%87%E6%9C%AC%E6%96%87%E4%BB%B6%E7%9A%84%E8%BE%93%E5%87%BA%E5%92%8C%E8%AE%BF%E9%97%AE%E6%93%8D%E4%BD%9C)
  - [8.4 文本文件的输入访问操作](#84-%E6%96%87%E6%9C%AC%E6%96%87%E4%BB%B6%E7%9A%84%E8%BE%93%E5%85%A5%E8%AE%BF%E9%97%AE%E6%93%8D%E4%BD%9C)
  - [8.5 二进制文件的访问操作](#85-%E4%BA%8C%E8%BF%9B%E5%88%B6%E6%96%87%E4%BB%B6%E7%9A%84%E8%AE%BF%E9%97%AE%E6%93%8D%E4%BD%9C)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 1. C语言概述

#### 1.1 C语言字符集

**C语言字符集**

字符、单词、语句、函数模块、程序文件、完成程序，主要可以分为以下几大类：

1. 大小写的英文字母(52个)

a-z，A-Z

C语言中的字符区分大小写，如a和A被认为是不同的字符，GO和go也被认为是不同的字符。

2. 十进制数字符号(10个)

0-9

3. 表点符号

,:;''""空格{}等

4. 单字符运算符号

()[]+-*/%.>=<!~&^|?

5. 特殊用途的符号

井号#、反斜杠\、下划线_

含128个单字节的ASCII编码表

含65536个字符的双字节的Unicode编码表

一对双引号括起来的为字符串，其中可以是任何的字符，如"name=Lily"、"年龄:16"都是合法的字符串

**区分大小写**

C语言中字符是区分大小写的，如A和a被认为是两个不同的字符，Name和name也被认为是两个不同的变量。

#### 1.2 C语言单词

C语言中允许使用的字符按照一定的组词规则就看看呀构成各种不同用途的单词。

C语言的单词分为5类：

1. 保留字

   c语言系统中已经定义好的、具有确定含义的英文单词，被称为保留字，也可以称为关键字。

   Visual C++6.0中关于C语言部分的保留字共有32个，具体可参考下表：

   | auto    | struct   | for    | case   | typedef | sizeof | int      | extern |
   | ------- | -------- | ------ | ------ | ------- | ------ | -------- | ------ |
   | default | volatile | short  | double | char    | union  | register | long   |
   | float   | break    | switch | goto   | else    | const  | unsigned | static |
   | return  | do       | while  | signed | if      | enum   | continue | void   |

   在以井(#)号字符开头的预处理命令中，其命令关键字虽然不被算作C语言中的保留字，但是最好把它们当作保留字看待，不要在自己编写的代码中使用这些字符，以免引起混乱。这些预处理命令关键字有字；include、define、if、else、ifdef、ifndef、endif、undef等。

2. 标识符

   C语言中使用到的标识符是用户在程序设计中给所使用到的对象(如常量、变量、函数、自定义数据类型等)进行标识的名字，也就是使用到的各种数据的名字。

   C语言中规定：标识符必须由英文字母、十进制数字和下划线组成，并且首字符只能是字母或者下划线。

   > 以前的C语言中，$也可以作为标识符的组成部分，但是新教材中没有说到$，现在不确认$是否已经不能作为C语言标识符的组成部分了。

   每个标识符的长度是任意的，但是只有前32位是有效的,也就是说，一般情况下，标识符也就是1-32个字符组成

   常用的标识符命名规则由下划线命名法、大驼峰命名法、小驼峰命名法

3. 常量

   C语言中的常量分为数值常量、字符常量喝字符串常量三种。

   日常使用的十进制数可以直接作为C语言中的数值常量使用，数值常量又可以细分为整数常量和实数常量(带小数点的常量)两种。

   整数常量简称整数，实数常量简称实数。

   C语言中的字符常量就是ASCII字符，表示时为了区分它同单个字符的标识(表示某个字符的变量)和数值的区别，必须将字符常量使用单引号扩起来。

   字符串常量就是使用双引号扩起来的字符序列。

4. 运算符

5. 分隔符

#### 1.3 C语句分类

C语言中将语句大概可以分成8类(不同的编程语言、不同的开发者根据不同的理解、不同的角度也可能会有不同的分类，但是本质上要做的事情是一致的)

1. 用户自定义类型语句

用户通过typedef自定义的类型的语句。typedef string User，typedef int iage

2. 变量定义语句

定义变量的语句，int a = 21

3. 函数原型语句

4. 表达式语句

5. 复合语句

6. 选择类语句

7. 循环类语句

8. 跳转类语句

#### 1.4 函数分类与使用

#### 1.5 C语言程序的层次结构

#### 1.6 标准输出函数printf()的使用

#### 1.7 标准输入函数scanf()的使用

#### 1.8 c语言程序的上机操作过程

### 2. 基本数据类型和表达式

#### 2.1 数据类型

#### 2.2 常量

#### 2.3 变量

#### 2.4 运算符和表达式

#### 2.5 一些函数的使用

### 3. 流程控制语句

#### 3.1 if条件语句

#### 3.2 switch开关语句

#### 3.3 for循环语句

#### 3.4 while循环语句

#### 3.5 do循环语句

#### 3.6 跳转类语句

### 4. 数组的概念

#### 4.1 数组的概念

#### 4.2 一维数组的定义和使用

#### 4.3 二维数组的定义和使用

#### 4.4 使用typedef语句定义数组类型

#### 4.5 数组的应用

#### 4.6 字符串的定义与应用

### 5. 指针的概念

#### 5.1 指针的概念

#### 5.2 指针变量的定义和使用

#### 5.3 指针运算

#### 5.4 指针与数组的关系

#### 5.5 变量存储空间的动态分配

#### 5.6 使用指针和动态存储分配的程序举例

### 6. 函数的定义

#### 6.1 函数的定义

#### 6.2 函数的使用

#### 6.3 变量的作用域

#### 6.4 分析变量作用域的程序举例

#### 6.5 递归函数和函数指针

#### 6.6 利用函数编写应用程序举例

### 7. 结构类型的定义

#### 7.1 结构类型的定义

#### 7.2 结构变量的定义和成员访问

#### 7.3 结构成员的访问

#### 7.4 结构与链表

#### 7.5 联合定义与使用

#### 7.6 使用结构的应用编程举例

### 8. 文件的概念

#### 8.1 文件的概念

#### 8.2 文件的打开和关闭

#### 8.3 文本文件的输出和访问操作

#### 8.4 文本文件的输入访问操作

#### 8.5 二进制文件的访问操作