### Vue3也上线了一段时间了,但是还是有一些问题

1. watch监听由reactive定义的响应式数据,不能正确获取oldValue,这是由于reactive实现的问题,暂时还没有从框架的层面去解决这个问题,也没有很好的解决方案

在做项目的时候,实际使用到oldValue这个值的情况,也不是很多,如果必须要使用oldValue的时候,可以把需要监听的值从对象中提取出去,使用ref定义,就可以规避watch监听不到oldValue的问题了

```js
watch(person,(newValue,oldValue) => {
    console.log(`watch监听的响应式数据变了: `,newValue,oldValue);
});
```

2. Vue3.0中,watch默认开启了deep监听,也可以理解为强者开启了deep监听吧,且不可关闭,也就是说通过deep:false的配置不会生效.

深度监听,会有性能上的问题.

```js
let person = reactive({
    name: "Nicholas Zakas",
    age: 18,
    job: {
        j1: {
            salary: 20    
        }
    }
});

watch(person,(newValue,oldValue) => {
    console.log(`watch监听的响应式数据变了: `,newValue,oldValue);
},{
    deep: false
});
```

3. Vue3.0深度监听对象上的某一个具体的属性

watch默认只能监听数组、ref和reactive定义的响应式数据,那么需要监听一个由reactive定义的响应式数据的属性时,可以通过函数的方式

```js
// 情况4:监听reactive定义的响应式对象中的某个具体的属性
// 通过函数返回值的方式使用,watch正常情况下只能监听数组、ref和reactive定义的响应式数据
// 比如需要监听年龄的变化
watch(() => { return person.age },(newValue,oldValue) => {
    console.log(`年龄变了: `,newValue,oldValue);
});
```

4. Vue3.0监听对象中某些属性的变化

```js
// 情况5: 监听对象中的某些属性的变化
watch([() => person.name,() => person.age], (newValue,oldValue) => {
    console.log(`对象中的姓名或者年龄变了:`, newValue,oldValue);
})
```

5. 特殊情况下的监听:监听由reactive定义的响应式数据的某个具体的对象属性,

```js
// 特殊情况:监听reactive定义的响应式数据中的对象属性,deep配置生效
watch(() => person.job,(newValue,oldValue) => {
    console.log("涨薪了:",newValue,oldValue);
},{
    deep: true
});
```