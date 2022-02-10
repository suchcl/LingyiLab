### zsh: command not found: umi

在终端执行umi dev时，报出了异常：

```bash
xx@xxxxf umi1 % umi dev
zsh: command not found: umi
```

原因很简单，肯定是没有找到umi指令，就是umi没有安装了，全局安装一下就可以了。

yarn global add umi

```bash
xx@xxxx umi1 % yarn global add umi 
yarn global v1.22.17
[1/4] 🔍  Resolving packages...
warning umi > @umijs/preset-built-in > @types/react-router-config > @types/history@5.0.0: This is a stub types definition. history provides its own type definitions, so you do not need this installed.
warning umi > @umijs/runtime > @types/react-router-dom > @types/history@5.0.0: This is a stub types definition. history provides its own type definitions, so you do not need this installed.
warning umi > @umijs/runtime > @types/react-router > @types/history@5.0.0: This is a stub types definition. history provides its own type definitions, so you do not need this installed.
warning umi > @umijs/bundler-webpack > node-libs-browser > url > querystring@0.2.0: The querystring API is considered Legacy. new code should use the URLSearchParams API instead.
warning umi > @umijs/bundler-webpack > postcss-preset-env > postcss-color-gray > postcss-values-parser > flatten@1.0.3: flatten is deprecated in favor of utility frameworks such as lodash.
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
[4/4] 🔨  Building fresh packages...
success Installed "umi@3.5.20" with binaries:
      - umi
✨  Done in 4.77s.
```

安装成功，接下来执行umi指令

umi dev

```bash
xxx@xxxxxx umi1 % umi dev 
Browserslist: caniuse-lite is outdated. Please run:
npx browserslist@latest --update-db

Why you should do it regularly:
https://github.com/browserslist/browserslist#browsers-data-updating
Bundle with webpack 5...
⏱️  MFSU Enabled
Starting the development server...

✔ Webpack
  Compiled successfully in 2.92s

 DONE  Compiled successfully in 2929ms                                                                                                                                                         上午9:50:15


● Webpack █████████████████████████ cache (99%)  
 store build dependencies


  App running at:
  - Local:   http://localhost:8000 (copied to clipboard)
  - Network: http://10.240.36.223:8000
```

可以看到，已经可以通过umi执行指令了。

umi有以下几个指令：

```bash
mfsu      
    build     # build application for production
    config    # umi config cli
    dev       # start a dev server for development
    generate  # generate code snippets quickly
    help      # show command helps
    plugin    # inspect umi plugins
    version   # show umi version
    webpack   # inspect webpack configurations
    dva       
    test      # test with jest
```

一般情况下，是不建议全局安装umi的，和webpack一样，只需要项目内安装就可以了。一来可以避免全局指令和项目内指令产生冲突、迷惑，项目内安装，在通过scripts执行的时候，是执行的项目内安装的指令的。