## package.json

现在的前端工程中，最好的管理本地包的方式，就是创建一个package.json文件。

可参考文档：[https://www.npmjs.cn/getting-started/using-a-package.json/](https://www.npmjs.cn/getting-started/using-a-package.json/)

### 简单认识package.json

1. 包含了项目的所有的依赖里列表

2. 我们可以通过package.json指定项目依赖的包的版本

3. 让我们的工程可复用程度高，可以让更多的开发者更快的分享我们的项目

### package.json文件要求

1. 文件名

    文件名中不能有空格，全部为小写，可以有中划线和下划线

2. 版本号

    版本号格式：x.x.x

    具体的语义化的版本规则，可参考: [https://docs.npmjs.com/about-semantic-versioning](https://docs.npmjs.com/about-semantic-versioning)

3. 创建一个package.json文件

    可以通过cli创建两种形式的package.json文件：1种是自定义package.json文件中内容的package.json，另1种创建含有默认内容的pacakge.json：

    * 创建自定义内容的package.json

    ```bash
    npm init 创建自定义内容的package.json，内容需要我们根据提示填充
    ```

    * 创建包含默认内容的package.json

    ```bash
    npm init --yes  通过加参数--yes的方式创建一个包含默认内容的package.json
    ```

    创建的默认的package.json文件的字段说明：

    * name：package.json文件所在的目录的目录名
    * version：默认是1.0.0
    * description:默认会读取和package.json同目录下的readme.md文件中的第一行内容，或者是空字符串""
    * main: 默认是index.js
    * scripts：默认会创建一个空的test脚本
    * keywords：空值
    * author：空值
    * license：MIT（文档上写的是ISC，我本地测试是MIT，各位看客注意下这个地方）

除了上面常用的一些属性之外，还有其他的一些属性，部分集成了webpack，部分不常用，不再一一介绍了。

