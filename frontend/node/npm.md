## 认识npm

[中文参考文档](https://www.npmjs.cn/)或者[英文参考文档](https://docs.npmjs.com/)

npm可以理解为现在前端技术栈最必要、最不可或缺的一项工具，它是世界上最大的软件注册表，每周大概有30亿次的下载量，包含超过600000个包,也就是package或代码块。来自世界的各地的开源软件开发者使用npm互相分享和借鉴。

### npm的组成

npm主要有3部分组成：
1. [网站](https://www.npmjs.com/)：网站时开发者查考包(package)、设置参数以及管理npm使用体验的主要途径

2. 注册表(registry)：注册表是一个巨大的数据库，保存了每个包(package)的信息

3. 命令行工具(cli)：命令行工具，是开发者与npm打交道的主要工具

## 常用命令

```bash
npm install package # 安装本地包(执行该命令后，会将包安装当前目录下的node_modules目录下，如果没有node_modules目录，则会新建)
npm install package -g # 全局安装，对本地所有项目都可用的包

npm install # 主要用来安装包，等价于 npm i，install可以简写为i

# npm通过--registry参数指定安装源
npm install cnpm --registry=https://registry.npm.taobao.org -g
```

### npm在安装包的过程总，--save、-S、--save-d、-D的区别

```bash
npm install --save-dev # 安装开发时依赖，等价于 npm install -D

npm install --save # 安装运行时依赖,等价于 npm instal -S
```

## 安装后的包的使用

当我们安装后需要的包以后，就需要使用它了。包在被正常的安装后，会被安装到当前项目中的node_modules目录下，当安装后，可以通过require来引入使用了。

比如我们安装了一个lodash包，新建换一个index.js文件，其代码如下：

```javascript
var lodash = require("lodash");
var output = lodash.without([1,2,3],1);
```

当我们运行node index.js指令输出[2,3]时说明lodash安装正常并被正确的引入和使用了，但是如果抛出了异常“Cannot find module ‘lodash’”则说明lodash没有被正常的引用，或者包的安装出了问题。

## 怎么使用npm查看包(package)版本

可以通过npm来查询通过npm来安装的包的版本信息，包括本地的全局安装的版本信息以及当前目录项目的版本目录

1. 查看本地安装包(package)的版本

```bash
npm ls package  查看当前目录（项目）下安装的包的版本

npm ls package -g 查看本地机器全局安装的包的版本
```

2. 查看远程服务器上包的版本

```bash
npm view package version 查看包的最新的版本

npm view package versions 查看包的所有的版本列表
```

3. npm缓存



## npm install和npm ci的区别

1. npm install依赖package.json，npm ci依赖package-lock.json
2. 当package-lock.json中的依赖与package.json不一致时，npm ci会退出但不会修改package-lock.json
3. npm ci只可以一次性的安装整个项目依赖，但无法单独添加某个依赖项
4. npm ci安装之前，会删除掉node_modules目录，不需要检查、校验已下载文件版本和控制版本的关系，也不用校验是否存在最新的版本库，下载速度更快
5. npm安装时，不会修改package.json和package-lock.json
