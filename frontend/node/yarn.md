### yarn

### yarn的安装

我经常是windows和mac切换着使用，所以我总结的文档中有的是用windows下的demo，有的是mac下的demo，不过我一般情况下都写清楚是在哪个环境下，不给读者造成困扰。

正式因为我经常使用windows和mac切换使用，所以我一般安装yarn会使用两种方式：npn和brew的方式。

```bash
# 通过npm的方式安装
npm install yarn -g
# 通过brew的方式安装
brew install yarn
```

安装

```bash
xxx@xxxxxx ~ % npm install yarn -g

> yarn@1.22.17 preinstall /Users/xxx/.nvm/versions/node/v14.12.0/lib/node_modules/yarn
> :; (node ./preinstall.js > /dev/null 2>&1 || true)

/Users/xxx/.nvm/versions/node/v14.12.0/bin/yarn -> /Users/xxx/.nvm/versions/node/v14.12.0/lib/node_modules/yarn/bin/yarn.js
/Users/xxx/.nvm/versions/node/v14.12.0/bin/yarnpkg -> /Users/xxx/.nvm/versions/node/v14.12.0/lib/node_modules/yarn/bin/yarn.js
+ yarn@1.22.17
added 1 package in 3.935s
```

一般看到这些信息，就表示yarn已经成功安装了，但是还是经过常规途径确认一下。

**安装完成后通过yarn --version检查版本的方式确认是否安装成功**

```bash
xxx@xxxxxx ~ % yarn --version
1.22.17
```

到这里就可以放心、大胆的确认，yarn已经被成功的安装了。
### 常用命令

检查/获取当前yarn的bin的位置

yarn global bin

```
PS C:\Users\xxx> yarn global bin
D:\NodeJs\node_global\bin
```

检查当前yarn的全局安装路径

yarn global dir

```
PS C:\Users\xxx> yarn global dir
C:\Users\xxx\AppData\Local\Yarn\Data\global
```

检查yarn安装的包的缓存位置

yarn cache dir

```
PS C:\Users\xxxx> yarn cache dir
C:\Users\xxxx\AppData\Local\Yarn\Cache\v6
```

设置、修改全局安装路径

yarn config set global-foler "path"

```
PS C:\Users\xxx> yarn config set global-folder "E:\nodejs\yarn\global"
yarn config v1.22.5
success Set "global-folder" to "E:\\nodejs\\yarn\\global".
Done in 0.06s.
```

设置、修改缓存目录

yarn config set cache-folder "path"

```
PS C:\Users\xxx> yarn config set cache-folder "E:\nodejs\yarn\cache"
yarn config v1.22.5
success Set "cache-folder" to "E:\\nodejs\\yarn\\cache".
Done in 0.06s.
```

> 我的所有案例都是在 windows 上做的 demo 和验证，不过在非 windows 平台如 linux、mac 上应该是大同小异
