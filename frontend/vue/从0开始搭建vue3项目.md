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
````

这样可以减少一些标签层级，降低内存的占用