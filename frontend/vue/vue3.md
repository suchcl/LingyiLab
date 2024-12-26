### 项目创建

新项目，已经不再使用vue-cli了，而是推荐使用vite当作脚手架工具。

**虚拟DOM**

虚拟DOM，不同的人的认知、理解不同，解说的方式也不同，有的人解说的简单，有的人解说的简单。但本质上，就是用js对象来描述UI的方式，就是所谓的虚拟DOM。

### 基本语法

### setup

setup有两种用法，一种是当作script函数的属性，一种是当作函数使用。

**两种setup的用法有什么区别吗？**



### 生命周期钩子函数

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

### 组件

#### 1. 父子组件引用

#### 2. 父子组件通信


### slot

