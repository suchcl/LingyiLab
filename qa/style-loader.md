### ERROR in ./src/css/normal.css Module build failed: TypeError: this.getOptions is not a function at Object.loader (D:\project\node_modules\style-loader\dist\index.js:19:24) @ ./src/main.js 6:0-27

在webpack中配置了css-loader和style-loader后，进行编译的时候，报了如题的异常。

这是因为style-loader、css-loader版本过高了，调低一下版本就可以了。