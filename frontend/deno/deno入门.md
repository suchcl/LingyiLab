### Deno简介

Deno是一个Javascript/Typescript的运行时,默认使用安全环境执行代码,有着卓越的开发体验.Deno有以下的一些功能亮点:

- 默认安全.外部代码没有文件系统、网络、环境的访问权限,除非显示开启

- 支持开箱即用的Typescript环境

- 只分发一个独立的可执行文件(deno)

- 有着内置的工具箱,如信息依赖查看器(deno info)、代码格式化工具(deno fmt)

- 有一组经过审计的标准模块,保证能够在deno上工作;

- 脚本代码能被打包为一个单独的javascript文件

### Deno安装

deno是一个跨平台的javascript、typescript、WebAssembly的运行时环境,即基于Chrome V8引擎的运行时环境,该运行时环境是使用rust语言开发的,并使用Tokio库来构建事件循环系统.Deno建立在V8、Rust和Tokio的基础上.

```bash
# MacOS
curl -fsSL https://x.deno.js.cn/install.sh | sh

# windows
irm https://x.deno.js.cn/install.ps1 | iex

# Linux
curl -fsSL https://x.deno.js.cn/install.sh | sh
```

检测是否安装成功:通过执行deno --version查看deno版本的方式可以确认deno是否被正常安装

```bash
[jsr]$ deno --version
deno 1.41.1 (release, x86_64-apple-darwin)
v8 12.1.285.27
typescript 5.3.3
```

执行了deno --version后,有关于deno、v8和ts版本的输出,就说明deno已经被正常安装了.

### 快速构建一个deno程序

```ts
// Hello.ts
interface Person {
    firstName: string;
    lastName: string;
}

function sayHello(p: Person): string {
    return `Hello, ${p.firstName} ${p.lastName}`;
}

const ada: Person = {
    firstName: "Ada",
    lastName: "Lovelace"
};
console.log(sayHello(ada));
```

通过deno来执行这个程序

```bash
deno run -A Hello.ts # Hello, Ada Lovelace
```

执行deno后,Hello.ts代码被正常的执行了.第一个入门的deno程序已经完成.

### Deno和Node的区别?


