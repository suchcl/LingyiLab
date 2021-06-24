### 初步了解webpack

在安装webpack之前，先确保已经安装了最新版本的nodejs，推荐的是长期稳定版本的最新版。如果是尝鲜、学习用的，可以安装最新版本，而不用纠结是不是长期稳定支持版。当然了，现在有了nvm这样的工具可以帮助我们很好的管理node多版本，我们可以根据需要切换不同的版本。


### 安装

建议是本地安装，而且从webpack 4+版本时，需要独立安装webpack-cli

> 是从webpack 4开始呢，还是从webpack 5开始需要单独安装webpack-cli呢？我在webpack 4的项目中，卸载了webpack-cli，对项目的运行没有什么障碍，那么webpack-cli起什么作用呢？尤其是使用vue、react脚手架搭建的项目。

这里的webpack 4+开始，需要单独安装webpack-cli,指的是从webpack5开始，需要单独安装webpack-cli，而webpack 4.*版本的，是不需要单独安装webpack-cli的。

> vue-cli可以指定webpack的版本吗？

这个暂时没有找到指定webpack版本的方法，但是我们可以升级webpack的版本。

我们知道，通过@vue/cli脚手架工具搭建的vue项目，cli工具本身集成了webpack，现在我本地安装的@vue/cli的最高版本是4.0.5，这个版本的cli内置的webpack版本是4.0.0。
### 默认安装webpack，不指定版本，那么会安装什么版本？

会安装一个webpack最新的稳定版本

### webpack5以下的版本，webpack和webpack-cli是集成到一起的，那么有需要命令行的地方，我不安装cli只安装webpack可以吗？

如果是在Vue、React全家桶工具构建的项目，webpack都已经内置在了项目中，如果仅仅是运行构建工具给我们内置的几个命令，如dev、build等，是没有任何问题的，是不需要单独安装webpack和webpack-cli的。但是如果有了自定义的插件，需要在命令行webpack指令，如我使用webpack-bundle-analyzer文件分析工具时，需要执行webpack指令，那么这个时候就需要单独安装webpack-cli了，当然了，如果我们项目中的webpack是webpack4以下版本的（不包括webpack4版本）也不需要单独安装webpack-cli。