<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1.pnpm简介](#1pnpm%E7%AE%80%E4%BB%8B)
- [2.pnpm特点](#2pnpm%E7%89%B9%E7%82%B9)
- [3.pnpm安装](#3pnpm%E5%AE%89%E8%A3%85)
- [4.pnpm升级](#4pnpm%E5%8D%87%E7%BA%A7)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 1.pnpm简介

> 英文官网：https://pnpm.io，中文网站：https://www.pnpm.cn

pnpm,全文为performant npm,意为高性能的npm。

### 2.pnpm特点

1. 快速：pnpm是同类包管理工具速度的2倍

2. 高效：node_modules中的所有文件均链接自单一存储位置
3. 支持单体仓库：pnpm内置了对单个源码仓库中包含多个软件包的支持
4. 权限严格：pnpm创建的node_modules默认并非扁平结构，因此代码无法对任意软件包进行访问

> 节省磁盘空间，提升安装速度

当我们使用npm或者yarn作为我们项目的包管理工具时，如果我们有100个项目，那么就需要在硬盘上保存100份相同依赖包的副本，但是如果使用pnpm就不一样了，因为使用pnpm，依赖包将被存放在一个统一的位置，因此：

1. 如果我们不同的项目对同一依赖包使用不同的版本，则仅有不同的版本的文件会被存储起来。如果某个依赖包有新的版本发布，这个新的版本只有1个文件有更新变动，那么在执行pnpm update的时候，只需要也是只会添加一个新的文件到硬盘中，而不会因为一个文件的修改而保存当前依赖包的所有文件。
2. 所有的文件都会保存在硬盘上的统一的位置。当安装软件包时，其包含的所有文件都会硬链接此位置，而不会占用额外的硬盘空间。这可以让不同的项目之间方便的共享相同的依赖包。

这样从最终的结果来看，我们节省了大量的硬盘空间，并且安装的速度也大大的提升了。

### 3.pnpm安装

1. 通过脚本安装

   在POSIX类的系统上，在没有安装nodejs的情况下，也可以通过curl或者wget来安装pnpm

   ```bash
   # 通过curl来安装pnpm
   curl -fsSL https://get.pnpm.io/install.sh | PNPM_VERSION=7.0.0-rc.2 sh -
   # 通过wget来安装pnpm
   wget -qO- https://get.pnpm.io/install.sh | PNPM_VERSION=7.0.0-rc.2 sh -
   # windows上可以通过powershell来安装pnpm
   $env:PNPM_VERSION='7.0.0-rc.2' ; iwr https://get.pnpm.io/install.ps1 -useb | iex
   ```

2. 使用corepack安装

   nodejs从16.13版本开始提供了管理Corepack来管理包管理器。

   首先需要启用corepack

   ```bash
   corepack enable # 启用corepackd
   ```

   启用了corepack后自动安装pnpm，然后自动安装的pnpm有可能不是pnpm的最新的版本，然后通过下面指令去更新pnpm的版本：

   ```bash
   corepack prepare pnpm@7.0.0 --activate
   ```

   [查看npm包的版本信息,可以参考](../node/npm.md)

3. 使用npm安装

   ```bash
   npm install pnpm -g
   ```

4. 使用scoop安装

   ```bash
   scoop install nodejs-lts pnpm
   ```

   > scoop可以简单理解为包管理工具，类似Mac下的HomeBrew，详细信息可参考：http://xerrors.fun/scoop-list/#_1-scoop-%E4%BB%8B%E7%BB%8D

5. mac上可以通过homebrew安装

   ```bash
   brew install pnpm
   ```

### 4.pnpm升级

一旦pnpm安装完成后，就不需要其他的包管理工具了，就可以使用pnpm自己来管理自己了

```bash
pnpm add -g pnpm # 升级
```

### 5.卸载pnpm

卸载pnpm之前，首先需要删除通过pnpm全局安装的依赖包。

查看通过pnpm安装的全局依赖包

```bash
pnpm ls -g # 查看通过pnpm安装的全局依赖包
```

**删除通过pnpm安装的全局依赖包**

有两种方式删除通过pnpm安装的全局依赖包

1. pnpm rm -g pck：逐个手动删除通过pnpm安装的全局依赖包
2. pnpm root -g去找到pnpm的全局目录，并手动的删除它

> pnpm,依赖nodejs版本，nodejs版本不能低于14.19.0.所以在安装pnpm的时候，需要先确认下nodejs的版本。

