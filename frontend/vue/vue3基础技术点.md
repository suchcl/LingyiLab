<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

**Table of Contents** _generated with [DocToc](https://github.com/thlorenz/doctoc)_

- [1. 简介](#1-%E7%AE%80%E4%BB%8B)
  - [1.1 发布](#11-%E5%8F%91%E5%B8%83)
  - [1.2 Vue3 带来了什么](#12-vue3%E5%B8%A6%E6%9D%A5%E4%BA%86%E4%BB%80%E4%B9%88)
  - [1.3 源码的升级](#13-%E6%BA%90%E7%A0%81%E7%9A%84%E5%8D%87%E7%BA%A7)
  - [1.4 友好的兼容 Typescript](#14-%E5%8F%8B%E5%A5%BD%E7%9A%84%E5%85%BC%E5%AE%B9typescript)
  - [1.5 新特性](#15-%E6%96%B0%E7%89%B9%E6%80%A7)
    - [1.5.1 Composition API(组合式 API)](#151-composition-api%E7%BB%84%E5%90%88%E5%BC%8Fapi)
    - [1.5.2 新的内置组件](#152-%E6%96%B0%E7%9A%84%E5%86%85%E7%BD%AE%E7%BB%84%E4%BB%B6)
    - [1.5.3 其他改变](#153-%E5%85%B6%E4%BB%96%E6%94%B9%E5%8F%98)
- [2.创建 Vue3 项目](#2%E5%88%9B%E5%BB%BAvue3%E9%A1%B9%E7%9B%AE)
  - [2.1 使用@vue/cli 创建 vue3 项目](#21-%E4%BD%BF%E7%94%A8vuecli%E5%88%9B%E5%BB%BAvue3%E9%A1%B9%E7%9B%AE)
  - [2.2 使用 vite 创建 vue3 项目](#22-%E4%BD%BF%E7%94%A8vite%E5%88%9B%E5%BB%BAvue3%E9%A1%B9%E7%9B%AE)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 1. 简介

#### 1.1 发布

2020.9.18 Vue3.0 发布

RFC：请求修改意见稿

https://github.com/vuejs/rfcs/tree/master/active-rfcs rfcs

Vue3 https://github.com/vuejs/vue-next/

#### 1.2 Vue3 带来了什么

打包大小减小了 41%

初次渲染快了 55%，更新渲染快 133%

内存使用减少了 54%

……

#### 1.3 源码的升级

使用 Proxy 代替 Object.defineProperty 实现响应式

重写虚拟 DOM 和 Tree-Shaking

……

> Tree-Shaking,是一个术语，不是什么库。webpack 本身支持 treeshaking

#### 1.4 友好的兼容 Typescript

Vue3 可以更加友好的支持 Typescript

#### 1.5 新特性

##### 1.5.1 Composition API(组合式 API)

setup 配置

ref 与 reactive

watch 与 watchEffect

provide 与 inject

##### 1.5.2 新的内置组件

Fragment

Teleport

Suspense

##### 1.5.3 其他改变

新的生命周期钩子

data 选项应始终被声明为一个函数

移除 keyCode 支持 v-on 修饰符

### 2.创建 Vue3 项目

两种方式创建 Vue3 项目

#### 2.1 使用@vue/cli 创建 vue3 项目

使用@vue/cli 创建 vue3 项目，要求@vue/cli 的版本是 4.5.0 以上版本

查看@vue/cli 版本

```bash
PS D:\> vue -V
@vue/cli 4.5.14
PS D:\> vue --version
@vue/cli 4.5.14
```

两种方式都可以查看@vue/cli 版本。从结果上来看，我的机器是满足要求的。

通过@vue/cli 创建 vue 项目，就是使用 webpack 构建项目。

创建项目

```bash
vue create vue3projectname
```

通过@vue/cli 创建好项目，可以直接进入项目启动服务运行，不需要单独安装 npm 包，因为在创建项目的时候，就已经把 npm 包都已经安装好了。

#### 2.2 使用 vite 创建 vue3 项目

```bash
# 使用npm创建项目
npm init vite

# 使用yarn创建项目
yarn create vite

# 使用pnpm创建项目
pnpm create vite
```

vite 创建项目,默认没有给安装好 npm 包,需要项目创建好之后,自己去手动的执行 npm install 安装 npm 包.所以在创建项目的时候,感觉是 vite 更快了.

但是一般情况下,不讨论项目的创建速度,而是去讨论项目创建完成后,服务的启动速度和编译速度.

vite:下一代的前端构建工具

**vite 的优势:**

1. 开发环境中,无需打包,可快速冷启动;
2. 轻量快速的热重载(HMR)
3. 真正的按需编译,不再等待整个应用编译完成;

vite 动态引入,动态分析,先准备好服务器,再去加载需要的模块

webpack:先准备好模块,然后再去准备服务器.

### 3. vue3 分析

vue3 中,不能再继续使用 Vue2 的构造函数了.

例如在 Vue3 中,不能通过导入 Vue 的方式,然后通过 new Vue 的方式创建 Vue 的实例了.

```js
import Vue from "vue";
import App from "./App.vue";

new Vue({
  render: (h) => h(App),
}).mount("#app");
s;
```

在 vue2 中,这样的代码应该没啥问题,但是<font color="#f20">到了 Vue3 中,这样的代码是绝对不允许的.</font>

Vue3 中,没有实现 Vue 的构造函数,而是通过 createApp 工厂函数去创建 Vue 实例的.

Vue3 中正确的创建 Vue 实例、挂载组件的方式为:

```js
import { createApp } from "vue";
import App from "./App.vue";

createApp(App).mount("#app");
```

> 工厂函数的特点:不能通过 new 来实例化对象,只需直接调用就可以了.

**Vue3 的特点:**

1. 组件可以没有根标签了,但是加上也没有任何问题
   1. Vue2 中的组件,必须要有一个根组件

#### 3.1 安装 vue 开发者工具(浏览器上)

现在(2021.11.9)vue3 的开发者工具还不完善,还在 beta 阶段,不过也不要纠结,有了总比没有好.感恩吧.

### 4.常用 Composition API 组合式 API

什么是组合式 api 呢?先学习,最后再悟什么是组合式 api 吧.

#### 4.1 setup

1. vue3 中新增的一个配置项,值为一个函数
2. setup 是所有组合式 API 表演的舞台:没有 setup,其他的 api 没有合适的地方去写
3. 组件中所用到的:数据、方法、计算属性、生命周期钩子函数等,都要配置在 setup 中
4. setup 函数的两种返回值:
   1. 对象:如果返回一个对象,则对象中的属性、方法,在模板中均可以直接使用 ----- 重点关注
   2. 渲染函数:如果返回一个渲染函数,则可以自定义渲染内容 ------ 了解即可
5. 注意
   1. 尽量不与 vue2.x 配置混用
      1. Vue2.x 配置(data、methods、computed……)可以访问 setup 中的属性、方法
      2. setup 中不能访问 Vue2.x 中的配置(data、methods、computed……)
      3. 如果有重名,setup 优先
   2. setup 不能是一个 async 函数,因为返回值不能再是 return 的对象,而是 promise,模板看不到 return 对象中的属性

setup 中定义的数据、方法,都必须通过 return 返回,被返回后,可以直接在模板中使用.

return 返回的方法,类似 vue2 中 methods 部分定义的方法.

```vue
<template>
  <!--vue3中,可以没有根标签了,但是也可以写,加根标签没有任何问题-->
  <!--根标签是否添加,可以根据实际的场景需要,有时为了性能,可以减少标签嵌套层级,就不加了,但是也有一些特别场景必须需要有这么一个层级,加上也不纠结-->
  <h3>姓名:{{ user.name }}</h3>
  <p>年龄:{{ user.age }}</p>
  <p>身高:{{ user.height }}</p>
  <button @click="sayHello">获取信息</button>
</template>

<script>
export default {
  name: "App",
  // 先测试一下setup,不考虑响应式
  setup() {
    // 定义数据
    let user = {
      name: "Nicholas Zakas",
      age: 18,
      height: 1.88,
    };
    let username = "yan";
    // 定义方法
    function sayHello() {
      console.log(`我是${user.name},今年${user.age}岁了,身高是:${user.height}`);
    }

    // 让setup有返回值,返回值可以在组件中直接使用
    return {
      user,
      username,
      sayHello, // setup返回的方法,类似vue2中methods配置的方法
    };
  },
};
</script>
```

#### 4.2 ref 函数

作用:定义一个响应式的数据

语法: const xxx = ref(initValue);
