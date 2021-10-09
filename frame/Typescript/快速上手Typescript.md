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

**安装**

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

浏览器默认是不能执行typescript代码的。

**编译**

我认为Ts比js具备优势的地方，就是Ts是强类型的语言，需要经过编译，这样就可以发现代码中一些语言层面的漏洞。

默认情况下，我们只安装了typescript，它需要手动的去执行tsc index.ts（文件名）的方式去编译文件

```bash
tsc index.ts # 会在当前目录生成一个index.js文件。
```

这种手动编译的方式，调式或者学习某个技术点的时候，比较合适，但是如果到了项目中，就有点不高效了，所以我们需要探索自动编译的方式。我希望我一边写代码一边去编译ts代码。

可以通过配置ts的配置文件、编辑器的方式，实现实时编译，下面以vscode为例，来逐步了解配置方法。

1. 创建ts的配置文件tsconfig.json

```bash
tsc --init
```
2. 对ts的配置文件进行相应的配置就可以了

```json
    "outDir": "./js",
    "rootDir": "./ts",   
```

配置好这两项就可以了，可以找到原ts代码，可以指定目标输出目录

3. 在项目的根目录下执行tsc进行编译

```bash
PS D:\ts> tsc
PS D:\ts> 
```

我测试执行完命令后没有任何提示，没有提示就说明已经正常编译了，如果有信息，则说明是出现了异常的信息提示，可以看下示例：

![ts编译有异常时信息提示](../../public/images/i102.png)

4. 设置自动实时编译

虽然前面我们已经配置了ts的配置文件tsconfig.json，只通过tsc指令就可以进行文件的编译了，不需要tsc指定具体的文件了，但是我们还可以进一步让编辑器给我们实时的自动编译，以vscode为例：

依次选择：终端-运行任务-tsc监视tsconfig.json，可看下图：

![设置vscode自动实时自动编译ts](../../public/images/i103.png)

![设置vscode自动实时自动编译ts](../../public/images/i104.png)

每次当我们修改了ts源码后，在进行保存动作时编辑器就会自动执行tsc指令，进行ts文件的编译。

> 如果编辑器关闭了，那么编辑器再次打开时需要重新进行第4步动作。