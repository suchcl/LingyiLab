<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [wget](#wget)
- [安装wget](#%E5%AE%89%E8%A3%85wget)
- [使用wget](#%E4%BD%BF%E7%94%A8wget)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### wget

wget是一个非交互式的网络下载工具，广泛用于从web上下载文件。它支持Http、Https和ftp协议，并且可以递归下载整个网站(镜像网站)。wget在linux和mac上都很流行，尤其是在命令行环境中。

我们可以简单理解wget是一个迅雷，它就是一个下载工具，只不过迅雷是桌面应用，wget更多是在命令行中使用。

### 安装wget

mac上面默认没有安装wget，所以在使用之前需要手动的去安装它。

wget在mac上有多种安装方式。

1. 通过homebrew安装

```bash
brew install wget

# 验证是否安装成功
wget --version
```

2. 通过MacPorts安装

如果喜欢使用MacPorts作为mac的包管理工具，那么也可以通过它来安装wget

```bash
sudo port install wget

# 验证是否安装成功
wget --version
```

3. 使用预编译的二进制文件

最后一种方式是下载预编译的二进制文件，因为这种方式不够方便和安全，因此在能使用前两种使用包管理器的情况下，不推荐使用这种方式。

### 使用wget

wget有多种下载模式

```bash
# 下载单个文件
wget http://xxxxx.com/file.zip

# 下载并指定保存文件名
wget -0 newfilename.zip http://xxxx.com/file.zip


# 继续未完成的下载
# 如果之前有未完成的下载，那么现在可以使用-c参数继续之前的下载
wget -c http://xxxxxx.com/file.zip


# 递归整个下载站点
# 这种方式将下载整个站点到本地
wget --mirror --convert-links --adjust-extension --page-requisites --no-parent http://xxxxxxx.com/


# 限制下载速度
wget --limit-rate=200k http://xxxxxxx.com/file.zip

# 设置代理服务器
# 如果需要使用代理服务器下载文件，那么需要配置一些代理参数
wget --proxy=on --proxy-user=user --proxy-password=pass http://xxxxxx.com/file.zip   # 这种方式本人没有使用到过
```