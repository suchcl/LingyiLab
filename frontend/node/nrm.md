### 1. nrm简单认识

nrm是一个js模块，一个可以通过命令行来切换npm镜像源的命令行工具。

```bash
# nrm安装----全局安装
npm install nrm -g

# 查看可选的nrm镜像源
nrm ls

# 切换npm镜像源
nrm use cnpm # 切换为使用cnpm镜像源

# 添加npm源
nrm add taobao https://registry.npmmirror.com  # 增加一个名为taobao源为https://registry.npmmirror.com的镜像

# 移除镜像源
nrm del taobao # del指令只能删除自定义的镜像源，如果是nrm内置的，则不能删除
```

### 2. 常用指令

```bash
nrm add 源的名字 源的地址  # 添加一个镜像源
nrm del 源的名字 # 移除镜像源，但是不能移除npm内置的镜像源
nrm test
```

### 3. cgr,一个类似nrm的yarn的源管理工具

nrm是一个很优秀的源管理工具，但是不足的是它只能管理npm的源，不能给yarn带来帮助。

有一个类似nrm的管理镜像源的工具cgr，现在可以管理npm、cnpm和yarn。

参考文档：https://github.com/daysai/cgr/

常用指令：

```bash
cgr ls # 查看常用源列表
cgr use 源的名字 # 切换到新的源
cgr add 源的名字 源的地址  # 添加新的源
cgr del 源的名字 # 删除自定义源
cgr help # 帮助
```

> npm和yarn都有自己的源，通过cgr来管理源的时候，会把npm、cnpm和yarn的源都进行切换。如果切换到3个工具都有的源，则会同步，省心省事了，但是大多数的情况下，是不一样的，那么我们在使用不同工具的时候，就需要先确认下源
推荐使用yarn吧

**通过cgr管理的yarn的源的文件地址**

通过cgr管理yarn的源后，cgr默认也是携带了一些源的，查找方法：

```bash
# 先通过yarn global查找到yarn的全局根目录 --- 前提是cgr是通过yarn安装的，如果是通过npm全局安装的cgr那么就需要在npm的目录中去找
yarn global dir 
/Users/xxxxx/.config/yarn/global

# 从yarn的node_modules中找cgr，并进入
cd node_modules/cgr

# 然后在cgr目录中找到registries.json文件，cgr默认携带的源列表就在这里
```

**我的cgr默认携带了下面几个源：**

```json
{
    "npm":{
        "home":"https://www.npmjs.org",
        "registry":"https://registry.npmjs.org/"
    },
    "cnpm":{
        "home":"http://cnpmjs.org",
        "registry":"http://r.cnpmjs.org/"
    },
    "taobao":{
        "home":"https://npmmirror.com",
        "registry":"https://registry.npmmirror.com/"
    },
    "yarn":{
        "home":"https://yarnpkg.com",
        "registry":"https://registry.yarnpkg.com/"
    }
}
```