### 搭建项目

官方文档: [https://nextjs.org/](https://nextjs.org/)

> 在有语言基础的情况下，尽量看官方文档，因为官方文档是最权威的。翻译的文档，带有译者的一些个人观点，可能不会那么客观，理解起来特别费劲，如果你和译者产生不了共鸣，就有可能会误入歧途。但是Next.js的官方文档呢，确实也不够争气，点哪个哪个不动，使用起来特别不顺手。

在最新的React中(React19)，官方推荐使用社区流行的框架去搭建React应用，然后在下面给出了Next.js的相关介绍，说明React从19开始，将重点放在了对Next.js的支持上，所以如果是搭建React的项目，可以考虑直接上Next.js了。


初始化项目

```bash
npx create-next-app@latest
```

### next.js初步了解

1. 布局文件


2. 集成scss

next.js默认不能使用scss，需要安装依赖，安装依赖之后，即可直接使用。

```bash
npm install sass --save-dev
yarn add sass --dev
pnpm add sass -D
```

包管理器任意，自己习惯即可。

3. 默认的项目目录结构

```markdown
next.js
├─README.md
├─eslint.config.mjs
├─next-env.d.ts
├─next.config.ts
├─package-lock.json
├─package.json
├─pnpm-lock.yaml
├─tsconfig.json
├─src
|  ├─app
|  |  ├─favicon.ico
|  |  ├─globals.css
|  |  ├─layout.tsx
|  |  ├─page.module.css
|  |  ├─page.tsx
|  |  ├─template.tsx
|  |  ├─dashboard
|  |  |     ├─dashboard.module.scss
|  |  |     ├─layout.tsx
|  |  |     ├─page.tsx
|  |  |     ├─settings
|  |  |     |    └page.tsx
├─public
|   ├─file.svg
|   ├─globe.svg
|   ├─next.svg
|   ├─vercel.svg
|   └window.svg
```

上面目录中，dashboard目录是我新增上的，app目录下的template.tsx我新增的，其他的都是默认的。这基本就是一个完整的next.js项目的目录结构。

每个文件的意义，不必赘述。

4. 路由：应用路由和页面路由

<font color="red">到目前为止，我不太理解这2种路由的区别。</font>

不太理解什么算是应用路由，什么算是页面路由。

5. 