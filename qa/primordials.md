### ReferenceError: primordials is not defined

项目中使用了gulp作为自动化工具来打包，由于是很久之前的一个项目了，今天在改动项目需要打包时，报了异常：
``` bash
PS D:\projefct\xx项目> gulp html
ReferenceError: primordials is not defined
    at fs.js:45:5
    at req_ (D:\juliveproject\static_www\m\node_modules\natives\index.js:143:24)
    at Object.req [as require] (D:\juliveproject\static_www\m\node_modules\natives\index.js:55:10)
    at Object.<anonymous> (D:\juliveproject\static_www\m\node_modules\graceful-fs\fs.js:1:37)
    at Module._compile (internal/modules/cjs/loader.js:1063:30)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:1092:10)
    at Module.load (internal/modules/cjs/loader.js:928:32)
    at Function.Module._load (internal/modules/cjs/loader.js:769:14)
    at Module.require (internal/modules/cjs/loader.js:952:19)
    at require (internal/modules/cjs/helpers.js:88:18)
```