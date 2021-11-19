### 1. 安装

可以全局安装create-nuxt-app

```bash
npm install create-nuxt-app -g
```

一般的情况下，我们很少经常性的去创建项目，所以更优的实践，已经不是去全局安装一个项目工具了，而是通过npx直接使用使用create-nuxt-app去创建一个nuxt.js项目

npx,在npm5.2.0版本中就已经继承了，不需要单独安装。

#### 1.1 创建项目

##### 1.1.1 通过全局的create-nuxt-app创建

```bash
create-nuxt-app nuxtpro // 创建一个项目名为nuxpro的nuxt项目
```

```bash
PS D:\nuxt> create-nuxt-app nuxt1

create-nuxt-app v3.7.1
✨  Generating Nuxt.js project in nuxt1
? Project name: nuxt1
? Programming language: JavaScript
? Package manager: Npm
? UI framework: Element
? Nuxt.js modules: (Press <space> to select, <a> to toggle all, <i> to invert selection)
? Linting tools: (Press <space> to select, <a> to toggle all, <i> to invert selection)
? Testing framework: None
? Rendering mode: Universal (SSR / SSG)
? Deployment target: Server (Node.js hosting)
? Development tools: (Press <space> to select, <a> to toggle all, <i> to invert selection)
? What is your GitHub username?
? Version control system: Git
npm WARN deprecated core-js@2.6.12: core-js@<3.3 is no longer maintained and not recommended for usage due to the numbe
r of issues. Because of the V8 engine whims, feature detection in old core-js versions could cause a slowdown up to 100
x even if nothing is polyfilled. Please, upgrade your dependencies to the actual version of core-js.
npm WARN deprecated querystring@0.2.1: The querystring API is considered Legacy. new code should use the URLSearchParam
s API instead.
npm WARN deprecated flatten@1.0.3: flatten is deprecated in favor of utility frameworks such as lodash.
npm WARN deprecated querystring@0.2.0: The querystring API is considered Legacy. new code should use the URLSearchParam
s API instead.
npm WARN deprecated chokidar@2.1.8: Chokidar 2 will break on node v14+. Upgrade to chokidar 3 with 15x less dependencie
s.
npm WARN deprecated resolve-url@0.2.1: https://github.com/lydell/resolve-url#deprecated
npm WARN deprecated urix@0.1.0: Please see https://github.com/lydell/urix#deprecated
npm WARN deprecated fsevents@1.2.13: fsevents 1 will break on node v14+ and could be using insecure binaries. Upgrade t
o fsevents 2.
# 后面是项目的初始化过程，代码没有全部贴过来
```

在创建项目时，和vue、react、next.js创建项目基本一直，有一些默认的选项需要选，或者一些需要填，也可以都使用默认的。

如果使用默认的选项，一路回车就可以了。

1.1.2 通过npx创建项目

```bash
npx create-nuxt-app nuxt2 # 创建一个项目名称为nuxt2的nuxt项目
```

使用npx创建项目，其本质上还是通过create-nuxt-app，只是不需要全局安装一下create-nuxt-app了，项目的创建过程就不再这里描述了。

1.1.3 项目目录结构

```markdown
├─.editorconfig
├─nuxt.config.js
├─package-lock.json
├─package.json
├─README.md
├─tree.md
├─store
|   └README.md
├─static
|   └favicon.ico
├─plugins
|    └element-ui.js
├─pages
|   └index.vue
├─components
|     ├─NuxtLogo.vue
|     └Tutorial.vue
```



