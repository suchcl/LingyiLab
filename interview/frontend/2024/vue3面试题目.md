<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. 构建工具webpack和vite的对比](#1-%E6%9E%84%E5%BB%BA%E5%B7%A5%E5%85%B7webpack%E5%92%8Cvite%E7%9A%84%E5%AF%B9%E6%AF%94)
  - [1.1 构建方式](#11-%E6%9E%84%E5%BB%BA%E6%96%B9%E5%BC%8F)
  - [1.2 启动速度](#12-%E5%90%AF%E5%8A%A8%E9%80%9F%E5%BA%A6)
  - [1.3 热模块替换(HMR)](#13-%E7%83%AD%E6%A8%A1%E5%9D%97%E6%9B%BF%E6%8D%A2hmr)
  - [1.4 配置复杂度](#14-%E9%85%8D%E7%BD%AE%E5%A4%8D%E6%9D%82%E5%BA%A6)
  - [1.5 插件生态](#15-%E6%8F%92%E4%BB%B6%E7%94%9F%E6%80%81)
  - [1.6 性能](#16-%E6%80%A7%E8%83%BD)
  - [1.7 支持的框架(兼容性)](#17-%E6%94%AF%E6%8C%81%E7%9A%84%E6%A1%86%E6%9E%B6%E5%85%BC%E5%AE%B9%E6%80%A7)
- [2. vue3实现了重大性能提升体现的具体方面](#2-vue3%E5%AE%9E%E7%8E%B0%E4%BA%86%E9%87%8D%E5%A4%A7%E6%80%A7%E8%83%BD%E6%8F%90%E5%8D%87%E4%BD%93%E7%8E%B0%E7%9A%84%E5%85%B7%E4%BD%93%E6%96%B9%E9%9D%A2)
  - [2.1 静态提升(Static Tree Hoisting)](#21-%E9%9D%99%E6%80%81%E6%8F%90%E5%8D%87static-tree-hoisting)
  - [2.2 预字符串化(Pre-Rendering)](#22-%E9%A2%84%E5%AD%97%E7%AC%A6%E4%B8%B2%E5%8C%96pre-rendering)
  - [2.3 缓存事件处理函数(Cache Event Handler Functions)](#23-%E7%BC%93%E5%AD%98%E4%BA%8B%E4%BB%B6%E5%A4%84%E7%90%86%E5%87%BD%E6%95%B0cache-event-handler-functions)
  - [2.4 块树(Block Tree)](#24-%E5%9D%97%E6%A0%91block-tree)
  - [2.5 布丁标记(Patch Flags)](#25-%E5%B8%83%E4%B8%81%E6%A0%87%E8%AE%B0patch-flags)
- [3. 为什么Vue3去掉了构造函数](#3-%E4%B8%BA%E4%BB%80%E4%B9%88vue3%E5%8E%BB%E6%8E%89%E4%BA%86%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0)
  - [3.1 简化API设计](#31-%E7%AE%80%E5%8C%96api%E8%AE%BE%E8%AE%A1)
  - [3.2 提供灵活性](#32-%E6%8F%90%E4%BE%9B%E7%81%B5%E6%B4%BB%E6%80%A7)
  - [3.3 Tree Shaking](#33-tree-shaking)
  - [3.4 小结](#34-%E5%B0%8F%E7%BB%93)
- [4. vue3数据响应式的理解](#4-vue3%E6%95%B0%E6%8D%AE%E5%93%8D%E5%BA%94%E5%BC%8F%E7%9A%84%E7%90%86%E8%A7%A3)
  - [4.1 Proxy和Reflect](#41-proxy%E5%92%8Creflect)
  - [4.2 Reactive和Ref](#42-reactive%E5%92%8Cref)
  - [4.3 依赖收集与触发更新](#43-%E4%BE%9D%E8%B5%96%E6%94%B6%E9%9B%86%E4%B8%8E%E8%A7%A6%E5%8F%91%E6%9B%B4%E6%96%B0)
  - [4.4 Computed与Watch](#44-computed%E4%B8%8Ewatch)
  - [4.5 响应式系统的优势](#45-%E5%93%8D%E5%BA%94%E5%BC%8F%E7%B3%BB%E7%BB%9F%E7%9A%84%E4%BC%98%E5%8A%BF)
- [5. vue3中v-model的变化](#5-vue3%E4%B8%ADv-model%E7%9A%84%E5%8F%98%E5%8C%96)
  - [5.1 更灵活的自定义组件支持](#51-%E6%9B%B4%E7%81%B5%E6%B4%BB%E7%9A%84%E8%87%AA%E5%AE%9A%E4%B9%89%E7%BB%84%E4%BB%B6%E6%94%AF%E6%8C%81)
  - [5.2 多值绑定](#52-%E5%A4%9A%E5%80%BC%E7%BB%91%E5%AE%9A)
  - [5.3 性能优化](#53-%E6%80%A7%E8%83%BD%E4%BC%98%E5%8C%96)
  - [5.4 移除.sync修饰符](#54-%E7%A7%BB%E9%99%A4sync%E4%BF%AE%E9%A5%B0%E7%AC%A6)
  - [5.5 自定义v-model指令](#55-%E8%87%AA%E5%AE%9A%E4%B9%89v-model%E6%8C%87%E4%BB%A4)
- [6. vue3中异步组件的用法](#6-vue3%E4%B8%AD%E5%BC%82%E6%AD%A5%E7%BB%84%E4%BB%B6%E7%9A%84%E7%94%A8%E6%B3%95)
  - [6.1 基本用法](#61-%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95)
  - [6.2 加载状态和错误处理](#62-%E5%8A%A0%E8%BD%BD%E7%8A%B6%E6%80%81%E5%92%8C%E9%94%99%E8%AF%AF%E5%A4%84%E7%90%86)
  - [6.3 结合Suspense使用](#63-%E7%BB%93%E5%90%88suspense%E4%BD%BF%E7%94%A8)
  - [6.4 动态导入](#64-%E5%8A%A8%E6%80%81%E5%AF%BC%E5%85%A5)
  - [6.5 结合路由使用](#65-%E7%BB%93%E5%90%88%E8%B7%AF%E7%94%B1%E4%BD%BF%E7%94%A8)
  - [6.6 高级用法：自定义加载逻辑](#66-%E9%AB%98%E7%BA%A7%E7%94%A8%E6%B3%95%E8%87%AA%E5%AE%9A%E4%B9%89%E5%8A%A0%E8%BD%BD%E9%80%BB%E8%BE%91)
  - [6.7 与Vue2的对比](#67-%E4%B8%8Evue2%E7%9A%84%E5%AF%B9%E6%AF%94)
  - [6.8 封装加载异步组件的工具类](#68-%E5%B0%81%E8%A3%85%E5%8A%A0%E8%BD%BD%E5%BC%82%E6%AD%A5%E7%BB%84%E4%BB%B6%E7%9A%84%E5%B7%A5%E5%85%B7%E7%B1%BB)
- [7. composition API相比Options API的优势](#7-composition-api%E7%9B%B8%E6%AF%94options-api%E7%9A%84%E4%BC%98%E5%8A%BF)
- [8. vue3 setup的作用和原理以及script setup做了什么事](#8-vue3-setup%E7%9A%84%E4%BD%9C%E7%94%A8%E5%92%8C%E5%8E%9F%E7%90%86%E4%BB%A5%E5%8F%8Ascript-setup%E5%81%9A%E4%BA%86%E4%BB%80%E4%B9%88%E4%BA%8B)
- [9. 介绍pinia以及其持久化最佳实践](#9-%E4%BB%8B%E7%BB%8Dpinia%E4%BB%A5%E5%8F%8A%E5%85%B6%E6%8C%81%E4%B9%85%E5%8C%96%E6%9C%80%E4%BD%B3%E5%AE%9E%E8%B7%B5)
- [10. ref和reactive的区别源码级别的比较](#10-ref%E5%92%8Creactive%E7%9A%84%E5%8C%BA%E5%88%AB%E6%BA%90%E7%A0%81%E7%BA%A7%E5%88%AB%E7%9A%84%E6%AF%94%E8%BE%83)
- [11. keep-alive的最佳实践](#11-keep-alive%E7%9A%84%E6%9C%80%E4%BD%B3%E5%AE%9E%E8%B7%B5)
- [12. vuex最佳实践以及持久化方案](#12-vuex%E6%9C%80%E4%BD%B3%E5%AE%9E%E8%B7%B5%E4%BB%A5%E5%8F%8A%E6%8C%81%E4%B9%85%E5%8C%96%E6%96%B9%E6%A1%88)
- [拷问：既然现在vite的优势那么多，也那么明显，那么vite会取代webpack吗？](#%E6%8B%B7%E9%97%AE%E6%97%A2%E7%84%B6%E7%8E%B0%E5%9C%A8vite%E7%9A%84%E4%BC%98%E5%8A%BF%E9%82%A3%E4%B9%88%E5%A4%9A%E4%B9%9F%E9%82%A3%E4%B9%88%E6%98%8E%E6%98%BE%E9%82%A3%E4%B9%88vite%E4%BC%9A%E5%8F%96%E4%BB%A3webpack%E5%90%97)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 1. 构建工具webpack和vite的对比

### 1.1 构建方式

- webpack:采用打包的方式，首先将所有的模块和资源进行静态分析，生成一个或多个包含所有依赖的打包后的文件。这个过程在开发阶段可能会感觉比较慢，因为代码每次修改后都需要重新打包。

- vite:使用原生的ES模块(ESM)，支持热模块替换(HMR)，在开发阶段不需要打包，而是通过服务器直接提供模块文件，速度更快。只有在生产环境中，vite才会打包代码(使用rollup进行打包)。因此在开发阶段，vite使用的是ESM，所以代码中不能够使用CommonJS。

### 1.2 启动速度

- webpack:首次构建较慢，尤其是在项目较大或者依赖较多的时候。增量构建时则会好一点，但整体来说，构建速度上，webpack不占据优势。

- vite:由于Vite使用的是ESM，不需要编译，不需要进行模块之间的依赖分析，所以启动速度较快，通常能够在几秒之内就够启动开发服务器。项目越负责、依赖越多，vite的优势就越明显。

### 1.3 热模块替换(HMR)

- webpack:支持HMR，但是在某些情况下如全局状态变更的时候，可能会出现页面闪烁，这是因为需要把该模块的所有依赖项都要编译一遍。

- vite:HMR机制非常高效，能够在大部分情况下保持应用状态，更新速度也非常快，改动一个模块仅仅需要浏览器重新请求该模块即可。

### 1.4 配置复杂度

- webpack:配置相对复杂，需要许多插件和loaders来处理不同的文件。对于新手来说，学习曲线较陡，有一定的学习成本。

- vite:配置简单，提高了开发效率，内置了许多常用功能，适合快速开发和原型设计。

### 1.5 插件生态

- webpack:拥有丰富的插件生态，几乎可以处理任何的构建需求，非常适合大型、复杂的项目

- vite:插件生态在快速更新迭代中，支持多种插件来扩展各种能力 —— 就是vite的插件生态，相对于webpack还有些差距。

### 1.6 性能

- webpack:在生产构建时性能强大，能够进行代码分割、懒加载等优化

- vite:在开发时性能优越，但是在某些情况下，生产构建相对于webpack相对不足——不过vite更新迭代很快，这一点应该也会很快就会有改善

### 1.7 支持的框架(兼容性)

- webpack:兼容性友好，支持React、Vue、Angular等多种前端框架；

- vite:对前端框架的支持也很友好，并提供了以框架为中心的优化；

## 2. vue3实现了重大性能提升体现的具体方面

### 2.1 静态提升(Static Tree Hoisting)

静态提升是指在编译阶段识别出不变的部分，将其提升为静态节点，从而避免不必要的重新渲染。

- 静态节点：对于那些不会改变的节点，vue3会在编译的时候将其提取出来，只在首次渲染时创建，而在后续更新时不需要再次处理这些节点

- 减少重复渲染：通过静态提升，vue3减少了对于静态内容的重复渲染，从而提高了性能，特别是在大型列表和复杂组件中

```vue
<template>
    <div class="home">
        <h3>首页</h3> <!-- 静态提升 -->
        {{ message }}
    </div>
</template>

<script setup lang="ts">
// <h3>首页</h3>是一个静态节点，vue3会在编译的时候识别并提升它，避免在每次渲染时都重新创建
import { ref } from 'vue';
const message = ref('Hello Vue!');
</script>

<style scoped></style>
```

### 2.2 预字符串化(Pre-Rendering)

预字符串化是指将模板编译为字符串形式，并在运行时直接使用

- 编译优化：在运行时直接使用预编译的字符串，避免了复杂的解析过程

- 提高渲染速度：通过减少不必要的编译和解析步骤，提升了渲染速度

```vue
<template>
    <div class="home">
        {{ concatStr }}
    </div>
</template>

<script setup lang="ts">
const str1 = "Hello";
const str2 = "World";
const concatStr = `${str1},${str2}`; // 预字符串化
</script>

<style scoped></style>
```

### 2.3 缓存事件处理函数(Cache Event Handler Functions)

vue3对事件处理函数进行了缓存优化

- 函数重用：在组件更新时，重复的事件处理函数不会被重新创建，而是复用之前创建的函数

- 提升性能：通过函数重用，减少了内存开销和函数创建的次数，提高了性能和效率

```vue
<template>
    <div class="home">
        <button @click="handleClick">Click me!</button>
    </div>
</template>

<script setup lang="ts">
// vue3中事件处理函数handleClick只会被创建1次，然后被缓存，当组件更新时函数不会被重新创建
const handleClick = () => {
    console.log('%c [  ]-22', 'font-size:13px; background:pink; color:#bf2c9f;', "Hello Vue3!");
}
</script>
```

### 2.4 块树(Block Tree)

块树是指在虚拟DOM中引入一种新的数据结构，用于优化渲染

- 组件分块：将组件分为多个块，每个块独立处理自己的更新，提升了更新时的颗粒度

- 控制渲染：通过高效管理不同块之间的逻辑关系，vue3可以精准的控制哪些部分需要更新渲染，从而提升渲染性能

> 这个说的就比较抽象了，其实这就是虚拟DOM的优势，只更新变化的部分，源码部分没有看过，总觉着这个地方说的优点牵强了

```vue
<template>
    <div class="home">
        <h3>{{ title }}</h3>
        <p v-for="item in terms" key="item.id">{{ item.text }}</p>
    </div>
</template>

<script setup lang="ts">
// <h3>和<p>标签分别组成了不同的块，vue3可以分别处理它们的更新，如title的变更则只会重新渲染h3标签，而p标签的更新则只会重新渲染p标签
import { ref, reactive } from 'vue';
const title = ref("Home ");
const terms = reactive([
    {
        id: 1,
        text: "Item 1"
    },
    {
        id: 2,
        text: "Item 2"
    }
]);
</script>
```

### 2.5 补丁标记(Patch Flags)

补丁标记是一种机制，用于识别虚拟DOM更新的类型

- 优化更新过程：通过使用补丁标记，vue3可以在diff过程中快速识别哪些节点发生了变化，并以最小的成本进行更新

- 细粒度更新：补丁标记的引入使得vue3的更新变得更加细粒度，这样在页面更新时可以避免不必要的完整渲染，进一步提升性能

```vue
<template>
    <div class="home">
        <h3>{{ title }}</h3>
        <button @click="changeTitle">Change Title</button>
    </div>
</template>

<script setup lang="ts">
// 当title改变时，补丁标记可以标识出这是一处“文本更新”，而不是解析整个组件，这样可以更高效的进行DOM更新
import { ref } from 'vue';
const title = ref("Home ");
const changeTitle = () => {
    title.value = "Home Page";
};
</script>
```

**虚拟DOM节点更新类型**

1. 创建节点

2. 更新节点

3. 删除节点

4. 移动节点

5. 文本节点更新

## 3. 为什么Vue3去掉了构造函数

### 3.1 简化API设计

### 3.2 提供灵活性

### 3.3 Tree Shaking

### 3.4 小结

## 4. vue3数据响应式的理解

### 4.1 Proxy和Reflect

### 4.2 Reactive和Ref

### 4.3 依赖收集与触发更新

### 4.4 Computed与Watch

### 4.5 响应式系统的优势

## 5. vue3中v-model的变化

### 5.1 更灵活的自定义组件支持

### 5.2 多值绑定

### 5.3 性能优化

### 5.4 移除.sync修饰符

### 5.5 自定义v-model指令

## 6. vue3中异步组件的用法

### 6.1 基本用法

### 6.2 加载状态和错误处理

### 6.3 结合Suspense使用

### 6.4 动态导入

### 6.5 结合路由使用

### 6.6 高级用法：自定义加载逻辑

### 6.7 与Vue2的对比

### 6.8 封装加载异步组件的工具类


## 7. composition API相比Options API的优势


## 8. vue3 setup的作用和原理以及script setup做了什么事

## 9. 介绍pinia以及其持久化最佳实践

## 10. ref和reactive的区别源码级别的比较

## 11. keep-alive的最佳实践

## 12. vuex最佳实践以及持久化方案

## 拷问：既然现在vite的优势那么多，也那么明显，那么vite会取代webpack吗？

