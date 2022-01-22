### 1. 简单介绍

### 2. 安装

### 3. 常用指令

**brew本身的管理、配置**

```bash
cd "$(brew --repo)"  # 跳转到homebrew的安装目录
git remote set-url origin https://mirrors.aliyun.com/homebrew/brew.git # 更换brew.git

cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.aliyun.com/homebrew/homebrew-core.git # 更换homebrew-core.git

brew update # brew更新

git config # 查看homebrew的基本配置
```

**brew安装管理应用**

```bash
# app 标识应用名称
brew search app # 搜索app
brew install app # 安装app
brew uninstall app # 卸载app
brew update app # 更新app，如果权限不足，则sudo brew update
brew list # 查看通过brew安装的应用列表
brew info app # 查看通过brew安装的app应用的信息
```

### 4. 常见问题

1. Mac上Homebrew安装应用非常慢

Homebrew时mac上非常好用的一个包管理工具，但由于网络环境原因，可能在使用Homebrew安装应用的时候会非常慢，甚至有的时候都下载不了，网络链接不成功。

其实，Hombrew主要分为2部分：git repo(位于github上)和二进制bottles，这2个网站在国内的网络环境访问起来都比较慢，那么我们在使用Homebrew的时候切换下它的源就可以了。

国内有阿里云的Homebrew镜像源可以加速。

在使用brew命令安装应用的时候，一般情况下会有3个仓库地址会影响到我们的下载速度，分别是：

brew.git

homebrew-core.git

homebrew-bottles

那么就来更换这些仓库吧。

**更换brew.git**

```bash
cd "$(brew --repo)" #跳转到homebrew的安装目录
git remote set-url origin https://mirrors.aliyun.com/homebrew/brew.git  #更换为阿里云的加速镜像
```

**更换homebrew-core.git**

```bash
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core" # 切换目录
git remote set-url origin https://mirrors.aliyun.com/homebrew/homebrew-core.git # 镜像更换
```

**通过brew config检查镜像是否更换成功**

```bash
xxx@xxxx homebrew % brew config
HOMEBREW_VERSION: 3.3.11
ORIGIN: https://mirrors.aliyun.com/homebrew/brew.git
HEAD: 537036ab3627b65d71dfa920b98d43774f861dec
Last commit: 6 days ago
Core tap ORIGIN: https://mirrors.aliyun.com/homebrew/homebrew-core.git
Core tap HEAD: ee88205b7584934f814156b43f4205901729a83d
Core tap last commit: 2 hours ago
Core tap branch: master
HOMEBREW_PREFIX: /opt/homebrew
HOMEBREW_CASK_OPTS: []
HOMEBREW_CORE_GIT_REMOTE: https://github.com/Homebrew/homebrew-core
HOMEBREW_MAKE_JOBS: 8
Homebrew Ruby: 2.6.8 => /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/bin/ruby
CPU: octa-core 64-bit arm_firestorm_icestorm
Clang: 13.0.0 build 1300
Git: 2.32.0 => /Library/Developer/CommandLineTools/usr/bin/git
Curl: 7.77.0 => /usr/bin/curl
macOS: 12.0.1-arm64
CLT: 13.2.0.0.1.1638488800
Xcode: N/A
Rosetta 2: false
```

从配置信息中看到，前面的2个源已经切换成功

**更换homebrew-bottles**

更换homebrew-bottles，和当前使用的shell有关系，因为在不同的shell下切换的方式稍微有所不同

```bash
xxx@xxxxx xxxx % echo $SHELL
/bin/zsh
```

一般情况下，会是/bin/zsh或者/bin/bash，在修改的时候，根据不同的shell需要修改不同的配置文件。

/bin/zsh

```bash
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.aliyun.com/homebrew/homebrew-bottles' >> ~/.zshrc  # 修改环境变量
source ~/.zshrc  # 快速生效
```

/bin/bash

```bash
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.aliyun.com/homebrew/homebrew-bottles' >> ~/.bash_profile
source ~/.bash_profile
```

**homebrew下载源的恢复**

在特殊的网络环境下，这样的配置就可以了，但也有极端的情况，需要恢复下默认的下载源

```bash
# 重置brew.git:
cd "$(brew --repo)"
git remote set-url origin https://github.com/Homebrew/brew.git

# 重置homebrew-core.git:
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://github.com/Homebrew/homebrew-core.git
```

下载源恢复之后，还需要删除Homebrew的环境变量，就是上面通过echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.aliyun.com/homebrew/homebrew-bottles' >> ~/.zshrc 或者echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.aliyun.com/homebrew/homebrew-bottles' >> ~/.bash_profile写入的这部分，直接删除就可以了，删除后重载下配置文件

```bash
source ~/.zshrc
# 或
source ~/.bash_profile
```