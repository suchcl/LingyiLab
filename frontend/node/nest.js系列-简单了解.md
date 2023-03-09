参考链接:https://juejin.cn/post/7195889798094962749

### 1. 快速创建一个nest.js项目

```bash
# 全局安装nestjs脚手架
npm install @nestjs/cli -g

# 使用脚手架创建nest.js项目
nest new project_name
```

创建新项目过程中，可以选择使用npm、yarn或者pnpm包管理工具，可以根据自己的喜好选择使用

#### 1.1 nest项目热启动

初始化完成了nest的项目之后，发现一个问题，就是nest不能支持热更新，当有什么改动之后都需要手动重启服务，很不便利，也可以给nest添加一个热启动的能力。

以前在学习express的时候使用过nodemon，可以用来管理服务启动，于是还是尝试着使用nodemon来管理nest服务。

1. 全局安装nodemon:可以通过yarn或者npm安装

```bash
npm install nodemon -g
```

2. 配置nodemon

项目根目录下创建nodemon.json文件

```json
{
    "restartable": "rs",
    "ignore": [
      ".git",
      ".svn",
      "logs",
      "pem",
      "node_modules/**/node_modules",
      "src/**/*.spec.ts"
    ],
    "verbose": true,
    "execMap": {
      "js": "node server/index.js"
    },
    "watch": [
      "src"
    ],
    "env": {
      "NODE_ENV": "development"
    },
    "ext": "ts js json",
    "exec": "ts-node -r tsconfig-paths/register src/main.ts"
  }
```

3. 启动服务

```bash
nodemon --exec
```

然后项目中有改动了服务就可以自动重新启动了。

不过这种方式不好的服务重启速度比较慢，文件有变动之后重启时间大概需要5秒以上的时间，有点忍受不了。不过项目中不用，也没有深究，有朋友研究了可以共同讨论学习。