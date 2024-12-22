vue3提供了强大的工具指令来操作DOM，常用的如v-bind、v-model、v-if、v-for、v-on等，使开发者能够轻松的创建交互式和响应式应用。

### 内置指令

1. v-bind：简写:，用于动态绑定属性，如src、alt、class等。

```vue
<template>
    <div>
        <h3>list 列表页面</h3>
        <img class="pic" :src="imgSrc" :alt="imgAlt">
    </div>
</template>

<script lang="ts">
    import { ref } from 'vue';
    export default{
        setup(){
            const imgSrc=ref("/images/i1.png");
            const imgAlt = ref("我的自定义alt");
            return {
                imgSrc,
                imgAlt
            };
        }
    }
</script>
```

2. v-model: 数据双向绑定

v-model使得表单输入和响应式属性之间的双向绑定成为可能，非常适合表单的数据输入场景。

```vue
<form @submit.prevent="handleSubmit">
    <ul class="ul-list">
        <li>
            <label for="username">姓名:</label>
            <input type="text" id="username" v-model="username">
        </li>
        <li>
            <label for="age">年龄:</label>
            <input type="text" id="age" v-model="age">
        </li>
    </ul>
    <button type="submit">提交</button>
</form>
<ul class="user-info">
    <li>姓名: {{ username }}</li>
    <li>年龄: {{ age }}</li>
</ul>

<script lang="ts">
    import { ref } from 'vue';
    export default{
        setup(){
            const username = ref("");
            const age = ref("");
            
            const handleSubmit = () => {
                const user = {
                    username: username.value,
                    age: age.value
                };
                console.log('%c [ user ]-36', 'font-size:13px; background:pink; color:#bf2c9f;', user);
            }
            return {
                username,
                age,
                handleSubmit
            };
        }
    }
</script>
```

3. v-if、v-else-if、v-else:条件渲染

除了v-if之外，还有另外一个指令v-show也是用来做条件渲染的判断的。

v-if: 条件为真，则渲染，否则DOM元素不渲染

v-show：也会根据条进行判断，只不过false的时候，DOM元素也会渲染，只不过是给元素加了个diaplay:none;的样式，用视觉的方式欺骗了我们。

> 如果没有特殊的要求，在做条件渲染的时候使用v-if，因为不渲染这部分不必要的DOM，可以减小页面的质量，提升加载速度，在性能上有一定的提升；

```vue
<div class="login" v-if="isLogined">登录</div>
<div class="login" v-show="isLogined">登录v-show</div>
<button @click="login">去登录</button>
<script lang="ts">
    import { ref } from 'vue';
    export default{
        setup(){
            let isLogined = ref(false);
            
            const login = () => {
                isLogined.value = !isLogined.value;
            };
            return {
                isLogined,
                login
            };
        }
    }
</script>
```

4. v-for遍历

v-for遍历数据列表

```vue
<ul class="list">
    <li v-for="item in data" key="{item.id}" class="item">
        <div class="name">{{ item.name }}</div>
        <div class="age">{{ item.age }}</div>
    </li>
</ul>
<script lang="ts">
import { ref } from 'vue';
import { data } from './testData';
export default {
    setup() {     
        return {
            data
        };
    }
}
</script>
```

5. v-on事件处理

v-on，简写为@

```vue
<!-- button绑定click事件 -->
<button @click="login">去登录</button>
<!-- or -->
<button v-on:click="login">去登录</button>
<script lang="ts">
    import { ref } from 'vue';
    export default{
        setup(){
            let isLogined = ref(false);
            const login = () => {
                isLogined.value = !isLogined.value;
            };
            return {
                isLogined,
                login
            };
        }
    }
</script>
```