<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. js中的|与||、&与&&](#1-js%E4%B8%AD%E7%9A%84%E4%B8%8E%E4%B8%8E)
- [2. &&和||](#2-%E5%92%8C)
  - [2.1 逻辑与&&](#21-%E9%80%BB%E8%BE%91%E4%B8%8E)
  - [2.2 逻辑或||](#22-%E9%80%BB%E8%BE%91%E6%88%96)
  - [2.3 逻辑非!](#23-%E9%80%BB%E8%BE%91%E9%9D%9E)
- [3. |和&](#3-%E5%92%8C)
- [4. 真值(truthy)、假值(falsy)](#4-%E7%9C%9F%E5%80%BCtruthy%E5%81%87%E5%80%BCfalsy)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 1. js中的|与||、&与&&

在js中，经常会用到||和&&，偶尔会用到|和||，这里说经常用到和偶尔用到，并不是就是说||和&&的使用频率一定会高于|和&,只是在普通的开发中，一点感性的印象而已，并不是说这是绝对的统计出来的数据值。

### 2. &&和||

js中的&&和||是逻辑运算符，js中除了&&和||外，还有一个逻辑运算符!.

#### 2.1 逻辑与&&



#### 2.2 逻辑或||

#### 2.3 逻辑非!

### 3. |和&

### 4. 真值(truthy)、假值(falsy)

js中，truthy是指在布尔值上下文中，转换后的值为true的值。

被定义为假值(falsy)以外的所有值都被认定为真值(truthy).

假值(falsy)是指在js中在布尔值的上下文中，转换后的值为false的值。js中有8个falsy值：

| 值         | 说明                                                         |
| ---------- | ------------------------------------------------------------ |
| false      | false关键字                                                  |
| 0          | 数值0                                                        |
| -0         | 数值，负0                                                    |
| 0n         | 当BigInt作为布尔值使用时，遵从其作为数值的规则，0n表示falsy值 |
| ""，''，`` | 空字符串(字符串长度为0)。js中的字符串可使用双引号""、单引号''和模板字面量``来定义 |
| null       | null                                                         |
| undefined  | undefined                                                    |
| NaN        | NaN，非数值                                                  |

