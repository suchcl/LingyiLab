参考文档:https://zhuanlan.zhihu.com/p/621795173

### moduleResolution 模块化解析策略

当谈到模块化解析策略的时候,首先要了解在前端领域的模块化规范或者叫模块化标准,当我们了解了前端领域的模块化标准以后,才能更好的去了解、研究去解析它、应用它.

有关前端的模块化规范,可参考:[前端模块化规范](./module模块化标准.md)

一般情况下,研究模块解析策略就是研究一个模块的路径即相对路径和绝对路径(也叫非相对路径,就是第三方库,也可以说是npm包)是按照怎么样的规则去查找的.相对路径相对来说简单一些,非相对路径相对来说复杂一些.

我注意到模块解析策略是在使用了ts的开发项目的时候,在tsconfig.json中有一个moduleResolution的配置选项,后来查询了一下该选项:最初的时候该属性支持2个值:classic和node,node策略是在typescript中又被称之为node10解析策略.

### moduleResolution:node

这个模块解析策略就是nodejs的模块解析策略,也就是require.resolve的实现.

```js
const lodash = require.resolve("lodash")
console.log('%c [ lodash ]-2', 'font-size:13px; background:pink; color:#bf2c9f;', lodash)
// /xxxx/module/node_modules/lodash/lodash.js
```

这种模块解析策略也是很多前端构建工具如webpac、vite所采用的模块解析策略.vite虽然使用了node的模块解析策略,但是它的实现并不完全和nodejs一致,它扩展了nodejs的模块策略解析.

> rollup没有内置模块解析策略,rollup默认所有的npm包都是external的,即都是外部的,需要使用node模块解析策略的插件@rollup/plugin-node-resolve来实现模块的解析.

**前端构建工具的模块解析策略**

虽然很多前端的共建工具都使用了nodejs的模块解析策略,但是在具体实现上又都是有所差异:

- vite使用的第三方库[resolve.exports](https://github.com/lukeed/resolve.exports)

- rollup在[@rollup/plugin-node-resolve](https://github.com/rollup/plugins/tree/master/packages/node-resolve)自己实现的

- webpack用的[enhanced-resolve](https://www.npmjs.com/package/enhanced-resolve)

- [resolve](https://www.npmjs.com/package/resolve)好像下载量最高,不过有个问题是不支持package.json的exports

- rspack用的rust模块[nodejs_resolve](https://github.com/web-infra-dev/nodejs_resolver)

### ts中的moduleResolution

Typescript5.3已经发布,tscofnig的moduleResolution选项支持5个值:

> 具体可参考:https://www.typescriptlang.org/docs/handbook/modules/theory.html#module-resolution

- classic

- node10(node)

- node16

- nodenext

- bundler

[tsconfig的moduleResolution支持的选项值](./images/i20.png)