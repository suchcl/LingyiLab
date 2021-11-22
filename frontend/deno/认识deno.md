### 1. 认识 deno

官网：[https://deno.js.cn/](https://deno.js.cn/)

Deno 是一个安全的 javascript 和 typescript 运行时环境。

deno 是一个简单、现代且安全的 javascript 和 typescript 运行时环境，其基于 V8 引擎并采用 rust 编程语言构建。

1. 默认安全设置：除非显示的开启，否则没有文件、网络，也不能访问运行环境
2. 原生支持 Typescript
3. 只有一个单一的可执行文件
4. 自带实用工具，例如依赖检查器（deno info）和代码格式化工具（demo fmt）
5. 有一套经过审核（审计）的标准模块，确保与 deno 兼容

### 2. 安装

deno 没有外部依赖，直接安装即可。

windows 上安装：

```bash
iwr https://deno.land/x/install/install.ps1 -useb | iex
```

Mac 可以通过 Homebrew 安装:

```bash
brew install deno
```

其他的还有多种安装方式，官网都提供了，因为我的机器是 windows 的，直接使用的 iwr 的方式安装的。

### 3. 入门

deno 通过 deno run filename 指令运行 js 或者 ts 文件

```bash
# 运行js文件
PS D:\deno> deno run .\index.js
deno

# 运行ts文件
PS D:\WebStudy\deno> deno run .\index.ts
Check file:///D:/WebStudy/deno/index.ts
Ts deno
```

从示例中可以看到，deno 运行 js 和 ts 文件时，运行 ts 文件比运行 js 文件多了一步 check 的动作。
