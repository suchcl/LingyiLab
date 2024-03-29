### vscode插件开发

#### 开发准备

1. 安装最新版本的vscode

2. 安装LTS版本的nodejs

3. 安装官方推荐的脚手架工具yeoman和Generator-code

4. 安装插件的打包和发布工具vsce

```bash
npm install yo generator-code -g
npm install vsce -g
```

#### nodejs

可以安装一个版本相对较高的版本，如果全局安装了yo和generator-code之后，在通过yo脚手架创建项目的时候提示找不到mem-fs模块，大概如下的信息，则说明nodejs的版本低了，切换到一个高版本的nodejs即可。

```bash
Error [ERR_MODULE_NOT_FOUND]: Cannot find package 'mem-fs' imported from /Users/a58/.nvm/versions/node/v14.16.0/lib/node_modules/yo/node_modules/yeoman-environment/dist/environment-base.js
```

#### 通过yo、generator-code创建项目

![初始化项目](./images/i5.png)

1. 重要文件

项目创建完之后，最重要的文件有2个：package.json和extension.js，了解了这2个文件，基本上就可以入门开发vscode插件了。

**package.json**

package.json是vscode扩展的清单文件，文件中有很多字段，官方文档中都有详细的介绍，主要有几个字段，可以重点介绍。

```json
{
  "name": "eslint-plugin", // 插件名
  "displayName": "eslint-plugin", // 显示在应用市场中的名字
  "description": "我的插件测试",
  "version": "0.0.1", // 插件的版本号
  "engines": {
    "vscode": "^1.84.0" // 最底支持的vscode版本
  },
  "categories": [
    "Other" // 扩展类别
  ],
  // 激活事件组，即都有哪些事件会激活插件
  "activationEvents": [],
  "main": "./extension.js", // 插件的入口文件
  "contributes": {
    // 指令、命令，发布内容配置
    "commands": [{
      "command": "eslint-plugin.helloWorld", // 
      "title": "Hello World"
    }]
  },
  "scripts": {
    "lint": "eslint .",
    "pretest": "npm run lint",
    "test": "node ./test/runTest.js"
  },
  "devDependencies": {
    "@types/vscode": "^1.84.0",
    "@types/mocha": "^10.0.3",
    "@types/node": "18.x",
    "eslint": "^8.52.0",
    "glob": "^10.3.10",
    "mocha": "^10.2.0",
    "typescript": "^5.2.2",
    "@vscode/test-electron": "^2.3.6"
  }
}
```

在这份package.json文件中，最重要的属性有3个：activationEvents、main和contributes。

main：指定插件的入口文件。

activationEvents：指定插件的激活场景。

contributes：通过扩展注册contributes来扩展vscode中的各项功能，有很多个配置项，具体可参考：https://code.visualstudio.com/api/references/contribution-points

文档中都给出了详细的介绍。

**extension.js**

该文件是插件的入口文件，即package.json中main字段对应的文件。该文件主要导出2个方法：activate和deactivate，两个方法分别有自己的执行世时机。

1. activate:插件被激活时执行

2. deactivate:插件被销毁时执行，如可以释放内存等。

### 发布插件

有3种发布、推广vscode插件的方法

1. 直接将源码分享出去，直接运行源文件进行使用

一般只有在开发、调试阶段会使用该方式，不建议使用

2. 打包成vsix插件，然后发送给被人安装使用

一般情况下，团队内部使用或者涉密的插件，可使用这种方式

3. 发布到应用市场：大多数插件推荐使用这种方式

发布到应用市场，插件包不需要被审核，但是插件名不能和已有的插件重名，保持插件名唯一

**打包vsix插件**

1. 安装vsce

如果没有安装过则进行安装，如果已经安装过了，则不需要重复安装

```bash
npm install vsce -g
```

2. 使用vsce进行打包

```bash
vsce package
```

3. 安装到vscode

**发布应用市场**

参考https://cloud.tencent.com/developer/article/2200774最下面的“发布到应用市场”部分 