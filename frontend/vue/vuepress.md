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