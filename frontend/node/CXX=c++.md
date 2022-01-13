### MacOS使用nvm安装nodejs，报错：clang: error: no such file or directory: 'CXX=c++'

系统环境：MacOS M1

安装好了nvm后，通过nvm安装指定版本的nodejs，报错了：

```bash
clang: error: no such file or directory: 'CXX=c++'
```

主要的报错信息就是这个。

**解决方案**

在终端中输入：

```bash
arch -x86_64 zsh
```

然后再通过nvm安装指定版本的nodejs就可以了。

```bash
xxx ~ % arch -x86_64 zsh
xxx ~ % nvm install v14.18.0                                   
Downloading and installing node v14.18.0...
Downloading https://nodejs.org/dist/v14.18.0/node-v14.18.0-darwin-x64.tar.gz...
################################################################################################################################################################################################### 100.0%
Computing checksum with shasum -a 256
Checksums matched!
nvm is not compatible with the npm config "prefix" option: currently set to "/Users/a58/Documents/nodejs/node_global"
Run `npm config delete prefix` or `nvm use --delete-prefix v14.18.0` to unset it.
```

已经通过nvm成功的安装了指定版本的nodejs