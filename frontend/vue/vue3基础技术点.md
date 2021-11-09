<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. 简介](#1-%E7%AE%80%E4%BB%8B)
  - [1.1 发布](#11-%E5%8F%91%E5%B8%83)
  - [1.2 Vue3带来了什么](#12-vue3%E5%B8%A6%E6%9D%A5%E4%BA%86%E4%BB%80%E4%B9%88)
  - [1.3 源码的升级](#13-%E6%BA%90%E7%A0%81%E7%9A%84%E5%8D%87%E7%BA%A7)
  - [1.4 友好的兼容Typescript](#14-%E5%8F%8B%E5%A5%BD%E7%9A%84%E5%85%BC%E5%AE%B9typescript)
  - [1.5 新特性](#15-%E6%96%B0%E7%89%B9%E6%80%A7)
    - [1.5.1 Composition API(组合式API)](#151-composition-api%E7%BB%84%E5%90%88%E5%BC%8Fapi)
    - [1.5.2 新的内置组件](#152-%E6%96%B0%E7%9A%84%E5%86%85%E7%BD%AE%E7%BB%84%E4%BB%B6)
    - [1.5.3 其他改变](#153-%E5%85%B6%E4%BB%96%E6%94%B9%E5%8F%98)
- [2.创建Vue3项目](#2%E5%88%9B%E5%BB%BAvue3%E9%A1%B9%E7%9B%AE)
  - [2.1 使用@vue/cli创建vue3项目](#21-%E4%BD%BF%E7%94%A8vuecli%E5%88%9B%E5%BB%BAvue3%E9%A1%B9%E7%9B%AE)
  - [2.2 使用vite创建vue3项目](#22-%E4%BD%BF%E7%94%A8vite%E5%88%9B%E5%BB%BAvue3%E9%A1%B9%E7%9B%AE)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 1. 简介

#### 1.1 发布

2020.9.18 Vue3.0发布

RFC：请求修改意见稿

https://github.com/vuejs/rfcs/tree/master/active-rfcs  rfcs 

Vue3  https://github.com/vuejs/vue-next/

#### 1.2 Vue3带来了什么

打包大小减小了41%

初次渲染快了55%，更新渲染快133%

内存使用减少了54%

……

#### 1.3 源码的升级

使用Proxy代替Object.defineProperty实现响应式

重写虚拟DOM和Tree-Shaking

……

> Tree-Shaking,是一个术语，不是什么库。webpack本身支持treeshaking

#### 1.4 友好的兼容Typescript

Vue3可以更加友好的支持Typescript

#### 1.5 新特性

##### 1.5.1 Composition API(组合式API)

setup配置

ref与reactive

watch与watchEffect

provide与inject

##### 1.5.2 新的内置组件

Fragment

Teleport

Suspense

##### 1.5.3 其他改变

新的生命周期钩子

data选项应始终被声明为一个函数

移除keyCode支持v-on修饰符

### 2.创建Vue3项目

两种方式创建Vue3项目

#### 2.1 使用@vue/cli创建vue3项目

使用@vue/cli创建vue3项目，要求@vue/cli的版本是4.5.0以上版本

查看@vue/cli版本

```bash
PS D:\> vue -V
@vue/cli 4.5.14
PS D:\> vue --version
@vue/cli 4.5.14
```

两种方式都可以查看@vue/cli版本。从结果上来看，我的机器是满足要求的。

通过@vue/cli创建vue项目，就是使用webpack构建项目。

创建项目

```bash
vue create vue3projectname
```

通过@vue/cli创建好项目，可以直接进入项目启动服务运行，不需要单独安装npm包，因为在创建项目的时候，就已经把npm包都已经安装好了。

#### 2.2 使用vite创建vue3项目

```bash
# 使用npm创建项目
npm init vite

# 使用yarn创建项目
yarn create vite

# 使用pnpm创建项目
pnpm create vite
```

vite创建项目,默认没有给安装好npm包,需要项目创建好之后,自己去手动的执行npm install安装npm包.所以在创建项目的时候,感觉是vite更快了.

但是一般情况下,不讨论项目的创建速度,而是去讨论项目创建完成后,服务的启动速度和编译速度.

vite:下一代的前端构建工具

**vite的优势:**

1. 开发环境中,无需打包,可快速冷启动;
2. 轻量快速的热重载(HMR)
3. 真正的按需编译,不再等待整个应用编译完成;

vite动态引入,动态分析,先准备好服务器,再去加载需要的模块

webpack:先准备好模块,然后再去准备服务器.

### 3. vue3分析

vue3中,不能再继续使用Vue2的构造函数了.

例如在Vue3中,不能通过导入Vue的方式,然后通过new Vue的方式创建Vue的实例了.

```js
import Vue from "vue";
import App from "./App.vue"

new Vue({
  render:h => h(App)
}).mount("#app");s
```

在vue2中,这样的代码应该没啥问题,但是<font color="#f20">到了Vue3中,这样的代码是绝对不允许的.</font>

Vue3中,没有实现Vue的构造函数,而是通过createApp工厂函数去创建Vue实例的.

Vue3中正确的创建Vue实例、挂载组件的方式为:

```js
import { createApp } from "vue";
import App from "./App.vue";

createApp(App).mount("#app");
```

> 工厂函数的特点:不能通过new来实例化对象,只需直接调用就可以了.

**Vue3的特点:**

1. 组件可以没有根标签了,但是加上也没有任何问题
   1. Vue2中的组件,必须要有一个根组件

#### 3.1 安装vue开发者工具(浏览器上)

现在(2021.11.9)vue3的开发者工具还不完善,还在beta阶段,不过也不要纠结,有了总比没有好.感恩吧.

