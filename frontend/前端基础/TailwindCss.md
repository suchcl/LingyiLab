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

#### 3.1 安装tailwindcss

```bash
npm install tailwindcss --dev
# 创建tailwindcss配置文件 tailwind.config.js
npx tailwindcss init

# 在tailwind.config.js配置文件中添加所有模板文件的路径

module.exports = {
    content: ["./src/**/*.{html,js}"],
    theme: {
        extends:{}
    },
    plugins:[]
};
```

#### 3.2 自定义样式

### 4. 总结

这个框架,有一定的优势,在遵守其规则的情况下,可以节省很多css代码的代码量,这样的系统在做后台管理系统的时候,风格较为统一,个人以为有很大的优势.但是如果是C端项目,追求个性化的项目,使用这样的库,就是给自己找麻烦.C端项目追求个性化,每个公司、每个业务的都想给用户最个性化的部分,展示给用户自己最美好的一面,而不会追求统一,那么这种的类库就不适合.

这个类库,就是bootstrap库的一个升级吧,在几年前bootsctrap可以直接通过script、link的方式引入到项目中,现在的tailwindcss可以通过npm、配置的方式注入到项目中了,比bootstrap在技术上有了提升,但是本质上是一样的UI库.