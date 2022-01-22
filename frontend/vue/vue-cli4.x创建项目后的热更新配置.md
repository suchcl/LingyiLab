在通过较新版本的@vue/cli工具创建vue项目时，默认可以选择vue2版本和vue3版本的，由于是为了做一些功能上的测试，我选择的vue2版本创建的项目。

项目创建完成之后，发现一个现象，就是代码响应速度特别慢，而且没有热更新。无论是修改了vue模板，还是修改了样式、js脚本，页面不会自动刷新做效果更新，在手动刷新后，页面刷新也是慢的不行，大概需要10s以上的时间。正常的情况下，是不能这么慢的速度的。

那就先解决热更新的问题吧。从网上查了一下，说是webapck4.0默认没有开启热更新，需要手动配置热更新。

> 关于网上查到的资料，说webpack4.0默认没有开启热更新，我是持怀疑态度的，因为同样的创建项目的方法，我只是选择vue3版本创建项目，那么这个vue3版本的项目是支持热更新的。通过vue create方式创建的vue项目，只是vue的版本不同，但是vue3版本项目是默认支持热更新的。

配置方法，安装一个开发时服务器webpack-dev-server，然后配置下支持热更新即可，最后也需要在package.json的scripts部分添加下webpack-dev-server配置。


安装webpack-dev-server

```bash
npm install webpack-dev-server --save
```

webpack配置

```js
// vue.config.js
module.exports = {
    devServer: {
        // open: true,
        // hot: true,
        // compress: true,
        // webpack4.x开启热更新
        disableHostCheck: true
    }
};
```

package.json启动脚本配置webpack-dev-server

```json
// package.json
"scripts": {
    "serve": "vue-cli-service serve && webpack-dev-server --open", // webpack-dev-server配置，支持热更新
    "dev": "npm run serve",
    "build": "vue-cli-service build",
    "lint": "vue-cli-service lint"
},
```

到此为止，vue2版本的项目已支持热更新了，不仅如此，更新的速度还非常的快，无论是css、js或者vue文件修改了，只要一保存，基本就是瞬间更新。

> 在vue@2.6.14、@vue/cli@4.5.15版本下是不生效的，

> 在vue@3.2.28、@vue/cli-service@4.5.15的版本下自动就有了热更新