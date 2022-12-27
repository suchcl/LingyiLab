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