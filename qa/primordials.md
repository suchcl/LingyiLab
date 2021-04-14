### ReferenceError: primordials is not defined

项目中使用了gulp作为自动化工具来打包，由于是很久之前的一个项目了，今天在改动项目需要打包时，报了异常：
``` bash
PS D:\projefct\xx项目> gulp html
ReferenceError: primordials is not defined
    at fs.js:45:5
    at req_ (D:\project\static_www\m\node_modules\natives\index.js:143:24)
    at Object.req [as require] (D:\project\static_www\m\node_modules\natives\index.js:55:10)
    at Object.<anonymous> (D:\project\static_www\m\node_modules\graceful-fs\fs.js:1:37)
    at Module._compile (internal/modules/cjs/loader.js:1063:30)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:1092:10)
    at Module.load (internal/modules/cjs/loader.js:928:32)
    at Function.Module._load (internal/modules/cjs/loader.js:769:14)
    at Module.require (internal/modules/cjs/loader.js:952:19)
    at require (internal/modules/cjs/helpers.js:88:18)
```

之前一直是这么操作的，从来没有出现过这样的问题，今天突然出现了整个问题。

突然想起来，之前使用的是Mac，一直在Mac平台下工作，最近更换了设备，从Mac更换成了windows，所有的环境都重新配置，我想了下可能问题出现在了这里。最终经过试验，原来是node和gulp版本冲突的问题，我出问题时的node和gulp的版本分别是：

```bash
PS D:\project\static_www\m> node -v
v14.15.4

PS D:\project\static_www\m> npm ls gulp
m.comjia.com@1.0.0 D:\project\static_www\m
`-- gulp@3.9.1
```

经过多次测试，发现只要是nodejs的版本低于12就可以了，至于gulp需要什么版本，暂时不确定，我机器上的gulp版本如下：

```bash
PS D:\project\static_www\m> gulp -v
CLI version: 2.3.0
Local version: 3.9.1
```

>> 现在不能确定究竟nodejs和gulp需要什么样的版本依赖，但是能确定的是有依赖关系，如果在项目过程中如果发生一些怪异问题的时候，可以尝试更改nodejs版本来解决一下。
>>> 为什么是修改nodejs版本而不是修改gulp？因为node.js有版本管理工具nvm和n，而gulp没有，就是为了减少工作量而已，没那么多道道，哈！

#### 总结一下：

针对原文问题总结一下，虽然说了很多，文中虽然含蓄的给了解决方案，但不够明确，这里就明确一下吧，两种解决方案：

1. 降级node

> 比较推荐使用nvm来管理node，简单、省心，降到12版本以下

```bash
PS D:\project\static_www\m> nvm ls

    14.15.4
    12.19.0
  * 10.20.0 (Currently using 64-bit executable)
    10.16.0
```
我修改之后使用这个版本就可以了。

2. 升级gulp
升级gulp也可以，但是不建议这么做。因为不同的版本可能会有变化，对于应用部分需要作出修改，尤其是gulp4开始有了语法的修改，成本高了。
