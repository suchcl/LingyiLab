### nvm的安装方法

有两种安装方法：

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash

# 或者

wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```

两种安装方法中的v0.39.1表示当前安装的nvm的版本，可以根据实际需要进行修改。

参考文档：https://github.com/nvm-sh/nvm

### nvm的安装目录

```bash
/Users/xxx/.nvm
```

当前用户目录的.nvm目录下

### 基本使用方法

nvm --version  查看nvm版本

nvm install version, 如 nvm install v15.0.0  安装v15.0.0版本的nodejs

nvm uninstal version  卸载指定版本的nodejs

nvm use version 切换到指定版本的nodejs

nvm current 显示当前使用的nodejs版本

nvm ls 查看本机上已经通过nvm安装的额nodejs版本列表

nvm ls-remote 查看服务器上可用的、可被安装的nodejs版本列表

nvm cache dir 展示nvm的缓存目录

nvm cache clear 清除nvm缓存

nvm alias default version 使用指定版本的node作为默认版本