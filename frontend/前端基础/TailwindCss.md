<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. 工作原理](#1-%E5%B7%A5%E4%BD%9C%E5%8E%9F%E7%90%86)
- [2. 优势](#2-%E4%BC%98%E5%8A%BF)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 1. 工作原理

Tailwind Css工作原理是扫描所有html、javascript文件以及任何模板中的css类(class)名,然后生成相应的样式代码并写入到一个css文件中.

### 2. 优势

它快速、灵活、可靠,没有运行时负担

### 3. 环境搭建

以vue项目中的使用为例

#### 3.1 安装tailwindcss

```bash
# 创建项目
npm create vite@latest demo -- --template vue
# 安装依赖
npm install tailwindcss postcss autoprefixer --save-dev
# 创建tailwindcss配置文件 tailwind.config.js
npx tailwindcss init

# 在tailwind.config.js配置文件中添加所有模板文件的路径

module.exports = {
    content: ["./src/**/*.{html,js,ts,jsx,tsx,vue}"],
    theme: {
        extends:{}
    },
    plugins:[]
};
# style.css中引入tailwindcss指令和基础类库
# style.css
@tailwind base;
@tailwind components;
@tailwind utilities;

# 运行开发环境
npm run dev

# 在vue中使用内置的class
<div class=" text-red-500 text-ellipsis text-6xl">测试一下</div>
```
<img src="./images/i14.png" width="500" />

以vite为打包工具时的react项目,和vue完全一样,只是在创建项目的时候将模板设置为react就可以了.

#### 3.2 自定义样式

### 4. 总结

这个框架,有一定的优势,在遵守其规则的情况下,可以节省很多css代码的代码量,这样的系统在做后台管理系统的时候,风格较为统一,个人以为有很大的优势.但是如果是C端项目,追求个性化的项目,使用这样的库,就是给自己找麻烦.C端项目追求个性化,每个公司、每个业务的都想给用户最个性化的部分,展示给用户自己最美好的一面,而不会追求统一,那么这种的类库就不适合.

这个类库,就是bootstrap库的一个升级吧,在几年前bootsctrap可以直接通过script、link的方式引入到项目中,现在的tailwindcss可以通过npm、配置的方式注入到项目中了,比bootstrap在技术上有了提升,但是本质上是一样的UI库.

bootstrap几个主要的大版本如bootstrap3、bootstrap4、bootstrap5,其每个版本的大功能的变化并不是很大,变的是一些功能在技术上的实现细节.如bootstrap3依赖jquery,bootstrap4不再依赖jquery了,bootstrap5开始就不再支持IE了,其发展方向根据当前的技术发展的趋势,而不是说去实现了一个大而全的能真正满足用户各种需求的库.