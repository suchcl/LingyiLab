### 项目创建

**初始化项目**

```bash
npm init # 根据提示信息填写项目基本信息即可
```

**依赖**

ts-node:

@types/node:

typescript:

express:

nodemon:

dotenv:

@types/express:

**安装依赖**

```bash
npm install typescript ts-node @types/node @types/express --dev

npm install express dotenv
```

**ts配置文件初始化**

```bash
npx tsc --init # 生成tsconfig.json文件
```

使用指令初始化的tsconfig.json文件的配置属性比较多,但大部分都是被注释掉了,可以根据需要修改编译配置.

**package.json指令配置**

```json
  "scripts": {
    "build": "rimraf ./dist && tsc --sourceMap false",
    "dev": "nodemon --watch src --exec ts-node src/index.ts",
    "tsc": "tsc --watch"
  }
```