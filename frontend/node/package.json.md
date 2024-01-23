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

#### version

#### description

#### keywords

#### scripts

#### bin

#### dependencies

#### devDependencies

#### peerDependencies

#### bundledDependencies

#### optionalDependencies

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

#### contributors

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