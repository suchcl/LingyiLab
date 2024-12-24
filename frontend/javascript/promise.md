<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. Promise简单认识](#1-promise%E7%AE%80%E5%8D%95%E8%AE%A4%E8%AF%86)
- [2. 术语](#2-%E6%9C%AF%E8%AF%AD)
- [3. 要求](#3-%E8%A6%81%E6%B1%82)
  - [3.1 Promise状态 --- status](#31-promise%E7%8A%B6%E6%80%81-----status)
  - [3.2 then方法](#32-then%E6%96%B9%E6%B3%95)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 1. Promise简单认识

1. 定义：promise是异步编程的一种解决方案，它是一个对象，代表了一个异步操作的最终结果，这个结果涵盖了异步操作的成功或者失败及其结果值。简单来说，它就像是一个对未来某个时刻才会知道结果的事件的承诺。

2. 状态机模型：Promise有三种状态，分别是pending(进行中)、fulfilled(已成功)、rejected(已失败)。一个promise对象的状态只能从pending转换为fulfilled或者rejected，并且这个转换是不可逆的。

### 2. 创建promise

```ts
const myPromis = new Promise((resolve, reject) => {
    const data = {};
    if(true){
        resolve(data);
    }else {
        reject("error");
    }
})
```

### 3. promise的使用场景

#### 3.1. 网络请求



#### 3.2. 文件读写

#### 3.3. 定时器相关场景

#### 3.4. 数据库操作相关

中文：https://www.ituring.com.cn/article/66566

英文原文地址：https://promisesaplus.com/
