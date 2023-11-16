### 创建并发布npm包

1. 创建项目

```bash
# 创建项目目录
mkdir npmproject

# 进入到项目，并初始化package.json
cd npmproject
npm init
# 根据提示，分别输入项目名称、作者等一些基本信息就可以了，下面是一个简易demo
```

```json
{
  "name": "countnumber",
  "version": "1.0.2",
  "description": "计算器",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "suchcl",
  "license": "ISC"
}
```

> 在通过npm init创建项目的时候，注意name的值，不能是在服务器上已经有的名字，这个字段名需要在npm服务器上唯一。

2. 开发项目代码

项目创建完成之后，就可以根据目标写功能了.我们这里主要是描述创建npm包并发包到npm服务器，项目本身不是重点，所以可以来看一个简单demo。

项目目录：

```markdown
├── README.md
├── index.js
├── package.json
└── src
    └── math.js
```

主要的功能，最优秀的实践是通过index.js导出，当然了，也可以不通过index.js，如demo，也可以直接通过src/math.js导出，那么在引用的时候，就需要写全路径了，如const math = require("countnumber/src/math");如果是通过index.js导出的，则可以直接是:const math = require('countnumber');就可以了。

src/math.js功能代码：

```js
const add = (a, b) => {
  return a + b;
};

const subtract = (a, b) => a - b;

module.exports = {
  add,
  subtract,
};
```

index.js

```js
// index.js中的内容，也可以省略，直接将math.js中的功能代码直接写到index.js中
const math = require("./src/math");

module.exports = math;
```

3. 创建npm账号

下面的操作是在命令行操作

```bash
npm adduser
```

剩下的按照提示操作就行了。需要注意的是秘密需要是10位以上，且不能是被筛查出来被泄漏过。邮箱写真实的邮箱，因为需要接收验证码。

根据提示注册完账号之后，默认就已经登录了。可以使用npm whoami指令来查询

```bash
npm whoami

[xxxxxx count]$ npm whoami
suchcl
```

有了这个提示，就表明name位suchcl的用户已经登录了。

如果没有登录，可以使用npm login指令来登录

```bash
npm login
```
然后根据提示输入用户名和密码就可以了

4. 发布npm包

```bash
npm publish
```

在项目的根目录下执行npm publish发包。