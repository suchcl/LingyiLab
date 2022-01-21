### vue中less配置

@vue/cli文档中介绍，@vue/cli天生支持less、sass预处理器，今天为了测试一个功能，本地随手初始化了一个项目，结果在模板中写less的时候，提示找不到less-loader。

看到这个提示又从@vue/cli的文档上翻了一遍，确实说的是vue/cli原生支持less预处理器，我先检查下我本地环境：

```bash
@vue/cli 4.5.15
vue 2.6.11
```

项目的初始化方式为：

```bash
vue create vuedemo
```

现在同时支持vue2和vue3版本的项目创建，我选择的vue2。

### 解决问题

既然提示了找不到less-loader，那就直接安装吧，因为less编译为css，是在开发环境，所以安装开发时依赖即可。

```bash
npm install less-loader --save-dev
```

安装完成之后，重启服务：

```bash
npm run serve
```

支持了，效果完美，无论是模板内写的less，还是单独的less文件，效果都没有问题。

参考链接：https://cli.vuejs.org/zh/guide/css.html

> 出现问题后，也在网上查了一些资料，说是需要安装style-resources-loader vue-cli-plugin-style-resources-loader以及less、less-loader，然后在vue.config.js中一点简单的配置

```js
// vue.config.js
const path = require("path");
function resolve(dir) {
    return path.join(__dirname, dir);
}
module.exports = {
    // less配置
    pluginOptions: {
        "style-resources-loader": {
            "preProcessor": "less",
            patterns: [
                resolve("src/assets/less/base.less")
            ]
        }
    }
}
```

但是我测试的是使用这种方式没有效果，没有生效，如果有大家遇到同样问题了，就根据自己的实际情况选择吧。