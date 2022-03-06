<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. Promise简单认识](#1-promise%E7%AE%80%E5%8D%95%E8%AE%A4%E8%AF%86)
- [2. 术语](#2-%E6%9C%AF%E8%AF%AD)
- [3. 要求](#3-%E8%A6%81%E6%B1%82)
  - [3.1 Promise状态 --- status](#31-promise%E7%8A%B6%E6%80%81-----status)
  - [3.2 then方法](#32-then%E6%96%B9%E6%B3%95)
  - [3.3 Promise解决过程](#33-promise%E8%A7%A3%E5%86%B3%E8%BF%87%E7%A8%8B)

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

1. 当promise是等待态(Pending)时：
    - 可以改变为完成态(Fulfilled)或者拒绝态(Rejected)
2. 当promise是完成态(Fulfilled)时：
    - promise不能改变为其他状态
    - 必须要有一个值value，且不能改变；
3. 当promise是拒绝态(Rejected)时：
    - promise不能被修改为其他状态；
    - 必须要有一个原因reason,并且不能改变；
这里说的不能改变，指的是恒等(即通过===判断相等)，而不是意味着更深层次的不能改变(指当value或reason不是基本类型值时，只要其引用地址相等，但是属性值可以被更改)。

#### 3.2 then方法

一个promise必须提供一个then方法来接收当前promise的的完成的值(value)或拒绝的原因(reason)

每一个promise的then都接收2个参数：

```js
promise.then(onFulfilled, onRejected);
```

1. onFulfilled和onRejcted都是可选参数： 
    - 如果onFulfilled不是函数，则必须省略；
    - 如果onRejected不是函数，则必须省略；
2. 如果onFulfilled是一个函数：
    - 此函数必须在promise完成(Fulfilled)后被调用，且以promise的值(value)作为它的第一个参数；
    - 此函数在promise完成(Fulfilled)之前一定不能被调用；
    - 此函数只能被调用一次；
3. 如果onRejected是一个函数
    - 此函数必须在promise被拒绝(onRejected)后被调用，且以promise拒绝的原因(reason)作为它的第一个参数；
    - 此函数在promise拒绝(onRejected)之前一定不能被调用；
    - 此函数只能被调用一次；
4. 在执行上下文堆栈仅包含平台代码之前，不得调用onFulfilled和onRejected；
5. onFulfilled和onRejected只能被当作回调函数调用，即没有this值；
6. then方法可以在同一个promise里被调用多次：
    - 如果当promise完成(Fulfilled)时，所有相应的onFulfilled回调必须按照then的顺序依次执行；
    - 如果当promise拒绝(Rejected)时，所有相应的onRejected回调必须按照then的顺序一次执行；
7. then方法必须返回一个promise

```js
promise2 = promise.then(onFulfilled, onRejected);
```
- 如果onFulfilled或者onRejected返回一个值x，则运行下面的Promise解决过程：
[[resolve]](promise2,x)
- 如果onFulfilled或者onRejected抛出一个异常e，则promise2必须拒绝(Rejected),并返回异常e的原因(reason);
- 如果onFulfilled不是函数且promise1完成(Fulfilled)执行，promise2必须完成执行(Fulfilled),并返回和promise1相同的值(value);
- 如果onRejected不是函数且promise1是拒绝(Reject)状态，promise2也必须是拒绝(Rejected)，且返回和promise1相同的原因(reason);

#### 3.3 Promise解决过程

