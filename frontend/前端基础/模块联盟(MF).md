什么是模块联盟呢？

模块联盟(module federation)，让javascript应用之间共享代码更加简单，团队协作更加高效。

类似于服务端的微服务，Module Federation(MF)是一种支持前端应用分治的架构模式，它允许我们在多个应用或微前端应用之间共享功能级代码，这种方案的好处是：

- 减少代码重复

- 提升代码的可维护性

- 降低应用程序的整体大小

- 提高应用程序的性能

### 什么是Module Federation 2.0？

老版本的模块联盟已经支持了模块导出、模块加载、依赖共享，MF2.0除了前面的能力之外，又提供了以下的一些能力：

- Manifest：定义Module Federation元数据信息

- 动态类型提示：使用远端模块时，和引入npm包一样的体验，支持类型提示，还支持热更新

- Module Federation(MF)运行时：支持通过运行时API注册共享依赖、动态注册和加载远程模块

- 运行时插件系统：提供了一套轻量的运行时插件系统，提供各种声明周期钩子，并可修改MF配置

- Chrome Devtool：开发调试工具

#### 目前支持MF的构建工具

1. rspack：需要安装插件 @module-federation/enhanced

2. webpack：需要安装插件 @module-federation/enhanced

3. rsbuild：需要安装插件 @module-federation/rsbuild-plugin

4. vite：需要安装插件 @module-federation/vite，不支持dts、dev配置选项