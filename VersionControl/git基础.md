### 1. git的安装

### 2. git的简单配置

#### 2.1 用户信息配置

用户信息配置，使用最多的是用户名和邮箱配置，可以分为全局配置和本地配置。

用户名和邮箱配置，不同的技术团队会有不同的要求,有些团队可能会使用用户名和邮箱作为团队成员识别的标识。

但是我们可能也会在一些开源的社区贡献自己的一些力量，但是又不想暴露自己的真实信息，就需要对个人的信息做灵活的配置。

**全局配置**

全局配置，指当前电脑机器上所有的git仓库都可以使用的用户信息

```bash
git config --global user.name xxxx # 设置全局的git用户名称为xxx

git config --global user.email xxxx@xx.com  # 设置全局的git用户邮箱为xxxx@xx.com
```

**当前仓库配置**

当前仓库配置，就是配置只针对当前仓库的用户信息，和全局的配置方式一样，去掉--global修饰符就可以了

```bash
git config user.name xxxx # 设置当前仓库的用户名为xxxx

git config user.email xxxx@xx.com  # 设置当前仓库的用户邮箱为xxxx@xx.com
```

#### 2.2 查看用户信息

查看用户信息，和配置信息方式基本一致，不给配置项设置值就是查看操作了

**查看全局的用户信息**

```bash
git config --global user.name # 查看全局的用户信息

git config --global user.email # 查看全局的用户邮箱信息
```

> 注意--global参数的位置不可变，如git config user.name --global是不可以的。对于做前端、经常使用npm的同学需要注意下

**查看当前仓库的用户信息**

和配置用户信息相同，去掉--global参数即可。

```bash
git config user.name  # 查看当前仓库的用户名

git config user.email # 查看当前仓库的用户邮箱
```


### 3. 常用的UI工具

### 4. 常用指令

git fetch

git pull

git 


### 5. 常见问题

1. git fetch和git pull的区别？什么时候使用git fetch，什么时候使用git pull?

2. git stash

3. 完成一次完美的代码提交，需要哪些必须的步骤？

```bash
git add  # 将文件添加到暂存区

git commit -m "注释"  # 将变动文件提交，添加到本地仓库

git push  # 将本地仓库推送到远程服务器端
```

这是几个必须的步骤，但是还有一些其他的操作，日常的操作中也需要注意。

一般情况下，使用了版本控制的项目，都会是多人协作的项目，所以我们在进行commit之前，做一下git pull的拉取操作，拉取最新的代码到本地并进行合并，有了代码冲突从本地开发环境发现、解决，以保证提交干净、整洁的代码到远程的git仓库。