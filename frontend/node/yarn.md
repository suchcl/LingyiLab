### yarn

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

> 我的所有案例都是在windows上做的demo和验证，不过在非windows平台如linux、mac上应该是大同小异