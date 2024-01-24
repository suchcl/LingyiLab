### package.json文件详解

package.json是node项目中的一个描述文件,在通过npm创建新项目或者其他的前端cli工具创建一个项目后,都会在项目的根目录下生成一个package.json文件.packages.json文件包含了项目的配置信息以及项目所需的各依赖包、项目管理中的各指令,如dev、build等.

> 因为该文件是一个json文件,所以该文件中不能添加注释.

### package.json属性详解

#### name

字符串,项目名称,如果项目要发布到npm服务器上,那么这个name属性值不能和npm服务器上已经有的包名相同,name属性是npm包区别的标识.

命名规则:

- 长度小于等于214个字符;

- 包名中不能包含有大写字母;

- 不能以点(.)或下划线(_)开头;

- 包名中不能出现一些特殊字符:因为包名可能会用在url中、文件夹名称中已经命令行参数中等,所以包名中不能出现在这些场景中被认为是非法字符的特殊字符;

```json
{
    "name": "espree"
}
```

包名可以加前缀,将包放到一个统一的命名空间下

```json
{
    "name": "@babel/core"
}
```

#### version

字符,版本号,和包名一起唯一确认一个npm包.

npm包的版本号是由node-semver模块解析的,格式一般采用{major}.{feature}.{patch}即主版本.次要版本.补丁版本模式.

- major: 大版本号

- feature: 迭代版本号

- patch: 当前迭代版本的发布次数,即当前迭代的版本号

```json
{
    "version": "3.6.23"
}
```

#### description

字符串,对当前包的一个简单的描述,以帮助用户更好、更快的了解当前的这个npm包.

```json
{
    "description": "cli tool for taro"
}
```

#### keywords

字符串数组,数组中可以只有一个项,也可以有多个项

```json
{
  "keywords": ["postcss", "css", "postcss-plugin", "pxtransform"]  
}
```
or
```json
"keywords": [ "taro" ]
```

#### scripts

scripts是一个由脚本指令组成的对象,该对象的键值是事件名称,值为事件要执行的指令

```json
{
  "scripts": {
    "build:weapp": "taro build --type weapp",
    "dev:weapp": "npm run build:weapp -- --watch"
  }
}
```

#### bin

#### dependencies

依赖管理,在生产环境需要的依赖可以安装到dependencies下进行管理.

```bash
npm install package --save # 会安装到dependencies管理项下
```

```json
"dependencies": {
    "@tarojs/binding": "workspace:*",
    "@tarojs/helper": "workspace:*",
    "@tarojs/service": "workspace:*",
    "adm-zip": "^0.4.13",
    "cli-highlight": "^2.1.11",
    "download-git-repo": "^2.0.0",
    "envinfo": "^7.8.1"
}
```

#### devDependencies

如果一些npm只需要在开发环境使用,生产环境并不需要依赖时,就可以安装到devDependencies管理项下

```bash
npm install pakcage --save-dev
```

```json
"devDependencies": {
    "@babel/core": "^7.14.5",
    "babel-jest": "^29.5.0",
    "jest": "^29.3.1",
    "jest-cli": "^29.3.1",
    "jest-environment-node": "^29.5.0",
    "ts-jest": "^29.0.5",
    "typescript": "^4.7.4"
}
```

devDependencies管理的依赖包不会被打包编译到生产环境.

#### engines

指定项目所需要的node版本的一些特殊要求,可以通过engines来指定.值为对象类型.

> 需要注意的是engines只是起到一个建议的作用(除非用户设置了engineStrict标记),并不会真正的去做代码上的限制.即使用户安装的版本不符合要求,依赖的安装包也能够正常安装.

```json
{
  "engines": {
    "node": ">=12.0.0",
    "npm": ">=6.0.0"
  }
}
```

#### engineStrict

将用户引擎设置为严格模式.除非可以非常确定的我们的模块一定不会运行在我们指定的node版本之外的node环境中,否则不要设置这个值.

