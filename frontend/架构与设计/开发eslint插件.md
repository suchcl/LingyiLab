### 开发工具

yeoman、generator-eslint，全局安装即可。

环境要求：
```js
Node.js ^14.17.0 || ^16.0.0 || >= 18.0.0
```

环境安装：

```bash
npm install yo generator-eslint -g
```

创建eslint插件项目

```bash
# 创建目录
mkdir eslint-plugin-et
# 初始化项目
yo eslint:plugin
```

创建新的eslint规则

```bash
yo eslint:rule
```