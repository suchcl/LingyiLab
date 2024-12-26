> 本文没有什么章法，就是一些关键信息的集合

### 1. 项目创建

新项目，已经不再使用vue-cli了，而是推荐使用vite当作脚手架工具。

**虚拟DOM**

虚拟DOM，不同的人的认知、理解不同，解说的方式也不同，有的人解说的简单，有的人解说的简单。但本质上，就是用js对象来描述UI的方式，就是所谓的虚拟DOM。

### 2. 基本语法

### 3. setup

setup有两种用法，一种是当作script函数的属性，一种是当作函数使用。

**两种setup的用法有什么区别吗？**



### 4. 生命周期钩子函数

vue3中有很多生命周期的钩子函数，现在Vue3中的钩子函数和React的用法比较类似了，就是用哪个函数，就导入哪个函数，这一点和Vue2的变化比较大。

Vue3中有很多钩子函数，具体如下：

1. beforeCreate:实例初始化之前调用

2. created:实例创建完成之后调用

3. beforeMount:组件挂载到DOM之前调用

4. mounted:组件挂载到DOM之后调用

5. beforeUpdate:数据更新时，具体是数据更新前也就是虚拟DOM打补丁之前

6. updated:数据更新完成之后调用，也就是虚拟DON打完了布丁了，数据已经更新到了虚拟DOM了

7. beforeUnmount:组件卸载之前调用

8. unmounted:组件卸载之后调用

前面说了，钩子函数使用时需要先导入。

```vue
<script lang="ts">
import Layout from '@/components/layout/index.vue';
import { onMounted } from 'vue'; // 导入钩子函数
export default {
  name: 'App',
  components: {
    Layout
  },
  setup() {
    const saveUserName = () => {
      
    };
    
    // 调用钩子函数，在setup函数中
    onMounted(() => {
      saveUserName();
    });

    return {
      
    }
  }
}
</script>
```

### 5. 组件

#### 1. 父子组件引用

父组件中使用子组件的时候，有个细节需要注意：

如果父组件中script标签使用了setup函数，则可以直接导入就可以了

#### 2. 父子组件通信


### 6. slot



### 7. 路由

#### 7.1 路由跳转

两种路由跳转方式：生命式路由跳转和命令式路由跳转

1. 声明式路由跳转

2. 命令式路由跳转

命令式路由跳转，需要从vue-router中导入useRouter钩子函数，然后在setup函数中声明一个useRouter的实例，最终通过这个实例去实现路由跳转

```vue
<template>
    <div class="menu">
        <div class="user-center">
            <!-- 命令式路由跳转 -->
            <div class="uname" @click="goUserList">{{ username }}</div>
        </div>
    </div>
</template>

<script lang="ts">
// 从vue-router导入useRouter
import { useRouter } from 'vue-router';
export default {
    name: 'Header',
    setup() {
        // 声明useRouter的实例
        const router = useRouter();
        const goUserList = () => {
            // 路由跳转
            router.push("/userList");
        };
        return {
            goUserList
        };
    }
}
</script>
```