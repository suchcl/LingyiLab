### 1.Umi 简介

Umi，是蚂蚁金服的底层、可扩展的企业级前端应用框架，以路由为基础，支持配置路由和约定式路由，保证路由的功能完备。

**Umi 的特点**

1. 可扩展：umi 实现了完整的生命周期，并使其插件化，umi 内部功能也全由插件完成，另外也支持插件和插件集，以满足功能和垂直域的分层需求；

2. 开箱即用：umi 内置了路由、构建、部署、测试等，仅需一个依赖即可上手开发，并且还提供针对 React 的集成插件集，内涵丰富的功能，可满足大部分的开发需求；

3. 企业级：蚂蚁内部以及阿里、优酷、网易、飞猪、口碑等公司的大量应用实践，值得信赖；

4. 大量自研：包含微前端、组件打包、文档工具、请求库、hooks、数据流等，满足日常的周边需求；

5. 完备路由：同时支持配置式路由和约定式路由，同时保证功能的完备性，比如动态路由、嵌套路由、权限路由等；

6. 面向未来：在满足需求开发的同时，也在实时保持对新技术的探索，如 dll 提速、modern mode、webpack@5、自动化 external、bundle less 等；

**不适合 Umi 的场景**

1. 需要兼容 IE8 以及更低版本的浏览器

2. 需要支持 16.8.0 以下版本的 React

3. 需要跑在 Node 10 以下版本的环境

4. 有很强的 webpack 自定义需求和主观意愿

5. 需要选择不同的路由方案

**插件和插件集**

<img src="./images/i1.png" alt="umi支持插件和插件集" style="zoom: 30%;">

Umi 支持插件和插件集，不同的插件集合到一起形成各种插件集，不同的插件集又可以支持不同的业务类型。

**配置式路由和约定式路由**

umi 同时支持配置式路由和约定式路由，配置式路由是大部分用户在使用的，是向现实的妥协，因为它功能强大；约定式路由是在努力的，因为它更加的优雅、简洁。

**.umi 临时文件**

.umi临时文件被称为整个umi项目的发动机，项目的入口文件、路由等都在这里，这些文件是由 umi 内部插件及第三方插件生成的。

.umi临时文件生成在src目录下

在.umi 目录下通常可以看到这样的目录/文件：

```markdown
.umi
├─umi.ts  // 入口文件
├─plugin-request
|       └request.ts
├─plugin-model
|      ├─Provider.tsx
|      ├─runtime.tsx
|      ├─useModel.tsx
|      ├─helpers
|      |    ├─constant.tsx
|      |    ├─dispatcher.tsx
|      |    └executor.tsx
├─plugin-initial-state
|          ├─Provider.tsx
|          ├─exports.ts
|          ├─runtime.tsx
|          ├─models
|          |   └initialState.ts
├─plugin-helmet
|       └exports.ts
├─core
|  ├─devScripts.ts
|  ├─history.ts
|  ├─plugin.ts
|  ├─pluginConfig.d.ts
|  ├─pluginRegister.ts
|  ├─polyfill.ts
|  ├─routes.ts
|  └umiExports.ts
├─.cache
|   ├─babel-loader
|   |      ├─0395cb2cefdacebd957375d458411a10.json.gz
|   |      ├─0dc2e049637a87e86d6a661a38dd651a.json.gz
|   |      ├─10402cd3212c5aa97f851abca1d23a18.json.gz
|   |      ├─112abf79079ca5a84012e798bd69353e.json.gz
|   |      ├─1c8e28554df70209c71e20b895c992e8.json.gz
```

.umi 临时文件是 umi 框架非常重要的一部分，框架和插件会根据我们的代码生成临时文件，原来一部分在项目中的调试、脏乱差的部分都移动到了这里；

我们可以在.umi 中调试代码，但是不要提交到.git，因为这个目录是临时文件，每次启动 umi 时都会删除之前的临时文件并重新生成新的临时文件。

### 2. 快速上手

通过yarn快速创建项目

> umi团队建议使用yarn作为umi项目中管理npm依赖的工具。

```bash
xxx@xxxx umi1 % yarn create @umijs/umi-app
yarn create v1.22.17
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
[4/4] 🔨  Building fresh packages...

success Installed "@umijs/create-umi-app@3.5.20" with binaries:
      - create-umi-app
[#################################################] 49/49Copy:  .editorconfig
Write: .gitignore
Copy:  .prettierignore
Copy:  .prettierrc
Write: .umirc.ts
Copy:  mock/.gitkeep
Write: package.json
Copy:  README.md
Copy:  src/pages/index.less
Copy:  src/pages/index.tsx
Copy:  tsconfig.json
Copy:  typings.d.ts
✨  Done in 1.44s.
```

表示已经通过yarn成功的创建了一个基于当前目录umi1的umi项目，其默认的项目目录结构如下：

```markdown
umi1
├─.editorconfig
├─.prettierignore
├─.prettierrc
├─.umirc.ts
├─README.md
├─package.json
├─tsconfig.json
├─typings.d.ts
├─src
|  ├─pages
|  |   ├─index.less
|  |   └index.tsx
├─mock
```

**安装依赖**

```bash
xxx@xxxx umi1 % yarn
yarn install v1.22.17
info No lockfile found.
****** # 这里省略了步骤，没有粘贴过程提示信息
[4/4] 🔨  Building fresh packages...
success Saved lockfile.
$ umi generate tmp
Browserslist: caniuse-lite is outdated. Please run:
npx browserslist@latest --update-db

Why you should do it regularly:
https://github.com/browserslist/browserslist#browsers-data-updating
✨  Done in 58.96s.
```

**项目启动**

```bash
xxx@xxxx umi1 % yarn start
yarn run v1.22.17
$ umi dev
Browserslist: caniuse-lite is outdated. Please run:
npx browserslist@latest --update-db

Why you should do it regularly:
https://github.com/browserslist/browserslist#browsers-data-updating
Starting the development server...

✔ Webpack
  Compiled successfully in 4.40s

 DONE  Compiled successfully in 4399ms                                                                                                                                                        下午10:58:58


  App running at:
  - Local:   http://localhost:8000 (copied to clipboard)
  - Network: http://192.168.3.78:8000
```

项目已经成功启动，可以通过http://localhost:8000去访问看效果：

![umi项目已经成功启动](./images/i2.png)