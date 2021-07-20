### Vetur can't find `tsconfig.json` or `jsconfig.json` in d:\www.xxx.com.

vetur0.31.0版本新增了一个vetur.config.js的配置文件，在这个版本之后，会先检查项目中是否有jsconfig.json文件（js项目，如果是ts开发的，就是tsconfig.json）。如果这两个文件都没有找到，就会给出这个提示：

```
Vetur can't find `tsconfig.json` or `jsconfig.json` in d:\www.xxx.com.
```

在创建了jsconfig.json或者tsconfig.json文件后，文件内容为：

```javascript
{
    "include": [
        "./src/*"
    ]
}
```

如果不加上上述内容，还会有异常报错，大概如下：

```bash
> @0.0.0 dev D:\viteapp
> vite
 > jsconfig.json:1:0: error: Unexpected end of file
    1 │
      ╵ ^

failed to load config from D:\viteapp\vite.config.js
error when starting dev server:
Error: Build failed with 1 error:
jsconfig.json:1:0: error: Unexpected end of file
    at failureErrorWithLog (D:\viteapp\node_modules\esbuild\lib\main.js:1449:15)
    at D:\viteapp\node_modules\esbuild\lib\main.js:1131:28
    at runOnEndCallbacks (D:\viteapp\node_modules\esbuild\lib\main.js:921:63)
    at buildResponseToResult (D:\viteapp\node_modules\esbuild\lib\main.js:1129:7)
    at D:\viteapp\node_modules\esbuild\lib\main.js:1236:14
    at D:\viteapp\node_modules\esbuild\lib\main.js:609:9
    at handleIncomingPacket (D:\viteapp\node_modules\esbuild\lib\main.js:706:9)
    at Socket.readFromStdout (D:\viteapp\node_modules\esbuild\lib\main.js:576:7)
    at Socket.emit (events.js:315:20)
    at Socket.EventEmitter.emit (domain.js:467:12)
npm ERR! code ELIFECYCLE
npm ERR! errno 1
npm ERR! @0.0.0 dev: `vite`
npm ERR! Exit status 1
npm ERR!
npm ERR! Failed at the @0.0.0 dev script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

npm ERR! A complete log of this run can be found in:
npm ERR!     D:\NodeJs\node_cache\_logs\2021-07-20T02_42_48_388Z-debug.log
```

就是匹配下这个目录下的文件，没有别的什么特殊含义，我们就按照要求加上就可以了，也可以通过配置文件的方式不让它提示。

我们知道在项目添加一个json文件不提示了就可以了，更多内容可以参考:[https://vuejs.github.io/vetur/](https://vuejs.github.io/vetur/)