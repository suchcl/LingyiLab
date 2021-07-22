### vue-router4.x的404路由配置

在项目中，经常会有一些特殊情况，页面跳转到一个404页面。怎么设置呢？

vue-router基本上已经给我们实现了这个功能，只需要在我们的代码中配置一下就可以了。最近在看vue-router4.x版本的，没有注意vue-router3.x的具体实现，不过大体上应该类似的。看配置代码：

```javascript
{
    path: "/:pathMatch(.*)*",
    name: "NotFound",
    component: NotFound
}
```

我们的项目是history的路由模式时，注意配置下服务器，需要服务器的支持。

<font color="#f00">另外一点需要注意的是,注意包含通配符的路由配置的顺序，放到所有配置路由的最下面，有限保证能够匹配到的路由，最后再匹配没有匹配到的路由，跳转到404</font>，详情可参考:[vue-router4.x中404配置](https://next.router.vuejs.org/zh/guide/essentials/dynamic-matching.html#%E6%8D%95%E8%8E%B7%E6%89%80%E6%9C%89%E8%B7%AF%E7%94%B1%E6%88%96-404-not-found-%E8%B7%AF%E7%94%B1)