### 运行环境区分

在开发项目的时候，我们经常需要区分不同的环境，如测试环境、沙盒环境（也叫预生产环境）、生产环境，然后针对不同的环境需要做一些特性化处理，如在测试环境（往往和开发环境需求相同）需要连接测试环境的数据库、沙盒环境需要连接沙盒的库、生产环境需要连接生产环境库，这个时候，我们就需要有一个方法来区分当前代码运行在哪个环境上面。

### 不做环境区分

虽然实际上有上面提到的场景需求，但是我现在不知道怎么做环境区分，在做环境部署的时候改下代码，简单明了，没有技术成本，也可以解决我们的环境需求的问题。但是同一个项目一般情况下都会有多人协作负责，有的时候这个人改了，有的时候那个人也改了，那么就都改了，还有一个可能是某次所有的团队同学都没有改，总之这种方式弊大于利，除非是一个人的团队，一个人负责项目，还好一点。

### 通过服务器环境变量来判断运行环境

在项目代码需要运行的服务器上，都添加一个同名的环境变量，我现在是在测试egg项目，比如我在服务器上添加一个egg_env的环境变量，表示我当前的环境，比如在本地开发环境设置值为dev，测试环境设置变量值为test，沙盒环境设置值为sandobx，生产环境值设置为prod，然后在项目代码中通过process.env.egg_env来判断当前环境，这种方式简单、明了，也不会有遗忘或者都改，以及由于粗心导致改错的问题。

```javascript
    /**
     * 获取运行环境
     * @returns env String
     */
    async getEnv(){
        let env = process.env.egg_env;
        return env;
    }
```

这种方式，就是需要在开始的时候，需要找运维同学帮忙分别在不同环境的服务器上配置一下环境变量，一劳永逸，推荐去做的。

### 在config/env文件指定

我们知道在egg项目中，config是一个内置对象，我们可以直接拿到config下的env文件中的内容。当然了，这个文件不能通过手动去管理，还是要借助构建工具，或者代码部署工具去自动化管理。

这个文件管理，可以在部署代码的时候，也可以在启动服务的时候，需要会写点shell，基本上很容易搞定