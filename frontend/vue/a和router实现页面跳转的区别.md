### vue项目中通过a和router实现页面跳转的区别

一般情况下，在HTML中，我们在实现页面跳转的时候都会通过a去实现，也可以通过js点击事件去实现不同页面之间的跳转。我们现在已经都转入到Vue或者React开发了，很少再使用套页面的方式去做项目了，那么我们在Vue项目中实现页面跳转的时候，我们都会通过router去跳转，而不会使用a标签去跳转，虽然标签a也可以实现同样的功能，那么在实现页面跳转的时候，a和router有什么区别呢？

直观的从现象来看，就是通过a实现页面跳转的时候，通过url的更改，整个页面都会刷新，而通过router方式的跳转，页面不会整体刷新，只是页面的局部刷新，但是也同样实现URL的变更，以及处理URL中携带的参数，或者URL变更过程中携带的各种参数的处理。


### Router4.x项目中，怎么设置路由模式？

vue-router4.x中设置路由模式和3.x有变化。在vue-router3.x中设置路由模式，是在创建路由时，为mode参数设置值，值为hash或者history，如

```javascript
const router = new VueRouter({
  mode: 'history',
  routes: [...]
})
```

而到了vue-router4.x时，路由的创建不再是通过new来实例化rouer对象了，而是通过createRouter方法来创建router的实例，再就是在创建router实例时，和vue-router3.x一样也还是有2种路由模式hash和history。只不过在4.x中，hash模式的路由模式，是通过createWebHashHistory()来创建的，H5的history模式是通过createWebHistory()来创建的。在创建路由的实例时，我们只需要对history来赋值就可以了，注意这个值是必选项，必须要赋值，否则会报错。

```javascript
const router = createRouter({
    history: createWebHistory(),
    routes
});
```