### node-sass是什么,有什么作用?

node-sass是一个库,它将node.js绑定到LibSass.它允许用户以令人难以执行的速度将.scss文件本地编译为css,并通过连接中间件自动编译.

**LibSass是什么?**

LibSass是用C/C++实现的Sass引擎.其核心特点是简单、快速、易于集成.

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

node-sass需要对应到某个指定的node版本吗?