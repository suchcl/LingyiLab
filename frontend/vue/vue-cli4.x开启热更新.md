### @vue/cli4.x开启热更新

因为热更新，基本一个项目只配置一次就可以了，没有经常关注过。我记得好像是在vue-cli3.x的热更新是自动开启的，也可能不是，我印象不深了，但是现在项目vue2.6.12，@vue/cli是4.5.15，webpack就是@vue/cli内置的，没有更新。每次更新了代码后，都还需要手动刷新页面，否则看不出效果。

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