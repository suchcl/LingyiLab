### 快速上手Typescript

1. 安装Typescript

安装Typescript一般情况下有两种方式：

* 使用npm安装
* 使用VSCode的Typescript插件

我习惯使用npm

```bash
npm install typescript -g
```

> 注意是全局安装typescript，这里安装的是Typescript的编译器

编写ts代码：

```typescript
function greeter(person: string) {
    return "Hello," + person;
}

let user: string = "Jane User";
document.body.innerHTML = greeter(user);
```

我们把这段代码保存到一个名为index.ts的文件中，然后使用tsc编译器编译，之后会生成一个index.js的js文件，文件内容如下：

```javascript
function greeter(person) {
    return "Hello," + person;
}
var user = "Jane User";
document.body.innerHTML = greeter(user);
```

我们可以看到，ts源文件和编译后的js文件，变化是去掉了类型控制，其他的没有什么变化。

另外，在Typescript中，有了接口、class的概念，再配合类型注解，可以让我们在代码的编写中增加很多乐趣。

### Typesript的应用

可以使用node的包管理工具npm、cnpm、yarn，都可以使用。

使用npm需要安装了nodejs，使用cnpm，需要先安装cnpm，使用yarn，也需要先安装了yarn管理工具。

1. 安装

```bash
npm install typescript -g
cnpm install typescript -g
yarn add typescript global
```

安装cnpm

```bash
npm install cnpm --registry=https://registry.npm.taobao.org -g
```

检测typescript是否安装成功：通过查看typescript版本的方式去验证

```bash
PS C:\Users\xxx> tsc -v
Version 4.2.3 # 正常的打印出来了typescript的版本号，说明typescript已经安装成功
```

yarn的安装方式：

```bash
npm install yarn -g
```

> typescript安装完成后，需要重新打开一个终端去验证typescript的安装状态。