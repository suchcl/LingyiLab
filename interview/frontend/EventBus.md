### EventBus

EventBus，Vue中又称为事件总线。

Vue中主要用来作为不同组件之间通信的桥梁，所有的组件有一个共同的事件中心，可以向该中心注册发送事件或者接收事件，事件的发送和接收，可以发生在不同的组件之间，组件之间可以是兄弟关系、父子关系，也可以是跨级关系，也可以是两个不同的页面。



> 在同一个页面中的兄弟组件之间传递数据，很方便、很好用。
>
> 但是如果是不同页面之间的数据传递，个人感觉体感不是很好，不如使用vuex方便、简单。

因为EventBus的使用过程是需要先注册事件，先绑定一个事件，然后才能去监听某个事件的触发，所以说如果是不同页面之间的通信，是一个回调，效果直观。

下面主要看下同一个页面中的兄弟节点之间的通信案例：

```vue
<!--组件A   组件A中提交事件-->
<template>
    <div class="wa">
        <h5>A页面</h5>
        <button @click="sendMsg">发送消息</button>
    </div>
</template>

<script>
export default {
    data() {
        return {}
    },
    methods: {
        sendMsg() {
            this.$EventBus.$emit("aMsg", "来自a页面的消息");
        }
    }
}
</script>

<!--组件B  组件B监听组件A中的事件-->
<template>
    <div class="wb">
        <h5>B页面</h5>
        <p>接收到的消息：{{ msg }}</p>
    </div>
</template>

<script>
export default {
    data() {
        return {
            msg: ""
        }
    },
    mounted() {
        this.$EventBus.$on("aMsg", (data) => {
            this.msg = `我是通过EventBus传递过来的信息：${data}`;
            console.log(data);
        });
    }
}
</script>

<!--组件A和组件B的父组件：组件C-->
<template>
    <div class="wc">
        <h5>C页面</h5>
        <Ca />
        <Cb />
    </div>
</template>

<script>
import Ca from "./A.vue";
import Cb from "./B.vue";
export default {
    data() {
        return {}
    },
    components: {
        Ca, Cb
    }
}
</script>
```

前面说到了跨页面之间使用EventBus不是很友好，主要是因为页面刷新了之后，与之关联的EventBus会被移除掉，这样就会导致正常的业务流程走不下去；再就是如果有某些业务有反复的操作，那么EventBus在监听的时候就会触发多次，这也是一个潜在的隐患。

所以在跨页面之间的数据通信时，尽量不要使用EventBus；同一个页面之间的兄弟组件之间，谨慎使用。

**EventBus的使用流程**

这是个重点，一定要留意：

创建EventBus：可以是单独创建一个event-bus.js文件，建立EventBus，也可以直接在Vue的原型上建立

引入EventBus：如果是在Vue原型上创建的EventBus，则不需要引入了，可以直接使用

监听(注册)事件

提交事件

销毁事件



这几个步骤不可以反着来，而且为了安全，最后的销毁步骤，一定要做。一般是在组件销毁的时候去销毁EventBus监听的事件。

```javascript
beforeDestroy() {
    this.$EventBus.$off("aMsg");
}
```

解除对监听事件的监听。