现在已经没有这个配置了,npm3.0.0中移除了这个配置.在现在的项目中,可以完全忽略这个属性

```json
{
    "engineStrict": true
}
```

#### os

指定npm包可以运行的操作系统,可以以白名单和黑名单两种方式去配置,配置项是一个数组

白名单方式
```json
{
  "os": ["win32", "linux"],
}
```

黑明单方式:在名称前加!
```json
{
  "os": ["!darwin"],
}
```

#### cpu

指定npm运行的cpu.如果npm包需要运行在指定的cpu架构下,那么就可以通过cpu属性来指定.可以以白名单和黑名单两种方式去配置:

白名单方式配置:

```json
{
    "cpu": ["arm", "mips"]
}
```

黑明单方式配置:在名称前加!

```json
{
    "cpu":["!AMD64"]
}
```

#### preferGlobal

#### private

#### publishConfig

#### homepage

项目的主页,字符串.

```json
{
    "homepage": "https://github.com/NervJS/taro#readme"
}
```

#### bugs

项目提交bug的地址,值为一个对象,可以配有提交bug的url地址和反馈bug的邮箱.

该配置项也可以简单的理解为github上的issues地址

```json
{
   "bugs": {
    "url": "https://github.com/NervJS/taro/issues",
    "email": "xxxxxx@xx.com"
  }
}
```

#### license

软件的开源协议.

开源协议表达了其他人获取到代码后拥有的权利,不同的协议指定了代码可以用于什么样的场景、什么样的目的、可以做什么样的操作等等.

常见的开源协议有下面几个:

- MIT:只要用户在自己的代码副本中包含了版权声明和许可声明,就可以用这部分代码做任何的事情,而不需要负法律责任(只针对对当前代码的使用场景)

- GPL:修改项目代码的用户再次分发源码或者其他目标形式的代码时,也需要公布他自己的修改的部分

- Apache:和MIT类似,同时也包含了贡献者向用户提供专利授权相关的条款

```json
{
    "license": "MIT"
}
```

#### author

字符串或者对象,当前包的作者信息.

当是字符串时,格式可以为: 作者 <邮箱>

```json
{
    "author": "xxxxxx <xxxx@xx.com>"
}
```

#### contributors

数组,可以有多个贡献者,每个贡献者信息和author字段类似.

```json
{
    "contributors": [
        {
            "name": "xxxxxx",
            "email": "xxxxx@xx.com",
            "url": "https://www.xxxx.com" // 个人主页、站点信息
        }
    ]
}
```

#### funding

基金捐助地址.可以是一个字符串、对象、数组.

字符串
```json
{
    "funding": "http://example.com/xxxx"
}
```

对象
```json
{
    "funding": {
        "type" : "patreon",
        "url" : "https://www.xxxx.com/xxxx"
    }
}
```

数组
```json
{
    "funding": [
      {
        "type" : "individual",
        "url" : "http://example.com/xxxx"
      },
      "http://example.com/xxxx",
      {
        "type" : "patreon",
        "url" : "https://www.xxxx.com/xxxx"
      }
    ]
}
```

#### files

一个包含项目文件列表的数组.如果命中了一个文件夹,那么文件夹下的文件也会被提交(除非被其他的限制条件忽略了).

可以通过.npmignore文件来限制一些指定的文件不被提交

```json
"files": [
    "dist",
    "src",
    "index.d.ts",
    "CHANGELOG.md",
    "README.md"
]
```

#### main

字符串,项目的入口文件,浏览器环境和node环境都可正常使用.

```json
{
    "main": "./src/index.js"
}
```

#### man

项目的说明文档(手册)地址,配置项可以是字符串,也可以是一个数组.

字符串
```json
{
    "man": "../doc/index.md"
}
```

数组
```json
{
    "main": [
        "../doc/index.md",
        "https://docs.taro.zone/docs/"
    ]
}
```

#### directories

#### browser

#### repository

#### config

### package.json demo


关于package.json的详细介绍,可以参考:https://docs.npmjs.com/cli/v6/configuring-npm/package-json