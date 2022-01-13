### 查看提交的用户名和邮箱信息

**查看本地的git显示用户名和密码**

```bash
git config user.name

git config user.email
```

**查看全局的git显示用户名和密码**

方法和本地的查看方式相同，只是需要加上--global指令

```bash
git config --global user.name

git config --global user.email
```


### 配置git提交的用户名和邮箱

配置提交用户名和邮箱，分为全局配置和当前仓库配置


**全局配置**

```bash
git config --global user.name "xxxx"

git config --global user.email "xxxx@xxx.com"
```

这样，默认全局的git提交角的用户名和邮箱都被设置成了xxxx和xxxx@xxx.com，除了设置了当前仓库自己的提交显示名和邮箱


**局部配置**

和全局配置方法一样，不同的是，在配置当前仓库显示用户名和邮箱的时候，首先需要进入到一个git仓库中，然后设置的方式同全局方式配置方式，去掉--global修饰符即可

```bash
git config user.name "xxxx"
git config user.email "xxxx@xxx.com"
```

> 在局部设置git提交显示用户名和邮箱之前，一定要先进入到git仓库，会提示当前不是一个git仓库的信息

```bash
xxxx learning % git config user.name "xxx"
fatal: not in a git directory
```

> 上面的介绍，就是简单介绍了使用最频繁的用户名和邮箱的设置。在实际使用git的过程中，还有其他的一些配置，但是只要是全局的配置，加上--global指令，局部的配置，不需要--global指令，然后再进入到一个git仓库目录中，就可以了。