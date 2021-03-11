### 目录结构

eggjs给我们提供了工具，可以快速初始化一个项目，行程了eggjs项目规范的目录结构，大概如下：

![目录结构](../../public/images/i5.png "目录结构")

关于目录结构的一些约定：

app/router.js：用于配置URL路由规则，关于router的详细介绍可以参考[router](router.md)

app/controller/**：用于解析用户的输入、处理后返回的相依结果，可以参考[controller](controller.md)

app/service/**：用于编写项目的业务逻辑层，可选，不是必须的，建议使用，具体可参考：[service](service.md)

app/middleware/**：用于编写中间件，可选，不是必须，具体可参考：[middleware](middleware.md)

app/public/**：存放静态资源，默认状态下静态资源放该目录下，但一般情况下用不到，因为静态资源会存放到CDN，或者我们不在egg项目中做view相关的工作

app/extend/**：用于框架的扩展，可选，具体可参考：[框架扩展](框架扩展.md)

config/config.{env}.js：配置文件，详情可参考[配置](配置.md)

config/plugin.js：用于配置需要加载的插件，可以参考[插件](插件.md)

test/**：用于单元测试，具体可参考[单元测试](单元测试.md)

app.js和agent.js：用于自定义启动时的初始化工作，可选，可参考[启动自定义](启动自定义.md),关于agent.js的作用参考[agent机制](agent.md)

app/schedule/**：用于定时任务，可选，详情可参考[定时任务](定时任务.md)，

app/view/**：用于放置模板文件，可选，由模板插件约定，可参考[模板渲染](模板渲染.md)

app/model/**：用于放置领域模型，可选，由领域类相关插件约定，如egg-sequelize