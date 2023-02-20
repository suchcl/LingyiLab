最近要做一个移动端项目，由于PC端项目是使用umi写的，所以这个移动端项目计划继续使用umi开发。在开发前需要解决移动端项目的适配问题。

### umi3项目配置移动端页面适配

umi3项目中，我使用了lib-flexible和postcss-px2rem-exclude这2个依赖包。配置步骤:

1. 下载依赖

```bash
yarn add lib-flexible postcss-px2rem-exclude -D
```

2. 在.umirc.ts中配置postcss-px2rem-exclude依赖

```ts
import { defineConfig } from 'umi';
// 导入依赖包
const px2rem = require("postcss-px2rem-exclude");

export default defineConfig({
  // 通过extraPostCSSPlugins配置插件
  extraPostCSSPlugins: [
    px2rem({
      remUnit: 75,
      exclude: '/node_modules/i'
    })
  ]
});
```

3. 在入口文件导入lib-flexible

umi项目中是没有入口文件的，严格来说有入口文件，在src/.umi目录下，只不过src/.umi目录中都是临时文件，只不过每次随着代码改动都会被重新生成，所以改动这里的入口文件是没有任何效果的。

在umi3项目中，可以通过在全局文件中导入，也可以在app.ts中导入。

> app.ts并不是umi项目的入口文件，而是项目的运行时配置文件，只不过这个文件可以被全局所引用

```ts
// 在app.ts中导入lib-flexible
import "lib-flexible";

// 或者在全局文件中导入lib-flexbile
// src/pages/index.tsx
import "lib-flexible";
```

在全局文件导入的时候，如果有全局布局文件如/src/layouts之类的文件，那么就可以该全局的布局文件中导入lib-flexible。

### umi4项目配置移动端页面适配