### react项目中接入react-router

react-router官网：[https://reactrouter.com/](https://reactrouter.com/)

react-router有多种实现，可以在web中，也就是常见的单页面(SPA)中使用，也可以在React Native应用中使用。针对Web中的实现，可以导入react-router-dom,如果希望既可以在web应用中使用过，也可以在react native应用中使用，那么可以直接导入react-router。

### react项目中导入react-router

大多数情况下，是不会在c端的react应用中导入react-router的,因为大部分的C端项目，都是有seo需求的，需要做服务端渲染，做服务端渲染的时候，直接使用react可能不是一个最优的选择。所以在C端项目中，如果使用了react技术栈，我倾向于直接使用next.js,如果使用vue技术栈，则nuxt.js是一个不错的选择；最次的，我搭建一个node的express项目，然后使用react或者vue搭建页面，然后将react或者vue页面编译为html后作为express的模板去使用，这个时候，就已经不需要处理前端路由了，而是使用的node路由。

当然了，这只是一些技术方案的可选择项，有些技术团队可能处于某些原因考虑，也会在C端项目中选择React以及服务端渲染的API去做一些实现，或者使用Vue以及vue的服务端渲染的api去做实现，在技术上可以实现，可以走通，但个人的一些理解，已经开源的、经过社会验证的框架可能效率上以及代码的健壮性上更具有优势。

如果是后端项目，react技术栈的话，个人认为umi是一个很优秀的技术解决方案，该框架以路由为基础、然后配以生命周期完善的插件体系，覆盖从源码到构件产物的每个生命周期，支持各种功能扩展和业务需求。如果是vue技术栈的话，其本身就是一个框架，相对于react来说，我个人觉着在技术选型上要简单一点。因为vue本身包含了丰富的生态系统，vite作为构建工具，本身也提供了丰富的能力，另外有直接vue官方团队维护的pinia状态管理库和路由管理工具vue-router，vue生态本身的这些能力都让vue自己就是一个技术方向的选择。

**回到React项目中，React项目中怎么接入react-router呢？**

首先需要纠正一个误区，尤其是以前接触过vue的同学。如果以前接触过了vue，那么应该都知道vue-router是vue的路由管理库，它只能用在vue中，不能用在react中，也不能用在angular中。但是react-router不同，react-router的定位是前端路由，它不仅可以用在react中，也可以用在vue中，只不过对于react的支持友好程度高一点罢了，再就是vue有了自己的路由管理库vue-router,在vue的项目中，基本不会使用react-router这么一个非官方的外来库。所以很多人就会直接以为react-router就是react的官方路由管理库，其实不是的。react本身就是第一个UI库，然后就没有别的了。其他的如cli工具、路由管理库react-router、状态管理库redux等，都是社区贡献的优秀生态圈。

**React项目中接入react-router**

1. 安装react-router-dom

我们以web应用为例，做web项目，只需要安装web的依赖就可以了。

```bash
pnpm install react-router-dom # 不能添加-D参数，生产环境也需要路由跳转
```

2. 

**创建类似umi中layout的布局文件**