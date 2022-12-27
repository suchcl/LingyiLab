### 怎么在vue中使用less预处理器？

几年以前，记得在vue项目中使用less选择器的时候，需要手动配置一些less-loader或者plugin啥的，具体配置哪个忘记了。但是今天在使用vue-cli构建一个新项目的时候，发现并不需要配置这些loader了，就可以直接使用less预处理器。

> 今天在使用@vue/cli4.5.0创建了个基于vue2的vue项目，直接使用less预处理器，结果在项目编译的时候异常，提示没有找到less-loader.
> 我重新翻看了vue/cli文档，https://cli.vuejs.org/zh/guide/css.html,提示Vue Cli天生支持Sass、Less在内的预处理器。但是实际上并不是，起码在@vue/cli4.5版本中不是，由于提示的是找不到less-loader,我就直接根据提示安装了less-loader，安装后，可以正常使用了。我这是在.vue文件内使用，不是单独的less文件，如果是单独的less文件，可以参考[vue项目中less的配置](./vue项目中less的配置.md).

> 之前vue项目应该是通过vue init webpack 项目名称 的方式创建的，今天是直接使用的vue create项目名称的方式创建的，不确认是否和创建项目的方式有关，不确认是否是不同的创建方式有着不同的webpack配置。

> 上面的问题暂且不论，我项目中已经配置好了，但我对官方文档对vue cli天生支持sass、less等预处理器的描述产生了怀疑，还需要我继续验证。

```json
"dependencies": {
    "core-js": "^3.6.5",
    "vue": "^2.6.11"
  },
  "devDependencies": {
    "@vue/cli-plugin-babel": "~4.5.0",
    "@vue/cli-plugin-eslint": "~4.5.0",
    "@vue/cli-service": "~4.5.0",
    "less": "^4.1.2",
    "less-loader": "^6.0.0",
  },
```

但是这里有个问题需要注意，如果安装less-loader是不加版本号，直接安装最新的版本，可能会有个报错：

```bash
 ERROR  Failed to compile with 1 error                                                                 5:50:14 ├F10: PM┤

 error  in ./src/layout/header.vue?vue&type=style&index=0&lang=less&

Syntax Error: TypeError: this.getOptions is not a function


 @ ./node_modules/vue-style-loader??ref--10-oneOf-1-0!./node_modules/@vue/cli-service/node_modules/css-loader/dist/cjs.js??ref--10-oneOf-1-1!./node_modules/vue-loader/lib/loaders/stylePostLoader.js!./node_modules/postcss-loader/src??ref--10-oneOf-1-2!./node_modules/less-loader/dist/cjs.js??ref--10-oneOf-1-3!./node_modules/cache-loader/dist/cjs.js??ref--0-0!./node_modules/vue-loader/lib??vue-loader-options!./src/layout/header.vue?vue&type=style&index=0&lang=less& 4:14-470 15:3-20:5 16:22-478
 @ ./src/layout/header.vue?vue&type=style&index=0&lang=less&
 @ ./src/layout/header.vue
 @ ./src/router/router.js
 @ ./src/main.js
 @ multi (webpack)-dev-server/client?http://192.168.50.43:8080&sockPath=/sockjs-node (webpack)/hot/dev-server.js ./src/main.js
```

我没有查这个问题的根源是什么，但是一个表象是less-loader的版本太高了，降低下less-loader的版本就可以了。比如我降低到6.2.0是可以的。

### vue3中配置less

首先是npm包的安装

```bash
npm install less@3.10.3 less-loader@6.1.0 style-resources-loader vue-cli-plugin-style-resources-loader --save-dev
```

然后是在vue.config.js中进行配置

```js
const path = require("path");
function resolve(dir) {
    return path.join(__dirname, dir);
}
module.exports = {
    // less配置
    pluginOptions: {
        "style-resources-loader": {
            "preProcessor": "less",
            // patterns: [
            //     resolve("src/assets/less/base.less")
            // ]
            patterns: [""] // 这里的配置有些不合理，还需要去探索
        }
    }
}
```

按照上面的方式已经配置成功，最近更新了下包，基本的方式和上面方式相同，简单贴下过程和代码吧。

1. 安装依赖

```bash
npm install less less-loader style-resources-loader vue-cli-plugin-style-resource-loader --save-dev
```

2. vue.config.js中配置

```js
const { defineConfig } = require('@vue/cli-service')
module.exports = defineConfig({
  transpileDependencies: true,
  pluginOptions: {
    "style-resources-loader": {
      "preProcessor": "less",
      patterns: [""]
    }
  }
})
```

就这2步就可以了，less已经可以在vue中使用了,在style元素上配置下lang属性为less。

```vue
<style lang="less">
.nav {
  list-style: none;
  padding: 0;
  margin-top: 20px;
  font-size: 16px;
  display: flex;
  li {
    margin: 0 10px;
  }
}
</style>
```