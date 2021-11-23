### 1. micro-app 应用搭建

> 本案例以 vue3 搭建的应用为基座应用，vue-router 为 4.0.12，使用 history 模式路由

#### 1.1 基座应用：<font color="#f20">这些配置是在基座应用中的操作，本案例是 vue3 搭建，vue-router@4.x版本</font>

1. 安装依赖

```bash
npm install @micro-zoe/micro-app --save
```

2. 在入口处导入依赖

```javascript
// main.js  入口文件，vue中以main.js为入口文件，也可以自定义入口文件，如自定义了index.js，那这里就去index.js中去配置就可以了
import microApp from "@micro-zoe/micro-app";
microApp.start();
```

3. 为子应用分配路由

```javascript
import { createRouter, createWebHistory } from "vue-router";

const VueApp = () => import("../view/Hr.vue");

const routes = [
  {
    path: "/vueapp/:page*", // 非严格匹配，/vueapp/*都将匹配到VueApp中，vue-router3.x中的配置方式为：'/vueapp/*'
    component: VueApp,
    meta: {
      title: "人力系统",
    },
  },
];

const router = createRouter({
  history: createWebHistory(),
  routes,
});

router.beforeEach((to, from, next) => {
  if (to.meta) {
    document.title = to.meta.title;
  }
  next();
});

export default router;
```

4. 在VueApp页面中使用micro-app组件

   ```vue
   <template>
     <div class="micro-app">
       <h2 class="title">{{ msg }}</h2>
       <!--
         micro-app组件中
         name：子应用名称，必传，且要唯一，需要以字母开头，名称中不能带有"."、"#"等特殊符号
         url：必传，子应用的url地址
         baseroute：可选，基座应用分配给子应用的路由前缀，就是route中配置的path字段，本案例中是/vueapp
       -->
       <micro-app
         name="vueapp"
         url="http://localhost:8080/"
         baseroute="/vueapp"
       ></micro-app>
   ```

   
