### 老项目升级到react19

参考链接:[升级到React19](https://react.dev/blog/2024/04/25/react-19-upgrade-guide)

React19之前发布过一个react18.3的版本，这个react18.3在功能上和react18.2相同，但是添加了一些可能会被弃用的API的警告，以及React19可能会带来的一些更改的内容。

所以如果是老版本React在升级react19的时候，建议先升级到18.3，然后再从18.3升级到19.

### 升级到React19的步骤

#### 安装

安装新版本的React和React DOM

```bash
npm install --save-exact react@^19.0.0 react-dom@^19.0.0
# or
yarn add --exact react@^19.0.0 react-dom@^19.0.0
```

安装Typescript支持

```bash
npm install --save-exact @types/react@^19.0.0 @types/react-dom@^19.0.0
# or
yarn add --exact @types/react@^19.0.0 @types/react-dom@^19.0.0
```

> 安装之前，可以先指定一下npm镜像的源。

默认情况下，npm使用的是https://registry.npmjs.org/这个源，有的时候国内的网络环境对这个镜像可能会很慢，导致依赖安装失败。淘宝技术团队搭建了一个镜像https://npmmirror.com/，网络环境相对较好，平常可以使用这个镜像源。

**淘宝镜像源**

网站地址：https://npmmirror.com/

这是一个完整都npmjs.com镜像，这是一个npmjs.com的只读版本，大多数情况下是与官方保持同步的，可以放心使用。

可以通过以下方式指定镜像源

1. 使用npm配置更改镜像源

```bash
npm config set registry https://registry.npmmirror.com/
```

2. 

#### 修改代码

#### 重大变更

#### 新的弃用

#### 显著变化

#### Typescript变更