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
