taro 开发入门，可以从 4 个方面去着手，分别为：环境准备、基础教程、项目实践、多端开发

### 1. 环境准备

现在 taro 仅提供了一种开发方式：安装 taro 命令行工具 --- Taro Cli 进行开发。

**Taro 命令行工具安装**

taro 开发环境依赖 nodejs，在 taro 开发之前，先在机器上安装 nodejs，建议使用 LTS 版本的 node.js，现在最新的稳定版为 V16.13.1。关于 nodejs 的安装，可以参考：[node.js 环境搭建](../node/nodejs环境搭建.md)

当 node.js 环境准备好之后，就可以安装 Taro 的命令行工具了

```bash
npm install @tarojs/cli -g
```

命令行工具安装完成后，可以通过执行 taro 指令检测命令行工具是否安装成功

```bash
xxx@xxx taroPro % taro
👽 Taro v3.3.19
```

如果出现了上述代码的效果，则表示 taro 的命令行工具安装成功。

可以通过-h 参数查看 taro 命令行工具提供的一些常用指令

```bash
xxx@xxx taroPro % taro -h
👽 Taro v3.3.19

Usage: taro <command> [options]

Options:
  -v, --version       output the version number
  -h, --help          output usage information

Commands:
  init [projectName]  Init a project with default templete
  config <cmd>        Taro config
  create              Create page for project
  build               Build a project with options
  update              Update packages of taro
  info                Diagnostics Taro env info
  doctor              Diagnose taro project
  inspect             Inspect the webpack config
  convert             Convert native WeiXin-Mini-App to Taro app
  help [cmd]          display help for [cmd]
```

日常的开发中，可以根据实际需要去使用这些指令帮我们完成一些操作。

**开发工具**

主要指编辑器，前端开发，使用较多的是 vscode 和 webstorm，个人建议使用 vscode

如果使用 vscode 编辑器，一定不要忘了其强大的插件系统， 可以帮我们非常大的提升开发效率。推荐 2 个非常非常建议安装的插件：ESLint、Prettier，这两个工具一个帮我们做代码的格式化，一个帮我们做格式化的规则校验，搭配使用，非常完美。

除了这 ESLint 和 Prettier 之外，也有其他的一些插件，这些插件，就根据各位开发者选择的开发技术选型自己做选择了，如果选择了 Vue 作为基础的技术栈，那么就建议安装 Vetur、volar，如果选择了 react 作为基础的技术栈，那么就建议安装 ES7 React/Redux/GraphQL/React-Native snippets。剩下的就比较具有针对性了，就不再一一列举了。

**终端**

对于使用 Mac 的开发者来说，也别配置的花里胡哨的了，就直接使用系统默认的终端 shell 就可以了，bash 或者 zsh。

如果使用的 Windows，也是建议使用系统默认的命令行工具 cmd 或者 PowerShell。因为新版本的 windows 集成了 WSL，那么 windows 上最好就是使用 WSL 并使用 Linux 分发版的终端运行 taro 的命令行工具。由于 taro 的命令行工具都是在类 unix 系统上做的测试，所以可能会出现在 windows 上运行的 bug，带来开发体验上的缺失。

### 2. 基础教程

**创建项目**

taro 命令行，通过 taro init 指令创建新的项目

```bash
xxx@xxx taroPro % taro init
👽 Taro v3.3.19

Taro 即将创建一个新项目!
Need help? Go and open issue: https://tls.jd.com/taro-issue-helper

? 请输入项目名称！ taro1
? 请输入项目介绍！ 基本环境熟悉、技术栈熟悉
? 请选择框架 React
? 是否需要使用 TypeScript ？ Yes
? 请选择 CSS 预处理器（Sass/Less/Stylus） Less
? 请选择模板源 Gitee（最快）
✔ 拉取远程模板仓库成功！
? 请选择模板 默认模板

✔ 创建项目: taro1
✔ 创建文件: taro1/.npmrc
✔ 创建文件: /Users/a58/Documents/workspace/learning/taroPro/taro1/.editorconfig
✔ 创建文件: /Users/a58/Documents/workspace/learning/taroPro/taro1/.eslintrc
✔ 创建文件: /Users/a58/Documents/workspace/learning/taroPro/taro1/.gitignore
✔ 创建文件: /Users/a58/Documents/workspace/learning/taroPro/taro1/babel.config.js
✔ 创建文件: /Users/a58/Documents/workspace/learning/taroPro/taro1/global.d.ts
✔ 创建文件: /Users/a58/Documents/workspace/learning/taroPro/taro1/package.json
✔ 创建文件: /Users/a58/Documents/workspace/learning/taroPro/taro1/project.config.json
✔ 创建文件: /Users/a58/Documents/workspace/learning/taroPro/taro1/project.tt.json
✔ 创建文件: /Users/a58/Documents/workspace/learning/taroPro/taro1/tsconfig.json
✔ 创建文件: /Users/a58/Documents/workspace/learning/taroPro/taro1/config/dev.js
✔ 创建文件: /Users/a58/Documents/workspace/learning/taroPro/taro1/config/index.js
✔ 创建文件: /Users/a58/Documents/workspace/learning/taroPro/taro1/config/prod.js
✔ 创建文件: /Users/a58/Documents/workspace/learning/taroPro/taro1/src/app.config.ts
✔ 创建文件: /Users/a58/Documents/workspace/learning/taroPro/taro1/src/app.less
✔ 创建文件: /Users/a58/Documents/workspace/learning/taroPro/taro1/src/app.ts
✔ 创建文件: /Users/a58/Documents/workspace/learning/taroPro/taro1/src/index.html
✔ 创建文件: /Users/a58/Documents/workspace/learning/taroPro/taro1/src/pages/index/index.config.ts
✔ 创建文件: /Users/a58/Documents/workspace/learning/taroPro/taro1/src/pages/index/index.less
✔ 创建文件: /Users/a58/Documents/workspace/learning/taroPro/taro1/src/pages/index/index.tsx

✔ cd taro1, 执行 git init
✔ 安装成功
……
```

