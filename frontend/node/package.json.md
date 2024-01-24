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

#### engineStrict

现在已经没有这个配置了,npm3.0.0中移除了这个配置.

#### os

#### cpu

#### preferGlobal

#### private

#### publishConfig

#### homepage

#### bugs

#### license

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

#### files

#### main

#### man

#### directories

#### browser

#### repository

#### config

### package.json demo


关于package.json的详细介绍,可以参考:https://docs.npmjs.com/cli/v6/configuring-npm/package-json