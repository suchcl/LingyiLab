<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. Promise简单认识](#1-promise%E7%AE%80%E5%8D%95%E8%AE%A4%E8%AF%86)
- [2. 术语](#2-%E6%9C%AF%E8%AF%AD)
- [3. 要求](#3-%E8%A6%81%E6%B1%82)
  - [3.1 Promise状态 --- status](#31-promise%E7%8A%B6%E6%80%81-----status)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 1. Promise简单认识

Promise表示最终操作的结果，与它进行交互的主要是then方法，then方法注册了两个回调函数，分别用来接收promise执行成功的结果和执行失败的原因。

核心的Promises/A+规范不涉及怎么去创建、实现和拒绝promise，而是专注于提供一个通用的then方法。

### 2. 术语

1. promise:一个对象或者函数，并且拥有符合本规范的then方法；
2. thenable：是定义then方法的对象或者函数；
3. value：是任意合法的javascript值，包括undefined、thenable、promise等；
4. exception：使用throw语句抛出的值；
5. reason：表示一个promise被拒绝的原因；

### 3. 要求

#### 3.1 Promise状态 --- status

一个Promise的状态，必须是一下3种状态之一：等待态(Pending)、完成态(Fulfilled)和拒绝态(Rejected).

