esno是一个基于esbuild的TS/ESNext的运行时环境.该库会针对不同的模块化标准,采用不同的编译方案.

**esno的使用方式**

因为esno是一个命令行工具,提供的是一个运行时环境,所以esno可以全局安装,也可以局部安装.

```bash
npm install esno -g # 全局安装

npm install esno # 局部安装
```

全局安装后,可以直接使用

```bash
esno index.ts
```

局部安装的esno,大多数场景下是配置到scritps脚本中,通过npm等包管理器的方式,在项目去使用

```json
{
    "scripts": {
        "start": "esno index.ts"
    },
	"dependencies": {
		"esno": "^4.8.0"
	}
}
```
