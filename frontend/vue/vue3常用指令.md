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

