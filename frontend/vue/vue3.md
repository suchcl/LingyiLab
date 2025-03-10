<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. 项目创建](#1-%E9%A1%B9%E7%9B%AE%E5%88%9B%E5%BB%BA)
- [2. 基本语法](#2-%E5%9F%BA%E6%9C%AC%E8%AF%AD%E6%B3%95)
- [3. setup](#3-setup)
- [4. 生命周期钩子函数](#4-%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E9%92%A9%E5%AD%90%E5%87%BD%E6%95%B0)
- [5. 组件](#5-%E7%BB%84%E4%BB%B6)
  - [1. 父子组件引用](#1-%E7%88%B6%E5%AD%90%E7%BB%84%E4%BB%B6%E5%BC%95%E7%94%A8)
  - [2. 父子组件通信](#2-%E7%88%B6%E5%AD%90%E7%BB%84%E4%BB%B6%E9%80%9A%E4%BF%A1)
- [6. slot](#6-slot)
- [7. 路由](#7-%E8%B7%AF%E7%94%B1)
  - [7.1 路由跳转](#71-%E8%B7%AF%E7%94%B1%E8%B7%B3%E8%BD%AC)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

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

1. props

```vue
<!-- 父组件 -->
<template>
    <div>
        <UserItem v-for="item in userList" :item="item" :key="item.id"></UserItem>
    </div>
</template>

<script lang="ts">
import { ref,onBeforeMount } from "vue";
import UserItem from "./components/userItem.vue";
import request from "@/service/request";
export default {
    name: "UserList",
    components:{
        UserItem
    },
    setup() {
        const userList:any = ref([]);
        const getUserList = () => {
            request.get("/uesrs/getTestUserList").then((res) => {
                const data = res.data.data;
                userList.value = data.userList;
            });
        }
        onBeforeMount(() => {
            getUserList()
        });
        return {
            userList
        }
    }
}
</script>

<!-- 子组件UserItem.vue -->
<template>
    <div class="user-item">
        <div class="pic">
            <img :src="item.imgUrl" :alt="item.name">
        </div>
        <div class="user-info">
            <div class="name">姓名:{{ item.name }}</div>
            <div class="birthday">生日: {{ item.birthday }}</div>
            <div class="mobile">电话:{{ item.mobile }}</div>
            <div class="email">邮箱:{{ item.email }}</div>
            <div class="address">住址:{{ item.address }}</div>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';

export default defineComponent({
    name: 'UserItem',
    props: {
        // 声明props，类型约束
        item: {
            type: Object as PropType<{ id: number, name: string, birthday: string, mobile: string, email: string, address: string, imgUrl: string }>, // 根据实际的 item 结构定义类型
            required: true
        }
    },
    setup() {
        return {
            message: "用户信息"
        }
    }
});
</script>
```

子组件接收props的时候，需要声明props，并进行类型约束

```vue
<script lang="ts">
import { defineComponent, PropType } from 'vue';

export default defineComponent({
    name: 'UserItem',
    props: {
        // 声明props，类型约束
        item: {
            type: Object as PropType<{ id: number, name: string, birthday: string, mobile: string, email: string, address: string, imgUrl: string }>, // 根据实际的 item 结构定义类型
            required: true
        }
    },
    setup() {
        return {
            message: "用户信息"
        }
    }
});
</script>
```

### 6. slot



### 7. 路由

路由模式：vue3中有3中路由模式：createMemoryHistory、createWebHistory、createWebHashHistory。

hash模式，就是路由中会有#，不太美观。

createWebHistory：vue2中就直接叫history模式，路由中不会有#，美观，但是在部署服务的时候，需要web服务器做一些支持，做一个反向代理。

```bash
server {
	location / {
		 try_files $uri $uri/ /index.html;
	}
    listen        80;
    server_name dev.mainapp.com;

    root /Users/xxx/Documents/workspace/project/xxxxx/dist;
    index index.html index.php index.htm;

    charset utf-8;
    client_max_body_size 100M;
}
```

createWebHashHistory:这种路由模式，本质上是history模式，但是和webhistory模式区别是路由上不会有任何变化，应该是内存中保存的吧，没有用过，暂时不说那么多。

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