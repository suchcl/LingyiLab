### react项目中接入react-router

react-router官网：[https://reactrouter.com/](https://reactrouter.com/)

react-router有多种实现，可以在web中，也就是常见的单页面(SPA)中使用，也可以在React Native应用中使用。针对Web中的实现，可以导入react-router-dom,如果希望既可以在web应用中使用过，也可以在react native应用中使用，那么可以直接导入react-router。

### react项目中导入react-router

大多数情况下，是不会在c端的react应用中导入react-router的,因为大部分的C端项目，都是有seo需求的，需要做服务端渲染，做服务端渲染的时候，直接使用react可能不是一个最优的选择。所以在C端项目中，如果使用了react技术栈，我倾向于直接使用next.js,如果使用vue技术栈，则nuxt.js是一个不错的选择；最次的，我搭建一个node的express项目，然后使用react或者vue搭建页面，然后将react或者vue页面编译为html后作为express的模板去使用，这个时候，就已经不需要处理前端路由了，而是使用的node路由。

当然了，这只是一些技术方案的可选择项，有些技术团队可能处于某些原因考虑，也会在C端项目中选择React以及服务端渲染的API去做一些实现，或者使用Vue以及vue的服务端渲染的api去做实现，在技术上可以实现，可以走通，但个人的一些理解，已经开源的、经过社会验证的框架可能效率上以及代码的健壮性上更具有优势。

如果是后端项目，react技术栈的话，个人认为umi是一个很优秀的技术解决方案，该框架以路由为基础。

