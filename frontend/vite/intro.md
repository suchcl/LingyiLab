## vite搭建前端工程

### vite简介

#### 预构建

- 将非ESM规范的代码转换为ESM规范的代码,另外就是将第三方依赖内部的多个文件合并为一个,减少http请求数量
- vite在一开始将应用中的模块分为依赖和源码两类:
  - 依赖部分:指在代码中用到的第三方模块,如vue、axios、react、lodash等,vite使用esbuild在应用启动时对于依赖部分进行预构建依赖;
  - 源码部分:日常项目开发时我们自定义的.js、.jsx、.vue等文件,这部分代码会在运行时被编译,但是并不会进行任何的打包动作,vite将以原生ESM方式的提供源码;
- 开发环境中,vite让浏览器接管了部分打包程序的工作,vite只需要在浏览器请求源码时进行转换并按需提供源码.根据情景动态导入代码,即只有在当前屏幕上显示时才会被处理;
- 在生产环境中,vite利用rollup对代码进行打包处理,并配合着tree-shaking、懒加载和chunk分割为浏览器提供最后的代码资源;

#### esbuild

- vite是使用esbuild来做预构建和内容转换的,同等规模的项目,使用esbuild可以将打包速度提升10-100倍;
- esbuild是一款基于go开发的javascript打包工具,其最大的特征就是快,核心目标就是开创构建工具性能的新时代,同时创建一个易于使用的现代构建工具;
- esbuild支持多种模块格式,包括commonjs、es6模块、AMD等,使得它适用于任何类型的js项目;

#### 缓存

#### 模块热重载HMR

### 基础配置

#### 配置文件

#### vite-plugin-html

#### 别名配置

#### 打包配置

#### css处理

#### css配置

#### 环境变量

#### 开发服务器

### 插件

#### @vitejs/plugin-vue2

#### @vitejs/plugin-vue

#### @vitejs/plugin-legacy

#### vite-plugin-mock

### 配置文件汇总

#### vite.config.js