### Node Sass does not yet support your current environment: OS X 64-bit with Unsupported runtime (93)

一个项目中使用到了node-sass，在项目启动过程中报了异常，主要信息如下：

```bash
Error: Node Sass does not yet support your current environment: OS X 64-bit with Unsupported runtime (93)
For more information on which environments are supported please see:
https://github.com/sass/node-sass/releases/tag/v4.14.1
// ……
```

主要就是说node-sass不支持当前运行时环境，查询了一些资料，说是node-sass的版本原因，降低下版本即可，降低到4.x版本即可。

### 解决方案

1. 卸载、安装4.x版本的node-sass

如果有安装了高版本的node-sass则卸载，然后重新安装4.x版本的，或者不用卸载直接安装也可以

```bash
npm install node-sass$4.14.1
```

2. 解决gyp: No Xcode or CLT version detected问题

大多数情况下出现了node-sass的问题后，也都伴随着该问题。出现该问题后，重新安装xcode开发工具即可

### 重新安装xcode开发工具

- 查看command-line tools的安装路径

```bash
xcode-select --print-path
```

一般情况下，该路径是/Library/Developer/CommandLineTools

- 移除掉已经安装的xcode开发工具

```bash
sudo rm -r -f /Library/Developer/CommandLineTools
```

在移除后，mac就会提示进行安装开发者工具，根据提示进行安装就可以了。