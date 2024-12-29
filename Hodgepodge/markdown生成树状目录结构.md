### markdown生成树状目录结构

在写文档的时候，很多场景会需要描绘出来一些树状的目录结构，但是markdown中又没有找到类似的语法，怎么把这个树状的目录结构给描述出来。

其实有一个npm包，可以帮我们生成这个树状的目录结构 ----- treer。

### treer：一个树状目录结构生成工具。

参考文档：[https://www.npmjs.com/package/treer](https://www.npmjs.com/package/treer)

```bash
# 安装
npm install treer -g
```

目录生成方式：

```bash
treer -e ./readme.md -i node_modules
```

这已经可以满足大部分的场景了，就是在当前执行命令的目录下的目录结构，输出打印到readme.md文件中，目录结构排除掉当前目录下的node_modules目录。

如果需要排除掉多个目录不生成目录文档，则-i参数需要给匹配符：

```bash
treer -e ./readme.md -i "/node_modules|.git/"
```

这样可以将当前目录中的node_modules和.git目录排除掉，可以生成如下的目录：

```
D:\WebStudy\reactapp
├─package.json
├─README.md
├─yarn.lock
├─src
|  ├─App.css
|  ├─App.js
|  ├─App.test.js
|  ├─index.css
|  ├─index.js
|  ├─logo.svg
|  ├─reportWebVitals.js
|  └setupTests.js
├─public
|   ├─favicon.ico
|   ├─index.html
|   ├─logo192.png
|   ├─logo512.png
|   ├─manifest.json
|   └robots.txt
```

这样，markdown生成的树状目录结构就完美的生成了。

treer模式导出的目录为当前的目录，还可以通过-d参数指定目录

```bash
treer -d app -e ./tree.md -i "/node_modules|.git/"
```

效果

```markdown
app
├─router.js
├─view
|  └home.html
├─service
|    └user.js
├─public
├─controller
|     ├─home.js
|     └user.js
```