下面还有一些提示的信息，不过到这里就已经提示项目创建成功了，就没有把所有的提示信息都贴过来了，各位开发者在自己创建项目的时候，可以注意一下。

创建好的最简单项目结构图

```markdown
taro1
├─.editorconfig
├─.eslintrc
├─babel.config.js
├─global.d.ts
├─package-lock.json
├─package.json
├─project.config.json
├─project.tt.json
├─tsconfig.json
├─src
| ├─app.config.ts
| ├─app.less
| ├─app.ts
| ├─index.html
| ├─pages
| | ├─index
| | | ├─index.config.ts
| | | ├─index.less
| | | └index.tsx
├─config
| ├─dev.js
| ├─index.js
| └prod.js
```

**项目运行**

项目创建好了之后，第一件要做的事情，就是要保证我们刚刚创建的干净的项目，是否可以正常的运行起来。

干净的项目能够正常的运行起来，是整个应用的基础，地基不牢，何谈高楼。

项目运行的方式，可以通过查看 package.json 去了解

```json
  "scripts": {
    "build:weapp": "taro build --type weapp",
    "build:swan": "taro build --type swan",
    "build:alipay": "taro build --type alipay",
    "build:tt": "taro build --type tt",
    "build:h5": "taro build --type h5",
    "build:rn": "taro build --type rn",
    "build:qq": "taro build --type qq",
    "build:jd": "taro build --type jd",
    "build:quickapp": "taro build --type quickapp",
    "dev:weapp": "npm run build:weapp -- --watch",
    "dev:swan": "npm run build:swan -- --watch",
    "dev:alipay": "npm run build:alipay -- --watch",
    "dev:tt": "npm run build:tt -- --watch",
    "dev:h5": "npm run build:h5 -- --watch",
    "dev:rn": "npm run build:rn -- --watch",
    "dev:qq": "npm run build:qq -- --watch",
    "dev:jd": "npm run build:jd -- --watch",
    "dev:quickapp": "npm run build:quickapp -- --watch"
  }
```

现在 taro 支持 9 个端，分别为微信小程序、百度小程序、支付宝小程序、头条小程序、H5、React Native、qq 小程序、jd 小程序以及快应用。

**输出目录设置**

输出目录，在 config/index.js 文件中设置，文件默认设置的输出目录为根目录下的 dist 目录。

如果是单一的项目，这样做也没什么问题，但是我觉着这样设置有点不够灵活，体现不了多端统一的优势,不同端的代码应该可以被编译到不同的目录下面。

当然了，我们同时只能调试一个端的效果，只要关注一个端就可以了，大部分时候这样也是没有问题的，只是我想有一个明确的提示，比如我当前在调试微信小程序端，那么我的目录就是在 weapp 目录下，那么我从目录就可以直观的看到我当前调试的是是微信小程序，再比如我当前调试的是 H5，那么我就可以直观的从编译的代码目录就直观的发现我现在在调试 H5。

当然了这些都不是技术上的问题，更大程度上仅仅是心理上的一点感知问题，如果想做一些灵活的配置，可以在/config/index.js 文件配置

```js
// config/index.js

// 文件固定编译输出到dist目录下
// outputRoot: 'dist',
// 编译后的文件，根据当前的端输出到不同的目录下
outputRoot: `dist/${process.env.TARO_ENV}`,
```
