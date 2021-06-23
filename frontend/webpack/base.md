### 初步了解webpack

在安装webpack之前，先确保已经安装了最新版本的nodejs，推荐的是长期稳定版本的最新版。如果是尝鲜、学习用的，可以安装最新版本，而不用纠结是不是长期稳定支持版。当然了，现在有了nvm这样的工具可以帮助我们很好的管理node多版本，我们可以根据需要切换不同的版本。


### 安装

建议是本地安装，而且从webpack 4+版本时，需要独立安装webpack-cli

> 是从webpack 4开始呢，还是从webpack 5开始需要单独安装webpack-cli呢？我在webpack 4的项目中，卸载了webpack-cli，对项目的运行没有什么障碍，那么webpack-cli起什么作用呢？尤其是使用vue、react脚手架搭建的项目。

这里的webpack 4+开始，需要单独安装webpack-cli,指的是从webpack5开始，需要单独安装webpack-cli，而webpack 4.*版本的，是不需要单独安装webpack-cli的。

> vue-cli可以指定webpack的版本吗？

这个暂时没有找到指定webpack版本的方法，但是我们可以升级webpack的版本。

我们知道，通过@vue/cli脚手架工具搭建的vue项目，cli工具本身集成了webpack，现在@vue/cli的最高版本是