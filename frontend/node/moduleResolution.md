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

- classic:Typescript最经典、最古老的模块解析策略.当module设置为node16、nodenext或commonjs以外选项的默认策略.在新的项目中尽量不要使用这种解析策略,Typescript团队计划在Typescript6.0中弃用这个选项.

- node10(node):以前称为node,当module设置为commonjs时的默认值.该模块解析策略支持从node_modules中查找包、加载目录的index.js文件以及在相关模块说明符中省略.js扩展名.由于Node V12为ES模块引入了不同的模块解析规则,易经不建议在新项目中使用这个解析策略了.

- node16:nodejs v12起同时支持CJS和ESM,每种模块解析策略都使用自己的模块解析策略.nodejs中,import调用模块不允许省略文件扩展名,require导入模块方式允许省略文件扩展名

- nodenext:当前与node16相同,它旨在成为一种前瞻性模式,支持新添加的nodejs模块解析功能.

- bundler:nodejs v12引入了一些用于导入npm包的新模块解析功能(package.json的"exports"和"imports"字段),许多打包构建工具采用了这些功能,但是没有采用严格的ESM导入规则,这种模块解析策略为针对打包工具的代码提供了基本的算法支持.

[tsconfig的moduleResolution支持的选项值](./images/i20.png)

classic和node10(node)是ts就支持的解析策略,但是它们不支持exports,后来新增的node16、nodenext和bundler都支持.

### 小结

模块解析策略随着exports的出现有了统一并且能够满足各种场景需求的标准,估计再过一段时间发布npm包的时候main字段也可以省略掉了.

- exports是一个强大并且被各种前端工具广泛支持的模块解析标准,我们发布npm包时,应该使用exports来管理它的解析规则;

- exports的解析规则较为复杂,社区的很多第三方的实现或多或少都有些bug,尤其是和优先级相关的;

- 对于很多不想写扩展名的typescript项目来说,应该使用bundler解析策略,这样第三方库就可以只写exports而不需要写typeVersions了;

- typescript的很多设计都是对现实妥协的产物,粗了bundler解析策略,还有装饰器,早期的装饰器并没有达到ECMAScript stage3标准,TS自己实现了一套.换句话说,就是Ts在开发效率和ECMAScript标准之间选择了开发效率;