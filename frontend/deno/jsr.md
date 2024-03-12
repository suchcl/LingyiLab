### JSR简介

文档:[https://jsr.io/](https://jsr.io/)

JSR,全名Javascript Registry,由Deno推出的javascript注册表.有着很高的兼容性,可以与任何一个javascript的包管理器一起使用,如npm、yarn、pnpm,也可以在任何具有node_modules文件夹的项目中使用,支持deno、node、Bun等众多运行时.

与npm不同的是,jsr原生typescript支持,可直接发包无需转译成js代码,deno环境可直接使用,如果是在node.js中运行,则会将代码转译成.d.ts文件.

JSR仅支持ESM,随着ESM规范多年发展已经逐渐成熟,并广为使用,CommonJS逐渐被取代,非常多的npm包也在向ESM迁移,如ECharts v5.5,AdonisJS v6等.

### JSR的用法

JSR可以与任何一个npm包管理器一起使用,如npm、pnpm、yarn,也可以在deno项目中使用

安装JSR模块,JSR模块有多种安装方式,可以使用各种npm的包管理器,也可以使用deno,Bun

```bash
# deno
deno add @emish89/smile2emoji

# npm
npx jsr add @emish89/smile2emoji

# yarn
yarn dlx jsr ad @emish89/smile2emoji

# pnpm
pnpm dlx jsr add @emish89/smile2emoji

# Bun
bunx jsr add @emish89/smile2emoji
```

代码中引入JSR包

```js
import * as mod from "@emish89/smile2emoji";
```

```js
import { debounce } from "@yuci/utils";

useEffect(() => {
    window.addEventListener("scroll", debounce(scroll, 50));
    return () => {
        window.removeEventListener("scroll", debounce(scroll, 50))
    }
},[]);
```

Deno原生支持JSR,可以不需要安装,直接使用jsr:说明符即可使用.

```js
import { capitalizeFirstLetter } from "jsr:@yuci/utils";
capitalizeFirstLetter('yuci');
```

### 发包到JSR

在官网([https://jsr.io](https://jsr.io))登录,点击publish a package进行发布即可,根据要求填写相应信息即可.

#### 1. 创建项目

可以通过npm init或者deno init来初始化项目.

```bash
[xxxxx jsr]$ deno init
✅ Project initialized

Run these commands to get started

  # Run the program
  deno run main.ts

  # Run the program and watch for file changes
  deno task dev

  # Run the tests
  deno test
```

通过deno init初始化的项目结构,如下图:

<img src="./images/i2.png" width="300" />

#### 2. 开发

#### 3. 发布

#### 4. 自动发布
