### nodemon

nodemon是一个用来监视node应用程序的应用，能够监视node服务由于文件的修改而自动重启服务，非常适合在开发环境。

**使用方式**

1. 全局安装

```bash
# npm安装
npm install nodemon -g

# yarn安装
yarn global add nodemon
```

2. 启动服务

```bash
nodemon bin/www # bin/www为express应用中默认的启动脚本，本质上是nodemon 启动应用脚本
```

如果我们自己单独测试的时候写了一个服务如文件名为app.js，则启动方式为：

```bash
nodemon app.js
```