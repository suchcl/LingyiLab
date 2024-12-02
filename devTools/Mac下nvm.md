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

nvm alias 别名 version 设置某个别名，并指定node版本

```bash
nvm alias dd v10.16.0 设置一个别名dd，并为其指定一个node版本10.16.0
```

nvm alias default version 使用指定版本的node作为默认版本

nvm unalias 别名 删除别名

### nvm unalias 别名

一般情况下，我们使用nvm ls查看已经安装的node列表的时候，会列出已经安装的node列表，也会通过nvm alias 版本的方式制定新的别名，有的时候，我们不想要这个别名了，想把它删除掉，那么就可以通过nvm unalias 别名的方式。


```bash
nvm ls
v10.16.0
       v12.16.2
       v14.18.0
->     v18.18.0
dd -> v10.16.0
default -> stable (-> v18.18.0)
node -> stable (-> v18.18.0) (default)
stable -> 18.18 (-> v18.18.0) (default)
iojs -> N/A (default)
lts/* -> lts/jod (-> N/A)
lts/argon -> v4.9.1 (-> N/A)
lts/boron -> v6.17.1 (-> N/A)
lts/carbon -> v8.17.0 (-> N/A)
lts/dubnium -> v10.24.1 (-> N/A)
lts/erbium -> v12.22.12 (-> N/A)
lts/fermium -> v14.21.3 (-> N/A)
lts/gallium -> v16.20.2 (-> N/A)
lts/hydrogen -> v18.20.5 (-> N/A)
lts/iron -> v20.18.1 (-> N/A)
lts/jod -> v22.11.0 (-> N/A)
```
如通过nvm ls查看当前的一些node版本列表，其中有一个dd -> v10.16.0这么一项，这项对我们来说没有实际价值或者是某个错误操作出来的结果，那么我们想删除它，怎么删除呢?这个时候就可以通过nvm unalias 别名的方式删除掉该项

```bash
nvm unalias dd
Deleted alias dd - restore it with `nvm alias "dd" "v10.16.0"`
```

这样就已经删除了dd这项不希望出现的项。