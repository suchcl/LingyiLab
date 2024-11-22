## vite搭建前端工程

### vite简介

#### 预构建

- 将非ESM规范的代码转换为ESM规范的代码,另外就是将第三方依赖内部的多个文件合并为一个,减少http请求数量
- vite在一开始将应用中的模块分为依赖和源码两类:
  - 依赖部分:指在代码中用到的第三方模块,如vue、axios、react、lodash等,vite使用esbuild在应用启动时对于依赖部分进行预构建依赖;
  - 源码部分:日常项目开发时我们自定义的.js、.jsx、.vue等文件,这部分代码会在运行时被编译,但是并不会进行任何的打包动作,vite将以原生ESM方式的提供源码;

#### esbuild

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