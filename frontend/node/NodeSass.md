### Node Sass does not yet support your current environment: OS X 64-bit with Unsupported runtime (93)

一个项目中使用到了node-sass，在项目启动过程中报了异常，主要信息如下：

```bash
Error: Node Sass does not yet support your current environment: OS X 64-bit with Unsupported runtime (93)
For more information on which environments are supported please see:
https://github.com/sass/node-sass/releases/tag/v4.14.1
// ……
```

主要就是说node-sass不支持当前运行时环境，查询了一些资料，说是node-sass的版本原因，降低下版本即可，降低到4.x版本即可。