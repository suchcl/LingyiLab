### node-sass是什么,有什么作用?

node-sass是一个库,它将node.js绑定到LibSass.它允许用户以令人难以执行的速度将.scss文件本地编译为css,并通过连接中间件自动编译.

**LibSass是什么?**

LibSass是用C/C++实现的Sass引擎.其核心特点是简单、快速、易于集成.LibSass的C实现,其目的是为了方便、简单的与多种编程语言集成.

随着时间的推移和技术的发展,LibSass在很多方面已经落后于DartSass了

**LibSass项目已经被弃用,新项目中推荐使用DartSass**

项目中怎么选择使用DartSass引擎呢?

关于DartSass的介绍可以参考:https://sass.bootcss.com/dart-sass.html

<span color="red">关于DartSass的应用方式,还没有研究明白,后续补充</span>

LibSass只是一个工具库,如果需要在本地运行(即编译sass代码),我们就需要安装一个LibSass的封装.当前,已经有很多针对LibSass的封装了:

- Sass C:用c语言开发的封装

- sass.cr:针对Crystal编程语言的LibSass封装

- go-libsass:是一个go语言实现的LibSass封装,是最活跃的go语言实现的LibSass封装

LibSass的更多介绍,可参考:https://sass.bootcss.com/libsass

**安装node-sass**

由于国内网络环境不太稳定,安装node-sass的时候成功率不是很高.

网络环境问题,可以通过指定npm源的方式来解决:

```bash
npm install -g cnpm --registry=https://registry.npm.taobao.org
cnpm install --save-dev node-sass
```

### node-sass和平台有关系吗?

node-sass需要和指定的node版本相对应,否则在安装或者编译的时候会出现各种问题.即便是同一个node-sass版本,在不同的平台上也可能会对应不同的node版本,所以在安装node-sass的时候,可以关注下node-sass和node的对应关系.具体可参考:https://github.com/sass/node-sass/releases