### npm link的使用

我们在开发完的npm包，可以发布到npm服务器上，通过包npm、yarn等包管理工具安装、导入包去使用，但是这些npm包在开发过程中怎么去调试呢，每开发一点功能都发布一次，也不合适，不仅效率低下，还会印象包的稳定性。这个时候，可以通过npm link指令，将开发调试中的npm模块链接到要运行的项目中去。

### 创建链接

创建链接的前提，需要有两个项目，一个是开发中的npm包项目count，一个是要引用npm包的项目testApp。

1. 进入到npm包的项目，执行npm link

```bash
npm link
```

执行npm link指令后，npm包会根据项目中package.json的配置，被链接到全局，路径为{prefix}/lib/node_modules/<package>

> 可以通过npm config get prefix来查看prefix的具体路径

2. 进入到要引用npm包的testApp项目

进入到开发项目后，执行npm link npm包名称

```bash
cd testApp
npm link countnumber
```

这个时候，testApp项目引用的npm包，就会从本地全局路径中去找，而本地全局中的npm包，实际上是指向了我们的开发目录的.

```bash
[xxx testApp]$ npm link countnumber
/Users/xxx/Documents/testApp/node_modules/countnumber -> /Users/xxx/.nvm/versions/node/v14.16.0/lib/node_modules/countnumber -> /Users/xxx/Documents/count
```

所以，本地项目testApp，实际上引用的，就是开发中的npm包项目。

这时在npm项目中开发的新功能，就都可以正常的使用了，也不影响线上的稳定版本，非常实用。

> 在实际中，可以使用npm link packagename来创建链接，也可以通过npm link package_path的方式来创建链接

```bash
npm link ../count
```

其实这种方式比前面的方式更加简洁、遍历，如果npm包项目和应用项目的目录组织的优秀的话，可以减少脏数据、脏文件的产生。

3. 移除链接 npm unlink

npm包的功能开发、测试都已经完成，可以发布到线上了，我们正常发布即可，新的版本发布后我们就需要移除项目中引用的开发版本的npm包了，可以执行npm unlink packageName

```bash
npm unlink packagename
```

npm unlink countnumber

在执行了npm unlink packagename后，本地的引用的npm包会被移除掉，之前引用的线上的稳定版本的依赖也会被清理掉，其实就相当于执行了一个npm uninstall指令。在执行了unlink指令后，需要重新install下npm包。

### 可行的link方式

除了npm link可以提供链接的方式之外，其他常用的包管理工具如pnpm、yarn也都提供了类似的能力；

```bash
npm link packagename

npm link package_path

npm install --no-save package_path # 通过路径安装，不会在package.json中留下安装路径

npx link package_path # 比较推荐的一种方式，也被认为是一种更安全、更强壮的link版本，https://www.yarnpkg.cn/package/link

pnpm link # https://www.pnpm.cn/cli/link
```

### npm link的弊端

有多种npm包link的方式，但是在使用npm link的是可能会存在一些弊端，具体可参考：https://hirok.io/posts/avoid-npm-link