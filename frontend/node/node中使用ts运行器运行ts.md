### Node.js对ts的支持

Deno可以原生的运行ts，但是Node.js还不行，它不能够原生的运行ts。

那么使用ts构建的node项目就需要通过一定的方式，将ts代码转换为js，然后再去运行。

> 不过node从22.6.0以来，对ts的某些语法进行了实验性的支持，这样，就可以直接在node中运行ts代码了。还没有测试过，找个机会测试下。

### Node.js中运行ts代码方式

传统ts文件的执行方式：

1. tsc进行类型检查,编译ts文件

2. 运行js

3. 程序运行,或者启动服务

那么现在的一些前端库项目中,大多数都是用ts开发了,然后选择rollup编译出es module或者Commonjs等同类型的模块,提供给其他应用去使用.那么问题来了.

怎么直接去运行ts或者tsx文件呢?

#### 使用转译器运行

使用tsc将ts代码转译为js，然后在node中运行js，这样间接实现了node中运行ts的能力

#### 使用运行器运行

node中常用的有ts-node和tsx。

通过使用运行器，也可以直接在node项目中运行ts了。

**那么ts-node和tsx有什么区别呢?**

Node.js环境带有ES Module运行ts文件

- t s-node
- tsx/esno

```json
{
    "scripts": {
        "dev::tsnode": "ts-node src/index.ts",
        "dev::tsnode::esm": "ts-node-esm src/index.ts",
        "dev::tsx": "tsx src/index.ts",
        "dev::esno": "esno src/index.ts"
    },
}
```

前端项目中,可以通过简单配置,使用node环境自带的es模块去执行ts文件.

参考链接: [https://juejin.cn/post/7163685872750034981](https://juejin.cn/post/7163685872750034981)

| ts-node                    | tsx               | esno              |
| -------------------------- | ----------------- | ----------------- |
| 区分es module和非es module | 原生支持es module | 原生支持es module |
| 默认运行commonjs模块       |                   |                   |
| 使用swc形式运行            |                   |                   |

tsx和esno基于esbuild,原生支持es module,无需指定环境,package.json中不需要指定type: "module"

```json
{
  "scripts": {
    "dev:tsx": "tsx src/index.ts",
    "dev:esno": "esno src/index.ts"
  }
}
```

**esno是什么?**

esno是一个基于esbuild的ts运行时,该库会针对不同的模块化标准,采用不同的方案.

- esno:Node in CJS mode - by esbuild-register
- esmo:Node in ems node - by esbuild-node-loader



#### node原生支持运行

自v22.6.0以来，node提供了某些对ts语法的实验性支持，这样，可以在node中直接运行ts代码了。
