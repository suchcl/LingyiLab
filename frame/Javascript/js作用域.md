<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [作用域的理解](#作用域的理解)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 作用域的理解

作用域，我一般就是简单的理解为变量的可被访问的、有效的范围。

### 1. 作用域的分类

#### 1.1 全局作用域

全局，就是字面意思，如果是一个文件，那么这个变量就是在整个文件中都可被访问，如果是一个项目，那么这个变量就是在整个项目都是可见的，都是可以被访问的。这个全局作用域的生成时间，在文件被打开、被引用，或者项目被打开、被运行时作用域生效，文件关闭、结束引用，或者项目关闭了、停止运行了，作用域自动消失。

一般情况下，在函数外部定义的变量就是全局的变量，拥有全局的作用域；

window是浏览器项目的最顶级的全局对象，也就是说它是浏览器项目中js的最顶级的作用域，也就是说具有着全局的作用域；

```javascript
// 全局作用域
// 定义在了函数外面，是一个全局变量，具有全局的作用域
var username = "Hanmeimei";
function getUserName() {
    return username;
}
console.log(getUserName());
```



#### 1.2 函数作用域

#### 1.3 块级作用域