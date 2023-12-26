### vuepress

vuepress是一个以markdown为中心的静态站点生成器,我们可以使用markdown来书写内容,然后通过Vuepress来生成一个静态的站点来显示它们.

一个Vuepress站点的本质就是一个由Vue和Vue-router驱动的单页面应用-SPA.

路由根据markdonw文件的相对路径自动生成.

### 快速创建vuepress项目

```bash
# 创建项目并进入到项目目录
mkdir vuepress && cd vuepress

# 初始化项目
yarn init # npm init也可以

# 安装依赖vuepress
yarn add -D vuepress

# 创建文档
mkdir docs && echo '# Hello Vuepress' > docs/README.md # 也可以通过编辑器的方式去创建

# 在package.json中添加scripts
{
  "scripts": {
    "dev": "vuepress dev docs",
    "build": "vuepress build docs"
  }
}

# 启动开发服务
yar dev
```

> vuepress项目,更推荐使用yarn而不是npm,因为低版本的npm可能会生成错误的版本依赖树.

### 目录结构

Vuepress遵循“约定优于配置”的原则,Vuepres是项目推荐的目录结构如下:

```markdown
vuepress
├─package.json
├─yarn.lock
├─docs
|  ├─README.md
|  ├─config.md
|  ├─guide
|  |   └README.md
|  ├─.vuepress(可选)
|  |     ├─config.js(可选)
|  |     ├─enhanceApp.js(可选)
|  |     ├─theme(可选)
|  |     |   └Layout.vue
|  |     ├─templates(可选,谨慎配置)
|  |     |     ├─dev.html
|  |     |     └ssr.html
|  |     ├─styles(可选)
|  |     |   ├─index.styl
|  |     |   └palette.styl
|  |     ├─public(可选)
|  |     ├─components(可选)
```

* docs/.vuepress:用于存放全局的配置、组件、静态资源等

* docs/.vuepress/components:该目录中的Vue组件将会被自动注册为全局组件

* docs/.vuepress/theme: 用于存放本地主题

* docs/.vuepress/styles:用于存放样式相关的文件

* docs/.vuepress/styles/index.styl:将会被自动应用到全局的样式文件,会最终生成css文件,比默认样式的优先级要高

* docs/.vuepress/styles/palette.styl:用于重写默认颜色常量,或者设置新的stylus颜色常量

* docs/.vueprss/public:静态资源目录

* docs/.vuepress/templates: 存储HTML模板文件

* docs/.vuepress/templates/dev.html: 用于开发环境的html模板文件

* docs/.vuepress/templates/ssr.html:构建时基于Vue SSR的HTML模板文件

* docs/.vuepress/configjs:配置文件的入口文件,也可以是YML或toml

* docs/.vueperss/enhanceApp.js:客户端应用的增强

### 默认的页面路由

默认的页面理由,是根据package.json中的dev和build配置来确定的,如下的配置:

```json
  "scripts": {
    "dev": "vuepress dev docs",
    "build": "vuepress build docs"
  },
```

这个配置的默认参考路由就是docs,docs就是targetDir,下面所有文件的相对路径都是相对于docs.

### 配置