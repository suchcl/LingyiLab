<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. 创建项目](#1-%E5%88%9B%E5%BB%BA%E9%A1%B9%E7%9B%AE)
- [2. Vue3基础知识点](#2-vue3%E5%9F%BA%E7%A1%80%E7%9F%A5%E8%AF%86%E7%82%B9)
  - [2.1 组合式API Composition API](#21-%E7%BB%84%E5%90%88%E5%BC%8Fapi-composition-api)
  - [2.2 Fragment](#22-fragment)
- [3. 路由配置](#3-%E8%B7%AF%E7%94%B1%E9%85%8D%E7%BD%AE)
- [4. 几个常用API](#4-%E5%87%A0%E4%B8%AA%E5%B8%B8%E7%94%A8api)
  - [4.1 setup](#41-setup)
  - [4.2 Suspense](#42-suspense)
    - [4.2.1 异步依赖](#421-%E5%BC%82%E6%AD%A5%E4%BE%9D%E8%B5%96)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 1. 创建项目

> 可以选择自己擅长的或喜欢的脚手架工具，常用的有@vue/cli和vite，在创建项目之前，先安装下脚手架工具。

```bash
# 使用@vue/cli创建vue项目
vue creae 项目名称 

# 使用vite创建vue项目
npm init vite-app 项目名称
```

### 2. Vue3基础知识点

#### 2.1 组合式API Composition API

Composition Api：组合式API

Option API：选项式API

vue2中使用的是OptionAPI，里面有data、methods、computed、watch等钩子函数。

vue3推荐使用CompositionAPI(组合式API)，当然了，OptionApi在vue3中依然适用，熟悉vue2中的data、methods、computed等钩子函数依旧可以在vue3中使用，只是不建议这么做了。

vue3升级了，支持了新的api方式，那么我理解新的实现方式肯定会有它的道理，所以我们还是学习vue3的api吧，学习新的用法。

#### 2.2 Fragment

在vue2中，每个组件都需要有一个根元素，在vue3中打破了这个限制。在每个vue组件中，template下可以有多个平级节点。

```vue
<template>
    <div class="baseinfo"></div>
    <div class="userinfo"></div>
</template>
```

这样可以减少一些标签层级，降低内存的占用.

### 3. 路由配置

为了方便管理，我把router提取到了src/router/index.js文件。

```javascript
import {createWebHistory, createRouter} from "vue-router";
const Home = () => import('@/components/Home.vue');
const BaseInfo = () => import('@/components/UserInfo.vue');
const routes = [
    {
        path: '/home',
        component: Home
    },
    {
        path: '/baseInfo',
        component: BaseInfo
    }
];

const router = createRouter({
    history: createWebHistory(),
    routes
});

export default router;
```

然后在项目的入口文件中导入下vue-router：

```js
// src/main.js
import { createApp } from 'vue'
import App from './App.vue'
import router from './router' // 导入在src/router/index.js中的router信息
createApp(App).use(router).mount('#app') // vue实例装载router插件
```

到这里，已经导入vue-router并完成了vue对vue-router的装载，已经可以在项目中正常使用了。

**路由模式相对于vue-router3的变化**

如果以前使用vue2，这里需要注意下的是配置路由模式的方式有变化，vue-router3及之前的版本中，路由模式的配置方式是配置mode字段就可以了，从vue-router4开始，不需要配置mode属性了，改成配置history属性了。

```js
const router = createRouter({
    // history: createWebHistory(), // HTML5模式(我习惯叫history模式)，需要服务器配置的支持
    history: createWebHashHistory(), // hash模式，url中有#
    routes
});
```

路由模式，究竟使用哪种模式，可以根据自己的项目特点自行选择。在使用HTML5模式的时候，需要服务器的支持，如nginx、apache等web服务器作个代理配置，如果使用hash模式则不需要服务器作任何的配合，直接使用即可。

### 4. 几个常用API

#### 4.1 setup

setup()是Composition API的入口，需要return一个对象

```js
  setup() {
    let baseInfo = {
      city: "北京",
      code: "10010",
    };

    return {
      baseInfo
    };
  },
```

**setup()执行顺序**

setup()在beforeCreate()之前执行一次，beforeCreate()的任务就是初始化，那么在初始化之前，这个时候实例还没有被初始化，还不能调用实例，也就是说不能调用this和$el

**setup()返回值**

setup()函数返回一个对象，这个对象的属性是属性和方法的集合。可以简单的这么理解，setup函数的返回值，就是vue2中data函数的属性和methods中的方法列表。不是在setup()返回的数据和方法，在组件中是不能正常使用的。

```vue
<template>
<button @click="printName">打印城市名</button>
</template>
<script>
    export default{
        setup(){
            let baseInfo = {
            city: "北京",
            code: "10010",
            };
        }

        const printName = () => {
            console.log(baseInfo.city);
        }

        return {
            baseInfo, // 数据，属性
            printName // 方法
        }
    }
</script>
```

#### 4.2 Suspense

<Suspense />是一个内置组件，用来在组件树中协调对异步依赖的处理。它让我们可以在组件树中的上层等待下层的多个嵌套组件中存在的异步依赖项解析完成，并可以在等待时渲染一个状态。

> element-ui,在适配vue2的element，是2.x版本，叫做element-ui。适配vue3的element，叫做element-plus，element-plus不再支持IE11，可以在支持es2018的浏览器上运行。

**vue3导入element-plus**

1. 安装element-plus

```bash
npm install element-plus --save
```

2. 项目导入element-plus并装载

```js
//项目入口文件main.js
import ElementPlus from "element-plus";
import 'element-plus/dist/index.css';

createApp(App).use(ElementPlus).use(router).mount('#app') // 通过use装载element-plus
```

element-plus已经正常导入，项目已经可以正常使用了。

##### 4.2.1 异步依赖

要了解<Suspense />解决的问题以及它是如何与异步依赖进行交互的，我们先想象一种这样的组件层级结构：

```js
<Suspense>
└─ <Dashboard>
   ├─ <Profile>
   │  └─ <FriendStatus>（组件有异步的 setup()）
   └─ <Content>
      ├─ <ActivityFeed> （异步组件）
      └─ <Stats>（异步组件）
```

在这个组件树中的一些组件依赖异步资源，要完全的渲染出这棵组件树，首先需要解析出组件中的异步资源。每个组件都需要处理自己的内部的资源的加载状态，处理报错和完成时的一些事件处理。在一些极端情况下，有可能会看到页面上多个加载中的小动画，然后在不同的时间分别显示出各自组件中的内容。这是一种很不友好的体验。

鉴于这种不友好的体验，<Suspense />组件可以帮助我们实现在等待多个层级组件树中的各个依赖获取结果时，在顶层展示提示架载中的loading或者提示资源处理失败的状态。

在一般的情况下，setup()是不能使用async修饰的，因为async修饰的函数会返回一个promise，返回promise是不能满足我们的页面展示数据的诉求的，方法的调用有的时候也会得不到及时的相应，因为我们不知道什么时候setup()会返回值。

<Suspense />可以等待的异步依赖有两种：

1. 异步的setup()函数

2. 异步组件

### 5. ref

ref,定义响应式数据。这是一个hooks函数，如果有接触过react，那么这里可能会更好理解一些。在使用ref的时候，首先需要从vue导入ref函数.

ref接收、声明一个基础类型的数据。

```js
import { ref } from "vue";
```

通过ref定义的变量的值，实际上是定义在了Ref对象的value属性上了，所以在对通过ref定义的变量的值的时候，修改变量的value属性即可。

```js
const addHeight = () => {
    height.value++;
};
```

#### 5.1 ref获取元素

在使用ref获取元素时，我遇到了一个命名上的问题，但后来不知道为什么好了。