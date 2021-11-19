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

##### 1.1.2 通过npx创建项目

```bash
npx create-nuxt-app nuxt2 # 创建一个项目名称为nuxt2的nuxt项目
```

使用npx创建项目，其本质上还是通过create-nuxt-app，只是不需要全局安装一下create-nuxt-app了，项目的创建过程就不再这里描述了。

##### 1.1.3 项目目录结构

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

> nuxt会自动监听pages目录中文件的变化，当pages目录中的文件发生变化时，不需要重新启动服务器就可以直接看到效果。

**assets**：资源目录，用来组织未编译的项目的静态资源目录，如less、sass、js、ts等

**components**：组件目录，拥有组织vue组件。nuxt不会扩展增强该目录下的vue组件，也就是说components目录下的vue组件不会像页面组件那样拥有asyncData方法的特性

layouts：布局目录。通过create-nuxt-app创建的项目，默认没有layouts目录，如果架构需要，可以自己创建，按照和这个规范去创建。该目录下的是应用的布局组件，如果没有额外的配置，该目录名不能被重命名

**middleWare**：中间件目录

**pages**：页面目录。nuxt.js框架读取该目录下的所有.vue文件并自动生成对应的路由配置

**plugins**：插件目录。

**static**：静态文件目录，该目录下存放不需要nuxt.js调用webpack进行构建、编译的处理的静态文件。服务器启动的时候，该目录下的文件会自动被映射到应用的根目录/下。如/static/index.html会被映射到/index.html。

**store**：用于组织项目的状态文件。Nuxt.js集成了Vuex状态树的相关功能配置，在store目录下创建一个index.js自动激活vuex相关配置。

如果没有必要的配置，store目录不可修改路径名

**nuxt.config.js**：用于组织Nuxt应用的个性化配置，以覆盖默认的配置。

如果没有必要的配置，该目录名不可修改

**package.json**：用于描述应用的依赖关系和对外暴露的脚本接口； 该文件不可被重命名









