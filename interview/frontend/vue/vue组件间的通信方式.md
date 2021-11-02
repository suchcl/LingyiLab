### 1. 组件间的通信

组件间的通信，有2个核心要素：

1. 组件

2. 通信

通信，简单理解，就是不同组件之间的数据传递、消息推送。

### 2.通信的场景

组件之间的通信，可以分为以下几种场景：

1. 父子组件之间的通信；

2. 兄弟组件之间的通信；

3. 祖孙组件之间的通信：指组件与后代组件之间的通信

4. 非关系组件之间的通信；

借用网上的一张图片，可以直观的表现出组件之间的关系：

![vue组件之间的关系](../images/i6.png)

### 3. 组件之间的通信方案

1. props

2. 通过$emit触发自定义事件

3. 使用ref

4. EventBus

5. $parent和$root

6. attrs和listeners

7. Provide和Inject

8. Vuex

#### 3.1 props

**使用场景**

主要用在父子组件之间通信的场景。

**使用方式**

子组件设置props属性，定义接收父组件传递过来的参数

父组件通过子组件中定义的属性字面量进行传值

```javascript
// router/index.js
    {
        path: "/compo",
        component:Cmp,
        children:[
            {
                path: "cpcmp",
                component: Pcmp,
                meta: {
                    title: "父组件"
                }
            }
        ]
    }
```

```vue
// 父组件 Parent.vue
<template>
    <div>
        <b>{{ msg }}</b>
        <child :username="username" :age="age" :height="height" />
    </div>
</template>

// 子组件 Child.vue
<template>
    <div>
        <b>{{ msg }}</b>
        <p>{{ username }}</p>
        <p>{{ age }}</p>
        <p>{{ height }}</p>
    </div>
</template>

<script>
export default {
    data() {
        return {
            msg: "子组件"
        }
    },
    props: {
        username: {
            type: String,
            default: "Nicholas Zakas"
        },
        age: Number,
        height: {
            type: Number,
            default: 1.98
        }
    }
}
</script>
```

子组件Child.vue中定义了props，接收从父组件中传递的值

父组件通过子组件中定义的props字面量进行传值

props，是vue中最常用的父子组件传值(通信)方式

#### 3.2 通过$emit触发自定义事件



#### 3.3 使用ref

#### 3.4 EventBus

#### 3.5 $parent和$root

#### 3.6 attrs和listeners

#### 3.7 Provide和Inject

#### 3.8 Vuex
